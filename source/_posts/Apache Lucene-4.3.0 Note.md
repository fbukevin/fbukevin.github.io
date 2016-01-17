title: Apache Lucene-4.3.0 Note
date: 2013-05-31 16:56:00
tags: [Apache,Java,Lucene]
---

  
     <下載與設定>  

1.  先到[官方網站](http://lucene.apache.org/core/)下載 [Lucene](http://www.apache.org/dyn/closer.cgi/lucene/java/4.3.0) (目前為 4.3.0)，Windows 上下載 .zip
2.  下載回來以後解壓縮 .zip
3.  根據官網說明，進入解壓的資料夾以後，分別在 /core、/demo、/analysis/common 和 /queryparser (不是 /queries) 四個子資料夾中可以找到 lucene-core-4.3.0.jar、lucene-demo-4.3.0.jar、 lucene-analyzers-common-4.3.0.jar 和 lucene-queryparser-4.3.0.jar 四個 jar 檔案 (tar.gz 會有點不一樣)
4.  將這四個檔案 "copy" 到你安裝 JDK 的 lib 資料夾中 (*1)
5.  將這四個檔案在 lib 中的絕對路徑加到 Java 的 CLASSPATH 設定中 (例如：C:\Program Files\Java\jdk1.7.0_05\lib\lucene-core-4.3.0.jar，別忘記要加 .jar 喔！如果你是直接複製檔名的話)

[閱讀更多 »](http://veckcode.blogspot.com/2013/05/apache-lucene-430.html#more)