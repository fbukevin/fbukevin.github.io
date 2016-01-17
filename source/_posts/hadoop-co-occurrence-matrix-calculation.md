---
layout: post
title: '以 Hadoop 計算共現矩陣'
date: 2014-09-08 12:16
comments: true
categories: 
---
翻譯自原文：http://codingjunkie.net/cooccurrence/

本文是《Data-Intensive Text Processing with MapReduce》提到的 MapReduce 演算法的系列文章的延續。這次我們會使用語料庫建立一個單字共現矩陣。
<!--more-->
所謂共現矩陣可以看成是對某件特定事件的追蹤，並給予一段時間或空間窗口(windows，就像作業系統中的排程那樣)，然後記錄還有其他哪些事件也發生了。本文中，我們的『事件(events)』都是文本中個別的『詞(words)』，而我們要追蹤看看(對於某個目標詞)其他哪些詞也在我們設定的窗口條件中出現，我們設定的窗口條件是相對於目標詞彙的位置，例如來看這句話：『The quick brown fox jumped over the lazy dog』，窗口值設為 2，則『jumped』的共現詞是『brown, fox, over, the』。

一個共現矩陣可以應用在很多其他需要找出『當某個事件發生，其他事件似乎也會同時發生』的領域，為了要建構我們的文本共現矩陣，我們需要實作 《Data-Intensive Test Processing with MapReduce》 第三章的 Pairs 和 Stripes 演算法，配合 MapReduce。本文用來建立我們的共現矩陣的文本資料來自於古騰保計畫的[William Shakespear](http://www.gutenberg.org/ebooks/100)。

Pairs 演算法
===

實作 pairs 演算法很簡單。當每次 map 函數被呼叫時傳入一行，便按照空白把傳入的行切割成字串陣列。接著是建立兩層迴圈。外層迴圈迭代陣列中的每個詞，内層迴圈走訪目前這個詞的相鄰詞。内層迴圈的迭代次數取決於需要捕捉的目前詞彙的相鄰距離。在内層迴圈的每次迭代的結束前，我們輸出一個 WordPair 物件（由兩個詞組成，目前的詞在左邊，相鄰詞在右邊）當做 key，這組詞的出現頻率 (one 的次數)當做 value。

以下是 pairs 演算法的程式碼：
```
public class PairsOccurrenceMapper extends Mapper<LongWritable, Text, WordPair, IntWritable> {
    private WordPair wordPair = new WordPair();
    private IntWritable ONE = new IntWritable(1);

    @Override
    protected void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
        int neighbors = context.getConfiguration().getInt("neighbors", 2);
        String[] tokens = value.toString().split("\\s+");
        if (tokens.length > 1) {
          for (int i = 0; i < tokens.length; i++) {
              wordPair.setWord(tokens[i]);

             int start = (i - neighbors < 0) ? 0 : i - neighbors;
             int end = (i + neighbors >= tokens.length) ? tokens.length - 1 : i + neighbors;
              for (int j = start; j <= end; j++) {
                  if (j == i) continue;
                   wordPair.setNeighbor(tokens[j]);
                   context.write(wordPair, ONE);
              }
          }
      }
  }
}
```
Pairs 演算法中的 Reducer 只是單純的將當做 key 的同一 WordPair 的計數總和：
```
public class PairsReducer extends Reducer<WordPair,IntWritable,WordPair,IntWritable> {
    private IntWritable totalCount = new IntWritable();
    @Override
    protected void reduce(WordPair key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
        int count = 0;
        for (IntWritable value : values) {
             count += value.get();
        }
        totalCount.set(count);
        context.write(key,totalCount);
    }
}
```

Stripes算法
===

共現矩陣中的 stripes 演算法實踐一樣很簡單。不過跟 pairs 演算法不同的是，每個詞的所有相鄰詞被存在一個 hashmap 中，以此相鄰詞 key，詞的出現頻率為 value。當迴圈走訪完每個詞的所有相鄰詞後，這個詞和跟他有關的 hashmap 會被輸出。
以下是 stripes 演算法的程式碼：
```
public class StripesOccurrenceMapper extends Mapper<LongWritable,Text,Text,MapWritable> {
  private MapWritable occurrenceMap = new MapWritable();
  private Text word = new Text();

  @Override
 protected void map(LongWritable key, Text value, Context context) throws IOException, InterruptedException {
   int neighbors = context.getConfiguration().getInt("neighbors", 2);
   String[] tokens = value.toString().split("\\s+");
   if (tokens.length > 1) {
      for (int i = 0; i < tokens.length; i++) {
          word.set(tokens[i]);
          occurrenceMap.clear();

          int start = (i - neighbors < 0) ? 0 : i - neighbors;
          int end = (i + neighbors >= tokens.length) ? tokens.length - 1 : i + neighbors;
           for (int j = start; j <= end; j++) {
                if (j == i) continue;
                Text neighbor = new Text(tokens[j]);
                if(occurrenceMap.containsKey(neighbor)){
                   IntWritable count = (IntWritable)occurrenceMap.get(neighbor);
                   count.set(count.get()+1);
                }else{
                   occurrenceMap.put(neighbor,new IntWritable(1));
                }
           }
          context.write(word,occurrenceMap);
     }
   }
  }
}
```

Stripe 演算法的 Reducer 有點複雜，因為我們需要迭代過一整個 map 集合，然後對每個 map，再迭代過所有它的 value：
```
public class StripesReducer extends Reducer<Text, MapWritable, Text, MapWritable> {
    private MapWritable incrementingMap = new MapWritable();

    @Override
    protected void reduce(Text key, Iterable<MapWritable> values, Context context) throws IOException, InterruptedException {
        incrementingMap.clear();
        for (MapWritable value : values) {
            addAll(value);
        }
        context.write(key, incrementingMap);
    }

    private void addAll(MapWritable mapWritable) {
        Set<Writable> keys = mapWritable.keySet();
        for (Writable key : keys) {
            IntWritable fromCount = (IntWritable) mapWritable.get(key);
            if (incrementingMap.containsKey(key)) {
                IntWritable count = (IntWritable) incrementingMap.get(key);
                count.set(count.get() + fromCount.get());
            } else {
                incrementingMap.put(key, fromCount);
            }
        }
    }
}
```

結論
===

比較這兩種演算法，看得出來相較於 Stripes 演算法，Pairs 算法會產生生更多的 key-value pair。而且 Pairs 算法捕捉到的是單一的共現事件，而 Stripes 演算法能夠捕捉到所有的共現事件。Pairs 演算法和 Stripes 演算法的實踐都非常適合使用Combiner。因為這兩種演算法實作產生的結果都是可交换(commutative)與可結合(associative) [*1]，所以我們可以輕易地重用 reducer 作為 Combiner。如前所述，共現矩矩陣不只能應用於文本處理，而且會是 MapReduce 演算法上一個有用的武器。謝謝你的閱讀。

註1: 可使用combiner 的資料必須能夠滿足交換律與結合律
註2: Pairs 和 Stripes 分別是兩種不同的共現矩陣演算法

參考資料
===

* 《Data-Intensive Processing with MapReduce》 by Jimmy Lin and Chris Dyer
* Hadoop: The Definitive Guide by Tom White
* Source Code and Tests from blog
* Hadoop API
* MRUnit: 用來測試 Apache Hadoop mapreduce
* A GitHub Repository: [hadoop-algorithm](https://github.com/bbejeck/hadoop-algorithms/tree/master/src/bbejeck/mapred/coocurrance)
* 我整合好的另一個專案：https://github.com/fbukevin/hadoop-cooccurrence
* 改寫 MapWritable：http://blog.csdn.net/jiyuanyi1992/article/details/37739413
