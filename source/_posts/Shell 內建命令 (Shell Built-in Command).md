title: Shell 內建命令 (Shell Built-in Command)
date: 2013-04-20 11:02:00
tags: [C/C++,Computer Science,Operating System,System Program]
---

  

Shell Built-in Command 是指與 shell code 寫在一起編譯成，屬於 shell 這個 program 本身功能的指令，在Windows中稱為 internal command，例如：cd, exit, umask, alias 等等，<span style="background-color: white;">這種內建在 shell 程式碼內的功能無法在 shell 中使用 execv() 去呼叫外部程式的方式執行</span>  

<span style="background-color: white;"><Shell.c></span>  
<span style="background-color: white;">int main()</span>  
<span style="background-color: white;">{</span>  
<span style="background-color: white;">    ...</span>  
<span style="background-color: white;">     if( strcmp(cmd, "cd") == 0)</span>  
<span style="background-color: white;">            cd(pathname);</span>  
<span style="background-color: white;">    ...</span>  
<span style="background-color: white;">}</span>  
<span style="background-color: white;"></span>  
[閱讀更多 »](http://veckcode.blogspot.com/2013/04/shell-shell-built-in-command.html#more)