title: Eclipse 安裝套件錯誤訊息 - Contacting Software Sites has encountered a problem
date: 2012-05-03 07:32:00
tags: [Java]
---

原因：未查證  

狀況：當你在 Eclipse 的 Install New Software 輸入套件網址，卻出現下列訊息"Contacting Software Sites has encountered a problem"，而無法安裝  

<div class="separator" style="clear: both; text-align: center;">[![](http://3.bp.blogspot.com/-AUQPuFFCf6o/T6HDF9_HwUI/AAAAAAAAASg/zanHvjApaJY/s1600/error_download.jpg)](http://3.bp.blogspot.com/-AUQPuFFCf6o/T6HDF9_HwUI/AAAAAAAAASg/zanHvjApaJY/s1600/error_download.jpg)</div>

解決方法：  
   1\. 打開你的 Eclipse安裝資料夾  
   2\. 找到 eclipse.ini 這個檔案  
   3\. 加入這行：<span style="background-color: white; font-family: Consolas, 'Bitstream Vera Sans Mono', 'Courier New', Courier, monospace; font-size: 14px; letter-spacing: 1px; line-height: 15px; text-align: left; white-space: pre;">-Djava.net.preferIPv4Stack=true</span>  
<span style="letter-spacing: 1px; line-height: 15px; white-space: pre;"><span style="font-family: inherit;">4\. 重新啟動 Eclipse，再次進入 Install New Software 就不會有這個錯誤訊息了</span></span>