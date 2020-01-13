##### Web Filters

Spring WebFlux 提供了一个 `WebFilter` 接口，可以用来过滤 HTTP 请求-响应交互。在应用程序上下文中找到的 `WebFilter` bean将自动用于过滤每次交互。

当过滤器的顺序很重要时，它们可以实现 `Ordered` 或用 `@Order` 注解。Spring Boot 自动配置可能会为您配置 Web 过滤器。这样做时，将使用下表中显示的顺序：

| Web Filter                              | Order                            |
| :-------------------------------------- | :------------------------------- |
| `MetricsWebFilter`                      | `Ordered.HIGHEST_PRECEDENCE + 1` |
| `WebFilterChainProxy` (Spring Security) | `-100`                           |
| `HttpTraceWebFilter`                    | `Ordered.LOWEST_PRECEDENCE - 10` |

