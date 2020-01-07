#### 4.4.2. 控制台输出

默认日志配置当纪录日志时会将它们同步显示到控制台中。默认情况下，`ERROR` 级别，`WARN` 级别和 `INFO` 级别的日志会被记录下来。你也可以通过在启动应用时使用 `--debug` 参数来开启 `debug` 模式。

```
$ java -jar myapp.jar --debug
```

> 你还可以在你的 `application.properties` 指定 `debug=true` 。

启用调试模式后，将配置一些核心记录器（嵌入式容器，Hibernate 和 Spring Boot）以输出更多信息。启用调试模式*不会*将您的应用程序配置为记录所有具有 `DEBUG` 级别的消息。

另外，您可以通过以 `--trace` 标志（或 `application.properties` 中的 `trace=true`）启动应用程序来启用“跟踪”模式。这样做可以为某些核心记录器（嵌入式容器，Hibernate 模式生成以及整个 Spring 产品组合）启用跟踪记录。

##### 日志输出颜色代码

如果你的终端支持 ANSI，则可以通过使用颜色输出来提升日志可读性。你可以设定 `spring.output.ansi.enabled` 为一个 [supported value](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/ansi/AnsiOutput.Enabled.html) 来覆盖自动探测的配置。

通过使用 `%clr` 转换字来配置颜色编码。转换器以最简单的形式根据日志级别为输出着色，如以下示例所示：

```
%clr(%5p)
```

下表列出了日志级别与颜色的映射关系：

| Level   | Color  |
| :------ | :----- |
| `FATAL` | Red    |
| `ERROR` | Red    |
| `WARN`  | Yellow |
| `INFO`  | Green  |
| `DEBUG` | Green  |
| `TRACE` | Green  |

另外，您可以通过将其提供为转换的选项来指定应使用的颜色或样式。例如，要使文本变黄，请使用以下设置：

```
%clr(%d{yyyy-MM-dd HH:mm:ss.SSS}){yellow}
```

支持的颜色和风格如下：

- `blue`
- `cyan`
- `faint`
- `green`
- `magenta`
- `red`
- `yellow`

