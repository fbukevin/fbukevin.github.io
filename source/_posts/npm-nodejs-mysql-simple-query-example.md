---
layout: post
title: '[npm] Node.js MySQL 簡單查詢範例'
date: 2015-12-25 10:13
comments: true
categories: 
---
#MySQL 簡單查詢範例

##node.js

```javascript
   var mysql = require('mysql');
   var connection = mysql.createConnection({
     host: '127.0.0.1',
     port: '3306',
     user: 'root',
     password: 'root',
     database: 'nodejs'
   });
  
  connection.connect();
  
  connection.query('SELECT * FROM `test`', function(err, rows, fields){
    if(err) throw err;
    for(var r in rows){
      console.log(rows[r].id);
    }
  });
 
 connection.end();
```

在 express 的 router 中這樣用：

routers/index.js

```javascript
router.get('/', function(req, res){
	connection.query('SELECT * FROM `test`', function(err, rows, fields){
  	res.render('index', {title: rows[0].id});
  });
});
```

