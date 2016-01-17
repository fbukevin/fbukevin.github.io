title: Python/C API On Linux Mint 
date: 2013-11-01 19:30:00
tags: [C/C++,Python]
---

今天第一次嘗試使用 Python/C API  

但是花了點時間處理 GCC 編譯器引入 Python.h 的問題  
-----------------------------------------------------------------------------------  

Python/C 是 Python 作為黏合語言的一個重點，要用 C 呼叫 Python 的模組，或是在 C 中使用 Python 語法，基本上需要透過這個 API ，其中有一個主要的 Header 叫做 Python.h，需要在其他標頭檔之前引入，接著就可以呼叫這個標頭檔中定義一些與 Python 有關的 C 函式了  

我實驗的平台是 Linux Mint x86_64 3.8.0-19-generic 、Python 2.7.4、GCC 4.7.3  

[閱讀更多 »](http://veckcode.blogspot.com/2013/11/python-pythonc-api-on-linux-mint.html#more)