---
layout: post
title: '[JavaScript] Test Suite 2 - Test Cases Library - Chai'
date: 2015-01-07 11:07
comments: true
categories: 
---

#Install
1. `npm install chai`, bundle with package
2. 官網補充：dependency and mocha
![dep.png](http://user-image.logdown.io/user/3330/blog/3407/post/248476/Cijx7PR1RSe5PT34tPZe_dep.png)


#Intro
在 mocha 中，我們有這樣一段程式：
```
describe('Array', function(){    
   describe('#indexOf()', function(){
      it('should return -1 when the value is not present', function(){  
         assert.equal(-1, [1, 2, 3].indexOf(5)) 
         assert.equal(-1, [1, 2, 3].indexOf(0))
      })
   })
});
```

其中 node 本身雖然也提供 assert，但是 chai 專門針對這部份提供更多 API，以下是官網的說明：
```	
The assert style is exposed through assert interface. 
This provides the classic assert-dot notation, similiar to that packaged with node.js. 
This assert module, however, provides several additional tests and is browser compatible.
```
 
#Usage
##Assert
```
 var assert = require('chai').assert
  , foo = 'bar'
  , beverages = { tea: [ 'chai', 'matcha', 'oolong' ] };

describe("try chai with mocha", function(){
     it("typeOf", function(){
        assert.typeOf(foo, 'string', 'foo is a string');
     })
  
     it("chai's equal", function(){
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
(因為是不同的 test case，所以一個 it 只會執行一種 assert，因此才要分開不同 it)

存檔成 test.js 後就可以用 mocha 來執行測試了:
```
 try chai with mocha
    ✓ typeOf 
    ✓ chai's equal 
    1) lengthOf
    ✓ lengthOf in array 


  3 passing (9ms)
  1 failing

  1) try chai with mocha lengthOf:
     AssertionError: foo`s value has a length of 3: expected 'bar' to have a length of 4 but got 3
      at Function.assert.lengthOf (/Users/veck/Desktop/JSTest/2_mocha_chai/node_modules/chai/lib/chai/interface/assert.js:890:37)
      at Context.<anonymous> (/Users/veck/Desktop/JSTest/2_mocha_chai/test.js:15:14)
      at callFn (/Users/veck/.nvm/v0.10.35/lib/node_modules/mocha/lib/runnable.js:251:21)
      at Test.Runnable.run (/Users/veck/.nvm/v0.10.35/lib/node_modules/mocha/lib/runnable.js:244:7)
      at Runner.runTest (/Users/veck/.nvm/v0.10.35/lib/node_modules/mocha/lib/runner.js:374:10)
      at /Users/veck/.nvm/v0.10.35/lib/node_modules/mocha/lib/runner.js:452:12
      at next (/Users/veck/.nvm/v0.10.35/lib/node_modules/mocha/lib/runner.js:299:14)
      at /Users/veck/.nvm/v0.10.35/lib/node_modules/mocha/lib/runner.js:309:7
      at next (/Users/veck/.nvm/v0.10.35/lib/node_modules/mocha/lib/runner.js:248:23)
      at Object._onImmediate (/Users/veck/.nvm/v0.10.35/lib/node_modules/mocha/lib/runner.js:276:5)
      at processImmediate [as _immediateCallback] (timers.js:354:15)
```

##Expect
BDD(behavior driven development) 的開發模式產生了兩種常用的測試方法：`expect` 和 `should`

(以下省略 mocha 部分程式碼)
```
var expect = require('chai').expect
  , foo = 'bar'
  , beverages = { tea: [ 'chai', 'matcha', 'oolong' ] };

expect(foo).to.be.a('string');
expect(foo).to.equal('bar');
expect(foo).to.have.length(3);
expect(beverages).to.have.property('tea').with.length(3);
```

##Should
`should` 跟 `expect` 基本上一樣，差別在於方法的實作上，expect 是做成 global function，而 should 是 class property，也就是物件可以用 property 的方式呼叫 expect 的測試案例

還有一點就是，`expect` 引用是用 `require('chai').expect`，但 `should` 是用 `require('chai').should()`

NOTICE: This style has some issues when used Internet Explorer, so be aware of browser compatibility.
```
var should = require('chai').should() //actually call the the function
  , foo = 'bar'
  , beverages = { tea: [ 'chai', 'matcha', 'oolong' ] };

foo.should.be.a('string');
foo.should.equal('bar');
foo.should.have.length(3);
beverages.should.have.property('tea').with.length(3);
```

#Plugin
Chai 可以透過下面的方法來取用外部工具
```
chai.use(_chai, util){
	// your helpers here
}
```