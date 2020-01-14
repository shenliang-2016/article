##### 自定义内置 Servlet 容器

可以通过使用 Spring 的 `Environment` 属性来配置常见的 servlet 容器设置。通常，您将在 `application.properties` 文件中定义属性。

常用服务器设置包括：

- 网络设置：侦听传入HTTP请求的端口（`server.port`），绑定到 `server.address` 的接口地址，等等。
- 会话设置：会话是否是持久性的（`server.servlet.session.persistent`），会话超时（`server.servlet.session.timeout`），会话数据的位置（`server.servlet.session.store-dir`）和会话 Cookie 配置（`server.servlet.session.cookie.*`）。
- 错误管理：错误页面位置 (`server.error.path`) 等等。
- [SSL](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-configure-ssl)
- [HTTP 压缩](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#how-to-enable-http-response-compression)

Spring Boot 尝试尽可能多地公开通用设置，但这并不总是可能的。在这种情况下，专用名称空间可提供服务器特定的自定义设置（请参见 `server.tomcat` 和 `server.undertow`）。例如，可以使用内置 servlet 容器特定功能配置 [访问日志](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-configure-accesslogs)。

> 参考 [`ServerProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/ServerProperties.java) 类以获得完整列表。

###### 编程式自定义

如果您需要以编程方式配置内置 servlet 容器，则可以注册一个实现 `WebServerFactoryCustomizer` 接口的 Spring bean。`WebServerFactoryCustomizer` 提供对 `ConfigurableServletWebServerFactory` 的访问，其中包括许多自定义设置方法。以下示例显示以编程方式设置端口：

```java
import org.springframework.boot.web.server.WebServerFactoryCustomizer;
import org.springframework.boot.web.servlet.server.ConfigurableServletWebServerFactory;
import org.springframework.stereotype.Component;

@Component
public class CustomizationBean implements WebServerFactoryCustomizer<ConfigurableServletWebServerFactory> {

    @Override
    public void customize(ConfigurableServletWebServerFactory server) {
        server.setPort(9000);
    }

}
```

> `TomcatServletWebServerFactory`，`JettyServletWebServerFactory` 和 `UndertowServletWebServerFactory` 是 `ConfigurableServletWebServerFactory` 的专用变体，分别具有针对 Tomcat，Jetty 和 Undertow 的其他自定义设置方法。

###### 直接自定义 ConfigurableServletWebServerFactory

如果上述自定义技术太有限，则可以自己注册 `TomcatServletWebServerFactory`，`JettyServletWebServerFactory` 或 `UndertowServletWebServerFactory` bean。

```java
@Bean
public ConfigurableServletWebServerFactory webServerFactory() {
    TomcatServletWebServerFactory factory = new TomcatServletWebServerFactory();
    factory.setPort(9000);
    factory.setSessionTimeout(10, TimeUnit.MINUTES);
    factory.addErrorPages(new ErrorPage(HttpStatus.NOT_FOUND, "/notfound.html"));
    return factory;
}
```

提供了许多配置选项的设置器。如果您需要做一些更奇特的操作，还提供了几种受保护的方法“挂钩”。请参阅 [源代码文档](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/web/servlet/server/ConfigurableServletWebServerFactory.html) 获取更多细节。

##### JSP 局限性

运行使用内置 servlet 容器（并打包为可执行档案）的 Spring Boot 应用程序时，JSP 支持存在一些限制。

- 使用 Jetty 和 Tomcat，如果使用 war 包装，它应该可以工作。可执行的 war 与 `java -jar` 一起启动时将起作用，并且也可部署到任何标准容器中。使用可执行 jar 时，不支持 JSP。

- Undertow 不支持 JSP。

- 创建自定义 `error.jsp` 页面不会覆盖 [错误处理](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-error-handling) 的默认视图。应使用 [自定义错误页面](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-error-handling-custom-error-pages) 代替。

