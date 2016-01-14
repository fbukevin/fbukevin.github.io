---
layout: post
title: '[JavaScript] Test Suit 1 - Test Framework - Mocha'
date: 2015-01-07 10:15
comments: true
categories: 
---

#Install and use
1. `npm install -g mocha` 安裝完以後，就可以直接用 mocha 指定來執行測試
2. 執行測試，mocha 會自動執行檔名為 test.js 的檔案，如果沒有會出現錯誤，你可以用 `mocha <testfile>` 來執行測試

#Intro 
Mocha 是一個 JavaScript 的 test framework，它提供用來組織 unit test 的 API，並且執行 test

#Usage
```
var assert = require("assert")
describe('Array', function(){
  describe('#indexOf()', function(){
    it('should return -1 when the value is not present', function(){
      assert.equal(-1, [1,2,3].indexOf(5));
      assert.equal(-1, [1,2,3].indexOf(0));
    })
  })
})
```
###require
`var assert = require('assert')` 

這個模組其實是 node.js 內建的，提供 assertion 相關 API

mocha 可以認得 describe()、it() 等函式，不需要 require

###describe
`describe(moduleName, testDetails)`

形成一個測試區塊

`moduleName` 是要用到的測試模組名稱，那是測試人員隨便取的

`testDetails` 放置測試內容，以 callback 實作

###it
`it (info, function)`

最基本的測試單元，通常一個 it 對應一個實際的 test case

`info` 是輸出訊息

`function` 放是這種 test assertion

#Asynchronize
```
fs = require('fs');
describe('File', function(){
    describe('#readFile()', function(){
        it('should read test.ls without error', function(done){
            fs.readFile('test.ls', function(err){
                if (err) throw err;
                done();
            });
        })
    })
})
```
`done()` 用來指示抵達 callback 串的最深處，開始要一層層返回

这里可能会有个疑问，假如我有两个异步函数（两条分叉的回调链），那我应该在哪里加 done() 呢？实际上这个时候就不应该在一个 it 里面存在两个要测试的函数，事实上 "一个 it 里面只能调用一次 done "，当你调用多次 done 的话 mocha 会抛出错误。所以应该类似这样：(這部份是大陸網友加上去的，官網沒有提到這個，但很實用)
```
fs = require('fs');
describe('File', function(){
    describe('#readFile()', function(){
        it('should read test.ls without error', function(done){
            fs.readFile('test.ls', function(err){
                if (err) throw err;
                done();
            });
        })
        it('should read test.js without error', function(done){
            fs.readFile('test.js', function(err){
                if (err) throw err;
                done();
            });
        })
    })
})
```
像是以下的多個 assertion，因為 test case 不同，因此只有 typeOf 會被執行
```
describe("try chai with mocha", function(){
        assert.typeOf(foo, 'string', 'foo is a string');
        assert.equal(foo, 'bar', 'foo equal `bar`');
        assert.lengthOf(foo, 4, 'foo`s value has a length of 3');
        assert.lengthOf(beverages.tea, 3, 'beverages has 3 types of tea');
  });
```
要改成這樣才會每個都執行到：
```
describe("try chai with mocha", function(){
     it("typeOf", function(){
        assert.typeOf(foo, 'string', 'foo is a string');
     })
  
     it("chai'a equal", function(){
         assert.equal(foo, 'bar', 'foo equal `bar`');
     })
  
     it("lengthOf", function(){
        assert.lengthOf(foo, 4, 'foo`s value has a length of 3');
     })
  
     it("lengthOf in array", function(){
        assert.lengthOf(beverages.tea, 3, 'beverages has 3 types of tea');
     })
  });
```

#Hook
```
describe('hooks', function() {
  before(function() {
    // 全部測試開始前就執行這裡
  })
  after(function(){
    // 全部測試結束後才執行這裡
  })
  beforeEach(function(){
    // 每個測試開始前都執行這裡
  })
  afterEach(function(){
    // 每個測試結束後都執行這裡
  })
  
  /* test cases */
})
```

#Pending
就是空著 callback 函數，mocha 會 pass 這段測試，一般用在你是負責寫好框架讓別人去實作測試案例，或者測試細節還沒完全實作好(類似 mock object 的想法)
```
describe('Array', function(){
    describe('#indexOf()', function(){
        it('should return -1 when the value is not present', function(){
        })
    })
});
```


#Exclusive & Inclusive
```
fs = require('fs');
describe('File', function(){
    describe('#readFile()', function(){
    	 /* skip 的 case */
        it.skip('should read test.ls without error', function(done){
            fs.readFile('test.ls', function(err){
                if (err) throw err;
                done();
            });
        })
        
        /* only 的 case */
        it('should read test.js without error', function(done){
        })
    })
})
```
這段程式碼只有 only 的會被執行，it.skip 會被忽略。每個函數中只能有一個 only，如果把 only 和 skip 一起用，因為 only 會遮蔽掉 skip 的效果，導致沒什麼效果

#BDD & TDD
* BDD: behavior driven development
* TDD: test driven development

這兩者主要的差別就是在寫測試時的思考角度不同

mocha 預設是採用 Behavior Driven Develop (BDD)，要想用 TDD 的測試需要加上參數，如:

`mocha -u tdd test.js`

BDD 就像上面的使用 describe() 和 it() 來構建測試程式碼，而 TDD 使用 suite() 和 test() 來組織測試

#Final
基本 API 就是這樣，官網沒有過多文件，而 mocha 有些有趣的用法也請見官網

#Reference
* 初识 mocha in NodeJS - https://cnodejs.org/topic/516526766d38277306c7d277