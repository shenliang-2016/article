# Spring Boot Reference Documentation

Phillip Webb, Dave Syer, Josh Long, Stéphane Nicoll, Rob Winch, Andy Wilkinson, Marcel Overdijk, Christian Dupuis, Sébastien Deleuze, Michael Simons, Vedran Pavić, Jay Bryant, Madhura Bhave

----

## 法律

2.2.2.RELEASE

版权所有©2012-2019

本文档的副本可以供您自己使用，也可以分发给他人，但前提是您不对此类副本收取任何费用，并且还应确保每份副本均包含本版权声明（无论是印刷版本还是电子版本）。

----

## 1. Spring Boot文档

本节简要概述了Spring Boot参考文档。它用作文档其余部分的地图。

### 1.1. 关于文档

Spring Boot参考指南可通过以下方式获得：

- [多页HTML](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/html)
- [单页HTML](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle)
- [PDF格式](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/pdf/spring-boot-reference.pdf)

最新的副本可在 [docs.spring.io/spring-boot/docs/current/reference](https://docs.spring.io/spring-boot/docs/current/reference) 中找到。

本文档的副本可以供您自己使用，也可以分发给他人，但前提是您不对此类副本收取任何费用，并且还应确保每份副本均包含本版权声明（无论是印刷版本还是电子版本）。

### 1.2. 获得帮助

如果您在使用Spring Boot时遇到问题，我们将为您提供帮助。

- 尝试使用[How-to 文档](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto)。他们为最常见的问题提供解决方案。
- 了解Spring基础知识。Spring Boot建立在许多其他Spring项目上。在[spring.io](https://spring.io/)网站上查看大量参考文档。如果您是从Spring开始的，请尝试其中的[指南之一](https://spring.io/guides)。
- 问一个问题。我们监视[stackoverflow.com](https://stackoverflow.com/)上是否有标记为的问题[`spring-boot`](https://stackoverflow.com/tags/spring-boot)。
- 在[github.com/spring-projects/spring-boot/issues上](https://github.com/spring-projects/spring-boot/issues)报告Spring Boot的[错误](https://github.com/spring-projects/spring-boot/issues)。

> 所有的Spring Boot都是开源的，包括文档。如果您发现文档有问题或想要改进它们，请[参与其中](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE)。

### 1.3. 第一步

如果您通常是从Spring Boot或“ Spring”开始的，请[从以下主题](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started)开始：

- **从头开始：** [概述](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started-introducing-spring-boot) | [要求](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started-system-requirements) | [安装](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started-installing-spring-boot)
- **教程：** [第1部分](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started-first-application) | [第2部分](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started-first-application-code)
- **运行示例：** [第1部分](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started-first-application-run) | [第2部分](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started-first-application-executable-jar)

### 1.4. 使用Spring Boot

准备好实际开始使用Spring Boot了吗？[我们为您服务](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot)：

- **构建系统：** [Maven](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-maven) | [Gradle](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-gradle) | [Ant](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-ant) | [Starters](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-starter)
- **最佳实践：** [代码结构](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-structuring-your-code) | [@Configuration](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-configuration-classes) | [@EnableAutoConfiguration](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-auto-configuration) | [Bean和依赖注入](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-spring-beans-and-dependency-injection)
- **运行您的代码：** [IDE](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-running-from-an-ide) | [Packaged](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-running-as-a-packaged-application) | [Maven](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-running-with-the-maven-plugin) | [Gradle](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-running-with-the-gradle-plugin)
- **包装您的应用程序：** [Production jars](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-packaging-for-production)
- **Spring Boot CLI：** [使用CLI](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#cli)

### 1.5. 了解Spring Boot功能

是否需要有关Spring Boot核心功能的更多信息？ [以下内容适合您](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features)：

- **核心功能：** [SpringApplication](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-application) | [外部配置](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config) | [Profiles](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-profiles) | [Logging](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-logging)
- **Web应用程序：** [MVC](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc) | [嵌入式容器](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-embedded-container)
- **处理数据：** [SQL](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-sql) | [NO-SQL](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-nosql)
- **消息：** [概述](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-messaging) | [JMS](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-jms)
- **测试：** [概述](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing) | [Boot  Applications](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications) | [Utils](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-test-utilities)
- **扩展：** [自动配置](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-developing-auto-configuration) | [@Conditions](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-condition-annotations)

### 1.6. 转向生产

当您准备将Spring Boot应用程序投入生产时，我们可能会喜欢[一些技巧](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready)：

- **管理端点：** [概述](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-endpoints)
- **连接选项：** [HTTP](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-monitoring) | [JMX](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-jmx)
- **监控：** [Metrics](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics) | [Auditing](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-auditing) | [HTTP Tracing](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-http-tracing) | [Process](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-process-monitoring)

### 1.7. 进阶主题

最后，我们为高级用户提供了一些主题：

- **春季启动应用程序部署：** [云部署](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#cloud-deployment) | [操作系统服务](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#deployment-service)
- **构建工具插件：** [Maven](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#build-tool-plugins-maven-plugin) | [Gradle](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#build-tool-plugins-gradle-plugin)
- **附录：** [应用程序属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#common-application-properties) | [配置元数据](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#configuration-metadata) | [自动配置类](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#auto-configuration-classes) | [测试自动配置注解](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) | [Executable jars](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#executable-jar) | [依赖版本](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#appendex-dependency-versions)

----

## 2.入门

如果您是从Spring Boot或“ Spring”开始的，请先阅读本节。它回答了基本的“是什么？”，“如何？”和“为什么？”问题。它包括对Spring Boot的介绍以及安装说明。然后，我们将引导您构建第一个Spring Boot应用程序，并讨论一些核心原理。

### 2.1. 介绍Spring Boot

Spring Boot使创建可运行的独立，生产级基于Spring的应用程序变得容易。我们对Spring平台和第三方库持固有的观点，这样您就可以以最小的代价开始使用。大多数Spring Boot应用程序只需要很少的Spring配置。

您可以使用Spring Boot创建可以通过使用 `java -jar` 或更传统的 war 包部署启动的Java应用程序。我们还提供了一个运行“ spring脚本”的命令行工具。

我们的主要目标是：

- 为所有Spring开发提供根本上更快且可广泛访问的入门体验。
- 开箱即用，但如果需求与默认值有所出入，也能迅速适配。
- 提供一系列大型项目通用的非功能性功能（例如嵌入式服务器，安全性，指标，运行状况检查和外部化配置）。
- 完全没有代码生成，也不需要XML配置。

### 2.2. 系统要求

Spring Boot 2.2.2.RELEASE需要[Java 8](https://www.java.com/)。并且与Java 13（包括）兼容。 还需要[Spring Framework 5.2.2.RELEASE](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/)或更高版本。

为以下构建工具提供了明确的构建支持：

| 制作工具 | 版                               |
| :------- | :------------------------------- |
| Maven    | 3.3+                             |
| Gradle   | 5.x和6.x（也支持4.10，但已弃用） |

#### 2.2.1. Servlet容器

Spring Boot支持以下嵌入式servlet容器：

| 名称         | Servlet版本 |
| :----------- | :---------- |
| Tomcat 9.0   | 4.0         |
| Jetty 9.4    | 3.1         |
| Undertow 2.0 | 4.0         |

您还可以将Spring Boot应用程序部署到任何Servlet 3.1+兼容的容器中。

### 2.3. 安装Spring Boot

Spring Boot可以与“经典” Java开发工具一起使用，也可以作为命令行工具安装。无论哪种方式，都需要[Java SDK v1.8](https://www.java.com/)或更高版本。在开始之前，您应该使用以下命令检查当前的Java安装：

```
$ java -version
```

如果您不熟悉Java开发，或者想尝试使用Spring Boot，则可能要先尝试使用[Spring Boot CLI](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started-installing-the-cli)（命令行界面）。否则，请继续阅读“经典”安装说明。

#### 2.3.1. Java开发人员的安装说明

您可以像使用任何标准Java库一样使用Spring Boot。为此，请将适当的 `spring-boot-*.jar` 文件放置在类路径中。Spring Boot不需要任何特殊的工具集成，因此您可以使用任何IDE或文本编辑器。而且，Spring Boot应用程序没有什么特别之处，因此您可以像运行其他Java程序一样运行和调试Spring Boot应用程序。

尽管您*可以*复制Spring Boot jars，但是我们通常建议您使用支持依赖关系管理的构建工具（例如Maven或Gradle）。

##### Maven安装

Spring Boot与Apache Maven 3.3或更高版本兼容。如果尚未安装Maven，则可以按照[maven.apache.org上](https://maven.apache.org/)的说明进行操作。

> 在许多操作系统上，Maven可以与程序包管理器一起安装。如果您使用OSX Homebrew，请尝试 `brew install maven`。Ubuntu用户可以运行 `sudo apt-get install maven`。具有[Chocolatey](https://chocolatey.org/) 的Windows用户可以 `choco install maven` 从提升的（管理员）提示符下运行。

Spring Boot依赖项使用 `org.springframework.boot` `groupId`。通常，您的Maven POM文件从 `spring-boot-starter-parent` 项目继承，并声明对一个或多个[“启动器”](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-starter)的依赖关系。Spring Boot还提供了一个可选的[Maven插件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#build-tool-plugins-maven-plugin)来创建可执行jar。

以下清单显示了一个典型的 `pom.xml` 文件：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>myproject</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <!-- Inherit defaults from Spring Boot -->
    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.2.RELEASE</version>
    </parent>

    <!-- Override inherited settings -->
    <description/>
    <developers>
        <developer/>
    </developers>
    <licenses>
        <license/>
    </licenses>
    <scm>
        <url/>
    </scm>
    <url/>

    <!-- Add typical dependencies for a web application -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
    </dependencies>

    <!-- Package as an executable jar -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
    </build>

</project>
````

> `spring-boot-starter-parent` 是使用Spring Boot的一种很好的方法，但是可能并不总是适合。有时您可能需要从其他父POM继承，或者您可能不喜欢我们的默认设置。在这些情况下，请参阅[使用没有父POM的Spring Boot](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-maven-without-a-parent)，以获得使用`import`的替代解决方案。

##### Gradle 安装

Spring Boot与5.x和6.x兼容，还支持4.10，但在将来的版本中将删除该支持。如果尚未安装Gradle，则可以按照[gradle.org上](https://gradle.org/)的说明进行[操作](https://gradle.org/)。

可以使用`org.springframework.boot` `group`来声明Spring Boot依赖项。通常，您的项目声明对一个或多个[“启动器”](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-starter)的依赖。Spring Boot提供了一个有用的[Gradle插件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#build-tool-plugins-gradle-plugin)，可用于简化依赖项声明和创建可执行jar。

> Gradle 包装器
>
> 当您需要构建项目时，Gradle包装器提供了一种“获取” Gradle的好方法。这是一个小的脚本和库，您随代码一起提交以引导构建过程。有关详细信息，请参见[gradle_wrapper.html](https://docs.gradle.org/current/userguide/gradle_wrapper.html)。

有关Spring Boot和Gradle [入门](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/gradle-plugin/reference/html//#getting-started) 的更多详细信息，可以在Gradle插件参考指南的 [“入门”](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/gradle-plugin/reference/html//#getting-started) 部分中找到。

#### 2.3.2. 安装Spring Boot CLI

Spring Boot CLI（命令行界面）是一个命令行工具，可用于快速使用Spring进行原型设计。它使您可以运行[Groovy](http://groovy-lang.org/)脚本，这意味着您具有类似Java的熟悉语法，而没有太多样板代码。

您无需使用CLI即可与Spring Boot一起工作，但这绝对是使Spring应用程序启动的最快方法。

##### 手动安装

你可以从 Spring 软件仓库下载 Spring CLI 分发版本：

- [spring-boot-cli-2.2.2.RELEASE-bin.zip](https://repo.spring.io/release/org/springframework/boot/spring-boot-cli/2.2.2.RELEASE/spring-boot-cli-2.2.2.RELEASE-bin.zip)
- [spring-boot-cli-2.2.2.RELEASE-bin.tar.gz](https://repo.spring.io/release/org/springframework/boot/spring-boot-cli/2.2.2.RELEASE/spring-boot-cli-2.2.2.RELEASE-bin.tar.gz)

也提供最先进的 [快照分发](https://repo.spring.io/snapshot/org/springframework/boot/spring-boot-cli/)。

下载完成后，请按照解压缩后的归档文件中的[INSTALL.txt](https://raw.githubusercontent.com/spring-projects/spring-boot/v2.2.2.RELEASE/spring-boot-project/spring-boot-cli/src/main/content/INSTALL.txt)说明进行操作。总而言之，`.zip`文件中的`bin/`目录中有一个`spring`脚本（对于Windows是`spring.bat`）。或者，您可以通过 `java -jar` 使用该 `.jar` 文件（脚本可帮助您确保正确设置类路径）。

##### SDKMAN! 安装

SDKMAN!（软件开发工具包管理器）可用于管理各种二进制SDK的多个版本，包括Groovy和Spring Boot CLI。从[sdkman.io](https://sdkman.io/) 获取 SDKMAN! 并使用以下命令安装Spring Boot：

```
$ sdk install springboot
$ spring --version
Spring Boot v2.2.2.RELEASE
```

如果您为CLI开发功能并希望轻松访问所构建的版本，请使用以下命令：

```
$ sdk install springboot dev /path/to/spring-boot/spring-boot-cli/target/spring-boot-cli-2.2.2.RELEASE-bin/spring-2.2.2.RELEASE/
$ sdk default springboot dev
$ spring --version
Spring CLI v2.2.2.RELEASE
```

前面的说明安装的`spring`本地实例称为`dev`实例。它指向您的目标构建位置，因此每次重建Spring Boot `spring`都是最新的。

您可以通过运行以下命令来查看它：

```
$ sdk ls springboot

================================================================================
Available Springboot Versions
================================================================================
> + dev
* 2.2.2.RELEASE

================================================================================
+ - local version
* - installed
> - currently in use
================================================================================
```

##### OSX Homebrew 安装

如果你在 Mac 上工作并使用 [Homebrew](https://brew.sh/)，你可以通过以下命令安装 Spring Boot CLI ：

```
$ brew tap pivotal/tap
$ brew install springboot
```

Homebrew 安装 `spring` 到 `/usr/local/bin`。

> 如果你没有看到输出，你的 brew 安装可能已经过时了。运行 `brew update` 升级然后重试。

##### MacPorts 安装

如果你在 Mac 上工作并使用 [MacPorts](https://www.macports.org/)，你可以使用以下命令安装 Spring Boot CLI ：

```
$ sudo port install spring-boot-cli
```

##### 命令行补全

Spring Boot CLI包括为[BASH](https://en.wikipedia.org/wiki/Bash_(Unix_shell))和[zsh](https://en.wikipedia.org/wiki/Z_shell) Shell 提供命令补全的脚本。您可以使用`source`命令将脚本（也称为`spring`）放在任何shell中，或将其放在个人或系统范围内的bash补全初始化文件目录中。在Debian系统上，系统范围的脚本位于`/shell-completion/bash`并且在启动新的Shell时将执行该目录中的所有脚本。例如，如果您是使用SDKMAN!安装的，则要手动运行脚本，请使用以下命令：

```
$ . ~/.sdkman/candidates/springboot/current/shell-completion/bash/spring
$ spring <HIT TAB HERE>
  grab  help  jar  run  test  version
```

> 如果使用Homebrew或MacPorts安装Spring Boot CLI，则命令行补全脚本会自动注册到您的Shell中。

##### Windows Scoop 安装

如果你工作在 Windows 上并使用 [Scoop](https://scoop.sh/)，你可以使用下面的命令安装 Spring Boot CLI：

```
> scoop bucket add extras
> scoop install springboot
```

Scoop 安装 `spring` 到 `~/scoop/apps/springboot/current/bin`.

> 如果你没有看到应用清单，你的 scoop 可能已经过时。运行 `scoop update` 然后重试。

##### 快速入门Spring CLI示例

您可以使用以下Web应用程序来测试安装。首先，创建一个名为的文件`app.groovy`，如下所示：

```groovy
@RestController
class ThisWillActuallyRun {

    @RequestMapping("/")
    String home() {
        "Hello World!"
    }

}
```

从 shell 运行它：

```
$ spring run app.groovy
```

> 首次运行会比较慢，因为需要下载依赖。后续的执行会快很多。

在浏览器中访问 `localhost:8080` 。你应该看到下面的输出：

```
Hello World!
```

#### 2.3.3. 从早期版本的 Spring Boot 升级

如果你要从 Spring Boot `1.x` 版本升级，参考 [“migration guide” on the project wiki](https://github.com/spring-projects/spring-boot/wiki/Spring-Boot-2.0-Migration-Guide) 提供的详细升级建议。同时参考列出详细升级内容的 [“release notes”](https://github.com/spring-projects/spring-boot/wiki) 。

当升级到新版本时，一些属性可能已经改名或者删除。Spring Boot 提供了一种方法分析你的应用环境并在启动时打印诊断信息，同时还会在运行时为你临时迁移属性。为了启用此特性，添加如下依赖到你的项目：

```xml-dtd
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-properties-migrator</artifactId>
    <scope>runtime</scope>
</dependency>
```

> 较晚被添加到环境中的属性，比如使用 `@PropertySource` 时，将不会被考虑。

> 一旦你完成了迁移，请确保从项目依赖中删除此模块。

为了升级现存的 CLI 安装，使用合适的包管理器命令（比如，`brew upgrade`）。如果你手动安装 CLI，请按照 [standard instructions](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started-manual-cli-installation) 操作，记得更新你的 `PATH` 环境变量来删除所有老的引用。

### 2.4. 开发第一个 Spring Boot 应用

本节描述如何开发一个简单的"Hello World" web 应用，其中重点突出一些 Spring Boot 的核心特性。我们使用 Maven 构建此项目，绝大多数 IDE 都支持它。

> [spring.io](https://spring.io/) 网站包含许多使用 Spring Boot 的 “Getting Started” [guides](https://spring.io/guides) 。如果你需要解决特定问题，首先参考它们。
>
> 你可以到 [start.spring.io](https://start.spring.io/) 并从依赖搜索器中选择 `Web` starter 来绕过下面的步骤。这样做可以直接生成一个新的项目结构，你就可以 [直接开始编写业务代码](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started-first-application-code)。参考 [Spring Initializr documentation](https://docs.spring.io/initializr/docs/current/reference/html//#user-guide) 获取更多细节。

开始之前，打开终端执行下面的命令来确保你已经安装了适当版本的 Java 和 Maven：

```
$ java -version
java version "1.8.0_102"
Java(TM) SE Runtime Environment (build 1.8.0_102-b14)
Java HotSpot(TM) 64-Bit Server VM (build 25.102-b14, mixed mode)
```

````
$ mvn -v
Apache Maven 3.5.4 (1edded0938998edf8bf061f1ceb3cfdeccf443fe; 2018-06-17T14:33:14-04:00)
Maven home: /usr/local/Cellar/maven/3.3.9/libexec
Java version: 1.8.0_102, vendor: Oracle Corporation
````

> 下面的示例代码需要创建在它自己的目录下。后续的命令都假定你已经创建了合适的目录，并且就是你的当前目录。

#### 2.4.1. 创建 POM

我们需要从创建 Maven `pom.xml` 文件开始。该文件是构建你的项目的配方。打开你喜欢的文本编辑器并添加下列内容：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>myproject</artifactId>
    <version>0.0.1-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.2.2.RELEASE</version>
    </parent>

    <description/>
    <developers>
        <developer/>
    </developers>
    <licenses>
        <license/>
    </licenses>
    <scm>
        <url/>
    </scm>
    <url/>

    <!-- Additional lines to be added here... -->

</project>
```

上面的文件内容可以给你一个可以工作的构建配置。你可以使用 `mvn package` 命令测试一下（目前，你可以忽略  “jar will be empty - no content was marked for inclusion!” 警告）。

> 现在，你可以将项目导入 IDE，绝大多数现代 Java IDE 都包含了 Maven 内建支持。简单起见，这个例子我们继续使用文本编辑器。

#### 2.4.2. 添加类路径依赖

Spring Boot 提供了大量的 Starters 帮助你添加依赖 jars 到类路径。我们用于冒烟测试的应用使用了 POM 文件中 `parent` 小节中的 `spring-boot-starter-parent` 。该 `spring-boot-starter-parent` 是一个特殊的启动器，提供了很有用的 Maven 默认配置。同时提供了 [`dependency-management`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-dependency-management) 小节进行依赖管理，因此你可以在具体的依赖中省略 `version` 标签。

其他启动器提供了开发特定类型的应用时可能需要的依赖。由于我们现在要开发一个 web 应用，因此添加 `spring-boot-starter-web` 依赖。在此之前，我们可以运行下面命令来查看我们已经拥有的依赖：

```
$ mvn dependency:tree

[INFO] com.example:myproject:jar:0.0.1-SNAPSHOT
```

`mve dependency:tree` 命令以树形打印你的项目的依赖。你可以看到 `spring-boot-starter-parent` 本身并不提供任何依赖。为了添加必要的依赖，编辑你的 `pom.xml` 文件并在 `parent` 小节之后添加 `spring-boot-starter-web` 依赖：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
</dependencies>
```

再次执行 `mvn dependency:tree`，你将看到大量依赖已经被添加进来，包括 Tomcat web server 和 Spring Boot 本身。

#### 2.4.3. 编写代码

为了完成我们的应用，我们需要创建一个 java 文件。默认地，Maven 编译 `src/main/java` 目录下的源代码文件，所以你需要创建该文件目录，然后创建名为 `src/main/java/Example.java` 的文件，包含以下代码：

```java
import org.springframework.boot.*;
import org.springframework.boot.autoconfigure.*;
import org.springframework.web.bind.annotation.*;

@RestController
@EnableAutoConfiguration
public class Example {

    @RequestMapping("/")
    String home() {
        return "Hello World!";
    }

    public static void main(String[] args) {
        SpringApplication.run(Example.class, args);
    }

}
```

尽管只有寥寥几行代码，实际上已经做了很多工作。我们将会在下面逐步介绍所有的关键内容。

##### @RestController 和 @RequestMapping 注解

我们 `Example` 类上的第一个注解是 `@RestController` 。众所周知，这是一个所谓的 *模板* 注解。它提示代码阅读者和 Spring ，该类在应用中扮演一个特殊角色。例子的场景下，我们的类是一个 web `@Controller` 。因此，Spring 在处理到来的 web 请求时就会考虑它。

`@RequestMapping` 注解提供了"路由"信息。它告诉 Spring ，所有携带 `/` 请求路径的 HTTP 请求都应该被映射到 `home` 方法。`@RestController` 注解告诉 Spring 直接将结果字符串返回给调用者。

> `@RestController` 和 `@RequestMappgin` 注解都是 Spring MVC 注解（并非专用于 Spring Boot）。参考 Spring 参考文档中的 [MVC section](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc) 获取更多细节。

##### @EnableAutoConfiguration 注解

第二个类级别的注解是 `@EnableAutoConfiguration` 。此注解告诉 Spring Boot 来猜测你希望如何配置 Spring ，基于你已经添加的依赖。由于 `spring-boot-starter-web` 添加了 Tomcat 和 Spring MVC，自动配置就会假定你正在开发一个 web 应用，然后为你相应配置 Spring 。

> 启动器和自动配置
>
> 自动配置被设计为可以与启动器良好匹配工作，不过这两个概念本身并没有直接绑定关系。你仍然可以在启动器之外随意选择添加 jar 依赖。Spring Boot 仍然会尽最大努力自动配置你的应用。

##### “main” 方法

我们应用的最后一部分就是 `main` 方法。这就是一个标准的方法，遵循 Java 语言传统作为应用的入口点。我们的 `main` 方法通过调用 `run` 方法委托给 Spring Boot 的 `SpringAppliation` 类。`SpringApplication` 引导我们的应用，启动 Spring，随后，启用自动配置好的 Tomcat web server。我们需要将 `Example.class` 作为参数传递给 `run` 方法，以告诉 `SpringApplication` 哪个类是 Spring 主组件。其中的 `args` 数组被传递以暴露任何命令行参数。

#### 2.4.4. 运行这个例子

此时，你的应用已经可以工作。由于你使用了 `spring-boot-starter-parent` POM，你拥有一个很有用的 `run` 目标可以用来启动应用。在项目的根目录中通过终端执行 `mvn spring-boot:run` 来启动应用。你应该看到类似下面内容的输出：

```
$ mvn spring-boot:run

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::  (v2.2.2.RELEASE)
....... . . .
....... . . . (log output here)
....... . . .
........ Started Example in 2.222 seconds (JVM running for 6.514)
```

在浏览器中访问 `localhost:8080`，你应该看到以下输出：

```
Hello World!
```

优雅地退出应用，请按 `ctrl-c`。

#### 2.4.5. 创建可执行 Jar

我们通过创建可以在生产环境中运行的完全独立的可执行jar文件来结束示例。可执行jar（有时称为“胖jar”）是包含您的已编译类以及代码需要运行的所有jar依赖项的归档文件。

> 可执行 jars 和 Java
>
> Java没有提供加载嵌套jar文件（jar中本身包含的jar文件）的标准方法。如果您要分发独立自包含的应用程序，则可能会出现问题。
>
> 为了解决这个问题，许多开发人员使用“超级”jars。超级jar将来自应用程序所有依赖项的所有类打包到一个存档中。这种方法的问题在于，很难查看应用程序中包含哪些库。如果在多个jar中使用相同的文件名（但具有不同的内容），也可能会产生问题。
>
> Spring Boot采用了 [不同的方法](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#executable-jar)，允许你实际上可以直接嵌套jar。

为了创建可执行 jar，我们需要添加 `spring-boot-maven-plugin` 到你的 `pom.xml` 中。为了做到这一点，将下面的内容添加到 `dependencies` 小节之后：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

> `spring-boot-starter-parent` POM 包含 `<executions>` 配置来绑定 `repackage` 目标。如果你不使用父 POM，你需要自己声明该配置。参考 [plugin documentation](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/maven-plugin//usage.html) 获取更多细节。

保存 `pom.xml` 文件然后从命令行运行 `mvn package` 命令：

```
$ mvn package

[INFO] Scanning for projects...
[INFO]
[INFO] ------------------------------------------------------------------------
[INFO] Building myproject 0.0.1-SNAPSHOT
[INFO] ------------------------------------------------------------------------
[INFO] .... ..
[INFO] --- maven-jar-plugin:2.4:jar (default-jar) @ myproject ---
[INFO] Building jar: /Users/developer/example/spring-boot-example/target/myproject-0.0.1-SNAPSHOT.jar
[INFO]
[INFO] --- spring-boot-maven-plugin:2.2.2.RELEASE:repackage (default) @ myproject ---
[INFO] ------------------------------------------------------------------------
[INFO] ------------------------------------------------------------------------
```

如果你检查 `target` 目录，你应该看到 `my project-0.0.1-SNAPSHOT.jar` 。该文件应该大约 10 MB 大小。如果你想要深入文件内部，使用 `jar tvf` ，如下所示：

```
$ jar tvf target/myproject-0.0.1-SNAPSHOT.jar
```

在 `target` 目录中，你应该还能看到一个更小的文件，名为 `myproject-0.0.1-SNAPSHOT.jar.original` 。这是 Maven 在 Spring Boot 重新打包之前创建的原始jar文件。

要运行应用，使用 `java -jar` 命令，如下所示：

```
$ java -jar target/myproject-0.0.1-SNAPSHOT.jar

  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::  (v2.2.2.RELEASE)
....... . . .
....... . . . (log output here)
....... . . .
........ Started Example in 2.536 seconds (JVM running for 2.864)
```

如前所述，要退出应用，请键入 `ctrl-c`。

### 2.5. 接下来

希望本节提供一些Spring Boot基础知识，并带您逐步编写自己的应用程序。如果您是面向任务的开发人员，则可能要跳至 [spring.io](https://spring.io/) 并查看一些 [入门](https://spring.io/guides/) 指南，用于解决特定的“我该如何使用Spring？”问题。我们还具有特定于Spring Boot的 [How-to](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto) 参考文档。

否则，下一个步骤是阅读*[使用Spring Boot](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot)*。如果您真的很急，还可以继续阅读并了解*[Spring Boot功能](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features)*。

## 3. 使用 Spring Boot

本节介绍更多你使用 Spring Boot 的细节。涵盖构建系统，自动配置，以及如何运行等几个主题。我们同时还会介绍几种 Spring Boot 最佳实践。尽管 Spring Boot 并没有什么特别的地方，它也只是另一个你可以使用的类库，还是存在一些建议可以让你的开发工作更加简单。

如果你刚开始使用 Spring Boot，你应该在深入本节之前阅读 *Getting Started* 向导部分。

### 3.1. 构建系统

强烈推荐你选用支持 [*dependency management*](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-dependency-management) 并且可以根据坐标获取发布到 Maven 中央仓库中的依赖的构建系统。我们推荐选择 Maven 或者 Gradle。Spring Boot 应该可以使用其它构建系统（比如 Ant），但是相关的支持并不是非常好。

#### 3.1.1. 依赖管理

Spring Boot 的每个发行版都提供了它所支持的依赖的列表。实际上，你并不需要为你的构建配置中的所有这些依赖提供版本号，因为 Spring Boot 帮你管理它们。当时升级 Spring Boot 本身时，这些依赖也会一致性地全部升级。

> 如果确实需要，你仍然可以指定依赖版本号来覆盖 Spring Boot 的推荐。

依赖列表包含所有你可以在 Spring Boot 中使用的 spring 模块，以及一系列精选的第三方类库的列表。该列表作为一个标准的 [Bills of Materials (`spring-boot-dependencies`)](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-maven-without-a-parent) 可以同时被 [Maven](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-maven-parent-pom) and [Gradle](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-gradle) 使用。

> Spring Boot的每个发行版都与Spring Framework的基本版本相关联。 我们**强烈**建议您不要指定其版本。

#### 3.1.2. Maven

Maven 用户可以从 `spring-boot-starter-parent` 项目继承以获得明智的默认配置。该父项目提供了以下特性：

- 默认编译级别是 Java 1.8 。
- UTF-8 源代码编码。
- [Dependency Management](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-dependency-management) 配置小节，继承自 `spring-boot-dependencies` pom，管理通用依赖的版本。这种依赖管理允许你当在你的 pom 中用到那些依赖时忽略依赖配置中的 `<version>` 标签。
- 带有 `repackage` 执行 id 的  [`repackage` goal](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/maven-plugin//repackage-mojo.html) 的执行。
- 明智的 [resource 过滤](https://maven.apache.org/plugins/maven-resources-plugin/examples/filter.html) 。
- 明智的插件配置（[exec plugin](https://www.mojohaus.org/exec-maven-plugin/), [Git commit ID](https://github.com/ktoso/maven-git-commit-id-plugin), 和 [shade](https://maven.apache.org/plugins/maven-shade-plugin/)）。
- 对 `application.properties` 和 `application.yml` 等文件明智的资源过滤，包括特定于环境的文件（比如， `application-dev.properties` 和 `application-dev.yml`）。

注意，由于 `application.properties` 和 `application.yml` 文件接受 Spring 风格的占位符（`${...}`），Maven 过滤器已经变成了使用 `@..@` 占位符（你可以通过设定名为 `resource.delimiter` 的 Maven 属性来覆盖它）。

##### 继承父启动器

配置你的项目以继承 `spring-boot-starter-parent`，如下设定 `parent` ：

```xml
<!-- Inherit defaults from Spring Boot -->
<parent>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-parent</artifactId>
    <version>2.2.2.RELEASE</version>
</parent>
```

> 这个依赖中你应该只需要制定 Spring Boot 版本号。如果你引入了额外的启动器，你就可以安全地忽略该版本号。

通过该设置，你还可以通过在你自己的项目中覆盖一个属性来覆盖各个依赖。比如，想要升级到另一个 Spring Data 发行版，你可以添加下面的配置到你的 `pom.xml` 文件中：

```xml
<properties>
    <spring-data-releasetrain.version>Fowler-SR2</spring-data-releasetrain.version>
</properties>
```

> 检查 [`spring-boot-dependencies` pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-dependencies/pom.xml) 了解所有支持的属性的列表。

##### 不继承父 POM 情况下使用 Spring Boot

并非每个人都喜欢从 `spring-boot-starter-parent` POM继承。您可能需要使用自己的公司标准父级，或者可能希望显式声明所有 Maven 配置。

如果您不想使用 `spring-boot-starter-parent`，仍然可以通过使用 `scope=import` 依赖项来保留依赖项管理（而不是插件管理）的好处，如下所示：

```xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <!-- Import dependency management from Spring Boot -->
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>2.2.2.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

如上所述，前面的示例设置不允许您使用属性来覆盖各个依赖项。为了获得相同的结果，您需要在项目的  `dependencyManagement` 中的 `spring-boot-dependencies` 条目之前添加一个条目。例如，要升级到另一个 Spring Data 发行版，您可以将以下元素添加到您的 `pom.xml` 中：

```xml
<dependencyManagement>
    <dependencies>
        <!-- Override Spring Data release train provided by Spring Boot -->
        <dependency>
            <groupId>org.springframework.data</groupId>
            <artifactId>spring-data-releasetrain</artifactId>
            <version>Fowler-SR2</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-dependencies</artifactId>
            <version>2.2.2.RELEASE</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

> 前面的例子中，我们指定了一个 BOM，但是所有依赖类型都可以以同样的方式覆盖。

##### 使用 Spring Boot Maven Plugin

Spring Boot 包含一个 [Maven plugin](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#build-tool-plugins-maven-plugin) ，该插件可以将项目打包为可执行 jar 文件。如果你想要使用它，请将插件添加到你的 `<plugins>` 小节中。如下面例子所示：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
        </plugin>
    </plugins>
</build>
```

> 如果您使用 Spring Boot 启动器的父 pom，则只需添加插件。除非您要更改父级中定义的设置，否则无需对其进行配置。

#### 3.1.3. Gradle

要了解有关将 Spring Boot 与 Gradle 结合使用的信息，请参阅 Spring Boot 的 Gradle 插件的文档：

- Reference ([HTML](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/gradle-plugin/reference/html/) and [PDF](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/gradle-plugin/reference/pdf/spring-boot-gradle-plugin-reference.pdf))
- [API](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/gradle-plugin/reference/api/)

#### 3.1.4. Ant

可以使用 Apache Ant + Ivy 构建 Spring Boot 项目。还可以使用 `spring-boot-antlib` `AntLib` 模块来帮助 Ant 创建可执行 jar。

为了声明依赖关系，典型的 `ivy.xml` 文件看起来类似于以下示例：

```xml
<ivy-module version="2.0">
    <info organisation="org.springframework.boot" module="spring-boot-sample-ant" />
    <configurations>
        <conf name="compile" description="everything needed to compile this module" />
        <conf name="runtime" extends="compile" description="everything needed to run this module" />
    </configurations>
    <dependencies>
        <dependency org="org.springframework.boot" name="spring-boot-starter"
            rev="${spring-boot.version}" conf="compile" />
    </dependencies>
</ivy-module>
```

典型的 `build.xml` 类似于下面例子所示：

```xml
<project
    xmlns:ivy="antlib:org.apache.ivy.ant"
    xmlns:spring-boot="antlib:org.springframework.boot.ant"
    name="myapp" default="build">

    <property name="spring-boot.version" value="2.2.2.RELEASE" />

    <target name="resolve" description="--> retrieve dependencies with ivy">
        <ivy:retrieve pattern="lib/[conf]/[artifact]-[type]-[revision].[ext]" />
    </target>

    <target name="classpaths" depends="resolve">
        <path id="compile.classpath">
            <fileset dir="lib/compile" includes="*.jar" />
        </path>
    </target>

    <target name="init" depends="classpaths">
        <mkdir dir="build/classes" />
    </target>

    <target name="compile" depends="init" description="compile">
        <javac srcdir="src/main/java" destdir="build/classes" classpathref="compile.classpath" />
    </target>

    <target name="build" depends="compile">
        <spring-boot:exejar destfile="build/myapp.jar" classes="build/classes">
            <spring-boot:lib>
                <fileset dir="lib/runtime" />
            </spring-boot:lib>
        </spring-boot:exejar>
    </target>
</project>
```

> 如果您不想使用 `spring-boot-antlib` 模块，请参阅 *从 Ant 构建可执行档案而不使用 spring-boot-antlib* 。

#### 3.1.5. 启动器

启动器是一系列你可以包含到你的应用中的方便的依赖集合描述符。借助启动器，你可以所有你需要的 Spring 及相关技术的一站式服务，而不需要从示例项目代码中拷贝依赖描述符。比如，如果你希望开始使用 Spring 和 JPA 用于数据库访问，将 `spring-boot-starter-data-jpa` 包含到你的项目中即可。

启动器包含大量的快速构建和运行项目所需的依赖项，以及一系列一致性的受支持的托管传递依赖。

> 启动器名称的含义
>
> 所有官方启动器都遵循相似的命名模式：`spring-boot-starter-*`，其中 `*` 表示特定的应用类型。该名称结构在你查找启动器时很有用。集成到许多 IDEs 中的 Maven 插件允许你按照名称搜索依赖。比如，安装相应的 Eclipse 或者 STS 插件之后，你可以在 POM 编辑器界面按 `ctrl-space` 快捷键并键入类型 `spring-boot-starter` 来查找一个完整的启动器列表。
>
> 如 “[Creating Your Own Starter](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-custom-starter)” 小节中所述，第三方启动器名称不应该以 `spring-boot` 开头，因为该前缀为官方 Spring Boot 坐标保留。实际上，第三方启动器名称通常以项目名称开始。比如，一个名为 `thirdpartyproject` 的第三方启动器项目对应的启动器会被命名为 `thirdpartyproject-spring-boot-starter` 。

下面的应用启动器由 Spring Boot 提供，位于 `org.springframework.boot` 组之下：

| Name                                          | Description                                                  | Pom                                                          |
| :-------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `spring-boot-starter`                         | 核心启动器，包含自动配置支持，日志以及 YAML。                | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter/pom.xml) |
| `spring-boot-starter-activemq`                | 使用 Apache ActiveMQ 处理的 JMS 消息的启动器。               | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-activemq/pom.xml) |
| `spring-boot-starter-amqp`                    | 使用 Spring AMQP 和 Rabbit MQ 的启动器。                     | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-amqp/pom.xml) |
| `spring-boot-starter-aop`                     | 使用 Spring AOP 和 AspectJ 进行面向切面编程的启动器。        | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-aop/pom.xml) |
| `spring-boot-starter-artemis`                 | 使用 Apache Artemis 处理的 JMS 消息的启动器。                | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-artemis/pom.xml) |
| `spring-boot-starter-batch`                   | 使用 Spring Batch 的启动器。                                 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-batch/pom.xml) |
| `spring-boot-starter-cache`                   | 使用 Spring 框架缓存支持的启动器。                           | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-cache/pom.xml) |
| `spring-boot-starter-cloud-connectors`        | 使用 Spring Cloud Connectors 的启动器，可简化与 Cloud Foundry 和 Heroku 等云平台中服务的连接。不建议使用 Java CFEnv。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-cloud-connectors/pom.xml) |
| `spring-boot-starter-data-cassandra`          | 使用 Cassandra 分布式数据库和 Spring Data Cassandra 的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-cassandra/pom.xml) |
| `spring-boot-starter-data-cassandra-reactive` | 使用 Cassandra Reactive 分布式数据库和 Spring Data Cassandra 的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-cassandra-reactive/pom.xml) |
| `spring-boot-starter-data-couchbase`          | 使用 Couchbase 文档数据库和 Spring Data Couchbase 的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-couchbase/pom.xml) |
| `spring-boot-starter-data-couchbase-reactive` | 使用 Couchbase 文档数据库和 Spring Data Couchbase Reactive 的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-couchbase-reactive/pom.xml) |
| `spring-boot-starter-data-elasticsearch`      | 使用 Elasticsearch 搜索和分析引擎以及 Spring Data Elasticsearch 的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-elasticsearch/pom.xml) |
| `spring-boot-starter-data-jdbc`               | 使用 Spring Data JDBC 的启动器。                             | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-jdbc/pom.xml) |
| `spring-boot-starter-data-jpa`                | 使用 Spring Data JPA 和 Hibernate 的启动器。                 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-jpa/pom.xml) |
| `spring-boot-starter-data-ldap`               | 使用 Spring Data LDAP 的启动器。                             | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-ldap/pom.xml) |
| `spring-boot-starter-data-mongodb`            | 使用 MongoDB 文档数据库和 Spring Data MongoDB 的启动器。     | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-mongodb/pom.xml) |
| `spring-boot-starter-data-mongodb-reactive`   | 使用 MongoDB 文档数据库和 Spring Data MongoDB Reactive 的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-mongodb-reactive/pom.xml) |
| `spring-boot-starter-data-neo4j`              | 使用 Neo4j 图数据库和 Spring Data Neo4j 的启动器。           | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-neo4j/pom.xml) |
| `spring-boot-starter-data-redis`              | 通过 Spring Data Redis 和 Lettuce 客户端使用 Redis 键－值数据存储的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-redis/pom.xml) |
| `spring-boot-starter-data-redis-reactive`     | 通过 Spring Data Redis reactive 和 Lettuce 客户端使用 Redis 键－值数据存储的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-redis-reactive/pom.xml) |
| `spring-boot-starter-data-rest`               | 使用 Spring Data REST 通过 REST 暴露 Spring Data repositories 的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-rest/pom.xml) |
| `spring-boot-starter-data-solr`               | 通过 Spring Data Solr 使用 Apache Solr 搜索平台的启动器。    | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-data-solr/pom.xml) |
| `spring-boot-starter-freemarker`              | 使用 FreeMarker 视图构建 MVC web 应用的启动器。              | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-freemarker/pom.xml) |
| `spring-boot-starter-groovy-templates`        | 使用 Groovy 模板视图构建 MVC web 应用的启动器。              | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-groovy-templates/pom.xml) |
| `spring-boot-starter-hateoas`                 | 使用 Spring MVC 和 Spring HATEOAS 构建基于超媒体的 RESTful Web 应用程序的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-hateoas/pom.xml) |
| `spring-boot-starter-integration`             | 使用 Spring Integration 的启动器。                           | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-integration/pom.xml) |
| `spring-boot-starter-jdbc`                    | 通过 HikariCP 连接池使用 JDBC 的启动器。                     | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jdbc/pom.xml) |
| `spring-boot-starter-jersey`                  | 使用 JAX-RS 和 Jersey 构建 RESTful web 应用的启动器。是 [`spring-boot-starter-web`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#spring-boot-starter-web) 的替代品。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jersey/pom.xml) |
| `spring-boot-starter-jooq`                    | 使用 JOOQ 访问 SQL 数据库的启动器。是 [`spring-boot-starter-data-jpa`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#spring-boot-starter-data-jpa) 或者 [`spring-boot-starter-jdbc`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#spring-boot-starter-jdbc) 的替代品。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jooq/pom.xml) |
| `spring-boot-starter-json`                    | 读写 json 的启动器。                                         | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-json/pom.xml) |
| `spring-boot-starter-jta-atomikos`            | 使用 Atomikos 实现 JTA 事务的启动器。                        | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jta-atomikos/pom.xml) |
| `spring-boot-starter-jta-bitronix`            | 使用 Bitronix 实现 JTA 事务的启动器。                        | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jta-bitronix/pom.xml) |
| `spring-boot-starter-mail`                    | 使用 Java Mail 和 Spring 框架的邮件发送支持的启动器。        | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-mail/pom.xml) |
| `spring-boot-starter-mustache`                | 使用 Mustache 视图构建 web 应用的启动器。                    | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-mustache/pom.xml) |
| `spring-boot-starter-oauth2-client`           | 使用 Spring Security 的 OAuth2/OpenID 连接客户端特性的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-oauth2-client/pom.xml) |
| `spring-boot-starter-oauth2-resource-server`  | 使用 Spring Security 的 OAuth2 资源服务器特性的启动器。      | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-oauth2-resource-server/pom.xml) |
| `spring-boot-starter-quartz`                  | 使用 Quartz 调度器的启动器。                                 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-quartz/pom.xml) |
| `spring-boot-starter-rsocket`                 | 构建 RSocket 客户端和服务器的启动器。                        | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-rsocket/pom.xml) |
| `spring-boot-starter-security`                | 使用 Spring Security 的启动器。                              | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-security/pom.xml) |
| `spring-boot-starter-test`                    | 用于使用包括 JUnit，Hamcrest 和 Mockito 在内的库测试 Spring Boot 应用的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-test/pom.xml) |
| `spring-boot-starter-thymeleaf`               | 使用 Thymeleaf 视图构建 MVC web 应用的启动器。               | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-thymeleaf/pom.xml) |
| `spring-boot-starter-validation`              | 使用 Hibernate Validator 进行 Java Bean Validation 的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-validation/pom.xml) |
| `spring-boot-starter-web`                     | 使用 Spring MVC 构建 web（包括 RESTful）应用程序的启动器。使用 Tomcat 作为默认的嵌入式容器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-web/pom.xml) |
| `spring-boot-starter-web-services`            | 使用 Spring Web Services 的启动器。                          | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-web-services/pom.xml) |
| `spring-boot-starter-webflux`                 | 使用 Spring Framework 的 Reactive Web 支持构建 WebFlux 应用程序的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-webflux/pom.xml) |
| `spring-boot-starter-websocket`               | 使用 Spring Framework 的 WebSocket 支持构建 WebSocket 应用程序的启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-websocket/pom.xml) |

除了上面的应用启动器，下面的启动器可以被用于添加*生产就绪*特性：

| Name                           | Description                                                  | Pom                                                          |
| :----------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `spring-boot-starter-actuator` | 使用 Spring Boot 的 Actuator 的启动器，Actuator 提供了生产就绪功能，可帮助您监视和管理应用程序。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-actuator/pom.xml) |

最后，Spring Boot 还包括以下启动程序，如果您想排除或替换特定的技术，可以使用这些启动程序：

| Name                                | Description                                                  | Pom                                                          |
| :---------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| `spring-boot-starter-jetty`         | 使用 Jetty 作为内置 servlet 容器的启动器。是 [`spring-boot-starter-tomcat`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#spring-boot-starter-tomcat) 的替代品。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-jetty/pom.xml) |
| `spring-boot-starter-log4j2`        | 使用 Log4j2 记录日志的启动器。是 [`spring-boot-starter-logging`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#spring-boot-starter-logging) 的替代品。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-log4j2/pom.xml) |
| `spring-boot-starter-logging`       | 使用 Logback 记录日志的启动器。是默认的日志启动器。          | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-logging/pom.xml) |
| `spring-boot-starter-reactor-netty` | 使用 Reactor Netty 作为内置 reactive HTTP 服务器的启动器。   | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-reactor-netty/pom.xml) |
| `spring-boot-starter-tomcat`        | 使用 Tomcat 作为内置 servlet 容器的启动器。是 [`spring-boot-starter-web`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#spring-boot-starter-web) 使用的默认 servlet 容器启动器。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-tomcat/pom.xml) |
| `spring-boot-starter-undertow`      | 使用 Undertow 作为内置 servlet 容器的启动器。是 [`spring-boot-starter-tomcat`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#spring-boot-starter-tomcat) 的替代品。 | [Pom](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-starters/spring-boot-starter-undertow/pom.xml) |

> 了解额外的社区贡献的启动器列表，参考 GitHub 上 `spring-boot-starters` 模块中的 [README](https://github.com/spring-projects/spring-boot/tree/master/spring-boot-project/spring-boot-starters/README.adoc) 文件。

### 3.2. 构建你的代码

Spring Boot 并不强制任何固定形式的代码组织形式。不过，倒是存在一些很有帮助的最佳实践。

#### 3.2.1. 使用 “default” 包

如果一个类不包含 `package` 声明，它就会被认为处于所谓的默认包中。通常情况下应该尽量避免使用默认包。因为它可能导致使用 `@ComponentScan` ，`@ConfigurationPropertiesScan` ，`@EntityScen` ，`@SpringBootApplication` 等注解的 Spring Boot 应用中发生某些问题，因为每个 jar 中的每个类都会被读取。

> 我们推荐你遵循 Java 推荐的包命名传统，使用逆序的域名作为包名（比如，`com.example.project`）

#### 3.2.2. 定位应用主类

我们通常建议您将应用程序主类放在其他类之上的根包中。通常将 [`@SpringBootApplication` 注解](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-using-springbootapplication-annotation) 放在您的主类上，它隐式定义某些项目的基本“搜索包”。例如，如果您正在编写 JPA 应用程序，则使用 `@SpringBootApplication` 注解修饰的类的包来搜索 `@Entity` 项目。使用根软件包还允许组件扫描仅应用于您的项目。

> 如果您不想使用  `@SpringBootApplication` ，由于它是通过引入 `@EnableAutoConfiguration` 和 `@ComponentScan` 注解来定义该行为，因此也可以直接使用它们来替代。

下面的列表展示了一种典型的项目结构：

```
com
 +- example
     +- myapplication
         +- Application.java
         |
         +- customer
         |   +- Customer.java
         |   +- CustomerController.java
         |   +- CustomerService.java
         |   +- CustomerRepository.java
         |
         +- order
             +- Order.java
             +- OrderController.java
             +- OrderService.java
             +- OrderRepository.java
```

`Application.java` 文件中可以随着基本的 `@SpringBootApplication` 声明 `main` 方法，如下面例子所示：

```java
package com.example.myapplication;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

### 3.3. 配置类

Spring 更喜欢基于 Java 的配置。尽管通过 XML 源文件使用 `SpringApplication` 也是可能的，我们还是推荐你将主要的配置源写成一个单独的 `@Configuration` 类。通常，定义 `main` 方法的类就是这个主 `@Configuration` 的理想选择。

> 许多已经发布到网上的 Spring 配置示例都使用了 XML 配置。如果可能，请始终使用等效的基于 Java 的配置。搜索 `Enable*` 注解将是一个很好的切入点。

#### 3.3.1. 引入额外的配置类

你不需要将所有的 `@Configuration` 都放在同一个类里。`@Import` 注解可以被用来引入另外的配置类。此外，你可以使用 `@ComponentScen` 自动获取所有的 Spring 组件，包括 `@Configuration` 类。

#### 3.3.2. 引入 XML 配置

如果你必须使用基于 XML 的配置，我们推荐你仍然从 `@Configuration` 类开始。你可以在其中使用 `@ImportResource` 注解加载 XML 配置文件。

### 3.4. 自动配置

Spring Boot 自动配置试图基于你已经添加的 jar 依赖自动配置你的 Spring 应用。比如，如果 `HSQLDB` 在你的类路径上，而你并没有手动配置任何数据库连接 beans ，则 Spring Boot 就会自动配置一个内存数据库。

你需要通过将 `@EnableAutoConfiguration` 或者 `@SpringBootApplication` 注解添加到其中一个你的 `@Configuration` 类中来选择加入自动配置。

> 您应该只添加一个 `@SpringBootApplication` 或 `@EnableAutoConfiguration` 注解。我们通常建议您仅将其中一个添加到您的主要 `@Configuration` 类中。

#### 3.4.1. 逐步替换自动配置

自动配置是非侵入性的。在任何时候，您都可以开始定义自己的配置，以替换自动配置的特定部分。例如，如果您添加自己的 `DataSource` bean，则默认的内置数据库支持将退出。

如果您需要找出当前正在应用的自动配置以及原因，请使用 `--debug` 开关参数启动您的应用程序。这样做可以启用调试日志以供选择核心记录器，并将条件报告记录到控制台。

#### 3.4.2. 禁用特定的自动配置类

如果你发现不想某个特定的自动配置类被应用，你可以使用 `@EnableAutoConfiguration` 注解的 `exclude` 属性来禁用它。如下面例子所示：

```java
import org.springframework.boot.autoconfigure.*;
import org.springframework.boot.autoconfigure.jdbc.*;
import org.springframework.context.annotation.*;

@Configuration(proxyBeanMethods = false)
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
public class MyConfiguration {
}
```

如果类不在类路径下，你可以使用注解的 `excludeName` 属性并指定全限定名。你也可以通过使用 `spring.autoconfigure.exclude` 属性控制需要禁用的自动配置类列表。

> 您可以在注解级别和使用属性来定义排除项。

> 即使自动配置类是 `public` 的，该类的唯一被认为是公共 API 的方面是可用于禁用自动配置的类的名称。这些类的实际内容（例如嵌套配置类或 bean 方法）仅供内部使用，我们不建议直接使用它们。

### 3.5. Spring Beans 和依赖注入

您可以自由使用任何标准的 Spring Framework 技术来定义 bean 及其注入的依赖关系。为简单起见，我们经常发现使用 `@ComponentScan`（查找您的 bean）和使用 `@Autowired`（进行构造函数注入）效果很好。

如果按照上面的建议构造代码（将应用程序类放在根包中），则可以添加不带任何参数的 `@ComponentScan`。您的所有应用程序组件（`@Component`，`@Service`，`@Repository`，`@Controller` 等）都将自动注册为 Spring Bean。

下面的例子展示了一个 `@Service` bean ，它使用了构造器注入来获取所需的 `RiskAssessor` bean：

```java
package com.example.service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

@Service
public class DatabaseAccountService implements AccountService {

    private final RiskAssessor riskAssessor;

    @Autowired
    public DatabaseAccountService(RiskAssessor riskAssessor) {
        this.riskAssessor = riskAssessor;
    }

    // ...

}
```

如果 bean 拥有构造器，你就可以忽略 `@Autowired` ，如下面例子所示：

```java
@Service
public class DatabaseAccountService implements AccountService {

    private final RiskAssessor riskAssessor;

    public DatabaseAccountService(RiskAssessor riskAssessor) {
        this.riskAssessor = riskAssessor;
    }

    // ...

}
```

> 请注意，使用构造函数注入如何将 `riskAssessor` 字段标记为 `final`，指示其随后无法更改。

### 3.6. 使用 @SpringBootApplication 注解

许多 Spring Boot 开发者喜欢他们的应用使用自动配置，组件扫描，并能够在他们的"应用类”中定义额外的配置。单独一个 `@SpringBootApplication` 就可以同时开启这三个特性。也就是：

- `@EnableAutoConfiguration`: 开启 [Spring Boot’s auto-configuration mechanism](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-auto-configuration) 。
- `@ComponentScan`: 在应用所在的包上开启 `@Component` 扫描 (参考 [the best practices](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-structuring-your-code))。
- `@Configuration`: 允许在上下文中注册额外 bean 或者引入额外的配置类。

```java
package com.example.myapplication;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication // same as @Configuration @EnableAutoConfiguration @ComponentScan
public class Application {

    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }

}
```

> `@SpringBootApplication` 还提供了别名来自定义 `@EnableAutoConfiguration` 和 `@ComponentScan` 属性。

> 这些功能都不是强制性的，您可以选择替换任何单个注解来开关用它启用的任何功能。例如，您可能不想在应用程序中使用组件扫描或配置属性扫描：
>
> ```java
> package com.example.myapplication;
> 
> import org.springframework.boot.SpringApplication;
> import org.springframework.context.annotation.ComponentScan
> import org.springframework.context.annotation.Configuration;
> import org.springframework.context.annotation.Import;
> 
> @Configuration(proxyBeanMethods = false)
> @EnableAutoConfiguration
> @Import({ MyConfig.class, MyAnotherConfig.class })
> public class Application {
> 
>     public static void main(String[] args) {
>             SpringApplication.run(Application.class, args);
>     }
> 
> }
> ```
>
> 在此示例中，除了没有自动检测到带有 `@Component` 注解的类和带有 `@ConfigurationProperties` 注解的类并且显式导入了用户定义的 Bean 之外，`Application` 就像其他任何 Spring Boot 应用程序一样（参考 `@Import`）。

### 3.7. 运行你的应用

将应用程序打包为 jar 并使用嵌入式 HTTP 服务器的最大优势之一是，您可以像运行其他应用程序一样运行 web 应用程序。调试 Spring Boot 应用程序也很容易。您不需要任何特殊的 IDE 插件或扩展。

> 本节仅介绍基于 jar 的打包。如果选择将应用程序打包为 war 文件，则应参考服务器和 IDE 文档。

#### 3.7.1. 从 IDE 运行

您可以将 IDE 中的 Spring Boot 应用程序作为简单的 Java 应用程序运行。但是，您首先需要导入您的项目。导入步骤因您的 IDE 和构建系统而异。大多数 IDE 可以直接导入 Maven 项目。例如，Eclipse 用户可以从“文件”菜单中选择“导入...”→“现有Maven项目”。

如果你无法直接将项目导入 IDE ，你可能需要通过构建插件生成相应的 IDE 所需的项目元数据。Maven 包含用于 [Eclipse](https://maven.apache.org/plugins/maven-eclipse-plugin/) 和 [IDEA](https://maven.apache.org/plugins/maven-idea-plugin/) 的插件。Gradle 提供了 [各种 IDE 的插件](https://docs.gradle.org/current/userguide/userguide.html) 。

> 如果不小心两次运行 Web 应用程序，则会看到“端口已在使用中”错误。STS 用户可以使用“重新启动”按钮而不是“运行”按钮来确保关闭任何现有实例。

#### 3.7.2. 作为打包的应用运行

如果使用 Spring Boot Maven 或 Gradle 插件创建可执行 jar，则可以使用 `java -jar` 运行应用程序，如以下示例所示：

```
$ java -jar target/myapplication-0.0.1-SNAPSHOT.jar
```

也可以在启用了远程调试支持的情况下运行打包的应用程序。这样做使您可以将调试器附加到打包的应用程序，如以下示例所示：

```
$ java -Xdebug -Xrunjdwp:server=y,transport=dt_socket,address=8000,suspend=n \
       -jar target/myapplication-0.0.1-SNAPSHOT.jar
```

#### 3.7.3. 使用 Maven 插件

Spring Boot Maven 插件包含一个 `run` 目标，可用于快速编译和运行您的应用程序。应用程序以解压缩形式运行，就像在 IDE 中一样。以下示例显示了运行 Spring Boot 应用程序的典型 Maven 命令：

```
$ mvn spring-boot:run
```

您可能还想使用 `MAVEN_OPTS` 操作系统环境变量，如以下示例所示：

```
$ export MAVEN_OPTS=-Xmx1024m
```

#### 3.7.4. 使用 Gradle 插件

Spring Boot Gradle 插件还包含一个 `bootRun` 任务，可用于以解压缩形式运行您的应用程序。每当您应用 `org.springframework.boot` 和 Java 插件时，都会添加 `bootRun` 任务，并在以下示例中显示：

```
$ gradle bootRun
```

您可能还想使用 `JAVA_OPTS` 操作系统环境变量，如以下示例所示：

```
$ export JAVA_OPTS=-Xmx1024m
```

#### 3.7.5. 热替换

由于 Spring Boot 应用程序只是普通的 Java 应用程序，因此 JVM 热替换应该可以直接使用。JVM 热替换在一定程度上受到它可以替换的字节码的限制。对于更完整的解决方案，可以使用 [JRebel](https://jrebel.com/software/jrebel/) 。

 `spring-boot-devtools` 模块也包含应用快速重启支持。参考稍后的 [Developer Tools](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools) 章节以及 [Hot swapping “How-to”](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-hotswapping) 部分获取更多细节。

### 3.8. 开发工具

Spring Boot 包含一组额外的工具，这些工具可以使应用程序开发体验更加愉快。 `spring-boot-devtools` 模块可以包含在任何项目中，以提供附加的开发时功能。要包括 `devtools` 支持，请将模块依赖项添加到您的构建配置中，如以下 Maven 和 Gradle 清单所示：

Maven

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-devtools</artifactId>
        <optional>true</optional>
    </dependency>
</dependencies>
```

Gradle

```groovy
configurations {
    developmentOnly
    runtimeClasspath {
        extendsFrom developmentOnly
    }
}
dependencies {
    developmentOnly("org.springframework.boot:spring-boot-devtools")
}
```

> 运行完全打包的应用程序时，将自动禁用开发人员工具。如果您的应用程序是从 `java -jar` 启动的，或者是从特殊的类加载器启动的，则将其视为“生产应用程序”。如果这不适用于您（例如，您是从容器中运行应用程序），请考虑排除 `devtools` 或设置 `-Dspring.devtools.restart.enabled = false` 系统属性。

> 在 Maven 中将依赖项标记为可选，或在 Gradle 中使用自定义 `developmentOnly` 配置（如上所示）是一种最佳实践，它可以防止将 `devtools` 传递地应用到使用您项目的其他模块。

> 重新打包的存档默认情况下不包含 `devtools`。如果您要使用 [某些远程 `devtools` 功能](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-remote)， 需要禁用 `excludeDevtools` 构建属性以包括它。Maven 和 Gradle 插件均支持该属性。

#### 3.8.1. 默认属性

Spring Boot 支持的某些类库使用缓存改善性能。比如，[template engines](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-template-engines) 缓存编译好的模板来避免重复解析模板文件。同样的，Spring MVC 能够添加 HTTP 首部缓存用于响应静态资源。

尽管缓存在生产环境中非常有益，但在开发过程中可能适得其反，因为它可能使您无法看到刚刚在应用程序中所做的更改。因此，默认情况下，`spring-boot-devtools` 禁用缓存选项。

缓存选项通常由 `application.properties` 文件中的设置配置。例如，Thymeleaf 提供了 `spring.thymeleaf.cache` 属性。不需要手动设置这些属性，`spring-boot-devtools` 模块会自动应用合理的开发时配置。

因为在开发 Spring MVC 和 Spring WebFlux 应用程序时需要有关 Web 请求的更多信息，所以开发人员工具将为 `web` 日志记录组启用 `DEBUG` 日志记录。这将为您提供有关传入请求，正在处理的处理程序，响应结果等的信息。如果您希望记录所有请求的详细信息（包括潜在的敏感信息），则可以打开 `spring.http.log-request -details` 的配置属性。

> 如果您不希望应用默认属性，则可以在 `application.properties` 中将 `spring.devtools.add-properties` 设置为 `false`。

> 开发者工具应用的所有属性的完整列表，详见 [DevToolsPropertyDefaultsPostProcessor](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-devtools/src/main/java/org/springframework/boot/devtools/env/DevToolsPropertyDefaultsPostProcessor.java) 。

#### 3.8.2. 自动重启

每当类路径上的文件改变时，使用 `spring-boot-devtools` 的应用程序会自动重启。在 IDE 中工作时，这可能是一个有用的功能，因为它为代码更改提供了非常快速的反馈循环。默认情况下，将监视类路径上指向文件夹的任何条目的更改。请注意，某些资源，例如静态资产和视图模板，[不需要重启应用](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-restart-exclude)。

> 触发重启
>
> 当 DevTools 监视类路径资源时，触发重启的唯一方法是更新类路径。导致类路径更新的方式取决于所使用的 IDE。在 Eclipse 中，保存修改后的文件将导致类路径被更新并触发重新启动。在 IntelliJ IDEA 中，构建项目（`Build +→+ Build Project`）具有相同的效果。

> 只要启用了分叉，您还可以使用受支持的构建插件（Maven 和 Gradle）启动应用程序，因为 DevTools 需要隔离的应用程序类加载器才能正常运行。默认情况下，Gradle 和 Maven 插件会分叉应用程序进程。

> 使用 LiveReload 时，自动重新启动效果很好。详情请参阅 [LiveReload](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-livereload) 部分。如果使用 JRebel，则禁用自动重新启动，而支持动态类重新加载。其他 devtools 功能（例如 LiveReload 和属性覆盖）仍可以使用。

> DevTools 依赖于应用程序上下文的关闭挂钩在重新启动期间将其关闭。如果禁用了关机挂钩，它将无法正常工作 (`SpringApplication.setRegisterShutdownHook(false)`)。

> 在确定类路径上的条目是否应在更改后触发重新启动时，DevTools 会自动忽略名为 `spring-boot`，`spring-boot-devtools`，`spring-boot-autoconfigure`，`spring-boot-actuator` 以及 `spring-boot-starter`。

> DevTools 需要自定义 `ApplicationContext` 使用的 `ResourceLoader`。如果您的应用程序已经提供了，它将被包装。不支持在 `ApplicationContext` 上直接覆盖 `getResource` 方法。

> 重新启动与重新加载
>
> Spring Boot 提供的重启技术通过使用两个类加载器来工作。不变的类（例如，来自第三方 jar 的类）将被加载到*base*类加载器中。您正在开发的类将加载到*restart*类加载器中。重新启动应用程序后，将丢弃*restart*类加载器，并创建一个新的类加载器。这种方法意味着应用程序的重启通常比“冷启动”要快得多，因为*bas*类加载器已经可用并已填充。
>
> 如果发现重新启动不适合您的应用程序，或者遇到类加载问题，则可以考虑从 ZeroTurnaround 重新加载诸如 [JRebel](https://jrebel.com/software/jrebel/) 之类的技术。这些方法通过在加载类时重写类来使其更易于重新加载。

##### 根据条件解析纪录变更

默认情况下，每次应用程序重新启动时，都会记录一个报告，其中显示了条件评估增量。该报告显示了您进行更改（例如添加或删除Bean以及设置配置属性）时对应用程序自动配置的更改。

要禁用报告的日志记录，请设置以下属性：

```
spring.devtools.restart.log-condition-evaluation-delta=false
```

##### 排除资源

某些资源在更改时不一定需要触发重新启动。例如，Thymeleaf 模板可以就地编辑。默认情况下，更改 `/META-INF/maven`，`/META-INF/resources`，`/resources`，`/static`，`/public` 或 `/templates` 中的资源不会触发重新启动，但是确实会触发 [实时重新加载](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-livereload)。如果要自定义这些排除项，可以使用 `spring.devtools.restart.exclude` 属性。例如，要仅排除 `/static` 和 `/public`，可以设置以下属性：

```
spring.devtools.restart.exclude=static/**,public/**
```

> 如果你想保持默认选项并添加额外的排除配置，使用 `spring.devtools.restart.additional-exclude` 属性。

##### 监控额外路径

当您对不在类路径上的文件进行更改时，您可能希望重新启动或重新加载应用程序。为此，请使用 `spring.devtools.restart.additional-paths` 属性配置其他路径以监视更改。您可以使用 [spring.devtools.restart.exclude](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-restart-exclude) 属性来控制其他路径下的更改是触发完全重启还是 [实时重新加载](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-livereload)。

##### 关闭重启

如果不想使用重启功能，可以通过使用 `spring.devtools.restart.enabled` 属性来禁用它。在大多数情况下，您可以在 `application.properties` 中设置此属性（这样做仍会初始化重启类加载器，但它不会监视文件更改）。

如果您需要*完全*禁用重启支持（例如，因为它不适用于特定的库），则需要在调用 `SpringApplication.run(…)` 之前将 `Spring.devtools.restart.enabled` `System` 属性设置为 `false`。如以下示例所示：

```java
public static void main(String[] args) {
    System.setProperty("spring.devtools.restart.enabled", "false");
    SpringApplication.run(MyApp.class, args);
}
```

##### 使用触发器文件

如果使用持续编译更改文件的 IDE，则可能更喜欢仅在特定时间触发重新启动。为此，您可以使用“触发文件”，这是一个特殊文件，当您要实际触发重新启动检查时必须对其进行修改。

> 对文件的任何更新都将触发检查，但是只有在 Devtools 检测到有事情要做的情况下，重启才真正发生。

要使用触发文件，请将 `spring.devtools.restart.trigger-file` 属性设置为触发文件的名称（不包括任何路径）。触发文件必须出现在类路径上的某个位置。

例如，如果您的项目具有以下结构：

```
src
+- main
   +- resources
      +- .reloadtrigger
```

 则你的 `trigger-file` 属性应该是：

```properties
spring.devtools.restart.trigger-file=.reloadtrigger
```

此时重启只会发生在 `src/main/resources/.reloadtrigger` 文件更新之后。

> 你可能会想将 `spring.devtools.restart.trigger-file` 设置为一个 [global setting](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-globalsettings)，从而你的所有项目行为都会保持一致。

某些 IDE 具有使您不必手动更新触发器文件的功能。 [用于Eclipse的Spring工具](https://spring.io/tools) 和 [IntelliJ IDEA（旗舰版）](https://www.jetbrains.com/idea/) 都具有这种支持。 使用 Spring Tools，您可以从控制台视图使用“重新加载”按钮（只要您的“触发文件”被命名为 `.reloadtrigger`）。对于 IntelliJ，您可以按照 [文档说明](https://www.jetbrains.com/help/idea/spring-boot.html#configure-application-update-policies-with-devtools)。

##### 自定义重启类加载器

如之前 [重新启动与重新加载](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-spring-boot-restart-vs-reload) 部分中所述，重新启动功能是通过使用两个类加载器实现的。对于大多数应用程序，此方法效果很好。但是，有时可能会导致类加载问题。

默认情况下，IDE 中任何打开的项目都使用“重新启动”类加载器加载，而任何常规的 `.jar` 文件都使用“基本”类加载器加载。如果您在多模块项目上工作，并且并非每个模块都导入到 IDE 中，则可能需要自定义内容。为此，您可以创建一个 `META-INF/spring-devtools.properties` 文件。

`spring-devtools.properties` 文件可以包含以 `restart.exclude` 和 `restart.include` 为前缀的属性。 `include` 元素是应提升到“重新启动”类加载器中的项目，而 `exclude` 元素是应下推到“基本”类加载器中的项目。该属性的值是应用于类路径的正则表达式模式，如以下示例所示：

```properties
restart.exclude.companycommonlibs=/mycorp-common-[\\w\\d-\.]+\.jar
restart.include.projectcommon=/mycorp-myproj-[\\w\\d-\.]+\.jar
```

> 所有属性键都必须是唯一的。只要属性以 `restart.include` 或 `restart.exclude` 开头即可。

> 所有来自类路径的 `META-INF/spring-devtools.properties` 都被加载。您可以将文件打包到项目内部，也可以打包到项目使用的库中。

##### 周知的局限性

重新启动功能不适用于使用标准的 `ObjectInputStream` 反序列化的对象。如果您需要反序列化数据，则可能需要结合使用 Spring 的 `ConfigurableObjectInputStream` 和 `Thread.currentThread().getContextClassLoader()`。

不幸的是，一些第三方库在不考虑上下文类加载器的情况下反序列化。 如果发现这样的问题，则需要向原始作者请求修复。

#### 3.8.3. LiveReload

`spring-boot-devtools` 模块包含一个内置的 LiveReload 服务器，可以在资源发生变化时用来触发浏览器刷新。来自 [livereload.com](http://livereload.com/extensions/) 的 LiveReload 浏览器插件对 Chrome、Firefox 和 Safari 浏览器开放使用。

如果你不想在应用运行时启动 LiveReload 服务器，你可以将 `spring.devtools.livereload.enabled` 属性设置为 `false`。

> 你可以每次运行一个 LiveReload 服务器。在启动你的应用之前，确保没有其它的 LiveReload 服务器在运行。如果你从 IDE 启动多个应用实例，只有第一个拥有 LiveReload 支持。

#### 3.8.4. 全局设定

你可以通过将以下任意文件添加到 `$HOME/.config/spring-boot` 文件夹下来进行开发者工作的全局配置：

1. `spring-boot-devtools.properties`
2. `spring-boot-devtools.yaml`
3. `spring-boot-devtools.yml`

所有添加到这些文件中的属性都会被应用于你的机器上所有使用开发者工具的 Spring Boot 应用。比如，为了配置重启始终使用 [trigger file](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-restart-triggerfile)，你可以添加如下属性：

**~/.config/spring-boot/spring-boot-devtools.properties**

```properties
spring.devtools.restart.trigger-file=.reloadtrigger
```

> 如果开发者工具配置文件没有在 `$HOME/.config/spring-boot` 路径下找到，则会在 `$HOME` 根目录下搜索存在的 `.spring-boot-devtools.properties` 文件。这就允许你在不支持 `$HOME/.config/spring-boot` 配置文件路径的老版本 Spring Boot 应用之间共享开发者工具全局配置。

> 在上述文件中激活的配置文件不会影响 [特定于配置文件的配置文件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-profile-specific-properties) 的加载。

#### 3.8.5. 远程应用

Spring Boot 开发人员工具不仅限于本地开发。远程运行应用程序时，您还可以使用多种功能。启用远程支持是可选的，因为启用它可能会带来安全风险。仅当在受信任的网络上运行或使用 SSL 保护时，才应启用它。如果这两个选项都不可用，则不应使用 DevTools 的远程支持。永远不要在生产部署上启用支持。

要启用它，您需要确保重新打包的档案中包含 `devtools`，如以下清单所示：

```xml
<build>
    <plugins>
        <plugin>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-maven-plugin</artifactId>
            <configuration>
                <excludeDevtools>false</excludeDevtools>
            </configuration>
        </plugin>
    </plugins>
</build>
```

然后您需要设置 `spring.devtools.remote.secret` 属性。像任何重要的密码或机密一样，该值应唯一且强壮，以免被猜测或强行使用。

远程 devtools 支持分为两部分：接受连接的服务器端端点和在 IDE 中运行的客户端应用程序。设置 `spring.devtools.remote.secret` 属性后，服务器组件自动启用。客户端组件必须手动启动。

##### 运行远程客户端应用

远程客户端应用程序旨在在您的 IDE 中运行。您需要使用与您连接到的远程项目相同的类路径来运行 `org.springframework.boot.devtools.RemoteSpringApplication`。该应用程序的唯一必需参数是它连接到的远程 URL。

例如，如果您使用的是 Eclipse 或 STS，并且有一个名为 `my-app` 的项目已部署到 Cloud Foundry，则可以执行以下操作：

- 从“运行”菜单中选择“运行配置...”。

- 创建一个新的 Java 应用程序“启动配置”。

- 选择 `my-app` 项目。

- 使用 `org.springframework.boot.devtools.RemoteSpringApplication` 作为主类。

- 将 `https://myapp.cfapps.io` （或任何远程URL）添加到“程序参数”。

正在运行的远程客户端可能类似于以下清单：

```
  .   ____          _                                              __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _          ___               _      \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` |        | _ \___ _ __  ___| |_ ___ \ \ \ \
 \\/  ___)| |_)| | | | | || (_| []::::::[]   / -_) '  \/ _ \  _/ -_) ) ) ) )
  '  |____| .__|_| |_|_| |_\__, |        |_|_\___|_|_|_\___/\__\___|/ / / /
 =========|_|==============|___/===================================/_/_/_/
 :: Spring Boot Remote :: 2.2.2.RELEASE

2015-06-10 18:25:06.632  INFO 14938 --- [           main] o.s.b.devtools.RemoteSpringApplication   : Starting RemoteSpringApplication on pwmbp with PID 14938 (/Users/pwebb/projects/spring-boot/code/spring-boot-project/spring-boot-devtools/target/classes started by pwebb in /Users/pwebb/projects/spring-boot/code)
2015-06-10 18:25:06.671  INFO 14938 --- [           main] s.c.a.AnnotationConfigApplicationContext : Refreshing org.springframework.context.annotation.AnnotationConfigApplicationContext@2a17b7b6: startup date [Wed Jun 10 18:25:06 PDT 2015]; root of context hierarchy
2015-06-10 18:25:07.043  WARN 14938 --- [           main] o.s.b.d.r.c.RemoteClientConfiguration    : The connection to http://localhost:8080 is insecure. You should use a URL starting with 'https://'.
2015-06-10 18:25:07.074  INFO 14938 --- [           main] o.s.b.d.a.OptionalLiveReloadServer       : LiveReload server is running on port 35729
2015-06-10 18:25:07.130  INFO 14938 --- [           main] o.s.b.devtools.RemoteSpringApplication   : Started RemoteSpringApplication in 0.74 seconds (JVM running for 1.105)
```

> 因为远程客户端使用与真实应用程序相同的类路径，所以它可以直接读取应用程序属性。这就是读取 `spring.devtools.remote.secret` 属性并将其传递给服务器进行身份验证的方式。

> 建议始终使用 `https://` 作为连接协议，以便对流量进行加密并且确保密码不能被截获。

> 如果您需要使用代理访问远程应用程序，请配置 `spring.devtools.remote.proxy.host` 和 `spring.devtools.remote.proxy.port` 属性。

##### 远程更新

远程客户端以与 [本地重新启动](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-restart)  相同的方式监视应用程序类路径的更改。任何更新的资源都会推送到远程应用程序，并且（*如果需要*）会触发重新启动。如果您迭代使用本地没有的云服务的功能，这将很有帮助。通常，远程更新和重新启动比完整的重建和部署周期快得多。

> 仅在远程客户端正在运行时监视文件。如果在启动远程客户端之前更改文件，则不会将其推送到远程服务器。

##### 配置文件系统监视器

[FileSystemWatcher](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-devtools/src/main/java/org/springframework/boot/devtools/filewatch/FileSystemWatcher.java) 的工作方式是按一定时间间隔轮询类更改，然后等待预定义的静默期以确保没有更多更改。然后将更改上传到远程应用程序。在更改较慢的开发环境中，可能会发生静默期不够的情况，并且类中的更改可能会分为几批。第一批类更改上传后，服务器将重新启动。由于服务器正在重新启动，因此下一批不能发送到应用程序。

这通常通过 `RemoteSpringApplication` 日志中的警告来证明，该警告关于无法上载某些类以及随后的重试。但是，这也可能导致应用程序代码不一致，并且在上传第一批更改后无法重新启动。

如果您经常观察到此类问题，请尝试将 `spring.devtools.restart.poll-interval` 和 `spring.devtools.restart.quiet-period` 参数增加到适合您的开发环境的值：

```properties
spring.devtools.restart.poll-interval=2s
spring.devtools.restart.quiet-period=1s
```

现在每 2 秒轮询一次受监视的 `classpath` 文件夹以进行更改，并保持 1 秒钟的静默时间以确保没有其他类更改。

### 3.9. 将你的应用打包为生产包

可执行 jar 可以用于生产部署。由于它们是独立的，因此它们也非常适合基于云的部署。

对于其他“生产准备就绪”功能，例如运行状况，审核和度量 REST 或 JMX 端点，请考虑添加 `spring-boot-actuator`。有关详细信息，请参见 *Spring Boot Actuator: Production-ready Features* 。

### 3.10. 后续阅读

现在，您应该了解如何使用 Spring Boot 以及应遵循的一些最佳实践。现在，您可以继续深入了解特定的 *Spring Boot功能*，或者可以跳过并阅读 “[production ready](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready)” 部分。

## 4. Spring Boot 特性

本节将深入介绍 Spring Boot。在这里，您可以了解可能要使用和自定义的关键功能。如果您尚未这样做，则可能需要阅读 "[Getting Started](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started)" 和 "[Using Spring Boot](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot)" 部分，这样您就可以深入了解基础知识。

### 4.1. SpringApplication

`SpringApplication` 类提供了一种便捷的方法来引导你的 Spring 应用从一个 `main()` 方法启动。很多情况下，你可以将该任务委托给静态 `SpringApplication.run` 方法。如下面例子所示：

```java
public static void main(String[] args) {
    SpringApplication.run(MySpringConfiguration.class, args);
}
```

当你的应用启动之后，你应该可以看到类似于下面的输出：

```
  .   ____          _            __ _ _
 /\\ / ___'_ __ _ _(_)_ __  __ _ \ \ \ \
( ( )\___ | '_ | '_| | '_ \/ _` | \ \ \ \
 \\/  ___)| |_)| | | | | || (_| |  ) ) ) )
  '  |____| .__|_| |_|_| |_\__, | / / / /
 =========|_|==============|___/=/_/_/_/
 :: Spring Boot ::   v2.2.2.RELEASE

2019-04-31 13:09:54.117  INFO 56603 --- [           main] o.s.b.s.app.SampleApplication            : Starting SampleApplication v0.1.0 on mycomputer with PID 56603 (/apps/myapp.jar started by pwebb)
2019-04-31 13:09:54.166  INFO 56603 --- [           main] ationConfigServletWebServerApplicationContext : Refreshing org.springframework.boot.web.servlet.context.AnnotationConfigServletWebServerApplicationContext@6e5a8246: startup date [Wed Jul 31 00:08:16 PDT 2013]; root of context hierarchy
2019-04-01 13:09:56.912  INFO 41370 --- [           main] .t.TomcatServletWebServerFactory : Server initialized with port: 8080
2019-04-01 13:09:57.501  INFO 41370 --- [           main] o.s.b.s.app.SampleApplication            : Started SampleApplication in 2.992 seconds (JVM running for 3.658)
```

默认地，`INFO` 日志消息会被记录，包含一些相关的启动细节，比如启动应用的用户等。如果你需要 `INFO` 之外的日志级别，你可以设置它，如 [Log Levels](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-custom-log-levels) 中所述。应用版本通过使用来自应用主类所在包的实现版本确定。启动消息日志可以通过将 `spring.main.log-startup-info` 设定为 `false` 来关闭。这将同时关闭应用的活动配置日志。

> 为了在启动过程中添加额外日志，你可以在 `SpringApplication` 的子类中覆盖 `logStartupInfo(boolean)` 方法。

#### 4.1.1. 启动失败

如果你的应用启动失败，注册的 `FailureAnalyzers` 获得一个机会提供专门的错误消息以及一种具体的行动来解决该问题。比如，如果你在端口 `8080` 上启动 web 应用而该端口已经在使用，你应该能够看到类似于下面的信息：

```
***************************
APPLICATION FAILED TO START
***************************

Description:

Embedded servlet container failed to start. Port 8080 was already in use.

Action:

Identify and stop the process that's listening on port 8080 or configure this application to listen on another port.
```

> Spring Boot 提供了许多 `FailureAnalyzer` 实现，而且你还可以 [添加你自己的](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-failure-analyzer) 。

如果没有失败分析器能够处理启动异常，你仍然可以显示完整的条件报告用来更好的获知错误信息。为了做到这一点，你需要为 `org.springframework.boot.autoconfigure.logging.ConditionEvaluationReportLoggingListener`  [开启 `debug` 属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config) 或者 [开启 `DEBUG` 日志](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-custom-log-levels) 。

比如，如果你通过 `java -jar` 运行你的应用，你可以如下开启 `debug` 属性：

```
$ java -jar myproject-0.0.1-SNAPSHOT.jar --debug
```

#### 4.1.2. 懒初始化

`SpringApplication` 允许延迟地初始化应用程序。启用延迟初始化后，将根据需要创建 bean，而不是在应用程序启动期间创建 bean。因此，启用延迟初始化可以减少应用程序启动所需的时间。在 Web 应用程序中，启用延迟初始化将导致许多与 Web 相关的 Bean 直到收到 HTTP 请求后才被初始化。

延迟初始化的缺点是，它可能会延迟发现应用程序问题的时间。如果错误配置的 Bean 延迟初始化，则启动期间将不再发生故障，并且只有在初始化 Bean 时问题才会显现。还必须注意确保 JVM 有足够的内存来容纳所有应用程序的 bean，而不仅仅是启动期间初始化的 bean。由于这些原因，默认情况下不会启用延迟初始化，因此建议在启用延迟初始化之前先对 JVM 的堆大小进行微调。

可以使用 `SpringApplicationBuilder` 上的 `lazyInitialization` 方法或 `SpringApplication` 上的 `setLazyInitialization` 方法以编程方式启用延迟初始化。另外，也可以使用 `spring.main.lazy-initialization` 属性来启用它，如以下示例所示：

```properties
spring.main.lazy-initialization=true
```

> 如果您想在应用程序的其余部分使用延迟初始化时禁用某些 bean 的延迟初始化，则可以使用 `@Lazy(false)` 注解将它们的延迟属性显式设置为 `false`。

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

#### 4.1.4. 自定义 SpringApplication

如果默认的 `SpringApplication` 不适合你，你可以创建一个本地实例并自定义它。比如，想要关闭横幅，你可以编写：

```java
public static void main(String[] args) {
    SpringApplication app = new SpringApplication(MySpringConfiguration.class);
    app.setBannerMode(Banner.Mode.OFF);
    app.run(args);
}
```

> 传递给 `SpringApplication` 的构造函数参数是 Spring bean 的配置源。在大多数情况下，它们是对 `@Configuration` 类的引用，但它们也可以对 XML 配置或应扫描的包进行引用。

通过使用 `application.properties` 文件配置 `SpringApplication` 是可能的。参考 *Externalized Configuration* 获取更多细节。

配置选项的完整列表，参考 [`SpringApplication` Javadoc](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/SpringApplication.html) 。

#### 4.1.5. 链式 Builder API

如果您需要构建一个 `ApplicationContext` 层次结构（具有父/子关系的多个上下文），或者您更喜欢使用“链式”构建器 API，则可以使用 `SpringApplicationBuilder`。

`SpringApplicationBuilder` 可让您将多个方法调用链接在一起，并包含可创建层次结构的 `parent` 方法和 `child` 方法，如以下示例所示：

```java
new SpringApplicationBuilder()
        .sources(Parent.class)
        .child(Application.class)
        .bannerMode(Banner.Mode.OFF)
        .run(args);
```

> 创建 `ApplicationContext` 层次结构时有一些限制。例如，Web 组件必须包含在子上下文中，并且相同的 `Environment` 用于父上下文和子上下文。有关完整的详细信息，请参见 [`SpringApplicationBuilder` Javadoc](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/builder/SpringApplicationBuilder.html) 。

#### 4.1.6. 应用事件和监听器

除了通常的 Spring 框架事件，比如 [`ContextRefreshedEvent`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/context/event/ContextRefreshedEvent.html)，`SpringApplication` 还发送一些别的应用事件。

> 有些事件实际上是在创建 `ApplicationContext` 之前触发的，因此您不能将这些事件的监听器注册为 `@Bean`。您可以使用 `SpringApplication.addListeners(…)` 方法或 `SpringApplicationBuilder.listeners(…)` 方法注册它们。
>
> 如果您希望这些侦听器自动注册，而不管创建应用程序的方式如何，都可以将 `META-INF/spring.factories` 文件添加到您的项目中，并使用 `org.springframework.context.ApplicationListener` 键引用您的侦听器 。如以下示例所示：
>
> ```
> org.springframework.context.ApplicationListener=com.example.project.MyListener
> ```

当你的应用运行时，应用事件按照下面的顺序发送：

1. `ApplicationStartingEvent` 在运行开始时发送，但在进行任何处理之前（侦听器和初始化器的注册除外）发送。

2. 当已知要在上下文中使用的 `Environment` 但在创建上下文之前，发送 `ApplicationEnvironmentPreparedEvent`。

3. 在准备好 `ApplicationContext` 并调用 `ApplicationContextInitializers` 之后，但在加载任何 bean 定义之前，将发送一个 `ApplicationContextInitializedEvent`。

4. 在刷新开始之前，但在加载了 bean 定义之后，发送一个 `ApplicationPreparedEvent`。

5. 在刷新上下文之后，但在调用任何应用程序和命令行运行程序之前，将发送 `ApplicationStartedEvent`。

6. 在调用了任何应用程序和命令行运行程序之后，将发送 `ApplicationReadyEvent`。它指示该应用程序已准备就绪，可以处理请求。

7. 如果启动时发生异常，则发送一个 `ApplicationFailedEvent`。

上面的列表仅包含与 `SpringApplication` 绑定的 `SpringApplicationEvent`。除此之外，以下事件还会在 `ApplicationPreparedEvent` 之后和 `ApplicationStartedEvent` 之前发布：

1. 当刷新 `ApplicationContext` 时，发送 `ContextRefreshedEvent`。

2. 在准备好 WebServer 之后，发送一个 `WebServerInitializedEvent`。`ServletWebServerInitializedEvent` 和 `ServletWebServerInitializedEvent` 分别是 servlet 和反应式变体。

> 您通常不需要使用应用程序事件，但是很容易知道它们的存在。在内部，Spring Boot 使用事件来处理各种任务。

应用程序事件是通过使用 Spring Framework 的事件发布机制发送的。此机制的一部分确保在子级上下文中发布给侦听器的事件也在任何祖先上下文中也发布给侦听器。结果，如果您的应用程序使用 `SpringApplication` 实例的层次结构，则侦听器可能会收到同一类型的应用程序事件的多个实例。

为了使您的侦听器能够区分其上下文的事件和后代上下文的事件，它应请求注入其应用程序上下文，然后将注入的上下文与事件的上下文进行比较。可以通过实现 `ApplicationContextAware` 来注入上下文，或者如果侦听器是 bean，则可以通过使用 `@Autowired` 注入上下文。

#### 4.1.7. Web 环境

`SpringApplication` 试图根据你的行为创建正确类型的 `ApplicationContext` 。用来确定 `WebApplicationType` 的算法相当简单：

- 如果存在 Spring MVC ，使用 `AnnotationConfigServletWebServerApplicationContext` 。
- 如果不存在 Spring MVC，而是存在 Spring WebFlux，使用 `AnnotationConfigReactiveWebServerApplicationContext` 。
- 否则，使用 `AnnotationConfigApplicationContext` 。

这就意味着如果你在同一个应用中使用 Spring MVC 和新的来自 Spring WebFlux 的 `WebClient` ，Spring MVC 将默认被使用。你可以通过调用 `setWebApplicationType(WebApplicationType)` 很容易地覆盖它。

通过调用 `setApplicationContextClass(…)` 对 `ApplicationContext` 类型进行完全控制也是可能的。

> 在 JUnit 测试中使用 `SpringApplication` 时，通常希望调用 `setWebApplicationType(WebApplicationType.NONE)`。

#### 4.1.8. 访问应用参数

如果您需要访问传递给 `SpringApplication.run(…)` 的应用程序参数，则可以注入 `org.springframework.boot.ApplicationArguments` bean。通过 `ApplicationArguments` 接口，可以访问原始的 `String[]` 参数以及已解析的 `option` 和 `non-option` 参数，如以下示例所示：

```java
import org.springframework.boot.*;
import org.springframework.beans.factory.annotation.*;
import org.springframework.stereotype.*;

@Component
public class MyBean {

    @Autowired
    public MyBean(ApplicationArguments args) {
        boolean debug = args.containsOption("debug");
        List<String> files = args.getNonOptionArgs();
        // if run with "--debug logfile.txt" debug=true, files=["logfile.txt"]
    }

}
```

> Spring Boot 还在 Spring `Environment` 中注册了 `CommandLinePropertySource` 。这也使您可以通过使用 `@Value` 注解来注入单个应用程序参数。

#### 4.1.9. 使用 ApplicationRunner 或者 CommandLineRunner

如果需要在 `SpringApplication` 启动后运行一些特定的代码，则可以实现 `ApplicationRunner` 或 `CommandLineRunner` 接口。两个接口都以相同的方式工作，并提供一个单一的 `run` 方法，该方法在 `SpringApplication.run(…)` 完成之前被调用。

`CommandLineRunner` 接口以简单的字符串数组提供对应用程序参数的访问，而 `ApplicationRunner` 使用前面讨论的 `ApplicationArguments` 接口。以下示例显示了带有 `Run` 方法的 `CommandLineRunner`：

```java
import org.springframework.boot.*;
import org.springframework.stereotype.*;

@Component
public class MyBean implements CommandLineRunner {

    public void run(String... args) {
        // Do something...
    }

}
```

如果定义了几个必须按特定顺序调用的 `CommandLineRunner` 或 `ApplicationRunner` Bean，则可以另外实现 `org.springframework.core.Ordered` 接口或使用 `org.springframework.core.annotation.Order` 注解。

#### 4.1.10. 应用退出

每个 `SpringApplication` 向 JVM 注册一个关闭钩子，以确保 `ApplicationContext` 在退出时正常关闭。所有标准的 Spring 生命周期回调（例如 `DisposableBean` 接口或 `@PreDestroy` 注解）都可以使用。

另外，如果 bean 希望在调用 `SpringApplication.exit()` 时返回特定的退出代码，则可以实现 `org.springframework.boot.ExitCodeGenerator` 接口。然后可以将此退出代码传递给 `System.exit()` 以将其作为状态代码返回，如以下示例所示：

```java
@SpringBootApplication
public class ExitCodeApplication {

    @Bean
    public ExitCodeGenerator exitCodeGenerator() {
        return () -> 42;
    }

    public static void main(String[] args) {
        System.exit(SpringApplication.exit(SpringApplication.run(ExitCodeApplication.class, args)));
    }

}
```

同样，`ExitCodeGenerator` 接口可以通过异常实现。当遇到这样的异常时，Spring Boot 返回由实现的 `getExitCode()` 方法提供的退出代码。

#### 4.1.11. 管理特性

通过指定 `spring.application.admin.enabled` 属性，可以为应用程序启用与管理员相关的功能。这暴露了 MBeanServer平台上的 [`SpringApplicationAdminMXBean`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/admin/SpringApplicationAdminMXBean.java) 。您可以使用此功能来远程管理 Spring Boot 应用程序。此功能对于任何服务包装器实现也可能很有用。

> 如果您想知道应用程序在哪个 HTTP 端口上运行，请使用 `local.server.port` 键获取属性。

### 4.2. 外部化配置

Spring Boot 使您可以外部化配置，以便可以在不同环境中使用相同的应用程序代码。您可以使用属性文件，YAML文件，环境变量和命令行参数来外部化配置。属性值可以通过使用 `@Value` 注解直接注入到您的 bean 中，可以通过 Spring 的 `Environment` 抽象访问，也可以通过 `@ConfigurationProperties` [绑定到结构化对象](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-typesafe-configuration-properties) 。

Spring Boot 使用一个非常特殊的 `PropertySource` 顺序，该顺序被设计为允许合理地覆盖值。按以下顺序考虑属性：

1. 当开发者工具激活时首先考虑 `$HOME/.config/spring-boot` 文件夹中的 [Devtools global settings properties](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools-globalsettings) 。
2. 你的测试类上的 [`@TestPropertySource`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/test/context/TestPropertySource.html) 注解。
3. 你的测试类上的 `properties` 属性。在 [`@SpringBootTest`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/test/context/SpringBootTest.html) 和 [test annotations for testing a particular slice of your application](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-tests) 上可用。
4. 命令行参数。
5. 来自 `SPRING_APPLICATION_JSON` 的属性（嵌入在环境变量或系统属性中的内联JSON）。
6. `ServletConfig` 初始参数。
7. `ServletContext` 初始参数。
8. 来自 `java:comp/env` 的 JNDI 属性。
9. Java System 属性 (`System.getProperties()`)。
10. 操作系统环境变量。
11.  `RandomValuePropertySource` ，仅拥有在 `random.*` 中的属性。
12. 在你的打包的 jar 之外的 [Profile-specific application properties](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-profile-specific-properties)  (`application-{profile}.properties` 以及 YAML 变体)。
13. 打包到你的 jar 内部的 [Profile-specific application properties](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-profile-specific-properties)  (`application-{profile}.properties` 以及 YAML 变体)。
14. 你的打包的 jar 之外的应用属性 (`application.properties` 以及 YAML 变体)。
15. 打包到你的 jar 之内的应用属性 (`application.properties` 以及 YAML 变体)。
16. 你的 `@Configuration` 类上的 [`@PropertySource`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/context/annotation/PropertySource.html) 注解。请注意，在刷新应用程序上下文之前，不会将此类属性源添加到 `Environment` 中。现在配置某些属性（例如在刷新开始之前读取的 `logging.*` 和  `spring.main.*` ）为时已晚。
17. 默认属性 (通过设定 `SpringApplication.setDefaultProperties` 指定)。

为了提供一个具体的示例，假设您开发一个使用 `@name` 属性的 `@Component`，如以下示例所示：

```java
import org.springframework.stereotype.*;
import org.springframework.beans.factory.annotation.*;

@Component
public class MyBean {

    @Value("${name}")
    private String name;

    // ...

}
```

在您的应用程序类路径上（例如，在 jar 中），您可以有一个 `application.properties` 文件，该文件为 `name` 提供了合理的默认属性值。在新环境中运行时，可以在 jar 外部提供一个 `application.properties` 文件来覆盖 `name`。对于一次性测试，您可以使用特定的命令行开关启动（例如，`java -jar app.jar --name="Spring"`）。

> 可以在命令行中使用环境变量来提供 `SPRING_APPLICATION_JSON` 属性。 例如，您可以在 UN * X shell 中使用以下行：
>
> ```
> $ SPRING_APPLICATION_JSON='{"acme":{"name":"test"}}' java -jar myapp.jar
> ```
>
> 在前面的示例中，您最终在 Spring `Environment` 中获得了 `acme.name=test` 。您还可以在 System 属性中以 `spring.application.json` 的形式提供 JSON，如以下示例所示：
>
> ```
> $ java -Dspring.application.json='{"name":"test"}' -jar myapp.jar
> ```
>
> 您还可以使用命令行参数来提供 JSON，如以下示例所示：
>
> ```
> $ java -jar myapp.jar --spring.application.json='{"name":"test"}'
> ```
>
> 您还可以将 JSON 作为 JNDI 变量提供，如下所示：`java:comp/env/spring.application.json`。

#### 4.2.1. 配置随机值

`RandomValuePropertySource` 可用于注入随机值（例如，注入密码或测试用例）。它可以产生整数，longs，uuid 或字符串，如以下示例所示：

```properties
my.secret=${random.value}
my.number=${random.int}
my.bignumber=${random.long}
my.uuid=${random.uuid}
my.number.less.than.ten=${random.int(10)}
my.number.in.range=${random.int[1024,65536]}
```

`random.int*` 语法是 `OPEN value (,max) CLOSE` ，其中 `OPEN,CLOSE` 是任何字符，而 `value,max` 是整数。如果提供了 `max`，则 `value` 为最小值，而 `max` 为最大值（不包括）。

#### 4.2.2. 访问命令行属性

默认情况下，`SpringApplication` 会将任何命令行选项参数（即以 `--` 开头的参数，例如 `--server.port=9000`）转换为 `property` 并将其添加到 Spring `Environment` 中。如前所述，命令行属性始终优先于其他属性源。

如果您不希望将命令行属性添加到 `Environment` 中，则可以使用 `SpringApplication.setAddCommandLineProperties(false)` 禁用它们。

#### 4.2.3. 应用属性文件

`SpringApplication` 从以下位置的 `application.properties` 文件中加载属性，并将它们添加到 Spring `Environment` 中：

1. 当前路径的 `/config` 子路径
2. 当前路径
3. 类路径的 `/config` 包
4. 类路径根目录

该列表按优先级排序（在列表较高位置定义的属性会覆盖在较低位置定义的属性）。

> 你也可以 [使用 YAML (`.yml`) 文件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-yaml) 作为 `.properties` 文件的替代。

如果您不喜欢 `application.properties` 作为配置文件名，则可以通过指定 `spring.config.name` 环境属性来切换到另一个文件名。您还可以通过使用 `spring.config.location` 环境属性（这是目录位置或文件路径的逗号分隔列表）来引用显式位置。下面的示例演示如何指定其他文件名：

```
$ java -jar myproject.jar --spring.config.name=myproject
```

下面的例子展示了如何指定两个位置：

```
$ java -jar myproject.jar --spring.config.location=classpath:/default.properties,classpath:/override.properties
```

> 使用 `spring.config.name` 和 `spring.config.location` 可以很早地确定哪些文件必须被加载。必须将它们定义为环境属性（通常是操作系统环境变量，系统属性或命令行参数）。

如果 `spring.config.location` 包含目录（而不是文件），则它们应以 `/` 结尾（在运行时，应在加载之前附加从 `spring.config.name` 生成的名称，包括特定于配置文件的文件名）。在 `spring.config.location` 中指定的文件按原样使用，不支持特定于配置文件的变体，并且被任何特定于配置文件的属性覆盖。

配置位置以相反的顺序搜索。 默认情况下，配置的位置是 `classpath:/,classpath:/config/,file:./,file:./config/`。实际的搜索顺序如下：

1. `file:./config/`
2. `file:./`
3. `classpath:/config/`
4. `classpath:/`

当使用 `spring.config.location` 配置自定义配置位置时，它们将替换默认位置。例如，如果将 `spring.config.location` 配置为值 `classpath:/custom-config/,file:./custom-config/`，则搜索顺序如下：

1. `file:./custom-config/`
2. `classpath:custom-config/`

另外，当使用 `spring.config.additional-location` 配置自定义配置位置时，除了默认位置外，还会使用它们。在默认位置之前会搜索其他位置。例如，如果配置了 `classpath:/custom-config/,file:./custom-config/` 的其他位置，则搜索顺序如下：

1. `file:./custom-config/`
2. `classpath:custom-config/`
3. `file:./config/`
4. `file:./`
5. `classpath:/config/`
6. `classpath:/`

通过此搜索顺序，您可以在一个配置文件中指定默认值，然后在另一个配置文件中有选择地覆盖这些值。您可以在默认位置之一的 `application.properties`（或使用 `spring.config.name` 选择的其他任何基本名称）中为应用程序提供默认值。然后，可以在运行时使用自定义位置之一中的其他文件覆盖这些默认值。

> 如果您使用环境变量而不是系统属性，则大多数操作系统都不允许使用句点分隔的键名，但可以使用下划线（例如，用 `SPRING_CONFIG_NAME` 代替 `spring.config.name`）。

> 如果您的应用程序在容器中运行，则可以使用 JNDI 属性（在 `java:comp/env` 中）或 servlet 上下文初始化参数代替环境变量或系统属性，也可以两者同时使用。

#### 4.2.4. 特定于配置文件的属性

除了 `application.properties` 文件之外，还可以使用以下命名约定来定义特定于配置文件的属性： `application-{profile}.properties`。如果没有设置任何活动配置文件，则 `Environment` 具有一组默认配置文件（默认为 `[default]`）。换句话说，如果没有显式激活任何配置文件，则将加载 `application-default.properties` 中的属性。

特定于配置文件的属性是从与标准 `application.properties` 相同的位置加载的，特定于配置文件的文件总是会覆盖非特定文件，无论特定于配置文件的文件位于打包 jar 的内部还是外部。

如果指定了多个配置文件，则采用后赢策略。例如，由 `spring.profiles.active` 属性指定的配置文件会在通过 `SpringApplication` API 配置的配置文件之后添加，因此具有优先权。

> 如果您在 `spring.config.location` 中指定了任何文件，则不考虑这些文件的特定于配置文件的变体。如果您还想使用特定于配置文件的属性，请使用 `spring.config.location` 中的目录。

#### 4.2.5. 属性中的占位符

使用时，`application.properties` 中的值将通过现有的 `Environment` 进行过滤，因此您可以引用以前定义的值（例如，在 System 属性中定义的）。

```properties
app.name=MyApp
app.description=${app.name} is a Spring Boot application
```

> 你还可以使用此技术创建现有 Spring Boot 属性的"短"变体。参考*如何使用'短'命令行参数*了解更对细节。

#### 4.2.6. 属性加密

Spring Boot 没有提供任何属性值加密的内建支持，不过，它提供了修改 Spring `Evironment` 中包含的属性值所必需的钩子。`EnvironmentPostProcessor` 接口允许你在应用启动之前修改 `Evironment` 。参考 [Customize the Environment or ApplicationContext Before It Starts](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-customize-the-environment-or-application-context) 了解更多细节。

如果你正在寻找保存账号和密码的安全方式， [Spring Cloud Vault](https://cloud.spring.io/spring-cloud-vault/) 项目提供了将外部好化配置存储到 [HashiCorp Vault](https://www.vaultproject.io/) 中的支持。

#### 4.2.7. 使用 YAML 替代属性文件

[YAML](https://yaml.org/) 是 JSON 的超集，因而，是一种描述层级配置数据的方便格式。`SpringApplication` 类自动支持 YAML 作为属性文件的替代，只要你的类路径上存在 [SnakeYAML](https://bitbucket.org/asomov/snakeyaml) 类库。

> 如果你使用启动器，SnakeYAML 则由 `spring-boot-starter` 自动提供。

##### 加载 YAML

Spring 框架提供两种方便的类用于加载 YAML 文件。`YamlPropertiesFactoryBean` 加载 YAML 为 `Properties` ，`YamlMapFactoryBean` 加载 YAML 为 `Map` 。

比如，考虑下面的 YAML 文件：

```yaml
environments:
    dev:
        url: https://dev.example.com
        name: Developer Setup
    prod:
        url: https://another.example.com
        name: My Cool App
```

上面的例子可以被转化为下面的配置：

```properties
environments.dev.url=https://dev.example.com
environments.dev.name=Developer Setup
environments.prod.url=https://another.example.com
environments.prod.name=My Cool App
```

YAML 列表表示为带有 [`index`] 解引用器的属性键。例如，考虑以下 YAML：

```yaml
my:
   servers:
       - dev.example.com
       - another.example.com
```

上面的例子将被转化为下面的属性：

```properties
my.servers[0]=dev.example.com
my.servers[1]=another.example.com
```

要通过使用 Spring Boot 的 `Binder` 实用程序（这是 `@ConfigurationProperties`的作用）进行类似的属性绑定，您需要在目标 bean 中有一个属性，类型为 `java.util.List`（或 `Set`）。同时需要提供一个 setter 或使用一个可变值对其进行初始化。例如，以下示例绑定到前面显示的属性：

```java
@ConfigurationProperties(prefix="my")
public class Config {

    private List<String> servers = new ArrayList<String>();

    public List<String> getServers() {
        return this.servers;
    }
}
```

##### 在 Spring 环境中暴露 YAML 为属性

`YamlPropertySourceLoader` 类可用于在 Spring 环境中将 YAML 作为 `PropertySource` 公开。这样做可以让您使用带有占位符语法的 `@Value` 注解来访问 YAML 属性。

##### 多配置文件的 YAML 文档

您可以使用 `spring.profiles` 键在一个文件中指定多个特定于配置文件的 YAML 文档，以指示何时应用该文档，如以下示例所示：

```yaml
server:
    address: 192.168.1.100
---
spring:
    profiles: development
server:
    address: 127.0.0.1
---
spring:
    profiles: production & eu-central
server:
    address: 192.168.1.120
```

在前面的示例中，如果 `development` 配置文件处于活动状态，则 `server.address` 属性为 `127.0.0.1`。类似地，如果 `production` **和** `eu-central` 配置文件处于活动状态，则 `server.address` 属性为 `192.168.1.120`。如果未启用 `development` ， `production` 和 `eu-central` 配置文件，则该属性的值为 `192.168.1.100`。

> 因此 `spring.profiles` 可以包含一个简单的配置文件名称（例如 `production`）或一个配置文件表达式。配置文件表达式允许表达更复杂的配置文件逻辑，例如 `production＆(eu-central | eu-west)`。有关更多详细信息，请参见 [参考指南](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/core.html#beans-definition-profiles-java)。

如果在启动应用程序上下文时未明确激活任何配置，则会激活默认配置文件。因此，在以下 YAML 中，我们为 `spring.security.user.password` 设置了一个值，该值仅在“默认”配置文件激活时可用：

```yaml
server:
  port: 8000
---
spring:
  profiles: default
  security:
    user:
      password: weak
```

而在以下示例中，始终设置密码是因为该密码未附加到任何配置文件，并且必须根据需要在所有其他配置文件中将其显式重置：

```yaml
server:
  port: 8000
spring:
  security:
    user:
      password: weak
```

使用 `spring.profiles` 元素指定的 Spring 配置可以通过使用 `!` 字符来取反。如果为单个文档指定了否定的配置文件和非否定的配置文件，则至少一个非否定的配置文件必须匹配，并且否定的配置文件不能匹配。

##### YAML 的缺点

无法通过使用 `@PropertySource` 注解来加载 YAML 文件。因此，在需要以这种方式加载值的情况下，需要使用属性文件。

在特定于配置文件的 YAML 文件中使用多 YAML 文档语法可能会导致意外行为。例如，考虑文件中的以下配置：

application-dev.yml

```yaml
server:
  port: 8000
---
spring:
  profiles: "!test"
  security:
    user:
      password: "secret"
```

如果使用参数 `--spring.profiles.active=dev` 来运行应用程序，则可能希望将 `security.user.password` 设置为“秘密的”，但实际情况并非如此。

嵌套文档将被过滤，因为主文件名为 `application-dev.yml`。它已经被认为是特定于配置文件的，并且嵌套文档将被忽略。

> 我们建议您不要混用特定于配置文件的 YAML 文件和多个 YAML 文档。坚持只使用其中之一。

#### 4.2.8. 类型安全的配置属性

使用 `@Value("${property}")` 注解来注入配置属性有时会很麻烦，尤其是当您使用多个属性或数据本质上是分层的情况下。Spring Boot 提供了一种使用属性的替代方法，该属性使强类型的 Bean 可以管理和验证应用程序的配置。

> 参考 [differences between `@Value` and type-safe configuration properties](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-vs-value).

##### JavaBean 属性绑定

可以绑定一个声明标准 JavaBean 属性的 bean，如以下示例所示：

```java
package com.example;

import java.net.InetAddress;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

import org.springframework.boot.context.properties.ConfigurationProperties;

@ConfigurationProperties("acme")
public class AcmeProperties {

    private boolean enabled;

    private InetAddress remoteAddress;

    private final Security security = new Security();

    public boolean isEnabled() { ... }

    public void setEnabled(boolean enabled) { ... }

    public InetAddress getRemoteAddress() { ... }

    public void setRemoteAddress(InetAddress remoteAddress) { ... }

    public Security getSecurity() { ... }

    public static class Security {

        private String username;

        private String password;

        private List<String> roles = new ArrayList<>(Collections.singleton("USER"));

        public String getUsername() { ... }

        public void setUsername(String username) { ... }

        public String getPassword() { ... }

        public void setPassword(String password) { ... }

        public List<String> getRoles() { ... }

        public void setRoles(List<String> roles) { ... }

    }
}
```

上面的 POJO 定义了下面的属性：

- `acme.enabled`，默认值是 `false` 。
- `acme.remote-address`，其类型可以从 `String` 强制转化而来。
- `acme.security.username`，带有一个嵌套的 `security` 对象，其名称由属性的名称确定。特别是，返回类型根本不使用，可能是 `SecurityProperties`。
- `acme.security.password`。
- `acme.security.roles`，值是默认为 `USER` 的 `String` 集合。

> Spring Boot 的自动配置在很大程度上利用了 `@ConfigurationProperties` 来轻松配置自动配置的 bean。与自动配置类相似，Spring Boot 中可用的 `@ConfigurationProperties` 类仅供内部使用。通过属性文件，YAML 文件，环境变量等配置的映射到该类的属性是公共 API，但是该类本身的内容并不意味着可以直接使用。

> 这种安排依赖于默认的空构造器，并且 getter 和 setter 通常是强制性的，因为绑定是通过标准 Java Beans 属性描述符进行的，就像在 Spring MVC 中一样。在以下情况下，可以忽略 setter：
>
> - 一旦 Map 初始化完成，就只需要使用 getter，而不再需要 setter，因为它们可以由绑定器修改。
> - 集合和数组能够通过索引（典型的是使用 YAML）或者使用单个逗号分隔的值（属性）来访问。在后者情况下，setter 是必需的。我们推荐始终为该类型添加 setter。如果你初始化一个集合，确保它是不可变的（如前面例子所示）。
> - 如果嵌套的 POJO 属性已初始化（例如前面示例中的 `Security` 字段），则不需要 setter。如果希望绑定器通过使用其默认构造函数动态创建实例，则需要一个 setter。
>
> 有些人使用 Lombok 项目自动添加 getter 和 setter。确保 Lombok 不会为这种类型生成任何特定的构造函数，因为容器会自动使用它来实例化该对象。
>
> 最后，仅考虑标准 Java Bean 属性，不支持对静态属性的绑定。

##### 构造器绑定

上一节中的例子可以被重写为不可变风格，如下所示：

```java
package com.example;

import java.net.InetAddress;
import java.util.List;

import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.boot.context.properties.ConstructorBinding;
import org.springframework.boot.context.properties.DefaultValue;

@ConstructorBinding
@ConfigurationProperties("acme")
public class AcmeProperties {

    private final boolean enabled;

    private final InetAddress remoteAddress;

    private final Security security;

    public AcmeProperties(boolean enabled, InetAddress remoteAddress, Security security) {
        this.enabled = enabled;
        this.remoteAddress = remoteAddress;
        this.security = security;
    }

    public boolean isEnabled() { ... }

    public InetAddress getRemoteAddress() { ... }

    public Security getSecurity() { ... }

    public static class Security {

        private final String username;

        private final String password;

        private final List<String> roles;

        public Security(String username, String password,
                @DefaultValue("USER") List<String> roles) {
            this.username = username;
            this.password = password;
            this.roles = roles;
        }

        public String getUsername() { ... }

        public String getPassword() { ... }

        public List<String> getRoles() { ... }

    }

}
```

在此设置中，使用 `@ConstructorBinding` 注解指示应使用构造函数绑定。这意味着绑定器将期望找到带有您希望绑定的参数的构造函数。

`@ConstructorBinding` 类的嵌套成员（例如上例中的 `Security`）也将通过其构造函数进行绑定。

可以使用 `@DefaultValue` 指定默认值，并且将应用相同的转换服务将 `String` 值强制转换为缺少属性的目标类型。

> 要使用构造函数绑定，必须使用 `@EnableConfigurationProperties` 或配置属性扫描来启用该类。您不能对通过常规 Spring 机制创建的 bean 使用构造函数绑定（例如，`@Component bean` 的 beans，通过 `@Bean` 方法创建的 bean 或使用 `@Import` 加载的 bean）。

> 如果您的类有多个构造函数，则还可以直接在应绑定的构造函数上使用 `@ConstructorBinding`。

##### 启用 `@ConfigurationProperties` 注解的类型

Spring Boot 提供了绑定 `@ConfigurationProperties` 类型并将其注册为 Bean 的基础架构。您可以逐类启用配置属性，也可以启用与组件扫描类似的方式进行配置属性扫描。

有时，带有 `@ConfigurationProperties` 注解的类可能不适用于扫描，例如，如果您正在开发自己的自动配置，或者想要有条件地启用它们。在这些情况下，请使用 `@EnableConfigurationProperties` 注解指定要处理的类型列表。可以在任何 `@Configuration` 类上完成，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
@EnableConfigurationProperties(AcmeProperties.class)
public class MyConfiguration {
}
```

要使用配置属性扫描，请在您的应用程序中添加 `@ConfigurationPropertiesScan` 注解。通常，它被添加到以 `@SpringBootApplication` 注解的主应用程序类中，但是也可以被添加到任何 `@Configuration` 类中。默认情况下，将从声明注解的类的包中进行扫描。如果要定义要扫描的特定程序包，可以按照以下示例所示进行操作：

```java
@SpringBootApplication
@ConfigurationPropertiesScan({ "com.example.app", "org.acme.another" })
public class MyApplication {
}
```

> 当使用配置属性扫描或通过 `@EnableConfigurationProperties` 注册了 `@ConfigurationProperties` bean时，该 bean 具有常规名称：`<prefix>-<fqn>`，其中，`<prefix>` 是在 `@ConfigurationProperties` 中指定的环境 key 前缀。`<fqn>` 是 Bean 的完全限定名称。如果注解不提供任何前缀，则仅使用 Bean 的完全限定名称。
>
> 上例中的 bean 名称是 `acme-com.example.AcmeProperties`。

我们建议 `@ConfigurationProperties` 只处理环境，尤其不要从上下文中注入其他 bean。对于极端情况，可以使用 setter 注入或框架提供的任何 `*Aware` 接口（例如，如果需要访问 `Environment`，则可以使用 `EnvironmentAware`）。如果仍然想使用构造函数注入其他 bean，则必须使用 `@Component` 注解配置属性 bean，并使用基于 JavaBean 的属性绑定。

##### 使用 `@ConfigurationProperties` 注解的类型

这种配置样式与 `SpringApplication` 外部 YAML 配置特别有效，如以下示例所示：

```yaml
# application.yml

acme:
    remote-address: 192.168.1.1
    security:
        username: admin
        roles:
          - USER
          - ADMIN

# additional configuration as required
```

要使用 `@ConfigurationProperties` bean，可以像使用其他任何 bean 一样注入它们，如以下示例所示：

```java
@Service
public class MyService {

    private final AcmeProperties properties;

    @Autowired
    public MyService(AcmeProperties properties) {
        this.properties = properties;
    }

    //...

    @PostConstruct
    public void openConnection() {
        Server server = new Server(this.properties.getRemoteAddress());
        // ...
    }

}
```

> 使用 `@ConfigurationProperties` 还可以让您生成元数据文件，IDE 可以使用这些元数据文件为您提供关键字自动完成功能。有关详细信息，请参见 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#configuration-metadata)。

##### 第三方配置

除了使用 `@ConfigurationProperties` 注解类之外，您还可以在公共 `@Bean` 方法上使用它。当您要将属性绑定到你控制范围之外的第三方组件时，这样做特别有用。

要通过 `Environment` 属性配置 bean，请在其 bean 注册中添加 `@ConfigurationProperties`，如以下示例所示：

```java
@ConfigurationProperties(prefix = "another")
@Bean
public AnotherComponent anotherComponent() {
    ...
}
```

任何以 `another` 前缀定义的 JavaBean 属性都被映射到该 `AnotherComponent` bean上，类似于前面的 `AcmeProperties` 示例。

##### 宽松绑定

Spring Boot 使用一些宽松的规则来将 `Environment` 属性绑定到 `@ConfigurationProperties` bean，因此 `Environment` 属性名称和 bean 属性名称之间不需要完全匹配。有用的常见示例包括破折号分隔的环境属性（例如，`context-path` 绑定到 `contextPath`）和大写的环境属性（例如，`PORT` 绑定到 `port`）。

作为示例，考虑下面的 `@ConfigurationProperties` 类：

```java
@ConfigurationProperties(prefix="acme.my-project.person")
public class OwnerProperties {

    private String firstName;

    public String getFirstName() {
        return this.firstName;
    }

    public void setFirstName(String firstName) {
        this.firstName = firstName;
    }

}
```

上面的代码可以使用下面的属性名：

| Property                            | Note                                                      |
| :---------------------------------- | :-------------------------------------------------------- |
| `acme.my-project.person.first-name` | 短横线隔开式，推荐使用在 `.properties` 和 `.yml` 文件中。 |
| `acme.myProject.person.firstName`   | 标准驼峰形式。                                            |
| `acme.my_project.person.first_name` | 下划线表示法，可以用于 `.properties` 和 `.yml` 文件中。   |
| `ACME_MYPROJECT_PERSON_FIRSTNAME`   | 大写形式，当使用系统环境变量时推荐使用这种形式。          |

> 记号中的 `prefix`值必须是短横线隔开形式(由短横线 `-` 隔开的小写字母，如 `acme.my-project.person`) 。

| Property Source | Simple                                                   | List                                                         |
| :-------------- | :------------------------------------------------------- | :----------------------------------------------------------- |
| Properties 文件 | 驼峰形式，短横线隔开形式或者下划线记法                   | 使用 `[]` 的标准列表语法或者逗号分隔的值列表                 |
| YAML 文件       | 驼峰形式，短横线隔开形式或者下划线记法                   | 标准 YAML 列表语法或者逗号分隔的值列表                       |
| 环境变量        | 以下划线作为定界符的大写格式。不得在属性名称中使用 `_`。 | 由下划线包围的数值，比如 `MY_ACME_1_OTHER = my.acme[1].other` |
| 系统属性        | 驼峰形式，短横线隔开形式或者下划线记法                   | 使用 `[]` 的标准列表语法或者逗号分隔的值列表                 |

> 我们建议，如果可能的话，属性以小写的短横线分隔格式存储，例如 `my.property-name = acme`。

绑定到 `Map` 属性时，如果 `key` 包含小写字母数字字符或 `-` 以外的任何内容，则需要使用方括号表示法，以便保留原始值。如果键没有被 `[]` 包围，则所有非字母数字或 `-` 的字符都将被删除。例如，考虑将以下属性绑定到 `Map`：

```yaml
acme:
  map:
    "[/key1]": value1
    "[/key2]": value2
    /key3: value3
```

上面的属性将会被绑定到 `Map` ，其中包含 `/key1`, `/key2` 和 `key3` 。

> 对于 YAML 文件，方括号需要用引号包围起来，以便正确解析 keys。

##### 合并复杂类型

如果在多个位置配置了列表，则通过替换整个列表来进行覆盖。

例如，假设一个 `MyPojo` 对象的 `name` 属性和 `description` 属性默认为 `null`。以下示例从 `AcmeProperties` 中公开了 `MyPojo` 对象的列表：

```java
@ConfigurationProperties("acme")
public class AcmeProperties {

    private final List<MyPojo> list = new ArrayList<>();

    public List<MyPojo> getList() {
        return this.list;
    }

}
```

考虑下面的配置：

```yaml
acme:
  list:
    - name: my name
      description: my description
---
spring:
  profiles: dev
acme:
  list:
    - name: my another name
```

如果 `dev` 环境配置文件未激活，则 `AcmeProperties.list` 包含一个 `MyPojo` 条目，如先前定义。但是，如果启用了 `dev` 环境配置文件，则 `list`  仍然仅包含一个条目（名称为 `my another name` ，描述为 `null` ）。此配置*不会*将第二个 `MyPojo` 实例添加到列表中，并且不会合并项目。

当在多个配置文件中指定一个 `List` 时，将使用优先级最高的列表（并且只使用那个）。考虑以下示例：

```yaml
acme:
  list:
    - name: my name
      description: my description
    - name: another name
      description: another description
---
spring:
  profiles: dev
acme:
  list:
    - name: my another name
```

在前面的示例中，如果 `dev` 环境配置文件处于活动状态，则 `AcmeProperties.list` 包含*一个* `MyPojo` 条目（名称为 `my another name`，描述为 `null`）。对于 YAML，可以使用逗号分隔的列表和 YAML 列表来完全覆盖列表的内容。

对于 `Map` 属性，您可以绑定从多个来源的属性值。但是，对于多个源中的同一属性，将使用优先级最高的属性值。以下示例从 `AcmeProperties` 中公开了 `Map<String, MyPojo>`：

```java
@ConfigurationProperties("acme")
public class AcmeProperties {

    private final Map<String, MyPojo> map = new HashMap<>();

    public Map<String, MyPojo> getMap() {
        return this.map;
    }

}
```

考虑下面的配置：

```yaml
acme:
  map:
    key1:
      name: my name 1
      description: my description 1
---
spring:
  profiles: dev
acme:
  map:
    key1:
      name: dev name 1
    key2:
      name: dev name 2
      description: dev description 2
```

如果 `dev` 环境配置文件未激活，则 `AcmeProperties.map` 包含一个键为 `key1` 的条目（名称为 `my name 1` ，描述为 `my description 1`）。但是，如果启用了 `dev` 配置文件，则 `map` 包含两个条目，其中包含键 `key1`（名称为 `dev name 1`，名称为 `my description 1`）和 `key2`（名称为 `dev name 2`，名称为 `my description 2`）。

> 前述合并规则不仅适用于 YAML 文件，而且适用于所有属性源中的属性。

##### Properties 转换

当 Spring Boot 绑定到 `@ConfigurationProperties` bean时，它试图将外部应用程序属性强制转换为正确的类型。如果需要自定义类型转换，则可以提供一个 `ConversionService` bean（带有名为 `conversionService` 的bean）或自定义属性编辑器（通过 `CustomEditorConfigurer` bean）或自定义的 `Converters`（带有定义为 `@ConfigurationPropertiesBinding` 的 bean 定义）。

> 由于在应用程序生命周期中非常早就请求了此 bean，因此请确保限制您的 `ConversionService` 使用的依赖项。通常，您需要的任何依赖项可能在创建时未完全初始化。如果配置键强制不需要自定义的 `ConversionService`，则可能要重命名，而仅依赖于具有 `@ConfigurationPropertiesBinding` 限定的自定义转换器。

###### 转换持续时间

Spring Boot 为表达持续时间提供了专门的支持。如果公开 `java.time.Duration` 属性，则应用程序属性中的以下格式可用：

- 常规的 `long` 表示形式（使用毫秒作为默认单位，除非指定了 `@DurationUnit`）
- 标准的 ISO-8601 格式 [used by `java.time.Duration`](https://docs.oracle.com/javase/8/docs/api//java/time/Duration.html#parse-java.lang.CharSequence-)
- 值和单位相结合的更具可读性的格式（例如，`10s` 表示10秒）

考虑下面的例子：

```java
@ConfigurationProperties("app.system")
public class AppSystemProperties {

    @DurationUnit(ChronoUnit.SECONDS)
    private Duration sessionTimeout = Duration.ofSeconds(30);

    private Duration readTimeout = Duration.ofMillis(1000);

    public Duration getSessionTimeout() {
        return this.sessionTimeout;
    }

    public void setSessionTimeout(Duration sessionTimeout) {
        this.sessionTimeout = sessionTimeout;
    }

    public Duration getReadTimeout() {
        return this.readTimeout;
    }

    public void setReadTimeout(Duration readTimeout) {
        this.readTimeout = readTimeout;
    }

}
```

要指定 30 秒的会话超时，`30`，`PT30S` 和 `30s` 都是等效的。可以用以下任何一种形式指定 500ms 的读取超时：`500`，`PT0.5S` 和 `500ms`。

您也可以使用任何受支持的单位。这些是：

- `ns` 纳秒

- `us` 微秒

- `ms` 毫秒（毫秒）

- `s` 秒

- `m` 分钟

- `h` 小时

- `d` 天

默认单位是毫秒，可以使用 `@DurationUnit` 覆盖，如上面的示例所示。

> 如果您要从仅使用 `Long` 表示持续时间的先前版本进行升级，请确保在转换为 `Duration` 的时间单位不是毫秒的情况下定义单位（使用 `@DurationUnit`）。这样做可以提供透明的升级路径，同时支持更丰富的格式。

###### 转换数据尺寸

Spring Framework 具有一个 `DataSize` 值类型，该值类型以字节为单位表示大小。如果您公开 `DataSize` 属性，则应用程序属性中的以下格式可用：

- 常规的 `long` 表示形式（除非指定了 `@DataSizeUnit`，否则使用字节作为默认单位）

- 将值和单位组合在一起的更具可读性的格式（例如，`10MB` 表示 10 兆字节）

考虑以下示例：

```java
@ConfigurationProperties("app.io")
public class AppIoProperties {

    @DataSizeUnit(DataUnit.MEGABYTES)
    private DataSize bufferSize = DataSize.ofMegabytes(2);

    private DataSize sizeThreshold = DataSize.ofBytes(512);

    public DataSize getBufferSize() {
        return this.bufferSize;
    }

    public void setBufferSize(DataSize bufferSize) {
        this.bufferSize = bufferSize;
    }

    public DataSize getSizeThreshold() {
        return this.sizeThreshold;
    }

    public void setSizeThreshold(DataSize sizeThreshold) {
        this.sizeThreshold = sizeThreshold;
    }

}
```

要指定 10 兆字节的缓冲区大小，`10` 和 `10MB` 是等效的。可以将 256 个字节的大小阈值指定为 `256` 或 `256B`。您也可以使用任何受支持的单位。这些是：

- `B` 表示字节

- `KB` 代表千字节

- `MB` 代表兆字节

- `GB` 代表GB

- `TB`（TB）

默认单位时字节，可以通过使用  `@DataSizeUnit` 覆盖，如上面例子所示。

> 如果您要从仅使用 `Long` 表示大小的先前版本进行升级，请确保在切换至 `DataSize` 而没有使用字节作为单位的情况下定义单位（使用 `@DataSizeUnit`）。这样做可以提供透明的升级路径，同时支持更丰富的格式。

##### @ConfigurationProperties 验证

每当使用 Spring 的 `@Validated` 注解进行注释时，Spring Boot 就会尝试验证 `@ConfigurationProperties` 类。您可以在配置类上直接使用 JSR-303 `javax.validation` 约束注解。为此，请确保在类路径上有兼容的 JSR-303 实现，然后将约束注解添加到字段中，如以下示例所示：

```java
@ConfigurationProperties(prefix="acme")
@Validated
public class AcmeProperties {

    @NotNull
    private InetAddress remoteAddress;

    // ... getters and setters

}
```

> 您也可以通过用 `@Validated` 注解创建配置属性的 `@Bean` 方法来触发验证。

为了确保始终为嵌套属性触发验证，即使没有找到属性，相关字段也必须使用 `@Valid` 注解修饰。以下示例以前面的 `AcmeProperties` 示例为基础：

```java
@ConfigurationProperties(prefix="acme")
@Validated
public class AcmeProperties {

    @NotNull
    private InetAddress remoteAddress;

    @Valid
    private final Security security = new Security();

    // ... getters and setters

    public static class Security {

        @NotEmpty
        public String username;

        // ... getters and setters

    }

}
```

您也可以通过创建一个名为 `configurationPropertiesValidator` 的 bean 定义来添加一个自定义的 Spring Validator。`@Bean` 方法应该声明为 `static`。配置属性验证器是在应用程序生命周期的早期创建的，并且将 `@Bean` 方法声明为静态方法可以创建 Bean，而不必实例化 `@Configuration` 类。这样做避免了由早期实例化引起的任何问题。

> `spring-boot-actuator` 模块包括一个端点，该端点公开了所有的 `@ConfigurationProperties` bean。将您的 Web 浏览器指向 `/actuator/configprops` 或使用等效的 JMX 端点。有关详细信息，请参见 [Production ready features](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-endpoints) 部分。

##### @ConfigurationProperties vs. @Value

`@Value` 注解是核心容器功能，它没有提供与类型安全的配置属性相同的功能。下表总结了 `@ConfigurationProperties` 和 `@Value` 支持的功能：

| Feature                                                      | `@ConfigurationProperties` | `@Value` |
| :----------------------------------------------------------- | :------------------------- | :------- |
| [Relaxed binding](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-relaxed-binding) | Yes                        | No       |
| [Meta-data support](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#configuration-metadata) | Yes                        | No       |
| `SpEL` evaluation                                            | No                         | Yes      |

如果您为自己的组件定义了一组配置键，我们建议您将它们组合在一个以 `@ConfigurationProperties` 注解修饰的 POJO 中。您还应该意识到，由于 `@Value` 不支持宽松的绑定，因此如果您需要通过使用环境变量来提供值，则不是一个好的选择。

最后，尽管你能够在 `@Value` 中编写 `SpEL` 表达式，但不会处理来自 [application property files](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-application-property-files)  的此类表达式。

### 4.3. Profiles

Spring Profiles 提供了隔离你的应用的配置部分并使得它们只在特定环境下可用的方法。所有的 `@Component` ，`@Configuration` ，或者 `@ConfigurationProperties` 都能够使用 `@Profile` 标记以限制它们何时加载。如下面例子所示：

```java
@Configuration(proxyBeanMethods = false)
@Profile("production")
public class ProductionConfiguration {

    // ...

}
```

> 如果通过 `@EnableConfigurationProperties` 注册了 `@ConfigurationProperties` bean而不是通过自动扫描进行注册，则需要在具有 `@EnableConfigurationProperties` 注解的 `@Configuration` 类上指定 `@Profile` 注解。在扫描 `@ConfigurationProperties` 的情况下，可以在 `@ConfigurationProperties` 类本身上指定 `@ Profile`。

您可以使用 `spring.profiles.active` 环境属性来指定哪些配置文件处于活动状态。您可以通过本章前面介绍的任何方式指定属性。例如，您可以将其包含在 `application.properties` 中，如以下示例所示：

```properties
spring.profiles.active=dev,hsqldb
```

你也可以在命令行中指定它，通过使用开关： `--spring.profiles.active=dev,hsqldb`。

#### 4.3.1. 添加活动 Profiles

`spring.profiles.active` 属性遵循与其他属性相同的排序规则：最高的 `PropertySource` 获胜。这意味着您可以在 `application.properties` 中指定活动 profile，然后使用命令行开关“替换”它们。

有时，将特定于配置文件的属性“添加”到活动 profile 文件而不是替换它们是有用的。`spring.profiles.include` 属性可用于无条件添加活动 profile 文件。`SpringApplication` 入口点还具有 Java API，用于设置其他配置文件（即，在由 `spring.profiles.active` 属性激活的 profile 的上面）。参见 [SpringApplication](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/SpringApplication.html) 中的 `setAdditionalProfiles()` 方法。

例如，当使用开关 `--spring.profiles.active=prod` 运行具有以下属性的应用程序时，也会激活 `proddb` 和 `prodmq` profile 文件：

```yaml
---
my.property: fromyamlfile
---
spring.profiles: prod
spring.profiles.include:
  - proddb
  - prodmq
```

> 请记住，可以在 YAML 文档中定义 `spring.profiles` 属性，以确定何时将该特定文档包括在配置中。请参阅 [根据环境更改配置](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-change-configuration-depending-on-the-environment ) 了解更多细节。

#### 4.3.2. 编程式设定 Profiles

您可以在应用程序运行之前通过调用 `SpringApplication.setAdditionalProfiles(…)` 来以编程方式设置活动 profile 文件。也可以使用 Spring 的 `ConfigurableEnvironment` 接口来激活 profile 文件。

#### 4.3.3. 特定于 Profile 的配置文件

`application.properties`（或 `application.yml`）和通过 `@ConfigurationProperties` 引用的文件的特定于配置文件的变体都被视为文件并已加载。参见“ [特定于配置文件的属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-profile-specific-properties) “以获取详细信息。

### 4.4. 日志

Spring Boot 使用 [Commons Logging](https://commons.apache.org/logging) 进行所有内部日志记录，但是对底层日志实现保持开放。为  [Java Util Logging](https://docs.oracle.com/javase/8/docs/api//java/util/logging/package-summary.html)， [Log4J2](https://logging.apache.org/log4j/2.x/)， 和 [Logback](https://logback.qos.ch/) 提供默认配置。在每种情况下，记录器都已预先配置为使用控制台输出，同时还提供可选文件输出。

默认情况下，如果使用“启动器”，则使用 Logback 进行日志记录。还包括适当的 Logback 路由，以确保使用 Java Util Logging，Commons Logging，Log4J 或 SLF4J 的依赖库都可以正常工作。

> Java 有许多可用的日志记录框架。如果上面的列表看起来令人困惑，请不要担心。通常，您不需要更改日志记录依赖项，并且 Spring Boot 默认值可以正常工作。

> 将应用程序部署到 Servlet 容器或应用程序服务器时，通过 Java Util Logging API 执行的日志记录不会路由到应用程序的日志中。这样可以防止容器或其他已部署到容器中的其它应用程序产生的日志记录出现在你的应用程序的日志中。

#### 4.4.1. 日志格式

Spring Boot 的默认日志输出类似于以下示例：

```
2019-03-05 10:57:51.112  INFO 45469 --- [           main] org.apache.catalina.core.StandardEngine  : Starting Servlet Engine: Apache Tomcat/7.0.52
2019-03-05 10:57:51.253  INFO 45469 --- [ost-startStop-1] o.a.c.c.C.[Tomcat].[localhost].[/]       : Initializing Spring embedded WebApplicationContext
2019-03-05 10:57:51.253  INFO 45469 --- [ost-startStop-1] o.s.web.context.ContextLoader            : Root WebApplicationContext: initialization completed in 1358 ms
2019-03-05 10:57:51.698  INFO 45469 --- [ost-startStop-1] o.s.b.c.e.ServletRegistrationBean        : Mapping servlet: 'dispatcherServlet' to [/]
2019-03-05 10:57:51.702  INFO 45469 --- [ost-startStop-1] o.s.b.c.embedded.FilterRegistrationBean  : Mapping filter: 'hiddenHttpMethodFilter' to: [/*]
```

输出包含以下项目：

- 日期和时间：毫秒精度，易于排序。

- 日志级别：`ERROR`， `WARN`， `INFO`， `DEBUG`， 或者 `TRACE`。

- 进程ID。

- 一个 `---` 分隔符，用于区分实际日志消息的开始。

- 线程名称：方括号内（对于控制台输出，可能会被截断）。

- 记录器名称：这通常是源类名称（通常缩写）。

- 日志消息。

> Logback 没有 `FATAL` 级别，该级别对应于其它日志框架的 `ERROR`。

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
> ```
> 2019-08-30 12:30:04.031 user:someone INFO 22174 --- [  nio-8080-exec-0] demo.Controller
> Handling authenticated request
> ```

#### 4.4.7. Logback 扩展

Spring Boot 包含许多 Logback 扩展，可以帮助进行高级配置。您可以在 `logback-spring.xml` 配置文件中使用这些扩展名。

> 由于标准的 `logback.xml` 配置文件加载得太早，因此您不能在其中使用扩展名。您需要使用 `logback-spring.xml` 或定义 `logging.config` 属性。

> 这些扩展不能与 Logback 的 [配置扫描](https://logback.qos.ch/manual/configuration.html#autoScan) 一起使用。如果尝试这样做，则对配置文件进行更改将导致类似于以下记录之一的错误：

```
ERROR in ch.qos.logback.core.joran.spi.Interpreter@4:71 - no applicable action for [springProperty], current ElementPath is [[configuration][springProperty]]
ERROR in ch.qos.logback.core.joran.spi.Interpreter@4:71 - no applicable action for [springProfile], current ElementPath is [[configuration][springProfile]]
```

##### 特定于 Profile 的配置

使用 `<springProfile>` 标签，您可以根据活动的 Spring profiles 文件有选择地包括或排除配置部分。在 `<configuration>` 元素内的任何位置都支持 profile 小节。使用 `name` 属性指定哪个 profile 文件接受配置。标签 `<springProfile>` 可以包含一个简单的 profile 文件名称（例如 `staging`）或一个 profile 文件表达式。profile 文件表达式允许表达更复杂的 profile 文件逻辑，例如 `production＆(eu-central | eu-west)`。有关更多详细信息，请参见 [参考指南](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/core.html#beans-definition-profiles-java)。以下清单显示了三个示例 profile 文件：

```xml
<springProfile name="staging">
    <!-- configuration to be enabled when the "staging" profile is active -->
</springProfile>

<springProfile name="dev | staging">
    <!-- configuration to be enabled when the "dev" or "staging" profiles are active -->
</springProfile>

<springProfile name="!production">
    <!-- configuration to be enabled when the "production" profile is not active -->
</springProfile>
```

##### 环境属性

使用 `<springProperty>` 标签可以暴露 Spring  `Environment` 中的属性，以便在 Logback 中使用。如果您想从 Logback 配置中访问 `application.properties` 文件中的值，则这样做很有用。该标签的工作方式类似于 Logback 的标准 `<property>` 标签。但是，不是指定直接的 `value`，而是指定属性的 `source`（来自 `Environment`）。如果您需要将属性存储在 `local` 范围之外的其他地方，则可以使用 `scope` 属性。如果需要后备值（如果未在`Environment` 中设置该属性），则可以使用 `defaultValue` 属性。以下示例显示如何公开在 Logback 中使用的属性：

```xml
<springProperty scope="context" name="fluentHost" source="myapp.fluentd.host"
        defaultValue="localhost"/>
<appender name="FLUENT" class="ch.qos.logback.more.appenders.DataFluentAppender">
    <remoteHost>${fluentHost}</remoteHost>
    ...
</appender>
```

> 必须在短横线分隔形式下指定 `source`（例如 `my.property-name`）。但是，可以使用宽松的规则将属性添加到 `Environment` 中。

### 4.5. 国际化

Spring Boot 支持本地化消息，因此您的应用程序可以迎合不同语言首选项的用户。默认情况下，Spring Boot 在类路径的根目录下查找 `messages` 资源包的存在。

> 当配置的资源包的默认属性文件可用时（即默认情况下为 `messages.properties`），将应用自动配置。如果您的资源包仅包含特定于语言的属性文件，则需要添加默认资源文件。如果找不到与任何配置的基本名称匹配的属性文件，则不会有自动配置的 `MessageSource`。

可以使用 `spring.messages` 名称空间配置资源包的基本名称以及其他几个属性，如以下示例所示：

```properties
spring.messages.basename=messages,config.i18n.messages
spring.messages.fallback-to-system-locale=false
```

> `spring.messages.basename` 支持逗号分隔的位置列表，可以是包限定符，也可以是从类路径根目录解析的资源。

参考 [`MessageSourceProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/context/MessageSourceProperties.java) 获取更多支持的选项。

### 4.6. JSON

Spring Boot 提供了三种 JSON 映射类库支持：

- Gson
- Jackson
- JSON-B

Jackson 是首选默认的类库。

#### 4.6.1. Jackson

提供了 Jackson 的自动配置功能，并且 Jackson 是 `spring-boot-starter-json` 的一部分。当 Jackson 在类路径上时，将自动配置 `ObjectMapper` bean。提供了几个配置属性用于 [自定义 `ObjectMapper` 的配置](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-customize-the-jackson-objectmapper)。

#### 4.6.2. Gson

提供了 Gson 的自动配置。当 Gson 在类路径上时，将自动配置 `Gson` bean。提供了几个 `spring.gson.*` 配置属性来定制配置。为了获得更多控制权，可以使用一个或多个 `GsonBuilderCustomizer` bean。

#### 4.6.3. JSON-B

提供了 JSON-B 的自动配置。当 JSON-B API 和实现位于类路径上时，将自动配置 `Jsonb` bean。首选的 JSON-B 实现是提供依赖管理的 Apache Johnzon。

### 4.7. 开发 Web 应用

Spring Boot 非常适合于 Web 应用程序开发。您可以使用嵌入式 Tomcat，Jetty，Undertow 或 Netty 创建独立的 HTTP 服务器。大多数网络应用程序都使用 `spring-boot-starter-web` 模块来快速启动和运行。您也可以选择使用 `spring-boot-starter-webflux` 模块构建反应式 Web 应用程序。

如果尚未开发 Spring Boot Web 应用程序，则可以遵循 *入门*部分中的 ”Hello World！"示例。

#### 4.7.1. Spring Web MVC 框架

[Spring Web MVC framework](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc) (通常简称为 “Spring MVC”) 是一个完整的 MVC web 框架。Spring MVC 允许您创建特殊的 `@Controller` 或 `@RestController` bean 来处理传入的 HTTP 请求。控制器中的方法通过使用 `@RequestMapping` 注解映射到 HTTP。

下面的代码展示了一个返回 JSON 数据的典型 `@RestController` ：

```java
@RestController
@RequestMapping(value="/users")
public class MyRestController {

    @RequestMapping(value="/{user}", method=RequestMethod.GET)
    public User getUser(@PathVariable Long user) {
        // ...
    }

    @RequestMapping(value="/{user}/customers", method=RequestMethod.GET)
    List<Customer> getUserCustomers(@PathVariable Long user) {
        // ...
    }

    @RequestMapping(value="/{user}", method=RequestMethod.DELETE)
    public User deleteUser(@PathVariable Long user) {
        // ...
    }

}
```

Spring MVC 是 Spring 框架核心的一部分，更多细节参考 [reference documentation](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc)。还有一些 Spring MVC 文档位于 [spring.io/guides](https://spring.io/guides)。

##### Spring MVC 自动配置

Spring Boot 为 Spring MVC 提供了自动配置，可与大多数应用程序完美配合。

自动配置在 Spring 的默认设置之上添加了以下功能：

- 包含 `ContentNegotiatingViewResolver` 和 `BeanNameViewResolver` bean。

- 支持提供静态资源，包括对 WebJars 的支持（在[本文档后面介绍](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-static-content)）。

- 自动转换 `Converter`，`GenericConverter` 和 `Formatter` bean。

- 支持 `HttpMessageConverters`（在 [本文档后面介绍](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-message-converters)）。

- 自动注册 `MessageCodesResolver`（在 [本文档后面介绍](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-message-codes)）。

- 静态的 `index.html` 支持。

- 自定义 `Favicon` 支持（在 [文档后续介绍](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-favicon)）。

- 自动使用 `ConfigurableWebBindingInitializer` bean（在 [本文档后面介绍](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-web-binding-initializer)）。

如果您想保留 Spring Boot MVC 功能并想要添加其他 [MVC配置](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc)（拦截器，格式化程序，视图控制器和其他功能），则可以添加自己的类型 `@WebConfiguration` 的类，类型为 `WebMvcConfigurer`，但不包含 `@EnableWebMvc`。如果您希望提供 `RequestMappingHandlerMapping`，`RequestMappingHandlerAdapter` 或 `ExceptionHandlerExceptionResolver` 的自定义实例，则可以声明 `WebMvcRegistrationsAdapter` 实例以提供此类组件。

如果您想完全控制 Spring MVC，则可以添加带有 `@EnableWebMvc` 注解的自己的 `@Configuration`。

##### HttpMessageConverters

Spring MVC 使用 `HttpMessageConverter` 接口转换 HTTP 请求和响应。其中包含开箱即用的明智的默认设置。例如，可以将对象自动转换为 JSON（通过使用 Jackson 库）或 XML（通过使用 Jackson XML 扩展（如果可用）或通过使用 JAXB（如果 Jackson XML 扩展不可用））。默认情况下，字符串以 `UTF-8` 编码。

如果您需要添加或自定义转换器，则可以使用 Spring Boot 的 `HttpMessageConverters` 类，如以下清单所示：

```java
import org.springframework.boot.autoconfigure.http.HttpMessageConverters;
import org.springframework.context.annotation.*;
import org.springframework.http.converter.*;

@Configuration(proxyBeanMethods = false)
public class MyConfiguration {

    @Bean
    public HttpMessageConverters customConverters() {
        HttpMessageConverter<?> additional = ...
        HttpMessageConverter<?> another = ...
        return new HttpMessageConverters(additional, another);
    }

}
```

上下文中的 `HttpMessageConverter` bean 被添加到转换器列表中。你也可以通过相同的方法覆盖默认转换器。

##### 自定义 JSON 序列化和反序列化

如果您使用 Jackson 来序列化和反序列化 JSON 数据，则可能要编写自己的 `JsonSerializer` 和 `JsonDeserializer` 类。自定义序列化程序通常是 [通过模块向 Jackson 进行注册](https://github.com/FasterXML/jackson-docs/wiki/JacksonHowToCustomSerializers)，但是 Spring Boot 提供了替代的 `@JsonComponent` 注解，这使得直接注册 Spring Beans 更容易。

您可以直接在 `JsonSerializer`，`JsonDeserializer` 或 `KeyDeserializer` 实现上使用 `@JsonComponent` 注解。您还可以在包含序列化器/反序列化器作为内部类的类上使用它，如以下示例所示：

```java
import java.io.*;
import com.fasterxml.jackson.core.*;
import com.fasterxml.jackson.databind.*;
import org.springframework.boot.jackson.*;

@JsonComponent
public class Example {

    public static class Serializer extends JsonSerializer<SomeObject> {
        // ...
    }

    public static class Deserializer extends JsonDeserializer<SomeObject> {
        // ...
    }

}
```

 `ApplicationContext` 中的所有 `@JsonComponent` bean都会自动向 Jackson 进行注册。因为 `@JsonComponent` 是用 `@Component` 进行元注解的，所以通常的组件扫描规则适用。

Spring Boot 还提供了 [`JsonObjectSerializer`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jackson/JsonObjectSerializer.java) 和 [`JsonObjectDeserializer`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jackson/JsonObjectDeserializer.java)  基类，可在序列化对象时为标准 Jackson 版本提供有用的替代方法。有关详情参见 [`JsonObjectSerializer`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/jackson/JsonObjectSerializer.html) 和 [`JsonObjectDeserializer`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/jackson/JsonObjectDeserializer.html) 。

##### MessageCodesResolver

Spring MVC 有一个生成错误代码以从绑定错误中渲染错误消息的策略：`MessageCodesResolver`。如果您将 `spring.mvc.message-codes-resolver-format` 属性设置为 `PREFIX_ERROR_CODE` 或 `POSTFIX_ERROR_CODE`，Spring Boot 会为您创建一个该类型实例（请参阅 [`DefaultMessageCodesResolver.Format`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/validation/DefaultMessageCodesResolver.Format.html) 中的枚举）。

##### 静态内容

默认情况下，Spring Boot 从类路径中的目录 `/static`（或 `/public` 或 `/resources` 或 `/META-INF/resources`）或 `ServletContext` 的根目录中提供静态内容。它使用 Spring MVC 中的 `ResourceHttpRequestHandler`，因此您可以通过添加自己的 `WebMvcConfigurer` 并覆盖 `addResourceHandlers` 方法来修改该行为。

在独立的 Web 应用程序中，还启用了容器中的默认 servlet 并充当备用，如果 Spring 决定不处理它，则从 ServletContext 的根目录提供内容。在大多数情况下，这不会发生（除非您修改默认的 MVC 配置），因为 Spring 始终可以通过 `DispatcherServlet` 处理请求。

默认情况下，资源映射在 `/**` 上，但是您可以使用 `spring.mvc.static-path-pattern` 属性进行调整。例如，将所有资源重定位到 `/resources/**` 可以实现如下：

```properties
spring.mvc.static-path-pattern=/resources/**
```

您还可以使用 `spring.resources.static-locations` 属性来自定义静态资源位置（将默认值替换为目录位置列表）。根 Servlet 上下文路径 `\` 也会自动添加为资源位置。

除了前面提到的“标准”静态资源位置外，[Webjars内容](https://www.webjars.org/) 也有特殊情况。如果 jar 文件以 Webjars 格式打包，则所有 `/webjars/**` 中所有路径下的资源都将通过 jar 文件提供。

> 如果您的应用程序打包为 jar，则不要使用 `src/main/webapp` 目录。尽管此目录是一个通用标准，但它仅在 war 打包中有效，并且在生成 jar 时，大多数构建工具都将其忽略。

Spring Boot 还支持 Spring MVC 提供的高级资源处理功能，例如缓存清除静态资源或对 Webjars 使用版本无关的 URL。

要为 Webjar 使用与版本无关的 URL，请添加 `webjars-locator-core` 依赖项。然后声明您的 Webjar。以 jQuery 为例，添加 `/webjars/jquery/jquery.min.js` 会生成 `/webjars/jquery/x.y.z/jquery.min.js`，其中 `x.y.z` 是 Webjar 版本。

> 如果使用 JBoss，则需要声明 `webjars-locator-jboss-vfs` 依赖，而不是 `webjars-locator-core`。否则，所有 Webjar 都解析为 `404`。

要使用缓存清除，以下配置可为所有静态资源配置缓存清除解决方案，并在 URL 中有效地添加内容哈希，例如 `<link href="/css/spring-2a2d595e6ed9a0b24f027f2b63b134d6.css"/>` ：

```properties
spring.resources.chain.strategy.content.enabled=true
spring.resources.chain.strategy.content.paths=/**
```

> 通过为 Thymeleaf 和 FreeMarker 自动配置的 `ResourceUrlEncodingFilter`，可以在运行时在模板中重写资源链接。使用 JSP 时，您应该手动声明此过滤器。目前尚不自动支持其他模板引擎，但可以使用自定义模板宏/帮助器以及使用 [`ResourceUrlProvider`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/servlet/resource/ResourceUrlProvider.html)。

例如，当使用 JavaScript 模块加载器动态加载资源时，不能重命名文件。这就是为什么其他策略也受支持并且可以组合的原因。 “固定”策略在 URL 中添加静态版本字符串，而不更改文件名，如以下示例所示：

```properties
spring.resources.chain.strategy.content.enabled=true
spring.resources.chain.strategy.content.paths=/**
spring.resources.chain.strategy.fixed.enabled=true
spring.resources.chain.strategy.fixed.paths=/js/lib/
spring.resources.chain.strategy.fixed.version=v12
```

通过这种配置，位于 `"/js/lib/"` 下的 JavaScript 模块使用固定的版本控制策略（`/v12/js/lib/mymodule.js“`），而其他资源仍使用内容版本（`<link href="/css/spring-2a2d595e6ed9a0b24f027f2b63b134d6.css"/>`）。

参见 [`ResourceProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/ResourceProperties.java) 以获取更多受支持的选项。

> 本特性已经在相关专门 [blog post](https://spring.io/blog/2014/07/24/spring-framework-4-1-handling-static-web-resources) 和 Spring Framework 的 [reference documentation](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-config-static-resources) 中进行了详尽描述。

##### 欢迎页面

Spring Boot 支持静态和模板欢迎页面。它首先在配置的静态内容位置中查找 `index.html` 文件。如果没有找到，它会寻找一个 `index` 模板。如果找到任何一个，它将自动用作应用程序的欢迎页面。

##### 自定义网站图标

与其他静态资源一样，Spring Boot 在已配置的静态内容位置中查找 `favicon.ico`。如果存在这样的文件，它将自动用作应用程序的收藏夹图标。

##### 路径匹配和内容协商

Spring MVC 可以通过查看请求路径并将其匹配到应用程序中定义的映射（例如 Controller 方法上的 `@GetMapping` 注解），将传入的 HTTP 请求映射到处理程序。

Spring Boot 选择默认情况下禁用后缀模式匹配，这意味着像 `"GET /projects/spring-boot.json"` 这样的请求将不会与 `@GetMapping("/projects/spring-boot")` 映射相匹配。这被视为 [Spring MVC 应用程序的最佳实践](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-ann-requestmapping-suffix-pattern-match) 。 过去，此功能主要用于未发送正确的 `Accept` 请求标头的 HTTP 客户端。我们需要确保将正确的内容类型发送给客户端。如今，内容协商已变得更加可靠。

还有其他处理 HTTP 客户端的方法，这些客户端不能始终发送正确的 `Accept` 请求标头。除了使用后缀匹配，我们还可以使用查询参数来确保将诸如 `"GET /projects/spring-boot?format=json"` 之类的请求映射到 `@GetMapping("/projects/spring-boot")`：

```properties
spring.mvc.contentnegotiation.favor-parameter=true

# We can change the parameter name, which is "format" by default:
# spring.mvc.contentnegotiation.parameter-name=myparam

# We can also register additional file extensions/media types with:
spring.mvc.contentnegotiation.media-types.markdown=text/markdown
```

如果您了解了以上注意事项，但仍希望您的应用程序使用后缀模式匹配，则需要以下配置：

```properties
spring.mvc.contentnegotiation.favor-path-extension=true
spring.mvc.pathmatch.use-suffix-pattern=true
```

另外，与其打开所有后缀模式，不如只支持已注册的后缀模式，这更安全：

```properties
spring.mvc.contentnegotiation.favor-path-extension=true
spring.mvc.pathmatch.use-registered-suffix-pattern=true

# You can also register additional file extensions/media types with:
# spring.mvc.contentnegotiation.media-types.adoc=text/asciidoc
```

##### ConfigurableWebBindingInitializer

Spring MVC 使用 `WebBindingInitializer` 来为特定请求初始化 `WebDataBinder`。如果创建自己的 `ConfigurableWebBindingInitializer` `@Bean`，Spring Boot 会自动配置 Spring MVC 以使用它。

##### 模板引擎

除了 REST Web 服务之外，您还可以使用 Spring MVC 来提供动态 HTML 内容。Spring MVC 支持各种模板技术，包括 Thymeleaf，FreeMarker 和 JSP。同样，许多其他模板引擎包括他们自己的 Spring MVC 集成。

Spring Boot 包含对以下模板引擎的自动配置支持：

- [FreeMarker](https://freemarker.apache.org/docs/)
- [Groovy](http://docs.groovy-lang.org/docs/next/html/documentation/template-engines.html#_the_markuptemplateengine)
- [Thymeleaf](https://www.thymeleaf.org/)
- [Mustache](https://mustache.github.io/)

> 如果可能，应避免使用 JSP。当将它们与嵌入式 servlet 容器一起使用时，存在几个 [已知限制](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-jsp-limitations) 。

当您使用这些模板引擎之一进行默认配置时，您的模板会自动从 `src/main/resources/templates` 中获取。

> 根据您运行应用程序的方式，IntelliJ IDEA 对类路径的排序不同。与使用 Maven 或 Gradle 或从其打包的 jar 运行应用程序时相比，从 IDE 的主要方法运行应用程序的顺序会有所不同。这可能导致 Spring Boot 无法在类路径上找到模板。如果遇到此问题，可以在 IDE 中重新排序类路径，以首先放置模块的类和资源。另外，您可以配置模板前缀，以搜索类路径上的每个 `templates` 目录，如下所示：`classpath*:/templates/`。

##### 错误处理

默认情况下，Spring Boot 提供一个 `/error` 映射，以一种明智的方式处理所有错误，并且在 servlet 容器中被注册为“全局”错误页面。对于机器客户端，它将生成一个 JSON 响应，其中包含错误，HTTP 状态和异常消息的详细信息。对于浏览器客户端，有一个“whitelabel”错误视图以 HTML 格式呈现相同的数据（要对其进行自定义，请添加一个可解析为 `error` 的 `view`）。要完全替换默认行为，您可以实现 `ErrorController` 并注册该类型的 bean 定义，或者添加类型为 `ErrorAttributes` 的 bean 以使用现有机制但替换其内容。

> `BasicErrorController` 可用作自定义 `ErrorController` 的基类。如果您要为新的内容类型添加处理程序（默认是专门处理 `text/html` 并为其他所有内容提供后备功能），则此功能特别有用。为此，扩展 `BasicErrorController`，添加一个具有 `produces` 属性的 `@RequestMapping` 注解的公共方法，并创建一个新类型的 bean。

您还可以定义一个带有 `@ControllerAdvice` 注解的类，以自定义 JSON 文档以针对特定的控制器和/或异常类型返回，如以下示例所示：

```java
@ControllerAdvice(basePackageClasses = AcmeController.class)
public class AcmeControllerAdvice extends ResponseEntityExceptionHandler {

    @ExceptionHandler(YourException.class)
    @ResponseBody
    ResponseEntity<?> handleControllerException(HttpServletRequest request, Throwable ex) {
        HttpStatus status = getStatus(request);
        return new ResponseEntity<>(new CustomErrorType(status.value(), ex.getMessage()), status);
    }

    private HttpStatus getStatus(HttpServletRequest request) {
        Integer statusCode = (Integer) request.getAttribute("javax.servlet.error.status_code");
        if (statusCode == null) {
            return HttpStatus.INTERNAL_SERVER_ERROR;
        }
        return HttpStatus.valueOf(statusCode);
    }

}
```

在前面的示例中，如果在与 `AcmeController` 相同的包中定义的控制器抛出了 `YourException`，则使用 `CustomErrorType` POJO 的 JSON 表示形式而不是 `ErrorAttributes` 表示形式。

###### 自定义错误页面

如果要显示给定状态代码的自定义 HTML 错误页面，则可以将文件添加到 `/error` 文件夹中。错误页面可以是静态 HTML（即添加到任何静态资源文件夹下），也可以使用模板来构建。文件名应为确切的状态代码或系列掩码。

例如，要将 `404` 映射到静态 HTML 文件，您的文件夹结构如下：

```
src/
 +- main/
     +- java/
     |   + <source code>
     +- resources/
         +- public/
             +- error/
             |   +- 404.html
             +- <other public assets>
```

要使用 `FreeMarker` 模板映射所有 `5xx` 错误，您的文件夹结构如下：

```
src/
 +- main/
     +- java/
     |   + <source code>
     +- resources/
         +- templates/
             +- error/
             |   +- 5xx.ftlh
             +- <other templates>
```

对于更复杂的映射，还可以添加实现 `ErrorViewResolver` 接口的 bean，如以下示例所示：

```java
public class MyErrorViewResolver implements ErrorViewResolver {

    @Override
    public ModelAndView resolveErrorView(HttpServletRequest request,
            HttpStatus status, Map<String, Object> model) {
        // Use the request or status to optionally return a ModelAndView
        return ...
    }

}
```

你也可以使用通用的 Spring MVC 特性，比如 [`@ExceptionHandler` methods](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-exceptionhandlers) 和 [`@ControllerAdvice`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-ann-controller-advice)。`ErrorController` 就会处理任何未处理的异常。

###### 映射 Spring MVC 之外的错误页面

对于不使用 Spring MVC 的应用程序，可以使用 `ErrorPageRegistrar` 接口直接注册 `ErrorPages`。此抽象直接与基础嵌入式 servlet 容器一起使用，即使您没有 Spring MVC `DispatcherServlet` 也可以使用。

```java
@Bean
public ErrorPageRegistrar errorPageRegistrar(){
    return new MyErrorPageRegistrar();
}

// ...

private static class MyErrorPageRegistrar implements ErrorPageRegistrar {

    @Override
    public void registerErrorPages(ErrorPageRegistry registry) {
        registry.addErrorPages(new ErrorPage(HttpStatus.BAD_REQUEST, "/400"));
    }

}
```

> 如果您注册的 `ErrorPage` 具有最终由 `Filter` 处理的路径（这在某些非 Spring Web 框架，如 Jersey 和 Wicket，中很常见），则必须将 `Filter` 明确注册为 `ERROR` 调度程序，如以下示例所示：

```java
@Bean
public FilterRegistrationBean myFilter() {
    FilterRegistrationBean registration = new FilterRegistrationBean();
    registration.setFilter(new MyFilter());
    ...
    registration.setDispatcherTypes(EnumSet.allOf(DispatcherType.class));
    return registration;
}
```

请注意，默认的 `FilterFilterationBean` 不包含 `ERROR` 调度程序类型。

注意：当 Spring Boot 部署到 servlet 容器时，将使用其错误页面过滤器将具有错误状态的请求转发到适当的错误页面。如果尚未提交响应，则只能将请求转发到正确的错误页面。缺省情况下，WebSphere Application Server 8.0 及更高版本在成功完成 servlet 的服务方法后提交响应。您应该通过将 `com.ibm.ws.webcontainer.invokeFlushAfterService` 设置为 `false` 来禁用此行为。

##### Spring HATEOAS

如果您开发使用超媒体的 RESTful API，Spring Boot 将为 Spring HATEOAS 提供自动配置，该配置可与大多数应用程序很好地兼容。自动配置取代了使用 `@EnableHypermediaSupport` 的需要，并注册了许多 bean 来简化基于超媒体的应用程序的构建，其中包括一个 `LinkDiscoverers`（用于客户端支持）和一个 `ObjectMapper`，这些对象被配置为将响应正确地编组到所需的表示形式。`ObjectMapper` 是通过设置各种 `spring.jackson.*` 属性来定制的，如果存在的话，是通过一个 `Jackson2ObjectMapperBuilder` bean来定制的。

您可以使用 `@EnableHypermediaSupport` 来控制 Spring HATEOAS 的配置。注意，这样做会禁用前面描述的 `ObjectMapper` 自定义。

##### CORS 支持

[跨域资源共享](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing)（CORS）是已通过 [大多数浏览器](https://caniuse.com/#feat=cors) 实现的 [W3C规范](https://www.w3.org/TR/cors/) ，您可以灵活地指定授权哪种类型的跨域请求，而不是使用一些安全性和功能不强的方法，例如 IFRAME 或 JSONP。

从4.2版开始，Spring MVC [支持CORS](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-cors)。将 [controller method CORS configuration](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-cors-controller) 与 [`@CrossOrigin` ](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/bind/annotation/CrossOrigin.html) 注解用在 Spring Boot应用程序中不需要任何注解具体配置。[Global CORS配置](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web.html#mvc-cors-global) 可以通过注册 `WebMvcConfigurer` 来定义具有自定义 `addCorsMappings(CorsRegistry)` 方法的 bean，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
public class MyConfiguration {

    @Bean
    public WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(CorsRegistry registry) {
                registry.addMapping("/api/**");
            }
        };
    }
}
```

#### 4.7.2. Spring WebFlux 框架

Spring WebFlux 是 Spring Framework 5.0 中引入的新的响应式 Web 框架。与 Spring MVC 不同，它不需要 Servlet API，是完全异步且无阻塞的，并通过 [Reactor项目](https://projectreactor.io/) 实现 [Reactive Streams](https://www.reactive-streams.org/) 规范。

Spring WebFlux 有两种形式：功能性的和基于注解的。基于注解的模型非常类似于 Spring MVC 模型，如以下示例所示：

```java
@RestController
@RequestMapping("/users")
public class MyRestController {

    @GetMapping("/{user}")
    public Mono<User> getUser(@PathVariable Long user) {
        // ...
    }

    @GetMapping("/{user}/customers")
    public Flux<Customer> getUserCustomers(@PathVariable Long user) {
        // ...
    }

    @DeleteMapping("/{user}")
    public Mono<User> deleteUser(@PathVariable Long user) {
        // ...
    }

}
```

功能变体 “WebFlux.fn” 将路由配置与请求的实际处理分开，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
public class RoutingConfiguration {

    @Bean
    public RouterFunction<ServerResponse> monoRouterFunction(UserHandler userHandler) {
        return route(GET("/{user}").and(accept(APPLICATION_JSON)), userHandler::getUser)
                .andRoute(GET("/{user}/customers").and(accept(APPLICATION_JSON)), userHandler::getUserCustomers)
                .andRoute(DELETE("/{user}").and(accept(APPLICATION_JSON)), userHandler::deleteUser);
    }

}

@Component
public class UserHandler {

    public Mono<ServerResponse> getUser(ServerRequest request) {
        // ...
    }

    public Mono<ServerResponse> getUserCustomers(ServerRequest request) {
        // ...
    }

    public Mono<ServerResponse> deleteUser(ServerRequest request) {
        // ...
    }
}
```

WebFlux 是 Spring 框架的一部分，详细信息可在其 [参考文档](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web-reactive.html#webflux-fn) 中找到。

> 您可以根据需要定义尽可能多的 `RouterFunction` bean，以对路由器的定义进行模块化。如果需要应用优先级，可以对 Bean 进行排序。

首先，将 `spring-boot-starter-webflux` 模块添加到您的应用程序中。

> 在应用程序中添加 `spring-boot-starter-web` 和 `spring-boot-starter-webflux` 模块会导致 Spring Boot 自动配置 Spring MVC，而不是 WebFlux。之所以选择这种行为，是因为许多 Spring 开发人员在其 Spring MVC 应用程序中添加了 `spring-boot-starter-webflux` 以使用反应性 WebClient。您仍然可以通过将选定的应用程序类型设置为 `SpringApplication.setWebApplicationType(WebApplicationType.REACTIVE)` 来强制执行选择。

##### Spring WebFlux 自动配置

Spring Boot 为 Spring WebFlux 提供的自动配置可以很好地应用于大部分的应用。

自动配置在 Spring 默认基础上添加爱了以下特性：

- 为 `HttpMessageReader` 和 `HttpMessageWriter` 实例配置编解码器（在 [本文档后面](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-webflux-httpcodecs) 介绍）。
- 支持提供静态资源，包括对 WebJars 的支持（在 [本文档后面](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-spring-mvc-static-content) 介绍）。

如果您想保留 Spring Boot WebFlux 功能并想要添加其他 [WebFlux配置](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web-reactive.html#webflux-config)，您可以添加自己的类型为 `WebFluxConfigurer` 的 `@Configuration` 类，而不需要添加 `@EnableWebFlux` 。

如果您想完全控制 Spring WebFlux，则可以添加带有 `@EnableWebFlux` 注解的自己的 `@Configuration`。

##### 带有 HttpMessageReaders 和 HttpMessageWriters 的 HTTP 编解码器

Spring WebFlux 使用 `HttpMessageReader` 和 `HttpMessageWriter` 接口来转换 HTTP 请求和响应。通过查看类路径中可用的库，将它们配置为 `CodecConfigurer` 以具有合理的默认值。

Spring Boot 为编解码器 `spring.codec.*` 提供了专用的配置属性。它还通过使用 `CodecCustomizer` 实例来应用进一步的自定义。例如，将 `spring.jackson.*` 配置键应用于 Jackson 编解码器。

如果您需要添加或自定义编解码器，则可以创建自定义 `CodecCustomizer` 组件，如以下示例所示：

```java
import org.springframework.boot.web.codec.CodecCustomizer;

@Configuration(proxyBeanMethods = false)
public class MyConfiguration {

    @Bean
    public CodecCustomizer myCodecCustomizer() {
        return codecConfigurer -> {
            // ...
        };
    }

}
```

您还可以利用 [Boot的自定义JSON序列化器和反序列化器](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-json-components)。

 静态内容

默认情况下，Spring Boot 从类路径中的目录 `/static` (或者 `/public` 或者 `/resources` 或者 `/META-INF/resources`) 中提供静态内容。它使用 Spring WebFlux 中的 `ResourceWebHandler`，因此您可以通过添加自己的 `WebFluxConfigurer` 并覆盖 `addResourceHandlers` 方法来修改该行为。

默认情况下，资源映射在 `/**` 上，但是您可以通过设置 `spring.webflux.static-path-pattern` 属性来对其进行调整。例如，将所有资源重定位到 `/resources/**` 可以实现如下：

```properties
spring.webflux.static-path-pattern=/resources/**
```

您还可以通过使用 `spring.resources.static-locations` 自定义静态资源位置。这样做会将默认值替换为目录位置列表。如果这样做，默认的欢迎页面检测将切换到您的自定义位置。因此，如果启动时您的任何位置都有一个 `index.html`，则它是应用程序的主页。

除了前面列出的“标准”静态资源位置之外，[Webjars内容](https://www.webjars.org/) 也有特殊情况。如果 jar 文件以 Webjars 格式打包，则所有 `/webjars/**` 中具有路径的资源都将通过 jar 文件提供。

> Spring WebFlux 应用程序不严格依赖 Servlet API，因此不能将它们部署为 war 文件，也不使用 `src/main/webapp` 目录。

##### 模板引擎

除了 REST Web 服务之外，您还可以使用 Spring WebFlux 来提供动态 HTML 内容。Spring WebFlux 支持各种模板技术，包括 Thymeleaf，FreeMarker 和 Mustache。

Spring Boot 包含对以下模板引擎的自动配置支持：

- [FreeMarker](https://freemarker.apache.org/docs/)
- [Thymeleaf](https://www.thymeleaf.org/)
- [Mustache](https://mustache.github.io/)

当您使用这些模板引擎之一进行默认配置时，您的模板会自动从 `src/main/resources/templates` 中获取。

##### 错误处理

Spring Boot 提供了一个 WebExceptionHandler，以一种明智的方式处理所有错误。它在处理顺序中的位置紧靠 WebFlux 提供的处理程序之前，该处理程序被认为是最后一个。对于机器客户端，它将生成一个 JSON 响应，其中包含错误，HTTP 状态和异常消息的详细信息。对于浏览器客户端，有一个 "whitelabel” 错误处理程序，以 HTML 格式呈现相同的数据。您还可以提供自己的 HTML 模板来显示错误（请参见 [下一节](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-webflux-error-handling-custom-error-pages)）。

定制此功能的第一步通常涉及使用现有机制，但替换或增加错误内容。为此，您可以添加类型为 `ErrorAttributes` 的 bean。

要更改错误处理行为，可以实现 `ErrorWebExceptionHandler` 并注册该类型的 bean 定义。由于 `WebExceptionHandler` 的级别很低，因此 Spring Boot 还提供了一个便捷的 `AbstractErrorWebExceptionHandler`，可让您以 WebFlux 功能性的方式处理错误，如以下示例所示：

```java
public class CustomErrorWebExceptionHandler extends AbstractErrorWebExceptionHandler {

    // Define constructor here

    @Override
    protected RouterFunction<ServerResponse> getRoutingFunction(ErrorAttributes errorAttributes) {

        return RouterFunctions
                .route(aPredicate, aHandler)
                .andRoute(anotherPredicate, anotherHandler);
    }

}
```

为了获得更完整的视图，您还可以直接将 `DefaultErrorWebExceptionHandler` 子类化，并覆盖特定的方法。

###### 自定义错误页面

如果要显示给定状态代码的自定义 HTML 错误页面，则可以将文件添加到 `/error` 文件夹中。错误页面可以是静态 HTML（即添加到任何静态资源文件夹下），也可以使用模板构建。文件名应为确切的状态代码或系列掩码。

例如，要将 `404` 映射到静态 HTML 文件，您的文件夹结构如下：

```
src/
 +- main/
     +- java/
     |   + <source code>
     +- resources/
         +- public/
             +- error/
             |   +- 404.html
             +- <other public assets>
```

要使用 Moustache 模板映射所有 `5xx` 错误，您的文件夹结构如下：

```
src/
 +- main/
     +- java/
     |   + <source code>
     +- resources/
         +- templates/
             +- error/
             |   +- 5xx.mustache
             +- <other templates>
```

##### Web Filters

Spring WebFlux 提供了一个 `WebFilter` 接口，可以用来过滤 HTTP 请求-响应交互。在应用程序上下文中找到的 `WebFilter` bean将自动用于过滤每次交互。

当过滤器的顺序很重要时，它们可以实现 `Ordered` 或用 `@Order` 注解。Spring Boot 自动配置可能会为您配置 Web 过滤器。这样做时，将使用下表中显示的顺序：

| Web Filter                              | Order                            |
| :-------------------------------------- | :------------------------------- |
| `MetricsWebFilter`                      | `Ordered.HIGHEST_PRECEDENCE + 1` |
| `WebFilterChainProxy` (Spring Security) | `-100`                           |
| `HttpTraceWebFilter`                    | `Ordered.LOWEST_PRECEDENCE - 10` |

#### 4.7.3. JAX-RS 和 Jersey

如果您更喜欢 REST 端点的 JAX-RS 编程模型，则可以使用可用的实现之一来代替 Spring MVC。[Jersey](https://jersey.github.io/) 和 [Apache CXF](https://cxf.apache.org/) 开箱即用。CXF 要求您在应用程序上下文中将其 Servlet 或 Filter 作为 `@Bean` 注册。Jersey 提供了一些本地的 Spring 支持，因此我们在 Spring Boot 中还与启动程序一起为其提供了自动配置支持。

要开始使用 Jersey，请将 `spring-boot-starter-jersey` 作为依赖项，然后需要一个 `ResourceConfig` 类型的 `@Bean` 在其中注册所有端点，如以下示例所示：

```java
@Component
public class JerseyConfig extends ResourceConfig {

    public JerseyConfig() {
        register(Endpoint.class);
    }

}
```

> Jersey 对扫描可执行档案的支持非常有限。例如，它无法扫描 [完全可执行的jar文件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#deployment-install) 中的包内部的端点，或运行可执行 war 文件时在 `WEB-INF/classes` 中的端点。为了避免这种限制，不应该使用 `packages` 方法，并且应该使用 `register` 方法分别注册端点，如前面的示例所示。

对于更高级的定制，您还可以注册任意数量的实现 `ResourceConfigCustomizer` 的 bean。

所有注册的端点应该是带有 HTTP 资源注解的 `@Components`（`@GET` 和其他注解），如以下示例所示：

```java
@Component
@Path("/hello")
public class Endpoint {

    @GET
    public String message() {
        return "Hello";
    }

}
```

由于 `Endpoint` 是 Spring 的 `@Component`，它的生命周期是由 Spring 管理的，因此您可以使用 `@Autowired` 注解注入依赖项，并使用 `@Value` 注解注入外部配置。默认情况下，Jersey servlet 被注册并映射到 `/*`。您可以通过将 `@ApplicationPath` 添加到 `ResourceConfig` 中来更改映射。

默认情况下，Jersey 被设置为名为 `jerseyServletRegistration` 的 `ServletRegistrationBean` 类型的 `@Bean` 中的 Servlet。默认情况下，该 Servlet 的初始化是延迟的，但是您可以通过设置 `spring.jersey.servlet.load-on-startup` 来自定义该行为。您可以通过创建自己的同名 bean 来禁用或覆盖该 bean。您还可以通过设置 `spring.jersey.type=filter`（在这种情况下，要替换或覆盖的 `@Bean` 是 `jerseyFilterRegistration`）来使用过滤器而非 Servlet。过滤器具有一个 `@Order`，可以通过 `spring.jersey.filter.order` 进行设置。可以通过使用 `spring.jersey.init.*` 来指定属性映射，从而为 servlet 和过滤器注册都赋予 `init` 参数。

#### 4.7.4. 内置 Servlet 容器支持

Spring Boot 包含对 [Tomcat](https://tomcat.apache.org/)、[Jetty](https://www.eclipse.org/jetty/) 和 [Undertow](https://github.com/undertow-io/undertow) 等多种内置 Servlet 服务器的支持。大多数开发者使用合适的启动器来获取完整配置的实例。默认情况下，内置的服务器在端口 `8080` 上监听 HTTP 请求。

##### Servlets, Filters, 和 listeners

使用内置 Servlet 容器时，您可以通过使用 Spring Bean 或扫描 Servlet 组件来注册 Servlet 规范中的 Servlet、过滤器和所有侦听器（例如 `HttpSessionListener`）。

###### 将 Servlets, Filters, 和 Listeners 注册为 Spring Beans

任何作为 Spring bean 的 Servlet，Filter 或 Servlet  `*Listener` 实例都向嵌入式容器注册。如果您想在配置过程中引用来自 `application.properties` 的值，这将特别方便。

默认情况下，如果上下文仅包含单个 Servlet，则将其映射到 `/`。对于多个 servlet bean，bean 名称用作路径前缀。过滤器映射到 `/*`。

如果基于约定的映射不够灵活，则可以使用 `ServletRegistrationBean`，`FilterRegistrationBean` 和 `ServletListenerRegistrationBean` 类进行完全控制。

通常情况下，过滤器 bean 处于无序状态是安全的。如果需要特定的顺序，则应使用 `@Order` 来注解 `Filter` 或使其实现 `Ordered`。您不能通过使用 `@Order` 注解 bean 方法的方法来配置 `Filter` 的顺序。如果您不能将 `Filter` 类更改为添加 `@Order` 或实现 `Ordered`，则必须为 `Filter` 定义 `FilterRegistrationBean` 并使用 `setOrder(int)` 方法设置注册 bean 的顺序。避免配置一个在 `Ordered.HIGHEST_PRECEDENCE` 上读取请求正文的过滤器，因为它可能与应用程序的字符编码配置不符。如果 Servlet 过滤器包装了请求，则应使用小于或等于 `OrderedFilter.REQUEST_WRAPPER_FILTER_MAX_ORDER` 的顺序来配置它。

> 要查看应用程序中每个 `Filter` 的顺序，请为 `web` [logging group](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-custom-log-groups)（`logging.level.web=debug`）启用 `debug` 级别日志。然后，将在启动时记录已注册过滤器的详细信息，包括其顺序和 URL 模式。

> 注册 `Filter` bean 时要小心，因为它们是在应用程序生命周期中很早就初始化的。如果您需要注册与其他 bean 交互的 `Filter`，请考虑使用 [`DelegatingFilterProxyRegistrationBean`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/web/servlet/DelegatingFilterProxyRegistrationBean.html) 。

##### Servlet 上下文初始化

内置 Servlet 容器不会直接执行 Servlet 3.0+ 的 `javax.servlet.ServletContainerInitializer` 接口或 Spring 的 `org.springframework.web.WebApplicationInitializer` 接口。这是一个有意的设计决定，旨在降低在 war 中运行的第三方库可能破坏 Spring Boot 应用程序的风险。

如果需要在 Spring Boot 应用程序中执行 servlet 上下文初始化，则应注册一个实现 `org.springframework.boot.web.servlet.ServletContextInitializer` 接口的 bean。单一的 `onStartup` 方法提供对 `ServletContext` 的访问，并且在必要时可以轻松地用作现有 `WebApplicationInitializer` 的适配器。

###### 扫描 Servlets, Filters, 和 listeners

当使用内置容器时，可以通过使用 `@ServletComponentScan` 来启用自动注册带有 `@WebServlet`，`@WebFilter` 和 `@WebListener` 的类。

> `@ServletComponentScan` 在独立容器中无效，在该容器中使用了容器的内置发现机制。

##### ServletWebServerApplicationContext

在后台，Spring Boot 使用另一种类型的 `ApplicationContext` 来支持内置 servlet 容器。`ServletWebServerApplicationContext` 是 `WebApplicationContext` 的一种特殊类型，它通过搜索单个 `ServletWebServerFactory` bean来进行自我引导。通常，已经自动配置了 `TomcatServletWebServerFactory`，`JettyServletWebServerFactory` 或 `UndertowServletWebServerFactory`。

> 通常，您不需要了解这些实现类。大多数应用程序都是自动配置的，并且代表您创建了相应的 `ApplicationContext` 和 `ServletWebServerFactory`。

##### 自定义内置 Servlet 容器

可以通过使用 Spring 的 `Environment` 属性来配置常见的 servlet 容器设置。通常，您将在 `application.properties` 文件中定义属性。

常用服务器设置包括：

- 网络设置：侦听传入HTTP请求的端口（`server.port`），绑定到 `server.address` 的接口地址，等等。
- 会话设置：会话是否是持久性的（`server.servlet.session.persistent`），会话超时（`server.servlet.session.timeout`），会话数据的位置（`server.servlet.session.store-dir`）和会话 Cookie 配置（`server.servlet.session.cookie.*`）。
- 错误管理：错误页面位置 (`server.error.path`) 等等。
- [SSL](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-configure-ssl)
- [HTTP 压缩](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#how-to-enable-http-response-compression)

Spring Boot 尝试尽可能多地公开通用设置，但这并不总是可能的。在这种情况下，专用名称空间可提供服务器特定的自定义设置（请参见 `server.tomcat` 和 `server.undertow`）。例如，可以使用内置 servlet 容器特定功能配置 [访问日志](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-configure-accesslogs)。

> 参考 [`ServerProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/web/ServerProperties.java) 类以获得完整列表。

###### 编程式自定义

如果您需要以编程方式配置内置 servlet 容器，则可以注册一个实现 `WebServerFactoryCustomizer` 接口的 Spring bean。`WebServerFactoryCustomizer` 提供对 `ConfigurableServletWebServerFactory` 的访问，其中包括许多自定义设置方法。以下示例显示以编程方式设置端口：

```java
import org.springframework.boot.web.server.WebServerFactoryCustomizer;
import org.springframework.boot.web.servlet.server.ConfigurableServletWebServerFactory;
import org.springframework.stereotype.Component;

@Component
public class CustomizationBean implements WebServerFactoryCustomizer<ConfigurableServletWebServerFactory> {

    @Override
    public void customize(ConfigurableServletWebServerFactory server) {
        server.setPort(9000);
    }

}
```

> `TomcatServletWebServerFactory`，`JettyServletWebServerFactory` 和 `UndertowServletWebServerFactory` 是 `ConfigurableServletWebServerFactory` 的专用变体，分别具有针对 Tomcat，Jetty 和 Undertow 的其他自定义设置方法。

###### 直接自定义 ConfigurableServletWebServerFactory

如果上述自定义技术太有限，则可以自己注册 `TomcatServletWebServerFactory`，`JettyServletWebServerFactory` 或 `UndertowServletWebServerFactory` bean。

```java
@Bean
public ConfigurableServletWebServerFactory webServerFactory() {
    TomcatServletWebServerFactory factory = new TomcatServletWebServerFactory();
    factory.setPort(9000);
    factory.setSessionTimeout(10, TimeUnit.MINUTES);
    factory.addErrorPages(new ErrorPage(HttpStatus.NOT_FOUND, "/notfound.html"));
    return factory;
}
```

提供了许多配置选项的设置器。如果您需要做一些更奇特的操作，还提供了几种受保护的方法“挂钩”。请参阅 [源代码文档](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/web/servlet/server/ConfigurableServletWebServerFactory.html) 获取更多细节。

##### JSP 局限性

运行使用内置 servlet 容器（并打包为可执行档案）的 Spring Boot 应用程序时，JSP 支持存在一些限制。

- 使用 Jetty 和 Tomcat，如果使用 war 包装，它应该可以工作。可执行的 war 与 `java -jar` 一起启动时将起作用，并且也可部署到任何标准容器中。使用可执行 jar 时，不支持 JSP。

- Undertow 不支持 JSP。

- 创建自定义 `error.jsp` 页面不会覆盖 [错误处理](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-error-handling) 的默认视图。应使用 [自定义错误页面](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-error-handling-custom-error-pages) 代替。

#### 4.7.5. 内置反应式服务器支持

Spring Boot 包含对以下内置反应式 Web 服务器的支持：Reactor Netty，Tomcat，Jetty 和 Undertow。大多数开发人员使用适当的“启动器”来获取完全配置的实例。默认情况下，内置服务器在端口 8080 上侦听 HTTP 请求。

#### 4.7.6. 反应式服务器资源配置

当自动配置 Reactor Netty 或 Jetty 服务器时，Spring Boot 将创建特定的 bean，这些 bean 将向服务器实例提供 HTTP 资源：`ReactorResourceFactory` 或 `JettyResourceFactory`。

默认情况下，这些资源还将与 Reactor Netty 和 Jetty 客户端共享，以实现最佳性能，前提是：

- 服务器和客户端使用相同的技术

- 使用 Spring Boot 自动配置的 `WebClient.Builder` bean构建客户端实例

开发者可以通过提供自定义的 `ReactorResourceFactory` 或 `JettyResourceFactory` bean 来覆盖 Jetty 和 Reactor Netty 的资源配置-这将同时应用于客户端和服务器。

您可以在 [WebClient运行时部分](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-webclient-runtime) 中了解有关客户端资源配置的更多信息。

### 4.8. RSocket

[RSocket](https://rsocket.io/) 是一个用于字节流传输的二进制协议。它通过通过单个连接传递的异步消息来启用对称交互模型。

Spring 框架的 `spring-messaging` 模块在客户端和服务器端都支持 RSocket 请求者和响应者。有关更多信息，请参见 Spring Framework 参考文档的 [RSocket部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web-reactive.html#rsocket-spring) 详细信息，包括 RSocket 协议概述。

#### 4.8.1. RSocket 策略自动配置

Spring Boot 自动配置一个 `RSocketStrategies` bean，该 bean 提供了编码和解码 RSocket 有效负载所需的所有基础结构。默认情况下，自动配置将尝试（按顺序）配置以下内容：

1. [CBOR](https://cbor.io/) 使用 Jackson 编码解码
2. JSON 使用 Jackson 编码解码

`spring-boot-starter-rsocket` 启动器提供了两种依赖关系。查阅 [Jackson支持部分](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-json-jackson) 以了解有关自定义可能性的更多信息 。

开发人员可以通过创建实现 `RSocketStrategiesCustomizer` 接口的 bean 来自定义 `RSocketStrategies` 组件。注意，它们的 `@Order` 很重要，因为它确定编解码器的顺序。

#### 4.8.2. RSocket 服务器自动配置

Spring Boot 提供了 RSocket 服务器自动配置。所需的依赖关系由 `spring-boot-starter-rsocket` 提供。

Spring Boot 允许从 WebFlux 服务器通过 WebSocket 公开 RSocket，或支持独立的 RSocket 服务器。这取决于应用程序的类型及其配置。

对于 WebFlux 应用程序（即 `WebApplicationType.REACTIVE` 类型的应用程序），只有在以下属性匹配的情况下，RSocket 服务器才会插入 Web 服务器：

```properties
spring.rsocket.server.mapping-path=/rsocket # a mapping path is defined
spring.rsocket.server.transport=websocket # websocket is chosen as a transport
#spring.rsocket.server.port= # no port is defined
```

> 由于 RSocket 本身是使用该库构建的，因此只有 Reactor Netty 支持将 RSocket 插入 Web 服务器。

另外，RSocket TCP 或 Websocket 服务器也可以作为独立的内置服务器启动。除了依赖性要求之外，唯一需要的配置是为该服务器定义端口：

```properties
spring.rsocket.server.port=9898 # the only required configuration
spring.rsocket.server.transport=tcp # you're free to configure other properties
```

#### 4.8.3. Spring Messaging RSocket 支持

Spring Boot 将为 RSocket 自动配置 Spring Messaging 基础结构。

这意味着 Spring Boot 将创建一个 `RSocketMessageHandler` bean，该 bean 将处理对您的应用程序的 RSocket 请求。

#### 4.8.4. 使用 `RSocketRequester` 调用 RSocket 服务

一旦在服务器和客户端之间建立了 `RSocket` 通道，任何一方都可以向对方发送或接收请求。

作为服务器，您可以在 RSocket `@Controller` 的任何处理程序方法上注入 `RSocketRequester` 实例。作为客户端，您需要首先配置和建立 RSocket 连接。在这种情况下，Spring Boot 使用预期的编解码器自动配置 `RSocketRequester.Builder`。

`RSocketRequester.Builder` 实例是一个原型 bean，这意味着每个注入点将为您提供一个新实例。这样做是有目的的，因为此构建器是有状态的，因此您不应使用同一实例创建具有不同设置的请求者。

下面的代码展示了一个典型的例子：

```java
@Service
public class MyService {

    private final RSocketRequester rsocketRequester;

    public MyService(RSocketRequester.Builder rsocketRequesterBuilder) {
        this.rsocketRequester = rsocketRequesterBuilder
                .connectTcp("example.org", 9898).block();
    }

    public Mono<User> someRSocketCall(String name) {
        return this.requester.route("user").data(name)
                .retrieveMono(User.class);
    }

}
```

### 4.9. 安全

如果 [Spring Security](https://spring.io/projects/spring-security) 位于类路径中，则默认情况下 Web 应用程序是安全的。Spring Boot 依靠 Spring Security 的内容协商策略来确定是使用 `httpBasic` 还是 `formLogin`。要将方法级安全性添加到 Web 应用程序，您还可以使用所需的设置添加 `@EnableGlobalMethodSecurity`。可以在 [Spring Security参考指南](https://docs.spring.io/spring-security/site/docs/5.2.1.RELEASE/reference/htmlsingle/#jc-method) 中找到更多信息。

默认的 `UserDetailsService` 只有一个用户。用户名为 `user`，密码为随机密码，并在应用程序启动时以 `INFO` 级别显示，如下例所示：

```
Using generated security password: 78fa095d-3f4c-48b1-ad50-e24c31d5cf35
```

> 如果您微调日志记录配置，请确保将 `org.springframework.boot.autoconfigure.security` 类别设置为记录 `INFO` 级消息。否则，不会打印默认密码。

您可以通过提供 `spring.security.user.name` 和 `spring.security.user.password` 来更改用户名和密码。

默认情况下，您在 Web 应用程序中获得的基本功能是：

- 具有内存存储区的 `UserDetailsService`（如果是 WebFlux 应用程序，则为 `ReactiveUserDetailsService`）Bean 和具有生成的密码的单个用户（请参阅 [`SecurityProperties.User`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/autoconfigure/security/SecurityProperties.User.html) 以获取用户的属性）。

- 整个应用程序的基于表单的登录或 HTTP 基本安全性（取决于请求中的 `Accept` 标头）（如果执行器位于类路径上，则包括执行器端点）。

- 用于发布身份验证事件的 `DefaultAuthenticationEventPublisher`。

您可以通过添加一个bean来提供一个不同的`AuthenticationEventPublisher`。

#### 4.9.1. MVC 安全

默认的安全配置在 `SecurityAutoConfiguration` 和 `UserDetailsServiceAutoConfiguration` 中实现。`SecuritySecurityConfiguration` 导入 `SpringBootWebSecurityConfiguration` 来实现 Web 安全，而 `UserDetailsServiceAutoConfiguration` 则配置身份验证，这在非 Web 应用程序中也很重要。要完全关闭默认的 Web 应用程序安全性配置或合并多个 Spring Security 组件（例如 OAuth 2 客户端和资源服务器），请添加类型为 `WebSecurityConfigurerAdapter` 的 bean（这样做不会禁用 `UserDetailsService` 配置或 `Actuator` 的安全性）。

要也关闭 `UserDetailsService` 配置，可以添加 `UserDetailsService`，`AuthenticationProvider` 或 `AuthenticationManager` 类型的 Bean。

可以通过添加自定义 `WebSecurityConfigurerAdapter` 来覆盖访问规则。Spring Boot 提供了方便的方法，可用于覆盖执行器端点和静态资源的访问规则。`EndpointRequest` 可以用来创建基于 `management.endpoints.web.base-path` 属性的 `RequestMatcher`。`PathRequest` 可以用来为常用位置的资源创建一个 `RequestMatcher`。

#### 4.9.2. WebFlux 安全

与 Spring MVC 应用程序类似，您可以通过添加 `spring-boot-starter-security` 依赖性来保护 WebFlux 应用程序。默认的安全配置在 `ReactiveSecurityAutoConfiguration` 和 `UserDetailsServiceAutoConfiguration` 中实现。`ReactiveSecurityAutoConfiguration` 导入 `WebFluxSecurityConfiguration` 以实现网络安全，而 `UserDetailsServiceAutoConfiguration` 则配置身份验证，这也与非 Web 应用程序相关。要完全关闭默认的 Web 应用程序安全性配置，您可以添加类型为 `WebFilterChainProxy` 的 bean（这样做不会禁用 `UserDetailsService` 配置或执行器的安全性）。

要也关闭 `UserDetailsService` 配置，可以添加 `ReactiveUserDetailsService` 或 `ReactiveAuthenticationManager` 类型的 Bean。

可以通过添加自定义 `SecurityWebFilterChain` bean来配置访问规则以及使用多个 Spring Security 组件（例如 OAuth 2 Client 和 Resource Server）。Spring Boot 提供了方便的方法，可用于覆盖执行器端点和静态资源的访问规则。`EndpointRequest` 可以用于创建基于 `management.endpoints.web.base-path` 属性的 `ServerWebExchangeMatcher`。

`PathRequest` 可用于为常用位置的资源创建 `ServerWebExchangeMatcher`。

例如，您可以通过添加以下内容来自定义安全配置：

```java
@Bean
public SecurityWebFilterChain springSecurityFilterChain(ServerHttpSecurity http) {
    return http
        .authorizeExchange()
            .matchers(PathRequest.toStaticResources().atCommonLocations()).permitAll()
            .pathMatchers("/foo", "/bar")
                .authenticated().and()
            .formLogin().and()
        .build();
}
```

#### 4.9.3. OAuth2

[OAuth2](https://oauth.net/2/) 是一个 Spring 支持的被广泛应用的身份认证框架。

##### 客户端

如果您在类路径中具有 `spring-security-oauth2-client`，则可以利用一些自动配置功能来轻松设置 OAuth2/Open ID Connect 客户端。该配置利用了 `OAuth2ClientProperties` 下的属性。相同的属性适用于 servlet 和反应式应用程序。

您可以在 `spring.security.oauth2.client` 前缀下注册多个 OAuth2 客户端和提供者，如以下示例所示：

```properties
spring.security.oauth2.client.registration.my-client-1.client-id=abcd
spring.security.oauth2.client.registration.my-client-1.client-secret=password
spring.security.oauth2.client.registration.my-client-1.client-name=Client for user scope
spring.security.oauth2.client.registration.my-client-1.provider=my-oauth-provider
spring.security.oauth2.client.registration.my-client-1.scope=user
spring.security.oauth2.client.registration.my-client-1.redirect-uri=https://my-redirect-uri.com
spring.security.oauth2.client.registration.my-client-1.client-authentication-method=basic
spring.security.oauth2.client.registration.my-client-1.authorization-grant-type=authorization_code

spring.security.oauth2.client.registration.my-client-2.client-id=abcd
spring.security.oauth2.client.registration.my-client-2.client-secret=password
spring.security.oauth2.client.registration.my-client-2.client-name=Client for email scope
spring.security.oauth2.client.registration.my-client-2.provider=my-oauth-provider
spring.security.oauth2.client.registration.my-client-2.scope=email
spring.security.oauth2.client.registration.my-client-2.redirect-uri=https://my-redirect-uri.com
spring.security.oauth2.client.registration.my-client-2.client-authentication-method=basic
spring.security.oauth2.client.registration.my-client-2.authorization-grant-type=authorization_code

spring.security.oauth2.client.provider.my-oauth-provider.authorization-uri=https://my-auth-server/oauth/authorize
spring.security.oauth2.client.provider.my-oauth-provider.token-uri=https://my-auth-server/oauth/token
spring.security.oauth2.client.provider.my-oauth-provider.user-info-uri=https://my-auth-server/userinfo
spring.security.oauth2.client.provider.my-oauth-provider.user-info-authentication-method=header
spring.security.oauth2.client.provider.my-oauth-provider.jwk-set-uri=https://my-auth-server/token_keys
spring.security.oauth2.client.provider.my-oauth-provider.user-name-attribute=name
```

对于支持 [OpenID Connect发现](https://openid.net/specs/openid-connect-discovery-1_0.html) 的 OpenID Connect 提供程序，可以进一步简化配置。提供者需要配置有一个 `issuer-uri`，它是它声明为其发行者标识符的 URI。例如，如果提供的 `issuer-uri` 是 "https://example.com"，则将向“https://example.com/.well-known/openid-configuration”发送 `OpenID Provider Configuration Request` 。预期结果将是 `OpenID Provider Configuration Response`。以下示例显示了如何使用 `issuer-uri` 配置 OpenID Connect 提供程序：

```properties
spring.security.oauth2.client.provider.oidc-provider.issuer-uri=https://dev-123456.oktapreview.com/oauth2/default/
```

默认情况下，Spring Security 的 `OAuth2LoginAuthenticationFilter` 仅处理与 `/login/oauth2/code/*` 匹配的 URL。如果您想自定义 `redirect-uri` 以使用其他模式，则需要提供配置以处理该自定义模式。例如，对于 servlet 应用程序，您可以添加自己的类似于以下内容的 `WebSecurityConfigurerAdapter`：

```java
public class OAuth2LoginSecurityConfig extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http
            .authorizeRequests()
                .anyRequest().authenticated()
                .and()
            .oauth2Login()
                .redirectionEndpoint()
                    .baseUri("/custom-callback");
    }
}
```

###### 常见提供者的 OAuth2 客户端注册

对于常见的 OAuth2 和 OpenID 提供程序，包括 Google，Github，Facebook 和 Okta，我们提供了一组提供程序默认值（分别为 `google`，`github`，`facebook` 和 `Okta`）。

如果不需要自定义这些提供程序，则可以将 `provider` 属性设置为需要推断默认值的属性。另外，如果用于客户端注册的 key 与默认支持的提供程序匹配，则 Spring Boot 也会进行推断。

换句话说，以下示例中的两个配置都使用 Google 提供程序：

```properties
spring.security.oauth2.client.registration.my-client.client-id=abcd
spring.security.oauth2.client.registration.my-client.client-secret=password
spring.security.oauth2.client.registration.my-client.provider=google

spring.security.oauth2.client.registration.google.client-id=abcd
spring.security.oauth2.client.registration.google.client-secret=password
```

##### 资源服务器

如果您的类路径上有 `spring-security-oauth2-resource-server`，则 Spring Boot 可以设置 OAuth2 资源服务器。对于 JWT 配置，需要指定 JWK 设置 URI 或 OIDC 颁发者 URI，如以下示例所示：

```properties
spring.security.oauth2.resourceserver.jwt.jwk-set-uri=https://example.com/oauth2/default/v1/keys
spring.security.oauth2.resourceserver.jwt.issuer-uri=https://dev-123456.oktapreview.com/oauth2/default/
```

> 如果授权服务器不支持 JWK 设置 URI，则可以使用用于验证 JWT 签名的公共密钥来配置资源服务器。这可以通过使用 `spring.security.oauth2.resourceserver.jwt.public-key-location` 属性来完成，该属性值需要指向包含 PEM 编码的 x509 格式的公钥的文件。

相同的属性适用于 servlet 和反应式应用程序。

另外，您可以为 servlet 应用程序定义自己的 `JwtDecoder` bean或为反应性应用程序定义 `ReactiveJwtDecoder`。

如果使用不透明令牌而不是 JWT，则可以配置以下属性以通过自省来验证令牌：

```properties
spring.security.oauth2.resourceserver.opaquetoken.introspection-uri=https://example.com/check-token
spring.security.oauth2.resourceserver.opaquetoken.client-id=my-client-id
spring.security.oauth2.resourceserver.opaquetoken.client-secret=my-client-secret
```

同样，相同的属性适用于 servlet 和反应式应用程序。

另外，您可以为 servlet 应用程序定义自己的 `OpaqueTokenIntrospector` bean或为响应应用程序定义 `ReactiveOpaqueTokenIntrospector`。

##### 认证服务器

当前，Spring Security 不提供对实现 OAuth 2.0 授权服务器的支持。但是，[Spring Security OAuth](https://spring.io/projects/spring-security-oauth) 项目提供了此功能，该项目最终将被 Spring Security 完全取代。在此之前，您可以使用 `spring-security-oauth2-autoconfigure` 模块轻松设置 OAuth 2.0 授权服务器；有关说明，请参阅其 [文档](https://docs.spring.io/spring-security-oauth2-boot) 。

#### 4.9.4. SAML 2.0

##### Relying Party

如果您在类路径中具有 `spring-security-saml2-service-provider`，则可以利用一些自动配置功能来轻松设置 SAML 2.0 Relying Party。该配置利用了 `Saml2RelyingPartyProperties` 下的属性。

Relying Party 注册代表身份提供商 IDP 和服务提供商 SP 之间的配对配置。您可以在 `spring.security.saml2.relyingparty` 前缀下注册多个 Relying Party，如以下示例所示：

```properties
spring.security.saml2.relyingparty.registration.my-relying-party1.signing.credentials[0].private-key-location=path-to-private-key
spring.security.saml2.relyingparty.registration.my-relying-party1.signing.credentials[0].certificate-location=path-to-certificate
spring.security.saml2.relyingparty.registration.my-relying-party1.identityprovider.verification.credentials[0].certificate-location=path-to-verification-cert
spring.security.saml2.relyingparty.registration.my-relying-party1.identityprovider.entity-id=remote-idp-entity-id1
spring.security.saml2.relyingparty.registration.my-relying-party1.identityprovider.sso-url=https://remoteidp1.sso.url

spring.security.saml2.relyingparty.registration.my-relying-party2.signing.credentials[0].private-key-location=path-to-private-key
spring.security.saml2.relyingparty.registration.my-relying-party2.signing.credentials[0].certificate-location=path-to-certificate
spring.security.saml2.relyingparty.registration.my-relying-party2.identityprovider.verification.credentials[0].certificate-location=path-to-other-verification-cert
spring.security.saml2.relyingparty.registration.my-relying-party2.identityprovider.entity-id=remote-idp-entity-id2
spring.security.saml2.relyingparty.registration.my-relying-party2.identityprovider.sso-url=https://remoteidp2.sso.url
```

#### 4.9.5. Actuator 安全

为了安全起见，默认情况下禁用除 `/health` 和 `/info` 外的所有执行器。`management.endpoints.web.exposure.include` 属性可用于启用执行器。

如果 Spring Security 在类路径上，并且不存在其他 `WebSecurityConfigurerAdapter`，则通过 Spring Boot 自动配置保护除 `/health` 和 `/info` 以外的所有执行器。如果您定义了一个自定义的 `WebSecurityConfigurerAdapter`，Spring Boot 的自动配置将退出，您将完全控制执行器访问规则。

> 在设置 `management.endpoints.web.exposure.include` 之前，请确保裸露的执行器不包含敏感信息和/或通过将它们放置在防火墙后面或通过诸如 Spring Security 之类的东西进行保护。

##### 跨站点请求伪造保护

由于 Spring Boot 依赖于 Spring Security 的默认设置，因此 CSRF 保护默认情况下处于启用状态。这意味着，在使用默认安全配置时，需要 `POST`（关闭和记录器端点），`PUT` 或 `DELETE` 的执行器端点将收到 `403` 禁止错误。

> 我们建议仅在创建非浏览器客户端使用的服务时完全禁用 CSRF 保护。

关于 CSRF 保护的其他信息可以在 [Spring Security参考指南](https://docs.spring.io/spring-security/site/docs/5.2.1.RELEASE/reference/htmlsingle/#csrf) 中找到。

### 4.10. 使用 SQL 数据库

 [Spring Framework](https://spring.io/projects/spring-framework) 提供了使用 SQL 数据库的丰富支持，从使用 `JdbcTemplate` 的直接 JDBC 访问到诸如 Hibernate 的完善的 "对象关系映射" 技术。 [Spring Data](https://spring.io/projects/spring-data) 提供了另一个级别的功能：直接从接口创建 `Repository` 实现，并使用约定从你的方法名称生成查询。

#### 4.10.1. 配置数据库

Java 的 `javax.sql.DataSource` 接口提供使用数据库连接的标准方法。传统上，`DataSource` 使用一个 `URL` 和一些凭证来建立数据库连接。

> 参考 [the “How-to” section](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-configure-a-datasource) 了解更多高级示例，其中一些是关于如何完全控制数据库配置。

##### 内置数据库支持

使用内存内置数据库来开发应用程序通常很方便。显然，内存数据库不提供持久存储。您需要在应用程序启动时填充数据库，并准备在应用程序结束时丢弃数据。

> “How-to” 章节包含 [section on how to initialize a database](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-database-initialization) 。

Spring Boot 可以自动配置内置 [H2](https://www.h2database.com/)，[HSQL](http://hsqldb.org/) 和 [Derby](https://db.apache.org/derby/) 数据库。您无需提供任何连接 URL。您只需要包含要使用的内置数据库的构建依赖项即可。

> 如果您在测试中使用此功能，则可能会注意到，整个测试套件将重复使用同一数据库，而不管您使用的应用程序上下文有多少。如果要确保每个上下文都有一个单独的内置数据库，则应将 `spring.datasource.generate-unique-name` 设置为 `true`。

比如，典型的 POM 依赖应该是：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
<dependency>
    <groupId>org.hsqldb</groupId>
    <artifactId>hsqldb</artifactId>
    <scope>runtime</scope>
</dependency>
```

> 您需要依赖于 `spring-jdbc` 才能自动配置内置数据库。在这个例子中，它是通过 `spring-boot-starter-data-jpa` 传递的。

> 如果出于某种原因确实为内置数据库配置了连接 URL，请务必确保禁用了数据库的自动关闭功能。如果您使用的是 H2，则应使用 `DB_CLOSE_ON_EXIT=FALSE`。如果使用 HSQLDB，则应确保不使用 `shutdown=true`。通过禁用数据库的自动关闭功能，Spring Boot 可以控制何时关闭数据库，从而确保一旦不再需要访问数据库时就可以进行自动关闭。

##### 连接到生产数据库

生产数据库的连接也可以通过使用 `DataSource` 池来自动配置。Spring Boot 使用以下算法来选择特定的实现：

1. 我们更喜欢 [HikariCP](https://github.com/brettwooldridge/HikariCP) 的性能和并发性。如果有 HikariCP，我们总是选择它。

2. 否则，如果 Tomcat 池 `DataSource` 可用，我们将使用它。

3. 如果 HikariCP 和 Tomcat 池数据源均不可用，而 [Commons DBCP2](https://commons.apache.org/proper/commons-dbcp/) 可用，我们将使用它。

如果您使用 `spring-boot-starter-jdbc` 或 `spring-boot-starter-data-jpa` `starters`，则会自动获得对  `HikariCP` 的依赖。

> 您可以通过设置 `spring.datasource.type` 属性来完全绕过该算法，并指定要使用的连接池。如果您在 Tomcat 容器中运行应用程序，这一点尤其重要，因为默认情况下会提供 `tomcat-jdbc`。

> 额外连接池始终可以手动配置。如果定义自己的 `DataSource` bean，则不会进行自动配置。

数据源的配置由 `spring.datasource.*` 中的外部配置属性控制。例如，您可以在 `application.properties` 中声明以下部分：

```properties
spring.datasource.url=jdbc:mysql://localhost/test
spring.datasource.username=dbuser
spring.datasource.password=dbpass
spring.datasource.driver-class-name=com.mysql.jdbc.Driver
```

> 您至少应通过设置 `spring.datasource.url` 属性来指定 URL。否则，Spring Boot 会尝试自动配置内置数据库。

> 您通常不需要指定 `driver-class-name`，因为 Spring Boot 可以从 `url` 中为大多数数据库推断出它。

> 对于要创建的 `DataSource` 池，我们需要能够验证有效的 `Driver` 类是否可用，因此我们在进行任何操作之前都要进行检查。换句话说，如果设置 `spring.datasource.driver-class-name=com.mysql.jdbc.Driver`，则该类必须是可加载的。

参见 [`DataSourceProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jdbc/DataSourceProperties.java) 以获取更多受支持的选项。这些是不管实际实现如何都起作用的标准选项。也可以通过使用各自的前缀（`spring.datasource.hikari.*`，`spring.datasource.tomcat.*` 和 `spring.datasource.dbcp2.*`）微调实现特定的设置。有关更多详细信息，请参阅所用连接池实现的文档。

例如，如果你使用 [Tomcat connection pool](https://tomcat.apache.org/tomcat-8.0-doc/jdbc-pool.html#Common_Attributes)，你可以自定义很多额外的设定，如下面例子所示：

```properties
# Number of ms to wait before throwing an exception if no connection is available.
spring.datasource.tomcat.max-wait=10000

# Maximum number of active connections that can be allocated from this pool at the same time.
spring.datasource.tomcat.max-active=50

# Validate the connection before borrowing it from the pool.
spring.datasource.tomcat.test-on-borrow=true
```

##### 连接到 JNDI 数据库

如果您将 Spring Boot 应用程序部署到 Application Server，则可能需要使用 Application Server 的内置功能来配置和管理 DataSource，并使用 JNDI 对其进行访问。

`spring.datasource.jndi-name` 属性可以替代 `spring.datasource.url`，`spring.datasource.username` 和 `spring.datasource.password` 属性来从特定的 JNDI 位置访问 `DataSource`。例如，`application.properties` 中的以下部分显示了如何访问 JBoss 作为定义的 `DataSource`：

```properties
spring.datasource.jndi-name=java:jboss/datasources/customers
```

#### 4.10.2. 使用 JdbcTemplate

Spring 的 `JdbcTemplate` 和 `NamedParameterJdbcTemplate` 类都会被自动配置，你可以使用 `@Autowire` 直接将它们注入你的 beans，如下面例子所示：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Component;

@Component
public class MyBean {

    private final JdbcTemplate jdbcTemplate;

    @Autowired
    public MyBean(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    // ...

}
```

你可以自定义该模板的一些属性，通过使用 `spring.jdbc.template.*` 属性，如下面例子所示：

```properties
spring.jdbc.template.max-rows=500
```

>  `NamedParameterJdbcTemplate` 内部复用了相同的 `JdbcTemplate` 实例。如果不只一个 `JdbcTemplate` 被定义而又不存在主要的候选者， `NamedParameterJdbcTemplate` 就不会被自动配置。

#### 4.10.3. JPA 和 Spring Data JPA

Java Persistence API 是一种标准技术，允许你将对象映射到关系数据库。`spring-boot-starter-data-jpa` POM 提供了一种快捷的入手方式。它提供了下面的关键依赖：

- Hibernate: 一种最流行的 JPA 实现。
- Spring Data JPA: 使基于 JPA 的存储库的实现变得容易。
- Spring ORMs: Spring Framework 中的核心 ORM 支持。

> 本章节我们并不深入太多 JPA 或者 [Spring Data](https://spring.io/projects/spring-data) 的细节。你可以参考 [spring.io](https://spring.io/) 上的 [“Accessing Data with JPA”](https://spring.io/guides/gs/accessing-data-jpa/) 文档以及 [Spring Data JPA](https://spring.io/projects/spring-data-jpa) 和 [Hibernate](https://hibernate.org/orm/documentation/) 参考文档。

##### Entity 类

传统上，JPA “Entity” 类是在 `persistence.xml` 文件中指定的。在 Spring Boot 中，此文件不是必需的，而是使用 “实体扫描”。默认情况下，将搜索主配置类（用 `@EnableAutoConfiguration` 或 `@SpringBootApplication` 注解修饰的软件包）下的所有软件包。

任何带有 `@Entity`，`@Embeddable` 或 `@MappedSuperclass` 注解修饰的类。典型的实体类类似于以下示例：

```java
package com.example.myapp.domain;

import java.io.Serializable;
import javax.persistence.*;

@Entity
public class City implements Serializable {

    @Id
    @GeneratedValue
    private Long id;

    @Column(nullable = false)
    private String name;

    @Column(nullable = false)
    private String state;

    // ... additional members, often include @OneToMany mappings

    protected City() {
        // no-args constructor required by JPA spec
        // this one is protected since it shouldn't be used directly
    }

    public City(String name, String state) {
        this.name = name;
        this.state = state;
    }

    public String getName() {
        return this.name;
    }

    public String getState() {
        return this.state;
    }

    // ... etc

}
```

> 你可以自定义实体扫描位置，通过使用 `@EntityScan` 注解。参考 “[Separate @Entity Definitions from Spring Configuration](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-separate-entity-definitions-from-spring-configuration)” 了解如何做。

##### Spring Data JPA Repositories

[Spring Data JPA](https://spring.io/projects/spring-data-jpa) 存储库是可以定义以访问数据的接口。JPA 查询是根据您的方法名称自动创建的。例如， `CityRepository` 接口可能会声明 `findAllByState(String state)` 方法以查找处于给定状态的所有城市。

对于更复杂的查询，您可以使用 Spring Data 的 [`Query`](https://docs.spring.io/spring-data/jpa/docs/2.2.3.RELEASE/api/org/springframework/data/jpa/repository/Query.html) 注解。

Spring Data 存储库通常从 [`Repository`](https://docs.spring.io/spring-data/commons/docs/2.2.3.RELEASE/api/org/springframework/data/repository/Repository.html ) 或 [`CrudRepository`](https://docs.spring.io/spring-data/commons/docs/2.2.3.RELEASE/api/org/springframework/data/repository/CrudRepository.html) 接口。如果您使用自动配置，则会从包含您的主要配置类（用 `@EnableAutoConfiguration` 或 `@SpringBootApplication` 注解的类）的包中搜索存储库。

以下示例显示了典型的 Spring Data 存储库接口定义：

```java
package com.example.myapp.domain;

import org.springframework.data.domain.*;
import org.springframework.data.repository.*;

public interface CityRepository extends Repository<City, Long> {

    Page<City> findAll(Pageable pageable);

    City findByNameAndStateAllIgnoringCase(String name, String state);

}
```

Spring Data JPA 存储库支持三种不同的引导模式：默认，延迟和惰性。要启用延迟引导或惰性引导，请将 `spring.data.jpa.repositories.bootstrap-mode` 属性分别设置为 `deferred` 或 `lazy`。当使用延迟或惰性引导时，自动配置的 `EntityManagerFactoryBuilder` 将使用上下文的 `AsyncTaskExecutor`（如果有）作为引导执行器。如果存在多个，将使用一个名为 `applicationTaskExecutor` 的应用。

> 我们仅仅是走马观花一般概述 Spring Data JPA 的表面特性。完整的细节，请参考 [Spring Data JPA reference documentation](https://docs.spring.io/spring-data/jdbc/docs/1.1.3.RELEASE/reference/html/) 。

##### 创建和丢弃 JPA Databases

默认情况下，仅当您使用内置数据库（H2，HSQL 或 Derby），才会自动创建 JPA 数据库。您可以通过使用 `spring.jpa.*` 属性显式配置 JPA 设置。例如，要创建和删除表，可以在 `application.properties` 中添加以下行：

```
spring.jpa.hibernate.ddl-auto=create-drop
```

> Hibernate 自己的内部属性名称（如果您记得更好的话）是 `hibernate.hbm2ddl.auto`。您可以通过使用 `spring.jpa.properties.*`（在将前缀添加到实体管理器之前删除前缀）来设置它以及其他 Hibernate 本地属性。下面的行显示了为 Hibernate 设置 JPA 属性的示例：

```
spring.jpa.properties.hibernate.globally_quoted_identifiers=true
```

前面示例中的行将 `hibernate.globally_quoted_identifiers` 属性的值 `true` 传递给 Hibernate 实体管理器。

默认情况下，DDL 执行（或验证）推迟到 `ApplicationContext` 启动之前。还有一个 `spring.jpa.generate-ddl` 标志，但是如果启用了休眠自动配置，则不会使用它，因为 `ddl-auto` 设置更细粒度。

##### 在视图中打开 EntityManager

如果您正在运行 Web 应用程序，则 Spring Boot 默认会注册 [`OpenEntityManagerInViewInterceptor`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/orm/jpa/support/OpenEntityManagerInViewInterceptor.html) 以应用“在视图中打开 EntityManager”模式，以允许在 Web 视图中进行惰性加载。如果您不希望出现这种情况，则应在 `application.properties` 中将 `spring.jpa.open-in-view` 设置为 `false`。

#### 4.10.4. Spring Data JDBC

Spring Data 包括对 JDBC 的存储库支持，并将自动为 `CrudRepository` 上的方法生成 SQL。对于更高级的查询，提供了一个 `@Query` 注解。

当必要的依赖项位于类路径上时，Spring Boot 将自动配置 Spring Data 的 JDBC 存储库。可以将它们添加到您的项目中，而只需依赖于 `spring-boot-starter-data-jdbc`。如有必要，您可以通过向应用程序添加 `@EnableJdbcRepositories` 注解或 `JdbcConfiguration` 子类来控制 Spring Data JDBC 的配置。

> 关于 Spring Data JDBC 的完整细节，请参考 [reference documentation](https://docs.spring.io/spring-data/jdbc/docs/1.1.3.RELEASE/reference/html/) 。

#### 4.10.5. 使用 H2 的 Web 控制台

[H2 database](https://www.h2database.com/) 提供一个 [browser-based console](https://www.h2database.com/html/quickstart.html#h2_console) ，Spring Boot 能够为你自动配置。当下列条件满足时该控制台会被自动配置：

- 你在开发的是基于 servlet 的 web 应用。
- `com.h2database:h2` 在类路径上。
- 你正在使用 [Spring Boot’s developer tools](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools) 。

> 如果你没有使用 Spring Boot 的开发工具，仍然可以使用 H2 的控制台，你可以将 `spring.h2.console.enabled` 属性设置为 `true`。

> H2 控制台应该仅在开发过程中使用，因此，你需要保证生产环境中 `spring.h2.console.enabled` 属性没有设定为 `true` 。

##### 修改 H2 控制台路径

默认情况下，控制台的访问路径是 `/h2-console`。你可以通过使用 `spring.h2.console.path` 属性来自定义控制台访问路径。

#### 4.10.6. 使用 jOOQ

jOOQ Object Oriented Querying ([jOOQ](https://www.jooq.org/)) 是一个来自 [Data Geekery](https://www.datageekery.com/) 的非常流行的产品，它可以依据你的数据库生成 Java 代码并帮助你通过它提供的链式 API 构建类型安全的 SQL 查询。商业版和开源版产品都可以在 Spring Boot 中使用。

##### 代码生成

为了使用 jOOQ 类型安全查询，您需要从数据库模式中生成 Java 类。您可以按照 [jOOQ用户手册](https://www.jooq.org/doc/3.12.3/manual-single-page/#jooq-in-7-steps-step3) 中的说明进行操作。如果您使用 `jooq-codegen-maven` 插件，并且还使用 `spring-boot-starter-parent` “父POM”，则可以安全地忽略该插件的 `<version>` 标签。您还可以使用 Spring Boot 定义的版本变量（例如 `h2.version`）来声明插件的数据库依赖项。以下清单显示了一个示例：

```xml
<plugin>
    <groupId>org.jooq</groupId>
    <artifactId>jooq-codegen-maven</artifactId>
    <executions>
        ...
    </executions>
    <dependencies>
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <version>${h2.version}</version>
        </dependency>
    </dependencies>
    <configuration>
        <jdbc>
            <driver>org.h2.Driver</driver>
            <url>jdbc:h2:~/yourdatabase</url>
        </jdbc>
        <generator>
            ...
        </generator>
    </configuration>
</plugin>
```

##### 使用 DSLContext

jOOQ 提供的链式 API 是通过 `org.jooq.DSLContext` 接口启动的。Spring Boot 将一个 `DSLContext` 自动配置为一个 Spring Bean，并将其连接到您的应用程序 `DataSource`。要使用 `DSLContext`，可以使用 `@Autowire`，如以下示例所示：

```java
@Component
public class JooqExample implements CommandLineRunner {

    private final DSLContext create;

    @Autowired
    public JooqExample(DSLContext dslContext) {
        this.create = dslContext;
    }

}
```

> jOOQ 手册使用名为 `create` 的变量来持有 `DSLContext`。

然后，你可以使用 `DSLContext` 来构建你的查询，如下面例子所示：

```java
public List<GregorianCalendar> authorsBornAfter1980() {
    return this.create.selectFrom(AUTHOR)
        .where(AUTHOR.DATE_OF_BIRTH.greaterThan(new GregorianCalendar(1980, 0, 1)))
        .fetch(AUTHOR.DATE_OF_BIRTH);
}
```

##### jOOQ SQL 方言

除非 `spring.jooq.sql-dialect` 属性已经被配置，Spring Boot 决定用于你的数据库的 SQL 方言。如果 Spring Boot 无法探测到方言，使用 `DEFAULT`。

> Spring Boot 只能自动配置开源版本的 jOOQ 支持的方言。

##### 自定义 jOOQ

可以通过定义自己的 `@Bean` 定义来实现更高级的自定义，这在创建 jOOQ `Configuration` 时使用。您可以为以下 jOOQ 类型定义 bean：

- `ConnectionProvider`
- `ExecutorProvider`
- `TransactionProvider`
- `RecordMapperProvider`
- `RecordUnmapperProvider`
- `Settings`
- `RecordListenerProvider`
- `ExecuteListenerProvider`
- `VisitListenerProvider`
- `TransactionListenerProvider`

如果您想完全控制 jOOQ 配置，也可以创建自己的 `org.jooq.Configuration` `@Bean`。

### 4.11. 使用 NoSQL 技术

Spring Data 提供了其他项目来帮助您访问各种 NoSQL 技术，包括：

- [MongoDB](https://spring.io/projects/spring-data-mongodb)
- [Neo4J](https://spring.io/projects/spring-data-neo4j)
- [Elasticsearch](https://spring.io/projects/spring-data-elasticsearch)
- [Solr](https://spring.io/projects/spring-data-solr)
- [Redis](https://spring.io/projects/spring-data-redis)
- [GemFire](https://spring.io/projects/spring-data-gemfire) or [Geode](https://spring.io/projects/spring-data-geode)
- [Cassandra](https://spring.io/projects/spring-data-cassandra)
- [Couchbase](https://spring.io/projects/spring-data-couchbase)
- [LDAP](https://spring.io/projects/spring-data-ldap)

Spring Boot 为 Redis，MongoDB，Neo4j，Elasticsearch，Solr Cassandra，Couchbase 和 LDAP 提供自动配置。您可以使用其他项目，但必须自己进行配置。请参阅 [spring.io/projects/spring-data](https://spring.io/projects/spring-data) 上的相应参考文档。

#### 4.11.1. Redis

[Redis](https://redis.io/) 是一个缓存，消息代理，以及一个拥有丰富特性的键值存储。Spring Boot 为 [Lettuce](https://github.com/lettuce-io/lettuce-core/) 和 [Jedis](https://github.com/xetorthio/jedis/) 客户端类库提供了基本的自动配置，并通过 [Spring Data Redis](https://github.com/spring-projects/spring-data-redis) 提供了它们之上的抽象。

有一个 `spring-boot-starter-data-redis` `Starter`，用于以方便的方式收集依赖项。默认情况下，它使用 [Lettuce](https://github.com/lettuce-io/lettuce-core/)。该启动程序可以处理传统应用程序和响应式应用程序。

> 我们还提供了一个 `spring-boot-starter-data-redis-reactive` `Starter`，以与其他具有反应性支持的存储保持一致。

##### 连接到 Redis

您可以像其他任何 Spring Bean 一样注入自动配置的 `RedisConnectionFactory`，`StringRedisTemplate` 或普通的 `RedisTemplate` 实例。默认情况下，该实例尝试连接到 Redis 服务器的 `localhost:6379`。下面的清单显示了这种 Bean 的示例：

```java
@Component
public class MyBean {

    private StringRedisTemplate template;

    @Autowired
    public MyBean(StringRedisTemplate template) {
        this.template = template;
    }

    // ...

}
```

> 您还可以注册任意数量的实现 `LettuceClientConfigurationBuilderCustomizer` 的 bean，以进行更高级的自定义。如果您使用 Jedis，`JedisClientConfigurationBuilderCustomizer` 也可用。

如果您添加自己的任何自动配置类型的 `@Bean`，它将替换默认值（除非排除是基于 bean 名称 `redisTemplate`而不是其类型的 `RedisTemplate` 除外） 。默认情况下，如果 `commons-pool2` 在类路径中，则将得到一个池化连接工厂。

#### 4.11.2. MongoDB

[MongoDB](https://www.mongodb.com/) 是一个开源 NoSQL 文档数据库，它使用类似 JSON 的数据结构而不是传统的基于表的关系数据。Spring Boot 为使用 MongoDB 提供了许多便利，包括 `spring-boot-starter-data-mongodb` 和 `spring-boot-starter-data-mongodb-active` “Starters”。

##### 连接到 MongoDB 数据库

要访问 Mongo 数据库，您可以注入自动配置的 `org.springframework.data.mongodb.MongoDbFactory` 。默认情况下，该实例尝试通过 `mongodb://localhost/test` 连接到 MongoDB 服务器。以下示例显示了如何连接到 MongoDB 数据库：

```java
import org.springframework.data.mongodb.MongoDbFactory;
import com.mongodb.DB;

@Component
public class MyBean {

    private final MongoDbFactory mongo;

    @Autowired
    public MyBean(MongoDbFactory mongo) {
        this.mongo = mongo;
    }

    // ...

    public void example() {
        DB db = mongo.getDb();
        // ...
    }

}
```

您可以设置 `spring.data.mongodb.uri` 属性来更改 URL 并配置其他设置，例如*数据库副本集*，如以下示例所示：

```properties
spring.data.mongodb.uri=mongodb://user:secret@mongo1.example.com:12345,mongo2.example.com:23456/test
```

另外，只要您使用 Mongo 2.x，就可以指定一个 `host`/`port`。例如，您可以在 `application.properties` 中声明以下设置：

```properties
spring.data.mongodb.host=mongoserver
spring.data.mongodb.port=27017
```

如果定义了自己的 `MongoClient`，它将用于自动配置合适的 `MongoDbFactory`。`com.mongodb.MongoClient` 和 `com.mongodb.client.MongoClient` 均受支持。

> 如果您使用 Mongo 3.0 Java 驱动程序，则不支持 `spring.data.mongodb.host` 和 `spring.data.mongodb.port`。在这种情况下，应使用 `spring.data.mongodb.uri` 来提供所有配置。

> 如果未指定 `spring.data.mongodb.port`，则使用默认值 `27017`。您可以从前面展示的示例中删除此行。

> 如果您不使用 Spring Data Mongo，则可以注入 `com.mongodb.MongoClient` bean而不是使用 `MongoDbFactory`。如果您想完全控制建立 MongoDB 连接的方式，还可以声明自己的 `MongoDbFactory` 或 `MongoClient` bean。

> 如果您使用反应式驱动程序，则 SSL 需要 Netty。如果可以使用 Netty 并且尚未自定义要使用的工厂，则自动配置会自动配置该工厂。

##### MongoTemplate

[Spring Data MongoDB](https://spring.io/projects/spring-data-mongodb) 提供了一个 [`MongoTemplate`](https://docs.spring.io/spring-data/mongodb/docs/2.2.3.RELEASE/api/org/springframework/data/mongodb/core/MongoTemplate.html) 类，非常类似于 Spring 的 `JdbcTemplate` 。就像使用 `JdbcTemplate` 那样，Spring Boot 自动为你配置 bean 来注入该模板，如下所示：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.stereotype.Component;

@Component
public class MyBean {

    private final MongoTemplate mongoTemplate;

    @Autowired
    public MyBean(MongoTemplate mongoTemplate) {
        this.mongoTemplate = mongoTemplate;
    }

    // ...

}
```

参考 [`MongoOperations` Javadoc](https://docs.spring.io/spring-data/mongodb/docs/2.2.3.RELEASE/api/org/springframework/data/mongodb/core/MongoOperations.html) 了解完整细节。

##### Spring Data MongoDB Repositories

Spring Data 包含对 MongoDB 的存储库支持。与前面讨论的 JPA 存储库一样，基本原理是根据方法名称自动构造查询。

实际上，Spring Data JPA 和 Spring Data MongoDB 共享相同的通用基础架构。您可以从前面的 JPA 示例开始，并假设 `City` 现在是 Mongo 数据类，而不是 JPA `@Entity`，它的工作方式相同，如以下示例所示：

```java
package com.example.myapp.domain;

import org.springframework.data.domain.*;
import org.springframework.data.repository.*;

public interface CityRepository extends Repository<City, Long> {

    Page<City> findAll(Pageable pageable);

    City findByNameAndStateAllIgnoringCase(String name, String state);

}
```

> 您可以使用 `@EntityScan` 注解来自定义文档扫描位置。

> 有关 Spring Data MongoDB 的完整详细信息，包括其丰富的对象映射技术，请参阅其 [参考文档](https://spring.io/projects/spring-data-mongodb)。

##### 内置 Mongo

Spring Boot 为 [内置 Mongo](https://github.com/flapdoodle-oss/de.flapdoodle.embed.mongo) 提供了自动配置。要在 Spring Boot 应用程序中使用它，请添加对 `de.flapdoodle.embed:de.flapdoodle.embed.mongo` 的依赖。

可以通过设置 `spring.data.mongodb.port` 属性来配置 Mongo 监听的端口。要使用随机分配的空闲端口，请使用 0 值。由 `MongoAutoConfiguration` 创建的 `MongoClient` 将自动配置为使用随机分配的端口。

> 如果未配置自定义端口，则默认情况下，内置支持会使用随机端口（而不是 27017）。

如果在类路径上有 SLF4J，则 Mongo 产生的输出将自动路由到名为 `org.springframework.boot.autoconfigure.mongo.embedded.EmbeddedMongo` 的记录器。

您可以声明自己的 `IMongodConfig` 和 `IRuntimeConfig` bean，以控制 Mongo 实例的配置和日志记录路由。可以通过声明一个 `DownloadConfigBuilderCustomizer` bean来定制下载配置。

#### 4.11.3. Neo4j

[Neo4j](https://neo4j.com/) 是一种开源的 NoSQL 图数据库，使用丰富的数据模型，该模型由通过第一类关系相互连接的节点组成，这种模型相对于传统 RDBMS 方式更加适合相互关联的大数据。Spring Boot 提供了一系列方便的工具来使用 Neo4j，包括 `spring-boot-starter-data-neo4j` “Starter”。

##### 连接到 Neo4j 数据库

为了访问 Neo4j 服务器，你可以注入一个自动配置的 `org.neo4j.ogm.session.Session`。默认情况下，实例尝试使用 Bolt 协议通过 `localhost:7687` 连接 Neo4j 服务器。下面的例子展示了如何注入 Neo4j `Session` ：

```java
@Component
public class MyBean {

    private final Session session;

    @Autowired
    public MyBean(Session session) {
        this.session = session;
    }

    // ...

}
```

你可以通过设定 `spring.data.neo4j.*` 属性配置需要使用的 url 和身份凭证，如下面例子所示：

```properties
spring.data.neo4j.uri=bolt://my-server:7687
spring.data.neo4j.username=neo4j
spring.data.neo4j.password=secret
```

你可以通过添加 `org.neo4j.ogm.config.Configuration` bean 或者 `org.neo4j.ogm.session.SessionFactory` bean 获取对会话创建的完全控制。

##### 使用内置模式

如果你添加 `org.neo4j:neo4j-ogm-embedded-driver` 到你的应用依赖中，Spring Boot 将自动配置一个同进程的内置 Neo4j 实例，你的应用关闭时不会有任何数据被持久化。

> 由于嵌入式 Neo4j OGM 驱动程序本身不提供 Neo4j 内核，因此您必须自己声明 `org.neo4j:neo4j` 作为依赖项。有关兼容版本的列表，请参阅 [Neo4j OGM文档](https://neo4j.com/docs/ogm-manual/current/reference/#reference:getting-started) 。

当类路径上有多个驱动程序时，内置驱动程序优先于其他驱动程序。您可以通过设置 `spring.data.neo4j.embedded.enabled=false` 显式禁用内置模式。

如果内置驱动程序和 Neo4j 内核位于上述类路径上，则 [Data Neo4j Tests](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-neo4j-test) 会自动使用内置 Neo4j 实例。

> 您可以通过在配置中提供数据库文件的路径来启用内置模式的持久性。比如 `spring.data.neo4j.uri=file://var/tmp/graph.db`。

##### 使用本地类型

Neo4j-OGM 可以将某些类型（例如，`java.time.*` 中的类型）映射到基于 `String` 的属性或 Neo4j 提供的本地类型之一。出于向后兼容的原因，Neo4j-OGM 的默认设置是使用基于字符串的表示形式。要使用本地类型，请添加对 `org.neo4j:neo4j-ogm-bolt-native-types` 或 `org.neo4j:neo4j-ogm-embedded-native-types` 的依赖，并配置 `spring.data.neo4j.use-native-types` 属性，如以下示例所示：

```properties
spring.data.neo4j.use-native-types=true
```

##### Neo4jSession

默认情况下，如果您正在运行 Web 应用程序，则会话将绑定到线程以进行请求的整个处理（即，它使用“在视图中打开会话”模式）。如果您不希望出现这种情况，请将以下行添加到您的 `application.properties` 文件中：

```properties
spring.data.neo4j.open-in-view=false
```

##### Spring Data Neo4j Repositories

Spring Data 包括对 Neo4j 的存储库支持。

Spring Data Neo4j 与许多其他 Spring Data 模块一样，与 Spring Data JPA 共享公共基础结构。您可以以前面的 JPA 示例为例，将 `City` 定义为 Neo4j OGM `@NodeEntity` 而不是 JPA `@Entity`，并且存储库抽象以相同的方式工作，如以下示例所示：

```java
package com.example.myapp.domain;

import java.util.Optional;

import org.springframework.data.neo4j.repository.*;

public interface CityRepository extends Neo4jRepository<City, Long> {

    Optional<City> findOneByNameAndState(String name, String state);

}
```

`spring-boot-starter-data-neo4j` “Starter” 可启用存储库支持以及事务管理。您可以通过在 `@Configuration` bean上分别使用 `@EnableNeo4jRepositories` 和 `@EntityScan` 来定制位置以查找存储库和实体。

> 有关 Spring Data Neo4j 的完整详细信息，包括其对象映射技术，请参阅 [参考文档](https://docs.spring.io/spring-data/neo4j/docs/5.2.3.RELEASE/reference/html/ )。

#### 4.11.4. Solr

[Apache Solr](https://lucene.apache.org/solr/) 是一个搜索引擎。Spring Boot 为 Solr 5 客户端库提供了基本的自动配置，并由 [Spring Data Solr](https://github.com/spring-projects/spring-data-solr) 在其之上提供了抽象。`spring-boot-starter-data-solr` "Starter" 是用来集合所需依赖的便捷方式。

##### 连接到 Solr

您可以像注入其他任何 Spring Bean 一样注入自动配置的 `SolrClient` 实例。默认情况下，该实例尝试连接到位于 `localhost:8983/solr` 的服务器。下面的示例显示如何注入 Solr bean：

```java
@Component
public class MyBean {

    private SolrClient solr;

    @Autowired
    public MyBean(SolrClient solr) {
        this.solr = solr;
    }

    // ...

}
```

如果你添加自己的 `SolrClient` 类型的 `@Bean` ，它将替换默认的实例。

##### Spring Data Solr Repositories

Spring Data 包含对 Apache Solr 的存储库支持。与前面讨论的 JPA 存储库一样，基本原理是根据方法名称自动为您构建查询。

实际上，Spring Data JPA 和 Spring Data Solr 共享相同的通用基础结构。您可以从以前的 JPA 示例开始，并假定 `City` 现在是 `@SolrDocument` 类，而不是 JPA `@Entity`，它的工作方式相同。

Spring Data Solr 的完整细节，请参考 [reference documentation](https://docs.spring.io/spring-data/solr/docs/4.1.3.RELEASE/reference/html/)。

#### 4.11.5. Elasticsearch

[Elasticsearch](https://www.elastic.co/products/elasticsearch) 是一个开源的，分布式，RESTful 搜索和分析引擎。Spring Boot 提供了 Elasticsearch 基本的自动配置。

Spring Boot 支持几种客户端：

- 官方 Java “高级”和“低级” REST 客户端
- 由 Spring Data Elasticsearch 提供的 `ReactiveElasticsearchClient` 

传输客户端仍然可用，但是 [Spring Data Elasticsearch](https://github.com/spring-projects/spring-data-elasticsearch) 和 Elasticsearch 本身已弃用了它的支持。它将在将来的版本中删除。Spring Boot 提供了专用的 “Starter”，即 `spring-boot-starter-data-elasticsearch`。

[Jest](https://github.com/searchbox-io/Jest) 客户端也已被弃用，因为 Elasticsearch 和 Spring Data Elasticsearch 都为 REST 客户端提供了官方支持。

##### 使用 REST 客户端连接 Elasticsearch

Elasticsearch 附带了 [两个不同的 REST 客户端](https://www.elastic.co/guide/en/elasticsearch/client/java-rest/current/index.html)，您可以用来查询集群：“低级"客户端和“高级”客户端。

如果您的类路径具有 `org.elasticsearch.client:elasticsearch-rest-client` 依赖，Spring Boot 将自动配置并注册一个默认情况下以 `localhost:9200` 为目标的 `RestClient` bean。您可以进一步调整 `RestClient` 的配置方式，如以下示例所示：

```properties
spring.elasticsearch.rest.uris=https://search.example.com:9200
spring.elasticsearch.rest.read-timeout=10s
spring.elasticsearch.rest.username=user
spring.elasticsearch.rest.password=secret
```

您还可以注册任意数量的实现 `RestClientBuilderCustomizer` 的 Bean，以进行更高级的自定义。要完全控制注册，请定义一个 `RestClient` bean。

如果您的类路径具有 `org.elasticsearch.client:elasticsearch-rest-high-level-client` 依赖，Spring Boot 将自动配置一个 `RestHighLevelClient`，它包装任何现有的 `RestClient` bean，并复用其 HTTP 配置。

##### 使用 Reactive REST 客户端连接 Elasticsearch

[Spring Data Elasticsearch](https://spring.io/projects/spring-data-elasticsearch) 附带了 `ReactiveElasticsearchClient`，用于以反应方式查询 Elasticsearch 实例。它建立在 `WebFlux的WebClient` 之上，因此 `spring-boot-starter-elasticsearch` 和 `spring-boot-starter-webflux` 依赖对于启用此支持很有用。

默认情况下，Spring Boot 将自动配置并注册一个以 `localhost:9200` 为目标的 `ReactiveElasticsearchClient` bean。您可以进一步调整其配置，如以下示例所示：

```properties
spring.data.elasticsearch.client.reactive.endpoints=search.example.com:9200
spring.data.elasticsearch.client.reactive.use-ssl=true
spring.data.elasticsearch.client.reactive.socket-timeout=10s
spring.data.elasticsearch.client.reactive.username=user
spring.data.elasticsearch.client.reactive.password=secret
```

如果配置属性还不够，并且您想完全控制客户端配置，则可以注册自定义 `ClientConfiguration` bean。

##### 使用 Jest 连接 Elasticsearch

现在，Spring Boot 支持官方的 `RestHighLevelClient`，不建议使用 Jest。

如果您在类路径上具有 `Jest`，则可以注入自动配置的 `JestClient`，默认情况下，其目标是 `localhost:9200`。您可以进一步调整客户端的配置方式，如以下示例所示：

```properties
spring.elasticsearch.jest.uris=https://search.example.com:9200
spring.elasticsearch.jest.read-timeout=10000
spring.elasticsearch.jest.username=user
spring.elasticsearch.jest.password=secret
```

您也可以注册任意数量的实现 `HttpClientConfigBuilderCustomizer` 的 bean，以进行更高级的自定义。以下示例调整其他 HTTP 设置：

```java
static class HttpSettingsCustomizer implements HttpClientConfigBuilderCustomizer {

    @Override
    public void customize(HttpClientConfig.Builder builder) {
        builder.maxTotalConnection(100).defaultMaxTotalConnectionPerRoute(5);
    }

}
```

要完全控制注册，请定义一个 `JestClient` bean。

##### 使用 Spring Data 连接 Elasticsearch

要连接到 Elasticsearch，必须定义一个 `RestHighLevelClient` bean，它由 Spring Boot 自动配置或由应用程序手动提供（请参阅前面的部分）。有了此配置后，可以像其他任何 Spring bean 一样注入 `ElasticsearchRestTemplate`，如以下示例所示：

```java
@Component
public class MyBean {

    private final ElasticsearchRestTemplate template;

    public MyBean(ElasticsearchRestTemplate template) {
        this.template = template;
    }

    // ...

}
```

在存在 `spring-data-elasticsearch` 和使用 `WebClient` 所需的依赖项（通常是 `spring-boot-starter-webflux`）的情况下，Spring Boot 还可以自动配置 [ReactiveElasticsearchClient](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-connecting-to-elasticsearch-reactive-rest)  和一个 `ReactiveElasticsearchTemplate` 作为 bean。它们与其他 REST 客户端是等效的。

##### Spring Data Elasticsearch Repositories

Spring Data 包括对 Elasticsearch 的存储库支持。与前面讨论的 JPA 存储库一样，基本原理是根据方法名称自动为您构造查询。

实际上，Spring Data JPA 和 Spring Data Elasticsearch 共享相同的通用基础架构。您可以从前面的 JPA 示例开始，并假设 `City` 现在是 Elasticsearch `@Document` 类，而不是 JPA `@Entity`，它的工作方式相同。

> 有关 Spring Data Elasticsearch 的完整细节，请参考 [reference documentation](https://docs.spring.io/spring-data/elasticsearch/docs/current/reference/html/) 。

Spring Boot 使用 `ElasticsearchRestTemplate` 或 `ReactiveElasticsearchTemplate` bean 支持经典和反应式 Elasticsearch 存储库。给定所需的依赖项，这些 bean 最有可能由 Spring Boot 自动配置。

如果您希望使用自己的模板来支持 Elasticsearch 存储库，则可以添加自己的 `ElasticsearchRestTemplate` 或 `ElasticsearchOperations` `@Bean`，只要将其命名为 `"elasticsearchTemplate"` 即可。同样的情况也适用于 `ReactiveElasticsearchTemplate` 和 `ReactiveElasticsearchOperations`，bean 名称为 `"reactiveElasticsearchTemplate"`。

您可以选择使用以下属性禁用存储库支持：

```properties
spring.data.elasticsearch.repositories.enabled=false
```

#### 4.11.6. Cassandra

[Cassandra](https://cassandra.apache.org/) 是一个开源的分布式数据库管理系统，旨在处理许多商用服务器上的大量数据。Spring Boot 为 Cassandra 提供自动配置，并由 [Spring Data Cassandra](https://github.com/spring-projects/spring-data-cassandra) 在其之上提供抽象。有一个 `spring-boot-starter-data-cassandra` “Starter”，用于以方便的方式收集依赖项。

##### 连接 Cassandra

您可以像使用其他任何 Spring Bean 一样注入自动配置的 `CassandraTemplate` 或 Cassandra `Session` 实例。`spring.data.cassandra.*` 属性可用于自定义连接。通常，您提供 `keyspace-name` 和 `contact-points` 属性，如以下示例所示：

```properties
spring.data.cassandra.keyspace-name=mykeyspace
spring.data.cassandra.contact-points=cassandrahost1,cassandrahost2
```

您还可以注册任意数量的实现 `ClusterBuilderCustomizer` 的 Bean，以进行更高级的自定义。

以下代码清单显示了如何注入 Cassandra bean：

```java
@Component
public class MyBean {

    private CassandraTemplate template;

    @Autowired
    public MyBean(CassandraTemplate template) {
        this.template = template;
    }

    // ...

}
```

如果添加自己的 `@CassandraTemplate` 类型的 `@Bean`，它将替换默认值。

##### Spring Data Cassandra Repositories

Spring Data 包含对 Cassandra 的基本存储库支持。当前，它比前面讨论的 JPA 存储库受到更多限制，并且需要使用 `@Query` 注解查找器方法。

> 有关 Spring Data Cassandra 的完整细节，请参考 [reference documentation](https://docs.spring.io/spring-data/cassandra/docs/)。

#### 4.11.7. Couchbase

[Couchbase](https://www.couchbase.com/) 是一个开源的，分布式，多模型的 NoSQL 面向文档的数据库，已针对交互式应用程序进行了优化。Spring Boot 提供了对 Couchbase 的自动配置，并由 [Spring Data Couchbase](https://github.com/spring-projects/spring-data-couchbase) 在其之上提供了抽象。有 `spring-boot-starter-data-couchbase` 和 `spring-boot-starter-data-couchbase-reactive` “Starters”，用于以方便的方式收集依赖项。

##### 连接 Couchbase

您可以通过添加 Couchbase SDK 和一些配置来获取 `Bucket` 和 `Cluster`。可以使用 `spring.couchbase.*` 属性来自定义连接。通常，您提供引导主机，存储桶名称和密码，如以下示例所示：

```properties
spring.couchbase.bootstrap-hosts=my-host-1,192.168.1.123
spring.couchbase.bucket.name=my-bucket
spring.couchbase.bucket.password=secret
```

> 您*至少*需要提供引导主机，在这种情况下，存储区名称为 `default` ，密码为空字符串。另外，您可以定义自己的 `org.springframework.data.couchbase.config.CouchbaseConfigurer` `@Bean` 以控制整个配置。

也可以自定义某些 `CouchbaseEnvironment` 设置。例如，以下配置更改了用于打开新的 `Bucket` 并启用 SSL 支持的超时：

```properties
spring.couchbase.env.timeouts.connect=3000
spring.couchbase.env.ssl.key-store=/location/of/keystore.jks
spring.couchbase.env.ssl.key-store-password=secret
```

检查 `spring.couchbase.env.*` 属性获取更多细节。

##### Spring Data Couchbase Repositories

Spring Data 包括对 Couchbase 的存储库支持。有关 Spring Data Couchbase 的完整详细信息，请参考 [参考文档](https://docs.spring.io/spring-data/couchbase/docs/current/reference/html/)。

您可以像使用任何其他 Spring Bean 一样注入自动配置的 `CouchbaseTemplate` 实例，前提是 *default* `CouchbaseConfigurer` 可用（如前所述，启用 Couchbase 支持时会发生这种情况）。

以下示例显示了如何注入 Couchbase bean：

```java
@Component
public class MyBean {

    private final CouchbaseTemplate template;

    @Autowired
    public MyBean(CouchbaseTemplate template) {
        this.template = template;
    }

    // ...

}
```

您可以在自己的配置中定义一些 Bean，以覆盖自动配置提供的那些：

- 一个名为 `CouchbaseTemplate` `@Bean`的名称。

- 名称为 `couchbaseIndexManager的IndexManager` `@Bean`。

- 名称为 `couchbaseCustomConversions` 的 CustomBeans `@Bean`。

为了避免在您自己的配置中对这些名称进行硬编码，您可以重用 Spring Data Couchbase 提供的 `BeanNames`。例如，您可以自定义要使用的转换器，如下所示：

```java
@Configuration(proxyBeanMethods = false)
public class SomeConfiguration {

    @Bean(BeanNames.COUCHBASE_CUSTOM_CONVERSIONS)
    public CustomConversions myCustomConversions() {
        return new CustomConversions(...);
    }

    // ...

}
```

> 如果您想完全绕过Spring Data Couchbase的自动配置，请提供您自己的`org.springframework.data.couchbase.config.AbstractCouchbaseDataConfiguration` 实现。

#### 4.11.8. LDAP

[LDAP](https://en.wikipedia.org/wiki/Lightweight_Directory_Access_Protocol) （轻量级目录访问协议）是一种开源的，与供应商无关的行业标准应用协议，用于通过 IP 网络访问和维护分布式目录信息服务。Spring Boot 从 [UnboundID](https://www.ldap.com/unboundid-ldap-sdk-for-java) 为任何兼容的 LDAP 服务器提供自动配置，并支持嵌入式内存 LDAP 服务器。

LDAP 抽象由 [Spring Data LDAP](https://github.com/spring-projects/spring-data-ldap) 提供。有一个 `spring-boot-starter-data-ldap` “Starter”，用于以方便的方式收集依赖项。

##### 连接 LDAP 服务器

要连接到 LDAP 服务器，请确保您声明对 `spring-boot-starter-data-ldap` “Starter” 或 `spring-ldap-core` 的依赖，然后在 `application.properties` 中声明服务器的 URL，如以下示例所示：

```properties
spring.ldap.urls=ldap://myserver:1235
spring.ldap.username=admin
spring.ldap.password=secret
```

如果您需要自定义连接设置，则可以使用 `spring.ldap.base` 和 `spring.ldap.base-environment` 属性。

将基于这些设置自动配置 `LdapContextSource`。如果您需要对其进行自定义（例如使用 `PooledContextSource`），则仍可以注入自动配置的 `LdapContextSource`。确保将自定义的 `ContextSource` 标记为 `@Primary`，以便自动配置的 `LdapTemplate` 使用它。

##### Spring Data LDAP Repositories

Spring Data 包括对 LDAP 的存储库支持。有关 Spring Data LDAP 的完整详细信息，请参考 [参考文档](https://docs.spring.io/spring-data/ldap/docs/1.0.x/reference/html/)。

您还可以像使用其他任何 Spring Bean 一样注入自动配置的 `LdapTemplate` 实例，如以下示例所示：

```java
@Component
public class MyBean {

    private final LdapTemplate template;

    @Autowired
    public MyBean(LdapTemplate template) {
        this.template = template;
    }

    // ...

}
```

##### 嵌入式内存 LDAP 服务器

出于测试目的，Spring Boot 支持从 [UnboundID](https://www.ldap.com/unboundid-ldap-sdk-for-java) 自动配置内存中的 LDAP 服务器。要配置服务器，请向 `com.unboundid：unboundid-ldapsdk` 添加一个依赖项，并声明一个 `spring.ldap.embedded.base-dn` 属性，如下所示：

```properties
spring.ldap.embedded.base-dn=dc=spring,dc=io
```

> 可以定义多个 base-dn 值，但是，由于专有名称通常包含逗号，因此必须使用正确的符号进行定义。在 yaml 文件中，可以使用 yaml 列表符号：
>
> ```yaml
> spring.ldap.embedded.base-dn:
> 	- dc=spring,dc=io
> 	- dc=pivotal,dc=io
> ```
>
> 在 properties 文件中，您必须将索引作为属性名称的一部分包括在内：
>
> ```properties
> spring.ldap.embedded.base-dn[0]=dc=spring,dc=io
> spring.ldap.embedded.base-dn[1]=dc=pivotal,dc=io
> ```

默认情况下，服务器在随机端口上启动并触发常规 LDAP 支持。无需指定 `spring.ldap.urls` 属性。

如果您的类路径中有一个 `schema.ldif` 文件，则该文件用于初始化服务器。如果您想从其他资源加载初始化脚本，也可以使用 `spring.ldap.embedded.ldif` 属性。

默认情况下，使用标准架构来验证 `LDIF` 文件。您可以通过设置 `spring.ldap.embedded.validation.enabled` 属性来完全关闭验证。如果您具有自定义属性，则可以使用 `spring.ldap.embedded.validation.schema` 来定义您的自定义属性类型或对象类。

#### 4.11.9. InfluxDB

[InfluxDB](https://www.influxdata.com/) 是一个开源的时间序列数据库，已针对运行监控，应用程序度量，物联网传感器数据和实时分析等领域中的时间序列数据进行快速，高可用性的存储和检索进行了优化。

##### 连接 InfluxDB

Spring Boot 自动配置一个 `InfluxDB` 实例，前提是 `influxdb-java` 客户端位于类路径上，并且设置了数据库的 URL，如以下示例所示：

```properties
spring.influx.url=https://172.0.0.1:8086
```

如果到 InfluxDB 的连接需要用户名和密码，则可以相应地设置 `spring.influx.user` 和 `spring.influx.password` 属性。

InfluxDB 依赖 OkHttp。如果您需要调整 InfluxDB 在后台使用的 HTTP 客户端，则可以注册 `InfluxDbOkHttpClientBuilderProvider` bean。

### 4.12. 缓存

Spring 框架支持透明地向应用程序添加缓存。从本质上讲，抽象将缓存应用于方法，从而根据缓存中可用的信息减少执行次数。缓存逻辑是对应用透明的，不会对调用者造成任何干扰。只要通过 `@EnableCaching` 注解启用了缓存支持，Spring Boot 就会自动配置缓存基础架构。

> 参考 Spring 框架文档的 [relevant section](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/integration.html#cache) 获取更多细节。

简而言之，将缓存添加到服务的操作就像将相关注解添加到其方法一样容易，如以下示例所示：

```java
import org.springframework.cache.annotation.Cacheable;
import org.springframework.stereotype.Component;

@Component
public class MathService {

    @Cacheable("piDecimals")
    public int computePiDecimal(int i) {
        // ...
    }

}
```

本示例说明了在潜在的代价高昂操作上使用缓存的方法。在调用 `computePiDecimal` 之前，抽象将在 `piDecimals` 缓存中查找与 `i` 参数匹配的条目。如果找到条目，则缓存中的内容会立即返回给调用方，并且不会调用该方法。否则，将调用该方法，并在返回值之前更新缓存。

> 您还可以透明地使用标准 JSR-107（JCache）注解（例如，`@CacheResult`）。但是，我们强烈建议您不要混合使用 Spring Cache 和 JCache 注解。

如果您不添加任何特定的缓存库，Spring Boot 会自动配置一个 [简单提供程序](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-simple) ，在内存中使用并发映射。需要缓存时（例如上例中的 `piDecimals`），此提供程序将为您创建它。实际上，不建议将简单的提供程序用于生产用途，但是它对于入门并确保您了解功能非常有用。确定要使用的缓存提供程序后，请确保阅读其文档，以了解如何配置应用程序使用的缓存。几乎所有提供程序都要求您显式配置在应用程序中使用的每个缓存。一些提供了一种方法来定制由 `spring.cache.cache-names` 属性定义的默认缓存。

> 也可以透明地 [更新](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/integration.html#cache-annotations-put) 或 [淘汰](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/integration.html#cache-annotations-evict) 来自缓存的数据。

#### 4.12.1. 支持的缓存提供程序

缓存抽象不提供实际的存储，而是依赖于由 `org.springframework.cache.Cache` 和 `org.springframework.cache.CacheManager` 接口实现的抽象。

如果尚未定义类型为 `CacheManager` 或名为 `CacheResolver` 的 `CacheResolver` 的 Bean（请参见 [`CachingConfigurer`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html)），Spring Boot 会尝试检测以下提供程序（按指示的顺序）：

1. [Generic](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-generic)
2. [JCache (JSR-107)](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-jcache) (EhCache 3, Hazelcast, Infinispan, and others)
3. [EhCache 2.x](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-ehcache2)
4. [Hazelcast](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-hazelcast)
5. [Infinispan](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-infinispan)
6. [Couchbase](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-couchbase)
7. [Redis](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-redis)
8. [Caffeine](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-caffeine)
9. [Simple](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-simple)

> 也可以通过设置 `spring.cache.type` 属性来强制特定的缓存提供程序。在某些环境中（例如测试环境），如果您需要 [完全禁用缓存](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-none)，请使用此属性。

> 使用 `spring-boot-starter-cache` “Starter”快速添加基本的缓存依赖项。该启动器引入了 `spring-context-support`。如果手动添加依赖项，则必须包含 `spring-context-support` 才能使用 JCache，EhCache 2.x 或 Caffeine 支持。

如果 `CacheManager` 是由 Spring Boot 自动配置的，则可以通过暴露一个实现 `CacheManagerCustomizer` 接口的 bean，在完全初始化之前进一步调整其配置。下面的示例设置一个标志，表示应将 `null` 值向下传递给基础映射：

```java
@Bean
public CacheManagerCustomizer<ConcurrentMapCacheManager> cacheManagerCustomizer() {
    return new CacheManagerCustomizer<ConcurrentMapCacheManager>() {
        @Override
        public void customize(ConcurrentMapCacheManager cacheManager) {
            cacheManager.setAllowNullValues(false);
        }
    };
}
```

> 在前面的示例中，应该使用自动配置的 `ConcurrentMapCacheManager`。如果不是这种情况（您提供了自己的配置，或者自动配置了其他缓存提供程序），则根本不会调用定制程序。您可以根据需要设置任意数量的定制器，也可以使用 `@Order` 或 `Ordered` 对其进行排序。

##### 通用缓存

如果上下文至少定义了一个 `org.springframework.cache.Cache` bean，则使用通用缓存。创建一个 `CacheManager`，包装所有该类型的 bean。

##### JCache (JSR-107)

[JCache](https://jcp.org/en/jsr/detail?id=107) 通过类路径上的 `javax.cache.spi.CachingProvider` （即类路径上存在的兼容 JSR-107 规范的缓存类库）进行引导，而 `JCacheCacheManager` 由 `spring-boot-starter-cache` “Starter” 提供。提供了各种兼容的库，Spring Boot 为 Ehcache 3，Hazelcast 和 Infinispan 提供了依赖管理。也可以添加任何其他兼容的库。

可能会出现多个提供者，在这种情况下，必须明确指定提供者。即使 JSR-107 标准没有强制采用标准化的方式来定义配置文件的位置，Spring Boot 也会尽其所能以设置带有实现细节的缓存，如以下示例所示：

```properties
# Only necessary if more than one provider is present
spring.cache.jcache.provider=com.acme.MyCachingProvider
spring.cache.jcache.config=classpath:acme.xml
```

> 当缓存库同时提供本机实现和 JSR-107 支持时，Spring Boot 会首选 JSR-107 支持，因此如果您切换到其他 JSR-107 实现，则可以使用相同的功能。

> Spring Boot 具有 [Hazelcast的一般支持](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-hazelcast)。如果单个 `HazelcastInstance` 可用，则除非指定了 `spring.cache.jcache.config` 属性，否则它也会自动被 `CacheManager` 重用。

有两种方法可以自定义基础的 `javax.cache.cacheManager`：

- 可以在启动时通过设置 `spring.cache.cache-names` 属性来创建缓存。如果定义了自定义的 `javax.cache.configuration.Configuration` bean，则用于自定义它们。

- 使用 `CacheManager` 的引用调用 `org.springframework.boot.autoconfigure.cache.JCacheManagerCustomizer` bean 进行完全定制。

> 如果定义了标准的 `javax.cache.CacheManager` bean，它将自动包装在抽象期望的 `org.springframework.cache.CacheManager` 实现中。不再对其进行定制。

##### EhCache 2.x

如果在类路径根目录找到名为 `ehcache.xml` 的文件 [EhCache](https://www.ehcache.org/) 2.x 就会被使用， `EhCacheCacheManager` 由 `spring-boot-starter-cache` “Starter” 提供，用于引导缓存管理器。也可以提供如下的另外一种形式的配置文件：

```properties
spring.cache.ehcache.config=classpath:config/another-config.xml
```

##### Hazelcast

Spring Boot 提供了 [对 Hazelcast 的通用支持](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-hazelcast)。如果已经自动配置了 `HazelcastInstance` ，它就会被自动包装为 `CacheManager`。

##### Infinispan

[Infinispan](https://infinispan.org/) 没有默认的配置文件位置，因此必须显式指定。否则将使用默认引导：

```properties
spring.cache.infinispan.config=infinispan.xml
```

通过设定 `spring.cache.cache-names` 属性，缓存可以在启动期间创建。如果自定义了 `ConfigurationBuilder` bean，它就会被用于自定义缓存。

> Spring Boot 对 Infinispan 的支持仅限于嵌入式模式，并且非常基础。如果您需要更多选择，则应该使用官方的 Infinispan Spring Boot starter。有关更多详细信息，请参见 [Infinispan 文档](https://github.com/infinispan/infinispan-spring-boot)。

##### Couchbase

如果 [Couchbase](https://www.couchbase.com/) Java 客户端和 `couchbase-spring-cache` 实现可用，并且 Couchbase 已 [配置](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-couchbase)，则会自动配置 `CouchbaseCacheManager` 。也可以通过设置 `spring.cache.cache-names` 属性来在启动时创建其他缓存。这些缓存在自动配置的 `Bucket` 上运行。您还可以定制在另一个 `Bucket` 上创建其他缓存。假设您在主 `Bucket` 上需要两个缓存（ `cache1` 和 `cache2`），并且在另一个 `Bucket` 上需要一个（自定义生存时间）为2秒的（ `cache3` ）缓存。您可以通过配置创建前两个缓存，如下所示：

```properties
spring.cache.cache-names=cache1,cache2
```

然后你就可以定义 `@Configuration` 类来配置额外的 `Bucket` 和 `cache3` 缓存，如下所示：

```java
@Configuration(proxyBeanMethods = false)
public class CouchbaseCacheConfiguration {

    private final Cluster cluster;

    public CouchbaseCacheConfiguration(Cluster cluster) {
        this.cluster = cluster;
    }

    @Bean
    public Bucket anotherBucket() {
        return this.cluster.openBucket("another", "secret");
    }

    @Bean
    public CacheManagerCustomizer<CouchbaseCacheManager> cacheManagerCustomizer() {
        return c -> {
            c.prepareCache("cache3", CacheBuilder.newInstance(anotherBucket())
                    .withExpiration(2));
        };
    }

}
```

这个示例配置服用了通过自动配置创建的 `Cluster` 。

##### Redis

如果 [Redis](https://redis.io/) 可用并已配置，则将自动配置 `RedisCacheManager`。通过设置 `spring.cache.cache-names` 属性可以在启动时创建其他缓存，并且可以使用 `spring.cache.redis.*` 属性配置缓存默认值。例如，以下配置将创建 `cache1` 和 `cache2` 缓存，其“生存时间”为10分钟：

```properties
spring.cache.cache-names=cache1,cache2
spring.cache.redis.time-to-live=600000
```

> 默认情况下，会自动添加 key 前缀，以便如果两个单独的缓存使用相同的 key，Redis 中也不会有相同的 key，也不会返回无效值。如果您创建自己的 `RedisCacheManager`，我们强烈建议将此设置保持启用状态。

> 您可以通过添加自己的 `RedisCacheConfiguration` `@Bean` 来完全控制配置。如果您要自定义序列化策略，这可能会很有用。

##### Caffeine

[Caffeine](https://github.com/ben-manes/caffeine) 是对 Guava 缓存的 Java 8 重写，取代了对 Guava 的支持。如果存在 Caffeine，则会自动配置 `CaffeineCacheManager`（由 `spring-boot-starter-cache` “Starter” 提供）。缓存可以在启动时通过设置 `spring.cache.cache-names` 属性来创建，并且可以通过以下方式之一自定义（按指示的顺序）：

1. 由 `spring.cache.caffeine.spec` 定义的缓存规范

2. 定义了一个 `com.github.benmanes.caffeine.cache.CaffeineSpec` bean

3. 定义了一个 `com.github.benmanes.caffeine.cache.Caffeine` bean

例如，以下配置将创建 `cache1` 和 `cache2` 缓存，最大大小为 500，并且“生存时间”为 10 分钟。

```properties
spring.cache.cache-names=cache1,cache2
spring.cache.caffeine.spec=maximumSize=500,expireAfterAccess=600s
```

如果定义了 `com.github.benmanes.caffeine.cache.CacheLoader` Bean，它将自动与 `CaffeineCacheManager` 关联。由于 `CacheLoader` 将与由缓存管理器管理的所有缓存相关联，因此必须将其定义为 `CacheLoader<Object, Object>`。自动配置将忽略任何其他通用类型。

##### 简单缓存

如果找不到其他提供者，则配置一个使用 `ConcurrentHashMap` 作为缓存存储的简单实现。如果您的应用程序中没有缓存库，则这是默认设置。默认情况下，根据需要创建缓存，但是您可以通过设置 `cache-names` 属性来限制可用缓存的列表。例如，如果只需要 `cache1` 和 `cache2` 缓存，则按如下所示设置 `cache-names` 属性：

```properties
spring.cache.cache-names=cache1,cache2
```

如果这样做，并且您的应用程序使用了未列出的缓存，那么当需要该缓存时，它将在运行时失败，但不会在启动时失败。这类似于使用未声明的缓存时“实际”缓存提供程序的行为。

##### 无缓存

当您的配置中存在 `@EnableCaching` 时，也需要合适的缓存配置。如果需要在某些环境中完全禁用缓存，请强制将缓存类型设置为 `none` 以使用无操作实现，如以下示例所示：

```properties
spring.cache.type=none
```

### 4.13. 消息

Spring 框架为与消息系统的集成提供了丰富的支持，从通过使用 `JmsTemplate` 来简化 JMS API 的使用，到异步接收消息的完整机车设施。Spring AMQP 提供了类似于高级消息队列协议的特性集合。Spring Boot 也提供了 `RabbitTemplate` 和 RabbitMQ 的自动配置选项。Spring WebSocket 本身包含 STOMP 消息支持，同时 Spring Boot 通过启动器和少量的自动配置支持该消息。Spring Boot 还支持 Apache Kafka。

#### 4.13.1. JMS

`javax.jms.ConnectionFactory` 接口提供了创建用于与 JMS 代理进行交互的 `javax.jms.Connection` 的标准方法。尽管 Spring 需要 `ConnectionFactory` 来与 JMS 一起使用，但是您通常不需要自己直接使用它，而可以依赖于更高级别的消息抽象。（有关详细信息，请参见 Spring Framework 参考文档的 [相关部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/integration.html#jms)。）Spring Boot 还自动配置了必要的基础设施，以发送和接收消息。

##### ActiveMQ Support

当 [ActiveMQ](https://activemq.apache.org/) 在类路径上可用时，Spring Boot 也能够配置一个 `ConnectionFactory`。如果代理存在，则会自动配置（如果没有通过配置指定代理 URL）并启动一个内置代理。

> 如果你使用 `spring-boot-starter-activemq`，连接或者内置 ActiveMQ 实例所必需的依赖就都提供好了，它们作为 Spring 集成 JMS 的基础设施存在。

ActiveMQ 配置由 `spring.activemq.*` 中的外部配置属性控制。例如，您可以在 `application.properties` 中声明以下部分：

```properties
spring.activemq.broker-url=tcp://192.168.1.210:9876
spring.activemq.user=admin
spring.activemq.password=secret
```

默认情况下，`CachingConnectionFactory` 将本机 `ConnectionFactory` 包装为明智的设置，您可以通过 `spring.jms.*` 中的外部配置属性来控制这些设置：

```properties
spring.jms.cache.session-cache-size=5
```

如果您想使用本机池，则可以通过向 `org.messaginghub:pooled-jms` 添加依赖项并相应地配置 `JmsPoolConnectionFactory` 来实现，如以下示例所示：

```properties
spring.activemq.pool.enabled=true
spring.activemq.pool.max-connections=50
```

> 参考 [`ActiveMQProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jms/activemq/ActiveMQProperties.java) 了解更多支持的选项。你还可以注册任意数量实现了 `ActiveMQConnectionFactoryCustomizer` 的 beans 来实现更高级的定制化。

默认情况下，ActiveMQ 创建一个目的地（如果尚不存在），以便根据其提供的名称解析目的地。

##### Artemis 支持

当 Spring Boot 检测到 [Artemis](https://activemq.apache.org/artemis/) 在类路径上可用时，它可以自动配置一个 `ConnectionFactory`。如果存在代理，则将自动启动和配置嵌入式代理（除非已明确设置 `mode` 属性）。支持的模式为 `embeded`（以明确要求使用嵌入式代理，并且如果代理在类路径上不可用，则会发生错误）和 `native`（使用 `netty` 传输协议连接到代理）。配置后者后，Spring Boot 会配置一个 `ConnectionFactory`，以默认设置连接到在本地计算机上运行的代理。

> 如果使用 `spring-boot-starter-artemis`，则将提供连接到现有 Artemis 实例所需的依赖项，以及与 JMS 集成的 Spring 基础结构。在您的应用程序中添加 `org.apache.activemq:artemis-jms-server` 可以使您使用嵌入式模式。

Artemis 配置由 `spring.artemis.*` 中的外部配置属性控制。例如，您可以在 `application.properties` 中声明以下部分：

```properties
spring.artemis.mode=native
spring.artemis.host=192.168.1.210
spring.artemis.port=9876
spring.artemis.user=admin
spring.artemis.password=secret
```

嵌入代理时，可以选择是否要启用持久性并列出应使其可用的目的地。可以将它们指定为以逗号分隔的列表，以使用默认选项创建它们，或者您可以定义类型为 `org.apache.activemq.artemis.jms.server.config.JMSQueueConfiguration` 或 `org.apache.activemq.artemis.jms.server.config.TopicConfiguration` 的 bean，分别用于高级队列和主题配置。

默认情况下，`CachingConnectionFactory` 将本机 `ConnectionFactory` 包装为明智的设置，您可以通过 `spring.jms.*` 中的外部配置属性来控制这些设置：

```properties
spring.jms.cache.session-cache-size=5
```

如果您想使用本机池，则可以通过向 `org.messaginghub:pooled-jms` 添加依赖项并相应地配置 `JmsPoolConnectionFactory` 来实现，如以下示例所示：

```properties
spring.artemis.pool.enabled=true
spring.artemis.pool.max-connections=50
```

参考 [`ArtemisProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jms/artemis/ArtemisProperties.java) 了解更多支持的选项。

不涉及 JNDI 查找，并且使用 Artemis 配置中的 `name` 属性或通过配置提供的名称来根据目的地名称解析目的地。

##### 使用 JNDI ConnectionFactory

如果你要在应用服务器上运行你的应用，Spring Boot 就会尝试使用 JNDI 寻找 JMS `ConnectionFactory` 。默认情况下，会检查 `java:/JmsXA` 和 `java:/XAConnectionFactory` 这两个位置。你可以使用 `spring.jms.jndi-name` 属性来指定别的位置。如下面例子所示：

```properties
spring.jms.jndi-name=java:/MyConnectionFactory
```

##### 发送消息

Spring 的 `JmsTemplate` 会被自动配置，你可以直接将其注入自己的 beans，如下面例子所示：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jms.core.JmsTemplate;
import org.springframework.stereotype.Component;

@Component
public class MyBean {

    private final JmsTemplate jmsTemplate;

    @Autowired
    public MyBean(JmsTemplate jmsTemplate) {
        this.jmsTemplate = jmsTemplate;
    }

    // ...

}
```

> [`JmsMessagingTemplate`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/jms/core/JmsMessagingTemplate.html) 能够通过类似的方式注入。如果定义了 `DestinationResolver` 或者 `MessageConverter` bean，它们就会自动联系到自动配置的 `JmsTemplate`。

##### 接收消息

存在 JMS 基础设施时，可以使用 `@JmsListener` 注解任何 bean 以创建侦听器端点。如果未定义 `JmsListenerContainerFactory`，则会自动配置一个默认值。如果定义了 `DestinationResolver` 或 `MessageConverter` bean，则它们将自动关联到默认工厂。

默认情况下，默认工厂是事务性的。如果您在存在 `JtaTransactionManager` 的基础架构中运行，则默认情况下将其关联到侦听器容器。如果不是，则启用 `sessionTransacted` 标志。在后一种情况下，可以通过在侦听器方法（或其委托）上添加 `@Transactional` 来将本地数据存储事务与传入消息的处理相关联。这样可以确保本地事务完成后，传入消息得到确认。这还包括发送已在同一 JMS 会话上执行的响应消息。

以下组件在 `someQueue` 目标上创建侦听器端点：

```java
@Component
public class MyBean {

    @JmsListener(destination = "someQueue")
    public void processMessage(String content) {
        // ...
    }

}
```

> 参考 [the Javadoc of `@EnableJms`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/jms/annotation/EnableJms.html) 获取更多细节。

如果您需要创建更多的 `JmsListenerContainerFactory` 实例，或者想要覆盖默认实例，Spring Boot 提供了 `DefaultJmsListenerContainerFactoryConfigurer` ，您可以使用与自动配置相同的设置来初始化 `DefaultJmsListenerContainerFactory`。

例如，以下示例公开了另一个工厂，该工厂使用特定的 `MessageConverter`：

```java
@Configuration(proxyBeanMethods = false)
static class JmsConfiguration {

    @Bean
    public DefaultJmsListenerContainerFactory myFactory(
            DefaultJmsListenerContainerFactoryConfigurer configurer) {
        DefaultJmsListenerContainerFactory factory =
                new DefaultJmsListenerContainerFactory();
        configurer.configure(factory, connectionFactory());
        factory.setMessageConverter(myMessageConverter());
        return factory;
    }

}
```

然后，您可以在任何带有 `@JmsListener` 注解的方法中使用该工厂，如下所示：

```java
@Component
public class MyBean {

    @JmsListener(destination = "someQueue", containerFactory="myFactory")
    public void processMessage(String content) {
        // ...
    }

}
```

#### 4.13.2. AMQP

高级消息队列协议（AMQP）是面向消息中间件的与平台无关的有线级别协议。Spring AMQP 项目将 Spring 的核心概念应用于基于 AMQP 的消息传递解决方案的开发。Spring Boot 为通过 RabbitMQ 使用 AMQP 提供了许多便利，包括 `spring-boot-starter-amqp` “Starter”。

##### RabbitMQ 支持

[RabbitMQ](https://www.rabbitmq.com/) 时一个轻量级的，可靠的，可扩展的，可移植的消息代理，基于 AMQP 协议。Spring 使用 `RabbitMQ` 来通过 AMQP 协议进行通信。

RabbitMQ 配置由 `spring.rabbitmq.*` 中的外部配置属性控制。例如，您可以在 `application.properties` 中声明以下部分：

```properties
spring.rabbitmq.host=localhost
spring.rabbitmq.port=5672
spring.rabbitmq.username=admin
spring.rabbitmq.password=secret
```

另外，你可以使用 `addresses` 属性来配置相同的连接：

```properties
spring.rabbitmq.addresses=amqp://admin:secret@localhost
```

如果上下文中存在一个 `ConnectionNameStrategy` bean，它将被自动用来命名由自动配置的 `ConnectionFactory` 创建的连接。参见 [`RabbitProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/amqp/RabbitProperties.java) 以获取更多受支持的选项。

> 参考 [Understanding AMQP, the protocol used by RabbitMQ](https://spring.io/blog/2010/06/14/understanding-amqp-the-protocol-used-by-rabbitmq/) 获取更多细节。

##### 发送消息

Spring 的 `AmqpTemplate` 和 `AmqpAdmin` 都是自动配置的，你可以直接将其注入自己的 beans，如下面例子所示：

```java
import org.springframework.amqp.core.AmqpAdmin;
import org.springframework.amqp.core.AmqpTemplate;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Component;

@Component
public class MyBean {

    private final AmqpAdmin amqpAdmin;
    private final AmqpTemplate amqpTemplate;

    @Autowired
    public MyBean(AmqpAdmin amqpAdmin, AmqpTemplate amqpTemplate) {
        this.amqpAdmin = amqpAdmin;
        this.amqpTemplate = amqpTemplate;
    }

    // ...

}
```

> [`RabbitMessagingTemplate`](https://docs.spring.io/spring-amqp/docs/2.2.2.RELEASE/api/org/springframework/amqp/rabbit/core/RabbitMessagingTemplate.html) 可以通过类似方式注入。如果定义了 `MessageConverter` bean，它就会自动联系到自动配置的 `AmqpTemplate`。

如有必要，任何定义为 bean 的 `org.springframework.amqp.core.Queue` 都会自动用于在 RabbitMQ 实例上声明相应的队列。

要重试操作，可以在 `AmqpTemplate` 上启用重试（例如，在代理连接丢失的情况下）：

```properties
spring.rabbitmq.template.retry.enabled=true
spring.rabbitmq.template.retry.initial-interval=2s
```

默认是禁用重试的。你也可以通过声明 `RabbitRetryTemplateCustomizer` bean 来以编程方式自定义 `RetryTemplate` 。

##### 接收消息

当存在 Rabbit 基础设施时，可以使用 `@RabbitListener` 注解任何 bean 以创建侦听器端点。如果未定义 `RabbitListenerContainerFactory`，则会自动配置默认的 `SimpleRabbitListenerContainerFactory`，您可以使用 `spring.rabbitmq.listener.type` 属性切换到直接容器。如果定义了一个 `MessageConverter` 或 `MessageRecoverer` bean，它将自动与默认工厂关联。

以下示例组件在 `someQueue` 队列上创建一个侦听器端点：

```java
@Component
public class MyBean {

    @RabbitListener(queues = "someQueue")
    public void processMessage(String content) {
        // ...
    }

}
```

> 参考 [the Javadoc of `@EnableRabbit`](https://docs.spring.io/spring-amqp/docs/2.2.2.RELEASE/api/org/springframework/amqp/rabbit/annotation/EnableRabbit.html) 获取更多细节。

如果您需要创建更多的 `RabbitListenerContainerFactory` 实例，或者想要覆盖默认实例，Spring Boot 提供了 `SimpleRabbitListenerContainerFactoryConfigurer` 和 `DirectRabbitListenerContainerFactoryConfigurer`，您可以使用它们初始化具有相同设置的 `SimpleRabbitListenerContainerFactory` 和 `DirectRabbitListenerContainerFactory`  作为自动配置使用的工厂。

> 选择哪种容器都没有关系。 这两个 bean 通过自动配置公开。

例如，以下配置类公开了另一个使用特定 `MessageConverter` 的工厂：

```java
@Configuration(proxyBeanMethods = false)
static class RabbitConfiguration {

    @Bean
    public SimpleRabbitListenerContainerFactory myFactory(
            SimpleRabbitListenerContainerFactoryConfigurer configurer) {
        SimpleRabbitListenerContainerFactory factory =
                new SimpleRabbitListenerContainerFactory();
        configurer.configure(factory, connectionFactory);
        factory.setMessageConverter(myMessageConverter());
        return factory;
    }

}
```

然后，您可以在任何带有 `@RabbitListener` 注解的方法中使用工厂，如下所示：

```java
@Component
public class MyBean {

    @RabbitListener(queues = "someQueue", containerFactory="myFactory")
    public void processMessage(String content) {
        // ...
    }

}
```

您可以启用重试以处理侦听器引发异常的情况。默认情况下，使用 `RejectAndDontRequeueRecoverer`，但是您可以定义自己的 `MessageRecoverer`。重试用尽后，如果将代理配置为这样做，则消息将被拒绝并被丢弃或路由到死信队列。默认情况下，重试是禁用的。您还可以通过声明 `RabbitRetryTemplateCustomizer` bean 来以编程方式自定义 `RetryTemplate`。

> 默认情况下，如果禁用了重试，并且侦听器引发了异常，则会无限期地重试传递。您可以通过两种方式修改此行为：将 `defaultRequeueRejected` 属性设置为 `false`，以便尝试进行零次重新传递，或者抛出 `AmqpRejectAndDontRequeueException` 来指示应拒绝该消息。后者是启用重试并达到最大传递尝试次数时使用的机制。

#### 4.13.3. Apache Kafka 支持

[Apache Kafka](https://kafka.apache.org/) 通过提供 `spring-kafka` 项目的自动配置而被支持。

Kafka 配置由 `spring.kafka.*` 中的外部配置属性控制。比如，你可能会在 `application.properties` 中声明下面的内容：

```properties
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.consumer.group-id=myGroup
```

> 想要在启动时创建主题，请添加一个 `NewTopic` 类型的 bean。如果该主题已经存在，该 bean 就会被忽略。

参考 [`KafkaProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/kafka/KafkaProperties.java) 了解更多支持的选项。

##### 发送消息

Spring 的 `KafkaTemplate` 自动配置，你可以直接将其注入自己的 beans 中，如下面例子所示：

```java
@Component
public class MyBean {

    private final KafkaTemplate kafkaTemplate;

    @Autowired
    public MyBean(KafkaTemplate kafkaTemplate) {
        this.kafkaTemplate = kafkaTemplate;
    }

    // ...

}
```

> 如果定义了 `spring.kafka.producer.transaction-id-prefix` 属性， `KafkaTransactionManager` 就会被自动配置。同时，如果定义了 `RecordMessageConverter` bean，它就会自动关联到自动配置好的 `KafkaTemplate`。

##### 接收消息

存在 Apache Kafka 基础结构时，可以使用 `@KafkaListener` 注解任何 bean，以创建侦听器端点。如果未定义 `KafkaListenerContainerFactory`，则会使用 `spring.kafka.listener.*` 中定义的键自动配置默认值。

以下组件在 `someTopic` 主题上创建侦听器端点：

```java
@Component
public class MyBean {

    @KafkaListener(topics = "someTopic")
    public void processMessage(String content) {
        // ...
    }

}
```

如果定义了 `KafkaTransactionManager` bean，它将自动与容器工厂关联。类似地，如果定义了 `ErrorHandler`，`AfterRollbackProcessor` 或 `ConsumerAwareRebalanceListener` bean，它将自动与默认工厂关联。

根据侦听器的类型，`RecordMessageConverter` 或 `BatchMessageConverter` Bean与默认工厂关联。如果批处理侦听器仅存在一个 `RecordMessageConverter` Bean，则将其包装在 `BatchMessageConverter` 中。

> 自定义的 `ChainedKafkaTransactionManager` 必须标记为 `@Primary`，因为它通常引用自动配置的 `KafkaTransactionManager` bean。

##### Kafka Streams

为了使用 Apache Kafka，Spring 提供了一个工厂 bean 来创建 `StreamsBuilder` 对象并管理其流的生命周期。只要在类路径上存在 `kafka-streams`，并且通过 `@EnableKafkaStreams` 注解启用了 Kafka Streams，Spring Boot 就会自动配置所需的 `KafkaStreamsConfiguration` bean。

启用 Kafka Streams 意味着必须设置应用程序 ID 和引导服务器。可以使用 `spring.kafka.streams.application-id` 来配置前者，如果未设置，则默认为 `spring.application.name`。后者可以全局设置，也可以仅针对流进行覆盖。

使用专用属性可以使用几个附加属性。可以使用 `spring.kafka.streams.properties` 命名空间设置其他任意 Kafka 属性。另请参阅 [其他Kafka属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-kafka-extra-props)。

为了使用该工厂 bean，可以简单地将 `StreamsBuilder` 包装进入你的 `@Bean` 类，如下面例子所示：

```java
@Configuration(proxyBeanMethods = false)
@EnableKafkaStreams
public static class KafkaStreamsExampleConfiguration {

    @Bean
    public KStream<Integer, String> kStream(StreamsBuilder streamsBuilder) {
        KStream<Integer, String> stream = streamsBuilder.stream("ks1In");
        stream.map((k, v) -> new KeyValue<>(k, v.toUpperCase())).to("ks1Out",
                Produced.with(Serdes.Integer(), new JsonSerde<>()));
        return stream;
    }

}
```

默认情况下，由它创建的 `StreamBuilder `对象管理的流会自动启动。您可以使用 `spring.kafka.streams.auto-startup` 属性来自定义此行为。

##### 附加 Kafka 属性

自动配置支持的属性展示在 [通用应用程序属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#common-application-properties) 中。请注意，在大多数情况下，这些属性（连字符连接的或驼峰记号表示）直接映射到 Apache Kafka 点连接的属性。有关详细信息，请参阅 Apache Kafka 文档。

这些属性的前几个属性适用于所有组件（生产者，使用者，管理器和流），但如果您希望使用不同的值，则可以在组件级别指定。 Apache Kafka 会指定重要性为 HIGH，MEDIUM 或 LOW 的属性。 Spring Boot 自动配置支持所有 HIGH 重要性属性，一些选定的 MEDIUM 和 LOW 属性以及任何没有默认值的属性。

通过 `KafkaProperties` 类可以直接使用 Kafka 支持的属性的子集。如果您希望使用不直接支持的其他属性来配置生产者或使用者，请使用以下属性：

```properties
spring.kafka.properties.prop.one=first
spring.kafka.admin.properties.prop.two=second
spring.kafka.consumer.properties.prop.three=third
spring.kafka.producer.properties.prop.four=fourth
spring.kafka.streams.properties.prop.five=fifth
```

这将常见的 `prop.one` Kafka 属性设置为 `first`（适用于生产者，消费者和管理员），将 `prop.two` admin 属性设置为 `second`，将 `prop.three` 消费者属性设置为 `Third`。将 `prop.four` 生产者属性设置为 `fourth`，将 `prop.five` 流属性设置为 `fifth`。

您还可以如下配置 Spring Kafka `JsonDeserializer`：

```properties
spring.kafka.consumer.value-deserializer=org.springframework.kafka.support.serializer.JsonDeserializer
spring.kafka.consumer.properties.spring.json.value.default.type=com.example.Invoice
spring.kafka.consumer.properties.spring.json.trusted.packages=com.example,org.acme
```

同样，您可以禁用在报头中发送类型信息的 `JsonSerializer` 默认行为：

```properties
spring.kafka.producer.value-serializer=org.springframework.kafka.support.serializer.JsonSerializer
spring.kafka.producer.properties.spring.json.add.type.headers=false
```

> 以这种方式设置的属性将覆盖 Spring Boot 显式支持的任何配置项。

##### 使用嵌入式 Kafka 进行测试

Spring 为 Apache Kafka 提供了一种使用嵌入式 Apache Kafka 代理测试项目的便捷方法。要使用此功能，请用 `spring-kafka-test` 模块的 `@EmbeddedKafka` 注解测试类。有关更多信息，请参见 [Spring for Apache Kafka 参考手册](https://docs.spring.io/spring-kafka/docs/current/reference/html/#embedded-kafka-annotation)。

要使 Spring Boot 自动配置与上述嵌入式 Apache Kafka 代理一起使用，您需要将嵌入式代理地址（由 `EmbeddedKafkaBroker` 填充）的系统属性重新映射到 Apache Kafka 的 Spring Boot 配置属性中。有几种方法可以做到这一点：

- 提供一个系统属性，以将嵌入式代理地址映射到测试类中的 `spring.kafka.bootstrap-servers` 中：

```java
static {
    System.setProperty(EmbeddedKafkaBroker.BROKER_LIST_PROPERTY, "spring.kafka.bootstrap-servers");
}
```

- 在 `@EmbeddedKafka` 注解上配置属性名称：

```java
@EmbeddedKafka(topics = "someTopic",
        bootstrapServersProperty = "spring.kafka.bootstrap-servers")
```

- 在配置属性中使用占位符：

```properties
spring.kafka.bootstrap-servers=${spring.embedded.kafka.brokers}
```

### 4.14. 使用 `RestTemplate` 调用 REST 服务 

如果你的应用需要调用远程 REST 服务，你可以使用 Spring 框架的 [`RestTemplate`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html) 类。由于 [`RestTemplate`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html) 在使用之前通常都需要进行定制，Spring Boot 不提供任何单独自动配置的 [`RestTemplate`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/web/client/RestTemplate.html) bean。不过，它提供了一个自动配置好的 `RestTemplateBuilder` ，它可以被用来在需要的时候创建 `RestTemplate` 实例。自动配置的 `RestTemplateBuilder` 保证了合适的 `HttpMessageConverters` 被应用于 `RestTemplate` 实例。

下面的代码是个典型的示例：

```java
@Service
public class MyService {

    private final RestTemplate restTemplate;

    public MyService(RestTemplateBuilder restTemplateBuilder) {
        this.restTemplate = restTemplateBuilder.build();
    }

    public Details someRestCall(String name) {
        return this.restTemplate.getForObject("/{name}/details", Details.class, name);
    }

}
```

> `RestTemplateBuilder` 包含大量有用的方法，可以用来快速配置 `RestTemplate` 实例。比如，要添加 BASIC 身份认证支持，你可以使用 `builder.basicAuthentication("user", "password").build()`。

#### 4.14.1. RestTemplate 定制

可以通过三种方法定制 `RestTemplate` ，采用哪种方法取决于你想在何种范围上定制。

为了使任何自定义的范围尽可能狭窄，请注入自动配置的 `RestTemplateBuilder`，然后根据需要调用其方法。每个方法调用都会返回一个新的 `RestTemplateBuilder` 实例，因此自定义设置仅会影响构建器的使用。

要进行整个应用程序的附加定制，请使用 `RestTemplateCustomizer` bean。所有这些 bean 都会自动注册到自动配置的 `RestTemplateBuilder` 中，并应用于使用它构建的任何模板。

以下示例显示了一个定制器，该定制器为除 `192.168.0.5` 之外的所有主机配置代理的使用：

```java
static class ProxyCustomizer implements RestTemplateCustomizer {

    @Override
    public void customize(RestTemplate restTemplate) {
        HttpHost proxy = new HttpHost("proxy.example.com");
        HttpClient httpClient = HttpClientBuilder.create().setRoutePlanner(new DefaultProxyRoutePlanner(proxy) {

            @Override
            public HttpHost determineProxy(HttpHost target, HttpRequest request, HttpContext context)
                    throws HttpException {
                if (target.getHostName().equals("192.168.0.5")) {
                    return null;
                }
                return super.determineProxy(target, request, context);
            }

        }).build();
        restTemplate.setRequestFactory(new HttpComponentsClientHttpRequestFactory(httpClient));
    }

}
```

最后，最极端（很少使用）的选项是创建自己的 `RestTemplateBuilder` bean。这样做会关闭 `RestTemplateBuilder` 的自动配置，并阻止使用任何 `RestTemplateCustomizer` bean。

### 4.15. 使用 `WebClient` 调用 REST 服务

如果您的类路径中包含 Spring WebFlux，则还可以选择使用 `WebClient` 来调用远程 REST 服务。与 `RestTemplate` 相比，此客户端具有更多的功能感，并且具有完全的反应性。您可以在 Spring Framework 文档的 [专用部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web-reactive.html#webflux-client) 中了解有关 WebClient 的更多信息。

Spring Boot 为您创建并预配置了 `WebClient.Builder`。强烈建议将其注入您的组件中，并使用它来创建 `WebClient` 实例。Spring Boot 配置该构建器以共享 HTTP 资源，以与服务器相同的方式反映编解码器的设置（请参阅 [WebFlux HTTP编解码器自动配置](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-webflux-httpcodecs)）等。

下面的代码展示了典型的示例：

```java
@Service
public class MyService {

    private final WebClient webClient;

    public MyService(WebClient.Builder webClientBuilder) {
        this.webClient = webClientBuilder.baseUrl("https://example.org").build();
    }

    public Mono<Details> someRestCall(String name) {
        return this.webClient.get().uri("/{name}/details", name)
                        .retrieve().bodyToMono(Details.class);
    }

}
```

#### 4.15.1. WebClient Runtime

Spring Boot 将根据应用程序类路径上可用的库自动检测要使用哪个 `ClientHttpConnector` 来驱动 `WebClient`。目前，还支持 Reactor Netty 和 Jetty RS 客户端。

`spring-boot-starter-webflux` 启动器默认情况下依赖于 `io.projectreactor.netty:reactor-netty`，这带来了服务器和客户端的实现。如果您选择使用 Jetty 作为反应式服务器，则应在 Jetty 反应式 HTTP 客户端库 `org.eclipse.jetty:jetty-reactive-httpclient` 上添加依赖项。对服务器和客户端使用相同的技术具有其优势，因为它将自动在客户端和服务器之间共享 HTTP 资源。

通过提供自定义的 `ReactorResourceFactory` 或 `JettyResourceFactory` bean，开发人员可以覆盖 Jetty 和 Reactor Netty 的资源配置—这将同时应用于客户端和服务器。

如果您希望为客户端覆盖该选择，则可以定义自己的 `ClientHttpConnector` bean，并完全控制客户端配置。

了解更多信息请参考 [`WebClient` 配置选项](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/web-reactive.html#webflux-client-builder)。

#### 4.15.2. WebClient 定制

`WebClient` 自定义有三种主要方法，具体取决于您希望自定义应用的范围。

为了使所有定制的范围尽可能狭窄，请注入自动配置的 `WebClient.Builder`，然后根据需要调用其方法。`WebClient.Builder` 实例是有状态的：构建器上的任何更改都会反映在随后使用它创建的所有客户端中。如果要使用同一构建器创建多个客户端，则还可以考虑使用 `WebClient.Builder other = builder.clone();` 克隆该构建器。

为了对所有 `WebClient.Builder` 实例进行应用范围的附加自定义，您可以声明 `WebClientCustomizer` bean 并在注入时在本地更改 `WebClient.Builder`。

最后，您可以使用原始 API 并使用 `WebClient.create()`。在这种情况下，不会应用任何自动配置或 `WebClientCustomizer`。

### 4.16. 验证

只要 JSR-303 实现（例如 Hibernate 验证器）位于类路径上，就会自动启用 Bean 验证 1.1 支持的方法验证功能。这样就可以在 bean 方法的参数和/或返回值上使用 `javax.validation` 约束对它们进行注解。具有此类注解方法的目标类需要在类型级别使用 `@Validated` 注解进行修饰，以便在其方法中搜索内联约束注解。

例如，以下服务触发第一个参数的验证，确保其大小在 8 到 10 之间：

```java
@Service
@Validated
public class MyBean {

    public Archive findByCodeAndAuthor(@Size(min = 8, max = 10) String code,
            Author author) {
        ...
    }

}
```

### 4.17. 发送邮件

Spring 框架通过使用 `JavaMailSender` 接口提供了用于发送电子邮件的简单抽象，Spring Boot 为它提供了自动配置以及启动程序模块。

> 参考 [reference documentation](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/integration.html#mail) 了解 `JavaMailSender` 使用方法的详细介绍。

如果有 `spring.mail.host` 和相关的库（由 `spring-boot-starter-mail` 定义）可用，则如果不存在默认的 `JavaMailSender`，则会创建该库。可以通过 `spring.mail` 命名空间中的配置项进一步定制发送者。参见 [`MailProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/mail/MailProperties.java) 以获取更多详细信息。

特别是，某些默认超时值是无限的，您可能需要更改该值，以避免线程被无响应的邮件服务器阻止，如以下示例所示：

```properties
spring.mail.properties.mail.smtp.connectiontimeout=5000
spring.mail.properties.mail.smtp.timeout=3000
spring.mail.properties.mail.smtp.writetimeout=5000
```

也可以使用来自 JNDI 的现有 `Session` 来配置 `JavaMailSender`：

```properties
spring.mail.jndi-name=mail/Session
```

设置 `jndi-name` 时，它优先于所有其他与 `Session` 相关的设置。

### 4.18. JTA 的分布式事务

Spring Boot 通过使用 [Atomikos](https://www.atomikos.com/) 或 [Bitronix](https://github.com/bitronix/btm) 嵌入式事务管理器，支持跨多个 XA 资源的分布式 JTA 事务。部署到合适的 Java EE 应用程序服务器时，还支持 JTA 事务。

检测到 JTA 环境后，将使用 Spring 的 `JtaTransactionManager` 来管理事务。自动配置的 JMS，DataSource 和 JPA Bean 已升级为支持 XA 事务。您可以使用标准的 Spring 习语（例如 `@Transactional`）来参与分布式事务。如果您在 JTA 环境中，但仍要使用本地事务，则可以将 `spring.jta.enabled` 属性设置为 `false`，以禁用 JTA 自动配置。

#### 4.18.1. 使用 Atomikos 事务管理器

[Atomikos](https://www.atomikos.com/) 是一种流行的开源事务管理器，可以嵌入到您的 Spring Boot 应用程序中。您可以使用 `spring-boot-starter-jta-atomikos` 启动器引入相应的 Atomikos 库。Spring Boot 自动配置 Atomikos，并确保将适当的 `depends-on` 设置应用于您的 Spring bean，以保证正确的启动和关闭顺序。

默认情况下，Atomikos 事务日志将写入应用程序主目录（应用程序 jar 文件所在的目录）中的 `transaction-logs` 目录。您可以通过在 `application.properties` 文件中设置一个 `spring.jta.log-dir` 属性来定制该目录的位置。以 `spring.jta.atomikos.properties` 开头的属性也可以用于自定义 Atomikos 的 `UserTransactionServiceImp`。请参阅 [`AtomikosProperties` Javadoc](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/jta/atomikos/AtomikosProperties.html) 了解更多细节。

> 为了确保多个事务管理器可以安全地协调同一资源管理器，必须为每个 Atomikos 实例配置一个唯一的 ID。默认情况下，此 ID 是运行 Atomikos 的计算机的 IP 地址。为了确保生产中的唯一性，应为应用程序的每个实例将 `spring.jta.transaction-manager-id` 属性配置为不同的值。

#### 4.18.2. 使用 Bitronix 事务管理器

[Bitronix](https://github.com/bitronix/btm) 是一种流行的开源 JTA 事务管理器实现。您可以使用 `spring-boot-starter-jta-bitronix` 启动器将适当的 Bitronix 依赖项添加到您的项目中。与 Atomikos 一样，Spring Boot 自动配置 Bitronix 并对您的 bean 进行后处理，以确保启动和关闭顺序正确。

默认情况下，Bitronix 事务日志文件（`part1.btm` 和 `part2.btm`）被写入应用程序主目录中的 `transaction-logs` 目录。您可以通过设置 `spring.jta.log-dir` 属性来定制该目录的位置。以 `spring.jta.bitronix.properties` 开头的属性也绑定到 `bitronix.tm.Configuration` bean上，以实现完全自定义。有关详细信息，请参见 [Bitronix文档](https://github.com/bitronix/btm/wiki/Transaction-manager-configuration)。

> 为了确保多个事务管理器可以安全地协调同一资源管理器，必须为每个 Bitronix 实例配置唯一的 ID。默认情况下，此 ID 是运行 Bitronix 的计算机的 IP 地址。为了确保生产中的唯一性，应为应用程序的每个实例将 `spring.jta.transaction-manager-id` 属性配置为不同的值。

#### 4.18.3. 使用 Java EE 管理的事务管理器

如果将 Spring Boot 应用程序打包为 `war` 或 `ear` 文件并将其部署到 Java EE 应用程序服务器，则可以使用应用程序服务器的内置事务管理器。Spring Boot 尝试通过查看常见的 JNDI 位置（例如 `java:comp/UserTransaction`，`java:comp/TransactionManager` 等）来自动配置事务管理器。如果您使用应用程序服务器提供的事务服务，则通常还需要确保所有资源都由服务器管理并通过 JNDI 公开。Spring Boot 尝试通过在 JNDI 路径（`java:/JmsXA` 或 `java:/XAConnectionFactory`）中查找 `ConnectionFactory` 来尝试自动配置 JMS，并且您可以使用 [`spring.datasource.jndi-name` 属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-connecting-to-a-jndi-datasource) 来配置您的 `DataSource`。

#### 4.18.4. 混合 XA 和非 XA JMS 连接

当使用 JTA 时，主要的 JMS `ConnectionFactory` bean 是 XA 感知的，并参与分布式事务。在某些情况下，您可能想通过使用非 XA `ConnectionFactory` 处理某些 JMS 消息。例如，您的 JMS 处理逻辑可能需要比 XA 超时更长的时间。

如果要使用非 XA 的 `ConnectionFactory`，则可以注入 `nonXaJmsConnectionFactory` bean 而不是 `@Primary` `jmsConnectionFactory` bean。为了保持一致性，还使用 bean 别名 `xaJmsConnectionFactory` 提供了 `jmsConnectionFactory` bean。

以下示例显示了如何注入 `ConnectionFactory` 实例：

```java
// Inject the primary (XA aware) ConnectionFactory
@Autowired
private ConnectionFactory defaultConnectionFactory;

// Inject the XA aware ConnectionFactory (uses the alias and injects the same as above)
@Autowired
@Qualifier("xaJmsConnectionFactory")
private ConnectionFactory xaConnectionFactory;

// Inject the non-XA aware ConnectionFactory
@Autowired
@Qualifier("nonXaJmsConnectionFactory")
private ConnectionFactory nonXaConnectionFactory;
```

#### 4.18.5. 支持替代嵌入式事务管理器

[`XAConnectionFactoryWrapper`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jms/XAConnectionFactoryWrapper.java) 和 [`XADataSourceWrapper`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jdbc/XADataSourceWrapper.java) 接口可用于支持其他嵌入式事务管理器。这些接口负责包装 `XAConnectionFactory` 和 `XADataSource` bean，并将它们作为常规的 `ConnectionFactory` 和 `DataSource` bean公开，它们透明地注册在分布式事务中。数据源和 JMS 自动配置使用 JTA 变体，前提是您具有 `JtaTransactionManager` bean 和在 `ApplicationContext` 中注册的适当 XA 包装 bean。

[BitronixXAConnectionFactoryWrapper](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jta/bitronix/BitronixXAConnectionFactoryWrapper.java) 和 [BitronixXADataSourceWrapper](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jta/bitronix/BitronixXADataSourceWrapper.java) 提供了有关如何编写 XA 包装器的良好示例。

### 4.19. Hazelcast

如果 [Hazelcast](https://hazelcast.com/) 位于类路径上，并且找到了合适的配置，则 Spring Boot 会自动配置一个 `HazelcastInstance`，您可以将其注入应用程序中。

如果定义 `com.hazelcast.config.Config` bean，Spring Boot 会使用它。如果您的配置定义了一个实例名称，Spring Boot 会尝试查找现有实例，而不是创建一个新实例。

您还可以指定通过配置使用的 Hazelcast 配置文件，如以下示例所示：

```
spring.hazelcast.config=classpath:config/my-hazelcast.xml
```

否则，Spring Boot 会尝试从默认位置查找 Hazelcast 配置：工作目录中或类路径根目录中的 `hazelcast.xml`，或相同位置中的 `.yaml` 副本。我们还将检查 `hazelcast.config` 系统属性是否已设置。有关更多详细信息，请参见 [Hazelcast文档](https://docs.hazelcast.org/docs/latest/manual/html-single/)。

如果在类路径中存在 `hazelcast-client`，Spring Boot 首先尝试通过检查以下配置选项来创建客户端：

- `com.hazelcast.client.config.ClientConfig` bean的存在。
- 由 `spring.hazelcast.config` 属性定义的配置文件。
- `hazelcast.client.config` 系统属性的存在。
- 工作目录中或类路径根目录中的 `hazelcast-client.xml`。
- 工作目录中或类路径根目录中的 `hazelcast-client.yaml`。

> Spring Boot 还具有 [对 Hazelcast 的显式缓存支持](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/htmlsingle/#boot-features-caching-provider-hazelcast)。 如果启用了缓存，则 `HazelcastInstance` 将自动包装在 `CacheManager` 实现中。

### 4.20. Quartz 调度器

Spring Boot 为使用 [Quartz Scheduler](https://www.quartz-scheduler.org/) 提供了许多便利，其中包括 `spring-boot-starter-quartz` “Starter”。如果 Quartz 可用，则自动配置 `Scheduler`（通过 `SchedulerFactoryBean` 抽象）。

以下类型的 Bean 将自动被拾取并与 `Scheduler` 相关联：

- `JobDetail` ：定义特定工作。 `JobDetail` 实例可以使用 `JobBuilder` API 构建。
- `Calendar`。
- `Trigger` ：定义特定工作何时被激活。

默认情况下，使用内存中的 `JobStore`。但是，如果应用程序中有可用的 `DataSource` bean，并且如果相应地配置了 `spring.quartz.job-store-type` 属性，则可以配置基于 JDBC 的存储，如以下示例所示：

```properties
spring.quartz.job-store-type=jdbc
```

使用 JDBC 存储时，可以在启动时初始化模式，如以下示例所示：

```properties
spring.quartz.jdbc.initialize-schema=always
```

> 默认情况下，使用 Quartz 库随附的标准脚本检测并初始化数据库。这些脚本删除现有表，并在每次重新启动时删除所有触发器。也可以通过设置 `spring.quartz.jdbc.schema` 属性来提供自定义脚本。

为了让 Quartz 使用应用程序的主 `DataSource` 之外的 `DataSource`，声明一个 `DataSource` bean，并用 `@QuartzDataSource` 标注其 `@Bean` 方法。这样可以确保 `SchedulerFactoryBean` 和 `Schema` 初始化都使用特定于 Quartz 的 `DataSource`。

默认情况下，通过配置创建的作业将不会覆盖从持久性作业存储中读取的已注册作业。为了覆盖现有的工作定义，设置 `spring.quartz.overwrite-existing-jobs` 属性。

可以使用 `spring.quartz` 属性和 `SchedulerFactoryBeanCustomizer` bean来定制 Quartz Scheduler 配置，这允许以编程方式自定义 `SchedulerFactoryBean`。可以使用 `spring.quartz.properties.*` 自定义高级 Quartz 配置属性。

> 特别是，`Executor` bean 与调度程序没有关联，因为 Quartz 通过 `spring.quartz.properties` 提供了一种配置调度程序的方法。如果您需要自定义任务执行器，请考虑实现 `SchedulerFactoryBeanCustomizer`。

作业可以定义设置器以注入数据映射属性。常规 bean 也可以类似的方式注入，如以下示例所示：

```java
public class SampleJob extends QuartzJobBean {

    private MyService myService;

    private String name;

    // Inject "MyService" bean
    public void setMyService(MyService myService) { ... }

    // Inject the "name" job data property
    public void setName(String name) { ... }

    @Override
    protected void executeInternal(JobExecutionContext context)
            throws JobExecutionException {
        ...
    }

}
```

### 4.21. 任务执行和调度

在上下文中没有 `Executor` bean 的情况下，Spring Boot 会自动配置具有合理默认值的 `ThreadPoolTaskExecutor`，这些默认值可以自动与异步任务执行（`@EnableAsync`）和 Spring MVC 异步请求处理相关联。

> 如果您在上下文中定义了一个自定义的 `Executor`，则常规任务执行（即 `@ EnableAsync`）将透明地使用它，但由于需要 `AsyncTaskExecutor` 实现（名为 `applicationTaskExecutor`），因此不会配置 Spring MVC 支持。根据您的目标安排，您可以将 `Executor` 更改为 `ThreadPoolTaskExecutor` 或定义包装自定义 `Executor` 的 `ThreadPoolTaskExecutor` 和 `AsyncConfigurer` 自动配置的 `TaskExecutorBuilder` 可以轻松创建实例，复制默认情况下自动配置的功能。

线程池使用 8 个核心线程，这些线程可以根据负载增长和收缩。可以使用 `spring.task.execution` 名称空间对这些默认设置进行微调，如以下示例所示：

```properties
spring.task.execution.pool.max-size=16
spring.task.execution.pool.queue-capacity=100
spring.task.execution.pool.keep-alive=10s
```

这会将线程池更改为使用有界队列，以便在队列已满（100 个任务）时，线程池最多增加到 16 个线程。线程的空闲时间为 10 秒（而不是默认情况下的 60 秒）时，回收线程会使池的收缩更加激进。

如果需要与计划任务执行相关联，也可以自动配置 `ThreadPoolTaskScheduler`（`@EnableScheduling`）。线程池默认使用一个线程，并且可以使用 `spring.task.scheduling` 名称空间对这些设置进行微调。

如果需要创建自定义执行程序或调度程序，则可以在上下文中同时使用 `TaskExecutorBuilder` bean和 `TaskSchedulerBuilder` bean。

### 4.22. Spring 集成

Spring Boot 为使用 [Spring Integration](https://spring.io/projects/spring-integration) 提供了许多便利，其中包括 `spring-boot-starter-integration` “Starter”。Spring Integration 在消息传递以及其他传输（例如 HTTP，TCP 等）上提供了抽象。如果 Spring Integration 在您的类路径中可用，则通过 `@EnableIntegration` 注解对其进行初始化。

Spring Boot 还配置了一些功能，这些功能由其他 Spring Integration 模块的存在触发。如果 `spring-integration-jmx` 也位于类路径中，则消息处理统计信息将通过 JMX 发布。如果 `spring-integration-jdbc` 可用，则可以在启动时创建默认的数据库模式，如以下行所示：

```properties
spring.integration.jdbc.initialize-schema=always
```

参考 [`IntegrationAutoConfiguration`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/integration/IntegrationAutoConfiguration.java) 和 [`IntegrationProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/integration/IntegrationProperties.java) 类获取更多细节。

默认情况下，如果存在 Micrometer `meterRegistry` bean，那么 Spring Integration 指标将由 Micrometer 管理。如果您希望使用传统的 Spring Integration 指标，请向应用程序上下文中添加一个 `DefaultMetricsFactory` bean。

### 4.23. Spring Session

Spring Boot 提供了 [Spring Session](https://spring.io/projects/spring-session) 使用大部分种类的数据存储技术的自动配置。当构建 Servlet web 应用时，下面的数据存储会被自动配置：

- JDBC
- Redis
- Hazelcast
- MongoDB

当创建反应式 web 应用时，下面的数据存储能够被自动配置：

- Redis
- MongoDB

如果类路径上存在单个 Spring Session 模块，则 Spring Boot 会自动使用该存储实现。如果您有多个实现，则必须选择您希望用来存储会话的 [`StoreType`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/session/StoreType.java) 。例如，要将 JDBC 用作后端存储，可以按以下方式配置应用程序：

```properties
spring.session.store-type=jdbc
```

> 你可以通过将 `store-type` 设定为 `none` 来禁用 Spring Session。

每种存储都有特定的其他设置。例如，可以为 JDBC 存储定制表的名称，如以下示例所示：

```properties
spring.session.jdbc.table-name=SESSIONS
```

为了设置会话超时，您可以使用 `spring.session.timeout` 属性。如果未设置该属性，则自动配置将降级到使用 `server.servlet.session.timeout` 的值。

### 4.24. 使用 JMX 的监控和管理

Java 管理扩展（JMX）提供了监视和管理应用程序的标准机制。Spring Boot 将最适合的 `MBeanServer` 公开为ID为 `mbeanServer` 的 bean。带有 Spring JMX 注解（`@ManagedResource`，`@ManagedAttribute` 或 `@ManagedOperation`）的任何 bean 都可以使用。

如果您的平台提供标准的 `MBeanServer`，则 Spring Boot 将使用该标准，并在必要时默认使用 VM `MBeanServer`。如果全部失败，将创建一个新的 `MBeanServer`。

参见 [`JmxAutoConfiguration`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/jmx/JmxAutoConfiguration.java) 类以获取更多详细信息。

### 4.25. 测试

Spring Boot 提供了许多实用程序和注解，可以在测试应用程序时提供帮助。测试支持由两个模块提供：`spring-boot-test` 包含核心项，`spring-boot-test-autoconfigure` 支持测试的自动配置。

大多数开发人员使用 `spring-boot-starter-test` “Starter”，它会导入 Spring Boot 测试模块以及 JUnit Jupiter，AssertJ，Hamcrest 和许多其他有用的库。

> 启动程序还带来了老式引擎，因此您可以运行 JUnit 4 和 JUnit 5 测试。如果已将测试迁移到 JUnit 5，则应排除对 JUnit 4 的支持，如以下示例所示：
>
> ```
> <dependency>
>     <groupId>org.springframework.boot</groupId>
>     <artifactId>spring-boot-starter-test</artifactId>
>     <scope>test</scope>
>     <exclusions>
>         <exclusion>
>             <groupId>org.junit.vintage</groupId>
>             <artifactId>junit-vintage-engine</artifactId>
>         </exclusion>
>     </exclusions>
> </dependency>
> ```

#### 4.25.1. 测试范围依赖

`spring-boot-starter-test` “Starter” (处于 `test` `scope` 中) 提供了下列类库：

- [JUnit 5](https://junit.org/junit5)（包括用于与 JUnit 4 向后兼容的老式引擎）：用于 Java 应用程序单元测试的事实上的标准。
- [Spring Test](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#integration-testing) & Spring Boot Test: 对 Spring Boot 应用程序的实用程序和集成测试支持。
- [AssertJ](https://joel-costigliola.github.io/assertj/): 流利的断言库。
- [Hamcrest](https://github.com/hamcrest/JavaHamcrest): 匹配器对象（也称为约束或谓词）库。
- [Mockito](https://mockito.github.io/): Java 模拟框架。
- [JSONassert](https://github.com/skyscreamer/JSONassert): JSON 的断言库。
- [JsonPath](https://github.com/jayway/JsonPath): JSON 的 XPath。

通常，我们发现这些通用库在编写测试时很有用。如果这些库不满足您的需求，则可以添加自己的其他测试依赖项。

#### 4.25.2. 测试 Spring 应用

依赖注入的主要优点之一是，它应该使您的代码更易于进行单元测试。您可以使用 `new` 运算符实例化对象，甚至不需要使用 Spring。您也可以使用 *mock objects* 代替真正的依赖。

通常，您需要超越单元测试并开始集成测试（使用 Spring `ApplicationContext`）。能够进行集成测试而无需部署应用程序或连接到其他基础结构是很有用的。

Spring 框架包括用于此类集成测试的专用测试模块。您可以直接向 `org.springframework:spring-test` 声明一个依赖项，也可以使用 `spring-boot-starter-test` “Starter”将其引入。

如果您以前没有使用过 `spring-test` 模块，则应先阅读 [相关部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#testing) 。

#### 4.25.3. 测试 Spring Boot 应用

一个 Spring Boot 应用就是一个 Spring `ApplicationContext`，因此，相比于传统的 Spring context 的测试，测试 Spring Boot 应用时，你不需要做任何特殊的额外操作。

> 默认情况下，仅当使用 `SpringApplication` 创建 Spring Boot 的外部属性，日志记录和其他功能时，才将其安装在上下文中。

Spring Boot 提供了一个 `@SpringBootTest` 注解，当你需要使用 Spring Boot 特性时，该注解可以替代标准的 `spring-test` `@ContextConfiguration` 注解用于测试。该注解通过 [creating the `ApplicationContext` used in your tests through `SpringApplication`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-detecting-config) 工作。除了 `@SpringBootTest` 之外，还提供了许多其他注解来 [测试更具体的切片](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-tests) 。

> 如果您使用的是 JUnit 4，请不要忘记在测试中也添加 `@RunWith(SpringRunner.class)`，否则注解将被忽略。如果您使用的是 JUnit 5，则无需在 `@SpringBootTest` 中添加等效的 `@ExtendWith(SpringExtension.class)` 和其他 `@…Test` 注解。

默认情况下，`@SpringBootTest` 将不会启动服务器。您可以使用 `@SpringBootTest` 的 `webEnvironment` 属性来进一步完善测试的运行方式：

- `MOCK`(默认) : 加载 Web `ApplicationContext` 并提供模拟 Web 环境。使用此注解时，不会启动嵌入式服务器。如果您的类路径中没有 Web 环境，则此模式将透明地降级到创建常规的非 Web `ApplicationContext`。它可以与 [`@AutoConfigureMockMvc` 或 `@AutoConfigureWebTestClient`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-with-mock-environment)结合使用，用于对 Web 应用程序进行基于模拟的测试。
- `RANDOM_PORT`: 加载一个 `WebServerApplicationContext` 并提供一个真实的 Web 环境。嵌入式服务器将启动并在随机端口上侦听。
- `DEFINED_PORT`: 加载一个 `WebServerApplicationContext` 并提供一个真实的 Web 环境。嵌入式服务器启动并在定义的端口（来自 `application.properties` ）或默认端口 `8080` 上侦听。
- `NONE`: 使用 `SpringApplication` 加载 `ApplicationContext`，但不提供任何 Web 环境（模拟或其他方式）。

> 如果您的测试是 `@Transactional`，则默认情况下它将在每个测试方法的末尾回滚事务。但是，由于将这种安排与 `RANDOM_PORT` 或 `DEFINED_PORT` 一起使用隐式提供了一个真实的 Servlet 环境，因此 HTTP 客户端和服务器在单独的线程中运行，因此在单独的事务中运行。在这种情况下，服务器上启动的任何事务都不会回滚。

> 如果您的应用程序对管理服务器使用不同的端口，则将带有 `WebEnvironment = WebEnvironment.RANDOM_PORT` 的 `@SpringBootTest` 还将在单独的随机端口上启动管理服务器。

##### 探测 Web 应用类型

如果 Spring MVC 可用，则配置基于常规 MVC 的应用程序上下文。如果您只有 Spring WebFlux，我们将检测到该情况并配置基于 WebFlux 的应用程序上下文。

如果两者都存在，则 Spring MVC 优先。如果要在这种情况下测试反应式 Web 应用程序，则必须设置 `spring.main.web-application-type` 属性：

```java
@SpringBootTest(properties = "spring.main.web-application-type=reactive")
class MyWebFluxTests { ... }
```

##### 探测测试配置

如果您熟悉 Spring Test Framework，可能会习惯于使用 `@ContextConfiguration(classes=…)` 来指定要加载哪个 Spring `@Configuration`。另外，您可能经常在测试中使用嵌套的 `@Configuration` 类。

在测试 Spring Boot 应用程序时，通常不需要这样做。只要您没有明确定义，Spring Boot 的 `@*Test` 注解就会自动搜索您的主要配置。

搜索算法从包含测试的程序包开始工作，直到找到带有 `@SpringBootApplication` 或 `@SpringBootConfiguration` 注解的类。只要您以明智的方式 [结构化代码](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-structuring-your-code)，通常可以找到您的主要配置。

>如果您使用 [测试注解来测试应用程序的特定部分](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-tests) ，则应避免在 [包含 main 方法的应用类](https://docs.spring.io/spring-boot/) 上添加特定于特定区域的配置设置。`@SpringBootApplication` 的底层组件扫描配置定义了排除过滤器，这些过滤器用于确保切片效果符合预期。如果在 `@SpringBootApplication` 注解的类上使用显式的 `@ComponentScan` 指令，请注意那些过滤器将被禁用。如果使用切片，则应重新定义它们。

如果要自定义主要配置，则可以使用嵌套的 `@TestConfiguration` 类。与将使用嵌套的 `@Configuration` 类而不是应用程序的主要配置不同的是，除了使用应用程序的主要配置之外，还使用嵌套的 `@TestConfiguration` 类。

>Spring 的测试框架会在测试之间缓存应用程序上下文。因此，只要您的测试共享相同的配置（无论如何发现），加载上下文的潜在耗时过程就只会发生一次。

