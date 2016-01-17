title: 又一種 ASP.NET 連接 MySQL 方法
date: 2013-07-29 19:22:00
tags: [C#、ASP.NET,MySQL,VB]
---

1.  <span style="font-family: 新細明體, serif; text-indent: -18pt;">安裝 </span><span lang="EN-US" style="text-indent: -18pt;">MySQL</span>
2.  <span style="font-family: 新細明體, serif; text-indent: -18pt;">安裝 </span><span lang="EN-US" style="text-indent: -18pt;">[MySQL Connector/ODBC](http://dev.mysql.com/downloads/connector/odbc/)</span>  
    <span style="font-family: 新細明體, serif;">安裝完成的檢查：控制台</span><span lang="EN-US">\</span><span style="font-family: 新細明體, serif;">系統管理工具</span><span lang="EN-US">\</span><span style="font-family: 新細明體, serif;">資料來源</span> <span lang="EN-US">(ODBC)\</span><span style="font-family: 新細明體, serif;">驅動程式</span>  
    <span style="font-family: 新細明體, serif;">看看有沒有成功安裝</span> <span lang="EN-US">(</span><span style="font-family: 新細明體, serif;">捲軸往下拉，應該會有 </span><span lang="EN-US">Mysql ODBC 5.1 Driver)</span>
3.  <span style="font-family: 新細明體, serif; text-indent: -18pt;">建立資料庫、資料表、灌資料</span>
4.  <span style="font-family: 新細明體, serif; text-indent: -18pt;">開啟 </span><span lang="EN-US" style="text-indent: -18pt;">VWD</span><span style="font-family: 新細明體, serif; text-indent: -18pt;">，建立 </span><span lang="EN-US" style="text-indent: -18pt;">ASP.NET Web</span> <span style="font-family: 新細明體, serif; text-indent: -18pt;">應用程式</span>
5.  <span style="font-family: 新細明體, serif; text-indent: -18pt;">在方案總管的**專案**</span><span lang="EN-US" style="text-indent: -18pt;">(not</span><span style="font-family: 新細明體, serif; text-indent: -18pt;">方案</span><span lang="EN-US" style="text-indent: -18pt;">)</span><span style="font-family: 新細明體, serif; text-indent: -18pt;">上方按右鍵，選擇『加入參考』，切換到『瀏覽』標籤，搜尋位置『</span><span lang="EN-US" style="text-indent: -18pt;">C:\Program Files (x86)\MySQL\MySQL Connector Net x.x.x\Assemblies\</span><span style="font-family: 新細明體, serif; text-indent: -18pt;">』，看要進入哪個版本，找到『</span><span lang="EN-US" style="text-indent: -18pt;">Mysql.Data.dll</span><span style="font-family: 新細明體, serif; text-indent: -18pt;">』加入</span>
6.  <span lang="EN-US" style="text-indent: -18pt;">xxx.aspx.vb </span><span style="font-family: 新細明體, serif; text-indent: -18pt;">加入</span> <span style="text-indent: -18pt;"></span> <span lang="EN-US" style="text-indent: -18pt;">Imports MySql.Data.MySqlClient </span>  
    <span lang="EN-US">xxx.aspx.cs </span><span style="font-family: 新細明體, serif;">加入</span> <span lang="EN-US">using MySql.Data.MySqlClient;</span>
7.  <span style="font-family: 新細明體, serif; text-indent: -18pt;">撰寫程式碼</span>

<div class="separator" style="clear: both; text-align: left;">    成功執行連線與檢索畫面：</div>

<div class="separator" style="clear: both; text-align: left;">[![](http://1.bp.blogspot.com/-oTaNS6JST5k/UfZNX44aLAI/AAAAAAAAC88/VON_4KO20yU/s320/0.JPG)](http://1.bp.blogspot.com/-oTaNS6JST5k/UfZNX44aLAI/AAAAAAAAC88/VON_4KO20yU/s1600/0.JPG)</div>

[閱讀更多 »](http://veckcode.blogspot.com/2013/07/aspnet-mysql.html#more)