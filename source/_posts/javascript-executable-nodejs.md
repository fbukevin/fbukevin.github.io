---
layout: post
title: '[JavaScript] Executable node.js'
date: 2015-01-29 02:26
comments: true
categories: 
---

1. 建立 package.json
```json
{
    "name": "filesearch",
  	"description": "just that",
  	"version": "0.1.0",
  	"main": "lib/filesearch",	
	  "preferGlobal": "true",
	  "bin": {
             "filesearch" : "lib/filesearch.js"		// tell node where to execute 
     }
}
```
<!--more-->
如果你有多個執行檔，bin 這裡可以多放幾個，名稱即指令，值為檔案路徑

2. 建立 lib/ 和 lib/filesearhc.js

3. filesearhc.js
```javascript
#!/usr/bin/env node			// 直譯器位置(建議不要用 #!/usr/bin/node)
console.log('execute without type "node" and make it global');
```

4. install our package locally
```
~/Desktop/exenode/lib -->npm link
/Users/veck/.nvm/v0.10.35/bin/filesearch -> /Users/veck/.nvm/v0.10.35/lib/node_modules/filesearch/lib/filesearch.js
/Users/veck/.nvm/v0.10.35/lib/node_modules/filesearch -> /Users/veck/Desktop/exenode
~/Desktop/exenode/lib -->
```

5.  cd to the other directory and type "filesearch" without node
```
~/Desktop -->filesearch 
execute without type "node" and make it global
```

6. to remove installation
```
npm unlink -g <package-name>		// 因為我們用 link 會安裝成 global 的指令，因此要用 -g 
```
![exe.png](http://user-image.logdown.io/user/3330/blog/3407/post/252813/tzIIkqRWCO7XFlTe7Fw2_exe.png)


如果用 npm 發佈了，只要用 `npm install -g <package>` 就可以安裝成 global command。

參考原文：http://javascriptplayground.com/blog/2012/08/writing-a-command-line-node-tool/