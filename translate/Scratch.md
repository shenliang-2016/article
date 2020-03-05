### 4.26. WebSockets

Spring Boot 提供了 WebSockets 自动配置用于内置的 Tomcat， Jetty，以及 Undertow。如果你将你的 war 文件部署在一个独立的容器中，Spring Boot 假定该容器会负责配置它自己的 WebSocket 支持。

Spring Framework 提供了 [丰富的 WebSocket 支持](https://docs.spring.io/spring/docs/5.2.4.RELEASE/spring-framework-reference/web.html#websocket) 用于 MVC web 应用，可以通过 `spring-boot-starter-websocket` 模块很方便地访问。

WebSocket 支持也可用于 [反应式 web 应用](https://docs.spring.io/spring/docs/5.2.4.RELEASE/spring-framework-reference/web-reactive.html#webflux-websocket) ，并且需要包含 WebSocket API 和 `spring-boot-starter-webflux`：

```xml
<dependency>
    <groupId>javax.websocket</groupId>
    <artifactId>javax.websocket-api</artifactId>
</dependency>
```