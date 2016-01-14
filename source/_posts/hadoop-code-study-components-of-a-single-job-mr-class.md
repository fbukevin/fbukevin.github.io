---
layout: post
title: 'Hadoop Code Study - Components of a Single Job MR Class'
date: 2014-09-08 14:49
comments: true
categories: 
---
Import Commonly(from v0.20.2)
===
```
import java.io.*;
import java.util.*;

import org.apache.hadoop.fs.Path;
import org.apache.hadoop.conf.*;
import org.apache.hadoop.io.*;
import org.apache.hadoop.mapreduce.*;			//it's "mapred" before
import org.apache.hadoop.util.*;
```

Methods Defined
===
```
class MR_JOB_NAME implements Tool{
	public static class Map extends Mapper<KEYIN_TYPE, VALUEIN_TYPE, KEYOUT_TYPE, VALUEOUT_TYPE>{}
  public static class Reduce extends Reducer<KEYIN_TYPE, VALUEIN_TYPE, KEYOUT_TYPE, VALUEOUT_TYPE>{}
  public int run(String[] args) throws Exeption{}
  public static void main(String[] args) throws Exxception{}
}
```

其中 Mapper Class 中會定義：
public void map(KEYIN_VAR, VALUEIN_VAR, Context context) throws IOException, InterrupedException{ ... }

Reduce Class 中會定義：

run() 中去用 Job 來設定一些參數，如果有多個 job 的 MR Class，這裡會定義執行的 Jobs 先後順序

main() 使用 ToolRunner 的 run() 方法來驅動 run()，其中 ToolRunner.run(new MR_JOB_NAME(), args) 可以得知，這個 run() 方法應該不是上方定義的 run() 方法，而是會建立一個 MR_JOB_NAME 物件，並利用該物件和所給予的參數 args 去呼叫上方定義的 run() 來執行 MapRuduce

* Hadoop 採用 Writable 的資料型態是因為它將資料 Serialize 
* Context 是用來給 MapReduce Process 間溝通用的資料型態