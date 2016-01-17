---
layout: post
title: '[Julia] UTF-8 字串存取'
date: 2015-05-25 15:51
comments: true
categories: [julia]
---
我現在有個需求，要讀取目錄下所有的檔案列表，然後拷貝檔名的部分就好，不要副檔名
可以直接這樣：`f = readdir()`，如此會回傳一個 `Array{Union(ASCIIString,UTF8String),1}`
接著我們可以存取陣列來取的特定檔案名稱：
<!--more-->
```shell
julia> println(f[1])
julia> f[1]
"likea玉儿躁郁症病患.csv"
``` 

注意！ index 從 1 開始喔! 這是承襲 Matlab 和 R 的，應該是比較符合科學家邏輯吧！從0開始是電腦的角度
這裡有一篇關於 Julia 從 1 開始的討論：
[https://groups.google.com/forum/?hl=en#!topic/julia-dev/tNN72FnYbYQ](https://groups.google.com/forum/?hl=en#!topic/julia-dev/tNN72FnYbYQ)

為了實現我的主題，我先拷貝到一個字串中，並且我試著去存取指定的幾個中文字元
```shell
julia> s = f[1]		# => "likea玉儿躁郁症病患.csv"
julia> println(s[6])	# => 玉
julia> println(s[7])	# => error
```

Ooop！當你試圖存取 `s[7]` (看起來應當是 `儿`)時，會出現以下錯誤：
```
ERROR: ArgumentError: invalid UTF-8 character index
 in next at ./utf8.jl:80
 in getindex at string.jl:62
```

根據[官網文件](http://julia.readthedocs.org/en/latest/manual/strings/#unicode-and-utf-8)的說明：
```
UTF-8 is a variable-width encoding, meaning that not all characters are encoded in the same number of 
bytes. In UTF-8, ASCII characters — i.e. those with code points less than 0x80 (128) — are encoded as 
they are in ASCII, using a single byte, while code points 0x80 and above are encoded using multiple 
bytes — up to four per character. This means that not every byte index into a UTF-8 string is necessarily
a valid index for a character.
```
簡單來說，是因為 UTF-8 的每個字符編碼長度不同造成的，也就是說 `玉` 和 `儿` 雖然同樣都是 UTF-8，但是兩者的編碼長度不同，`玉` 可能只占用 byte 6，但 `儿` 可能占用 byte 7-9 (假設)，換句話說，length(s) 在 Julia 中是你所能看到的『字串長度』，但是實際上字串的『編碼總長(記憶體空間)』是 endof(s) 的值，以下馬上來實驗看看:
```shell
julia> println("length of s is " , length(s))
julia> length of s is 16
julia> println("end index of s is ", endof(s))
julia> end index of s is 30
```
解決辦法：我們可以透過 nextind(str, i) 這個函數來取得下一個合法的字串索引，下面我們用 for 迴圈來查看 s 這個字串所有 [1] 之後的合法索引
```shell
julia> for i = 1:endof(s)
	       println(nextind(s, i))
       end
2 	  
3 
4 
5 
6 
9 
12 
15 
18 
21 
24 
27 
28 
29 
30 
31 # (刪除重複後) 
```

Hoho! 出現啦！
剛剛 s[6] 是合法的，所以我們印得出 `玉`，可以看到下一個合法的索引是 9 不是 7
馬上印印看：`println(s[9])`
![擷取.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/277334/5o2iKvNFSlCBz5yMFSGs_%E6%93%B7%E5%8F%96.JPG)

YA~! 
接下來我們可以用 `for i = i:endof(s)` 或 `for c in s` 來進行字串拷貝了~
