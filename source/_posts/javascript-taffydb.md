---
layout: post
title: '[JavaScript] TaffyDB'
date: 2014-05-29 20:47
comments: true
categories: 
---
TaffyDB 是一個輕量級及 Open Source 的 JavaScript Database

它的專案內容很小，主要的 library 只有一個 taffy.js，所以它的操作應該都是在瀏覽器執行的程式記憶體中，沒有寫入到檔案系統
![螢幕快照 2014-05-29 下午8.53.39.png](http://user-image.logdown.io/user/3330/blog/3407/post/202080/AyMG7ElrRKmmLMIr33PQ_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-05-29%20%E4%B8%8B%E5%8D%888.53.39.png)

Taffy 是 ORM 實作的一種，它也有提供 extension 讓網頁程式可以介接 MySQL 等資料庫，像 mongoDB 那樣

在 HTML 中使用 TaffyDB，首先要引入 taffy.js：
``` 
<script src="https://github.com/typicaljoe/taffydb/raw/master/taffy.js"></script> 
```

接著我們要建立一個 TAFFY 物件來操作 taffy 資料庫：
``` 
var students = TAFFY();	 
```
這樣就算是建立了 students 這個資料表了

接著我們就可以利用這個物件來對資料庫 CRUD，taffy 採用的是 json 的表示方式 (啊就是 JavaScript 物件啊！)
```
    students.insert([
     	{ name: "Veck", gender:"male" },
      { name: "Candice", gender:"female" }
    ]);
```
這裡我們新增了兩個 entry 到 students 這個資料表物件中

最後，我們就可以呼叫一些資料庫函式來查詢：
```
students({name:"Candice"}).count();				# => 1
```

試著查詢第一筆資料：
```
students().first();
```
\* student.first() is wrong usage.
會得到這樣的結果：
```
{ name: 'Veck',
  gender: 'male',
  ___id: 'T000002R000002',
  ___s: true }
```
其中 ___id 和 ___s 是 taffy 加入的欄位

在 node.js 中只要引入 taffy 物件就可以使用了：
```
var TAFFY = require("./taffydb/taffy").taffy;		// import taffy library

var students = TAFFY();  	//create a TAFFY Object
```