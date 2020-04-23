### 5.9. 进程监控

在 `spring-boot` 模块中，你可以找到两个类用来创建通常对进程监控很有用的文件：

- `ApplicationPidFileWriter` 创建一个包含应用 PID 的文件（默认是在应用目录下，文件名是 `application.pid`）。
- `WebServerPortFileWriter` 创建一个文件（或者多个文件）包含运行 web 服务器的端口（默认实在应用目录下，文件名是 `application.port`）。

默认情况下，这些写入器都没有激活，不过你可以通过一下方式手动启用：

- [通过扩展配置](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-process-monitoring-configuration)
- [编程方式](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-process-monitoring-programmatically)

#### 5.9.1. 扩展配置

在 `META-INF/spring.factories` 文件中，你可以激活写 PID 文件的监听器，如下面例子所示：

```
org.springframework.context.ApplicationListener=\
org.springframework.boot.context.ApplicationPidFileWriter,\
org.springframework.boot.web.context.WebServerPortFileWriter
```

#### 5.9.2. 编程方式

你还可以通过调用 `SpringApplication.addListeners(…)` 方法并出入相应的 `Writer` 对象激活监听器。这种方式也允许你在 `Writer` 构造器中自定义文件名和路径。