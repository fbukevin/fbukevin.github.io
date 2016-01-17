title: Ubuntu Server 12.04 LTS 設定 iptables 實現 NAT Server
date: 2014-02-26 16:19:00
tags: [Network,Network Management,Operating System]
---

  
情境：實驗室的 AP 原本有一個實體 IP，由於想讓實驗室其他設備也可以有網路但是不要佔用實體 IP，所以想架一個 NAT Server  

環境與 IP 配置：  

NAT Server: Ubuntu 12.04.3 LTS (GNU/Linux 3.8.0-29-generic x86_64)  
<span class="Apple-tab-span" style="white-space: pre;"></span>-eth0: 對外，有一實體 IP (140.xxx.xxx.xxx)  
<span class="Apple-tab-span" style="white-space: pre;"></span>-eth1: 對內，有一虛擬 IP (10.0.10.1)<span class="Apple-tab-span" style="white-space: pre;"></span>  
                  [不用 192.168.x.x 或 173.16.xxx.xxx 沒有特別原因]  

AP: TP-LINK TL-WR940N  
<span class="Apple-tab-span" style="white-space: pre;"></span>-WAN: 對外，連接至 NAT Server 10.0.10.2  
<span class="Apple-tab-span" style="white-space: pre;"></span>-LAN: 對內，DHCP 派發至各設備 192.168.x.x  

[閱讀更多 »](http://veckcode.blogspot.com/2014/02/ubuntu-server-1204-lts-iptables-nat.html#more)