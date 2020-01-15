### 4.9. 安全

如果 [Spring Security](https://spring.io/projects/spring-security) 位于类路径中，则默认情况下 Web 应用程序是安全的。Spring Boot 依靠 Spring Security 的内容协商策略来确定是使用 `httpBasic` 还是 `formLogin`。要将方法级安全性添加到 Web 应用程序，您还可以使用所需的设置添加 `@EnableGlobalMethodSecurity`。可以在 [Spring Security参考指南](https://docs.spring.io/spring-security/site/docs/5.2.1.RELEASE/reference/htmlsingle/#jc-method) 中找到更多信息。

默认的 `UserDetailsService` 只有一个用户。用户名为 `user`，密码为随机密码，并在应用程序启动时以 `INFO` 级别显示，如下例所示：

```
Using generated security password: 78fa095d-3f4c-48b1-ad50-e24c31d5cf35
```

> 如果您微调日志记录配置，请确保将 `org.springframework.boot.autoconfigure.security` 类别设置为记录 `INFO` 级消息。否则，不会打印默认密码。

您可以通过提供 `spring.security.user.name` 和 `spring.security.user.password` 来更改用户名和密码。

默认情况下，您在 Web 应用程序中获得的基本功能是：

- 具有内存存储区的 `UserDetailsService`（如果是 WebFlux 应用程序，则为 `ReactiveUserDetailsService`）Bean 和具有生成的密码的单个用户（请参阅 [`SecurityProperties.User`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/autoconfigure/security/SecurityProperties.User.html) 以获取用户的属性）。

- 整个应用程序的基于表单的登录或 HTTP 基本安全性（取决于请求中的 `Accept` 标头）（如果执行器位于类路径上，则包括执行器端点）。

- 用于发布身份验证事件的 `DefaultAuthenticationEventPublisher`。

您可以通过添加一个bean来提供一个不同的`AuthenticationEventPublisher`。

