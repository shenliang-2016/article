#### 7.2.4. 初始化一个新项目

`init` 命令允许你通过使用 [start.spring.io](https://start.spring.io/) 创建新项目而不需要离开 shell，如下面例子所示：

```
$ spring init --dependencies=web,data-jpa my-project
Using service at https://start.spring.io
Project extracted to '/Users/developer/example/my-project'
```

前面的示例使用 `spring-boot-starter-web` 和 `spring-boot-starter-data-jpa` 的基于 Maven 的项目创建了一个 `my-project` 目录。您可以通过使用 `--list` 标志来列出服务的功能，如以下示例所示：

```
$ spring init --list
=======================================
Capabilities of https://start.spring.io
=======================================

Available dependencies:
-----------------------
actuator - Actuator: Production ready features to help you monitor and manage your application
...
web - Web: Support for full-stack web development, including Tomcat and spring-webmvc
websocket - Websocket: Support for WebSocket development
ws - WS: Support for Spring Web Services

Available project types:
------------------------
gradle-build -  Gradle Config [format:build, build:gradle]
gradle-project -  Gradle Project [format:project, build:gradle]
maven-build -  Maven POM [format:build, build:maven]
maven-project -  Maven Project [format:project, build:maven] (default)

...
```

`init` 命令支持许多选项。请参阅 `help` 输出以获取更多详细信息。例如，以下命令创建一个使用 Java 8 和 `war` 打包的 Gradle 项目：

```
$ spring init --build=gradle --java-version=1.8 --dependencies=websocket --packaging=war sample-app.zip
Using service at https://start.spring.io
Content saved to 'sample-app.zip'
```

#### 7.2.5. 使用内置 Shell

Spring Boot 包含用于 BASH 和 zsh shell 的命令行完成脚本。如果您不使用这两个 shell 程序（也许您是 Windows 用户），则可以使用 `shell` 命令启动内置集成 shell 程序，如以下示例所示：

```
$ spring shell
Spring Boot (v2.2.2.RELEASE)
Hit TAB to complete. Type \'help' and hit RETURN for help, and \'exit' to quit.
```

从内置 shell 内部，你可以直接运行其它命令：

```
$ version
Spring CLI v2.2.2.RELEASE
```

嵌入式 shell 支持 ANSI 颜色输出以及 `tab` 补全。如果需要运行本机命令，则可以使用 `!` 前缀。要退出嵌入式外壳，请按 `ctrl-c`。

#### 7.2.6. 添加扩展到 CLI

您可以使用 `install` 命令将扩展添加到 CLI。该命令采用 `group:artifact:version` 格式的一组或多组工件坐标，如以下示例所示：

```
$ spring install com.example:spring-boot-cli-extension:1.0.0.RELEASE
```

除了安装由您提供的坐标标识的工件之外，还将安装所有工件的依赖项。

要卸载一个依赖，使用 `uninstall` 命令。与 `install` 命令一样，它采用 `group:artifact:version` 格式的一组或多组工件坐标，如以下示例所示：

```
$ spring uninstall com.example:spring-boot-cli-extension:1.0.0.RELEASE
```

它将卸载由您提供的坐标及其依赖项标识的工件。

要卸载所有其他依赖项，可以使用 `--all` 选项，如以下示例所示：

```
$ spring uninstall --all
```