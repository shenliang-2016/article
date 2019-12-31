#### 3.8.1. 默认属性

Spring Boot 支持的某些类库使用缓存改善性能。比如，[template engines](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-template-engines) 缓存编译好的模板来避免重复解析模板文件。同样的，Spring MVC 能够添加 HTTP 首部缓存用于响应静态资源。

尽管缓存在生产环境中非常有益，但在开发过程中可能适得其反，因为它可能使您无法看到刚刚在应用程序中所做的更改。因此，默认情况下，`spring-boot-devtools` 禁用缓存选项。

缓存选项通常由 `application.properties` 文件中的设置配置。例如，Thymeleaf 提供了 `spring.thymeleaf.cache` 属性。不需要手动设置这些属性，`spring-boot-devtools` 模块会自动应用合理的开发时配置。

因为在开发 Spring MVC 和 Spring WebFlux 应用程序时需要有关 Web 请求的更多信息，所以开发人员工具将为 `web` 日志记录组启用 `DEBUG` 日志记录。这将为您提供有关传入请求，正在处理的处理程序，响应结果等的信息。如果您希望记录所有请求的详细信息（包括潜在的敏感信息），则可以打开 `spring.http.log-request -details` 的配置属性。

> 如果您不希望应用默认属性，则可以在 `application.properties` 中将 `spring.devtools.add-properties` 设置为 `false`。

> 开发者工具应用的所有属性的完整列表，详见 [DevToolsPropertyDefaultsPostProcessor](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-devtools/src/main/java/org/springframework/boot/devtools/env/DevToolsPropertyDefaultsPostProcessor.java) 。

