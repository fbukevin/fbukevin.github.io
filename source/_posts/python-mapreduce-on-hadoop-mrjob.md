---
layout: post
title: '[Python] MapReduce on Hadoop - mrjob'
date: 2014-08-04 19:29
comments: true
categories: 
---
* mrjon: https://pythonhosted.org/mrjob/
* 翻譯改寫自：http://mrjob.readthedocs.org/en/latest/guides/quickstart.html#writing-your-first-job

用 Python 來寫 Hadoop 的 MapReduce 程式

* 安裝：`pip install mrjob`

* 一個官網最簡單的 word_count.py 範例：

```
from mrjob.job import MRJob

class MRWordFrequencyCount(MRJob):
    def mapper(self, _, line):
        yield "chars", len(line)
        yield "words", len(line.split())
        yield "lines", 1

    def reducer(self, key, values):
        yield key, sum(values)


if __name__ == '__main__':
    MRWordFrequencyCount.run()
```

* 執行：`python word_count.py input.txt`

```
no configs found; falling back on auto-configuration
no configs found; falling back on auto-configuration
creating tmp directory /var/folders/bz/z8d70ds17y59ggw906xdqrvw0000gn/T/mrjob1.veck.20140804.113920.115769
writing to /var/folders/bz/z8d70ds17y59ggw906xdqrvw0000gn/T/mrjob1.veck.20140804.113920.115769/step-0-mapper_part-00000
Counters from step 1:
  (no counters found)
writing to /var/folders/bz/z8d70ds17y59ggw906xdqrvw0000gn/T/mrjob1.veck.20140804.113920.115769/step-0-mapper-sorted
> sort /var/folders/bz/z8d70ds17y59ggw906xdqrvw0000gn/T/mrjob1.veck.20140804.113920.115769/step-0-mapper_part-00000
writing to /var/folders/bz/z8d70ds17y59ggw906xdqrvw0000gn/T/mrjob1.veck.20140804.113920.115769/step-0-reducer_part-00000
Counters from step 1:
  (no counters found)
Moving /var/folders/bz/z8d70ds17y59ggw906xdqrvw0000gn/T/mrjob1.veck.20140804.113920.115769/step-0-reducer_part-00000 -> /var/folders/bz/z8d70ds17y59ggw906xdqrvw0000gn/T/mrjob1.veck.20140804.113920.115769/output/part-00000
Streaming final output from /var/folders/bz/z8d70ds17y59ggw906xdqrvw0000gn/T/mrjob1.veck.20140804.113920.115769/output
"chars"	21
"lines"	1
"words"	5
removing tmp directory /var/folders/bz/z8d70ds17y59ggw906xdqrvw0000gn/T/mrjob1.veck.20140804.113920.115769
```

其中統計結果：
```
"chars" 21
"lines"	1
"words"	5
```

程式碼中有個 `MRJob`，這個物件的 `class` 定義了你建立的 `job` 的 `steps` 中會用到的方法：`mapper, combiner, reducer`，不一定全部都要有，但每個 step 至少要有三者其中之一，也就是說，你的 job 可以只有一個 mapper、一個 combiner 或一個 reducer

mapper(): 吃一個 key 和一個 value 參數，並且產生許多  key-value pair，就跟原本 Java 的 Mapper 一樣
reducer(): 吃一個 key 和一個 iterable value，也會產生許多 key-value pair，同原本 Java 的 Reducer 

而最後的兩行程式碼，用來驅動我們的 job：
```
if __name__ == '__main__':
    MRWordCounter.run()  # where MRWordCounter is your job class
```

mrjob 預設是將 job 跑在 single python process，這樣比較方便 debug，但這樣不是分散式運算，要切換成其他的執行模式，可以加上 `-r`，共有三種不同模式：`-r local, -r hadoop, -r emr`

1. -r local: 執行在多個子行程上 (虛擬分散式)
2. -r hadoop: 執行在 hadoop 叢集上 (完全分散式)
3. -r emr: 執行在 Elastic MapReduce 上

假如你的 input 檔案存放在 HDFS 或 S3 上(with EMR)：
```
$ python my_job.py -r emr s3://my-inputs/input.txt
$ python my_job.py -r hadoop hdfs://my_home/input.txt
```

假如你有多個 step (通常)在一個 job 中，你可以透過覆寫 `steps()` 方法來定義 steps，建立 `mrjob.step.MRStep` 的 `step list`，例如以下範例：
```
from mrjob.job import MRJob
from mrjob.step import MRStep
import re

WORD_RE = re.compile(r"[\w']+")

class MRMostUsedWord(MRJob):

    # 覆寫 steps()
    def steps(self):
        return [
          # 定義 MRStep 1
          MRStep(mapper=self.mapper_get_words,	# 指定此 step 的 mapper 為 mapper_get_words
                 combiner=self.combiner_count_words,# 指定此 step 的 combiner 為 combiner_count_words
                 reducer=self.reducer_count_words), # 指定此 step 的 reducer 為 reducer_count_words
          # 定義 MRStep 2
          MRStep(reducer=self.reducer_find_max_word)
        ]

    def mapper_get_words(self, _, line):
        # yield each word in the line
        for word in WORD_RE.findall(line):
            yield (word.lower(), 1)

    def combiner_count_words(self, word, counts):
        # optimization: sum the words we've seen so far
        yield (word, sum(counts))

    def reducer_count_words(self, word, counts):
        # send all (num_occurrences, word) pairs to the same reducer.
        # num_occurrences is so we can easily use Python's max() function.
        yield None, (sum(counts), word)

    # discard the key; it is just None
    def reducer_find_max_word(self, _, word_count_pairs):
        # each item of word_count_pairs is (count, word),
        # so yielding one results in key=counts, value=word
        yield max(word_count_pairs)


if __name__ == '__main__':
    MRMostUsedWord.run()
```