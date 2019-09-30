## 7.10 HTTP 严格传输安全

### 问题

你需要指示浏览器永远不要通过 HTTP 发送请求。

### 解决方案

通过设定 `Strict-Transport-Security` 首部来使用 HTTP 严格传输安全(HSTS) 增强：

````
add_header Strict-Transport-Security max-age=31536000;
````

此配置将 `Strict-Transport-Security` 标头设置为最长使用期限为一年。这将指示浏览器在尝试向该域发出 HTTP 请求时始终执行内部重定向，以便所有请求都将通过 HTTPS 发出。

### 讨论

对于某些应用程序，一个在中间攻击中被人篡改的 HTTP 请求可能会造成严重破坏。如果包含敏感信息的表单发布是通过 HTTP 发送的，则来自 NGINX 的 HTTPS 重定向将无法保存您；损坏同样会发生。这种可选的安全性增强功能通知浏览器从不发出 HTTP 请求，因此该请求绝不会未经加密发送。

### 参考

[RFC-6797 HTTP Strict Transport Security](https://tools.ietf.org/html/rfc6797)
[OWASP HSTS Cheat Sheet](https://www.owasp.org/index.php/HTTP_Strict_Transport_Security_Cheat_Sheet)

