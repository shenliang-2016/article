### 4.4. 日志

Spring Boot 使用 [Commons Logging](https://commons.apache.org/logging) 进行所有内部日志记录，但是对底层日志实现保持开放。为  [Java Util Logging](https://docs.oracle.com/javase/8/docs/api//java/util/logging/package-summary.html)， [Log4J2](https://logging.apache.org/log4j/2.x/)， 和 [Logback](https://logback.qos.ch/) 提供默认配置。在每种情况下，记录器都已预先配置为使用控制台输出，同时还提供可选文件输出。

默认情况下，如果使用“启动器”，则使用 Logback 进行日志记录。还包括适当的 Logback 路由，以确保使用 Java Util Logging，Commons Logging，Log4J 或 SLF4J 的依赖库都可以正常工作。

> Java 有许多可用的日志记录框架。如果上面的列表看起来令人困惑，请不要担心。通常，您不需要更改日志记录依赖项，并且 Spring Boot 默认值可以正常工作。

> 将应用程序部署到 Servlet 容器或应用程序服务器时，通过 Java Util Logging API 执行的日志记录不会路由到应用程序的日志中。这样可以防止容器或其他已部署到容器中的其它应用程序产生的日志记录出现在你的应用程序的日志中。

#### 4.4.1. 日志格式

Spring Boot 的默认日志输出类似于以下示例：

```
2019-03-05 10:57:51.112  INFO 45469 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet Engine: Apache Tomcat/7.0.52
2019-03-05 10:57:51.253  INFO 45469 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-03-05 10:57:51.253  INFO 45469 --- [ost-startStop-1] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1358 ms
2019-03-05 10:57:51.698  INFO 45469 --- [ost-startStop-1] o.s.b.c.e.ServletRegistrationBean        : Mapping servlet: 'dispatcherServlet' to [/]
2019-03-05 10:57:51.702  INFO 45469 --- [ost-startStop-1] o.s.b.c.embedded.FilterRegistrationBean  : Mapping filter: 'hiddenHttpMethodFilter' to: [/*]
```

输出包含以下项目：

- 日期和时间：毫秒精度，易于排序。

- 日志级别：`ERROR`， `WARN`， `INFO`， `DEBUG`， 或者 `TRACE`。

- 进程ID。

- 一个 `---` 分隔符，用于区分实际日志消息的开始。

- 线程名称：方括号内（对于控制台输出，可能会被截断）。

- 记录器名称：这通常是源类名称（通常缩写）。

- 日志消息。

> Logback 没有 `FATAL` 级别，该级别对应于其它日志框架的 `ERROR`。

