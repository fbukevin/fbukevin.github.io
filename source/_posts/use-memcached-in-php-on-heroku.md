---
layout: post
title: 'Use Memcached in PHP on heroku'
date: 2013-10-09 21:41
comments: true
categories: [php, heroku, memcached]
---
[Memcached](http://zh.wikipedia.org/wiki/Memcached) 在網頁中可以用來加速網頁的存取速度，也可以用來減少回應相同使用者需求的時間

因為課程的關係，我使用了 [Heroku](https://www.heroku.com) 這個平台來 deploy 我的網頁，Heroku 免費的版本提供了 25 MB 大小的 Memcached，但是你必須先註冊你的信用卡資料才可以將這項服務套用至你的網頁程式中

要選用 Memcached 這樣服務，要到 [Add-on](https://addons.heroku.com/) 的頁面來設定

![擷取.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/146015/O2bRZ4xqSxSbnR8G1YYz_%E6%93%B7%E5%8F%96.JPG)

請選擇 `MemCachier` 這個項目，進去以後往下拉可以看到中間有一個區塊讓你選擇要採用多少大小的 Memcached
![2.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/146015/2V0lssxjQVCqiApdIEwp_2.JPG)

以免費版的為例，我們點選最後一個 `Developer Free` 的項目以後，右下方的有一個選項請你選擇你要套用的網頁應用程式，我選擇 cryptic-atoll-1791，接著 Add Developer for Free
![3.png](http://user-image.logdown.io/user/3330/blog/3407/post/146015/y02vqOuUQW64qAE4b5YH_3.png)
如果你還沒填寫信用卡資料，在這一步驟會請你先去填完信用卡資料再回來設定
既然是免費的為什麼還需要信用卡？和 Amazon 的 AWS 一樣，如果你有 more over 的需求時，系統會藉由此信用卡先向你 charge，但是免費的就是免費的，不會收費

當設定好 Memcached 以後，就要來修改我們的程式碼，讓它具有 Memcached 的功能了，我們以一個可以找到小於使用者輸入的數字的最大質數做範例：
<pre class="php" style="font-family:monospace;"><span style="color: #000000; font-weight: bold;">&lt;?php</span>
&nbsp;
<span style="color: #666666; font-style: italic;">&nbsp;/* include MemcacheSASL.php */</span>
<span style="color: #b1b100;">include</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">'MemcacheSASL.php'</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #000088;">$m</span> <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> MemcacheSASL<span style="color: #339933;">;</span>
<span style="color: #000088;">$server</span> <span style="color: #339933;">=</span> <span style="color: #990000;">explode</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;,&quot;</span><span style="color: #339933;">,</span> <span style="color: #990000;">getenv</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;MEMCACHIER_SERVERS&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #b1b100;">foreach</span> <span style="color: #009900;">&#40;</span><span style="color: #000088;">$server</span> <span style="color: #b1b100;">as</span> <span style="color: #000088;">$s</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
  <span style="color: #000088;">$parts</span> <span style="color: #339933;">=</span><span style="color: #990000;">explode</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;:&quot;</span><span style="color: #339933;">,</span> <span style="color: #000088;">$s</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
  <span style="color: #000088;">$m</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">addServer</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$parts</span><span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">0</span><span style="color: #009900;">&#93;</span><span style="color: #339933;">,</span> <span style="color: #000088;">$parts</span><span style="color: #009900;">&#91;</span><span style="color: #cc66cc;">1</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span>
<span style="color: #000088;">$m</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">setSaslAuthData</span><span style="color: #009900;">&#40;</span><span style="color: #990000;">getenv</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;MEMCACHIER_USERNAME&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">,</span><span style="color: #990000;">getenv</span><span style="color: #009900;">&#40;</span><span style="color: #0000ff;">&quot;MEMCACHIER_PASSWORD&quot;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
&nbsp;
<span style="color: #666666; font-style: italic;">/* GET user input number */</span>
<span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #339933;">!</span><span style="color: #990000;">isset</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$_GET</span><span style="color: #009900;">&#91;</span><span style="color: #0000ff;">&quot;n&quot;</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
  <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">&quot;Invalid numver n !&quot;</span><span style="color: #339933;">;</span>
  <span style="color: #990000;">exit</span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span>
<span style="color: #000088;">$n</span> <span style="color: #339933;">=</span> <span style="color: #990000;">intval</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$_GET</span><span style="color: #009900;">&#91;</span><span style="color: #0000ff;">&quot;n&quot;</span><span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
<span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #000088;">$n</span> <span style="color: #339933;">&lt;=</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
  <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">&quot;n should be &gt;1!&quot;</span><span style="color: #339933;">;</span>
  <span style="color: #990000;">exit</span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span> <span style="color: #b1b100;">else</span> <span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #000088;">$n</span> <span style="color: #339933;">&gt;</span> <span style="color: #cc66cc;">1000</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
  <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">&quot;n should be &lt;=1000!&quot;</span><span style="color: #339933;">;</span>
<span style="color: #009900;">&#125;</span>
&nbsp;
<span style="color: #666666; font-style: italic;">&nbsp;/*
  * using cache here to check if the prime is exist in cache. 
  * (PHP Site uses Memcached as its class, SASL uses MemcacheSASL as its class, I use the latter one)
  */</span>
 <span style="color: #b1b100;">if</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$p</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$m</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">get</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$n</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>      <span style="color: #666666; font-style: italic;">// check cache </span>
    <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">&quot;Get &quot;</span><span style="color: #339933;">.</span><span style="color: #000088;">$p</span><span style="color: #339933;">.</span><span style="color: #0000ff;">&quot; from memcached!&quot;</span><span style="color: #339933;">;</span>
 <span style="color: #009900;">&#125;</span>
 <span style="color: #b1b100;">else</span> <span style="color: #009900;">&#123;</span>        <span style="color: #666666; font-style: italic;">// if cache miss, find the prime</span>
  <span style="color: #000088;">$prime</span> <span style="color: #339933;">=</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span>
  <span style="color: #b1b100;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000088;">$i</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$n</span><span style="color: #339933;">;</span> <span style="color: #000088;">$i</span> <span style="color: #339933;">&gt;</span> <span style="color: #cc66cc;">1</span><span style="color: #339933;">;</span> <span style="color: #000088;">$i</span><span style="color: #339933;">--</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
    <span style="color: #000088;">$is_prime</span> <span style="color: #339933;">=</span> <span style="color: #009900; font-weight: bold;">true</span><span style="color: #339933;">;</span>
    <span style="color: #b1b100;">for</span> <span style="color: #009900;">&#40;</span><span style="color: #000088;">$j</span> <span style="color: #339933;">=</span> <span style="color: #cc66cc;">2</span><span style="color: #339933;">;</span> <span style="color: #000088;">$j</span> <span style="color: #339933;">&lt;</span> <span style="color: #000088;">$i</span><span style="color: #339933;">;</span> <span style="color: #000088;">$j</span><span style="color: #339933;">++</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
      <span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #000088;">$i</span> <span style="color: #339933;">%</span> <span style="color: #000088;">$j</span> <span style="color: #339933;">==</span> <span style="color: #cc66cc;">0</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#123;</span>
        <span style="color: #000088;">$is_prime</span> <span style="color: #339933;">=</span> <span style="color: #009900; font-weight: bold;">false</span><span style="color: #339933;">;</span>
        <span style="color: #b1b100;">break</span><span style="color: #339933;">;</span>
      <span style="color: #009900;">&#125;</span>
    <span style="color: #009900;">&#125;</span>
    <span style="color: #b1b100;">if</span> <span style="color: #009900;">&#40;</span><span style="color: #000088;">$is_prime</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
      <span style="color: #000088;">$prime</span> <span style="color: #339933;">=</span> <span style="color: #000088;">$i</span><span style="color: #339933;">;</span>
      <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">&quot;&lt;=&quot;</span><span style="color: #339933;">.</span><span style="color: #000088;">$n</span><span style="color: #339933;">.</span><span style="color: #0000ff;">&quot; has the biggest prime &quot;</span><span style="color: #339933;">.</span><span style="color: #000088;">$prime</span><span style="color: #339933;">.</span><span style="color: #0000ff;">&quot;&lt;/br&gt;&quot;</span><span style="color: #339933;">;</span>
      <span style="color: #b1b100;">echo</span> <span style="color: #0000ff;">&quot;&lt;a href='index.php'&gt;Back&lt;/a&gt;&quot;</span><span style="color: #339933;">;</span>
      <span style="color: #b1b100;">break</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span>
  <span style="color: #009900;">&#125;</span>
&nbsp;
  <span style="color: #666666; font-style: italic;">/*store it in cache */</span>
  <span style="color: #000088;">$m</span><span style="color: #339933;">-&gt;</span><span style="color: #004000;">set</span><span style="color: #009900;">&#40;</span><span style="color: #000088;">$n</span><span style="color: #339933;">,</span> <span style="color: #000088;">$prime</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
 <span style="color: #009900;">&#125;</span>
<span style="color: #000000; font-weight: bold;">?&gt;</span>
&nbsp;</pre>

在第一部分我們引用了一個名為 PHPMemcachedSASL.php 的 library，讓我們可以操作 Memcached，這個函式庫需要到作者的 GitHub 上去下載：https://github.com/ronnywang/PHPMemcacheSASL

事實上 PHP Library 中就有 Memcached 的操作函式，可能是因為 Memcached 缺乏認證與安全管制，所以 Heroku 官方文件才會建議採用 MemcachedSASL 而不是使用 PHP 內建 Memcached Library 作為網頁 Memcached API 的原因，但是兩者的使用方式都相同，基本的 get()、set() 和 add() 都有!

第二部份我們接收來自 index.php 這張網頁的輸入值，驗證他的合法性與範圍

第三部分一開始我們呼叫 Memcached 物件 $m 的 `get($key)` 這個方法，來檢查看看我們要查的質數是否已經在 Cache 中，這裡的 $key 正是使用者所輸入的值，如果找到的話，我們就印出這個值數，否則會得到 False，我們才接著尋找質數

最後一部分是在進行尋找質數之後，因為我們沒有在 Cache 中找到質數，所以找到質數以後，為了讓下次有使用者輸入同樣的數要找質數時可以較快速的直接從 Cache 找而不用做運算，所以我們呼叫了 $m 的 `set($key, $value)` 這個方法，其中 $key 一樣是我們給使用者輸入的數，$value 就是我們找到的質數啦! 我們用使用者輸入的值當作查找 cache 的鍵值，有點像雜湊的

事實上，`set($key, $value)` 完整的簽名是這樣的: `set($key, $value, [$expiration])`
最後的 $expiration 參數是選擇性的，用來指定這筆快取頁存在 Cache 多久以後可以被清掉

而 set() 有一個與他簽名完全相同的攣生兄弟 `add($key, $value, [$expiration])`
另外還有一個沒有 $expiration 的相似方法 `replace($key, $value)`
![memcached 使用 add, set 和 replace 的差異.png](http://user-image.logdown.io/user/3330/blog/3407/post/146015/hUWOBYbiQNqXjm8fu5mv_memcached%20%E4%BD%BF%E7%94%A8%20add,%20set%20%E5%92%8C%20replace%20%E7%9A%84%E5%B7%AE%E7%95%B0.png)
(圖表來源：http://blog.roga.tw/2010/09/%E5%B0%8D-memcached-server-%E5%81%9A-add-set-replace-%E5%B7%AE%E5%88%A5/)

寫好之後重新 push 到 Heroku 上，就可以測試 Memcached 的效果囉!
http://cryptic-atoll-1791.herokuapp.com/index.php

假設輸入 10
![1.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/146015/cP38DVSSYuuMyiItFNzn_1.JPG)

因為沒有查找過，所以進行尋找質數的運算，並偷偷地加入的快取中
![2.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/146015/8yGe0mEcTHqT9FNqgu69_2.JPG)

回到首頁在輸入一次 10
![1.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/146015/qvlKcF75QQOFxSlhIoCK_1.JPG)

這次就 Cache Hit 了!

![3.JPG](http://user-image.logdown.io/user/3330/blog/3407/post/146015/1zaaBrEvRJyyxiLH7Rd1_3.JPG)

更多關於 Heroku 的使用，請見:
1. https://www.heroku.com/about
2. http://www.inside.com.tw/2010/09/20/heroku
