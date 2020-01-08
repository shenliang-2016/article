#### 4.4.6. 自定义日志配置

可以通过在类路径中包含适当的库来激活各种日志记录系统，并可以通过在类路径的根目录中或在以下 Spring `Environment` 属性指定的位置中提供适当的配置文件来进一步自定义各种日志记录系统：`logging.config `。

您可以通过使用 `org.springframework.boot.logging.LoggingSystem` 系统属性来强制 Spring Boot 使用特定的日志系统。该值应该是 `LoggingSystem` 实现的完全限定的类名。您还可以通过使用值 `null` 来完全禁用 Spring Boot 的日志记录配置。

> 由于日志系统是在 `ApplicationContext` 创建**之前**初始化的，因此将无法从 Spring `@Configuration` 文件中的 `@PropertySources` 中控制日志系统。更改日志记录系统或完全禁用它的唯一方法是通过系统属性。

根据你的日志系统，下面的文件被加载：

| Logging System          | Customization                                                |
| :---------------------- | :----------------------------------------------------------- |
| Logback                 | `logback-spring.xml`, `logback-spring.groovy`, `logback.xml`, or `logback.groovy` |
| Log4j2                  | `log4j2-spring.xml` or `log4j2.xml`                          |
| JDK (Java Util Logging) | `logging.properties`                                         |

> 如果可能，我们建议您为日志配置使用 `-spring` 变体（例如，`logback-spring.xml` 而不是 `logback.xml`）。如果使用标准配置位置，Spring 将无法完全控制日志系统初始化。

> 从“可执行jar”运行时，Java Util Logging 存在一些已知的类加载问题，这会引起问题。我们建议您从“可执行jar”运行时尽可能避免使用它。

为了帮助进行自定义，如下表所述，将一些其他属性从Spring `Environment` 转移到 `System` 属性：

| Spring Environment                    | System Property                   | Comments                                                     |
| :------------------------------------ | :-------------------------------- | :----------------------------------------------------------- |
| `logging.exception-conversion-word`   | `LOG_EXCEPTION_CONVERSION_WORD`   | 记录异常时使用的转换字。                                     |
| `logging.file.clean-history-on-start` | `LOG_FILE_CLEAN_HISTORY_ON_START` | 是否在启动时清除存档日志文件（如果启用了 LOG_FILE ）。 （仅默认的 Logback 设置受支持。） |
| `logging.file.name`                   | `LOG_FILE`                        | 如果定义，它将在默认日志配置中使用。                         |
| `logging.file.max-size`               | `LOG_FILE_MAX_SIZE`               | 最大日志文件大小（如果启用了LOG_FILE）。（仅默认的Logback设置受支持。） |
| `logging.file.max-history`            | `LOG_FILE_MAX_HISTORY`            | 要保留的最大归档日志文件数（如果启用了LOG_FILE）。 （仅默认的Logback设置受支持。） |
| `logging.file.path`                   | `LOG_PATH`                        | 如果定义，它将在默认日志配置中使用。                         |
| `logging.file.total-size-cap`         | `LOG_FILE_TOTAL_SIZE_CAP`         | 要保留的日志备份的总大小（如果启用了LOG_FILE）。 （仅默认的Logback设置受支持。） |
| `logging.pattern.console`             | `CONSOLE_LOG_PATTERN`             | 控制台上使用的日志模式（stdout）。 （仅默认的Logback设置受支持。） |
| `logging.pattern.dateformat`          | `LOG_DATEFORMAT_PATTERN`          | 记录日期格式的附加模式。 （仅默认的Logback设置受支持。）     |
| `logging.pattern.file`                | `FILE_LOG_PATTERN`                | 文件中使用的日志模式（如果启用了LOG_FILE）。 （仅默认的Logback设置受支持。） |
| `logging.pattern.level`               | `LOG_LEVEL_PATTERN`               | 呈现日志级别时使用的格式（默认为 `％5p`）。（仅默认的Logback设置受支持。） |
| `logging.pattern.rolling-file-name`   | `ROLLING_FILE_NAME_PATTERN`       | 滚动日志文件名的模式（默认为`${LOG_FILE}.%d{yyyy-MM-dd}.%i.gz`）。（仅默认的Logback设置受支持。） |
| `PID`                                 | `PID`                             | 当前进程ID（如果可能被发现，并且尚未将其定义为OS环境变量时）。 |

所有受支持的日志记录系统在解析其配置文件时都可以查阅系统属性。有关示例，请参见 `spring-boot.jar` 中的默认配置：

- [Logback](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/resources/org/springframework/boot/logging/logback/defaults.xml)
- [Log4j 2](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/resources/org/springframework/boot/logging/log4j2/log4j2.xml)
- [Java Util logging](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/resources/org/springframework/boot/logging/java/logging-file.properties)

> 如果要在日志记录属性中使用占位符，则应使用 [Spring Boot的语法](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-placeholders-in-properties) ，而不是基础框架的语法。值得注意的是，如果使用 Logback，则应使用 `:` 作为属性名称与其默认值之间的分隔符，而不应使用 `:-`。

> 您可以通过仅覆盖 `LOG_LEVEL_PATTERN`（或带有 Logback 的 `logging.pattern.level`）来将 MDC 和其他临时内容添加到日志行。例如，如果使用`logging.pattern.level=user:%X{user} %5p`，则默认日志格式包含“ user”的 MDC 条目（如果存在），如以下示例所示。
>
> ````
> 2019-08-30 12:30:04.031 user:someone INFO 22174 --- [  nio-8080-exec-0] demo.Controller
> Handling authenticated request
> ````

