---
layout: post
title: '常用 debug 工具筆記'
date: 2016-01-17 20:20
comments: true
categories: [javascript, nodejs]
---

# Python

## logger 

```python
import logging

logging.basicConfig(filename="") 
logging.error('...')
```

<!--more-->

## elapsed_time 

```python
import time (單位：sec)

start = time.time()
elapsed_time = time.time() - start 
```
## timestamp 
    
```python
import time

time.strftime("%Y-%m-%d %H:%M:%s", time.localtime(time.time()))
```

## wait

```python
import time

time.sleep(<second>)
```

## send GET request

```
import requests

requests.get(<url>)
```

# JavaScript

* contain

	1. logger
	2. timestamp
	3. elapsed_time
	4. mailer
	5. facebook login

```javascript
/* veck's module for web application */

var log = require('npmlog')
	, fs = require('fs')
	, mailer = require('nodemailer');

log.__proto__.setLogFile = function(path){
	log.stream = fs.createWriteStream(path, {flags: 'a'});	
}

/* timestamp */
log.__proto__.getLogTime = function(){
	var date = new Date();
	var day = date.getFullYear() +'/'+ date.getDate() +'/'+ date.getMonth();
	var time = date.getHours() + ':' + date.getMinutes() + ':' + date.getSeconds() + '.' + date.getMilliseconds();
	return day + ' ' + time;
}
log.__proto__.getLogDate = function(){
	var date = new Date();
	return date.getFullYear() +'/'+ date.getDate() +'/'+ date.getMonth();	
}

module.exports = log;

/*******************************************************/

/* elapsed time */
// Date.now() // return milliseconds (10^-3)
start = Date.now()
elasped = (Date.now - start)/1000

/*******************************************************/

/* mailer */
var transporter = mailer.createTransport({
	service: 'ses',
	host: 'email-smtp.us-west-2.amazonaws.com',
	auth: {
  	user: '<username>',
		pass: '<password>'
	}
});
var message = '恭喜您已成功註，請點選以下連結完成註冊認證！';
transporter.sendMail({
	from: 'fbukevin@gmail.com',
  to: confirm.mail.address,
	subject: '註冊認證信',
	text: message
});

/*******************************************************/

/* facebook login */

/*
	TODO: 包成一個 module
 */	

var express = require('express');
var router = express.Router();
var log = require('log_tool');

log.setLogFile('log/auth.js.log');
log.info(log.getLogTime(), 'router index.js logging successfully');
function getRequestIP(req){
  return req.header('x-forwarded-for') || req.connection.remoteAddress;
}

function logging(req){
  log.info(log.getLogTime(), 'Request IP: ' + getRequestIP(req));
}

var passport = require('passport')
  , util = require('util')
  , FacebookStrategy = require('passport-facebook').Strategy
  , logger = require('morgan')
  , session = require('express-session')
  , bodyParser = require("body-parser")
  , cookieParser = require("cookie-parser")
  , methodOverride = require('method-override');

var FACEBOOK_APP_ID = "<FACEBOOK_APP_ID>"
var FACEBOOK_APP_SECRET = "<FACEBOOK_APP_SECRET>";

router.use(session({ secret: 'keyboard cat' }));
router.use(passport.initialize());
router.use(passport.session());

passport.serializeUser(function(user, done) {
  done(null, user);
});

passport.deserializeUser(function(obj, done) {
  done(null, obj);
});

passport.use(new FacebookStrategy({
    clientID: FACEBOOK_APP_ID,
    clientSecret: FACEBOOK_APP_SECRET,
    callbackURL: "http://localhost:3000/auth/facebook/callback",
    profileFields: ['id', 'displayName', 'photos']
  },
  function(accessToken, refreshToken, profile, done) {   
    process.nextTick(function () {
      return done(null, profile);
    });
  }
));
```
