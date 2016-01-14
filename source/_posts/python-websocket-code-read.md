---
layout: post
title: 'Python WebSocket [Code Read and Demo]'
date: 2014-09-25 13:00
comments: true
categories: 
---
Source Code: https://github.com/isnowfy/python-websocket
Tutorial: http://www.isnowfy.com/python-websocket-server/

Project 中的 `index.html` 就扮演著 Client 的角色，用瀏覽器執行後，他會發 request 給 server，其中主要建立 WebSocket 連線的 JavaScript 片段如下：
```
  function openConnection() {
      conn = new WebSocket('ws://localhost:7000/');   // 建立連線
      conn.onopen = function () {
        alert("open");
        conn.send("hello");
      };

      conn.onmessage = function (event) {
        alert(event.data);
        /* TODO: 做連線建立後想做的事情 */
      };

      conn.onclose = function (event) {
      };

      conn.onerror = function(event){
        alert(event.data);
      }
    }    

  setTimeout(function () {
    openConnection();
  }, 1000);
```
`onopen`, `onclose`, `onerror` 這三個方法比較直觀，就是在連線建立、連線關閉和連線出錯時，要執行的內容
`onmessage` 則是在連線成功建立以後要做的事情

而 server 就是 `ws.py`，使用 terminal 開啟以後，使用 `python ws.py`，就會去聽指定的 port (作者這邊預設為 7000)，在 ws.py 中的 main 裡面的 `select(socket_list, [], [])` 會監看 socket_list 中的 socket 變化，一旦 client 端發出 request，server 端接收到以後，select 會知道，並回傳這個 socket，此 socket 會被丟入 WebSocket.handshake 中去解析認證，接著就 response 連線資訊給 client，如此就建立起連線了：

```
def main(handle=process):
    port = 7000     # 定義要監聽的 port
    try:
        server.bind(('', port))     # 綁定服務
        server.listen(100)          # 設定最大監聽連線數目 (可能有多個連線同時來，排隊等著回應)
    except Exception, e:
        print e
        exit()
    socket_list.add(server)         # 將新的監聽物件加入監聽列表中
    print 'server start on port %d' % port
    while True:                     # 開始監聽
        r, w, e = select(socket_list, [], [])   # 利用 select 來監控監聽物件的變化
        for sock in r:
            if sock == server:
                conn, addr = sock.accept()      # 取出物件連線資訊，包含 socket 物件和 client 位址
                if WebSocket.handshake(conn):   # 處理連線資訊
                    socket_list.add(conn)       # 保持 socket 監聽 (即保持連線)
            else:								# 例外處理
                data = WebSocket.recv(sock)
                if not data:
                    socket_list.remove(sock)
                else:
                    handle(sock, data)
```

Server 接收到 HTTP request 後，會取出 `Sec-WebSocket-Key` 的值，並加上一串 magic string `258EAFA5-E914-47DA-95CA-C5AB0DC85B11`，接著使用 SHA-1 加密後在進行 BASE-64 編碼，最後將結果放到 response 封包中的 `Sec-WebSocket-Accept`，返回給 client，如此便完成連線，這就是 WebSocket 基本的連線建立原理，因此在 handshake 中會是如此：
```
    def handshake(conn):
        key = None 
        data = conn.recv(8192)      # 從收到 request 的 socket 中取得資料，8192 是 buffer size
        if not len(data):
            return False
        for line in data.split('\r\n\r\n')[0].split('\r\n')[1:]:
            k, v = line.split(': ')     # 取出 Sec-WebSocket-Key
            if k == 'Sec-WebSocket-Key':
                key = base64.b64encode(hashlib.sha1(v + '258EAFA5-E914-47DA-95CA-C5AB0DC85B11').digest())
        if not key:
            conn.close()
            return False
        response = 'HTTP/1.1 101 Switching Protocols\r\n'\
                   'Upgrade: websocket\r\n'\
                   'Connection: Upgrade\r\n'\
                   'Sec-WebSocket-Accept:' + key + '\r\n\r\n'
        conn.send(response)
        return True
```

Class WebSocket 中的 recv 和 send，以及全域方法 sendall 和 process 是在例外處理時會被呼叫的，這部份要自己客製化你要的處理方式

補充：
"258EAFA5-E914-47DA-95CA-C5AB0DC85B11" 這個魔術字串，在 RFC 文件中有說明，它是一個 Globally Unique Identifier，詳可見 RFC6455(WebSocket) 與 RFC4122(Universal Unique Identifier)