title: LINQ to SQL 增刪改
date: 2011-12-12 00:49:00
tags: [C#、ASP.NET]
---

  
假設今天要更新一筆 Table tb(int No, string Name, string Favorite_Song) 中的資料呢?  

<span class="Apple-style-span" style="color: #e69138;"> <新增></span>  
  var tmp = new tb  
  {  
   tmp.No = 1,  
   tmp.Name = "Veck",  
   tmp.Favorite_Song = "Amazing Grace"  
  };  

  tb.InsertOnSubmit(tmp);   <span class="Apple-style-span" style="color: #e06666;">//在.NET 3.5 是 tb.Add(tmp);</span>  
  this.SubmitOnChange();   <span class="Apple-style-span" style="color: #e06666;"> //一定要有這一行，不然資料會卡在記憶體，沒有寫入資料庫中</span>  

[閱讀更多 »](http://veckcode.blogspot.com/2011/12/linq-to-sql.html#more)