---
layout: post
title: '[Python] Executable Python'
date: 2015-01-29 02:41
comments: true
categories: 
---
繼 node.js 後，我也想讓 Python 的程式碼可以不需要輸入 "python" 就可以執行，找到大部分的作法，這是在 UNIX/Linux 和 Mac 上的說明
<!--more-->
1. 寫個簡單的 exe.py
```python
#!/usr/bin/env python
if __name__ == "__main__":
print("Execute Python without typing \"python\")
```
2. 在終端機輸入 `chmod +x exe.py` 修改權限
3. 答啦！
```
 ~/Desktop -->./exe.py 
Execute Python without typing "python"
```

甚至也不用打 "./" 了！

如果想連附檔名都不要，有篇[教學](http://sebug.net/paper/python/ch03s05.html)說可以把檔名改成 exe，也就是拿掉附檔名，而系統會自己知道要用程式碼第一行指定的那個直譯器來執行這個檔案 `~/Desktop -->exe`
![螢幕快照 2015-01-29 上午3.08.56.png](http://user-image.logdown.io/user/3330/blog/3407/post/252814/k5oRwu97Qeqzv62Es8b5_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202015-01-29%20%E4%B8%8A%E5%8D%883.08.56.png)

當然，你也可以把 exe 加入 PATH 中，這樣就可以到處都直接執行它了～

有個問題是，Python 利用 pip 來管理和發佈套件，在 node.js 那邊我們用 npm install -g <package> 就可以安裝成 global command，不需要另外設定權限，那如果今天需要設定權限，那給人安裝後，是不是應該寫 shell script 來設定呢？

還沒研究有沒有人用 pip 來安裝成 command tool，pip 好像主要是拿來安裝 Python module package，如果用 shell script 來設定路徑好像就不是 pip 的用途了

原文參考：http://sebug.net/paper/python/ch03s05.html