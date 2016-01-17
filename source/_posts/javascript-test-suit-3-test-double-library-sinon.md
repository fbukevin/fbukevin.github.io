---
layout: post
title: '[JavaScript] Test Suit 3 - Test Double Library - Sinon'
date: 2015-01-07 15:51
comments: true
categories: 
---
# Install 

* `npm install sinon`
* 相依於專案
<!--more-->
# Intro
Sinon 主要是用來作 unit test 上測試案例實體的區隔，像是 mock object 這樣的應用，也就是建立測試會用到的實體(例如裝置、呼叫到的函數)，如此一來測試時就可以斬斷相依性，單獨測試某個部分

Sinon 有三大物件：spy、stub、mock，分別是 test double 中的三種替身方法：Test Spy、Test Stub、Mock Object
* Spy：把物件或函數包起來『監視』。例如：`sinon.spy(math, "power");` 監視  math.power 這個 function，然後在後面當呼叫 math.power() 後，就可以查看函數的相關訊息：

```
sinon.spy(math, "power");	// 監視 math.power()

...呼叫過 math.power()...

math.power.callCount > 1; // 查看函數被呼叫的次數
math.power.withArgs("xxx").calledOnce; // 該函數是否被 xxx 呼叫過一次  
math.power.restore(); // 取消監視
```
* Stub：主要用來切割相依性，讓要測試的單元不受其他單元影響。以下為例，我們只是要測試 math.power 的功能，是否能正確運作(例如正確返回值)，如果還要去想說 math.power 可能需要給定什麼參數才能滿足其呼叫的其他函數，就被相依性困住了，因此 stub 這樣用就可以在測試 math.power 時忽略掉 math.power 實際上會呼叫到的其他函數，或使用到的其他物件

```
var stub = sinon.stub(); 				  // 建立 stub 物件	
var stub = sinon.stub(math, "power"); 	// 將 math.power() 替換成為 stub 物件
var stub = sinon.stub(math, "power"， function(){
										// 用 function 替換
										}); 
	
stub.returns(10);	// stub() 總是 return 10
stub(); 			// 呼叫 stub()

stub.throws("xxx"); // stub() 總是 throw "xxx"
stub(); 

stub.withArgs(1).returns(10);	// 當 stub(1) 時 return 10
stub(1); 

stub.restore();  // 用 stub.restore() 或 math.power.restore() 還原物件
```
在 sinon 中，stub 也具有 spy 的功能，因此可以使用 spy 的方法，例如 callCount
* Mock：= Spy + Stub + 可以在執行測試前設定預期結果，最後檢查 mock obejct 是否有照計畫執行。如下例子中，我們一開始建立了一個 math 物件，因為不像 spy 或 stub 是用我們真正要側的 math 物件，所以是 mock 的 object

```		
/* 建立 mock object */
var math = { ...	};
var mock = sinon.mock(math);
	
/* 設定 math.power(10) 預期要有 3 次 */
mock.expect("power").atLeast(3).withArgs(10); 
	...
mock.verify(); 	// 檢查現在的 math 是否與其條件
mock.restore(); // 復原物件
```

# Usage
## 同一測試三種版本
### Spies
```
1 // Function under test
2 function once(fn) {
3    var returnValue, called = false;
4    return function () {
5        if (!called) {
6            called = true;
7            returnValue = fn.apply(this, arguments);
8        }
9        return returnValue;
10    };
11 }
12
13 it("calls the original function", function () {
14    var spy = sinon.spy();
15    var proxy = once(spy);
16
17    proxy();
18
19    assert(spy.called);
20 });
```
這樣寫的目的，就是在 line 17 先呼叫一次 once，傳入的 spy 物件在 once 中被使用，因此可以在後面 line 19 去查看 once 是否有被呼叫過(在此 spy 被使用過等效於 once 被呼叫)

### Stubs
```
1 // Function under test
2 function once(fn) {
3    var returnValue, called = false;
4    return function () {
5        if (!called) {
6            called = true;
7            returnValue = fn.apply(this, arguments);
8        }
9        return returnValue;
10    };
11 }
12
13 it("returns the return value from the original function", function () {
14    var stub = sinon.stub().returns(42);
15    var proxy = once(stub);
16
17    assert.equals(proxy(), 42);
18 });
```
這樣寫就是用 stub 替換掉實際要傳入 once() 的物件，並且設定 stub 總是 return 42

### Mocks
```
1 // Function under test
2 function once(fn) {
3    var returnValue, called = false;
4    return function () {
5        if (!called) {
6            called = true;
7            returnValue = fn.apply(this, arguments);
8        }
9        return returnValue;
10    };
11 }
12
13 it("returns the return value from the original function", function () {
14    var myAPI = { method: function () {} };
15    var mock = sinon.mock(myAPI);
16    mock.expects("method").once().returns(42);  // set expect behavior
17
18    var proxy = once(myAPI.method);		// register
19
20    assert.equals(proxy(), 42);			// invoke and test return value
21    mock.verify();						// verify expected behavior 
22 });
```
在 line 14-15 我建立了一個 mock object，這個 mock object 有一個 function 叫做 method，我們設定它預期應該要以 method 為參數執行 once 並且回傳 42

跟 stub 不同的是，我們可以在最後 line 22 的地方去驗證這個 mock object 是否真的照著預期的執行

## Use with Mocha and Chai
跟 mocha 和 chai 一起用的方法如下範例：
```
/* describe 與 it 即 mocha 方法 */
describe("mocha-chai-sino", function(){
	it("calls the original function", function () {
   		var callback = sinon.spy();		// 建立 sinon.spy 物件
    	var proxy = once(callback);

	    proxy();

   		 assert(callback.called);		 	// 使用 assert 方法，可替換成 chai 的 api
    })
});
```
完整簡單測試：
```
  var sinon = require('sinon')
  var assert = require('assert')
   
  /* function to be test */
  function once(fn) { 
     var returnValue, called = false;
     return function () {
        if (!called) {
           called = true;
           returnValue = fn.apply(this, arguments);
       }
        return returnValue;
     };
  }
  
  /* test code */
  describe("mocha-chai-sino", function(){
     it("calls the original Functionn", function () {
        var callback = sinon.spy();// 建立 sinon.spy 物件
        var proxy = once(callback);
        
        proxy();
        
        assert(callback.called); // 使用 assert 方法，可替換成 chai 的 api
     })
  });
```
測試結果：
```
  mocha-chai-sino
    ✓ calls the original Functionn 


  1 passing (6ms)
```
