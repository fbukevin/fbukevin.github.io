title: C# 不使用 SqlDataSource 連接資料庫
date: 2011-09-01 02:30:00
tags: [C#、ASP.NET]
---

話說在學習 ASP.NET 的時候，因為初學的關係，所以許多教材都會教導使用 sqlDataSource 這個控制項來設定連接資料庫，好處是可以不用自己去 call  C#中呼叫資料庫的方法和免去輸入SQL語法的麻煩，另一個好處是可以直接使用 ASP.NET 提供的登入控制項，繫結資料庫做到登入驗證。  

但是使用登入控制項的缺點，就是會受限於 ASP.NET 的格式化限制，也就是你不能夠自由的改變登入控制項的外貌(只有幾個樣式可以選擇)，這個時候如果想要自己實作登入控制項，像是 PHP 那樣使用 HTML 的 Input-Text 和 Input-Button ，就沒辦法直接使用 sqlDataSource 繫結資料庫，首先我這邊先介紹如何在 ASP.NET 中不使用 SqlDataSource 連接資料庫，以下是我上網找了些資料以後測試成功的連接方法。  

1\. 建立一個 WebForm (WebForm1.aspx)，並在 App_Data 中建立一個 SQL Server 資料庫檔案(Datebase1.mdf)  

<div class="separator" style="clear: both; text-align: center;">[![](http://4.bp.blogspot.com/-Q3zkLCnlZJQ/Tl55u2tpvrI/AAAAAAAAAGc/d7Ot0ROiBZ8/s320/1.jpg)<span class="Apple-style-span" style="-webkit-text-decorations-in-effect: none; color: black;"></span>](http://4.bp.blogspot.com/-Q3zkLCnlZJQ/Tl55u2tpvrI/AAAAAAAAAGc/d7Ot0ROiBZ8/s1600/1.jpg)[![](http://1.bp.blogspot.com/-VhOtP3dZMWs/Tl55eQxpxuI/AAAAAAAAAGY/_4VCUYaB2o0/s320/2.jpg)](http://1.bp.blogspot.com/-VhOtP3dZMWs/Tl55eQxpxuI/AAAAAAAAAGY/_4VCUYaB2o0/s1600/2.jpg)</div>

2.接著開啟程式碼 WebForm1.aspx.cs，並加入 using System.Data.SqlClient 這個命名空間，這個是 C# 提供連接資料庫的一個命名空間，後面所實體化出來的 SQL 物件都是在這個命名空間中的類別  
[閱讀更多 »](http://veckcode.blogspot.com/2011/08/c-sqldatasource.html#more)