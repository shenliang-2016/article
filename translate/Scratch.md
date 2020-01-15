#### 4.9.2. WebFlux 安全

与 Spring MVC 应用程序类似，您可以通过添加 `spring-boot-starter-security` 依赖性来保护 WebFlux 应用程序。默认的安全配置在 `ReactiveSecurityAutoConfiguration` 和 `UserDetailsServiceAutoConfiguration` 中实现。`ReactiveSecurityAutoConfiguration` 导入 `WebFluxSecurityConfiguration` 以实现网络安全，而 `UserDetailsServiceAutoConfiguration` 则配置身份验证，这也与非 Web 应用程序相关。要完全关闭默认的 Web 应用程序安全性配置，您可以添加类型为 `WebFilterChainProxy` 的 bean（这样做不会禁用 `UserDetailsService` 配置或执行器的安全性）。

要也关闭 `UserDetailsService` 配置，可以添加 `ReactiveUserDetailsService` 或 `ReactiveAuthenticationManager` 类型的 Bean。

可以通过添加自定义 `SecurityWebFilterChain` bean来配置访问规则以及使用多个 Spring Security 组件（例如 OAuth 2 Client 和 Resource Server）。Spring Boot 提供了方便的方法，可用于覆盖执行器端点和静态资源的访问规则。`EndpointRequest` 可以用于创建基于 `management.endpoints.web.base-path` 属性的 `ServerWebExchangeMatcher`。

`PathRequest` 可用于为常用位置的资源创建 `ServerWebExchangeMatcher`。

例如，您可以通过添加以下内容来自定义安全配置：

````java
@Bean
public SecurityWebFilterChain springSecurityFilterChain(ServerHttpSecurity http) {
    return http
        .authorizeExchange()
            .matchers(PathRequest.toStaticResources().atCommonLocations()).permitAll()
            .pathMatchers("/foo", "/bar")
                .authenticated().and()
            .formLogin().and()
        .build();
}
````

