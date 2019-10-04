## 8.2 gRPC

### 问题

你需要对 gRPC 方法调用进行终止、检测、路由或者负载均衡。

### 解决方案

使用 NGINX 代理 gRPC 连接。

````
server {
        listen 80 http2;
        location / {
            grpc_pass grpc://backend.local:50051;
				} 
}
````

在此配置中，NGINX 在 80 端口上监听未加密的 HTTP/2 流量，将该流量代理至名为 `backend.local` 的机器的 `50051` 端口。`grpc_pass` 指令指示 NGINX 将该通信作为 gRPC 调用对待。我们的后端服务器位置之前的 `grpc://` 不是必需的，不过，它确实直接表明了后端的通信是未加密的。

为了在客户端和 NGINX 之间使用 TLS 加密，并在将调用传递给应用服务器之前终止加密，请像第一节中所述，开启 SSL 和 HTTP/2。

````
server {
        listen 443 ssl http2 default_server;
        ssl_certificate    server.crt;
        ssl_certificate_key server.key;
        location / {
            grpc_pass grpc://backend.local:50051;
        }
}
````

此配置在 NGINX 处终止 TLS 并通过未加密的 HTTP/2 将 gRPC 通信发送给应用服务器。

如果要配置 NGINX 以加密发送给应用服务器的 gRPC 通信，以提供端到端的加密传输，可以简单地修改 `grpc_pass` 指令以在服务器信息之前指定 `grpcs://` (注意，其中的 `s` 后缀表示安全通信)：

````
grpc_pass grpcs://backend.local:50051;
````

你还可以基于 gRPC URI 使用 NGINX 将调用路由到不同的后端服务器，该 URI 包含包名、服务名以及方法名。使用 `location` 指令来做到这一点：

````
location /mypackage.service1 {
        grpc_pass grpc://backend.local:50051;
}
location /mypackage.service2 {
        grpc_pass grpc://backend.local:50052;
}
location / {
        root /usr/share/nginx/html;
        index index.html index.htm;
}
````

此配置展示了使用 `location` 指令将到来的 HTTP/2 流量路由到两个独立的 gRPC 服务，同时，该 `location` 也提供静态内容服务。`mypackage.service1` 服务的方法调用被发送到 `backend.local` 服务器的 `50051` ，而 `mypackage.service2` 的方法调用将发送到端口 `50052` 。`location /` 捕获所有其他 HTTP 请求和静态资源请求。这就说明了 NGINX 如何提供同一个 HTTP/2 服务断点下的 gRPC 和非-gRPC 请求，同时进行相应路由。

负载均衡的 gRPC 调用类似于非-gRPC HTTP 流量：

````
upstream grpcservers {
        server backend1.local:50051;
        server backend2.local:50051;
}
server {
        listen 443 ssl http2 default_server;
        ssl_certificate    server.crt;
        ssl_certificate_key server.key;
        location / {
            grpc_pass grpc://grpcservers;
        }
}
````

`upstream` 块对 gRPC 和其他所有 HTTP 流量作用完全相同。唯一的不同是该 `upstream` 被 `grpc_pass` 引用。

### 讨论

NGINX 能够接收，代理，负载均衡，路由和终止 gRPC 调用的加密。gRPC 模块使 NGINX 可以设置，更改或删除 gRPC 调用首部，设置请求超时以及设置上游 SSL/TLS 规范。当 gRPC 通过 HTTP/2 协议进行通信时，您可以将 NGINX 配置为在同一端点上接受 gRPC 和非-gRPC Web 通信。

