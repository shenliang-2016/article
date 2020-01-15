### 4.8. RSocket

[RSocket](https://rsocket.io/) 是一个用于字节流传输的二进制协议。它通过通过单个连接传递的异步消息来启用对称交互模型。

Spring 框架的 `spring-messaging` 模块在客户端和服务器端都支持 RSocket 请求者和响应者。有关更多信息，请参见 Spring Framework 参考文档的 [RSocket部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web-reactive.html#rsocket-spring) 详细信息，包括 RSocket 协议概述。

#### 4.8.1. RSocket 策略自动配置

Spring Boot 自动配置一个 `RSocketStrategies` bean，该 bean 提供了编码和解码 RSocket 有效负载所需的所有基础结构。默认情况下，自动配置将尝试（按顺序）配置以下内容：

1. [CBOR](https://cbor.io/) 使用 Jackson 编码解码
2. JSON 使用 Jackson 编码解码

`spring-boot-starter-rsocket` 启动器提供了两种依赖关系。查阅 [Jackson支持部分](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-json-jackson) 以了解有关自定义可能性的更多信息 。

开发人员可以通过创建实现 `RSocketStrategiesCustomizer` 接口的 bean 来自定义 `RSocketStrategies` 组件。注意，它们的 `@Order` 很重要，因为它确定编解码器的顺序。

