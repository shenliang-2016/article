#### 4.9.1. MVC 安全

默认的安全配置在 `SecurityAutoConfiguration` 和 `UserDetailsServiceAutoConfiguration` 中实现。`SecuritySecurityConfiguration` 导入 `SpringBootWebSecurityConfiguration` 来实现 Web 安全，而 `UserDetailsServiceAutoConfiguration` 则配置身份验证，这在非 Web 应用程序中也很重要。要完全关闭默认的 Web 应用程序安全性配置或合并多个 Spring Security 组件（例如 OAuth 2 客户端和资源服务器），请添加类型为 `WebSecurityConfigurerAdapter` 的 bean（这样做不会禁用 `UserDetailsService` 配置或 `Actuator` 的安全性）。

要也关闭 `UserDetailsService` 配置，可以添加 `UserDetailsService`，`AuthenticationProvider` 或 `AuthenticationManager` 类型的 Bean。

可以通过添加自定义 `WebSecurityConfigurerAdapter` 来覆盖访问规则。Spring Boot 提供了方便的方法，可用于覆盖执行器端点和静态资源的访问规则。`EndpointRequest` 可以用来创建基于 `management.endpoints.web.base-path` 属性的 `RequestMatcher`。`PathRequest` 可以用来为常用位置的资源创建一个 `RequestMatcher`。

