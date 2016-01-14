---
layout: post
title: 'Revo.io - Quick Customize Your Vagrantfile'
date: 2014-10-30 05:08
comments: true
categories: [ruby, vagrant, Virtualization, docker, Revo]
---

![螢幕快照 2014-10-30 上午5.10.39.png](http://user-image.logdown.io/user/3330/blog/3407/post/240407/Ce9kFn2HSVWJfjy9eiPQ_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-10-30%20%E4%B8%8A%E5%8D%885.10.39.png)
[Rove.io](http://rove.io/) 這個網站可以讓你客製化你要的環境，然後幫你產生 Vagrantfile 和 Cheffile (需要另外預先安裝好 library-chef：`gem install library-chef`)，下載後解壓縮進入資料夾，輸入 `curl -L http://rove.io/ | bash`，就會自動下載 box 並安裝好你客製化的軟體 (應該跟 Docker 一樣是堆疊方式)，`vagrant ssh` 就可以連入測試了

![1.jpg](http://user-image.logdown.io/user/3330/blog/3407/post/240407/yZzhbyuXQTa1mBlR1eMD_1.jpg)
![2.jpg](http://user-image.logdown.io/user/3330/blog/3407/post/240407/LXCMMzLUQxKgRYHlNLFo_2.jpg)

After Generate：

![3.jpg](http://user-image.logdown.io/user/3330/blog/3407/post/240407/fAGMC1RGS4Omf08riZKc_3.jpg)

After `curl -L install http://revo.io | bash` finished：
NOTE：基本上過程沒有錯誤的話，curl 結束後就會完成安裝，就可以直接 `vagrant ssh` 進去了
![螢幕快照 2014-10-30 上午5.21.12.png](http://user-image.logdown.io/user/3330/blog/3407/post/240407/9Zka2W5aRO2gbZ7A3pU7_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-10-30%20%E4%B8%8A%E5%8D%885.21.12.png)
![螢幕快照 2014-10-30 上午5.21.55.png](http://user-image.logdown.io/user/3330/blog/3407/post/240407/iLqnps6IQvOA5Yyoqxb3_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-10-30%20%E4%B8%8A%E5%8D%885.21.55.png)

但是如果中途有斷掉過，你可能需要手動執行套件下載和安裝
`librarian-chef install`：
![5.jpg](http://user-image.logdown.io/user/3330/blog/3407/post/240407/5aFGRh1vRSmNQ5dJZBQi_5.jpg)


NOTE： 此時，因為 curl 已經(或可能)讓 vm 已經 run 起來，因此需要先 `vagrant halt` 才能安裝客製化的應用程式

接著要 `vagrant provision`    
這個動作才會真的 `Setting the run_list to ["recipe[apt]", "recipe[vim]", "recipe[git]", "recipe[apache2]", "recipe[mysql::server]"] from JSON`，將 chef cookbook 設定且下載的應用程式裝載 vm 中
![6.jpg](http://user-image.logdown.io/user/3330/blog/3407/post/240407/Z1fgZTSzTI26ThDtIKpb_6.jpg)


最後 `vagrant up`，然後 `vagrant ssh` 後：
![7.jpg](http://user-image.logdown.io/user/3330/blog/3407/post/240407/oeXqlBWcSalmYw2iYLLl_7.jpg)


* curl 時遇到問題：
```
/usr/local/Cellar/ruby/2.1.4/lib/ruby/2.1.0/net/http.rb:920:in `connect': SSL_connect returned=1 errno=0 state=SSLv3 read server certificate B: certificate verify failed (OpenSSL::SSL::SSLError)
```

花了很久時間嘗試，終於解決了！！！！！！！！
因為我是在 Mac 上安裝 Vagrant
原來在 Mac 上要這樣指定 SSL_CERT_FILE：`export SSL_CERT_FILE='/usr/local/etc/openssl/osx_cert.pem'`
不是指定到 `/usr/local/etc/certs/cacert.pem` 
(osx_cert.pem 是另外下載安裝的)

* vagrant up 遇到的問題：
```
Vagrant cannot forward the specified ports on this VM, since they
would collide with some other application that is already listening
on these ports. The forwarded port to 3000 is already in use
on the host machine.

To fix this, modify your current projects Vagrantfile to use another
port. Example, where '1234' would be replaced by a unique host port:

  config.vm.network :forwarded_port, guest: 3000, host: 1234

Sometimes, Vagrant will attempt to auto-correct this for you. In this
case, Vagrant was unable to. This is usually because the guest machine
is in a state which doesn't allow modifying port forwarding.
```
這表示你有沒關掉的 vargant instance，導致預設要綁定的 port 已經被某個 process 佔用了，因此請先用 `ps aux | grep vm` 來看:
```
veck            78729   1.1  5.6  3000248 471340   ??  U     4:45AM   2:08.39 /Applications/VirtualBox.app/Contents/MacOS/VBoxHeadless --comment rove-27c8af801d4c671e25f2791b7311bbe0_default_1414614223406_26774 --startvm 541cafa7-5bb3-45d7-bd27-899a824a3e74 --vrde config
```
再用 kill -9 [PID] 砍掉 Process，然後重新 `vagrant up` 就可以了
