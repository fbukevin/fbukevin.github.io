---
layout: post
title: '[Julia] 集大成的科學計算新星'
date: 2015-05-24 19:14
comments: true
categories: [Matlab, r, data, julia]
---
最近在調查比較想學習的資料處理語言
我的需求是要開源如 R、簡潔如 Python
剛好我在非資訊領域做科學分析的朋友說 Matlab 很容易寫(他以建構矩陣為例子)
找來找去，大概就是 `Julia` 了

[http://julialang.org/](http://julialang.org/)
![j.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/277068/BWSV4K8nR3GfIs3nZUVK_j.JPG)

這個語言野心極大，標榜結合了像 Python/Matlab/R 的易用和彈性，又兼具 Fortran 或是 C 的執行速度，能無縫銜接現有的 C/Fortran/python/R 所累積的龐大函式庫，又可以支援平行運算，並具有處理資料表格(data frame)的能力。

這麼剛好符合我要的需求 XD

它的創作者是一群用 Matlab 出身的 MIT guys，很有感啊！

# Julia REPL 執行畫面
![Julia_REPL.png](http://user-image.logdown.io/user/3330/blog/3407/post/277068/F1C7gItXRRaDsXdek81k_Julia_REPL.png)


不過資料還很少，中文也是

以下是一些我覺得蠻喜歡的特性

# 變數預設採用 Unicode

![var_name1.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/277068/KanvGy1ESfS24KOisHww_var_name1.JPG)

![var_name2.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/277068/4V4nytUTg2XDHC2ktdU6_var_name2.JPG)

這讓我想到了[易語言](http://www.dywt.com.cn/)和[周蟒](https://code.google.com/p/zhpy/wiki/AboutZhpy)...

# 新舊定義 function 的方式
1. traditional
```
julia> function f(x,y)
       x + y, x-y
       end
f (generic function with 1 method)
julia> f(2,4)
(6,-2)
```
2. Functional 
```
julia> ∑(x,y) = x + y
∑ (generic function with 1 method)
julia> ∑(2,3)
5
( ∑ in OS X is “option + w")
```

# 有三種使用 function 的方式
1. genaral
`julia> f(2,3)`

2. apply()
`julia> apply(f, 2, 3)`

3. special operator syntax for certain function name
(waiting)

# function 回傳多個值的方法

![回傳多個值.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/277068/57QaF83WSdyjVPhjxIlO_%E5%9B%9E%E5%82%B3%E5%A4%9A%E5%80%8B%E5%80%BC.JPG)

![回傳多個值2.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/277068/TzpNTAsSAS9Q2T0Wwh81_%E5%9B%9E%E5%82%B3%E5%A4%9A%E5%80%8B%E5%80%BC2.JPG)

hkl31 大的 iThome 2014 鐵人邦幫忙系列文章：
[Julia(1) - Why Julia?](http://ithelp.ithome.com.tw/question/10157446)
[Julia (2) -- 2048遊戲的架構，Julia的安裝和暖身](http://ithelp.ithome.com.tw/question/10157714)
[Julia (3) -- 2048遊戲實作開始](http://ithelp.ithome.com.tw/question/10157888)
[Julia(4) - 2048遊戲核心完成!](http://ithelp.ithome.com.tw/question/10158099)
[Julia (5) -- Julia的標準輸出](http://ithelp.ithome.com.tw/question/10158208)
[Julia (6) -- Julia的標準輸入，2048主程式迴圈](http://ithelp.ithome.com.tw/question/10158466)
(其餘文章請參考作者 [iThome 活動列表](http://ithelp.ithome.com.tw/profile/share?id=20091968&page=1))


Julia for Matlab User 系列文章：
[http://sveme.org/julia-for-matlab-users-i.html](http://sveme.org/julia-for-matlab-users-i.html)
[http://sveme.org/julia-for-matlab-users-ii.html](http://sveme.org/julia-for-matlab-users-ii.html)
[http://sveme.org/julia-for-matlab-users-iii.html](http://sveme.org/julia-for-matlab-users-iii.html)

Reference：
[http://juliatw.readthedocs.org/zh_TW/latest/](http://juliatw.readthedocs.org/zh_TW/latest/)
[Learn Julia in Y minutes](http://learnxinyminutes.com/docs/julia/)