#####  自定义启动脚本

由 Maven 或 Gradle 插件编写的默认嵌入式启动脚本可以通过多种方式进行自定义。对于大多数人来说，使用默认脚本以及一些自定义设置通常就足够了。如果发现无法自定义所需的内容，请使用 `embeddedLaunchScript` 选项完全编写自己的文件。

###### 编写时自定义启动脚本

在将启动脚本写入 jar 文件时，自定义启动脚本的元素通常很有意义。例如，init.d 脚本可以提供“描述”。由于您已经预先了解了描述（并且无需更改），因此在生成 jar 时也可以提供它。

要自定义编写好的元素，使用 Spring Boot Maven plugin 的 `embeddedLaunchScriptProperties` 选项或者 [Spring Boot Gradle plugin `launchScript` 的 `properties` 属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/gradle-plugin/reference/html//#packaging-executable-configuring-launch-script).

默认脚本支持以下属性替换：

| Name                       | Description                                                  | Gradle default                                               | Maven default                                                |
| :------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `mode`                     | 脚本模式                                                     | `auto`                                                       | `auto`                                                       |
| `initInfoProvides`         | “INIT INFO” 的 `Provides` 部分                               | `${task.baseName}`                                           | `${project.artifactId}`                                      |
| `initInfoRequiredStart`    | “INIT INFO” 的 `Required-Start` 部分                         | `$remote_fs $syslog $network`                                | `$remote_fs $syslog $network`                                |
| `initInfoRequiredStop`     | “INIT INFO” 的 `Required-Stop`  部分                         | `$remote_fs $syslog $network`                                | `$remote_fs $syslog $network`                                |
| `initInfoDefaultStart`     | “INIT INFO” 的 `Default-Start` 部分                          | `2 3 4 5`                                                    | `2 3 4 5`                                                    |
| `initInfoDefaultStop`      | “INIT INFO” 的 `Default-Stop` 部分                           | `0 1 6`                                                      | `0 1 6`                                                      |
| `initInfoShortDescription` | “INIT INFO” 的 `Short-Description` 部分                      | Single-line version of `${project.description}` (falling back to `${task.baseName}`) | `${project.name}`                                            |
| `initInfoDescription`      | “INIT INFO” 的 `Description` 部分                            | `${project.description}` (falling back to `${task.baseName}`) | `${project.description}` (falling back to `${project.name}`) |
| `initInfoChkconfig`        | “INIT INFO” 的 `chkconfig` 部分                              | `2345 99 01`                                                 | `2345 99 01`                                                 |
| `confFolder`               | `CONF_FOLDER` 的默认值                                       | Folder containing the jar                                    | Folder containing the jar                                    |
| `inlinedConfScript`        | 引用应在默认启动脚本中内联的文件脚本。这可以用来在加载任何外部配置文件之前设置环境变量，例如 `JAVA_OPTS`。 |                                                              |                                                              |
| `logFolder`                | `LOG_FOLDER` 的默认值，仅对 `init.d` 服务有效。              |                                                              |                                                              |
| `logFilename`              | `LOG_FILENAME` 的默认值，仅对 `init.d` 服务有效。            |                                                              |                                                              |
| `pidFolder`                | `PID_FOLDER` 的默认值，仅对 `init.d` 服务有效。              |                                                              |                                                              |
| `pidFilename`              | `PID_FOLDER` 中 PID 文件名的默认值，仅对 `init.d` 服务有效。 |                                                              |                                                              |
| `useStartStopDaemon`       | 是否可以使用 `start-stop-daemon` 命令来控制该过程            | `true`                                                       | `true`                                                       |
| `stopWaitTime`             | `STOP_WAIT_TIME` 的默认值，单位秒，仅对 `init.d` 服务有效。  | 60                                                           | 60                                                           |

###### 在运行时自定义脚本

对于*编写* jar 之后需要定制的脚本项目，可以使用环境变量或 [config文件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#deployment-script-customization-conf-file)。

默认脚本支持以下环境属性：

| Variable                | Description                                                  |
| :---------------------- | :----------------------------------------------------------- |
| `MODE`                  | 操作的“模式”。默认值取决于 jar 的构建方式，但通常为 `auto`（这意味着它会通过检查它是否是目录 `init.d` 中的符号链接来尝试猜测它是否为初始化脚本）。您可以将其显式设置为`service`，以便 `stop|start|status|restart` 命令可以使用，或者如果你想要在前台执行脚本，则可以将其设置为 `run`。 |
| `RUN_AS_USER`           | 将用于运行应用程序的用户。未设置时，将使用拥有 jar 文件的用户。 |
| `USE_START_STOP_DAEMON` | 是否可以使用 `start-stop-daemon` 命令来控制该过程。默认为 `true`。 |
| `PID_FOLDER`            | pid 文件夹的根名称 (默认为 `/var/run`)。                     |
| `LOG_FOLDER`            | 放置日志文件的文件夹名称 (默认为`/var/log`)。                |
| `CONF_FOLDER`           | 从中读取 `.conf` 文件的文件夹的名称（默认情况下与 jar 文件相同的文件夹）。 |
| `LOG_FILENAME`          | `LOG_FOLDER` 中日志文件名称 (默认为 `<appname>.log`)。       |
| `APP_NAME`              | 应用程序的名称。如果 jar 是从符号链接运行的，则脚本会猜测应用程序名称。如果它不是符号链接，或者您要显式设置应用程序名称，则此功能很有用。 |
| `RUN_ARGS`              | 传递给程序（Spring Boot app）的参数。                        |
| `JAVA_HOME`             | `java` 可执行文件的位置默认情况下是通过使用 `PATH` 找到的，但是如果在 `$JAVA_HOME/bin/java` 目录中有可执行文件，则可以显式设置它。 |
| `JAVA_OPTS`             | JVM 启动时传递给它的选项。                                   |
| `JARFILE`               | jar 文件的显式位置，以防脚本被用于启动实际上未嵌入的 jar。   |
| `DEBUG`                 | 如果不为空，请在 shell 进程中设置 `-x` 标志，从而易于查看脚本中的逻辑。 |
| `STOP_WAIT_TIME`        | 停止应用程序之前要强制关闭的等待时间（以秒为单位）（默认为60）。 |

> `PID_FOLDER`，`LOG_FOLDER` 和 `LOG_FILENAME` 变量仅对 `init.d` 服务有效。对于 `systemd`，等效的自定义是通过使用 'service' 脚本进行的。有关更多详细信息，请参见 [服务单元配置手册页](https://www.freedesktop.org/software/systemd/man/systemd.service.html)。

除 `JARFILE` 和 `APP_NAME` 外，上一节中列出的设置都可以使用 `.conf` 文件进行配置。该文件应该在 jar 文件的旁边，并且具有相同的名称，但后缀为 `.conf` 而不是 `.jar`。例如，名为 `/var/myapp/myapp.jar` 的 jar 使用名为 `/var/myapp/myapp.conf` 的配置文件，如以下示例所示：

**myapp.conf**

```
JAVA_OPTS=-Xmx1024M
LOG_FOLDER=/custom/log/folder
```

> 如果您不喜欢在 jar 文件旁边放置配置文件，则可以设置一个 `CONF_FOLDER` 环境变量来自定义配置文件的位置。

要了解有关适当保护此文件的信息，请参阅 [保护 init.d 服务的准则](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#deployment-initd-service-securing)。

#### 6.3.3. Microsoft Windows 服务

可以使用 [`winsw`](https://github.com/kohsuke/winsw) 将 Spring Boot 应用程序作为 Windows 服务启动。

[单独维护的示例](https://github.com/snicoll-scratches/spring-boot-daemon) 逐步描述了如何为 Spring Boot 应用程序创建 Windows 服务。

### 6.4. 进一步学习

查看 [Cloud Foundry](https://www.cloudfoundry.org/)，[Heroku](https://www.heroku.com/)，[OpenShift](https://www.openshift.com/ ) 和 [Boxfuse](https://boxfuse.com/) 网站，以获取有关 PaaS 可以提供的各种功能的更多信息。这些只是最受欢迎的 Java PaaS 提供程序中的四个。由于 Spring Boot 非常适合基于云的部署，因此您也可以自由考虑其他提供商。

下一部分将继续介绍  *Spring Boot CLI*，或者您也可以直接阅读有关 *build tool plugins* 的内容。

