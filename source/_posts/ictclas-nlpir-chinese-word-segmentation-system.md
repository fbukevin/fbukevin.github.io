---
layout: post
title: 'ICTCLAS NLPIR 漢語分詞系統'
date: 2014-06-06 04:30
comments: true
categories: 
---
因為台灣中研院的中文斷詞工具[CKIP](http://ckipsvr.iis.sinica.edu.tw/)好像從 2012 年以後就沒再更新，而我申請介接的帳號一直收不到信，所以嘗試使用了之前偶然得知中國大陸中科院的漢語分詞工具 [ICTCLAS](http://ictclas.org/)，不過這個網址的版本最後更新也只到2011年，而且在線演示一直沒辦法呈現結果，最後進一步搜尋到 张华平 博士于 2014 年的版本(好像從2013年開始維護)：[ICTCLAS NLPIR](http://ictclas.nlpir.org/)
<!--more-->
2014/06/09 更新：就在我發完以後，過了兩天就突然無法啟動，看了 error log，寫說是『Not valid license or your license expired! Please feel free to contact pipy_zhang@msn.com!』，上網查了論壇討論，似乎這個新版本有三個月的使用期限，而六月出正式這個時候....
1. http://www.bigdatabbs.com/forum.php?mod=viewthread&tid=5309
2. http://www.bigdatabbs.com/forum.php?mod=viewthread&tid=5226

![擷取.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/2Yettap7RFGcJvHtBAQN_%E6%93%B7%E5%8F%96.PNG)

可以直接按首頁動畫其中一個的『[点击下载](http://ictclas.nlpir.org/upload/20140324095815_ICTCLAS2014.rar)』获得一整个文件包，大小大約是 50.7 MB，在邊等待下載的同時，就先來玩一下『在线演示』(基于对该系统开发者的尊重....还有我懒得切换繁简中文输入-微软怎么没有快速切换呢?-所以以下直接以简体介绍，如有错误字词，还请包容与来信更正!)

![0.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/IWscjFTIu5fRAbSSYswk_0.PNG)
这个展示画面上部份是输入文本的地方，右边提供了两组示范文字

因为最近刚听闻『屌丝』这神奇的词汇，所以就选了它的一段来试试
![1.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/TeEjElKKRACSrP3A3HMu_1.PNG)

按下『普通分词』或『自适应分词』后，就可以得到相对应的分词结果
(我不太清楚普通分词与自适应分词的差异，因为按下两个按钮得到的结果好像差不多，有待后续研究...)
![2.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/kwzJS8YrTQuYg0b3wk2G_2.PNG)
可以看到，除了是以空白键 (space) 去断开词汇以外，这个实作所采用的词性标记方式是在字词的後方加上 "/x"，其中 x 是这套系统定义的一系列词汇对应的词性，中研院的斷詞系統其實有類似的標記方式，不過這些詞性就要進一步去研究了

中研院線上展示結果中『包含未知詞的斷詞標記結果』的畫面
![3.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/B2ouRhyjTjKJtEuUy0cw_3.PNG)

进一步看結果，我研判中研院系統的『未知詞列表』與中科院的『新词列表』应该是指一样的事物，有趣的是，针对同一份样本，中研院的结果有几笔未知词，中科院则没有未知词，可能的原因我想有二：所收纳的字典词汇不同、我丢进中研院系统的是中科院范本的内容(即简体字内容)

中研院『未知詞列表』
![4.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/zn0Rq9fSj6cEtsRpLtuQ_4.PNG)
中科院『新词列表』
![5.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/NDMSnhFeRVCMEA5mPiP9_5.PNG)

再来我试试看汇入挡案，所以我编辑了一个挡案如下：
![6.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/fSWo5UMiRwudRPuhniyC_6.PNG)

然后在网页中点选『选择文件』，找到对应的这个挡案名后开启：
![7.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/WRzctFUgTtiVAD9SlTDG_7.PNG)

Oops！我输入的挡案竟然是乱码，我调整了挡案的编码，从 ANSI、UTF-8、UTF-16 LE、UTF-16 BE、Unicode，都是一样的结果，但是用 Word 开启时是可以自动转换的，我观察了一下 Word 开启时的编码，后来在我所用的编辑器 Notepad++ 中找到相似的编码选项，就可以正常显示我的内容了
![要选这个编码才能正确显示.png](http://user-image.logdown.io/user/3330/blog/3407/post/203081/gCxp3q2vQ76R9mt3TSA8_%E8%A6%81%E9%80%89%E8%BF%99%E4%B8%AA%E7%BC%96%E7%A0%81%E6%89%8D%E8%83%BD%E6%AD%A3%E7%A1%AE%E6%98%BE%E7%A4%BA.png)

做法是这样的：『編碼/編碼字符集/中文/GB2312(Simplified)』，
接着才开始输入你要的内容，繁简皆可
存挡的时后会自动以此编码来存挡，如此就可以成功载入了
![8.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/B0SZ11TTQhOdjXq2kmNc_8.PNG)

GB 2312 (GB0)好像就跟 Big5 一樣，是中國地區自行編篡的一套文字編碼系統，很多可以將 GB 轉 Big5 的網站，例如:http://www.j4.com.tw/big-gb/ (请原谅我对字元编码没有足够深的了解 T^T)，不过我猜想语系是设定为简体中文的操作系统应该是没这个问题

载入挡案的分词结果
![10.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/49V8lC8xTeujiuDK9luq_10.PNG)

好了，至此，我们的文件包已经下载完了，我们可以解压缩，里面的挡案很多，有一些是给开发人员客制化自己程式需求时可以介接的函数库(类别库)，ICTCLAS 这个专案目前以 C/C++/Java 为主要实作语言，但是根据文件说明，也有提供 C# 和 Python 的介接端口(API)，详细的说明可以参考解压缩后的资料夹中 Readme 这个挡案
![12.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/YZqfApNFS3WARt8lgPg1_12.PNG)


我们可以开起 Readme 来看看
![11.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/1gqFswTBWYpkPUZG5OQw_11.PNG)
很好，又是乱码，这个问题跟前面的问题是一样的，不再赘述，请自行切换成人类语言~

我这边要介绍的用法主要是在 bin 这个资料夹中的 ICTCLAS2014，进入之后，挡案列表如下：
![13.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/7ThSjJjkQiSafqlakGdg_13.PNG)

我们点选『NLPIR_WinDemo』这个执行挡案来启动程式
![14.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/qmYdtZbLS8C7xYV73zp6_14.PNG)
恩，又是乱码，这次不是文字挡，没法儿直接修改编码，需要改系统语系，但是整个改掉很麻烦滴，使用 Windows 的捧油上网搜一下就知道解决方案是：[AppLocale](http://www.microsoft.com/zh-tw/download/details.aspx?id=13209)，详细怎么设定开启可以参考 [这里](http://www.cooltey.tw/ping/applocale.htm)

解决的语系问题，就可以知道有哪些功能选项了
![15.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/m6651P5hSb2qlMgAmev5_15.PNG)
(嘿嘿! 张华平 博士 的名字现身了～广告被压缩了...XD)

首先我们使用『分词』，点选以后的画面如刚启动时的上图，在不调整『分词粒度』與『词性标注集』的情况下，试着在上方栏输入字串，接着与在线演示一样，点选普通分词，即可得到分词结果，与在线演示的结果如出一轍
![16.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/7cRRat9iQpSZwBDs7D5v_16.PNG)

玩玩看打开文件，我们开启方才为了在线演示建立的测试文本
![17.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/V3Zu1eCRlKTmwOrbgno1_17.PNG)

![18.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/mWH0tltnTeSJl4XfVk76_18.PNG)

最后我们尝试『用户词典』
![19.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/AjqdStTQOycmULnUpg0s_19.PNG)

一样可以输入文字后做分词，但是这里的重点是在使用者自定词汇，所以我们先来看看字典在哪，事实上，字典是随意的，你可以自行建立，但是需要符合这套系统的『词汇 词性』规范，回顾资料夹中会看到有个挡案叫做 userdic，就是它了，开起来看内容：
![20.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/JMN8Uh9wRStcPiqUnIcv_20.PNG)
很明显的至少『周鸿祎』为人名，不会收录在普通字典中，因此是属于用户自定义的词汇

好，让我们输入一段有这两个词汇的语句，并分词
![21.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/G5hDruNwR2hVWXOQe3gQ_21.PNG)
可以看到我标红的地方，就成功地将那两个自定义词汇分出来了，词性也符合我们定义的

如果你在自己定义的字典中漏掉某些词汇，也可以直接在程式中新增，但是注意噢！这个新增的词汇并无法写回到你自定义的字典挡案中

我在下方的『用户词』中添加了『韦克』与『溫拿』，然後輸入『韦克是个研究计算机科学与语言学的研究生，他求学路成顺遂，是个温拿』，得到结果如下图
![22.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/203081/mK6DU9sQTzS7VGdapc4F_22.PNG)
哈哈！『韦克』被成功断出来了，但是...『温拿』怎么被拆开了呢？请自行观察吧！ 这可不是 Bug～
Hint: 『人』 vs 『一』

对于这套系统的研究目前至此，有些可以改进的地方：在用户新增的词汇那边不知道怎么删除词汇

最后较重要待研究的议题：词性类目有哪些？内建字典在哪？普通分词与自适应分词的差异？
