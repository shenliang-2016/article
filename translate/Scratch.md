## 7.12 满足任意数量的安全方法

### 问题

你需要提供通过一个站点的安全保障的多种方法。

### 解决方案

使用 `satisfy` 指令来指示 NGINX 你希望满足站点使用的任意或者所有安全方法：

````
location / {
        satisfy any;
        allow 192.168.1.0/24;
        deny  all;
        auth_basic           "closed site";
        auth_basic_user_file conf/htpasswd;
}
````

此配置告诉 NGINX 用户对 `location /` 的请求需要满足一个安全方法：要么请求需要来自 `192.168.1.0/24` CIDR 块，要么请求可以提供用户名和密码，该信息可以从 *conf/htpasswd* 文件中找到。`satisfy` 指令携带两个选项值之一：`any` 或者 `all` 。

### 讨论

`satisfy` 指令可以提供多种方法向你的 web 应用认证你的身份。通过为 `satisfy` 指令指定 `any` 值，用户就必须满足所有的安全挑战之一。为 `satisfy` 指令指定 `all` 值时，用户必须满足所有的安全挑战。此指令可以结合 `http_access_module` ，`http_auth_basic_module` ，`http_auth_request_module` ，以及 `http_auth_jwt_module` 。只有在多个层次同时进行的安全机制才是可以信任的。`satisfy` 指令将帮助你为需要高级安全规则的 location 或者服务器实现可信安全性。

