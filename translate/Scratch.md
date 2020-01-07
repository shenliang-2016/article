#### 4.4.3. 文件输出

默认情况下，Spring Boot 仅记录到控制台，不写日志文件。如果除了控制台输出外还想写日志文件，则需要设置一个 `logging.file.name` 或 `logging.file.path` 属性（例如，在 `application.properties` 中）。

下表显示了如何一起使用 `logging.*` 属性：

| `logging.file.name` | `logging.file.path` | Example    | Description                                                  |
| :------------------ | :------------------ | :--------- | :----------------------------------------------------------- |
| *(none)*            | *(none)*            |            | 仅输出到控制台。                                             |
| 指定文件            | *(none)*            | `my.log`   | 写入指定日志文件。文件名可以是外部位置或者当前目录的相对位置。 |
| *(none)*            | 指定路径            | `/var/log` | 将 `spring.log` 写入指定目录。文件名可以是外部位置或者当前目录的相对位置。 |

日志文件达到 10 MB 时会自动切换，并且与控制台输出一样，缺省情况下会记录 `ERROR` 级，`WARN` 级和 `INFO` 级消息。大小限制可以使用 `logging.file.max-size` 属性来更改。除非已设置 `logging.file.max-history` 属性，否则以前生成的文件将无限期存档。可以使用 `logging.file.total-size-cap` 限制日志档案的总大小。当日志归档的总大小超过该阈值时，将删除备份。要在应用程序启动时强制清除日志存档，请使用 `logging.file.clean-history-on-start` 属性。

> 日志记录属性独立于实际的日志记录基础结构。因此，特定的配置键（例如 Logback 的 `loglog.configurationFile`）不是由 Spring Boot 管理的。

