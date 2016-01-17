---
layout: post
title: '[Scheme] Quote, Quasiquote, Unquote'
date: 2014-10-20 21:22
comments: true
categories: 
---
最早是從 LISP 的 quote( ' ), quasiquote( \` ), unquote( , ) 演變而來
quote 的意思是避免 expression 被 evaluate (求值)
例如原本寫 `(+ 1 2)` 會得到 3，因為直譯器會將 + 當成 function (事實上是將 +, 1, 2 都當成函數去求值) 
如果寫成 `'(+ 1 2)` 會得到 `(+ 1 2)`，也就是這個敘述變成了 symbol
更進一步說：
```
'1		 => 1		 ;本來就是符號
'a		=> a			;a 變成符號，不會當成變數求值
'"hi"	=> "hi"		;"" 和 hi 變成符號，不會被求值為字串
```
<!--more-->
然後下面兩個一起說：
```
'(1 2 3) => (1 2 3)	
'(+ 1 2) => (+ 1 2)
```
事實上，`'(1 2 3)` 的概念是 `(list '1 (list '2 (list '3))`，`'(+ 1 2)` 則是 `(list '+ (list '1 (list '2)))`
但是有時候，我們並不想針對整個敘述都當成 list symbol，例如 `'(1 2 (+ 3 4))` 會得到 `(1 2 (+ 3 4))`
假如我們希望保留 1 和 2，然後運算 (+ 3 4)，就可以利用『 \` 』取代『 ' 』，這個符號允許我們設定 quote 的運算中止點，用『 , 』指定之
例如：
```
`(1 2 ,(+ 3 4))    => '(1 2 7)
```
就是指定 (+ 3 4) 以後就不是 quote 運算，但後面運算完以後的結果，還是會變成 quote 的元素之一，因此 (1 2 7) 仍是一個 quote 運算產生的 symbol

Reference: http://courses.cs.washington.edu/courses/cse341/04wi/lectures/14-scheme-quote.html