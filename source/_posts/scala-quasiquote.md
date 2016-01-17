---
layout: post
title: '[Scala] Quasiquote'
date: 2014-11-04 20:19
comments: true
categories: 
---
String with Interpreter
===
```
scala> import scala.math.Pi
scala> Tau = 2 * Pi
scala> println(s"Happy $Tau Day")
     Happy 6.283185307179586 Day
scala> println("Happy $Tau Day")
     Happy $Tau Day
scala> val s1 = "$Tau"
     s1: String = $Tau
scala> val s2 = s"$Tau"
     s2: String = 6.283185307179586
```
<!--more-->
所以 string 加上 s 是指要以 string interpreter 來處理這個字串

String in Quasiquote
===
而 string 前面加上 q 是 quasiquote，編譯器會自動將這個 string 變成一棵 tree
Quasiquote 是 Scala 2.11 以後的巨集工具，但預設不會載入模組
所以直接宣告 `q"..."` 會出現 `value q is not a member of StringContext` 的錯誤
解決方法：http://docs.scala-lang.org/overviews/quasiquotes/setup.html

在 Scala 2.11, in REPL，要先做些前置：
```
scala> val universe: reflect.runtime.universe.type = reflect.runtime.universe
scala> import universe._
```
接著就可以用了：
```
scala> val tree = q"i am { a quasiquote }"
tree: universe.Tree = i.am(a.quasiquote)

scala> println(tree match { case q"i am { a quasiquote }" => "it worked!" })
it worked!
```

在 IntelliJ 中，則要在檔案中引用：`import reflect.runtime.universe._` 就可以了
![螢幕快照 2014-11-04 上午3.46.12.png](http://user-image.logdown.io/user/3330/blog/3407/post/241235/C1HxnqzjRAKuxgHVNTr3_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-11-04%20%E4%B8%8A%E5%8D%883.46.12.png)


