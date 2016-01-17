---
layout: post
title: '[Firefox OS] Flashing Tablet (Contribution Program)'
date: 2014-12-12 22:30
comments: true
categories: 
---

剛收到 TCP (Tablet Contribution Program)的平板
查看一下資訊
韌體版本是 Flatfish_20140112 的(末兩碼我忘了)
作業系統是 1.x.x.x 版本
<!--more-->
要升級 OS 
首先要照 `https://wiki.mozilla.org/FirefoxOS/TCP/Flashing_the_Flatfish_bootloader` 先刷 bootloader
我再 Mac OS X 10.10 上：
1. 下載 LiveSuite for Mac
2. 解壓縮後解開 LiveSuite 並執行
3. 啟動 LiveSuite
4. 下載  known-working build files (img files)
5. 在 LiveSuite 中選擇 .img
6. 關閉平板的電源，然後先將 USB 接上平板，但不要接上電腦
7. 長按住音量鍵的 (-)，然後將 USB 另一頭接上電腦，此時應該會看到一個彈跳視窗問你要 format 嗎？選擇 Yes
	 (沒有的話重複按下電源鍵大約 10 次，我的沒有這個狀況)
8. 接著等待 Process 跑完顯示 success，平板會自動重開機，此時你可以放開音量鍵並關閉 LiveSuite 了
9. 平板畫面會停在 FASTBOOT，接著你就可以開始刷 OS
(如果累了可以先將平板關機，大丈夫！重新開機還是會停在 FASTBOOT 字樣等你刷 OS，是不是反而覺得要是不會刷了就等於刷壞了這台...)

目前在 Mac 上還不能刷 OS，所以我還是找了一台 Windows 來用
https://wiki.mozilla.org/FirefoxOS/TCP/Flashing_your_device/
1. 接上電腦後，有可能抓不到 Android 驅動，可以先按照[這裡](https://wiki.mozilla.org/FirefoxOS/TCP/Installing_USB_Drivers_on_Windows)去下載驅動程式安裝
![擷取.PNG](http://user-image.logdown.io/user/3330/blog/3407/post/245944/o3msQWzS3K6bNjS2KWPA_%E6%93%B7%E5%8F%96.PNG)

2. 下載[這包](http://test1.manichord.com/moz-tcp/ADB-Fastboot-and-Scripts.zip)，解壓縮後，再到[這裡](https://www.dropbox.com/sh/b2py1btcwstqldl/AABblbq_csa1IHQwdvLdfptTa)下載最新的 build files (至目前為止最後更新為 20141212)，解壓縮後的東西都跟前面的 ADB-Fastboot-and-script 內的東西放在同一目錄下面
3. 雙擊執行 `flash.bat` 這個批次檔案，沒有錯誤的話正常來說需要等個幾分鐘，就會完成刷新 OS 的作業，並自動重新開機，進入 Firefox OS 最新版囉！

![2014-12-13-00-38-47.png](http://user-image.logdown.io/user/3330/blog/3407/post/245944/pAx0wFGaSVmMQYDR3BaS_2014-12-13-00-38-47.png)
作業系統版本：2.2.0.0-prerelease
韌體版本：flatfish_20141212-0135
硬體版本：flatfish
Build Number：20141212
![2014-12-13-00-39-40.png](http://user-image.logdown.io/user/3330/blog/3407/post/245944/XArOQ5gGT92yFRIUiDNV_2014-12-13-00-39-40.png)
