#### 4.7.2. Spring WebFlux 框架

Spring WebFlux 是 Spring Framework 5.0 中引入的新的响应式 Web 框架。与 Spring MVC 不同，它不需要 Servlet API，是完全异步且无阻塞的，并通过 [Reactor项目](https://projectreactor.io/) 实现 [Reactive Streams](https://www.reactive-streams.org/) 规范。

Spring WebFlux 有两种形式：功能性的和基于注解的。基于注解的模型非常类似于 Spring MVC 模型，如以下示例所示：

```java
@RestController
@RequestMapping("/users")
public class MyRestController {

    @GetMapping("/{user}")
    public Mono<User> getUser(@PathVariable Long user) {
        // ...
    }

    @GetMapping("/{user}/customers")
    public Flux<Customer> getUserCustomers(@PathVariable Long user) {
        // ...
    }

    @DeleteMapping("/{user}")
    public Mono<User> deleteUser(@PathVariable Long user) {
        // ...
    }

}
```

功能变体 “WebFlux.fn” 将路由配置与请求的实际处理分开，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
public class RoutingConfiguration {

    @Bean
    public RouterFunction<ServerResponse> monoRouterFunction(UserHandler userHandler) {
        return route(GET("/{user}").and(accept(APPLICATION_JSON)), userHandler::getUser)
                .andRoute(GET("/{user}/customers").and(accept(APPLICATION_JSON)), userHandler::getUserCustomers)
                .andRoute(DELETE("/{user}").and(accept(APPLICATION_JSON)), userHandler::deleteUser);
    }

}

@Component
public class UserHandler {

    public Mono<ServerResponse> getUser(ServerRequest request) {
        // ...
    }

    public Mono<ServerResponse> getUserCustomers(ServerRequest request) {
        // ...
    }

    public Mono<ServerResponse> deleteUser(ServerRequest request) {
        // ...
    }
}
```

WebFlux 是 Spring 框架的一部分，详细信息可在其 [参考文档](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web-reactive.html#webflux-fn) 中找到。

> 您可以根据需要定义尽可能多的 `RouterFunction` bean，以对路由器的定义进行模块化。如果需要应用优先级，可以对 Bean 进行排序。

首先，将 `spring-boot-starter-webflux` 模块添加到您的应用程序中。

> 在应用程序中添加 `spring-boot-starter-web` 和 `spring-boot-starter-webflux` 模块会导致 Spring Boot 自动配置 Spring MVC，而不是 WebFlux。之所以选择这种行为，是因为许多 Spring 开发人员在其 Spring MVC 应用程序中添加了 `spring-boot-starter-webflux` 以使用反应性 WebClient。您仍然可以通过将选定的应用程序类型设置为 `SpringApplication.setWebApplicationType(WebApplicationType.REACTIVE)` 来强制执行选择。

