---
layout: post
title: 'LXC Start Problem and Solution on Mint'
date: 2014-05-20 15:05
comments: true
categories: [LXC, KVM, Mint, docker]
---
解決了在 Mint 上無法找到 Template 的問題，接著建立好一個 VM，就準備要啟動它了！

但是就在期待中輸入  ```lxc-start -n test-lxc -d```		( -d : launch as daemon)

竟然出現了：
```
lxc-start: command get_init_pid failed to receive response
```

以為只是某個 Calling 失敗，所以還是試著用 lxc-console 連看看，果然是   ```test-lxc is not running```

同樣是 PTT 上 soom 大大提供的資料，在 [The Linux Mint  Distribution](https://launchpad.net/linuxmint) 網站  
有人提報了這個問題：https://bugs.launchpad.net/linuxmint/+bug/1257109

一樣是相依套件的問題，所以額外在安裝了：
```
sudo apt-get install bridge-utils cgroup-lite cloud-image-utils distro-info distro-info-data euca2ools libaio1 libboost-thread1.53.0 liblxc0 librados2 librbd1 libseccomp1 python-boto python-distro-info python-m2crypto python3-lxc qemu-utils sharutils
```

如此就成功 launch 並且可以連入 VM 了！

![Terminal_001.png](http://user-image.logdown.io/user/3330/blog/3407/post/200540/mEbfT0d7S6ijzllI70xa_Terminal_001.png)

相關連結：
    - KVM：http://www.linux-kvm.org/page/Main_Page
    - LXC：https://linuxcontainers.org/
    - Docker：https://www.docker.io/
    - Linux KVM 研究室：http://linuxkvm.blogspot.tw/
	  - Mr. Q - [Linux Container (lxc) - 物美價廉的 Virtualization](http://littleqnote.blogspot.tw/2012/11/linux-container-lxc-virtualization.html)
