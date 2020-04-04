#### 5.2.7. 实现自定义端点

如果你添加带有 `@Endpoint` 注解的 `@Bean` 注解，任何使用 `@ReadOperation`, `@WriteOperation`, 或者 `@DeleteOperation` 注解修饰的方法都会自动通过 JMX 暴露，如果是在 web 应用中，同时还会通过 HTTP 暴露。端点能够通过 HTTP 暴露，使用 Jersey, Spring MVC, 或者 Spring WebFlux。如果 Jersey 和 Spring MVC 都可用，Spring MVC 将会被使用。

你也可以使用 `@JmxEndpoint` 或者 `@WebEndpoint` 编写特定于技术的端点。这些端点局限于它们各自相应的技术。比如， `@WebEndpoint` 仅仅通过 HTTP 暴露，而不通过 JMX 暴露。

你可以使用 `@EndpointWebExtension` 和 `@EndpointJmxExtension` 编写特定于技术的扩展。这些注解允许你提供特定技术的操作以配置现有的端点。

最后，如果你需要访问特定于 web 框架的功能，你可以实现 Servlet 或者 Spring `@Controller` 和 `@RestController` 端点，不过代价是它们无法通过 JMX 暴露，并且当使用不同的 web 框架时不可用。