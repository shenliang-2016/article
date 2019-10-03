# 8 HTTP/2

## 8.0 介绍

HTTP/2 是 HTTP 协议的一个大版本。该版本中完成的很多工作都聚焦于传输层，诸如允许请求和响应服用一个 TCP 连接，通过压缩 HTTP 首部字段来提高效率，以及对请求优先级的支持。另外一个大的新特性是支持服务器推送消息给客户端。本章将详细介绍 NGINX 中开启 HTTP/2 的支持的基础配置，以及如何配置 gRPC 和 HTTP/2 服务器推送支持。

## 8.1 基础配置

### 问题

你希望使用 HTTP/2。

### 解决方案

在你的 NGINX 服务器上开启 HTTP/2 ：

````
server {
        listen 443 ssl http2 default_server;
        ssl_certificate    server.crt;
        ssl_certificate_key server.key;
        ... 
}
````

### 讨论

要打开 HTTP/2，只需将 `http2` 参数添加到 `listen` 指令。但是，要注意的是，尽管该协议不需要将连接包装在 SSL/TLS 中，但是 HTTP/2 客户端的某些实现仅在加密连接上支持 HTTP/2。另一个警告是，HTTP/2 规范将许多 TLS 1.2 加密套件列为黑名单，因此将使握手失败。NGINX 默认使用加密的不在黑名单中。要测试您的设置是否正确，您可以为 Chrome 和 Firefox 浏览器安装一个插件，该插件指示网站何时使用 HTTP/2，或者在命令行上使用 `nghttp` 实用工具。

### 参考

[HTTP/2 RFC Blacklisted Ciphers](https://tools.ietf.org/html/rfc7540#appendix-A)
[Chrome HTTP2 and SPDY Indicator Plugin](https://chrome.google.com/webstore/detail/http2-and-spdy-indicator/mpbpobfflnpcgagjijhmgnchggcjblin)
[Firefox HTTP2 Indicator Add-on](https://addons.mozilla.org/en-US/firefox/addon/http2-indicator/)

