##### 欢迎页面

Spring Boot 支持静态和模板欢迎页面。它首先在配置的静态内容位置中查找 `index.html` 文件。如果没有找到，它会寻找一个 `index` 模板。如果找到任何一个，它将自动用作应用程序的欢迎页面。

##### 自定义网站图标

与其他静态资源一样，Spring Boot 在已配置的静态内容位置中查找 `favicon.ico`。如果存在这样的文件，它将自动用作应用程序的收藏夹图标。

##### 路径匹配和内容协商

Spring MVC 可以通过查看请求路径并将其匹配到应用程序中定义的映射（例如 Controller 方法上的 `@GetMapping` 注解），将传入的 HTTP 请求映射到处理程序。

Spring Boot 选择默认情况下禁用后缀模式匹配，这意味着像 `"GET /projects/spring-boot.json"` 这样的请求将不会与 `@GetMapping("/projects/spring-boot")` 映射相匹配。这被视为 [Spring MVC 应用程序的最佳实践](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-suffix-pattern-match) 。 过去，此功能主要用于未发送正确的 `Accept` 请求标头的 HTTP 客户端。我们需要确保将正确的内容类型发送给客户端。如今，内容协商已变得更加可靠。

还有其他处理 HTTP 客户端的方法，这些客户端不能始终发送正确的 `Accept` 请求标头。除了使用后缀匹配，我们还可以使用查询参数来确保将诸如 `"GET /projects/spring-boot?format=json"` 之类的请求映射到 `@GetMapping("/projects/spring-boot")`：

```properties
spring.mvc.contentnegotiation.favor-parameter=true

# We can change the parameter name, which is "format" by default:
# spring.mvc.contentnegotiation.parameter-name=myparam

# We can also register additional file extensions/media types with:
spring.mvc.contentnegotiation.media-types.markdown=text/markdown
```

如果您了解了以上注意事项，但仍希望您的应用程序使用后缀模式匹配，则需要以下配置：

```properties
spring.mvc.contentnegotiation.favor-path-extension=true
spring.mvc.pathmatch.use-suffix-pattern=true
```

另外，与其打开所有后缀模式，不如只支持已注册的后缀模式，这更安全：

```properties
spring.mvc.contentnegotiation.favor-path-extension=true
spring.mvc.pathmatch.use-registered-suffix-pattern=true

# You can also register additional file extensions/media types with:
# spring.mvc.contentnegotiation.media-types.adoc=text/asciidoc
```

##### ConfigurableWebBindingInitializer

Spring MVC 使用 `WebBindingInitializer` 来为特定请求初始化 `WebDataBinder`。如果创建自己的 `ConfigurableWebBindingInitializer` `@Bean`，Spring Boot 会自动配置 Spring MVC 以使用它。

##### 模板引擎

除了 REST Web 服务之外，您还可以使用 Spring MVC 来提供动态 HTML 内容。Spring MVC 支持各种模板技术，包括 Thymeleaf，FreeMarker 和 JSP。同样，许多其他模板引擎包括他们自己的 Spring MVC 集成。

Spring Boot 包含对以下模板引擎的自动配置支持：

- [FreeMarker](https://freemarker.apache.org/docs/)
- [Groovy](http://docs.groovy-lang.org/docs/next/html/documentation/template-engines.html#_the_markuptemplateengine)
- [Thymeleaf](https://www.thymeleaf.org/)
- [Mustache](https://mustache.github.io/)

> 如果可能，应避免使用 JSP。当将它们与嵌入式 servlet 容器一起使用时，存在几个 [已知限制](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-jsp-limitations) 。

当您使用这些模板引擎之一进行默认配置时，您的模板会自动从 `src/main/resources/templates` 中获取。

> 根据您运行应用程序的方式，IntelliJ IDEA 对类路径的排序不同。与使用 Maven 或 Gradle 或从其打包的 jar 运行应用程序时相比，从 IDE 的主要方法运行应用程序的顺序会有所不同。这可能导致 Spring Boot 无法在类路径上找到模板。如果遇到此问题，可以在 IDE 中重新排序类路径，以首先放置模块的类和资源。另外，您可以配置模板前缀，以搜索类路径上的每个 `templates` 目录，如下所示：`classpath*:/templates/`。

