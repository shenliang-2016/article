## 8.3 HTTP/2 服务器推送

### 问题

你需要抢先地推送内容到客户端。

### 解决方案

使用 NGINX 的 HTTP/2 的服务器推送特性。

````
server {
        listen 443 ssl http2 default_server;
        ssl_certificate    server.crt;
        ssl_certificate_key server.key;
        root /usr/share/nginx/html;
        location = /demo.html {
            http2_push /style.css;
            http2_push /image1.jpg;
			} 
}
````

### 讨论

为了使用 HTTP/2 服务器推送，你的服务器必须配置为使用 HTTP/2，如 7.1 章节所述。由此，你可以指示 NGINX  使用 `http2_push` 指令抢先推送特定文件。该指令携带一个参数，表示需要推动给客户端的文件的完整 URI 路径。

NGINX 还可以自动推送资源给客户端，如果被代理的应用包含一个 HTTP 响应首部，名为 `Link` 。该首部可以指示 NGINX 预加载特定资源。为了启用此特性，添加 `http2_push_preload on;` 到 NGINX 配置中。

