---
layout: post
title: '[mongoDB] Nodejs、Python 和 Ruby Driver'
date: 2015-10-28 23:26
comments: true
categories: 
---
#PyMongo 簡單查詢

```python
>>> import pymongo
>>> from pymongo import MongoClient
>>> client = MongoClient('localhost', 27017)
>>> db = client['express-wait']
>>> collection = db.waits
>>> collection.find_one()
{u'content': u'http://benchmarkjs.com/', u'_id': ObjectId('5629de95d488910889000001'), u'__v': 0}
```

reference: [https://api.mongodb.org/python/current/tutorial.html](https://api.mongodb.org/python/current/tutorial.html)

#mongojs 簡單查詢

```javascript
var mongojs = require('mongojs');
var db = mongojs('mongodb://dbuser:dbpass@host:post/db', ["waits"]);

db.waits.find(function(err, docs){
  console.log(docs);  
});
```

refence: [http://mafintosh.github.io/mongojs/](http://mafintosh.github.io/mongojs/)

#Ruby Mongo 簡單查詢

```ruby
irb(main):004:0> require "mongo"
irb(main):005:0> Mongo::Client.new(['127.0.0.1:27017'], :database => 'express-wait')
irb(main):006:0> client = Mongo::Client.new(['127.0.0.1:27017'], :database => 'express-wait')
irb(main):009:0> client[:waits].find().each do |document|
irb(main):010:1*  p document
irb(main):011:1> end
{"_id"=>BSON::ObjectId('5629de95d488910889000001'), "content"=>"http://benchmarkjs.com/", "__v"=>0}
```

reference: [https://docs.mongodb.org/ecosystem/tutorial/ruby-driver-tutorial/](https://docs.mongodb.org/ecosystem/tutorial/ruby-driver-tutorial/)
