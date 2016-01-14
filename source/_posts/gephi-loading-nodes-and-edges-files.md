---
layout: post
title: '[Gephi] Loading Nodes and Edges Files'
date: 2014-06-25 01:14
comments: true
categories: 
---

1. 準備兩個檔案，分別是 node.csv 和 edge.csv，其中 node.csv 長這樣
![1.png](http://user-image.logdown.io/user/3330/blog/3407/post/207356/Wb81248DSsyxL073UGli_1.png)
請在第一行加上 label,id，label 可以視為 user name，id 則是 user id
然後edge.csv長這樣
![2.png](http://user-image.logdown.io/user/3330/blog/3407/post/207356/zo2GnpRli9ec2DcakrAi_2.png)
一樣在第一行加上 source,target,type，這是為了符合 Gephi 載入格式
其中 source 與 target 對應到 node.csv 的 id
type 有兩種，分別是 Directed (預設) 和 Undirected

2. 以 New Project 開啟 Gephi
3. 切換到 『Data Laboratory』，選擇『Import Spreadsheet』
![3.png](http://user-image.logdown.io/user/3330/blog/3407/post/207356/N45c2iStT2SrQRSTRGAJ_3.png)

4. 先選擇要 node.csv，並以『Node table』載入 
(編碼自己注意，中國大陸簡體編碼可能為GBK，台灣繁體編碼可能為Big5)
![4.png](http://user-image.logdown.io/user/3330/blog/3407/post/207356/DTszGrt5SiWhS6YSsVdc_4.png)
可以看到下方 Preview 將 label 和 id 作為 title

5. 下一步以後
![5.png](http://user-image.logdown.io/user/3330/blog/3407/post/207356/RA5orAayTPqlyzaCCVsB_5.png)
直接按下『完成』

6. 載入 node.csv 的 Nodes 結果
![6.png](http://user-image.logdown.io/user/3330/blog/3407/post/207356/PJ5vVPU7Sl2B5uWBWztt_6.png)

7. 在接著載入 edge.csv，注意要切換成載入為『Edge table』
![7.png](http://user-image.logdown.io/user/3330/blog/3407/post/207356/tIdpRFgQSG8VnRS87imG_7.png)

8. 下一步
![8.png](http://user-image.logdown.io/user/3330/blog/3407/post/207356/6ZAR9ZRDeOPxpkflvVWw_8.png)
這裡可以看到有說 Source 和 Target 都需要是 id of node，所以你要是填寫成 label 的話，就會因為 missing node，所以會自動 create 在 node table 中

9. 沒問題就按下完成
![9.png](http://user-image.logdown.io/user/3330/blog/3407/post/207356/N48tjVoRSRmJw3EEX1aG_9.png)
注意到最右邊那一欄的 Weight，第二個是 2，是因為我們在 edge.csv 中，有兩個 1,5,Undirected，所以 Gephi 自動幫我們加成 weight 為 2，這個可以用在兩個人共同對多少個不同的第三對象有關係，例如以下關係：
A 和 B 都喜歡吃 apple
A 和 C 都喜歡吃 apple
A 和 C 都喜歡吃 banana
則在編制 edge.csv 時，就會寫成：
A,B,Undirected
A,C,Undirected
A,C,Undirected

10. 接著就可以切換到 Overview 來看關係圖，可以看到 a (id=1) 和 i (id=5) 的線比較粗，就是因為們的權重是 2
![10.png](http://user-image.logdown.io/user/3330/blog/3407/post/207356/0820H5kQFiOoKrKSZx9Z_10.png)

(Thanks for advise from Mr. Shiug-Feng Shih @ IM Lab NCCU-CS, Taiwan)
