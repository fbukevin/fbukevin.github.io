---
layout: post
title: '[Python] Requests + Google Finance API'
date: 2015-10-29 13:24
comments: true
categories: 
---
本文是要介紹如何使用 *Python* 的 `request` 模組來呼叫 Google Finance API 並解析取得的股價內容。

有關 requests 模組的介紹，請參考：[http://docs.python-requests.org/en/latest/user/quickstart/](http://docs.python-requests.org/en/latest/user/quickstart/)
<!--more-->
首先當然就是要安裝 request 模組啦！

`pip install requests`

然後就可以開始寫程式了

```python
>>> import requests
>>> r = requests.get("https://finance.google.com/finance/info", params = {"client":"ig", "q":"TPE:2330"})
```

這段是以 HTTP GET 方法呼叫 Google Finance 的 API，可以得到不同國家區域證券交易所提供的即時股價資訊，requests 物件的 get 方法可以給予兩個參數，第一個參數是資源的 URI，第二個參數是相關設定，項目很多種，這裡我們用來設定 GET 傳輸所夾帶的資料，有 `client` (通常設定 "ig") 和 `q` (query string 的意思，格式為 `<證券交易所代碼>:<股票代碼>`)，本例整個發送的資源敘述會變成：

`https://finance.google.com/finance/info?client=ig&q=TPE:2330`

如果成功取得回應資源，我們可以用 `r.text` 來查看回應內容本文，用 `print()` 可以印的比較漂亮點(人類可讀)：

```python
>>> print(r.text) 		#pretty output
// [
{
"id": "674465"
,"t" : "2330"
,"e" : "TPE"
,"l" : "138.00"
,"l_fix" : "138.00"
,"l_cur" : "NT$138.00"
,"s": "0"
,"ltt":"1:30PM GMT+8"
,"lt" : "Oct 28, 1:30PM GMT+8"
,"lt_dts" : "2015-10-28T13:30:02Z"
,"c" : "-1.00"
,"c_fix" : "-1.00"
,"cp" : "-0.72"
,"cp_fix" : "-0.72"
,"ccol" : "chr"
,"pcls_fix" : "139"
}
]
```

##Parse Response String
假如回傳的資料內容確定是 JSON 格式內容，你可以用 `r.json()` 來 parse 出內容，但是注意回傳的內容，雖然長得很像 JSON 的格式，但是在整個字串最前面多了兩個 '/'，這導致這個物件並不是 JSON 物件，呼叫 `r.json()` 會出錯誤，因此我們需要先處理掉這兩個反斜線。

由於 JSON 的字串物件無法直接替換掉字串指定索引的內容，所以我採用複製子字串的方式來取得不帶有反斜線的其他內容：

```python
>>> s = r.text[4:] 		#copy from "["
>>> import json
>>> o = json.loads(s)
>>> o[0]['l']
u'138.00'
>>> import decimal
>>> d = decimal.Decimal(o[0]['l'])
Decimal('138.00')
>>> int(d)
138
>>> float(d)
138.0
```


補充一下，`requests.get()` 帶的第二個參數，用 `params` 和 `data` 是不同的項目喔，如果用 `data`，會得到 `Bad request`。


然後要小心，不要一次發太多個 request，不然會被封鎖....