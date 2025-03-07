+++
date = '2025-03-07T12:18:52+08:00'
draft = false
title = 'Datadog Agent Test'
read_more_copy= '閱讀更多...'
+++


1. 安裝 Datadog Agent on macOS: https://docs.datadoghq.com/agent/basic_agent_usage/osx/
2. 安裝 Datadog dogshell on macOS: https://docs.datadoghq.com/developers/guide/dogshell/

安裝好以後確認一下 dogshell 有正常運作

```shell
datadog-agent status
```

![](/images/screenshot_20250206140009.png)
<!--more-->
![](/images/screenshot_20250206140021.png)

```shell
launchctl list com.datadoghq.agent
```
![](/images/screenshot_20250206142020.png)


進入到 Datadog 的 Web dasboard，一開始沒看到註冊的 local agent，後來發現不同 region 的 site 是分開 url 的 (api key 和 app key 不是共用的)，我一開始選 ap1，但 `~/.datadog-agent/datadog.yml` 中還是用預設的 region us1 ，所以切換過來就看得到了

https://docs.datadoghq.com/getting_started/site/#access-the-datadog-site

![](/images/screenshot_20250206140931.png)
![](/images/screenshot_20250206140944.png)

修改完 ~/datadog-agent/datadog.yml 後
重新啟動：`launchctl stop com.datadoghq.agent then launchctl start com.datadoghq.agent`
也可以用：`datadog-agent stop then datadog-agent start`

![](/images/screenshot_20250206142719.png)
![](/images/screenshot_20250206142733.png)

但 dashboard 那邊還是沒有改...

做一下連線檢測：
```shell
✗ curl -v https://ap1.datadoghq.com/api/v1/validate -H "DD-API-KEY: *********************"
* Host ap1.datadoghq.com:443 was resolved.
* IPv6: (none)
* IPv4: 43.206.164.133, 43.206.164.131, 43.206.164.132
*   Trying 43.206.164.133:443...
* Connected to ap1.datadoghq.com (43.206.164.133) port 443
* ALPN: curl offers h2,http/1.1
* (304) (OUT), TLS handshake, Client hello (1):
*  CAfile: /etc/ssl/cert.pem
*  CApath: none
* (304) (IN), TLS handshake, Server hello (2):
* (304) (IN), TLS handshake, Unknown (8):
* (304) (IN), TLS handshake, Certificate (11):
* (304) (IN), TLS handshake, CERT verify (15):
* (304) (IN), TLS handshake, Finished (20):
* (304) (OUT), TLS handshake, Finished (20):
* SSL connection using TLSv1.3 / AEAD-CHACHA20-POLY1305-SHA256 / [blank] / UNDEF
* ALPN: server accepted h2
* Server certificate:
*  subject: C=US; ST=New York; L=New York; O=Datadog, Inc.; CN=*.ap1.datadoghq.com
*  start date: Mar  1 00:00:00 2024 GMT
*  expire date: Mar  2 23:59:59 2025 GMT
*  subjectAltName: host "ap1.datadoghq.com" matched cert's "ap1.datadoghq.com"
*  issuer: C=US; O=DigiCert Inc; CN=DigiCert Global G2 TLS RSA SHA256 2020 CA1
*  SSL certificate verify ok.
* using HTTP/2
* [HTTP/2] [1] OPENED stream for https://ap1.datadoghq.com/api/v1/validate
* [HTTP/2] [1] [:method: GET]
* [HTTP/2] [1] [:scheme: https]
* [HTTP/2] [1] [:authority: ap1.datadoghq.com]
* [HTTP/2] [1] [:path: /api/v1/validate]
* [HTTP/2] [1] [user-agent: curl/8.7.1]
* [HTTP/2] [1] [accept: */*]
> GET /api/v1/validate HTTP/2
> Host: ap1.datadoghq.com
> User-Agent: curl/8.7.1
> Accept: */*
>
* Request completely sent off
< HTTP/2 403
< content-type: application/json
< content-length: 24
< x-content-type-options: nosniff
< strict-transport-security: max-age=31536000; includeSubDomains; preload
< date: Thu, 06 Feb 2025 06:37:13 GMT
<
* Connection #0 to host ap1.datadoghq.com left intact
{"errors":["Forbidden"]}* Could not resolve host: ****************************************"
* Closing connection
curl: (6) Could not resolve host: ****************************************"
```
先刪除 datadog agent https://docs.datadoghq.com/agent/basic_agent_usage/osx/#uninstall-the-agent
再重新安裝：
```shell
DD_API_KEY=XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX DD_SITE="ap1.datadoghq.com" bash -c "$(curl -L https://install.datadoghq.com/scripts/install_mac_os.sh)"
```

![](/images/screenshot_20250206150909.png)

要過一段時間等待，才會出現在 dashboard 上
![](/images/screenshot_20250206160510.png)

```shell
$ datadog-agent hostname
VeckdeiMac.local
```

在 dashboard 中編輯 query 像這樣，效果如下：

![](/images/screenshot_20250206162442.png)
![](/images/screenshot_20250206162503.png)

如果有多個不同名稱的 agent，應該在這個指標圖表上會有多條線，我猜是這樣，可以拿別台機器來試試看。
