---
layout: post
title: '[JavaScript] Node.js Blog Framework - Hexo - 私人伺服器佈署'
date: 2014-08-08 19:05
comments: true
categories: 
---
http://hexo.io/

有鑑於網路上大部分的文章都是教學如何佈署到 GitHub 和 Heroku 為主的教學
雖然我的需求沒什麼太大不同，還是分享一下給需要的人參考
簡單建立專案、基本設定、套用主題、產生靜態檔案和佈署設定這邊不說，我針對佈署到個人站台做說明

1. 建立好專案和寫了些 post 之後，使用 `hexo generate` 或 `hexo g` 產生靜態檔案，會放在 public 這個資料夾下，當我們使用 `hexo deploy` 的時候，其實是把 public 的內容傳上 GitHub 或 Heroku 等空間(更正確來說是上傳 .deploy 的內容)，因此我們同樣只需要把 public 的東西放到站台上就好了

例如我在：`http://fancy.cs.nccu.edu.tw` 伺服器中的 Apache 根目錄中建立了 `project/vexo` 這個目錄，我打算把專案放在這裡，因此我用 FTP 傳送到這個目錄下
![螢幕快照 2014-08-08 下午9.28.20.png](http://user-image.logdown.io/user/3330/blog/3407/post/218116/TFTHfj5CRGasXCDRKqsk_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-08-08%20%E4%B8%8B%E5%8D%889.28.20.png)

接著我們就可以連上網址看結果了
![螢幕快照 2014-08-08 下午9.29.14.png](http://user-image.logdown.io/user/3330/blog/3407/post/218116/KibjJfQZQ6CzRtudN1Eu_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-08-08%20%E4%B8%8B%E5%8D%889.29.14.png)

Oops! 看來 CSS 和 JavaScript 等靜態資料沒有正確的載入
開一下 console 來看
![螢幕快照 2014-08-08 下午9.29.25.png](http://user-image.logdown.io/user/3330/blog/3407/post/218116/HATLWCATQyGbCZ5T9WZz_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-08-08%20%E4%B8%8B%E5%8D%889.29.25.png)

resource 的路徑直接 request 根目錄下的 img、css 和 js，所以當然找不到，因為我們是放在 根目錄下的 `project/novex`
解決方法是設定好 _config.yml 的 url 和 root 
```
   url: http://fancy.cs.nccu.edu.tw/project/novex
   root: /project/novex
```
把 root 設定為我們專案的根目錄，然後再 generate 一次後放到站台上
![螢幕快照 2014-08-08 下午9.58.19.png](http://user-image.logdown.io/user/3330/blog/3407/post/218116/8p2eLpOuT3eSaAnfg4iD_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-08-08%20%E4%B8%8B%E5%8D%889.58.19.png)


參考文章：
* 基本教學
http://yangjian.me/workspace/building-blog-with-hexo/
http://blog.zjun.tw/2014/02/01/hexoSetupNote/
http://zipperary.com/2013/05/28/hexo-guide-2/

* 有提到 gh-pages (Project site)
http://eva0919.github.io/2013/04/21/%E4%BD%BF%E7%94%A8hexo%E4%BB%A5%E5%8F%8Agithub-page%E5%BB%BA%E7%AB%8B%E8%87%AA%E5%B7%B1%E7%9A%84%E9%83%A8%E8%90%BD%E6%A0%BC/

* 有提到購買網域
http://jianshu.io/p/05289a4bc8b2

* CSS 和 JavaScript 配置問題
http://blog.fens.me/hexo-blog-github/


PS: 後來發現是台灣人寫的，採用 MIT License，也真的是 Made in Taiwan，感動！