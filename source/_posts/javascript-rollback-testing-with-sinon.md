---
layout: post
title: '[JavaScript] Rollback Testing with Sinon'
date: 2015-01-30 00:31
comments: true
categories: 
---
mocha, chai 和 sinon，我覺得最難的是 sinon 了，因為 mocha 只是驅動，chai 是 assert ，你給他結果值就好，sinon 考慮的是物件的『行為』，最麻煩的就是如果呼叫一個函數或建立一個物件，結果會有副作用(開檔、寫檔、修改資料庫、傳送網路資料等)，又不是像 try...catch... 會幫你 rollback 的話，你就得自己來處理，因此本篇想測試 sinon 的物件是否提供 rollback 或類似的測試方法。

複習一下概念：
* spy 是 監視，所以還是會 invoke function
* stub 是 隔離，不 invoke function，把 function 替換成 stub 物件或自定義物件函式
* mock 是直接模擬物件或函式，包含 spy 和 stub 的所有功能，而且還可以最後來驗證物件是否照預期執行

這樣看來主要嘗試就是 spy 和 stub 物件了，mock 物件繼承上述兩者的能力，就不需去嘗試

我們拿 node.js 的 fs.openSync(); 來做例子，它的功能是同步的建立一個檔案
```javascript
var sinon = require('sinon');
var assert =require('assert');
var fs = require('fs');

/**
 * test if fs.openSync() will rollback(create then delete file after test)
 * automatically with the two main kind of objects in Sinon.
 */

//Spy
describe('Spy', function(){
    it('should call open with w mode to create file', function(){
       var spy = sinon.spy(fs, "openSync");
       spy.withArgs('index.html', 'w');   // register arguments
       fs.openSync('index.html', 'w');  // call
       assert(spy.withArgs('index.html').calledOnce);
       spy.restore();
    });
});

//Stub
describe('Stub', function(){
    it('should call open with w mode to create file', function(){
        var stub = sinon.stub(fs, "openSync");
        stub.withArgs('index2.html', 'w');
        stub("index2.html", "w");
        stub.restore();
    });
});

```
本來還在想，如果兩者都不會 rollback，就要自己在 mocha 的 afterAll 去 remove file 了，但這樣的話 write 怎半？真的寫了怎麼再去 afterAll 做 rollback？尤其當我嘗試了 spy 並證實，很遺憾的，spy 還是會產生檔案，不會 rollback，所以不太適合寫建立和寫入的操作 ...

接著邊思考邊期待，stub 好像是把指定的 funtion 替換成 stub 物件，也可以自己定義要替換成的 funtion，做到相依斬斷
也許...	

緊張緊張，這麼重要的功能的測試的結果就要來了的啦！
![rollback.png](http://user-image.logdown.io/user/3330/blog/3407/post/252948/NnN91MTxThCDaGbNcRo2_rollback.png)

Yes! stub 就沒有真的建立檔案了！
不過我認為並不是 stub 有去自動做 rollback 的動作，而是因為 stub 的功能就是要隔離相依性，亦即讓不同功能 (module, method, function) 之間戶不影響測試，因此，這個結果只是 stub 沒有去呼叫真正的那個 function 罷了！
