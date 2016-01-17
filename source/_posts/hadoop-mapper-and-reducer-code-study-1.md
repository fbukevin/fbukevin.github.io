---
layout: post
title: 'Hadoop Code Study - Mapper and Reducer Class Type'
date: 2014-09-08 14:24
comments: true
categories: 
---
以 Mapper 來說
===
``` 
 public class TokenCounterMapper 
     extends Mapper<Object, Text, Text, IntWritable>{
    
   private final static IntWritable one = new IntWritable(1);
   private Text word = new Text();
   
   public void map(Object key, Text value, Context context) throws IOException, InterruptedException {
     StringTokenizer itr = new StringTokenizer(value.toString());
     while (itr.hasMoreTokens()) {
       word.set(itr.nextToken());
       context.write(word, one);
     }
   }
 }
```
<!--more--> 
 `<Obejct, Text, Text, IntWritable>` 分別對應到 KEYIN, VALUEIN, KEYOUT, VALUEOUT
而在 mapper 函數中使用到的部份：
* public void map(Object key, Text value, Context context) 的頭兩個參數就是符合 KEYIN 和 VALUEIN 的部分
* context.write(word, one) 的 word 和 one 就分別對應到 KEYOUT 和 VALUEOUT

 

以 Reducer 來說
===
```
 public class IntSumReducer<Key> extends Reducer<Key,IntWritable, Key,IntWritable>{
	 private IntWritable result = new IntWritable();
   public void reduce(Key key, Iterable<IntWritable> values, Context context) throws IOException, InterruptedException {
     int sum = 0;
     for (IntWritable val : values) {
       sum += val.get();
     }
     result.set(sum);
     context.write(key, result);
   }
 }
``` 
`<Key, IntWritable, Key, IntWritable>` 分別對應到 KEYIN, VALUEIN, KEYOUT, VALUEOUT
而在 reduce 函數中使用到的部份：
* public void reduce(Key key, Interable<IntWritable> values, Context context) 的頭兩個參數就是符合 KEYIN 和 VALUEIN 的部分
* context.write(key, result) 的 key 和 result 就分別對應到 KEYOUT 和 VALUEOUT



Reference:
1. [MapReduce：并行计算框架](http://blog.csdn.net/jerome_s/article/details/26213099)
2. [Hadoop入门实践之类型与格式](http://blog.csdn.net/workformywork/article/details/14127823)