title: ~Java~ 提示字符讀取輸入
date: 2011-04-26 02:44:00
tags: [Java]
---

大家有沒有一個疑問  
為什麼  

public static void main(String args[]){   }  
                                        ↑↑↑  
                                        這是做什麼的?  

今天看到一個程式內的應用，所以就自己想到這個想法實作一遍  
以下是我的程式碼片段:  

<pre style="background: #000000; color: white;"> <span style="color: #7f0055; font-weight: bold;">public</span> <span style="color: #7f0055; font-weight: bold;">class</span> argsStream  
 {  
     <span style="color: #7f0055; font-weight: bold;">public</span> <span style="color: #7f0055; font-weight: bold;">static</span> <span style="color: #7f0055; font-weight: bold;">void</span> main(<span style="color: #7f0055; font-weight: bold;">String</span> args[])  
     {  
        <span style="color: #7f0055; font-weight: bold;">for</span>(<span style="color: #7f0055; font-weight: bold;">int</span> i=0;i<args.length;i++)  
         {  <span style="color: #7f0055; font-weight: bold;">System</span>.out.println(args[i]);  }  
    }  
} </pre>

<div>

<div>要測試時，請用命令提示字元，輸入java argsStream</div>

<div>當你按下Enter會發現程式沒有作用  

</div>

<div>接著請你再輸入一次，但是這一次，請輸入 java argsStream Iamnotcool</div>

<div>按下Enter後</div>

<div>

<pre style="background: black; color: white;">C:\User\Desktop>java argsStream iamnotcool   </pre>

</div>

<div>就會出現你所輸入的字串!!!</div>

<div>所以知道為什麼了吧!</div>

</div>

[閱讀更多 »](http://veckcode.blogspot.com/2011/04/java.html#more)