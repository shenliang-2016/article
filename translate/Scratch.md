### 4.15. 使用 `WebClient` 调用 REST 服务

如果您的类路径中包含 Spring WebFlux，则还可以选择使用 `WebClient` 来调用远程 REST 服务。与 `RestTemplate` 相比，此客户端具有更多的功能感，并且具有完全的反应性。您可以在 Spring Framework 文档的 [专用部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web-reactive.html#webflux-client) 中了解有关 WebClient 的更多信息。

Spring Boot 为您创建并预配置了 `WebClient.Builder`。强烈建议将其注入您的组件中，并使用它来创建 `WebClient` 实例。Spring Boot 配置该构建器以共享 HTTP 资源，以与服务器相同的方式反映编解码器的设置（请参阅 [WebFlux HTTP编解码器自动配置](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-webflux-httpcodecs)）等。

下面的代码展示了典型的示例：

```java
@Service
public class MyService {

    private final WebClient webClient;

    public MyService(WebClient.Builder webClientBuilder) {
        this.webClient = webClientBuilder.baseUrl("https://example.org").build();
    }

    public Mono<Details> someRestCall(String name) {
        return this.webClient.get().uri("/{name}/details", name)
                        .retrieve().bodyToMono(Details.class);
    }

}
```