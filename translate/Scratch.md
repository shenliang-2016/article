##### Servlet 上下文初始化

内置 Servlet 容器不会直接执行 Servlet 3.0+ 的 `javax.servlet.ServletContainerInitializer` 接口或 Spring 的 `org.springframework.web.WebApplicationInitializer` 接口。这是一个有意的设计决定，旨在降低在 war 中运行的第三方库可能破坏 Spring Boot 应用程序的风险。

如果需要在 Spring Boot 应用程序中执行 servlet 上下文初始化，则应注册一个实现 `org.springframework.boot.web.servlet.ServletContextInitializer` 接口的 bean。单一的 `onStartup` 方法提供对 `ServletContext` 的访问，并且在必要时可以轻松地用作现有 `WebApplicationInitializer` 的适配器。

###### 扫描 Servlets, Filters, 和 listeners

当使用内置容器时，可以通过使用 `@ServletComponentScan` 来启用自动注册带有 `@WebServlet`，`@WebFilter` 和 `@WebListener` 的类。

> `@ServletComponentScan` 在独立容器中无效，在该容器中使用了容器的内置发现机制。

##### ServletWebServerApplicationContext

在后台，Spring Boot 使用另一种类型的 `ApplicationContext` 来支持内置 servlet 容器。`ServletWebServerApplicationContext` 是 `WebApplicationContext` 的一种特殊类型，它通过搜索单个 `ServletWebServerFactory` bean来进行自我引导。通常，已经自动配置了 `TomcatServletWebServerFactory`，`JettyServletWebServerFactory` 或 `UndertowServletWebServerFactory`。

> 通常，您不需要了解这些实现类。大多数应用程序都是自动配置的，并且代表您创建了相应的 `ApplicationContext` 和 `ServletWebServerFactory`。

