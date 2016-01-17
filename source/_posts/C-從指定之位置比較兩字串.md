title: C 從指定之位置比較兩字串
date: 2012-06-21 14:02:00
tags: [C/C++]
---

  

<pre style="background: #ffffff; color: black;"><span style="color: dimgrey;">/*</span>  
<span style="color: dimgrey;"> * Program: Complement header file of string compare</span>   
<span style="color: dimgrey;"> * Language:GNU C/ ANSI C</span>  
<span style="color: dimgrey;"> * Author:  Veck Hsiao @ Taiwan, National Chung Cheng University</span>  
<span style="color: dimgrey;"> * Time:    June/21/2012</span>   
<span style="color: dimgrey;"> * Usage:   Compare string 1 with string 2 start from assigned index</span>  
<span style="color: dimgrey;"> * Result:  If matched, return 0, otherwise, return -1</span>  
<span style="color: dimgrey;"> */</span>  

<span style="color: #004a43;">#</span><span style="color: #004a43;">include</span><span style="color: maroon;"><</span><span style="color: #40015a;">stdio.h</span><span style="color: maroon;">></span> <span style="color: #004a43;"></span>   
<span style="color: #004a43;">#</span><span style="color: #004a43;">include</span><span style="color: maroon;"><</span><span style="color: #40015a;">stdlib.h</span><span style="color: maroon;">></span>  
<span style="color: #004a43;">#</span><span style="color: #004a43;">include</span><span style="color: maroon;"><</span><span style="color: #40015a;">string.h</span><span style="color: maroon;">></span>  

<span style="color: maroon; font-weight: bold;">int</span> strmidcmp<span style="color: #808030;">(</span><span style="color: maroon; font-weight: bold;">const</span> <span style="color: maroon; font-weight: bold;">char</span> <span style="color: #808030;">*</span>str1<span style="color: #808030;">,</span> <span style="color: maroon; font-weight: bold;">const</span> <span style="color: maroon; font-weight: bold;">char</span> <span style="color: #808030;">*</span>str2<span style="color: #808030;">,</span> <span style="color: maroon; font-weight: bold;">int</span> start<span style="color: #808030;">)</span>   
<span style="color: purple;">{</span>  
    <span style="color: maroon; font-weight: bold;">int</span> i<span style="color: #808030;">=</span><span style="color: #008c00;">0</span><span style="color: #808030;">,</span> j<span style="color: #808030;">=</span><span style="color: #008c00;">0</span><span style="color: purple;">;</span>  

    <span style="color: maroon; font-weight: bold;">for</span><span style="color: #808030;">(</span>i<span style="color: #808030;">=</span>start<span style="color: #808030;">,</span> j<span style="color: #808030;">=</span><span style="color: #008c00;">0</span><span style="color: purple;">;</span> j<span style="color: #808030;"><</span><span style="color: #603000;">strlen</span><span style="color: #808030;">(</span>str2<span style="color: #808030;">)</span><span style="color: purple;">;</span> i<span style="color: #808030;">+</span><span style="color: #808030;">+</span><span style="color: #808030;">,</span> j<span style="color: #808030;">+</span><span style="color: #808030;">+</span><span style="color: #808030;">)</span>      
     <span style="color: maroon; font-weight: bold;">if</span><span style="color: #808030;">(</span>str1<span style="color: #808030;">[</span>i<span style="color: #808030;">]</span><span style="color: #808030;">=</span><span style="color: #808030;">=</span>str2<span style="color: #808030;">[</span>j<span style="color: #808030;">]</span><span style="color: #808030;">)</span>  
       <span style="color: maroon; font-weight: bold;">continue</span><span style="color: purple;">;</span>  
     <span style="color: maroon; font-weight: bold;">else</span>  
       <span style="color: maroon; font-weight: bold;">return</span> <span style="color: #808030;">-</span><span style="color: #008c00;">1</span><span style="color: purple;">;</span>  

     <span style="color: maroon; font-weight: bold;">return</span> <span style="color: #008c00;">0</span><span style="color: purple;">;</span>  

<span style="color: purple;">}</span>  
</pre>

<pre style="background: #ffffff; color: black;"><span style="color: purple;">  
</span></pre>

<pre style="background: #ffffff; color: black;"><span style="color: purple;">  
</span></pre>

<pre style="background: #ffffff; color: black;"><span style="color: purple;">  
</span></pre>

<pre style="background-color: white; background-position: initial initial; background-repeat: initial initial;">**Usage:**</pre>

<pre style="background-color: white; background-position: initial initial; background-repeat: initial initial;"> <span style="color: purple;"></span> printf("%d\n",strmidcmp("middle","ddlejd",2));    <span style="color: #6aa84f;">**//-1**</span>  
    printf("%d\n",strmidcmp("middle","dd",2));        <span style="color: #6aa84f;">**//0**</span>  
    printf("%d\n",strmidcmp("middle","add",2));      ** <span style="color: #6aa84f;">//-1</span>**</pre>