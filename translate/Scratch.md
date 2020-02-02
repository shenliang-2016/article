### 4.14. 使用 `RestTemplate` 调用 REST 服务 

如果你的应用需要调用远程 REST 服务，你可以使用 Spring 框架的 [`RestTemplate`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html) 类。由于 [`RestTemplate`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html) 在使用之前通常都需要进行定制，Spring Boot 不提供任何单独自动配置的 [`RestTemplate`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html) bean。不过，它提供了一个自动配置好的 `RestTemplateBuilder` ，它可以被用来在需要的时候创建 `RestTemplate` 实例。自动配置的 `RestTemplateBuilder` 保证了合适的 `HttpMessageConverters` 被应用于 `RestTemplate` 实例。

下面的代码是个典型的示例：

```java
@Service
public class MyService {

    private final RestTemplate restTemplate;

    public MyService(RestTemplateBuilder restTemplateBuilder) {
        this.restTemplate = restTemplateBuilder.build();
    }

    public Details someRestCall(String name) {
        return this.restTemplate.getForObject("/{name}/details", Details.class, name);
    }

}
```

> `RestTemplateBuilder` 包含大量有用的方法，可以用来快速配置 `RestTemplate` 实例。比如，要添加 BASIC 身份认证支持，你可以使用 `builder.basicAuthentication("user", "password").build()`。

