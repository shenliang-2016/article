#### 4.1.3. 自定义启动横幅

启动时打印在控制台的横幅可以通过在类路径上添加 `banner.txt` 文件或者设定 `spring.banner.location` 属性为该文件的路径。如果文件编码不是 UTF-8，你还可以设定 `spring.banner.charset` 。除了文本文件，你还可以添加 `banner.gif` ，`banner.jpg` ，或者 `banner.png` 图片文件到你的类路径，或者设定 `spring.banner.image.location` 属性。图片将被转化为 ASCII 码图形式并打印在所有文本横幅上面。

在你的 `banner.txt` 文件中，你可以使用下面这些占位符：

| Variable                                                     | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| `${application.version}`                                     | 应用的版本号，在 `MANIFEST.MF` 中声明。比如，`Implementation-Version: 1.0` 被打印为 `1.0`。 |
| `${application.formatted-version}`                           | 应用的版本号，在 `MANIFEST.MF` 中声明，并为显示进行格式化（括号包围并以 `v` 作为前缀）。比如 `(v1.0)`。 |
| `${spring-boot.version}`                                     | 你使用的 Spring Boot 版本。比如 `2.2.2.RELEASE`。            |
| `${spring-boot.formatted-version}`                           | 你使用的 Spring Boot 版本，并为显示进行格式化（括号包围并以 `v` 作为前缀）。比如 `(v2.2.2.RELEASE)`。 |
| `${Ansi.NAME}` (or `${AnsiColor.NAME}`, `${AnsiBackground.NAME}`, `${AnsiStyle.NAME}`) | 其中 `NAME` 是 ANSI 转义代码的名称。参见 [`AnsiPropertySource`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/ansi/AnsiPropertySource.java) 以获取详细信息。 |
| `${application.title}`                                       | 您的应用程序的标题，在`MANIFEST.MF`中声明。例如，`Implementation-Title:MyApp` 被打印为 `MyApp`。 |

> 如果您要以编程方式生成横幅，则可以使用 `SpringApplication.setBanner(…)` 方法。使用 `org.springframework.boot.Banner` 接口并实现自己的 `printBanner()` 方法。

您还可以使用 `spring.main.banner-mode` 属性来确定横幅是否必须在 `System.out` (`console`) 上打印，发送到已配置的记录器（`log`）还是不生成（`off`）。

打印的横幅以以下名称注册为单例 bean：`springBootBanner`。

