#### 5.2.3. 保护 HTTP 端点

您应该像对待其他任何敏感 URL 一样，小心保护 HTTP 端点的安全。如果存在 Spring Security，则默认情况下将使用 Spring Security 的内容协商策略保护端点的安全。例如，如果您希望为 HTTP 端点配置自定义安全性，只允许具有特定角色的用户访问它们，Spring Boot 提供了一些方便的 `RequestMatcher` 对象，可以将它们与 Spring Security 结合使用。

典型的 Spring Security 配置看起来类似下面这样：

```java
@Configuration(proxyBeanMethods = false)
public class ActuatorSecurity extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.requestMatcher(EndpointRequest.toAnyEndpoint()).authorizeRequests((requests) ->
                requests.anyRequest().hasRole("ENDPOINT_ADMIN"));
        http.httpBasic();
    }

}
```

上面的例子使用 `EndpointRequest.toAnyEndpoint()` 来匹配发往任何端点的请求以确保它们都具有 `ENDPOINT_ADMIN` 角色。 `EndpointRequest` 上还具有若干其他匹配方法可用。参考 API 文档 ([HTML](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/actuator-api//html) 或者 [PDF](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/actuator-api//pdf/spring-boot-actuator-web-api.pdf)) 获取更多细节。

如果你的应用部署在防火墙之后，你可能更倾向于你的执行器端点可以不需要强制身份认证。你可以通过修改 `management.endpoints.web.exposure.include` 属性来做到这一点，如下所示：

**application.properties**

```properties
management.endpoints.web.exposure.include=*
```

另外，如果存在 Spring Security，则需要添加自定义安全配置，该配置允许未经身份认证的端点访问，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
public class ActuatorSecurity extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.requestMatcher(EndpointRequest.toAnyEndpoint()).authorizeRequests((requests) ->
            requests.anyRequest().permitAll());
    }

}
```