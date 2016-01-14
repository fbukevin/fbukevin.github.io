---
layout: post
title: 'LXC Template Problem and Solution on Mint 16'
date: 2014-05-20 13:01
comments: true
categories: [LXC, Mint]
---
我安裝的 Linux Mint 版本是 16 MATE

在使用 ```apt-get install lxc``` 安裝好 LXC 以後

按照網路教學就要直接建立一個新的 VM

所以我用 ```lxc-create -t ubuntu -n test-lxc```

但是一直出現以下的錯誤訊息：

```
lxc-create: No such file or directory - bad template: ubuntu

lxc-create: bad template: ubuntu
```

上網 Google 不太到這樣的問題，最終在 PTT 的 Linux 板上問得 soom 大大的建議看法是沒有 lxc-template

Mint 下好像除了安裝 lxc， 還要安裝 lxc-template 和 debootstrap  兩個套件

安裝好以後再下一次 ```lxc-create -t ubuntu -n test-lxc``` 就可以了
