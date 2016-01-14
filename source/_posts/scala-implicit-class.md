---
layout: post
title: '[Scala] Implicit Class'
date: 2014-11-05 01:29
comments: true
categories: 
---
簡單來說，加上 `implicit` 關鍵字的 class，在有效範圍內(scope)內，會自動建立一個 implicit primary constructor，拿[官方文件](http://docs.scala-lang.org/overviews/core/implicit-classes.html)的例子加以說明(為了方便對照區塊，排版做的調整)：
```
object Helpers 
{
  implicit class IntWithTimes(x: Int) 
  {
    def times[A](f: => A): Unit = 
    {
    
      def loop(current: Int): Unit =	// 定義一個迴圈函數
        if(current > 0) 
        {
          f
          loop(current - 1)
        }
        
      loop(x)	// 呼叫迴圈函數
    }
  }
}
```
把宣告為 implicit 的部份抽出來：
```
implicit class IntWithTimes(x: Int){
	...
}
```
這一段在編譯後會自動轉換成：
```
class IntWithTimes(x: Int){
	...
}
implicit final def IntWithTimes(x: Int): IntWithTimes = new IntWithTimes(x)
```
其中最下面多的那一個 function 呼叫後會回傳一個同 Class 名稱的物件實例，也就是這個類別的 primary constructor，因為我們把這個 implicit class 宣告在 object class 內，所以我們可以直接 import 這個 class 並直接使用這個 implicit class 的方法：
```
scala> import Helpers._
import Helpers._
scala> 5 times println("HI")
HI
HI
HI
HI
HI
```

References:
[1] http://docs.scala-lang.org/overviews/core/implicit-classes.html
[2] http://stackoverflow.com/questions/11931623/how-to-use-scala-2-10-implicit-classes