## 7. Spring Boot CLI

Spring Boot CLI 是一个命令行工具，如果您想快速开发 Spring 应用程序，可以使用它。它使您可以运行 Groovy 脚本，这意味着您具有类似 Java 的熟悉语法，而没有太多样板代码。您也可以引导一个新项目或为它编写自己的命令。

### 7.1. 安装 CLI

可以使用 SDKMAN! 手动安装 Spring Boot CLI（命令行界面），或使用 Homebrew 或 MacPorts（如果您是 OSX 用户）。请参阅“入门”部分中的“安装 Spring Boot CLI”以获取全面的安装说明。

### 7.2. 使用 CLI

一旦安装了 CLI，就可以通过键入 `spring` 并在命令行中按 Enter 来运行它。如果您在不带任何参数的情况下运行 `spring`，则会显示一个简单的帮助屏幕，如下所示：

```
$ spring
usage: spring [--help] [--version]
       <command> [<args>]

Available commands are:

  run [options] <files> [--] [args]
    Run a spring groovy script

  ... more command help is shown here
```

您可以输入 `spring help` 以获取有关任何受支持命令的更多详细信息，如以下示例所示：

```
$ spring help run
spring run - Run a spring groovy script

usage: spring run [options] <files> [--] [args]

Option                     Description
------                     -----------
--autoconfigure [Boolean]  Add autoconfigure compiler
                             transformations (default: true)
--classpath, -cp           Additional classpath entries
--no-guess-dependencies    Do not attempt to guess dependencies
--no-guess-imports         Do not attempt to guess imports
-q, --quiet                Quiet logging
-v, --verbose              Verbose logging of dependency
                             resolution
--watch                    Watch the specified file for changes
```

 `version` 命令提供了一种快速的方法来检查您使用的 Spring Boot 版本，如下所示：

```
$ spring version
Spring CLI v2.2.2.RELEASE
```

