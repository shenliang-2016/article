#### 4.7.3. JAX-RS 和 Jersey

如果您更喜欢 REST 端点的 JAX-RS 编程模型，则可以使用可用的实现之一来代替 Spring MVC。[Jersey](https://jersey.github.io/) 和 [Apache CXF](https://cxf.apache.org/) 开箱即用。CXF 要求您在应用程序上下文中将其 Servlet 或 Filter 作为 `@Bean` 注册。Jersey 提供了一些本地的 Spring 支持，因此我们在 Spring Boot 中还与启动程序一起为其提供了自动配置支持。

要开始使用 Jersey，请将 `spring-boot-starter-jersey` 作为依赖项，然后需要一个 `ResourceConfig` 类型的 `@Bean` 在其中注册所有端点，如以下示例所示：

```java
@Component
public class JerseyConfig extends ResourceConfig {

    public JerseyConfig() {
        register(Endpoint.class);
    }

}
```

> Jersey 对扫描可执行档案的支持非常有限。例如，它无法扫描 [完全可执行的jar文件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#deployment-install) 中的包内部的端点，或运行可执行 war 文件时在 `WEB-INF/classes` 中的端点。为了避免这种限制，不应该使用 `packages` 方法，并且应该使用 `register` 方法分别注册端点，如前面的示例所示。

对于更高级的定制，您还可以注册任意数量的实现 `ResourceConfigCustomizer` 的 bean。

所有注册的端点应该是带有 HTTP 资源注解的 `@Components`（`@GET` 和其他注解），如以下示例所示：

```java
@Component
@Path("/hello")
public class Endpoint {

    @GET
    public String message() {
        return "Hello";
    }

}
```

由于 `Endpoint` 是 Spring 的 `@Component`，它的生命周期是由 Spring 管理的，因此您可以使用 `@Autowired` 注解注入依赖项，并使用 `@Value` 注解注入外部配置。默认情况下，Jersey servlet 被注册并映射到 `/*`。您可以通过将 `@ApplicationPath` 添加到 `ResourceConfig` 中来更改映射。

默认情况下，Jersey 被设置为名为 `jerseyServletRegistration` 的 `ServletRegistrationBean` 类型的 `@Bean` 中的 Servlet。默认情况下，该 Servlet 的初始化是延迟的，但是您可以通过设置 `spring.jersey.servlet.load-on-startup` 来自定义该行为。您可以通过创建自己的同名 bean 来禁用或覆盖该 bean。您还可以通过设置 `spring.jersey.type=filter`（在这种情况下，要替换或覆盖的 `@Bean` 是 `jerseyFilterRegistration`）来使用过滤器而非 Servlet。过滤器具有一个 `@Order`，可以通过 `spring.jersey.filter.order` 进行设置。可以通过使用 `spring.jersey.init.*` 来指定属性映射，从而为 servlet 和过滤器注册都赋予 `init` 参数。

