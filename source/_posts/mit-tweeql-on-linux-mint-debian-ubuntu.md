---
layout: post
title: 'MIT TweeQL on Linux Mint (Debian/Ubuntu)'
date: 2013-09-10 20:57
comments: true
categories: [Twitter, tweeql, twitinfo, tweet]
---

![1.jpg](http://user-image.logdown.io/user/3330/blog/3407/post/138429/tPqBcTKaTROi4UYO1CXf_1.jpg)[TweeQL](https://github.com/marcua/tweeql) 是 MIT 實驗室實作的一個 SQL-like 查詢語言，讓你可以用類似 SQL 的語法來使用 Twitter API 做推文的查詢，例如：
<!--more-->
```
SELECT text 
FROM twitter 
WHERE text contains 'obama' 
  AND location in [bounding box for NYC];
```
這樣子的查詢結果為：`含有 obama 且位置落在 NYC 的推文內容`

要使用 TweeQL，在GitHub 上面的專案 Readme 有兩種安裝方式，我使用第二種 from github 的方式：
1. 開啟終端機(Terminal)
2. 從 github 上 clone 專案原始碼下來：`git clone https://github.com/marcua/tweeql.git`
3. 安裝 python-setuptools 套件： `sudo apt-get install python-setuptools`
4. 切換到 tweeql 資料夾中
5. `sudo python setup.py install`
6. 安裝 curl 工具套件： `sudo apt-get install curl`
7. 產生 tweeql 初始設定檔： `curl https://raw.github.com/marcua/tweeql/master/settings.py.template > settings.py` 
(`curl [URL]` 會抓取該網頁的檔案內容，所以這段指令的意思就是將 setting.py.template 的內容抓下來並寫入 setting.py 中)

到這邊就完成安裝與設定了，接下來要測試的話，直接在終端機輸入： `tweeql_command_line.py`
如果出現：
```
Check if CONSUMER_KEY, CONSUMER_SECRET, ACCESS_TOKEN, and ACCESS_TOKEN_SECRET are defined in settings.py
Consumer key:   
```
就表示安裝與設定成功，接著輸入帳號與密碼即可：
```
Check if CONSUMER_KEY, CONSUMER_SECRET, ACCESS_TOKEN, and ACCESS_TOKEN_SECRET are defined in settings.py
Consumer key: XXX
Consumer secret: 
Access token: XXX
Access token secret:
tweeql>
```
要查詢 tweets，只要在 `tweeql>` 輸入 SQL-like 語法就可以了 

如果你不想總是要重新輸入 Keys，或是你的 App 需要做頻繁的查詢，你可以直接在 settings.py 這個檔案中找到：

\#CONSUMER_KEY=""
\#CONSUMER_SECRET=""

和

\#ACCESS_TOKEN=""
\#ACCESS_TOKEN_SECRET=""

把 # 拿掉以後，在 "" 之間填入 Keys 後存檔就可以了

要離開 tweeql 的方法，只要和下 `ctrl + c` 就可以了

---
##TwitInfo
這是一個用 TweeQL 所建立的 tweet 查詢網站 http://twitinfo.csail.mit.edu/

首頁是簡單的搜尋提示框
![1.jpg](http://user-image.logdown.io/user/3330/blog/3407/post/138429/oY8OWzNScyOefSurdbL2_1.jpg)

輸入 'Obama'，按下確定後，會列出可能的結果連結
![2.jpg](http://user-image.logdown.io/user/3330/blog/3407/post/138429/JPxbG8DwSMi5VQKijoaP_2.jpg)

點進去任意連結
![544899_718032928213945_1053281325_n.jpg](http://user-image.logdown.io/user/3330/blog/3407/post/138429/qRDDD48GSbuCbh6hbQRa_544899_718032928213945_1053281325_n.jpg)
這個畫面顯示的資訊是搜尋到包含 Obama 字樣的最新推文各項資訊