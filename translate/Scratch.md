#### 4.7.4. 内置 Servlet 容器支持

Spring Boot 包含对 [Tomcat](https://tomcat.apache.org/)、[Jetty](https://www.eclipse.org/jetty/) 和 [Undertow](https://github.com/undertow-io/undertow) 等多种内置 Servlet 服务器的支持。大多数开发者使用合适的启动器来获取完整配置的实例。默认情况下，内置的服务器在端口 `8080` 上监听 HTTP 请求。

##### Servlets, Filters, 和 listeners

使用内置 Servlet 容器时，您可以通过使用 Spring Bean 或扫描 Servlet 组件来注册 Servlet 规范中的 Servlet、过滤器和所有侦听器（例如 `HttpSessionListener`）。

###### 将 Servlets, Filters, 和 Listeners 注册为 Spring Beans

任何作为 Spring bean 的 Servlet，Filter 或 Servlet  `*Listener` 实例都向嵌入式容器注册。如果您想在配置过程中引用来自 `application.properties` 的值，这将特别方便。

默认情况下，如果上下文仅包含单个 Servlet，则将其映射到 `/`。对于多个 servlet bean，bean 名称用作路径前缀。过滤器映射到 `/*`。

如果基于约定的映射不够灵活，则可以使用 `ServletRegistrationBean`，`FilterRegistrationBean` 和 `ServletListenerRegistrationBean` 类进行完全控制。

通常情况下，过滤器 bean 处于无序状态是安全的。如果需要特定的顺序，则应使用 `@Order` 来注解 `Filter` 或使其实现 `Ordered`。您不能通过使用 `@Order` 注解 bean 方法的方法来配置 `Filter` 的顺序。如果您不能将 `Filter` 类更改为添加 `@Order` 或实现 `Ordered`，则必须为 `Filter` 定义 `FilterRegistrationBean` 并使用 `setOrder(int)` 方法设置注册 bean 的顺序。避免配置一个在 `Ordered.HIGHEST_PRECEDENCE` 上读取请求正文的过滤器，因为它可能与应用程序的字符编码配置不符。如果 Servlet 过滤器包装了请求，则应使用小于或等于 `OrderedFilter.REQUEST_WRAPPER_FILTER_MAX_ORDER` 的顺序来配置它。

> 要查看应用程序中每个 `Filter` 的顺序，请为 `web` [logging group](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-custom-log-groups)（`logging.level.web=debug`）启用 `debug` 级别日志。然后，将在启动时记录已注册过滤器的详细信息，包括其顺序和 URL 模式。

> 注册 `Filter` bean 时要小心，因为它们是在应用程序生命周期中很早就初始化的。如果您需要注册与其他 bean 交互的 `Filter`，请考虑使用 [`DelegatingFilterProxyRegistrationBean`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/web/servlet/DelegatingFilterProxyRegistrationBean.html) 。

