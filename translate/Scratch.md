#### 4.7.5. 内置反应式服务器支持

Spring Boot 包含对以下内置反应式 Web 服务器的支持：Reactor Netty，Tomcat，Jetty 和 Undertow。大多数开发人员使用适当的“启动器”来获取完全配置的实例。默认情况下，内置服务器在端口 8080 上侦听 HTTP 请求。

#### 4.7.6. 反应式服务器资源配置

当自动配置 Reactor Netty 或 Jetty 服务器时，Spring Boot 将创建特定的 bean，这些 bean 将向服务器实例提供 HTTP 资源：`ReactorResourceFactory` 或 `JettyResourceFactory`。

默认情况下，这些资源还将与 Reactor Netty 和 Jetty 客户端共享，以实现最佳性能，前提是：

- 服务器和客户端使用相同的技术

- 使用 Spring Boot 自动配置的 `WebClient.Builder` bean构建客户端实例

开发者可以通过提供自定义的 `ReactorResourceFactory` 或 `JettyResourceFactory` bean 来覆盖 Jetty 和 Reactor Netty 的资源配置-这将同时应用于客户端和服务器。

您可以在 [WebClient运行时部分](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-webclient-runtime) 中了解有关客户端资源配置的更多信息。

