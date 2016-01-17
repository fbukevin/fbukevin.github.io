---
layout: post
title: '[Python] Scrapy'
date: 2014-05-27 18:38
comments: true
categories: 
---
Reference: [Scrapy Documentation](http://doc.scrapy.org/en/latest/)

Installation: ```pip install scrapy ```

Create Project: ```scrapy startproject  [project name]```
<!--more-->
Project Directory Tree:
````
tutorial/
    scrapy.cfg
    tutorial/
        __init__.py
        items.py
        pipelines.py
        settings.py
        spiders/
            __init__.py
```

進入專案以後，我們首先要設定哪些項目是我們要抓的，因此要編輯 /tutorial/items.py：
```
from scrapy.item import Item, Field
	class TutorialItem(Item):
      title = Field()
      link = Field()
      desc = Field()
```
＊這些 Field() 是在 scrapy.item 中定義的類別，在此我們宣告了三個 scrapy.item 的 Field 物件

接著就是要編寫我們的第一個 Crawler，在 /tutorial/spiders 中建立一個檔案 dmoz_spider.py(你的crawler檔)：
```
    from scrapy.spider import Spider
    
    class DmozSpider(Spider):
      name = "dmoz"						// 設定 crawler  的名稱
      allowed_domains = ["dmoz.org"]	// ???
      start_urls = [					// 	設定要爬的網頁 URL 列表
      	"http://www.dmoz.org/Computers/Programming/Languages/Python/Books/",
   	"http://www.dmoz.org/Computers/Programming/Languages/Python/Resources/"
      ]
      
      /* 定義抓回來物件的處理函式 */
      def parse(self, response):
      	filename = response.url.split("/")[-2]	// 從最後面開始擷取字元為 filename，並在遇到 '/' 時結束擷取
        with open(filename, "wb") as f:			// 建立或開啟名為 filename 的檔案，並指定為 f 
        	f.write(response.body)				// 將物件 response 的 body 內容寫入檔案中
```

然後就可以執行這隻爬蟲程式，將上面兩個 URL 的網頁抓下來了，回到專案的根目錄，輸入：
```scrapy crawl [spider_name]```

然後就得到下面的執行畫面，並且在根目錄下得到 Books 和 Resources 這兩個 URL 的網頁檔案
![螢幕快照 2014-05-27 下午6.16.41.png](http://user-image.logdown.io/user/3330/blog/3407/post/201739/atPjO0zS3yqh8iFA2OQI_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-05-27%20%E4%B8%8B%E5%8D%886.16.41.png)


![螢幕快照 2014-05-27 下午6.34.33.png](http://user-image.logdown.io/user/3330/blog/3407/post/201739/shUGeoZ9RnKY93OsNrYI_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-05-27%20%E4%B8%8B%E5%8D%886.34.33.png)

在 tutorial/spiders 中，我們可以編寫多個 spider，但是各個 spider 的名稱 (name 屬性) 必須唯一


Note:
本文參考的 Document 版本是 0.22.2，這個版本的專案預設 import 方式與 0.23.0 有點不一樣
在 0.22.2 的 from scrapy.xxx import .... 到了 0.23.0 中是 import scrapy 
所以像是：
>	from scrapy.item import Item

>	class DmozItem(Item):

都要改成：
>	import scrapy

> class DmozItem(scrapy.Item):

另外要注意的是，from 那邊是 item，import 是 Item，大小寫不一樣！