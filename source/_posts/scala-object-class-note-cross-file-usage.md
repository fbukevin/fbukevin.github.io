---
layout: post
title: '[Scala] Object Class Note: Cross Files Usage'
date: 2014-11-04 18:52
comments: true
categories: 
---
object class 不能夠跨檔案 new，可能原因是 object 是 singleton, 這意味這整個專案就只能有一份 instance (?):
ex. 
	File A：`object SampleClass{ ... }`
  File B：`val sample = new SampleClass()`	=> error: cannot resolve symbol SampleClass
 <!--more-->
但是可以直接存取使用：
ex.
	File A：`object SampleClass { def foo() = { ... } )`
  File B：`val sample = SampleClass.foo()`	=> passed!

如果使用 object class 來建立兩個物件：
```
val sample1 = SampleClass.foo()
val sample2 = SampleClass.foo()
print(sample1 == sample2)		=> false
```
所以兩個實例是獨立的兩個物件

但是如果想要這樣：
```
val sample1 = SampleClass
val sample2 = SampleClass
print(sample1 == sample2)		=> true
sample1.foo()
sample2.foo()
```
因為是直接指定 object 物件給新的變數，所以兩個指向的記憶體位置是相同的，因此比較結果是 true