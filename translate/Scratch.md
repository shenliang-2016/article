### 4.1. SpringApplication

`SpringApplication` 类提供了一种便捷的方法来引导你的 Spring 应用从一个 `main()` 方法启动。很多情况下，你可以将该任务委托给静态 `SpringApplication.run` 方法。如下面例子所示：

```java
public static void main(String[] args) {
    SpringApplication.run(MySpringConfiguration.class, args);
}
```

当你的应用启动之后，你应该可以看到类似于下面的输出：

```
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::   v2.2.2.RELEASE

2019-04-31 13:09:54.117  INFO 56603 --- [           main] o.s.b.s.app.SampleApplication            : Starting SampleApplication v0.1.0 on mycomputer with PID 56603 (/apps/myapp.jar started by pwebb)
2019-04-31 13:09:54.166  INFO 56603 --- [           main] ationConfigServletWebServerApplicationContext : Refreshing org.springframework.boot.web.servlet.context.AnnotationConfigServletWebServerApplicationContext@6e5a8246: startup date [Wed Jul 31 00:08:16 PDT 2013]; root of context hierarchy
2019-04-01 13:09:56.912  INFO 41370 --- [           main] .t.TomcatServletWebServerFactory : Server initialized with port: 8080
2019-04-01 13:09:57.501  INFO 41370 --- [           main] o.s.b.s.app.SampleApplication            : Started SampleApplication in 2.992 seconds (JVM running for 3.658)
```

默认地，`INFO` 日志消息会被记录，包含一些相关的启动细节，比如启动应用的用户等。如果你需要 `INFO` 之外的日志级别，你可以设置它，如 [Log Levels](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-custom-log-levels) 中所述。应用版本通过使用来自应用主类所在包的实现版本确定。启动消息日志可以通过将 `spring.main.log-startup-info` 设定为 `false` 来关闭。这将同时关闭应用的活动配置日志。

> 为了在启动过程中添加额外日志，你可以在 `SpringApplication` 的子类中覆盖 `logStartupInfo(boolean)` 方法。

