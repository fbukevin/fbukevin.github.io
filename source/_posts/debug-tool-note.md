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

待補...
