---
layout: post
title: '[Python] Generator'
date: 2014-08-03 20:00
comments: true
categories: 
---

`generator function` 是在一個 function 中使用了 `yield` 這個關鍵字來回傳函數結果
但與一般 function 不同的在於，yield 回傳以後，不會就結束 function，而是暫停函數的處理狀態
直到你呼叫 .next() 這個 function，就會再次執行 function

```
yield = return + pause
```
例如我們可以這樣用：
```
def foo(n):
	for i in range(1, n):
		yield i
```

我們可以這樣用這個 function:
```
y = foo(10)
y.next()
```
此時，會回傳 1，接著我們可以再 `y.next()` 一次，會得到 2，一直到 y.next() 回傳 10 以後，function 才算結束執行

這種用法可以用來優化 `iterable function`
以下方程式碼來說，要取得小於 n 的所有數列
我們建立了一個 list 來存放結果，並且逐一將符合小於 n 的數加入到 list 中
最後才一次回傳這個 list
```
# Build and return a list
def firstn(n):
    num, nums = 0, []
    while num < n:
        nums.append(num)
        num += 1
    return nums

def mysum(iterable_object):
		sum = 0
		for i in iterable_object:
  		sum += i
   	return sum

sum_of_first_n = mysum(firstn(1000000))
```
這樣的運作方式需要把一整個 list 存在記憶體中
如果項目太多，會導致記憶體浪費(太多被佔用的空間無法釋放給其他行程使用)或是所需記憶體不足的情況

generator 讓我們可以的 function 可以不用一次取得所有的 list 來累加
而可以取得一個就加一次
```
# a generator that yields items instead of returning a list
def firstn(n):
    num = 0
    while num < n:
        yield num
        num += 1

def mysum(iterable_object):
	sum = 0
	for i in iterable_object:			# 每次執行至此，就會 yield 一個新值
		sum += i
	return sum

sum_of_first_n = mysum(firstn(1000000))
```

