在 NGINX Plus 中使用 JWT 模块来保护一个 location 或者 server，同时构建 `auth_jwt` 指令来使用`$cookie_auth_token`作为 token 来校验：

````
location /private/ {
	auth_jwt "Google Oauth" token=$cookied_auth_token;
	auth_jwt_key_file /etc/nginx/google_certs.jwk;
}
````

此配置指示 NGINX Plus 使用 JWT 校验保护 */private* URI 路径。Google Oauth 2.0 OpenID Connect 使用 cookie `auth_token` 而不是默认的 bearer token。因此，你必须指示 NGINX 在该 cookie 中寻找 token ，而不是在 NGINX Plus 默认位置寻找。`auth_jwt_key_file` 位置可以设置为任意路径，我们将在 6.6 章节中介绍。

### 讨论

此配置展示了你如何使用 NGINX Plus 校验 Google Oauth 2.0 OpenID Connect JSON Web Token 。用于 HTTP 的 NGINX Plus JWT 认证模块能够校验任何遵循 JSON Web Signature 规范 RFC 的 JSON Web Token，立即启用任何利用 JSON Web Token 的SSO权限在 NGINX Plus 层进行验证。OpenID 1.0 协议是 OAuth 2.0 身份验证协议之上的一个层，它添加了身份标识，允许使用 JWT 来证明发送请求的用户的身份。通过令牌的签名，NGINX Plus 可以验证令牌自签名以来未被修改。通过这种方式，Google 正在使用异步签名方法，并且可以在保持其私有 JWK 秘密的同时分发公共 JWK。

NGINX Plus 还可以控制 OpenID Connect 1.0 的授权代码流，使 NGINX Plus 成为OpenID Connect 的中继方。此功能支持与大多数主要身份提供程序集成，包括 CA Single Sign-On（以前称为 SiteMinder），ForgeRock OpenAM，Keycloak，Okta，OneLogin 和 Ping Identity。有关NGINX Plus 作为 OpenID Connect 认证的中继方的更多信息和参考实现，请查看 [NGINX Inc OpenID Connect GitHub Reposory](https://github.com/nginxinc/nginx-openid-connect) 。

### 参考

[Detailed NGINX Blog on OpenID Connect](https://www.nginx.com/blog/authenticating-users-existing-applications-openid-connect-nginx-plus/)
[OpenID Connect](https://openid.net/connect/)

##6.6 从 Google 获取 JSON Web Key

### 问题

当使用 NGINX Plus 验证 OpenID Connect tokens 时你需要从 Google 获取 JSON Web Key。

### 解决方案

使用 Cron 来每个小时请求一个密钥集合来保证你的密钥始终是最新的：

````
0 * * * * root wget https://www.googleapis.com/oauth2/v3/ \
		certs-0/etc/nginx/google_certs.jwk
````

这行代码来自一个 crontab 文件。类 Unix 系统有很多选项用于配置 crontab 文件。每个用户都可以拥有自己特定的 crontab，同时，在*/etc/directory*路径下也存在大量文件和文件夹。

### 讨论

Cron 是在类 Unix 系统上运行计划任务的常用方法。应定期更新 JSON Web 密钥，以确保密钥的安全性，进而确保系统的安全性。为了确保您始终拥有 Google 提供的最新密钥，您需要定期检查新的 JWK。这种 Cron 解决方案是这样做的一种方式。

### 参考

[Cron](https://linux.die.net/man/8/cron)

