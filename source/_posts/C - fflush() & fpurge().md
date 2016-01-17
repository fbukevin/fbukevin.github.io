title: C - fflush() & fpurge()
date: 2011-11-01 22:26:00
tags: [C/C++]
---

在寫C程式的時候，我們經常會碰到 scanf() 的一些陷阱，很多時候我們必須用函式來清除標準輸入的緩衝區，例如以下的程式碼：  

<pre style="background: #ffffff; color: black;"><span style="color: #004a43;">#</span><span style="color: #004a43;">include</span><span style="color: maroon;"><</span><span style="color: #40015a;">stdio.h</span><span style="color: maroon;">></span>  
<span style="color: #004a43;">#</span><span style="color: #004a43;">include</span><span style="color: maroon;"><</span><span style="color: #40015a;">stdlib.h</span><span style="color: maroon;">></span>  

<span style="color: maroon; font-weight: bold;">int</span> <span style="color: #400000;">main</span><span style="color: #808030;">(</span><span style="color: #808030;">)</span>  
<span style="color: purple;">{</span>  
    <span style="color: maroon; font-weight: bold;">int</span> size <span style="color: #808030;">=</span> <span style="color: #008c00;">0</span><span style="color: purple;">;</span>  
    <span style="color: maroon; font-weight: bold;">int</span> i<span style="color: #808030;">=</span><span style="color: #008c00;">0</span><span style="color: #808030;">,</span>j<span style="color: #808030;">=</span><span style="color: #008c00;">0</span><span style="color: purple;">;</span>  

    <span style="color: maroon; font-weight: bold;">do</span>  
    <span style="color: purple;">{</span>  
       <span style="color: #603000;">printf</span><span style="color: #808030;">(</span><span style="color: maroon;">"</span><span style="color: #0000e6;">Please input rows of triangle, exit please input</span> <span style="color: #0f69ff;">-</span><span style="color: #0000e6;">1</span><span style="color: #0f69ff;">\n</span><span style="color: maroon;">"</span><span style="color: #808030;">)</span><span style="color: purple;">;</span>  
       <span style="color: #603000;">scanf</span><span style="color: #808030;">(</span><span style="color: maroon;">"</span><span style="color: #0f69ff;">%d</span><span style="color: maroon;">"</span><span style="color: #808030;">,</span><span style="color: #808030;">&</span>size<span style="color: #808030;">)</span><span style="color: purple;">;</span>  
    </pre>

[閱讀更多 »](http://veckcode.blogspot.com/2011/11/fflush-fpurge.html#more)