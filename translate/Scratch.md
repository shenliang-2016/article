#### 4.1.1. 启动失败

如果你的应用启动失败，注册的 `FailureAnalyzers` 获得一个机会提供专门的错误消息以及一种具体的行动来解决该问题。比如，如果你在端口 `8080` 上启动 web 应用而该端口已经在使用，你应该能够看到类似于下面的信息：

```
***************************
APPLICATION FAILED TO START
***************************

Description:

Embedded servlet container failed to start. Port 8080 was already in use.

Action:

Identify and stop the process that's listening on port 8080 or configure this application to listen on another port.
```

> Spring Boot 提供了许多 `FailureAnalyzer` 实现，而且你还可以 [添加你自己的](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-failure-analyzer) 。

如果没有失败分析器能够处理启动异常，你仍然可以显示完整的条件报告用来更好的获知错误信息。为了做到这一点，你需要为 `org.springframework.boot.autoconfigure.logging.ConditionEvaluationReportLoggingListener`  [开启 `debug` 属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config) 或者 [开启 `DEBUG` 日志](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-custom-log-levels) 。

比如，如果你通过 `java -jar` 运行你的应用，你可以如下开启 `debug` 属性：

```
$ java -jar myproject-0.0.1-SNAPSHOT.jar --debug
```

#### 4.1.2. 懒初始化

`SpringApplication` 允许延迟地初始化应用程序。启用延迟初始化后，将根据需要创建 bean，而不是在应用程序启动期间创建 bean。因此，启用延迟初始化可以减少应用程序启动所需的时间。在 Web 应用程序中，启用延迟初始化将导致许多与 Web 相关的 Bean 直到收到 HTTP 请求后才被初始化。

延迟初始化的缺点是，它可能会延迟发现应用程序问题的时间。如果错误配置的 Bean 延迟初始化，则启动期间将不再发生故障，并且只有在初始化 Bean 时问题才会显现。还必须注意确保 JVM 有足够的内存来容纳所有应用程序的 bean，而不仅仅是启动期间初始化的 bean。由于这些原因，默认情况下不会启用延迟初始化，因此建议在启用延迟初始化之前先对 JVM 的堆大小进行微调。

可以使用 `SpringApplicationBuilder` 上的 `lazyInitialization` 方法或 `SpringApplication` 上的 `setLazyInitialization` 方法以编程方式启用延迟初始化。另外，也可以使用 `spring.main.lazy-initialization` 属性来启用它，如以下示例所示：

```properties
spring.main.lazy-initialization=true
```

> 如果您想在应用程序的其余部分使用延迟初始化时禁用某些 bean 的延迟初始化，则可以使用 `@Lazy(false)` 注解将它们的延迟属性显式设置为 `false`。

