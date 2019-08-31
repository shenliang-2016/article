# 7 安全控制

## 7.0 介绍

安全性是分层完成的，安全模型必须有多个层才能真正加强。在本章中，我们将通过许多不同的方式使用 NGINX 和 NGINX Plus 来保护您的 Web 应用程序。您可以将这些安全方法中的许多方法相互结合使用，以帮助加强安全性。以下是一些探索 NGINX 和 NGINX Plus 功能的安全部分，可以帮助您加强应用程序。您可能会注意到本章未涉及 NGINX 的最大安全功能之一，即 ModSecurity 3.0 NGINX 模块，它将 NGINX 转变为 Web 应用防火墙（WAF）。要了解有关 WAF 功能的更多信息，请下载 [ModSecurity 3.0和NGINX：快速入门指南](https://www.nginx.com/resources/library/modsecurity-3-nginx-quick-start-guide/) 。

## 7.1 基于 IP 地址访问

### 问题

你需要基于客户端 IP 地址进行访问控制。

### 解决方案

使用 HTTP 访问模块来控制对受保护资源的访问：

````
location /admin/ {
	deny 10.0.0.1;
	allow 10.0.0.0/20;
	allow 2001:0db8::/32;
	deny all;
}
````

给定的 location 块允许从`10.0.0.0/20`中的任何 IPv4 地址（`10.0.0.1`除外）进行访问，允许从`2001:0db8::/32`子网中的 IPv6 地址进行访问，并对来自任何其他地址的请求返回 403。`allow`和`deny`指令在 HTTP，server 和 location 上下文中有效。按顺序检查规则，直到找到远程地址的匹配项。

### 讨论

保护互联网上宝贵的资源和服务必须分层进行。NGINX 提供了成为这些层之一的能力。`deny`指令阻止访问给定的上下文，而`allow`指令可用于允许阻止访问的子集。您可以使用 IP 地址，IPv4 或 IPv6，CIDR 块范围，关键字`all`和 Unix 套接字。通常，在保护资源时，可能允许一块内部 IP 地址并拒绝其他所有人访问。

