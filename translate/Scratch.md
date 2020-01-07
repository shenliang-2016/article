#### 4.4.4. 日志级别

通过使用 `logging.level.<logger-name>=<level>`，其中 `level` 是 TRACE， DEBUG， INFO， WARN， ERROR， FATAL， 或者 OFF，所有的受支持的日志记录系统级别都可以在 Spring `Environment` 中设置（例如，在 `application.properties` 中）。可以使用 `logging.level.root` 配置 `root` 记录器。

以下示例显示了 `application.properties` 中的潜在日志记录设置：

```properties
logging.level.root=warn
logging.level.org.springframework.web=debug
logging.level.org.hibernate=error
```

也可以使用环境变量设置日志记录级别。例如，`LOGGING_LEVEL_ORG_SPRINGFRAMEWORK_WEB=DEBUG` 将 `org.springframework.web` 设置为 `DEBUG`。

> 以上方法仅适用于程序包级别的日志记录。由于宽松的绑定总是将环境变量转换为小写，因此无法以这种方式为单个类配置日志记录。如果您需要为一个类配置日志记录，则可以使用 [the `SPRING_APPLICATION_JSON`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-application-json) 变量。

#### 4.4.5. 日志组

能够将相关记录器分组在一起以便可以同时配置它们通常是很有用的。例如，您可能通常会更改与 Tomcat 相关的所有记录器的日志记录级别，但是您不容易记住顶级软件包。

为了解决这个问题，Spring Boot 允许您在 Spring `Environment` 中定义日志记录组。例如，以下是通过将其添加到 `application.properties` 中来定义“tomcat”组的方法：

```properties
logging.group.tomcat=org.apache.catalina, org.apache.coyote, org.apache.tomcat
```

定义后，您可以使用一行更改该组中所有记录器的级别：

```properties
logging.level.tomcat=TRACE
```

Spring Boot 包含以下预定义的日志记录组，它们可以直接使用：

| Name | Loggers                                                      |
| :--- | :----------------------------------------------------------- |
| web  | `org.springframework.core.codec`, `org.springframework.http`, `org.springframework.web`, `org.springframework.boot.actuate.endpoint.web`, `org.springframework.boot.web.servlet.ServletContextInitializerBeans` |
| sql  | `org.springframework.jdbc.core`, `org.hibernate.SQL`, `org.jooq.tools.LoggerListener` |

