title: 先有雞還是先有蛋？Compiler vs Program
date: 2012-02-22 20:11:00
tags: [Computer Science]
---

  

<div class="MsoNormal" style="text-indent: 24.0pt;"><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">這學期準備要修</span> <span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">編譯器設計，我想到一個之前逢甲資工的老頭問我的一個問題，同時這也是他們編譯器老師問的問題：</span></div>

<div class="MsoNormal" style="text-indent: 24.0pt;"><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">  
</span></div>

<div class="MsoNormal" style="text-indent: 24.0pt;">**<span style="color: red; font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">先有</span> <span lang="EN-US" style="color: red;">Compiler</span> <span style="color: red; font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">還是先有程式</span>**<span lang="EN-US" style="color: red;">**?**</span></div>

<div class="MsoNormal" style="text-indent: 24.0pt;"><span lang="EN-US" style="color: red;"></span></div>

<div class="MsoNormal" style="text-indent: 24.0pt;"><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">其實同樣的問題也出現在作業系統上面，因為作業系統也是由程式所設計出來的，例如</span><span lang="EN-US">UNIX</span><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">就是用</span><span lang="EN-US">C</span><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">語言所編寫出來的。</span></div>

<div class="MsoNormal" style="text-indent: 24.0pt;"><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">  
</span></div>

<div class="MsoNormal" style="text-indent: 24.0pt;"><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">針對這個問題我找了為基百科和一些網頁資料，**我認為應該是先有程式，才有編譯器**，因為去看電腦發展的歷史，很早期的電腦</span><span lang="EN-US">(</span><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">真的是很早期</span><span lang="EN-US">)</span><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">，或是更精確一點說是計算機，其實是沒有</span><span lang="EN-US">”</span><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">程式</span><span lang="EN-US">”</span><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">的，是以純機械原理模擬出運算能力，而晶體管</span><span lang="EN-US">(transistor)</span><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">發明以後，機械進入的電子的時代，電子電機工程開始興起，也就產生了數位系統。</span></div>

<div class="MsoNormal" style="text-indent: 24.0pt;"><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">  
</span></div>

<div class="MsoNormal" style="text-indent: 24.0pt;"><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">第一次是聽補教界的名師洪逸在課堂上說的，後來在</span><span lang="EN-US"><**Pirate of Silicon Valley**></span><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">中看到比爾蓋茲和賈伯斯他們真的是這樣寫程式而印象深刻，後來發展出的打洞卡</span><span lang="EN-US">(Punch Card)</span><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">，電腦先輩們都必須利用打卡的方式控制機器，而這也就是最早的程式語言，也就是為什麼影片中兩位大老會想要說服當時的電腦大廠接受他們開發的作業系統，作業系統本身也是程式，也是由程式語言創作出來的，基於這個概念，因此編譯器也是後來才有的。</span></div>

<div class="MsoNormal" style="text-indent: 24.0pt;"><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">  
</span></div>

<div class="MsoNormal" style="text-indent: 24.0pt;"><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">另一個可以支持這個說法的還有一點，那就是高階程式語言是在後期才出現的，早期的電腦由打卡控制提升到指令控制時，幾乎都是接近於機器碼的組合語言</span><span lang="EN-US">(Assembly Language)</span><span style="font-family: &quot;新細明體&quot;,&quot;serif&quot;; mso-ascii-font-family: Calibri; mso-hansi-font-family: Calibri;">，而高階語言經過編譯器編譯以後都是轉譯成組合語言，再轉譯成機器碼，這也就是為什麼組合語言比較難學，卻也是最直接能與硬體做互動的原因。</span></div>