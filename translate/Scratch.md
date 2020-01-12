##### Spring HATEOAS

如果您开发使用超媒体的 RESTful API，Spring Boot 将为 Spring HATEOAS 提供自动配置，该配置可与大多数应用程序很好地兼容。自动配置取代了使用 `@EnableHypermediaSupport` 的需要，并注册了许多 bean 来简化基于超媒体的应用程序的构建，其中包括一个 `LinkDiscoverers`（用于客户端支持）和一个 `ObjectMapper`，这些对象被配置为将响应正确地编组到所需的表示形式。`ObjectMapper` 是通过设置各种 `spring.jackson.*` 属性来定制的，如果存在的话，是通过一个 `Jackson2ObjectMapperBuilder` bean来定制的。

您可以使用 `@EnableHypermediaSupport` 来控制 Spring HATEOAS 的配置。注意，这样做会禁用前面描述的 `ObjectMapper` 自定义。

##### CORS 支持

[跨域资源共享](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)（CORS）是已通过 [大多数浏览器](https://caniuse.com/#feat=cors) 实现的 [W3C规范](https://www.w3.org/TR/cors/) ，您可以灵活地指定授权哪种类型的跨域请求，而不是使用一些安全性和功能不强的方法，例如 IFRAME 或 JSONP。

从4.2版开始，Spring MVC [支持CORS](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-cors)。将 [controller method CORS configuration](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-cors-controller) 与 [`@CrossOrigin` ](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/bind/annotation/CrossOrigin.html) 注解用在 Spring Boot应用程序中不需要任何注解具体配置。[Global CORS配置](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-cors-global) 可以通过注册 `WebMvcConfigurer` 来定义具有自定义 `addCorsMappings(CorsRegistry)` 方法的 bean，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
public class MyConfiguration {

    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/api/**");
            }
        };
    }
}
```

