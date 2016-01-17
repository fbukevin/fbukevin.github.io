title: 環境變數 Path 的應用
date: 2012-07-24 23:41:00
tags: [Computer Science]
---

(小兒科篇，單純覺得這樣應用很有趣 !!! ^<span style="background-color: white; color: #222222; font-family: arial, sans-serif; font-size: x-small; line-height: 16px;">ω</span><span style="background-color: white;">^)</span>  

相信大部分的人都寫過 Java，在安裝完 JDK 以後，都一定要做一件事情，也就是到我的電腦去把 javac.exe 和 java.exe 這兩個執行檔所在的目錄 bin 這個相對路徑加入系統的環境變數中，甚至有些系統中會自動幫你加入，所以很多人只知道要這麼做，好讓你在使用命令提是字元編譯和執行 java 程式的時候可以直接輸入 java 和 javac 對原始碼進行處理，不過其實這個 Path 的用途最主要是用來讓系統搜尋 "指令程式" 用的。  

一般我們在命令提示字元輸入的指令，大部分都是作業系統自動在所有 Path 變數中指定的目錄下尋找與輸入的指令名稱相同的可執行檔或批次檔，並執行它工作，所以 Java 的環境變數才會要求要把 javac.exe 和 java.exe 所在的目錄 bin (這個名稱的目錄底下一般都存放可執行檔)路徑給加入到 Path 中。  

[閱讀更多 »](http://veckcode.blogspot.com/2012/07/path.html#more)