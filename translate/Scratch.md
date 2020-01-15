#### 4.8.2. RSocket 服务器自动配置

Spring Boot 提供了 RSocket 服务器自动配置。所需的依赖关系由 `spring-boot-starter-rsocket` 提供。

Spring Boot 允许从 WebFlux 服务器通过 WebSocket 公开 RSocket，或支持独立的 RSocket 服务器。这取决于应用程序的类型及其配置。

对于 WebFlux 应用程序（即 `WebApplicationType.REACTIVE` 类型的应用程序），只有在以下属性匹配的情况下，RSocket 服务器才会插入 Web 服务器：

```properties
spring.rsocket.server.mapping-path=/rsocket # a mapping path is defined
spring.rsocket.server.transport=websocket # websocket is chosen as a transport
#spring.rsocket.server.port= # no port is defined
```

> 由于 RSocket 本身是使用该库构建的，因此只有 Reactor Netty 支持将 RSocket 插入 Web 服务器。

另外，RSocket TCP 或 Websocket 服务器也可以作为独立的内置服务器启动。除了依赖性要求之外，唯一需要的配置是为该服务器定义端口：

```properties
spring.rsocket.server.port=9898 # the only required configuration
spring.rsocket.server.transport=tcp # you're free to configure other properties
```

#### 4.8.3. Spring Messaging RSocket 支持

Spring Boot 将为 RSocket 自动配置 Spring Messaging 基础结构。

这意味着 Spring Boot 将创建一个 `RSocketMessageHandler` bean，该 bean 将处理对您的应用程序的 RSocket 请求。

#### 4.8.4. 使用 `RSocketRequester` 调用 RSocket 服务

一旦在服务器和客户端之间建立了 `RSocket` 通道，任何一方都可以向对方发送或接收请求。

作为服务器，您可以在 RSocket `@Controller` 的任何处理程序方法上注入 `RSocketRequester` 实例。作为客户端，您需要首先配置和建立 RSocket 连接。在这种情况下，Spring Boot 使用预期的编解码器自动配置 `RSocketRequester.Builder`。

`RSocketRequester.Builder` 实例是一个原型 bean，这意味着每个注入点将为您提供一个新实例。这样做是有目的的，因为此构建器是有状态的，因此您不应使用同一实例创建具有不同设置的请求者。

下面的代码展示了一个典型的例子：

```java
@Service
public class MyService {

    private final RSocketRequester rsocketRequester;

    public MyService(RSocketRequester.Builder rsocketRequesterBuilder) {
        this.rsocketRequester = rsocketRequesterBuilder
                .connectTcp("example.org", 9898).block();
    }

    public Mono<User> someRSocketCall(String name) {
        return this.requester.route("user").data(name)
                .retrieveMono(User.class);
    }

}
```

