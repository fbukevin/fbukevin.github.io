---
layout: post
title: 'Install Maven Plugin to ADT Bundle Eclipse(PDE) '
date: 2014-08-01 17:15
comments: true
categories: 
---
我是下載 ADT Bundle 版本的 Eclipse
我想要安裝 Maven Plugin 
於是我找到了 m2e (maven to eclipse) 的安裝網址：http://download.eclipse.org/technology/m2e/releases/
到了 Eclipse 的 Help/Install New Software 的地方，將網址填入 Work with 後按下 Enter
就可以找到 m2e 的安裝套件
<!--more-->
但是就在 next 之後，Eclipse 去檢查 dependency 發現有個沒有安裝：
```
Missing requirement: Maven Integration for Eclipse 1.5.0.20140606-0033 (org.eclipse.m2e.core 1.5.0.20140606-0033) requires 'bundle com.google.guava [14.0.1,16.0.0)' but it could not be found
```

解決方法，先在 Install New Software 的 Work with 輸入：http://download.eclipse.org/releases/luna/ 
按確定後將把 luna 加入 Available Sites
找到套件就好，不需要安裝，接著就可以直接在 Work with 那邊輸入 m2e 找到剛剛加入 Available Sites 的 m2e 網址
就可以安裝了！

