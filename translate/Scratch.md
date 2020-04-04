#### 5.2.6. CORS 支持

[跨域资源共享](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) (CORS) is a [W3C 规范](https://www.w3.org/TR/cors/) ，允许你以灵活的方式指定哪种跨域请求是被授权的。如果你使用 Spring MVC 或者 Spring WebFlux，执行器 Actuator 的 web 端点能够配置为支持这种场景。

CORS 支持默认关闭，只有当 `management.endpoints.web.cors.allowed-origins` 属性被设定之后才会开启。下面的配置许可来自 `example.com` 域名的 `GET` 和 `POST` 调用：

```properties
management.endpoints.web.cors.allowed-origins=https://example.com
management.endpoints.web.cors.allowed-methods=GET,POST
```

> 参考 [CorsEndpointProperties](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator-autoconfigure/src/main/java/org/springframework/boot/actuate/autoconfigure/endpoint/web/CorsEndpointProperties.java) 获取选项的完整列表。