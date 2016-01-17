---
layout: post
title: 'Compare of Xen, KVM, LXC and Traditional VM'
date: 2014-05-20 17:27
comments: true
categories: [LXC, KVM, XEN, Container]
---
\* 以下將 VMware、Virtual Box、Virtual PC 歸類為 Traditional Vitual Machine，簡稱 TVM 

```
TVM 和 其他虛擬化技術 的最主要差異是主系統的資源共享
```
<!--more-->
- TVM 這是完整一個系統，這裡的系統包含了所有軟體模擬出來的硬體設備，因此他的執行效能最差，但是能夠完整模擬出一個不同於主系統的環境
![螢幕快照 2014-05-20 下午6.02.35.png](http://user-image.logdown.io/user/3330/blog/3407/post/200566/ZyW2Z6keRD648EdlNBXU_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-05-20%20%E4%B8%8B%E5%8D%886.02.35.png)


- Xen 是在 Linux 環境下最早出來的虛擬化技術，這是在硬體與 Linux 核心之間插入一個 Xen 程序，讓開機時的 bootloader 原本是要載入 Linux Kernel Code，改成 loading Xen code，而 Linux Kernel 和其他 VM 則是由 Xen 來管理
![螢幕快照 2014-05-20 下午6.00.35.png](http://user-image.logdown.io/user/3330/blog/3407/post/200566/iG59YD7lShmmPfy5ktz5_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-05-20%20%E4%B8%8B%E5%8D%886.00.35.png)

- LXC 是緊接著出來的技術，由 IBM 創立，後來才納入 Linux Kernel)，這個作法是在主系統的 Processes 中，將虛擬機的 process"es" 偽裝成主系統的 process，讓主系統的 OS 將之加入 Process Scheduling 中

會說是偽裝，是因為主系統中本身會有一套屬於作業系統的 Process，這些 Process 也會在虛擬機的系統中存在，例如 Linux 的 init (PID = 1)，如果直接將虛擬機的 Process 插入主系統的排成，可能造成系統錯亂，因此 container 會將虛擬機的 process 偽裝成其他號碼的 process 後才加入排程

![螢幕快照 2014-05-20 下午6.00.28.png](http://user-image.logdown.io/user/3330/blog/3407/post/200566/XtXDLjNSRQi6xZao7hfg_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-05-20%20%E4%B8%8B%E5%8D%886.00.28.png)

container 要求的虛擬機環境要跟主系統一樣，例如你在 Ubuntu 上安裝並建立一個 container，則 container 的環境就只能是 Ubuntu (因此 ```-t ubuntu``` 只是將一個已經包裝好的 ubuntu template (image) 下載下來)，適合 hadoop 那樣需要相同平台的

- KVM 是最新的虛擬化技術，這跟 TVM 的架構有點像，不同的在於，這個技術的虛擬機器上所有的 Process 都是由主系統的 Linux Kernel 管理，而 TVM 則是由虛擬系統自己管理，而且 TVM 需要用軟體模擬硬體(增加 Process)，所以效能較差，KVM 則因為是跟主系統共享資源，因此不會增加硬體模擬的負擔，效能較好

![螢幕快照 2014-05-20 下午6.03.48.png](http://user-image.logdown.io/user/3330/blog/3407/post/200566/HvpwufIWRMHA9FvXJAZg_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-05-20%20%E4%B8%8B%E5%8D%886.03.48.png)


從效能上來看，TVM 架構下的主系統(host)需要切割實體資源給 Virtual Machine，這些資源就被 Virtaul Machine 佔用了；而 KVM 和 LXC 因為是共享 host 的實體資源，資源的共享就跟 process 或 thread 的佔用與釋放一樣，不會有永久持有，所以硬體資源可以更充分利用，當一個機器(host 或 vm)需要較多資源時，主系統就可以協調另一機器的資源來使用

另一方面，KVM 和 LXC 因為共享主系統資源，所以不需要將檔案從主系統複製或移動到虛擬機器上，即可在虛擬機上存取或運行，如此一來對於要做快速測試的開發專案而言，可以達到快速測試或佈署的目的

在進一步拿目前效能最好的 KVM 跟 LXC 做比較，KVM 的效能略遜於 LXC，因為它是完整的一個作業系統，有自己完整同主系統的 Process，但是 LXC 是一個 container 自己就是一個 process，因此使用的資源較少，但是 LXC 相較上來說彈性較差，因為它要求與主系統相同的環境

額外補充資料：
- [KVM](http://www.linux-kvm.org/page/Main_Page)：Kernel-bases Virtual Machine
- [LXC](https://linuxcontainers.org/)：LinuX Container
- [Xen](http://www.xenproject.org/)