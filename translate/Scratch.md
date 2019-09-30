## 7.10 重定向到在 NGINX 之前终止 SSL/TLS 的 HTTPS

### 问题

您需要重定向到 HTTPS，但是，您已经在 NGINX 之前的一层终止了 SSL/TLS。

### 解决方案

使用标准的 `X-Forwarder-Proto` 首部来确定你是否需要重定向：

````
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        server_name _;
        if ($http_x_forwarded_proto = 'http') {
            return 301 https://$host$request_uri;
        }
}
````

此配置非常近似 HTTPS 重定向配置。不过，此配置中我们只有在 `X-Forwarded-Proto` 首部等于 HTTP 时才会重定向。

### 讨论

通常的情况是，您可以在 NGINX 前面的层中终止 SSL/TLS。您可以这样做的原因之一是节省计算成本。但是，您需要确保每个请求都是 HTTPS，但是终止 SSL/TLS 的层不具有重定向功能。但是，它可以设置代理标头。此配置可与诸如 Amazon Web Services Elastic Load Balancer 之类的层一起使用，这些层将无成本地卸载 SSL/TLS。这是一个方便的技巧，可确保 HTTP 通信的安全。

