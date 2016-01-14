---
layout: post
title: '[C] Making Progress Bar'
date: 2014-11-02 15:55
comments: true
categories: 
---

看到很多用 command line 安裝的程式，都會有類似 "#####"、"..." 或是 "[===]" 的 progress bar，所以想說來研究一下怎麼在 C 的程式實現這個進度條的顯示，程式不長，直接貼上來解說。

```
#include<stdio.h>

int main(void){
   int i = 0, j = 0;
   for(i = 0; i <= 10000; i++){		// 這是用來控制進度的
      for(j = 0; j < 10000; j++)		// 這是用來控制速度的
      {  }
      printf("\rIn progress %%%d[", i/100); 	// 輸出 percentage，\r 是 return (回到行首)
      for(j = 0; j < (i/100); j++)
         printf("=");			// 輸出 "="
      printf("]");
      fflush(stdout);			// 清除螢幕(standard output)
   }
   printf("\n");
   return 0;
}
```

Note：雖然使用了 \r 和 fflush(stdout); 來刷新螢幕，但是如果單一行的輸出超出螢幕最右方可以顯示的範圍，好像會因為 overflow 而造成 fflush(stdout) 失效，重複填滿整個螢幕。

Demo Video: http://youtu.be/R7LRsSCmSuo