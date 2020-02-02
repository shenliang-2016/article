#### 4.15.1. WebClient Runtime

Spring Boot 将根据应用程序类路径上可用的库自动检测要使用哪个 `ClientHttpConnector` 来驱动 `WebClient`。目前，还支持 Reactor Netty 和 Jetty RS 客户端。

`spring-boot-starter-webflux` 启动器默认情况下依赖于 `io.projectreactor.netty:reactor-netty`，这带来了服务器和客户端的实现。如果您选择使用 Jetty 作为反应式服务器，则应在 Jetty 反应式 HTTP 客户端库 `org.eclipse.jetty:jetty-reactive-httpclient` 上添加依赖项。对服务器和客户端使用相同的技术具有其优势，因为它将自动在客户端和服务器之间共享 HTTP 资源。

通过提供自定义的 `ReactorResourceFactory` 或 `JettyResourceFactory` bean，开发人员可以覆盖 Jetty 和 Reactor Netty 的资源配置—这将同时应用于客户端和服务器。

如果您希望为客户端覆盖该选择，则可以定义自己的 `ClientHttpConnector` bean，并完全控制客户端配置。

了解更多信息请参考 [`WebClient` 配置选项](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web-reactive.html#webflux-client-builder)。