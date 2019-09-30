## 7.9 HTTPS 重定向

### 问题

你需要将未加密的请求重定向到 HTTPS 。

### 解决方案

使用重写将 HTTP 流量转向 HTTPS。

````
server {
        listen 80 default_server;
        listen [::]:80 default_server;
        server_name _;
        return 301 https://$host$request_uri;
}
````

此配置在端口 80 上侦听，作为 IPv4 和 IPv6 以及任何主机名的默认服务器。`return` 语句返回一个到同一主机上的 HTTPS 服务器的相同请求 URI 的 301 永久重定向。

### 讨论

请务必始终在适当的时候重定向到 HTTPS。您可能会发现您不需要重定向所有请求，而仅重定向那些在客户端和服务器之间传递敏感信息的请求。在这种情况下，您可能只想将 `return` 语句放在特定的位置，例如 */login*。

