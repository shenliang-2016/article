#### 7.2.1. 使用 CLI 运行应用

您可以使用 `run` 命令来编译和运行 Groovy 源代码。Spring Boot CLI 是完全独立的，因此您不需要任何外部 Groovy 安装。

以下示例显示了用 Groovy 编写的“hello world”  Web 应用程序：

**hello.groovy**

```groovy
@RestController
class WebApplication {

    @RequestMapping("/")
    String home() {
        "Hello World!"
    }

}
```

编译和运行应用，使用下面的命令：

```
$ spring run hello.groovy
```

要将命令行参数传递给应用程序，请使用 `--` 将命令与 “spring” 命令参数分开，如以下示例所示：

```
$ spring run hello.groovy -- --server.port=9000
```

要设置 JVM 命令行参数，可以使用 `JAVA_OPTS` 环境变量，如以下示例所示：

```
$ JAVA_OPTS=-Xmx1024m spring run hello.groovy
```

> 在 Microsoft Windows 上设置 `JAVA_OPTS` 时，请确保引用整个指令，例如 `set "JAVA_OPTS=-Xms256m -Xmx2048m"` 。这样做可以确保将值正确传递到进程。

