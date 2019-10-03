## 7.13 动态 DDoS 缓解

### 问题

你需要动态分布式拒绝服务(DDoS) 缓解解决方案。

### 解决方案

使用 NGINX Plus 来创建一个集群敏感的速率阈值和自动黑名单：

````
limit_req_zone   $remote_addr zone=per_ip:1M rate=100r/s sync;
                 # Cluster-aware rate limit
limit_req_status 429;
keyval_zone zone=sinbin:1M timeout=600 sync;
              # Cluster-aware "sin bin" with
              # 10-minute TTL
keyval $remote_addr $in_sinbin zone=sinbin;
              # Populate $in_sinbin with
              # matched client IP addresses
server {
    listen 80;
        location / {
            if ($in_sinbin) {
                set $limit_rate 50; # Restrict bandwidth of bad clients
            }
            limit_req zone=per_ip;
                  # Apply the rate limit here
            error_page 429 = @send_to_sinbin;
                  # Excessive clients are moved to
                  # this location
            proxy_pass http://my_backend;
        }
        location @send_to_sinbin {
            rewrite ^ /api/3/http/keyvals/sinbin break;
                  # Set the URI of the
                  # "sin bin" key-val
            proxy_method POST;
            proxy_set_body '{"$remote_addr":"1"}';
            proxy_pass http://127.0.0.1:80;
        }
        location /api/ {
            api write=on;
            # directives to control access to the API
        }
}
````

### 讨论

该解决方案使用同步速率限制和同步键值存储来动态响应 DDoS 攻击并减轻其影响。提供给 `limit_req_zone` 和 `keyval_zone` 指令的 `sync` 参数将共享内存区域与双活 `NGINX Plus` 集群中的其他计算机同步。该示例标识了每秒发送 100 个以上请求的客户端，而不管哪个 NGINX Plus 节点接收到该请求。当客户端超过速率限制时，通过调用 NGINX Plus API，将其 IP 地址添加到 “sin bin” 键值存储中。 "sin bin" 在整个群集中同步。无论哪个 NGINX Plus 节点收到请求，来自 "sin bin" 中的客户端的其他请求都将受到非常低的带宽限制。与完全拒绝请求相比，限制带宽是更可取的，因为它不会明确告知客户端 DDoS 缓解措施已生效。 10分钟后，客户端将自动从 "sin bin" 黑名单中移除。

