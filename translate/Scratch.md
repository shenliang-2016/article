## 7.3 客户端加密

### 问题

你需要加密你的 NGINX 服务器和客户端之间的流量。

### 解决方案

使用一个 SSL 模块，比如`ngx_http_ssl_module`或者`ngx_stream_ssl_module`来加密流量：

````
http { # All directives user below are also valid in stream
	server {
		listen 8433 ssl;
    ssl_protocols TLSv1.2 TLSv1.3;
    ssl_ciphers HIGH:!aNULL:!MD5;
    ssl_certificate /etc/nginx/ssl/example.pem;
    ssl_certificate_key /etc/nginx/ssl/example.key;
    ssl_certificate /etc/nginx/ssl/example.ecdsa.crt;
    ssl_certificate_key /etc/nginx/ssl/example.ecdsa.key;
    ssl_session_cache shared:SSL:10m;
    ssl_session_timeout 10m;
	}
}
````

此配置设置服务器以侦听使用 SSL 加密的端口 8443。服务器接受 SSL 协议版本 TLSv1.2 和 TLSv1.3。向服务器公开两组证书和密钥对 locations 以供使用。服务器被指示使用客户端提供的最高强度协议版本，同时限制一些不安全的。椭圆曲线 Cryptopgraphy（ECC）密码优先，因为我们提供了 ECC 证书密钥对。SSL 会话缓存和超时允许工作线程在给定的时间内缓存和存储会话参数。还有许多其他会话缓存选项可以帮助提高所有类型使用场景的性能或安全性。您可以将会话缓存选项彼此结合使用。但是，指定一个没有默认值的选项将关闭该默认的内置会话缓存。

