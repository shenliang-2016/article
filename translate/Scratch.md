##### 静态内容

默认情况下，Spring Boot 从类路径中的目录 `/static`（或 `/public` 或 `/resources` 或 `/META-INF/resources`）或 `ServletContext` 的根目录中提供静态内容。它使用 Spring MVC 中的 `ResourceHttpRequestHandler`，因此您可以通过添加自己的 `WebMvcConfigurer` 并覆盖 `addResourceHandlers` 方法来修改该行为。

在独立的 Web 应用程序中，还启用了容器中的默认 servlet 并充当备用，如果 Spring 决定不处理它，则从 ServletContext 的根目录提供内容。在大多数情况下，这不会发生（除非您修改默认的 MVC 配置），因为 Spring 始终可以通过 `DispatcherServlet` 处理请求。

默认情况下，资源映射在 `/**` 上，但是您可以使用 `spring.mvc.static-path-pattern` 属性进行调整。例如，将所有资源重定位到 `/resources/**` 可以实现如下：

```properties
spring.mvc.static-path-pattern=/resources/**
```

您还可以使用 `spring.resources.static-locations` 属性来自定义静态资源位置（将默认值替换为目录位置列表）。根 Servlet 上下文路径 `\` 也会自动添加为资源位置。

除了前面提到的“标准”静态资源位置外，[Webjars内容](https://www.webjars.org/) 也有特殊情况。如果 jar 文件以 Webjars 格式打包，则所有 `/webjars/**` 中所有路径下的资源都将通过 jar 文件提供。

> 如果您的应用程序打包为 jar，则不要使用 `src/main/webapp` 目录。尽管此目录是一个通用标准，但它仅在 war 打包中有效，并且在生成 jar 时，大多数构建工具都将其忽略。

Spring Boot 还支持 Spring MVC 提供的高级资源处理功能，例如缓存清除静态资源或对 Webjars 使用版本无关的 URL。

要为 Webjar 使用与版本无关的 URL，请添加 `webjars-locator-core` 依赖项。然后声明您的 Webjar。以 jQuery 为例，添加 `/webjars/jquery/jquery.min.js` 会生成 `/webjars/jquery/x.y.z/jquery.min.js`，其中 `x.y.z` 是 Webjar 版本。

> 如果使用 JBoss，则需要声明 `webjars-locator-jboss-vfs` 依赖，而不是 `webjars-locator-core`。否则，所有 Webjar 都解析为 `404`。

要使用缓存清除，以下配置可为所有静态资源配置缓存清除解决方案，并在 URL 中有效地添加内容哈希，例如 `<link href="/css/spring-2a2d595e6ed9a0b24f027f2b63b134d6.css"/>` ：

```properties
spring.resources.chain.strategy.content.enabled=true
spring.resources.chain.strategy.content.paths=/**
```

> 通过为 Thymeleaf 和 FreeMarker 自动配置的 `ResourceUrlEncodingFilter`，可以在运行时在模板中重写资源链接。使用 JSP 时，您应该手动声明此过滤器。目前尚不自动支持其他模板引擎，但可以使用自定义模板宏/帮助器以及使用 [`ResourceUrlProvider`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/servlet/resource/ResourceUrlProvider.html)。

例如，当使用 JavaScript 模块加载器动态加载资源时，不能重命名文件。这就是为什么其他策略也受支持并且可以组合的原因。 “固定”策略在 URL 中添加静态版本字符串，而不更改文件名，如以下示例所示：

```properties
spring.resources.chain.strategy.content.enabled=true
spring.resources.chain.strategy.content.paths=/**
spring.resources.chain.strategy.fixed.enabled=true
spring.resources.chain.strategy.fixed.paths=/js/lib/
spring.resources.chain.strategy.fixed.version=v12
```

通过这种配置，位于 `"/js/lib/"` 下的 JavaScript 模块使用固定的版本控制策略（`/v12/js/lib/mymodule.js“`），而其他资源仍使用内容版本（`<link href="/css/spring-2a2d595e6ed9a0b24f027f2b63b134d6.css"/>`）。

参见 [`ResourceProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/ResourceProperties.java) 以获取更多受支持的选项。

> 本特性已经在相关专门 [blog post](https://spring.io/blog/2014/07/24/spring-framework-4-1-handling-static-web-resources) 和 Spring Framework 的 [reference documentation](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-config-static-resources) 中进行了详尽描述。

