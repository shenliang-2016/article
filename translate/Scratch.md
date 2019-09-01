### 讨论

安全传输层是加密信息最常用的传输方式。在本文写作时，TLS 协议优先于 SSL 协议被选择。这是因为 SSL 协议的版本 1 到 3 目前都被认为是不安全的。尽管协议的名称不尽相同，TLS 仍然建立了安全的套接字。NGINX 使得你的服务可以在你和你的客户致歉保护敏感信息，同样也可以反过来保护你的客户和你的业务。当使用签名证书时，你需要将证书与证书颁发机构联系起来。当你建立这种联系后，你的证书应该是从该链产生的一个文件。如果你的证书颁发机构在链上提供了多个文件，它也会同时提供这些文件的层次顺序。SSL 会话缓存通过不必协商 SSL/TLS 版本和密码来增强性能。

在测试中，发现 ECC 证书比同等强度的 RSA 证书更快。密钥大小较小，这使得能够提供更多的 SSL/TLS连接，并具有更快的握手。NGINX 允许您配置多个证书和密钥，然后为客户端浏览器提供最佳证书。这使您可以利用更新的技术，但同时仍然为老客户服务。

### 参考

[Mozilla Server Side TLS Page](https://wiki.mozilla.org/Security/Server_Side_TLS)
[Mozilla SSL Configuration Generator]([https://ssl-config.mozilla.org](https://ssl-config.mozilla.org/))
[Test Your SSL Configuration with SSL Labs SSL Test](https://www.ssllabs.com/ssltest/)

## 7.4 上游加密

### 问题

您需要加密 NGINX 和上游服务之间的流量，并为兼容性规则设置特定的协商规则，或者如果上游服务器在您的安全网络之外。

### 解决方案

使用 HTTP 代理模块的 SSL 指令来指定 SSL 规则：

````
location / {
	proxy_pass https://upstream.example.com;
	proxy_ssl_verify on;
	proxy_ssl_verify_depth 2;
	proxy_ssl_protocols TLSv1.2;
}
````

这些代理指令设定 NGINX 需要遵循的特定 SSL 规则。配置的指令确保 NGINX 校验上游服务上的证书和授权链最多拥有两个有效证书。`proxy_ssl_protocols`指令指定 NGINX 将仅使用 TLSv1.2。默认地，NGINX 不会校验上游证书，并接受所有 TLS 版本。

### 讨论

HTTP 代理模块的配置指令非常庞大，如果您需要加密上游流量，至少应该启用验证。只需通过更改传递给`proxy_pass`指令的值的协议，就可以通过 HTTPS 进行代理。但是，这不会验证上游证书。其他指令（例如`proxy_ssl_certificate`和`proxy_ssl_certificate_key`）允许您锁定上游加密以增强安全性。您还可以指定`proxy_ssl_crl`或证书吊销列表，其中列出了不再被视为有效的证书。这些 SSL 代理指令有助于加强在您自己的网络内或公共互联网上的通信渠道的安全性。

