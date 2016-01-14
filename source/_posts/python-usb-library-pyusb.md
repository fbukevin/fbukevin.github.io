---
layout: post
title: 'Python USB Library - pyusb'
date: 2014-09-25 15:46
comments: true
categories: 
---
Website: http://walac.github.io/pyusb/
GitHub: https://github.com/walac/pyusb/

目前教學只有教在 Ubuntu 和 Windows 上安裝的方法，我以 Ubuntu 為例，首先需要先有 python (應該是 builtin 了)，然後要安裝 `libusb-1.0-0`
```
$ sudo apt-get install libusb-1.0-0
```

然後下載 library，解壓縮以後，進入資料夾，輸入 `sudo python setup install`，就完成安裝了

簡單的測試 USB 連線，你需要先知道各個 USB 裝置的 `Vendor ID` 和 `Product ID`，可以用 `lsusb` 來查看：
```
~/Desktop$ lsusb
Bus 002 Device 003: ID 046d:c016 Logitech, Inc. Optical Wheel Mouse
Bus 002 Device 002: ID 8087:0020 Intel Corp. Integrated Rate Matching Hub
Bus 002 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
Bus 001 Device 024: ID 0b05:5481 ASUSTek Computer, Inc. 
Bus 001 Device 002: ID 8087:0020 Intel Corp. Integrated Rate Matching Hub
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
```
以第一個裝置 `Logitech, Inc. Optical Wheel Mouse` 為例，在 ID 後面的 046d:c016 分別對應到 Vendor ID 和 Product ID，接著我們進入 interactive shell，首先要 `import usb`，接著我們利用 usb 模組下的 core 類別的 find 方法，把剛才的兩個 id 給它 `dev = usb.core.find(idVendor=0x046d, idProduct=0xc016)`：
```
>>> import usb
>>> dev = usb.core.find(idVendor=0x046d, idProduct=0xc016)
```
然後我們就可以印出 dev 的資訊，看看是不是有抓到我們指定的 USB 裝置：
```
>>> dev
<DEVICE ID 046d:c016 on Bus 002 Address 003>
```


![螢幕快照 2014-09-25 下午3.45.16.png](http://user-image.logdown.io/user/3330/blog/3407/post/234960/qrKxqlkxSK6UQ9lTTaYF_%E8%9E%A2%E5%B9%95%E5%BF%AB%E7%85%A7%202014-09-25%20%E4%B8%8B%E5%8D%883.45.16.png)
