---
layout: post
title: '[JavaScript] nodemailer'
date: 2015-09-11 15:15
comments: true
categories: [javascript, nodejs]
---
這是一個簡單易用的 Node.js 寄信模組，因為太容易使用，本文只是一個使用紀錄，官網的範例已足以滿足大家~

[nodemailer](http://www.nodemailer.com/)

# 安裝套件

`npm install nodemailer`
<!--more-->
# 寫程式

```javascript
var nodemailer = require('nodemailer');

// 這個模組是透過 STMP 協定來做信件傳輸，所以需要設定代理伺服器
var transporter = nodemailer.createTransport({		// 建立 sender 物件: transporter
    service: 'Gmail',
    auth: {
        user: 'fbukevin@gmail.com',
        pass: '*******'
    }
});

// 設定 mail 選項
var mailOptions = {
    from: 'fbukevin@plsm.nccu.edu.tw',
    to: 'fbukevin@gmail.com', // 若有多個收件者，請在 ''  中用 ',' 點隔開
    subject: 'Test nodemailer',
    text: 'hello world',
    html: '<b>What does this option use?</b>' // 我一開始不知道這個是做什麼的
};

// 傳送
transporter.sendMail(mailOptions, function(error, info){
    if(error){
        console.log(error);
    }else{
        console.log('Message sent: ' + info.response);
    }
});
```

## 傳送成功的回傳訊息
```
fbukevin@plsm:~/test/nodemailer$ node test.js
Message sent: 250 2.0.0 OK 1441955541 sl7sm343448pbc.54 - gsmtp
```
