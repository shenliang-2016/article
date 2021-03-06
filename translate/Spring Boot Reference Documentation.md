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

Spring 框架为与消息系统的集成提供了丰富的支持，从通过使用 `JmsTemplate` 来简化 JMS API 的使用，到异步接收消息的完整基础设施。Spring AMQP 提供了类似于高级消息队列协议的特性集合。Spring Boot 也提供了 `RabbitTemplate` 和 RabbitMQ 的自动配置选项。Spring WebSocket 本身包含 STOMP 消息支持，同时 Spring Boot 通过启动器和少量的自动配置支持该消息。Spring Boot 还支持 Apache Kafka。

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

##### 排除测试配置

如果您的应用程序使用组件扫描（例如，如果使用 `@SpringBootApplication` 或 `@ComponentScan` ），则可能会偶然发现为局部创建的仅为特定测试使用的配置类被全局应用了。

正如我们 [之前所见](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-detecting-config )，可以在测试的内部类上使用 `@TestConfiguration` 来自定义主要配置。如果将 `@TestConfiguration` 放在顶级类上，则表明 `src/test/java` 中的类不应通过扫描来拾取。然后，可以在需要的位置显式导入该类，如以下示例所示：

```java
@SpringBootTest
@Import(MyTestsConfiguration.class)
class MyTests {

    @Test
    void exampleTest() {
        ...
    }

}
```

>如果您直接使用 `@ComponentScan`（即不是通过 `@SpringBootApplication`），则需要向其中注册 `TypeExcludeFilter`。有关详细信息，请参见 [Javadoc](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/context/TypeExcludeFilter.html)。

##### 使用应用参数

如果你的应用期望 [arguments](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-application-arguments)，你可以通过 `@SpringBootTest` 的 `args` 属性注入它们。

```java
@SpringBootTest(args = "--app.test=one")
class ApplicationArgumentsExampleTests {

    @Test
    void applicationArgumentsPopulated(@Autowired ApplicationArguments args) {
        assertThat(args.getOptionNames()).containsOnly("app.test");
        assertThat(args.getOptionValues("app.test")).containsOnly("one");
    }

}
```

##### 使用模拟环境测试

默认情况下， `@SpringBootTest` 不会启动服务器。如果你希望在模拟环境中测试你的 web 服务端点，你可以如下面例子所示配置 [`MockMvc`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference//testing.html#spring-mvc-test-framework) ：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.web.servlet.MockMvc;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@SpringBootTest
@AutoConfigureMockMvc
class MockMvcExampleTests {

    @Test
    void exampleTest(@Autowired MockMvc mvc) throws Exception {
        mvc.perform(get("/")).andExpect(status().isOk()).andExpect(content().string("Hello World"));
    }

}
```

>如果你希望聚焦于 web 层，并不需要启动一个完整的 `ApplicationContext`，考虑 [使用 `@WebMvcTest` 代替](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-mvc-tests)。

另外，你可以配置 [`WebTestClient`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#webtestclient-tests) ，如下面例子所示：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.reactive.AutoConfigureWebTestClient;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.web.reactive.server.WebTestClient;

@SpringBootTest
@AutoConfigureWebTestClient
class MockWebTestClientExampleTests {

    @Test
    void exampleTest(@Autowired WebTestClient webClient) {
        webClient.get().uri("/").exchange().expectStatus().isOk().expectBody(String.class).isEqualTo("Hello World");
    }

}
```

>在模拟环境中进行测试通常比在完整的 Servlet 容器中运行更快。但是，由于模拟是在 Spring MVC 层进行的，因此无法直接使用 MockMvc 来测试依赖于较低级别 Servlet 容器行为的代码。例如，Spring Boot 的错误处理基于 Servlet 容器提供的“错误页面”支持。这意味着，尽管您可以按预期测试 MVC 层引发和处理异常，但是您无法直接测试特定的 [自定义错误页面](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-error-handling-custom-error-pages) 呈现。如果您需要测试这些较低级别的问题，则可以按照下一节中的描述启动一个完全运行的服务器。

##### 使用运行服务器测试

如果需要启动完全运行的服务器，建议您使用随机端口。如果使用 `@SpringBootTest(webEnvironment=WebEnvironment.RANDOM_PORT)`，则每次运行测试时都会随机选择一个可用端口。

`@LocalServerPort` 注解可用于 [注入使用的实际端口](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-discover-the-http-port-at-runtime) 进入测试。为了方便起见，需要对启动的服务器进行 REST 调用的测试可以另外使用 `@Autowire` 一个 [`WebTestClient`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#webtestclient-tests)，它解析到正在运行的服务器的相对链接，并带有用于验证响应的专用 API，如以下示例所示：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.context.SpringBootTest.WebEnvironment;
import org.springframework.test.web.reactive.server.WebTestClient;

@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
class RandomPortWebTestClientExampleTests {

    @Test
    void exampleTest(@Autowired WebTestClient webClient) {
        webClient.get().uri("/").exchange().expectStatus().isOk().expectBody(String.class).isEqualTo("Hello World");
    }

}
```

这种设置需要在类路径上使用 `spring-webflux`。如果您无法或不会添加 webflux，则 Spring Boot 还提供了 `TestRestTemplate` 工具：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.context.SpringBootTest.WebEnvironment;
import org.springframework.boot.test.web.client.TestRestTemplate;

import static org.assertj.core.api.Assertions.assertThat;

@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
class RandomPortTestRestTemplateExampleTests {

    @Test
    void exampleTest(@Autowired TestRestTemplate restTemplate) {
        String body = restTemplate.getForObject("/", String.class);
        assertThat(body).isEqualTo("Hello World");
    }

}
```

##### 自定义 WebTestClient

要自定义 `WebTestClient` bean，请配置 `WebTestClientBuilderCustomizer` bean。使用 `WebTestClient.Builder` 调用任何此类 bean，用于创建 `WebTestClient`。

##### 使用 JMX

由于测试上下文框架缓存上下文，因此默认情况下禁用 JMX，以防止相同的组件在同一域上注册。如果这样的测试需要访问 `MBeanServer`，请考虑将其标记为脏：

```java
@ExtendWith(SpringExtension.class)
@SpringBootTest(properties = "spring.jmx.enabled=true")
@DirtiesContext
class SampleJmxTests {

    @Autowired
    private MBeanServer mBeanServer;

    @Test
    void exampleTest() {
        // ...
    }

}
```

##### 模拟并监视 Beans

运行测试时，有时有必要在应用程序上下文中模拟某些组件。例如，您可能在开发过程中无法使用某些远程服务的门面。当您要模拟在实际环境中可能难以触发的故障时，模拟功能也很有用。

Spring Boot 包含一个 `@MockBean` 注解，可用于为 `ApplicationContext` 内部的 bean 定义一个 Mockito 模拟。您可以使用注解添加新的 bean 或替换单个现有的 bean 定义。注解可以直接用于测试类，测试中的字段或 `@Configuration` 类和字段。在字段上使用时，还将注入创建的模拟的实例。每种测试方法后，模拟 beans 都会自动重置。

>如果您的测试使用 Spring Boot 的测试注解之一（例如 `@SpringBootTest` ），则会自动启用此功能。要以其他方式使用此功能，必须明确添加侦听器，如以下示例所示：
>
>```java
>@TestExecutionListeners(MockitoTestExecutionListener.class)
>```

以下示例使用模拟实现替换了现有的 `RemoteService` bean：

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.*;
import org.springframework.boot.test.context.*;
import org.springframework.boot.test.mock.mockito.*;

import static org.assertj.core.api.Assertions.*;
import static org.mockito.BDDMockito.*;

@SpringBootTest
class MyTests {

    @MockBean
    private RemoteService remoteService;

    @Autowired
    private Reverser reverser;

    @Test
    void exampleTest() {
        // RemoteService has been injected into the reverser bean
        given(this.remoteService.someCall()).willReturn("mock");
        String reverse = reverser.reverseSomeCall();
        assertThat(reverse).isEqualTo("kcom");
    }

}
```

>`@MockBean` 不能用于模拟应用程序上下文刷新期间执行的 bean 的行为。到执行测试时，应用程序上下文刷新已完成，并且配置模拟行为为时已晚。我们建议在这种情况下使用 `@Bean` 方法创建和配置模拟。

另外，您可以使用 `@SpyBean` 来将任何现有的 bean 与 Mockito 的 `spy` 一起包装。有关完整的详细信息，请参见 [Javadoc](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/test/mock/mockito/SpyBean.html)。

>CGLib 代理（例如为作用域范围内的 bean 创建的代理）将代理的方法声明为 `final`。这会阻止 Mockito 正常运行，因为它无法在其默认配置中模拟或监视 `final` 方法。如果您想对这样的 bean 进行模拟或监视，请通过在应用程序的测试依赖项中添加 `org.mockito:mockito-inline` 来将 Mockito 配置为使用其内联模拟程序。这使 Mockito 可以模拟并监视 `final` 方法。

>Spring 的测试框架在测试之间缓存应用程序上下文，并为共享相同配置的测试重用上下文，而 `@MockBean` 或 `@SpyBean` 的使用会影响缓存键，这很可能会增加上下文数量。

>如果您使用 `@SpyBean` 来监视通过名称引用参数的 `@Cacheable` 方法，则您的应用程序必须使用 `-parameters` 进行编译。这样可以确保一旦侦察到 bean，就可以将参数名称用于缓存基础结构。

##### 自动配置的测试

Spring Boot 的自动配置系统适用于应用程序，但有时对于测试来说可能有点过多。它通常仅有助于加载测试应用程序“切片”所需的配置部分。例如，您可能想测试 Spring MVC 控制器是否正确映射了 URL，并且不想在这些测试中涉及数据库调用，或者您想测试 JPA 实体，并且当您使用 JPA 实体时，您对 Web 层不感兴趣。

`spring-boot-test-autoconfigure` 模块包含许多注解，可用于自动配置此类“切片”。它们中的每一个都以类似的方式工作，提供了一个可加载 `ApplicationContext` 的 `@…Test` 注解和一个或多个可用于自定义自动配置设置的 `@AutoConfigure…` 注解。

>每个切片将组件扫描范围限制为适当的组件，并加载一组非常受限制的自动配置类。如果您需要排除其中之一，则大多数 `@…Test` 注解都提供了 `excludeAutoConfiguration` 属性。或者，您可以使用 `@ImportAutoConfiguration#exclude`。

>不支持在一个测试中使用多个 `@…Test` 注解来包含多个“切片”。如果需要多个“切片”，请选择一个 `@…Test` 注解，并手动添加其他“切片”的 `@AutoConfigure…` 注解。

>也可以将 `@AutoConfigure…` 注解与标准的 `@SpringBootTest` 注解一起使用。如果您对“切片”应用程序不感兴趣，但需要一些自动配置的测试 bean，则可以使用此组合。

##### 自动配置的 JSON 测试

要测试对象 JSON 序列化和反序列化是否按预期工作，可以使用 `@JsonTest` 注解。`@JsonTest` 自动配置可用的受支持的 JSON 映射器，可以是以下库之一：

-Jackson `ObjectMapper`, 所有 `@JsonComponent` beans 和所有 Jackson `Module`s
-`Gson`
-`Jsonb`

>可以通过 `@JsonTest` 启用的自动配置列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

如果您需要配置自动配置的元素，则可以使用 `@AutoConfigureJsonTesters` 注解。

Spring Boot 包括基于 AssertJ 的助手，这些助手与 JSONAssert 和 JsonPath 库一起使用，以检查 JSON 是否按预期方式显示。`JacksonTester`，`GsonTester`，`JsonbTester` 和 `BasicJsonTester` 类可分别用于 Jackson，Gson，Jsonb 和 Strings。使用 `@JsonTest` 时，测试类上的任何帮助程序字段都可以为 `@Autowired`。以下示例显示了 Jackson 的测试类：

```java
import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.*;
import org.springframework.boot.test.autoconfigure.json.*;
import org.springframework.boot.test.context.*;
import org.springframework.boot.test.json.*;

import static org.assertj.core.api.Assertions.*;

@JsonTest
class MyJsonTests {

    @Autowired
    private JacksonTester<VehicleDetails> json;

    @Test
    void testSerialize() throws Exception {
        VehicleDetails details = new VehicleDetails("Honda", "Civic");
        // Assert against a `.json` file in the same package as the test
        assertThat(this.json.write(details)).isEqualToJson("expected.json");
        // Or use JSON path based assertions
        assertThat(this.json.write(details)).hasJsonPathStringValue("@.make");
        assertThat(this.json.write(details)).extractingJsonPathStringValue("@.make")
                .isEqualTo("Honda");
    }

    @Test
    void testDeserialize() throws Exception {
        String content = "{\"make\":\"Ford\",\"model\":\"Focus\"}";
        assertThat(this.json.parse(content))
                .isEqualTo(new VehicleDetails("Ford", "Focus"));
        assertThat(this.json.parseObject(content).getMake()).isEqualTo("Ford");
    }

}
```

>JSON 帮助程序类也可以直接在标准单元测试中使用。为此，如果不使用 `@JsonTest`，请在 `@Before` 方法中调用帮助程序的 `initFields` 方法。

如果您使用的是 Spring Boot 基于 AssertJ 的帮助器，以给定的 JSON 路径声明数字值，则可能无法使用 `isEqualTo`，具体取决于类型。相反，您可以使用 AssertJ 的 `satisfies` 来断言该值符合给定条件。例如，以下示例断言实际数字是与 `0.15` 差距不超过 `0.01` 的浮点值。

```java
assertThat(json.write(message))
    .extractingJsonPathNumberValue("@.test.numberValue")
    .satisfies((number) -> assertThat(number.floatValue()).isCloseTo(0.15f, within(0.01f)));
```

##### 自动配置的 Spring MVC 测试

要测试 Spring MVC 控制器是否按预期工作，请使用 `@WebMvcTest` 注解。`@WebMvcTest` 自动配置 Spring MVC 基础结构并将扫描的 bean 限制为 `@Controller`，`@ControllerAdvice`，`@JsonComponent`，`Converter`，`GenericConverter`，`Filter`，`HandlerInterceptor`，`WebMvcConfigurer` 和 `HandlerMethodArgumentResolver`。使用此注解时，不会扫描常规的 `@Component` Bean。

> `@WebMvcTest` 能够开启的自动配置设定的列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

> 如果你需要注册额外组件，比如 Jackson `Module` ，你可以通过使用 `@Import` 将额外的配置类导入你的测试中。

通常，`@WebMvcTest` 仅限于单个控制器，并与 `@MockBean` 结合使用以为所需的协作者提供模拟实现。

`@WebMvcTest` 还可以自动配置 `MockMvc`。Mock MVC 提供了一种强大的方法来快速测试 MVC 控制器，而无需启动完整的 HTTP 服务器。

> 您还可以通过在非 `@WebMvcTest`（例如，`@SpringBootTest`）中自动配置 `MockMvc`，方法是使用 `@AutoConfigureMockMvc` 对其进行注解。以下示例使用 `MockMvc`：

```java
import org.junit.jupiter.api.*;
import org.springframework.beans.factory.annotation.*;
import org.springframework.boot.test.autoconfigure.web.servlet.*;
import org.springframework.boot.test.mock.mockito.*;

import static org.assertj.core.api.Assertions.*;
import static org.mockito.BDDMockito.*;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@WebMvcTest(UserVehicleController.class)
class MyControllerTests {

    @Autowired
    private MockMvc mvc;

    @MockBean
    private UserVehicleService userVehicleService;

    @Test
    void testExample() throws Exception {
        given(this.userVehicleService.getVehicleDetails("sboot"))
                .willReturn(new VehicleDetails("Honda", "Civic"));
        this.mvc.perform(get("/sboot/vehicle").accept(MediaType.TEXT_PLAIN))
                .andExpect(status().isOk()).andExpect(content().string("Honda Civic"));
    }

}
```

> 如果您需要配置自动配置的元素（例如，当应该应用 servlet 过滤器时），则可以使用 `@AutoConfigureMockMvc` 注解中的属性。

如果使用 HtmlUnit 或 Selenium，则自动配置还会提供 HtmlUnit `WebClient` bean 和/或 Selenium `WebDriver` bean。以下示例使用 HtmlUnit：

```java
import com.gargoylesoftware.htmlunit.*;
import org.junit.jupiter.api.*;
import org.springframework.beans.factory.annotation.*;
import org.springframework.boot.test.autoconfigure.web.servlet.*;
import org.springframework.boot.test.mock.mockito.*;

import static org.assertj.core.api.Assertions.*;
import static org.mockito.BDDMockito.*;

@WebMvcTest(UserVehicleController.class)
class MyHtmlUnitTests {

    @Autowired
    private WebClient webClient;

    @MockBean
    private UserVehicleService userVehicleService;

    @Test
    void testExample() throws Exception {
        given(this.userVehicleService.getVehicleDetails("sboot"))
                .willReturn(new VehicleDetails("Honda", "Civic"));
        HtmlPage page = this.webClient.getPage("/sboot/vehicle.html");
        assertThat(page.getBody().getTextContent()).isEqualTo("Honda Civic");
    }

}
```

> 默认情况下，Spring Boot 将 `WebDriver` bean 放在一个特殊的“作用域”中，以确保驱动程序在每次测试后退出并注入新实例。如果您不希望出现这种情况，则可以将 `@Scope("singleton")` 添加到您的 `WebDriver`  `@Bean` 定义中。

> 由 Spring Boot 创建的 `webDriver` 作用域将替换任何用户定义的同名作用域。如果您定义自己的 `webDriver` 范围，则可能会在使用 `@WebMvcTest` 时发现它停止工作。

如果您在类路径上具有 Spring Security，则 `@WebMvcTest` 还将扫描 `WebSecurityConfigurer` Bean。您可以使用 Spring Security 的测试支持来代替完全禁用此类测试的安全性。有关如何使用 Spring Security 的 `MockMvc` 支持的更多详细信息，请参见 *使用Spring Security测试* 方法部分。

> 有时编写 Spring MVC 测试是不够的。Spring Boot 可以帮助您运行 [使用实际服务器进行全面的端到端测试](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-with-running-server)。

##### 自动配置的 Spring WebFlux 测试

要测试 [Spring WebFlux](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference//web-reactive.html) 控制器是否按预期工作，可以使用 `@WebFluxTest` 注解。`@WebFluxTest` 自动配置 Spring WebFlux 基础结构，并将扫描的 bean 限制为 `@Controller`，`@ControllerAdvice`，`@JsonComponent`，`Converter`，`GenericConverter`，`WebFilter` 和 `WebFluxConfigurer`。使用 `@WebFluxTest` 注解时，不会扫描常规的 `@Component` bean。

> `@WebFluxTest` 能够开启的自动配置设定列表可以在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中找到。

> 如果您需要注册其他组件，例如 Jackson `Module`，则可以在测试中使用 `@Import` 导入其他配置类。

通常，`@WebFluxTest` 仅限于单个控制器，并与 `@MockBean` 注解结合使用，以为所需的协作者提供模拟实现。

`@WebFluxTest` 也会自动配置 [WebTestClient](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#webtestclient)，提供了快速测试 WebFlux 控制器而无需启动完整的 HTTP 服务器的强大方法。

> 您也可以在非 `@WebFluxTest`（例如，`@SpringBootTest`）中自动配置 `WebTestClient`，方法是使用 `@AutoConfigureWebTestClient` 对其进行注解。以下示例显示了同时使用 `@WebFluxTest` 和 `WebTestClient` 的类：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.reactive.WebFluxTest;
import org.springframework.http.MediaType;
import org.springframework.test.web.reactive.server.WebTestClient;

@WebFluxTest(UserVehicleController.class)
class MyControllerTests {

    @Autowired
    private WebTestClient webClient;

    @MockBean
    private UserVehicleService userVehicleService;

    @Test
    void testExample() throws Exception {
        given(this.userVehicleService.getVehicleDetails("sboot"))
                .willReturn(new VehicleDetails("Honda", "Civic"));
        this.webClient.get().uri("/sboot/vehicle").accept(MediaType.TEXT_PLAIN)
                .exchange()
                .expectStatus().isOk()
                .expectBody(String.class).isEqualTo("Honda Civic");
    }

}
```

> 只有 WebFlux 应用程序支持此设置，因为在模拟的 web 应用程序中使用 `WebTestClient` 目前仅适用于WebFlux。

> `@WebFluxTest` 无法检测通过功能性 web 框架注册的路由。为了在上下文中测试 `RouterFunction` bean，请考虑自己通过 `@Import` 或使用 `@SpringBootTest` 导入 `RouterFunction`。

> `@WebFluxTest` 无法检测通过 `SecurityWebFilterChain` 类型的 `@Bean` 注册的自定义安全配置。为了将其包含在测试中，您将需要通过 `@Import` 或使用 `@SpringBootTest` 导入用于注册 bean 的配置。

> 有时候编写 Spring WebFlux 测试是不够的；Spring Boot 能够帮助你运行 [实际服务器上完整的端到端测试](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-with-running-server))。

##### 自动配置的 Data JPA 测试

您可以使用 `@DataJpaTest` 注解来测试 JPA 应用程序。默认情况下，它扫描 `@Entity` 类并配置 Spring Data JPA 存储库。如果在类路径上有嵌入式数据库，它也会配置一个。常规的 `@Component` Bean不会加载到 `ApplicationContext` 中。

> `@DataJpaTest` 能够开启的自动配置设定列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

默认情况下，数据 JPA 测试是事务性的，并在每次测试结束时回滚。请参阅 Spring Framework 参考文档中的 [相关部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#testcontext-tx-enabling-transactions) 了解更多详细信息。如果这不是您想要的，则可以按以下方式禁用测试或整个类的事务管理：

```java
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.transaction.annotation.Propagation;
import org.springframework.transaction.annotation.Transactional;

@DataJpaTest
@Transactional(propagation = Propagation.NOT_SUPPORTED)
class ExampleNonTransactionalTests {

}
```

数据 JPA 测试也可以注入 [`TestEntityManager`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-test-autoconfigure/src/main/java/org/springframework/boot/test/autoconfigure/orm/jpa/TestEntityManager.java) bean，它提供了专门为测试设计的标准 JPA `EntityManager` 的替代方案。如果您要在 `@DataJpaTest` 实例之外使用 `TestEntityManager`，则还可以使用 `@AutoConfigureTestEntityManager` 注解。如果需要，也可以使用 `JdbcTemplate`。以下示例显示了使用中的 `@DataJpaTest` 注解：

```java
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.autoconfigure.orm.jpa.*;

import static org.assertj.core.api.Assertions.*;

@DataJpaTest
class ExampleRepositoryTests {

    @Autowired
    private TestEntityManager entityManager;

    @Autowired
    private UserRepository repository;

    @Test
    void testExample() throws Exception {
        this.entityManager.persist(new User("sboot", "1234"));
        User user = this.repository.findByUsername("sboot");
        assertThat(user.getUsername()).isEqualTo("sboot");
        assertThat(user.getVin()).isEqualTo("1234");
    }

}
```

内存嵌入式数据库通常运行良好，不需要任何安装，因此通常可以很好地进行测试。但是，如果您希望对真实数据库运行测试，则可以使用 `@AutoConfigureTestDatabase` 注解，如以下示例所示：

```java
@DataJpaTest
@AutoConfigureTestDatabase(replace=Replace.NONE)
class ExampleRepositoryTests {

    // ...

}
```

##### 自动配置的 JDBC 测试

`@JdbcTest` 与 `@DataJpaTest` 类似，但适用于仅需要 `DataSource` 且不使用 Spring Data JDBC 的测试。默认情况下，它配置一个内存嵌入式数据库和一个 `JdbcTemplate`。常规的 `@Component` Bean 不会加载到 `ApplicationContext` 中。

> `@JdbcTest` 能够开启的自动配置设定列表参见 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 。

缺省情况下，JDBC 测试是事务性的，并在每次测试结束时回滚。请参阅 Spring Framework 参考文档中的 [相关部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#testcontext-tx-enabling-transactions) 了解更多详细信息。如果这不是您想要的，则可以为测试或整个类禁用事务管理，如下所示：

```java
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.autoconfigure.jdbc.JdbcTest;
import org.springframework.transaction.annotation.Propagation;
import org.springframework.transaction.annotation.Transactional;

@JdbcTest
@Transactional(propagation = Propagation.NOT_SUPPORTED)
class ExampleNonTransactionalTests {

}
```

如果您希望测试针对真实数据库运行，则可以使用 `@AutoConfigureTestDatabase` 注解，方法与对 `DataJpaTest` 的方法相同。（请参阅 “[自动配置的 Data JPA 测试](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-jpa-test)”）

##### 自动配置的 Data JDBC 测试

`@DataJdbcTest` 类似于 `@JdbcTest` ，不过是用于使用 Spring Data JDBC 存储仓库的测试。默认情况下，它配置一个内存嵌入式数据库，一个 `JdbcTemplate`，以及 Spring Data JDBC 存储仓库。普通的 `@Component` beans 不会被加载进入 `ApplicationContext`。

>由 `@DataJdbcTest` 开启的自动配置列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

默认地，Data JDBC 测试是事务性的，会在每个测试结束之后回滚。参考 Spring Framework 参考文档的 [相关章节](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#testcontext-tx-enabling-transactions) 获取更多细节。如果这不是你希望的，你可以为单个测试用例或者整个测试类关闭事务管理，如 [JDBC 示例](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-jdbc-test) 中所示。

如果你想要你的测试运行在真实的数据库上，你可以使用 `@AutoConfigureTestDatabase` 注解，以与 `DataJpaTest` 相同的方式。 (参考 "[自动配置的 Data JPA 测试](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-jpa-test)".)

##### 自动配置的 jOOQ 测试

您可以使用与 `@JdbcTest` 类似的方式来使用 `@JooqTest`，但是可以进行与 jOOQ 相关的测试。由于 jOOQ 严重依赖与数据库模式相对应的基于 Java 的模式，因此将使用现有的 `DataSource`。如果要用内存数据库替换它，则可以使用 `@AutoConfigureTestDatabase` 覆盖那些设置。（有关将 jOOQ 与 Spring Boot 结合使用的更多信息，请参阅本章的前面的 “ [使用jOOQ](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-jooq) “。）常规的 `@Component` Bean不会加载到 `ApplicationContext` 中。

>由 `@JooqTest` 开启的自动配置列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

`@JooqTest` 配置一个 `DSLContext`。普通的 `@Component` beans 不会被加载进入 `ApplicationContext`。下面的例子展示了 `@JooqTest` 注解使用：

```java
import org.jooq.DSLContext;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.autoconfigure.jooq.JooqTest;

@JooqTest
class ExampleJooqTests {

    @Autowired
    private DSLContext dslContext;
}
```

JOOQ 测试是事务性的，每个测试结束之后就会回滚。如果这不是你想要的，可以为单个测试用例或者整个测试类关闭事务管理，如 [JDBC 示例](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-jdbc-test) 中所示。

##### 自动配置的 Data MongoDB 测试

您可以使用 `@DataMongoTest` 来测试 MongoDB 应用程序。默认情况下，它配置内存嵌入式 MongoDB（如果可用），配置 `MongoTemplate`，扫描 `@Document` 类，并配置 Spring Data MongoDB 存储库。常规的 `@Component` Bean不会加载到 `ApplicationContext` 中。（有关将 MongoDB 与 Spring Boot 结合使用的更多信息，参见在本章前面的 [MongoDB](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-mongodb) ）

>由 `@DataMongoTest` 开启的自动配置设定列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

下面的类展示了 `@DataMongoTest` 注解的使用：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.data.mongo.DataMongoTest;
import org.springframework.data.mongodb.core.MongoTemplate;

@DataMongoTest
class ExampleDataMongoTests {

    @Autowired
    private MongoTemplate mongoTemplate;

    //
}
```

内存嵌入式 MongoDB 通常运行良好，不需要任何开发人员安装，因此通常可以很好地用于测试。但是，如果您希望对真实的 MongoDB 服务器运行测试，则应排除嵌入式 MongoDB 自动配置，如以下示例所示：

```java
import org.springframework.boot.autoconfigure.mongo.embedded.EmbeddedMongoAutoConfiguration;
import org.springframework.boot.test.autoconfigure.data.mongo.DataMongoTest;

@DataMongoTest(excludeAutoConfiguration = EmbeddedMongoAutoConfiguration.class)
class ExampleDataMongoNonEmbeddedTests {

}
```

##### 自动配置的 Data Neo4j 测试

您可以使用 `@DataNeo4jTest` 来测试 Neo4j 应用程序。默认情况下，它使用内存中嵌入式 Neo4j（如果有嵌入式驱动程序可用），扫描 `@NodeEntity` 类，并配置 Spring Data Neo4j 存储库。常规的 `@Component` Bean 不会加载到 `ApplicationContext` 中。（有关将 Neo4J 与 Spring Boot 结合使用的更多信息，请参阅在本章前面的 [Neo4j](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-neo4j)）

>由 `@DataNeo4jTest` 开启的自动配置设定列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

下面的例子展示了在 Spring Boot 中使用 Neo4J 测试的典型设定：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.data.neo4j.DataNeo4jTest;

@DataNeo4jTest
class ExampleDataNeo4jTests {

    @Autowired
    private YourRepository repository;

    //
}
```

默认情况下，Data Neo4j 测试是事务性的，并在每次测试结束时回滚。请参阅 Spring Framework 参考文档中的 [相关部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#testcontext-tx-enabling-transactions) 有关更多详细信息。如果这不是您想要的，则可以为测试或整个类禁用事务管理，如下所示：

```java
import org.springframework.boot.test.autoconfigure.data.neo4j.DataNeo4jTest;
import org.springframework.transaction.annotation.Propagation;
import org.springframework.transaction.annotation.Transactional;

@DataNeo4jTest
@Transactional(propagation = Propagation.NOT_SUPPORTED)
class ExampleNonTransactionalTests {

}
```

##### 自动配置的 Data Redis 测试

你可以使用 `@DataRedisTest` 来测试 Redis 应用程序。默认情况下，它会扫描 `@RedisHash` 类并配置 Spring Data Redis 存储库。常规的 `@Component` Bean 不会加载到 `ApplicationContext` 中。（有关将 Redis 与 Spring Boot 结合使用的更多信息，参见 [Redis](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-redis) 。）

> 由 `@DataRedisTest` 开启的自动配置设定列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

下面的例子展示了 `@DataRedisTest` 注解的使用：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.data.redis.DataRedisTest;

@DataRedisTest
class ExampleDataRedisTests {

    @Autowired
    private YourRepository repository;

    //
}
```

##### 自动配置的 Data LDAP 测试

你可以使用 `@DataLdapTest` 来测试 LDAP 应用程序。默认情况下，它配置内存嵌入式 LDAP（如果可用），配置 `LdapTemplate`，扫描 `@Entry` 类，并配置 Spring Data LDAP 存储库。常规的 `@Component` Bean 不会加载到 `ApplicationContext` 中。（有关将 LDAP 与 Spring Boot 结合使用的更多信息，请参阅 [LDAP](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/htmlsingle/#boot-features-ldap) ）

>  由 `@DataLdapTest` 开启的自动配置设定列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

下面的例子展示了 `@DataLdapTest` 注解的使用：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.data.ldap.DataLdapTest;
import org.springframework.ldap.core.LdapTemplate;

@DataLdapTest
class ExampleDataLdapTests {

    @Autowired
    private LdapTemplate ldapTemplate;

    //
}
```

内存嵌入式 LDAP 通常非常适合测试，因为它速度快并且不需要安装任何开发人员。但是，如果您希望针对真实的 LDAP 服务器运行测试，则应排除嵌入式 LDAP 自动配置，如以下示例所示：

```java
import org.springframework.boot.autoconfigure.ldap.embedded.EmbeddedLdapAutoConfiguration;
import org.springframework.boot.test.autoconfigure.data.ldap.DataLdapTest;

@DataLdapTest(excludeAutoConfiguration = EmbeddedLdapAutoConfiguration.class)
class ExampleDataLdapNonEmbeddedTests {

}
```

##### 自动配置的 REST 客户端

您可以使用 `@ RestClientTest` 来测试 REST 客户端。默认情况下，它会自动配置 Jackson，GSON 和 Jsonb 支持，配置 `RestTemplateBuilder`，并增加对 `MockRestServiceServer` 的支持。常规的 `@Component` Bean 不会加载到 `ApplicationContext` 中。

>  由 `@RestClientTest` 开启的自动配置设定列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

你希望测试的特定 beans 应该使用 `@RestClientTest` 注解的 `value` 或者 `components` 属性标示，如下面例子所示：

```java
@RestClientTest(RemoteVehicleDetailsService.class)
class ExampleRestClientTest {

    @Autowired
    private RemoteVehicleDetailsService service;

    @Autowired
    private MockRestServiceServer server;

    @Test
    void getVehicleDetailsWhenResultIsSuccessShouldReturnDetails()
            throws Exception {
        this.server.expect(requestTo("/greet/details"))
                .andRespond(withSuccess("hello", MediaType.TEXT_PLAIN));
        String greeting = this.service.callRestService();
        assertThat(greeting).isEqualTo("hello");
    }

}
```

##### 自动配置的 Spring REST Docs 测试

您可以在 Mock MVC，REST Assured 或 WebTestClient 的测试中使用 `@AutoConfigureRestDocs` 来使用 [Spring REST Docs](https://spring.io/projects/spring-restdocs)。它消除了 Spring REST Docs 中对 JUnit 扩展的需求。

可以使用 `@AutoConfigureRestDocs` 覆盖默认输出目录（如果使用 Maven，则使用 `target/generated-snippets`；如果使用 Gradle，则使用 `build/generated-snippets`）。它也可以用于配置出现在任何记录的 URI 中的主机，模式和端口。

###### 自动配置的 Spring REST Docs 测试使用 Mock MVC

`@AutoConfigureRestDocs` 定制 `MockMvc` bean 使用 Spring REST Docs。您可以使用 `@Autowired` 注入它，并像通常使用 Mock MVC 和 Spring REST Docs 一样在测试中使用它。如下面例子所示：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;

import static org.springframework.restdocs.mockmvc.MockMvcRestDocumentation.document;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@WebMvcTest(UserController.class)
@AutoConfigureRestDocs
class UserDocumentationTests {

    @Autowired
    private MockMvc mvc;

    @Test
    void listUsers() throws Exception {
        this.mvc.perform(get("/users").accept(MediaType.TEXT_PLAIN))
                .andExpect(status().isOk())
                .andDo(document("list-users"));
    }

}
```

如果您需要对 Spring REST Docs 配置的控制多于 `@AutoConfigureRestDocs` 的属性所提供的控制，则可以使用 `RestDocsMockMvcConfigurationCustomizer` bean，如以下示例所示：

```java
@TestConfiguration
static class CustomizationConfiguration
        implements RestDocsMockMvcConfigurationCustomizer {

    @Override
    public void customize(MockMvcRestDocumentationConfigurer configurer) {
        configurer.snippets().withTemplateFormat(TemplateFormats.markdown());
    }

}
```

如果您想使用 Spring REST Docs 对参数化输出目录的支持，则可以创建一个 `RestDocumentationResultHandler` bean。自动配置使用此结果处理程序调用 `alwaysDo`，从而使每个 `MockMvc` 调用自动生成默认代码段。以下示例显示了一个已定义的 `RestDocumentationResultHandler`：

```java
@TestConfiguration(proxyBeanMethods = false)
static class ResultHandlerConfiguration {

    @Bean
    public RestDocumentationResultHandler restDocumentation() {
        return MockMvcRestDocumentation.document("{method-name}");
    }

}
```

###### 自动配置的 Spring REST Docs 测试使用 WebTestClient

`@AutoConfigureRestDocs` 还可以用于 `WebTestClient`。你可以使用 `@Autowired` 注入它在你的测试中，如同通常使用 `@WebFluxTest` 和 Spring REST Docs 那样，如下面例子所示：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.restdocs.AutoConfigureRestDocs;
import org.springframework.boot.test.autoconfigure.web.reactive.WebFluxTest;
import org.springframework.test.web.reactive.server.WebTestClient;

import static org.springframework.restdocs.webtestclient.WebTestClientRestDocumentation.document;

@WebFluxTest
@AutoConfigureRestDocs
class UsersDocumentationTests {

    @Autowired
    private WebTestClient webTestClient;

    @Test
    void listUsers() {
        this.webTestClient.get().uri("/").exchange().expectStatus().isOk().expectBody()
                .consumeWith(document("list-users"));
    }

}
```

如果您需要对 Spring REST Docs 配置进行更多控制，而不是 `@AutoConfigureRestDocs` 属性提供的控制，则可以使用 `RestDocsWebTestClientConfigurationCustomizer` bean，如以下示例所示：

```java
@TestConfiguration(proxyBeanMethods = false)
public static class CustomizationConfiguration implements RestDocsWebTestClientConfigurationCustomizer {

    @Override
    public void customize(WebTestClientRestDocumentationConfigurer configurer) {
        configurer.snippets().withEncoding("UTF-8");
    }

}
```

###### 自动配置的 Spring REST Docs 测试使用 REST Assured

`@AutoConfigureRestDocs` 使可配置为使用 Spring REST Docs 的 `RequestSpecification` bean 可供您的测试使用。可以使用 `@Autowired` 注入它，并像使用 REST Assured 和 Spring REST Docs 一样，在测试中使用它，如以下示例所示：

```java
import io.restassured.specification.RequestSpecification;
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.restdocs.AutoConfigureRestDocs;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.context.SpringBootTest.WebEnvironment;
import org.springframework.boot.web.server.LocalServerPort;

import static io.restassured.RestAssured.given;
import static org.hamcrest.Matchers.is;
import static org.springframework.restdocs.restassured3.RestAssuredRestDocumentation.document;

@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
@AutoConfigureRestDocs
class UserDocumentationTests {

    @Test
    void listUsers(@Autowired RequestSpecification documentationSpec, @LocalServerPort int port) {
        given(documentationSpec).filter(document("list-users")).when().port(port).get("/").then().assertThat()
                .statusCode(is(200));
    }

}
```

如果您需要对 Spring REST Docs 配置进行更多控制，而不是通过 `@AutoConfigureRestDocs` 属性来提供更多控制，则可以使用 `RestDocsRestAssuredConfigurationCustomizer` bean，如以下示例所示：

```java
@TestConfiguration(proxyBeanMethods = false)
public static class CustomizationConfiguration implements RestDocsRestAssuredConfigurationCustomizer {

    @Override
    public void customize(RestAssuredRestDocumentationConfigurer configurer) {
        configurer.snippets().withTemplateFormat(TemplateFormats.markdown());
    }

}
```

##### 附加自动配置和切片

每个切片提供一个或多个 `@ AutoConfigure…` 注解，即定义应包含在切片中的自动配置。可以通过创建自定义的 `@AutoConfigure…` 注解来添加其他自动配置，也可以简单地通过向测试中添加 `@ImportAutoConfiguration` 来添加其他自动配置，如以下示例所示：

```java
@JdbcTest
@ImportAutoConfiguration(IntegrationAutoConfiguration.class)
class ExampleJdbcTests {

}
```

> 确保不要使用常规的 `@Import` 注解来引入自动配置，因为自动配置类由 Spring Boot 通过特殊的方式处理。

##### 用户配置和切片

如果你以明智的方式 [结构化你的代码](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/htmlsingle/#using-boot-structuring-your-code)，则你的 `@SpringBootApplication` 类就会 [默认被用作](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-detecting-config) 你的测试的配置类。

因此，变得不重要的是，不要使用特定于其功能特定区域的配置设置来丢弃应用程序的主类。

假设您正在使用 Spring Batch，并且依赖于它的自动配置，您可以如下定义您的 `@SpringBootApplication`：

```java
@SpringBootApplication
@EnableBatchProcessing
public class SampleApplication { ... }
```

因为此类是测试的源配置，所以任何切片测试实际上都尝试启动 Spring Batch，这绝对不是您想要执行的操作。推荐的方法是将特定于区域的配置移到与您的应用程序相同级别的单独的 `@Configuration` 类，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
@EnableBatchProcessing
public class BatchConfiguration { ... }
```

> 根据您应用程序的复杂性，您可以为自定义设置一个单独的 `@Configuration` 类，也可以为每个域指定一个类。后一种方法使您可以在其中的一个测试中启用它，并在必要时使用 `@Import` 注解。

测试切片从扫描中排除了 `@Configuration` 类。例如，对于一个 `@WebMvcTest`，以下配置将在测试切片加载的应用程序上下文中不包含给定的 `WebMvcConfigurer` Bean：

```java
@Configuration
public class WebConfiguration {
    @Bean
    public WebMvcConfigurer testConfigurer() {
        return new WebMvcConfigurer() {
            ...
        };
    }
}
```

但是，以下配置将导致测试切片加载自定义的 `WebMvcConfigurer`。

```java
@Component
public class TestWebMvcConfigurer implements WebMvcConfigurer {
    ...
}
```

混乱的另一个来源是类路径扫描。假定在以合理的方式构造代码时，您需要扫描其他程序包。您的应用程序可能类似于以下代码：

```java
@SpringBootApplication
@ComponentScan({ "com.example.app", "org.acme.another" })
public class SampleApplication { ... }
```

这样做有效地覆盖了默认的组件扫描指令，并且具有扫描这两个软件包的副作用，而与您选择的切片无关。例如，一个 `@DataJpaTest` 似乎突然扫描了应用程序的组件和用户配置。同样，将自定义指令移至单独的类是解决此问题的好方法。

> 如果这不是您的选择，则可以在测试层次结构中的某个位置创建一个 `@SpringBootConfiguration`，以便使用它。或者，您可以为测试指定一个源，从而禁用查找默认源的行为。

##### 使用 Spock 测试 Spring Boot 应用

如果您希望使用 Spock 测试 Spring Boot 应用程序，则应在应用程序的构建中添加对 Spock 的 `spock-spring` 模块的依赖。`spock-spring` 将 Spring 的测试框架集成到了 Spock 中。建议您使用 Spock 1.2 或更高版本，以受益于 Spock 的 Spring Framework 和 Spring Boot 集成的许多改进。有关更多详细信息，请参见 [Spock 的 Spring 模块的文档](http://spockframework.org/spock/docs/1.2/modules.html#_spring_module)。

#### 4.25.4. 测试工具

一些通用的测试工具类作为其一部分打包在 `spring-boot` 中。

##### ConfigFileApplicationContextInitializer

`ConfigFileApplicationContextInitializer` 是一个 `ApplicationContextInitializer` ，你可以用在你的测试中用来加载 Spring Boot `application.properties` 文件。当你不需要使用 `@SpringBootTest` 提供的完整的特性集合的情况下可以使用它，如下面例子所示：

```java
@ContextConfiguration(classes = Config.class,
    initializers = ConfigFileApplicationContextInitializer.class)
```

> 单独使用 `ConfigFileApplicationContextInitializer` 不会提供对 `@Value("${…}")` 注入的支持。它仅仅保证 `application.properties` 文件被加载进入 Spring’s `Environment`。为了 `@Value` 支持，你需要要么额外配置一个 `PropertySourcesPlaceholderConfigurer` 或者使用 `@SpringBootTest`，它会自动为你配置一个。

##### TestPropertyValues

`TestPropertyValues` 帮助你快速地添加属性到 `ConfigurableEnvironment` 或者 `ConfigurableApplicationContext`。你可以通过 `key=value` 字符串调用它，如下：

```java
TestPropertyValues.of("org=Spring", "name=Boot").applyTo(env);
```

##### OutputCapture

`OutputCapture` 是一个 JUnit `Extension` ，可以用来捕获 `System.out` 和 `System.err` 输出。为你的测试类的构造函数添加 `@ExtendWith(OutputCaptureExtension.class)` 并注入 `CapturedOutput` 作为构造函数或者测试方法的一个参数，如下所示：

```java
@ExtendWith(OutputCaptureExtension.class)
class OutputCaptureTests {

    @Test
    void testName(CapturedOutput output) {
        System.out.println("Hello World!");
        assertThat(output).contains("World");
    }

}
```

##### TestRestTemplate

`TestRestTemplate` 是 Spring’s `RestTemplate` 的方便的替代品，在集成测试中非常有用。你可以获得一个普通的模板或者发送 Basic HTTP 认证 (使用用户名和密码) 的模板。无论哪种情况，该模板都会以测试友好的方式工作，而不会抛出服务端错误异常。

> Spring Framework 5.0 提供了一个新的 `WebTestClient` 用于 [WebFlux 集成测试](https://docs.spring.io/spring-boot/docs/2.2.5.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-webflux-tests) 和 [WebFlux 和 MVC 端到端测试](https://docs.spring.io/spring-boot/docs/2.2.5.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-with-running-server)。它提供了链式的 API 用于断言，这一点不同于 `TestRestTemplate`。

推荐。而非强制要求，使用 Apache HTTP Client (version 4.3.2 或更高)。如果你的类路径上存在，则 `TestRestTemplate` 就会作为你合理配置客户端的响应。如果你没有使用 Apache’s HTTP client，则有其它测试友好的特性可用：

- Redirects 不被允许 (因此你可以断言相应位置)。
- Cookies 被忽略 (因此该模板是无状态的)。

`TestRestTemplate` 可以在你的集成测试中直接被实例化，如下面例子所示：

```java
public class MyTest {

    private TestRestTemplate template = new TestRestTemplate();

    @Test
    public void testRequest() throws Exception {
        HttpHeaders headers = this.template.getForEntity(
                "https://myhost.example.com/example", String.class).getHeaders();
        assertThat(headers.getLocation()).hasHost("other.example.com");
    }

}
```

另外，如果您结合 `WebEnvironment.RANDOM_PORT` 或 `WebEnvironment.DEFINED_PORT` 使用 `@SpringBootTest` 注解，则可以注入完全配置的 `TestRestTemplate` 并开始使用它。如有必要，可以通过 `RestTemplateBuilder` bean 来应用其他定制。未指定主机和端口的所有 URL 都会自动连接到嵌入式服务器，如以下示例所示：

```java
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
class SampleWebClientTests {

    @Autowired
    private TestRestTemplate template;

    @Test
    void testRequest() {
        HttpHeaders headers = this.template.getForEntity("/example", String.class).getHeaders();
        assertThat(headers.getLocation()).hasHost("other.example.com");
    }

    @TestConfiguration(proxyBeanMethods = false)
    static class Config {

        @Bean
        RestTemplateBuilder restTemplateBuilder() {
            return new RestTemplateBuilder().setConnectTimeout(Duration.ofSeconds(1))
                    .setReadTimeout(Duration.ofSeconds(1));
        }

    }

}
```

### 4.26. WebSockets

Spring Boot 提供了 WebSockets 自动配置用于内置的 Tomcat， Jetty，以及 Undertow。如果你将你的 war 文件部署在一个独立的容器中，Spring Boot 假定该容器会负责配置它自己的 WebSocket 支持。

Spring Framework 提供了 [丰富的 WebSocket 支持](https://docs.spring.io/spring/docs/5.2.4.RELEASE/spring-framework-reference/web.html#websocket) 用于 MVC web 应用，可以通过 `spring-boot-starter-websocket` 模块很方便地访问。

WebSocket 支持也可用于 [反应式 web 应用](https://docs.spring.io/spring/docs/5.2.4.RELEASE/spring-framework-reference/web-reactive.html#webflux-websocket) ，并且需要包含 WebSocket API 和 `spring-boot-starter-webflux`：

```xml
<dependency>
    <groupId>javax.websocket</groupId>
    <artifactId>javax.websocket-api</artifactId>
</dependency>
```

### 4.27. Web Services

Spring Boot 提供 Web Services 自动配置，你所需要做的就只是定义你的 `Endpoints`。

[Spring Web Services 特性](https://docs.spring.io/spring-ws/docs/3.0.8.RELEASE/reference/) 能够很方便地通过 `spring-boot-starter-webservices` 模块访问。

`SimpleWsdl11Definition` 和 `SimpleXsdSchema` beans 能够自动创建，分别用于 WSDLs 和 XSDs 。为了实现这一点，配置它们的位置，如下面例子所示：

```properties
spring.webservices.wsdl-locations=classpath:/wsdl
```

#### 4.27.1. 使用 `WebServiceTemplate` 调用 Web Services 

如果你需要在应用中调用远程 Web services ，可以使用 [`WebServiceTemplate`](https://docs.spring.io/spring-ws/docs/3.0.8.RELEASE/reference/#client-web-service-template) 类。由于 `WebServiceTemplate` 使用之前通常都需要按照需求自定义，Spring Boot 并未提供任何单独的自动配置的 `WebServiceTemplate` bean。相反，它自动配置了一个 `WebServiceTemplateBuilder` ，用来按需创建 `WebServiceTemplate` 实例。

下面是个典型的例子：

```java
@Service
public class MyService {

    private final WebServiceTemplate webServiceTemplate;

    public MyService(WebServiceTemplateBuilder webServiceTemplateBuilder) {
        this.webServiceTemplate = webServiceTemplateBuilder.build();
    }

    public DetailsResp someWsCall(DetailsReq detailsReq) {
         return (DetailsResp) this.webServiceTemplate.marshalSendAndReceive(detailsReq, new SoapActionCallback(ACTION));
    }

}
```

默认地， `WebServiceTemplateBuilder` 探测合适的 HTTP-based `WebServiceMessageSender` 使用类路径上可用的 HTTP client 类库。你也可以如下自定义读取或者连接超时时间：

```java
@Bean
public WebServiceTemplate webServiceTemplate(WebServiceTemplateBuilder builder) {
    return builder.messageSenders(new HttpWebServiceMessageSenderBuilder()
            .setConnectTimeout(5000).setReadTimeout(2000).build()).build();
}
```

### 4.28.  创建你自己的  Auto-configuration

如果你在一个开发共享类库的公司，或者你在使用开源或者社区类库，你可能希望开发自己的自动配置。自动配置类可以打包成为外部 jars 包，从而仍然能够被 Spring Boot 使用。

自动配置可以配置启动器使用，像那些同样提供了自动配置的典型类库那样。我们首先介绍构建自己的自动配置所需要了解的内容，然后介绍 [创建自定义启动器的必需步骤](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-custom-starter) 。

>  这个 [示例项目](https://github.com/snicoll-demos/spring-boot-master-auto-configuration) 可以展示如何一步步创建一个启动器。

#### 4.28.1. 理解自动配置 Beans

在底层，自动配置由标准的 `@Configuration` 类实现。附加的 `@Conditional` 注解用来限制何时应用自动配置。通常，自动配置类使用 `@ConditionalOnClass` 和 `@ConditionalOnMissingBean` 注解。这能够保证该自动配置只是在相关类没有找到，以及当你没有声明自己的 `@Configuration` 类时。

你可以阅读 [`spring-boot-autoconfigure`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure) 的源码来了解 Spring 提供的 `@Configuration` 类 (参考 [`META-INF/spring.factories`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/resources/META-INF/spring.factories) 文件)。

#### 4.28.2. 定位自动配置候选者

Spring Boot 会检查你发布的 jar 中是否存在 `META-INF/spring.factories` 文件。该文件应该在 `EnableAutoConfiguration` 键下列出你的配置类，如下面例子所示：

```
org.springframework.boot.autoconfigure.EnableAutoConfiguration=\
com.mycorp.libx.autoconfigure.LibXAutoConfiguration,\
com.mycorp.libx.autoconfigure.LibXWebAutoConfiguration
```

> 自动配置必须通过唯一的特殊方式加载。确保它们定义在特定的包空间下，使得它们永远不会成为组件扫描的目标。进一步地，自动配置类不应该开启组件扫描发现附加组件。可以使用特定的 `@Import` 来替代。

如果你的配置需要按照特定顺序应用，你可以使用 [`@AutoConfigureAfter`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/AutoConfigureAfter.java) 或者 [`@AutoConfigureBefore`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/AutoConfigureBefore.java) 注解。比如，如果你提供了特定与 web 的配置，该配置类就需要在 `WebMvcAutoConfiguration` 之后应用。

如果你希望排序某些互相完全不了解的自动配置，你也可以使用 `@AutoConfigureOrder`。该注解提供了与普通的 `@Order` 注解相同的语义，但是未自动配置类提供了专用的顺序。

#### 4.28.3. 条件注解

你几乎永远都希望在自动配置类中包含一个或者多个 `@Conditional` 注解。`@ConditionalOnMissingBean`  注解是一个常用的例子，用来允许开发者在某些不符合默认条件的情况下覆盖自动配置。

Spring Boot 包含大量的 `@Conditional` 注解，你可以在你的代码中注解 `@Configuration` 类或者单个的 `@Bean` 方法。这些注解包括：

- [Class 条件](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-class-conditions)
- [Bean 条件](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-bean-conditions)
- [Property 条件](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-property-conditions)
- [Resource 条件](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-resource-conditions)
- [Web Application 条件](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-web-application-conditions)
- [SpEL Expression 条件](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-spel-conditions)

##### Class 条件

`@ConditionalOnClass` 和 `@ConditionalOnMissingClass` 注解允许根据特定类的存在或不存在来包含 `@Configuration` 类。由于注解元数据是使用 [ASM](https://asm.ow2.org/) 进行解析的，因此即使该类实际上可能不会出现在运行的应用程序类路径上，也可以使用`value`属性来引用真实的类。如果您更愿意通过使用`String`值来指定类名，那么也可以使用`name`属性。

这种机制不适用于通常使用返回类型作为条件的目标的 `@Bean` 方法：在方法的条件适用之前，JVM 将加载该类和可能经过处理的方法引用，如果该类不存在，则该方法将失败。

为了处理这种情况，可以使用一个单独的 `@Configuration` 类来隔离条件，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
// Some conditions
public class MyAutoConfiguration {

    // Auto-configured beans

    @Configuration(proxyBeanMethods = false)
    @ConditionalOnClass(EmbeddedAcmeService.class)
    static class EmbeddedConfiguration {

        @Bean
        @ConditionalOnMissingBean
        public EmbeddedAcmeService embeddedAcmeService() { ... }

    }

}
```

> 如果你使用 `@ConditionalOnClass` 或者 `@ConditionalOnMissingClass` 作为部分元注解来组成你的组合注解，你必须使用 `name` 作为这种情况下未被处理的类的引用。

##### Bean 条件

通过使用 `@ConditionalOnBean` 和 `@ConditionalOnMissingBean` 注解，可以根据是否存在特定的 bean 来包含 bean。您可以使用 `value` 属性按类型指定 bean，或使用 `name` 按名称指定 bean。使用 `search` 属性可以限制在搜索 bean 时应考虑的 `ApplicationContext` 层次结构。

当放在 `@Bean` 方法上时，目标类型默认为方法的返回类型，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
public class MyAutoConfiguration {

    @Bean
    @ConditionalOnMissingBean
    public MyService myService() { ... }

}
```

前面的例子中， `myService` bean 将被创建，如果类型为 `MyService` 的 bean 尚未包含在 `ApplicationContext` 中时。

> 您需要非常注意添加 bean 定义的顺序，因为这些条件是根据到目前为止已处理的内容来评估的。因此，我们建议在自动配置类上仅使用 `@ConditionalOnBean` 和 `@ConditionalOnMissingBean` 注解（保证在添加任何用户定义的 Bean 定义后将加载这些注解）。

> `@ConditionalOnBean` 和 `@ConditionalOnMissingBean` 不会阻止创建 `@Configuration` 类。在类级别使用这些条件与使用注解标记每个包含的 `@Bean` 方法之间的唯一区别是，如果条件不匹配，则前者会阻止将 `@Configuration` 类注册为 bean。

##### Property 条件

通过 `@ConditionalOnProperty` 注解，可以基于 Spring Environment 属性包含配置。使用`prefix`和`name`属性来指定应检查的属性。默认情况下，匹配存在且不等于 `false` 的任何属性。您还可以使用 `havingValue` 和 `matchIfMissing` 属性来创建更高级的检查。

##### Resource 条件

`@ConditionalOnResource` 注解仅在存在特定资源时才包括配置。可以使用通常的 Spring 约定来指定资源，如以下示例所示： `file:/home/user/test.dat` 。

##### Web Application 条件

通过 `@ConditionalOnWebApplication` 和 `@ConditionalOnNotWebApplication` 注解，可以根据应用程序是否为 Web 应用程序来包含配置。基于 Servlet 的 Web 应用程序是任何使用 Spring `WebApplicationContext`，定义 `session` 作用域或具有 `ConfigurableWebEnvironment` 的应用程序。响应式 Web 应用程序是使用 `ReactiveWebApplicationContext` 或具有 `ConfigurableReactiveWebEnvironment` 的任何应用程序。

##### SpEL Expression 条件

`@ConditionalOnExpression` 注解允许根据 [SpEL expression](https://docs.spring.io/spring/docs/5.2.5.RELEASE/spring-framework-reference/core.html#expressions) 的结果来决定是否包含配置。

#### 4.28.4. 测试你的自动配置

自动配置可能受许多因素影响：用户配置（`@Bean` 定义和 `Environment` 自定义），条件评估（存在特定库）以及其他因素。具体而言，每个测试都应创建定义良好的 `ApplicationContext`，以表示这些自定义项的组合。`ApplicationContextRunner` 提供了一种实现此目标的好方法。

通常将 `ApplicationContextRunner` 定义为测试类的一个字段，以收集基本的通用配置。下面的示例确保始终调用 `UserServiceAutoConfiguration`：

```java
private final ApplicationContextRunner contextRunner = new ApplicationContextRunner()
        .withConfiguration(AutoConfigurations.of(UserServiceAutoConfiguration.class));
```

> 如果必须定义多个自动配置，则无需按与运行应用程序时完全相同的顺序调用它们的声明。

每个测试都可以使用运行器来表示特定的用例。例如，下面的示例调用一个用户配置（`UserConfiguration`），并检查自动配置是否正确退出。调用`run`提供了可与`Assert4J`一起使用的回调上下文。

```java
@Test
void defaultServiceBacksOff() {
    this.contextRunner.withUserConfiguration(UserConfiguration.class).run((context) -> {
        assertThat(context).hasSingleBean(UserService.class);
        assertThat(context).getBean("myUserService").isSameAs(context.getBean(UserService.class));
    });
}

@Configuration(proxyBeanMethods = false)
static class UserConfiguration {

    @Bean
    UserService myUserService() {
        return new UserService("mine");
    }

}
```

同样可能很容易地自定义 `Environment` ，如下面例子所示：

```java
@Test
void serviceNameCanBeConfigured() {
    this.contextRunner.withPropertyValues("user.name=test123").run((context) -> {
        assertThat(context).hasSingleBean(UserService.class);
        assertThat(context.getBean(UserService.class).getName()).isEqualTo("test123");
    });
}
```

运行器也可以用来显示`ConditionEvaluationReport`。该报告可以以 `INFO` 或 `DEBUG` 级别打印。以下示例显示了如何使用`ConditionEvaluationReportLoggingListener`在自动配置测试中打印报告。

```java
@Test
public void autoConfigTest {
    ConditionEvaluationReportLoggingListener initializer = new ConditionEvaluationReportLoggingListener(
            LogLevel.INFO);
    ApplicationContextRunner contextRunner = new ApplicationContextRunner()
            .withInitializer(initializer).run((context) -> {
                    // Do something...
            });
}
```

##### 模拟 Web 上下文

如果您需要测试仅在 Servlet 或 Reactive Web 应用程序上下文中运行的自动配置，请分别使用`WebApplicationContextRunner`或`ReactiveWebApplicationContextRunner`。

##### 覆盖类路径

也可以测试在运行时不存在特定的类和/或程序包时发生的情况。Spring Boot 附带有一个 `FilteredClassLoader`，运行器可以轻松使用。在以下示例中，我们断言，如果不存在 `UserService`，则会自动禁用自动配置：

```java
@Test
void serviceIsIgnoredIfLibraryIsNotPresent() {
    this.contextRunner.withClassLoader(new FilteredClassLoader(UserService.class))
            .run((context) -> assertThat(context).doesNotHaveBean("userService"));
}
```

#### 4.28.5. 创建你自己的启动器

一个类库的完整 Spring Boot 启动器可能包含下列组件：

- 包含自动配置代码的 `autoconfigure` 模块。
- `starter` 模块，提供 `autoconfigure` 模块所需的依赖、类库以及任何附加的有用以来。简而言之，添加启动器应该提供开始使用该类库所需的所有条件。

> 如果你不需要分开管理自动配置和依赖管理，你就可以将两者组合为一个模块。

##### 命名

您应确保为启动器提供适当的名称空间。即使使用不同的 Maven`groupId`，也不要以`spring-boot`开头模块名称。将来，我们可能会为您自动配置的内容提供官方支持。

根据经验，应在启动器后命名一个组合模块。例如，假设您要为 `acme` 创建启动器，并命名自动配置模块 `acme-spring-boot-autoconfigure` 和启动器 `acme-spring-boot-starter`。如果只有一个将两者结合的模块，则将其命名为 `acme-spring-boot-starter`。

##### 配置键

如果你的启动器提供配置键，为它们使用唯一的命名空间。特别的，切勿将你的配置键包含到 Spring Boot 使用的明明空间中（比如 `server`，`management`，`spring`  等等）。如果你使用相同的命名空间，你就可能随后意外修改这些命名空间，从而打破你的模块。根据经验，最佳实践是为你的配置键添加你所使用的命名空间前缀（比如，`acme`）。

确保所有的配置键中的每个属性都添加了 javadoc 文档说明，如下面例子所示：

```java
@ConfigurationProperties("acme")
public class AcmeProperties {

    /**
     * Whether to check the location of acme resources.
     */
    private boolean checkLocation = true;

    /**
     * Timeout for establishing a connection to the acme server.
     */
    private Duration loginTimeout = Duration.ofSeconds(3);

    // getters & setters

}
```

> 您应该仅将简单文本与 `@ConfigurationProperties` 字段 Javadoc 一起使用，因为在将它们添加到 JSON 之前不会对其进行处理。

这里是一些我们默认遵循的规则以保持描述的一致性：

- 不要用 "The" 或者 "A" 开始描述。
- 对于 `boolean` 类型，使用 "Whether" 或者 "Enable" 开始描述。
- 对于基于集合的类型，使用 "Comma-separated list" 开始描述。
- 使用 `java.time.Duration` 而不是 `long` ，同时描述默认单位，如果不是毫秒。比如：如果没有使用时间间隔后缀，那么使用的就是秒。
- 描述中不要给出默认值，除非它必须在运行时确定。

确保 [触发元数据生成](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#configuration-metadata-annotation-processor) 以便 IDE 助手也能够对你的配置键产生作用。你可能希望浏览生成的元数据 (`META-INF/spring-configuration-metadata.json`) 以确保你的配置键都被准确地文档化了。在兼容的 IDE 中使用你的启动器也是检验这些元数据质量的好办法。

##### `autoconfigure` 模块

 `autoconfigure` 模块包含了开始使用类库所需要的一切。它还可以包含配置键定义 (比如 `@ConfigurationProperties`) 以及所有回调接口，这些回调接口可以用来进一步自定义组件的初始化。

> 您应该将对库的依赖项标记为可选，以便可以更轻松地在项目中包含`autoconfigure`模块。如果这样做，将不提供该库，并且默认情况下，Spring Boot 将退出。

Spring Boot 使用注解处理器来收集元数据文件 (`META-INF/spring-autoconfigure-metadata.properties`) 中自动配置的条件。如果存在该文件，它将用于过滤不匹配的自动配置，这将缩短启动时间。建议在包含自动配置的模块中添加以下依赖项：

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-autoconfigure-processor</artifactId>
    <optional>true</optional>
</dependency>
```

对 Gradle 4.5 或者更早版本，依赖项应该声明在 `compileOnly` 配置中，如下所示：

```groovy
dependencies {
    compileOnly "org.springframework.boot:spring-boot-autoconfigure-processor"
}
```

对 Gradle 4.6 或者更高版本，依赖项应该声明在 `annotationProcessor` 配置中，如下所示：

```groovy
dependencies {
    annotationProcessor "org.springframework.boot:spring-boot-autoconfigure-processor"
}
```

##### Starter 模块

起动器确实是一个空 jar 。其唯一目的是提供必要的依赖关系以使用库。您可以将其视为对开始使用所需条件的视图。

不要对添加了启动器的项目做出假设。如果您要自动配置的库通常需要其他启动器，请也提及它们。如果可选依赖项的数量很高，那么提供一组适当的 *default* 依赖项可能会很困难，因为您应该避免包括对于库的典型用法而言不必要的依赖项。换句话说，您不应包括可选的依赖项。

> 无论哪种方式，您的启动器都必须直接或间接引用核心 Spring Boot 启动器（`spring-boot-starter`）（即，如果您的启动器依赖于另一个启动器，则无需添加它）。如果仅使用您的自定义启动器创建了一个项目，则该核心启动器的存在将兑现 Spring Boot 的核心功能。

### 4.30. 进一步学习

如果你想要深入了解本章节讨论的任何类，请参考 [Spring Boot API documentation](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/api/) ，或者可以 [直接浏览源代码](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE)。如果你有任何其他问题，参考 [how-to](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#howto) 章节。

如果你更感兴趣 Spring Boot 的核心特性，你可以继续阅读本文档后续的 [production-ready features](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready)。

## 5. Spring Boot Actuator：生产就绪特性

当你把应用发布到生产环境，Spring Boot 包含大量特性帮助你监控和管理你的应用。你可以选择通过使用 HTTP 端点或者 JMX 监控管理你的应用。审计、健康监测、性能指标收集等功能也会自动应用到你的应用。

### 5.1. 启用生产就绪特性

[`spring-boot-actuator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator) 模块提供了所有 Spring Boot 的生产就绪特性。开启这一特性最简单的方法就是添加一个 `spring-boot-starter-actuator` 启动器的依赖。

> Actuator 定义
>
> 执行器是制造业术语，是指用于移动或控制某些物体的机械设备。执行器可以通过很小的变化产生大量的运动。

添加执行器到基于 Maven 的项目，添加下面的启动器依赖：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
</dependencies>
```

对于 Gradle，使用下面的声明：

```groovy
dependencies {
    compile("org.springframework.boot:spring-boot-starter-actuator")
}
```

### 5.2. 端点

执行器端点允许你监控你的引用并与之交互。Spring Boot 包含大量内建端点，同时允许你自行添加自己的端点。比如，`health` 端点提供了基本的应用健康信息。

每个端点都可以单独 [开启或者关闭](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-endpoints-enabling-endpoints)。这可以控制该端点是否会被创建，以及相关的 bean 是否存在于应用上下文中。为了远程访问，端点必须 [通过 JMX 或者 HTTP 暴露](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-endpoints-exposing-endpoints)。大部分应用选择了 HTTP，此时，端点的 ID 包含前缀 `/actuator` 映射到一个 URL。比如，默认地，`health` 端点映射到 `/actuator/health`。

下列与技术无关的端点是可用的：

| ID                 | Description                                                  |
| :----------------- | :----------------------------------------------------------- |
| `auditevents`      | 暴露当前应用的审计事件信息。需要 `AuditEventRepository` bean。 |
| `beans`            | 展示你的应用中所有 Spring beans 的完整列表。                 |
| `caches`           | 暴露可用的缓存。                                             |
| `conditions`       | 展示配置和自动配置上被评估的条件，以及它们满足与否的原因。   |
| `configprops`      | 展示所有的 `@ConfigurationProperties` 的整理好的列表。       |
| `env`              | 暴露来自 Spring’s `ConfigurableEnvironment` 的属性。         |
| `flyway`           | 显示任何已经被应用的 Flyway database 迁移。需要一个或者多个 `Flyway` beans。 |
| `health`           | 显示应用健康状态信息。                                       |
| `httptrace`        | 显示 HTTP 跟踪信息（默认地，最近 100 次请求-响应交互）。需要 `HttpTraceRepository` bean。 |
| `info`             | 显示任意应用信息。                                           |
| `integrationgraph` | 展示 Spring 集成图。需要 `spring-integration-core` 依赖。    |
| `loggers`          | 展示和修改应用中的日志记录器配置。                           |
| `liquibase`        | 展示任何已经应用的 Liquibase 数据库迁移。需要一个或者多个 `Liquibase` beans。 |
| `metrics`          | 显示当前应用的 ‘metrics’ 信息。                              |
| `mappings`         | 显示整理好的所有 `@RequestMapping` 路径的列表。              |
| `scheduledtasks`   | 显示你的应用中的调度任务。                                   |
| `sessions`         | 允许从 Spring Session 支持的会话存储中检索和删除用户会话。需要使用 Spring Session 的基于 Servlet 的 Web 应用程序。 |
| `shutdown`         | 允许应用优雅地关闭。默认关闭。                               |
| `threaddump`       | 执行线程转储。                                               |

如果你的应用是 web 应用 (Spring MVC, Spring WebFlux, 或者 Jersey)，你还可以使用下面的附加端点：

| ID           | Description                                                  |
| :----------- | :----------------------------------------------------------- |
| `heapdump`   | 返回一个 `hprof` 堆转储文件。                                |
| `jolokia`    | 通过 HTTP暴露 JMX beans  (当 Jolokia 在类路径上时，对 WebFlux 不可用)。需要 `jolokia-core` 依赖。 |
| `logfile`    | 返回日志文件的内容 (如果设置了 `logging.file.name` 或者 `logging.file.path` 属性)。支持使用 HTTP `Range` 请求首部获取日志文件的部分内容。 |
| `prometheus` | 以 Prometheus 服务器可以抓取的格式暴露指标信息。需要依赖于`micrometer-registry-prometheus`。 |

了解更多有关 Actuator’s 端点以及相应的请求响应格式，请参考独立 API 文档 ([HTML](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/actuator-api//html/) 或者 [PDF](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/actuator-api//pdf/spring-boot-actuator-web-api.pdf))。

#### 5.2.1. 开启端点

默认情况下，除 `shutdown` 外的所有端点均处于启用状态。要配置端点的启用，请使用其`management.endpoint..enabled`属性。以下示例启用了`shutdown`端点：

```properties
management.endpoint.shutdown.enabled=true
```

如果您宁愿选择默认关闭所有端点而手动个别开启，请将 `management.endpoints.enabled-by-default` 属性设置为 `false`，并使用各个端点 `enabled` 属性进行开启。以下示例启用`info`端点并禁用所有其他端点：

```properties
management.endpoints.enabled-by-default=false
management.endpoint.info.enabled=true
```

> 被关闭的端点会从应用上下文中彻底删除。如果你只希望在该端点暴露的具体技术实现层面进行控制，使用 [`include` 和 `exclude` 属性](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-endpoints-exposing-endpoints) 代替。

#### 5.2.2. 暴露端点

由于端点可能包含敏感信息，谨慎考虑何时暴露它们。下表展示了内建端点的默认暴露情况：

| ID                 | JMX  | Web  |
| :----------------- | :--- | :--- |
| `auditevents`      | Yes  | No   |
| `beans`            | Yes  | No   |
| `caches`           | Yes  | No   |
| `conditions`       | Yes  | No   |
| `configprops`      | Yes  | No   |
| `env`              | Yes  | No   |
| `flyway`           | Yes  | No   |
| `health`           | Yes  | Yes  |
| `heapdump`         | N/A  | No   |
| `httptrace`        | Yes  | No   |
| `info`             | Yes  | Yes  |
| `integrationgraph` | Yes  | No   |
| `jolokia`          | N/A  | No   |
| `logfile`          | N/A  | No   |
| `loggers`          | Yes  | No   |
| `liquibase`        | Yes  | No   |
| `metrics`          | Yes  | No   |
| `mappings`         | Yes  | No   |
| `prometheus`       | N/A  | No   |
| `scheduledtasks`   | Yes  | No   |
| `sessions`         | Yes  | No   |
| `shutdown`         | Yes  | No   |
| `threaddump`       | Yes  | No   |

为了修改端点的暴露情况，使用下面的特定于技术的 `include` 和 `exclude` 属性：

| Property                                    | Default        |
| :------------------------------------------ | :------------- |
| `management.endpoints.jmx.exposure.exclude` |                |
| `management.endpoints.jmx.exposure.include` | `*`            |
| `management.endpoints.web.exposure.exclude` |                |
| `management.endpoints.web.exposure.include` | `info, health` |

`include` 属性列出了暴露的端点的 IDs。`exclude` 属性列出了不应该暴露的端点。后者的优先级高于前者。两者都可以配置为端点 IDs 列表。

比如，为了停止所有通过 JMX 暴露的端点，仅仅暴露 `health` 和 `info` 端点，使用下面的属性：

```properties
management.endpoints.jmx.exposure.include=health,info
```

`*` 可以用于选择所有端点。比如，为了通过 HTTP 暴露所有端点，除了 `env` 和 `beans` 端点，使用下面的属性：

```properties
management.endpoints.web.exposure.include=*
management.endpoints.web.exposure.exclude=env,beans
```

> `*` 在 YMAL 中有特殊含义，因此需要用双引号标识，以表示选择或者不选所有端点。如下面例子所示：
>
> ````
> management:
>   endpoints:
>     web:
>       exposure:
>         include: "*"
> ````

> 如果你的应用暴露在公开环境中，我们强烈建议你 [为你的端点添加安全设施](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-endpoints-security)。 

> 如果你想要实现自己的端点暴露策略，你可以注册一个 `EndpointFilter` bean。

#### 5.2.3. 保护 HTTP 端点

您应该像对待其他任何敏感 URL 一样，小心保护 HTTP 端点的安全。如果存在 Spring Security，则默认情况下将使用 Spring Security 的内容协商策略保护端点的安全。例如，如果您希望为 HTTP 端点配置自定义安全性，只允许具有特定角色的用户访问它们，Spring Boot 提供了一些方便的 `RequestMatcher` 对象，可以将它们与 Spring Security 结合使用。

典型的 Spring Security 配置看起来类似下面这样：

```java
@Configuration(proxyBeanMethods = false)
public class ActuatorSecurity extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.requestMatcher(EndpointRequest.toAnyEndpoint()).authorizeRequests((requests) ->
                requests.anyRequest().hasRole("ENDPOINT_ADMIN"));
        http.httpBasic();
    }

}
```

上面的例子使用 `EndpointRequest.toAnyEndpoint()` 来匹配发往任何端点的请求以确保它们都具有 `ENDPOINT_ADMIN` 角色。 `EndpointRequest` 上还具有若干其他匹配方法可用。参考 API 文档 ([HTML](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/actuator-api//html) 或者 [PDF](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/actuator-api//pdf/spring-boot-actuator-web-api.pdf)) 获取更多细节。

如果你的应用部署在防火墙之后，你可能更倾向于你的执行器端点可以不需要强制身份认证。你可以通过修改 `management.endpoints.web.exposure.include` 属性来做到这一点，如下所示：

**application.properties**

```properties
management.endpoints.web.exposure.include=*
```

另外，如果存在 Spring Security，则需要添加自定义安全配置，该配置允许未经身份认证的端点访问，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
public class ActuatorSecurity extends WebSecurityConfigurerAdapter {

    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.requestMatcher(EndpointRequest.toAnyEndpoint()).authorizeRequests((requests) ->
            requests.anyRequest().permitAll());
    }

}
```

#### 5.2.5. 用于执行器 Web 端点的超媒体

添加了一个“发现页面”，其中包含指向所有端点的链接。默认情况下， `/actuator` 上提供“发现页面”。

配置了自定义管理上下文路径后，“发现页面”会自动从 `/actuator` 移动到管理上下文的根目录。例如，如果管理上下文路径为 `/management`，则发现页面可从 `/management` 访问。当管理上下文路径设置为`/`时，发现页面将被禁用，以防止与其他映射发生冲突的可能性。

#### 5.2.6. CORS 支持

[跨域资源共享](https://en.wikipedia.org/wiki/Cross-origin_resource_sharing) (CORS) is a [W3C 规范](https://www.w3.org/TR/cors/) ，允许你以灵活的方式指定哪种跨域请求是被授权的。如果你使用 Spring MVC 或者 Spring WebFlux，执行器 Actuator 的 web 端点能够配置为支持这种场景。

CORS 支持默认关闭，只有当 `management.endpoints.web.cors.allowed-origins` 属性被设定之后才会开启。下面的配置许可来自 `example.com` 域名的 `GET` 和 `POST` 调用：

```properties
management.endpoints.web.cors.allowed-origins=https://example.com
management.endpoints.web.cors.allowed-methods=GET,POST
```

> 参考 [CorsEndpointProperties](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator-autoconfigure/src/main/java/org/springframework/boot/actuate/autoconfigure/endpoint/web/CorsEndpointProperties.java) 获取选项的完整列表。

#### 5.2.7. 实现自定义端点

如果你添加带有 `@Endpoint` 注解的 `@Bean` 注解，任何使用 `@ReadOperation`, `@WriteOperation`, 或者 `@DeleteOperation` 注解修饰的方法都会自动通过 JMX 暴露，如果是在 web 应用中，同时还会通过 HTTP 暴露。端点能够通过 HTTP 暴露，使用 Jersey, Spring MVC, 或者 Spring WebFlux。如果 Jersey 和 Spring MVC 都可用，Spring MVC 将会被使用。

你也可以使用 `@JmxEndpoint` 或者 `@WebEndpoint` 编写特定于技术的端点。这些端点局限于它们各自相应的技术。比如， `@WebEndpoint` 仅仅通过 HTTP 暴露，而不通过 JMX 暴露。

你可以使用 `@EndpointWebExtension` 和 `@EndpointJmxExtension` 编写特定于技术的扩展。这些注解允许你提供特定技术的操作以配置现有的端点。

最后，如果你需要访问特定于 web 框架的功能，你可以实现 Servlet 或者 Spring `@Controller` 和 `@RestController` 端点，不过代价是它们无法通过 JMX 暴露，并且当使用不同的 web 框架时不可用。

##### 接收输入

端点上的操作通过它们的参数接收输入。当通过 web 暴露时，这些参数的值取自 URL 的查询参数以及 JSON 请求体。当通过 JMX 暴露时，参数被映射到 MBean 操作的参数。参数默认是强制需要的。通过使用 `@org.springframework.lang.Nullable` 注解修饰它们可以将其变为可选的。

JSON 请求体中的每个根属性都能够映射到端点参数。考虑下面的 JSON 请求体：

```json
{
    "name": "test",
    "counter": 42
}
```

这可以被用于调用一个携带 `String name` 和 `int counter` 参数的写操作。

> 由于端点与技术无关，因此只能在方法签名中指定简单类型。特别地，不支持使用自定义类型声明一个单独的参数来定义 `name` 和 `counter` 属性。

> 为了使输入映射到操作方法的参数，实现端点的 Java 代码应使用 `-parameters` 进行编译，而实现端点的 Kotlin 代码应使用 `-java-parameters` 进行编译。如果您使用的是 Spring Boot 的 Gradle 插件，或者您使用的是 Maven 和 `spring-boot-starter-parent`，则此操作会自动发生。

###### 输入类型转换

传递给端点操作方法的参数，如果必要，会自动被转换为需要的数据类型。在调用操作方法之前，通过 JMX 或者 HTTP 请求接收的输入被转换为需要的数据类型，使用一个  `ApplicationConversionService` 实例。或者任何由 `@EndpointConverter` 修饰的 `Converter` 或者 `GenericConverter` beans。

##### 自定义 Web 端点

一个 `@Endpoint`, `@WebEndpoint`, 或者 `@EndpointWebExtension` 上的操作会自动通过 HTTP 暴露，使用 Jersey, Spring MVC, 或者 Spring WebFlux。如果 Jersey 和 Spring MVC 都可用， Spring MVC 将被优先使用。

###### Web 端点请求谓词

请求谓词会为 web 暴露端点上的每个操作自动生成。

###### Path

谓词的路径由端点的 ID 和暴露的端点的根路径决定。默认的根路径是 `/actuator`。比如，ID 为 `sessions` 的端点将使用 `/actuator/sessions` 作为它的谓词中的路径。

通过使用 `@Selector` 注解修饰操作方法的一个或多个参数，可以进一步自定义路径。将这样的参数作为路径变量添加到路径谓词。调用端点操作时，变量的值将传递到操作方法中。如果要捕获所有剩余的路径元素，则可以在最后一个参数上添加 `@Selector(Match=ALL_REMAINING)` ，并将其设置为与 `String[]` 兼容的转换类型。

###### HTTP 方法

谓词的 HTTP 方法取决于操作类型，如下所示：

| Operation          | HTTP method |
| :----------------- | :---------- |
| `@ReadOperation`   | `GET`       |
| `@WriteOperation`  | `POST`      |
| `@DeleteOperation` | `DELETE`    |

###### Consumes

对于使用请求体的 `@WriteOperation` (HTTP `POST`)，谓词的 consumes 子句是 `application/vnd.spring-boot.actuator.v2+json, application/json`。对于其他操作，consumes 子句是空。

###### Produces

谓词的 produces 子句由 `@DeleteOperation`, `@ReadOperation`, 和 `@WriteOperation` 注解的 `produces` 属性确定。该属性是可选的，如果没有使用，则 produces 子句被自动确定。

如果操作方法返回 `void` 或者 `Void` 则 produces 子句是空。如果操作防范返回 `org.springframework.core.io.Resource`，produces 子句是 `application/octet-stream`。所有其他操作， produces 子句是 `application/vnd.spring-boot.actuator.v2+json, application/json`。

###### Web 端点响应状态

端点操作的响应状态默认取决于操作类型（读、写、或者删除），以及，如果存在，操作返回值。

一个 `@ReadOperation` 返回一个值，则响应状态将是 200 (OK)。如果它没有返回值，响应状态将是 404 (Not Found)。

如果一个 `@WriteOperation` 或者 `@DeleteOperation` 返回一个值，响应状态将是 200 (OK)。如果没有返回值，响应状态将是 204 (No Content)。

如果一个操作被无参数调用，或者调用参数无法转换为需要的类型，操作方法就不会被调用，并且响应状态将是 400 (Bad Request)。

###### Web Endpoint 范围请求

HTTP 范围请求可以用于请求部分 HTTP 资源。当使用 Spring MVC 或者 Spring Web Flux 时，返回 `org.springframework.core.io.Resource` 的操作自动支持范围请求。

> 使用 Jersey 时不支持范围请求。

###### Web 端点安全

在 Web 端点或特定于 Web 的端点扩展上的操作可以接收当前的 `java.security.Principal` 或 `org.springframework.boot.actuate.endpoint.SecurityContext` 作为方法参数。前者通常与 `@Nullable` 结合使用，以为经过身份验证和未经身份验证的用户提供不同的行为。后者通常用于使用其 `isUserInRole(String)` 方法执行授权检查。

##### Servlet 端点

通过实现带有 `@ServletEndpoint` 注解、同时也实现了 `Supplier` 的类，`Servlet` 可以作为端点公开。Servlet 端点提供了与 Servlet 容器的更深层集成，但以可移植性为代价。它们旨在用于将现有的 `Servlet` 公开为端点。对于新的端点，应尽可能使用 `@Endpoint` 和 `@WebEndpoint` 注解。

##### Controller 端点

`@ControllerEndpoint` 和 `@RestControllerEndpoint` 可用于实现仅由 Spring MVC 或 Spring WebFlux 公开的端点。方法使用 Spring MVC 和 Spring WebFlux 的标准注解（例如，`@RequestMapping` 和 `@GetMapping`）进行映射，端点的 ID 用作路径的前缀。控制器端点提供了与 Spring web 框架的更深层集成，但以可移植性为代价。尽可能使用 `@Endpoint` 和 `@WebEndpoint` 注解。

#### 5.2.8. 健康信息

你可以使用健康信息来检查运行中应用的状态。健康信息通常会被监控软件用来在生产系统发生故障时发出告警。健康信息通过 `health` 端点暴露，取决于 `management.endpoint.health.show-details` 和 `management.endpoint.health.show-components` 属性，这两个属性可以设置为下面的值：

| Name              | Description                                                  |
| :---------------- | :----------------------------------------------------------- |
| `never`           | 永远不展示细节。                                             |
| `when-authorized` | 细节信息只向授权用户展示。授权角色可以通过 `management.endpoint.health.roles` 配置。 |
| `always`          | 细节向所有用户展示。                                         |

默认值是 `never`。当用户属于一个或者多个端点角色时会被认为是授权用户。如果端点没有配置角色（默认情况）所有通过身份认证的用户都被认为是授权用户。角色可以通过 `management.endpoint.health.roles` 属性配置。

> 如果您已经保护了您的应用程序并希望使用 `always`，则您的安全配置必须允许经过身份验证的用户和未经身份验证的用户都可以访问健康状况端点。

健康状况信息收集自 [`HealthContributorRegistry`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthContributorRegistry.java) 的内容 (默认情况下所有定义在你的 `ApplicationContext` 中的 [`HealthContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthContributor.java) 实例)。Spring Boot 包含大量自动配置的 `HealthContributors` ，同时你哈可以编写你自己的。

一个 `HealthContributor` 可以是一个 `HealthIndicator` 或者一个 `CompositeHealthContributor`。`HealthIndicator`  提供实际的健康状况信息，包括 `Status`。`CompositeHealthContributor` 提供其他 `HealthContributors` 的组合。组合在一起，构成一个树形结构从整体上反映系统健康状况。

默认情况下，最终的系统健康状况是由 `StatusAggregator` 派生的，该 `StatusAggregator` 根据状态的有序列表对每个 `HealthIndicator` 中的状态进行排序。排序列表中的第一个状态用作整体运行状况。如果没有 `HealthIndicator` 返回 `StatusAggregator` 已知的状态，则使用 `UNKNOWN` 状态。

> `HealthContributorRegistry` 可以被用于在运行时注册或者注销健康状况指标。

##### 自动配置的健康状况指标

下面的 `HealthIndicators` 在适当的时候由 Spring Boot 自动配置：

| Name                                                         | Description                          |
| :----------------------------------------------------------- | :----------------------------------- |
| [`CassandraHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/cassandra/CassandraHealthIndicator.java) | 检查 Cassandra 数据库已经启动。      |
| [`CouchbaseHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/couchbase/CouchbaseHealthIndicator.java) | 检查 Couchbase 集群已经启动。        |
| [`DiskSpaceHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/system/DiskSpaceHealthIndicator.java) | 检查低磁盘空间。                     |
| [`DataSourceHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/jdbc/DataSourceHealthIndicator.java) | 检查与 `DataSource` 的连接可以获取。 |
| [`ElasticSearchRestHealthContributorAutoConfiguration`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/elasticsearch/ElasticSearchRestHealthContributorAutoConfiguration.java) | 检查 Elasticsearch 集群已经启动。    |
| [`HazelcastHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/hazelcast/HazelcastHealthIndicator.java) | 检查 Hazelcast 服务器已经启动。      |
| [`InfluxDbHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/influx/InfluxDbHealthIndicator.java) | 检查 InfluxDB 服务器已经启动。       |
| [`JmsHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/jms/JmsHealthIndicator.java) | 检查 JMS broker 已经启动。           |
| [`LdapHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/ldap/LdapHealthIndicator.java) | 检查 LDAP 服务器已经启动。           |
| [`MailHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/mail/MailHealthIndicator.java) | 检查邮件服务器已经启动。             |
| [`MongoHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/mongo/MongoHealthIndicator.java) | 检查 Mongo 数据库已经启动。          |
| [`Neo4jHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/neo4j/Neo4jHealthIndicator.java) | 检查 Neo4j 数据库已经启动。          |
| [`PingHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/PingHealthIndicator.java) | 永远响应 `UP`。                      |
| [`RabbitHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/amqp/RabbitHealthIndicator.java) | 检查 Rabbit 服务器已经启动。         |
| [`RedisHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/redis/RedisHealthIndicator.java) | 检查 Redis 服务器已经启动。          |
| [`SolrHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/solr/SolrHealthIndicator.java) | 检查 Solr 服务器已经启动。           |

> 你可以通过设置 `management.health.defaults.enabled` 属性将它们全部禁用。

##### 编写自定义健康状况指标

要提供自定义的健康信息，您可以注册实现 [`HealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthIndicator.java) 接口。您需要提供`health()`方法的实现并返回`Health`响应。 `Health` 响应应包含状态，并可以选择包含要显示的其他详细信息。以下代码显示了示例 `HealthIndicator` 的实现：

```java
import org.springframework.boot.actuate.health.Health;
import org.springframework.boot.actuate.health.HealthIndicator;
import org.springframework.stereotype.Component;

@Component
public class MyHealthIndicator implements HealthIndicator {

    @Override
    public Health health() {
        int errorCode = check(); // perform some specific health check
        if (errorCode != 0) {
            return Health.down().withDetail("Error Code", errorCode).build();
        }
        return Health.up().build();
    }

}
```

> 给定 `HealthIndicator` 的标识符是不带 `HealthIndicator` 后缀（如果存在）的 bean 名称。前面的例子中，健康信息可以通过名为 `my` 的入口得到。

除了 Spring Boot 预定义的 [`Status`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/Status.java) 类型，为 `Health` 返回自定义 `Status` 以表示新的系统状态也是可以的。这种情况下，需要提供相应的 [`StatusAggregator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/StatusAggregator.java) 接口自定义实现。或者该接口的默认实现通过 `management.endpoint.health.status.order` 配置属性进行了配置。

比如，假定携带编码 `FATAL` 的 `Status` 被用于你的 `HealthIndicator` 实现。为了配置优先顺序，将下面的属性添加到你的应用配置中：

```properties
management.endpoint.health.status.order=fatal,down,out-of-service,unknown,up
```

响应中的 HTTP 状态代码反映了总体健康状态（例如，`UP` 映射为 200，而 `OUT_OF_SERVICE` 和 `DOWN` 映射为 503）。如果通过 HTTP 访问运行状况端点，则可能还需要注册自定义状态映射。例如，以下属性将 `FATAL` 映射到 503（服务不可用）：

```properties
management.endpoint.health.status.http-mapping.fatal=503
```

> 如果你需要更多控制，可以定义你自己的 `HttpCodeStatusMapper` bean。

下表展示了内建状态包含的默认状态映射：

| Status         | Mapping                                      |
| :------------- | :------------------------------------------- |
| DOWN           | SERVICE_UNAVAILABLE (503)                    |
| OUT_OF_SERVICE | SERVICE_UNAVAILABLE (503)                    |
| UP             | No mapping by default, so http status is 200 |
| UNKNOWN        | No mapping by default, so http status is 200 |

##### 反应式健康指标

对于反应式应用，比如使用 Spring WebFlux 的应用， `ReactiveHealthContributor` 提供了一种非阻塞式的获取应用健康状况信息的协议。类似于传统的 `HealthContributor`，健康状况信息收集自 [`ReactiveHealthContributorRegistry`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/ReactiveHealthContributorRegistry.java) (默认是你的 `ApplicationContext` 中定义的所有 [`HealthContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/HealthContributor.java) 和 [`ReactiveHealthContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/ReactiveHealthContributor.java) 实例) 的内容。不检查反应式 API 的常规`HealthContributors`在弹性调度程序上执行。

> 在反应式应用程序中，应使用 `ReactiveHealthContributorRegistry` 在运行时注册和注销健康指标。如果需要注册常规的 `HealthContributor`，则应使用`ReactiveHealthContributor#adapt`对其进行包装。

为了从反应式 API 提供自定义健康信息，你可以注册实现 [`ReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/health/ReactiveHealthIndicator.java) 接口的 Spring beans。下面的代码展示了一个简单的 `ReactiveHealthIndicator` 实现：

```java
@Component
public class MyReactiveHealthIndicator implements ReactiveHealthIndicator {

    @Override
    public Mono<Health> health() {
        return doHealthCheck() //perform some specific health check that returns a Mono<Health>
            .onErrorResume(ex -> Mono.just(new Health.Builder().down(ex).build()));
    }

}
```

> 为了自动处理错误，考虑从 `AbstractReactiveHealthIndicator` 扩展。

##### 自动配置反应式健康指标

下面的 `ReactiveHealthIndicators` 在适当的时候会由 Spring Boot 自动配置：

| Name                                                         | Description                     |
| :----------------------------------------------------------- | :------------------------------ |
| [`CassandraReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/cassandra/CassandraReactiveHealthIndicator.java) | 检查 Cassandra 数据库已经启动。 |
| [`CouchbaseReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/couchbase/CouchbaseReactiveHealthIndicator.java) | 检查 Couchbase 集群已经启动。   |
| [`MongoReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/mongo/MongoReactiveHealthIndicator.java) | 检查 Mongo 数据库已经启动。     |
| [`RedisReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/redis/RedisReactiveHealthIndicator.java) | 检查 Redis 服务器已经启动。     |

> 如果必要，反应式指标会替换普通的指标。同时所有未被显式处理的指标都会被自动包装。

##### 健康组

有时候将健康指标组织成组可能会有用，这样便于用于不同目的。比如，如果你将应用部署到 Kubernetes，您可能需要一套不同的健康指标来进行“活力”和“就绪”检查。

要创建一个健康指标组，您可以使用 `management.endpoint.health.group.<name>` 属性，并指定一个健康指标 ID 列表以 `include` 或 `exclude`。例如，要创建仅包含数据库指示符的组，可以定义以下内容：

```properties
management.endpoint.health.group.custom.include=db
```

然后，您可以点击 `localhost:8080/actuator/health/custom` 来检查结果。

默认情况下，组将继承与系统运行状况相同的 `StatusAggregator` 和 `HttpCodeStatusMapper` 设置，但是，也可以在每个组的基础上进行定义。如果需要，也可以覆盖 `show-details` 和 `roles` 属性：

```properties
management.endpoint.health.group.custom.show-details=when-authorized
management.endpoint.health.group.custom.roles=admin
management.endpoint.health.group.custom.status.order=fatal,up
management.endpoint.health.group.custom.status.http-mapping.fatal=500
```

> 你可以使用 `@Qualifier("groupname")` 如果你需要注册自定义 `StatusAggregator` 或者 `HttpCodeStatusMapper` beans 以和该组一起使用。

#### 5.2.9. 应用信息

应用信息暴露收集自所有定义在你的 `ApplicationContext` 中的 [`InfoContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/InfoContributor.java) beans 的各种信息。Spring Boot 包含大量自动配置的 `InfoContributor` beans，你也可以编写自己的。

##### 自动配置的信息贡献者

下面的 `InfoContributor` beans 在合适的时候由 Spring Boot 自动配置：

| Name                                                         | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [`EnvironmentInfoContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/EnvironmentInfoContributor.java) | 暴露所有来自 `Environment` 的位于 `info` 键下的键。          |
| [`GitInfoContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/GitInfoContributor.java) | 暴露 git 信息，如果 `git.properties` 文件可用。              |
| [`BuildInfoContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/BuildInfoContributor.java) | Exposes build information if a `META-INF/build-info.properties` file is available. |

> 可以通过设定 `management.info.defaults.enabled` 属性将它们全部关闭。

##### 自定义应用信息

你可以通过设定 `info.*` Spring 属性自定义通过 `info` 端点暴露的数据。位于 `info` 键之下的所有 `Environment` 属性会自动暴露。比如，你可以添加下面的设定到你的 `application.properties` 文件中：

```properties
info.app.encoding=UTF-8
info.app.java.source=1.8
info.app.java.target=1.8
```

> 除了硬编码这些值，你还可以 [在构建时扩展 info 属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-automatic-expansion).
>
>  假定你使用了 Maven，你还可以像下面这样重写上面的例子：
>
> ```properties
> info.app.encoding=@project.build.sourceEncoding@
> info.app.java.source=@java.version@
> info.app.java.target=@java.version@
> ```

##### Git 提交信息

`info` 端点的另一个有用的功能是它能够在构建项目时发布有关 `git` 源代码存储库状态的信息。如果有一个 `GitProperties` bean，则将暴露 `git.branch`，`git.commit.id` 和 `git.commit.time` 属性。

> 如果 `git.properties` 文件存在于类路径根目录下则 `GitProperties` bean 会被自动配置。参考 "[生成 git 信息](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-git-info)" 了解更多细节。

如果你想要显示完整的 git 信息（也就是 `git.properties` 的完整内容），使用 `management.info.git.mode` 属性，如下所示：

```properties
management.info.git.mode=full
```

##### 构建信息

如果 `BuildProperties` bean 可用， `info` 端点还能够有关构建的信息。如果 `META-INF/build-info.properties` 文件存在于类路径下时就会如此。

> Maven 和 Gradle 插件都会生成该文件。参考 "[生成构建信息](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-build-info)" 了解更多细节。

##### 编写自定义 InfoContributors

为了提供自定义应用信息，你可以注册实现了 [`InfoContributor`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/info/InfoContributor.java) 接口的 Spring beans。

下面的例子提供携带单个值的 `example` 条目：

```java
import java.util.Collections;

import org.springframework.boot.actuate.info.Info;
import org.springframework.boot.actuate.info.InfoContributor;
import org.springframework.stereotype.Component;

@Component
public class ExampleInfoContributor implements InfoContributor {

    @Override
    public void contribute(Info.Builder builder) {
        builder.withDetail("example",
                Collections.singletonMap("key", "value"));
    }

}
```

访问 `info` 端点，你应该可以看到包含下列额外数据条目的响应：

```json
{
    "example": {
        "key" : "value"
    }
}
```

### 5.3.  通过 HTTP 进行监控和管理

如果您正在开发 Web 应用程序，则 Spring Boot Actuator 会自动配置所有启用的端点以通过 HTTP 公开。默认约定是使用端点的 `id` 和前缀 `/actuator` 作为 URL 路径。例如，`health` 被公开为 `/actuator/health`。

> Spring MVC，Spring WebFlux 和 Jersey 本身支持 Actuator。如果 Jersey 和 Spring MVC 均可用，则将使用 Spring MVC。

#### 5.3.1. 自定义管理端点路径

有时，自定义管理端点的前缀很有用。例如，您的应用程序可能已经将 `/actuator` 用于其他用途。您可以使用 `management.endpoints.web.base-path` 属性来更改管理端点的前缀，如以下示例所示：

```properties
management.endpoints.web.base-path=/manage
```

前面的 `application.properties` 示例将端点由 `/actuator/{id}` 修改为 `/manage/{id}` (比如，`/manage/info`)。

> 除非管理端口已配置为 [通过使用其他 HTTP 端口公开端点](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-customizing-management-server-port)。`management.endpoints.web.base-path` 相对于 `server.servlet.context-path`。如果配置了 `management.server.port`，则 `management.endpoints.web.base-path` 相对于 `management.server.servlet.context-path`。

如果要将端点映射到其他路径，则可以使用 `management.endpoints.web.path-mapping` 属性。

以下示例将 `/actuator/health` 重新映射为 `/healthcheck`：

application.properties

```properties
management.endpoints.web.base-path=/
management.endpoints.web.path-mapping.health=healthcheck
```

#### 5.3.2. 自定义管理服务器端口

对于基于云的部署，通过使用默认的 HTTP 端口公开管理端点是明智的选择。但是，如果您的应用程序在自己的数据中心内运行，则您可能更喜欢使用其他 HTTP 端口公开端点。

您可以设置 `management.server.port` 属性来更改 HTTP 端口，如以下示例所示：

```properties
management.server.port=8081
```

> 在 Cloud Foundry 上，默认情况下，应用程序仅在端口 8080 上接收 HTTP 和 TCP 路由请求。如果要在 Cloud Foundry 上使用自定义管理端口，则需要明确设置应用程序的路由，以将流量转发到该自定义端口。

#### 5.3.3. 配置管理专用的 SSL

当配置为使用自定义端口时，还可以通过使用各种 `management.server.ssl.*` 属性为管理服务器配置其自己的 SSL。例如，这样做可以使管理服务器在主应用程序使用 HTTPS 时通过 HTTP 可用，如以下属性设置所示：

```properties
server.port=8443
server.ssl.enabled=true
server.ssl.key-store=classpath:store.jks
server.ssl.key-password=secret
management.server.port=8080
management.server.ssl.enabled=false
```

或者，主服务器和管理服务器都可以使用 SSL，但具有不同的密钥库，如下所示：

```properties
server.port=8443
server.ssl.enabled=true
server.ssl.key-store=classpath:main.jks
server.ssl.key-password=secret
management.server.port=8080
management.server.ssl.enabled=true
management.server.ssl.key-store=classpath:management.jks
management.server.ssl.key-password=secret
```

#### 5.3.4.  自定义管理服务器地址

您可以通过设置 `management.server.address` 属性来定制管理端点可用的地址。如果您只想在内部或面向操作的网络上侦听或仅侦听来自 `localhost` 的连接，则这样做很有用。

> 仅当端口与主服务器端口不同时，您才能在其他地址上侦听。

下面的例子 `application.properties` 不允许远程管理连接：

```properties
management.server.port=8081
management.server.address=127.0.0.1
```

#### 5.3.5. 禁用 HTTP 端点

如果你不希望通过 HTTP 暴露端点，你可以设定管理端口为 `-1`，如下面例子所示：

```properties
management.server.port=-1
```

也可以使用 `management.endpoints.web.exposure.exclude` 属性来实现，如以下示例所示：

```properties
management.endpoints.web.exposure.exclude=*
```

### 5.4. 通过 JMX 监控和管理

Java 管理扩展（JMX）提供了监视和管理应用程序的标准机制。默认情况下，此功能未启用，可以通过将配置属性 `spring.jmx.enabled` 设置为 `true` 来启用。默认情况下，Spring Boot 将管理端点作为 `org.springframework.boot` 域下的 JMX MBean 公开。

#### 5.4.1. 自定义 MBean 名称

MBean 的名称通常由端点的 `id` 生成。例如， `health` 端点公开为 `org.springframework.boot:type=Endpoint,name=Health`。

如果您的应用程序包含多个 Spring `ApplicationContext`，您可能会发现名称冲突。为了解决这个问题，可以将 `spring.jmx.unique-names` 属性设置为 `true`，以便 MBean 名称始终是唯一的。

您还可以自定义暴露端点的 JMX 域。以下设置显示了在 `application.properties` 中执行此操作的示例：

```properties
spring.jmx.unique-names=true
management.endpoints.jmx.domain=com.example.myapp
```

#### 5.4.2. 禁用 JMX 端点

如果你不想通过 JMX 暴露端点，你可以设置 `management.endpoints.jmx.exposure.exclude` 属性为 `*`，如下面例子所示：

```properties
management.endpoints.jmx.exposure.exclude=*
```

#### 5.4.3. 在 HTTP 上为 JMX 使用 Jolokia

Jolokia 是一种 JMX-HTTP 桥接技术，提供了另一种访问 JMX beans 的方法。为了使用 Jolokia，引入 `org.jolokia:jolokia-core` 依赖。比如，使用 Maven，你需要添加下面的依赖：

```xml
<dependency>
    <groupId>org.jolokia</groupId>
    <artifactId>jolokia-core</artifactId>
</dependency>
```

然后 Jolokia 端点就可以通过添加 `jolokia` 或者 `*` 到 `management.endpoints.web.exposure.include` 属性而暴露。这样你就可以通过使用 `/actuator/jolokia` 在你的管理 HTTP 服务器上访问它们。

##### 自定义 Jolokia

Jolokia 包含一些设定，你可以通过设定 servlet 参数来配置它们。在 Spring Boot 中，你可以使用 `application.properties` 文件。为了做到这一点，为参数名称添加前缀 `management.endpoint.jolokia.config.`，如下面例子所示：

```properties
management.endpoint.jolokia.config.debug=true
```

##### 禁用 Jolokia

如果你使用 Jolokia 但不希望 Spring Boot 配置它，设定 `management.endpoint.jolokia.enabled` 属性为 `false`，如下所示：

```properties
management.endpoint.jolokia.enabled=false
```

### 5.5. Loggers

Spring Boot Actuator 包含在运行时查看和配置应用的日志级别的能力。你可以查看整体配置列表或者单个 logger 配置。该配置由显式配置的日志级别以及日志框架赋予的有效的日志级别组成。日志级别可以是：

- `TRACE`

- `DEBUG`

- `INFO`

- `WARN`

- `ERROR`

- `FATAL`

- `OFF`

- `null`

`null` 表示没有显式配置。

#### 5.5.1. 配置 Logger

为了配置给定的 logger，`POST` 一个部分实体到该资源 URI，如下面例子所示：

```json
{
    "configuredLevel": "DEBUG"
}
```

>要“重置”记录器的特定级别（并使用默认配置），可以将传入 `null` 作为 `configuredLevel` 值。

### 5.6. Metrics

Spring Boot Actuator 为 [Micrometer](https://micrometer.io/) 提供了依赖管理和自动配资，一个应用度量门面，支持各种监控系统，包括：

- [AppOptics](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-appoptics)

- [Atlas](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-atlas)

- [Datadog](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-datadog)

- [Dynatrace](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-dynatrace)

- [Elastic](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-elastic)

- [Ganglia](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-ganglia)

- [Graphite](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-graphite)

- [Humio](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-humio)

- [Influx](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-influx)

- [JMX](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-jmx)

- [KairosDB](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-kairos)

- [New Relic](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-newrelic)

- [Prometheus](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-prometheus)

- [SignalFx](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-signalfx)

- [Simple (in-memory)](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-simple)

- [StatsD](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-statsd)

- [Wavefront](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-wavefront)

>为了进一步了解 Micrometer’s 能力，请参考相应的 [参考文档](https://micrometer.io/docs)，特别是 [概念章节](https://micrometer.io/docs/concepts).

#### 5.6.1. 起步

Spring Boot 自动配置一个复合 `MeterRegistry`，并为它在类路径中找到的每个受支持的实现向复合添加一个注册表。在运行时类路径中具有对 `micrometer-registry-{system}` 的依赖就足以让 Spring Boot 配置注册表。

大多数注册表具有共同的特征。例如，即使 Micrometer 注册表实现位于类路径中，您也可以禁用特定的注册表。例如，禁用 Datadog：

```properties
management.metrics.export.datadog.enabled=false
```

Spring Boot 还会将任何自动配置的注册表添加到 `Metrics` 类的全局静态复合注册表中，除非您明确告知不要这么做：

```properties
management.metrics.use-global-registry=false
```

您可以注册任意数量的 `MeterRegistryCustomizer` bean 来进一步配置注册表，例如在将任何计量表注册到注册表之前应用通用标签：

```java
@Bean
MeterRegistryCustomizer<MeterRegistry> metricsCommonTags() {
    return registry -> registry.config().commonTags("region", "us-east-1");
}
```

您可以通过更详细地了解通用类型，将自定义项应用于特定的注册表实现：

```java
@Bean
MeterRegistryCustomizer<GraphiteMeterRegistry> graphiteMetricsNamingConvention() {
    return registry -> registry.config().namingConvention(MY_CUSTOM_CONVENTION);
}
```

有了该设置后，您可以在组件中注入 `MeterRegistry` 并注册指标：

```java
@Component
public class SampleBean {

    private final Counter counter;

    public SampleBean(MeterRegistry registry) {
        this.counter = registry.counter("received.messages");
    }

    public void handleMessage(String message) {
        this.counter.increment();
        // handle message implementation
    }

}
```

Spring Boot 还可以[配置内置工具](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-meter)（即 `MeterBinder` 实现) 您可以通过配置或专用注释标记来控制这些实现。

#### 5.6.2. 支持的监控系统

##### AppOptics

默认情况下，AppOptics 注册会将度量值周期性推送到 `api.appoptics.com/v1/measurements` 。为了将度量值导出给 SaaS [AppOptics](https://micrometer.io/docs/registry/appoptics) ，你必须提供 API token：

```properties
management.metrics.export.appoptics.api-token=YOUR_TOKEN
```

##### Atlas

默认情况下，度量值被暴露给运行在你本地的 [Atlas](https://micrometer.io/docs/registry/atlas) 。要使用的 [Atlas server](https://github.com/Netflix/atlas) 的位置可以通过下面方式提供：

```properties
management.metrics.export.atlas.uri=https://atlas.example.com:7101/api/v1/publish
```

##### Datadog

Datadog 注册将度量值周期性推送至 [datadoghq](https://www.datadoghq.com/) 。为了导出度量值到 [Datadog](https://micrometer.io/docs/registry/datadog)，必需提供你的 API key：

```properties
management.metrics.export.datadog.api-key=YOUR_KEY
```

你也可以修改度量值向 Datadog 推送的时间间隔：

```properties
management.metrics.export.datadog.step=30s
```

##### Dynatrace

Dynatrace 注册周期性地将度量值推动到配置的 URI 。为了导出度量值到 [Dynatrace](https://micrometer.io/docs/registry/dynatrace) ，必需提供 API token，设备 ID，以及 URI ：

```properties
management.metrics.export.dynatrace.api-token=YOUR_TOKEN
management.metrics.export.dynatrace.device-id=YOUR_DEVICE_ID
management.metrics.export.dynatrace.uri=YOUR_URI
```

你也可以修改向 Dynatrace 推送度量值的时间间隔：

```properties
management.metrics.export.dynatrace.step=30s
```

##### Elastic

默认情况下，度量值被导出至你本地机器上运行的 [Elastic](https://micrometer.io/docs/registry/elastic) 。要使用的 Elastic server 的地址可以通过以下方式指定：

```properties
management.metrics.export.elastic.host=https://elastic.example.com:8086
```

##### Ganglia

默认情况下，度量值被导出至你本地机器上运行的 [Ganglia](https://micrometer.io/docs/registry/ganglia) 。要使用的 [Ganglia server](http://ganglia.sourceforge.net/) 的地址和端口可以通过以下方式指定：

```properties
management.metrics.export.ganglia.host=ganglia.example.com
management.metrics.export.ganglia.port=9649
```

##### Graphite

默认情况下，度量值被导出至你本地机器上运行的 [Graphite](https://micrometer.io/docs/registry/graphite) 。要使用的 [Graphite server](https://graphiteapp.org/) 的地址和端口可以通过以下方式指定：

```properties
management.metrics.export.graphite.host=graphite.example.com
management.metrics.export.graphite.port=9004
```

Micrometer 提供了默认的 `HierarchicalNameMapper` 用来管理如何将空间尺度 id [映射到平面层级名称](https://micrometer.io/docs/registry/graphite#_hierarchical_name_mapping)。

>为了控制该映射行为，定义你自己的 `GraphiteMeterRegistry` 并提供相应的 `HierarchicalNameMapper`。一个自动配置的 `GraphiteConfig` 和 `Clock` beans 也会被提供，除非你定义自己的：

```java
@Bean
public GraphiteMeterRegistry graphiteMeterRegistry(GraphiteConfig config, Clock clock) {
    return new GraphiteMeterRegistry(config, clock, MY_HIERARCHICAL_MAPPER);
}
```

##### Humio

默认情况下，Humio 注册会将度量值周期性推送到 [cloud.humio.com](https://cloud.humio.com/) 。为了将度量值导出给 SaaS [Humio](https://micrometer.io/docs/registry/humio)，你必须提供 API token：

```properties
management.metrics.export.humio.api-token=YOUR_TOKEN
```

你还应该配置一个或者多个标签来标示将被推送的度量值的数据源：

```properties
management.metrics.export.humio.tags.alpha=a
management.metrics.export.humio.tags.bravo=b
```

##### Influx

默认情况下，度量值被导出至你本地机器上运行的 [Influx](https://micrometer.io/docs/registry/influx) 。要使用的 [Influx server](https://www.influxdata.com/) 的地址可以通过以下方式指定：

```properties
management.metrics.export.influx.uri=https://influx.example.com:8086
```

##### JMX

Micrometer 提供了到 [JMX](https://micrometer.io/docs/registry/jmx) 的层次结构映射，主要是作为一种便宜且可移植的方式在本地查看度量。默认情况下，指标被导出到 `metrics` JMX 域。可以使用以下方式提供要使用的域：

```properties
management.metrics.export.jmx.domain=com.example.app.metrics
```

Micrometer 提供了一个默认的 `HierarchicalNameMapper` 负责管理将空间尺度 id [映射到平面层级名称](https://micrometer.io/docs/registry/jmx#_hierarchical_name_mapping)。

>为了控制这种映射行为，定义你自己的 `JmxMeterRegistry` 并提供相应的 `HierarchicalNameMapper`，一个自动配置的 `JmxConfig` 和 `Clock` beans 会被自动提供，除非你自己定义它们：

```java
@Bean
public JmxMeterRegistry jmxMeterRegistry(JmxConfig config, Clock clock) {
    return new JmxMeterRegistry(config, clock, MY_HIERARCHICAL_MAPPER);
}
```

##### KairosDB

默认情况下，度量值被导出至你本地机器上运行的 [KairosDB](https://micrometer.io/docs/registry/kairos) 。要使用的 [KairosDB server](https://kairosdb.github.io/) 的地址可以通过以下方式指定：

```properties
management.metrics.export.kairos.uri=https://kairosdb.example.com:8080/api/v1/datapoints
```

##### New Relic

New Relic 注册将度量值周期性推送至 [New Relic](https://micrometer.io/docs/registry/new-relic) 。为了导出度量值到 [New Relic](https://micrometer.io/docs/registry/new-relic) ，必需提供你的 API key 和账户 id ：

```properties
management.metrics.export.newrelic.api-key=YOUR_KEY
management.metrics.export.newrelic.account-id=YOUR_ACCOUNT_ID
```

你也可以修改度量值推送到 New Relic 的时间间隔：

```properties
management.metrics.export.newrelic.step=30s
```

##### Prometheus

[Prometheus](https://micrometer.io/docs/registry/prometheus) 希望抓取或轮询单个应用程序实例以获取指标。Spring Boot 在 `/actuator/prometheus` 提供了一个执行器端点，以适当格式显示 [Prometheus scrape](https://prometheus.io/)。

>该端点默认不可用，需要手动暴露。更多相关细节请参考 [exposing endpoints](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-endpoints-exposing-endpoints) 。

这里是需要添加到 `prometheus.yml` 中的 `scrape_config` 的例子：

```yaml
scrape_configs:
  - job_name: 'spring'
    metrics_path: '/actuator/prometheus'
    static_configs:
      - targets: ['HOST:PORT']
```

对于可能不存在足够长的时间而无法被废弃的临时或批处理作业，可以使用 [Prometheus Pushgateway](https://github.com/prometheus/pushgateway) 支持将其指标暴露给 Prometheus。要启用 Prometheus Pushgateway 支持，请将以下依赖项添加到您的项目中：

```xml
<dependency>
    <groupId>io.prometheus</groupId>
    <artifactId>simpleclient_pushgateway</artifactId>
</dependency>
```

当在类路径上存在 Prometheus Pushgateway 依赖项时，Spring Boot 会自动配置一个 `PrometheusPushGatewayManager` bean。这可以管理将指标推送到 Prometheus Pushgateway。可以使用 `management.metrics.export.prometheus.pushgateway` 下的属性来调整 `PrometheusPushGatewayManager`。 对于高级配置，您还可以提供自己的 `PrometheusPushGatewayManager` bean。

##### SignalFx

SignalFx 注册将度量值周期性推送至 [SignalFx](https://micrometer.io/docs/registry/signalfx) 。为了导出度量值到 [SignalFx](https://micrometer.io/docs/registry/signalfx) ，必需提供你的访问 token：

```properties
management.metrics.export.signalfx.access-token=YOUR_ACCESS_TOKEN
```

你也可以修改度量值推送到 SignalFx 的时间间隔：

```properties
management.metrics.export.signalfx.step=30s
```

##### Simple

Micrometer 附带一个简单的内存后端，如果未配置其他注册表，该后端将自动用作后备。这使您可以查看在 [metrics endpoint](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-endpoint) 中收集了哪些指标。

使用任何其他可用后端时，内存中后端都会自行禁用。您也可以显式禁用它：

```properties
management.metrics.export.simple.enabled=false
```

##### StatsD

StatsD 注册急切地通过 UDP 将度量推送到 StatsD 代理。默认情况下，指标会导出到本地计算机上运行的 [StatsD](https://micrometer.io/docs/registry/statsd) 代理中。可以使用以下方式提供要使用的 StatsD 代理主机和端口：

```properties
management.metrics.export.statsd.host=statsd.example.com
management.metrics.export.statsd.port=9125
```

您还可以更改要使用的 StatsD 线路协议（默认为 Datadog）：

```properties
management.metrics.export.statsd.flavor=etsy
```

##### Wavefront

Wavefront 注册将度量值周期性推送至 [Wavefront](https://micrometer.io/docs/registry/wavefront) 。为了直接导出度量值到 [Wavefront](https://micrometer.io/docs/registry/wavefront) ，必需提供你的 API token：

```properties
management.metrics.export.wavefront.api-token=YOUR_API_TOKEN
```

或者，您可以使用在您的环境中设置的 Wavefront 辅助工具或内部代理，将指标数据转发到 Wavefront API 主机：

```properties
management.metrics.export.wavefront.uri=proxy://localhost:2878
```

>如果将指标发布到Wavefront代理（如 [文档](https://docs.wavefront.com/proxies_installing.html) 中所述），则主机必须为 `proxy://HOST:PORT` 格式。

你也可以修改度量值推送到 Wavefront 的时间间隔：

```properties
management.metrics.export.wavefront.step=30s
```

#### 5.6.3. 支持的 Metrics

在适用情况下，Spring Boot 将注册以下核心度量指标：

- JVM metrics，报告下列利用率：

- 各种内存和缓存池

- 有关垃圾收集的统计数据

- 线程利用率

- 加载/卸载的类的数量

- CPU metrics

- 文件描述符 metrics

- Kafka consumer metrics

- Log4j2 metrics: 记录每个级别记录到 Log4j2 的事件数

- Logback metrics: 记录每个级别记录到 Logback 的事件数

- Uptime metrics: 报告正常运行时间的量度和代表应用程序绝对启动时间的固定量度

- Tomcat metrics (`server.tomcat.mbeanregistry.enabled` 必需设定为 `true` 对所有将被注册的 Tomcat metrics)

- [Spring Integration](https://docs.spring.io/spring-integration/docs/5.2.2.RELEASE/reference/html/system-management.html#micrometer-integration) metrics

##### Spring MVC Metrics

通过自动配置，可以检测由 Spring MVC 处理的请求。当 `management.metrics.web.server.request.autotime.enabled` 为 `true` 时，将对所有请求进行检测。 另外，当设置为 `false` 时，可以通过在请求处理方法中添加 `@Timed` 来启用检测：

```java
@RestController
@Timed // 控制器类，用于对控制器中的每个请求处理程序启用计时。
public class MyController {

    @GetMapping("/api/people")
    @Timed(extraTags = { "region", "us-east-1" }) // 一种启用单个端点的方法。如果您将它放在类中，则不必这样做，但是可以用于进一步为此特定端点自定义计时器。
    @Timed(value = "all.people", longTask = true) // longTask = true 的方法为该方法启用长任务计时器。长任务计时器需要单独的度量标准名称，并且可以与短任务计时器堆叠在一起。
    public List<Person> listPeople() { ... }

}
```

默认情况下，使用名称 `http.server.requests` 生成度量。可以通过设置 `management.metrics.web.server.request.metric-name` 属性来自定义名称。

默认情况下，与 Spring MVC 相关的指标带有以下信息标记：

| Tag         | Description                                                  |
| :---------- | :----------------------------------------------------------- |
| `exception` | 处理请求时引发的任何异常的简单类名。                         |
| `method`    | 请求方法 (比如， `GET` 或者 `POST`)                          |
| `outcome`   | 根据响应的状态码请求的结果。1xx 是 `INFORMATIONAL`，2xx 是 `SUCCESS`，3xx 是 `REDIRECTION`，4xx 是 `CLIENT_ERROR`，5xx 是 `SERVER_ERROR` |
| `status`    | 响应的 HTTP 状态码 (比如， `200` 或者 `500`)                 |
| `uri`       | 应用变量之前的请求的 URI 模板，如果可能 (比如， `/api/person/{id}`) |

为了自定义这些标签，提供一个实现了 `WebMvcTagsProvider` 接口的 `@Bean` 类。

##### Spring WebFlux Metrics

自动配置为所有由 WebFlux 控制器和功能处理的请求启用指标基础设施。

默认情况下，度量指标使用名称 `http.server.requests` 生成。你可以通过设定 `management.metrics.web.server.request.metric-name` 属性来自定义名称。

默认地，WebFlux 相关的指标会被以下信息标记：

| Tag         | Description                                                  |
| :---------- | :----------------------------------------------------------- |
| `exception` | 处理请求时抛出的任何异常的简单类名。                         |
| `method`    | 请求方法 (比如，`GET` 或者 `POST`)                           |
| `outcome`   | 基于响应状态码的请求输出。 1xx 是 `INFORMATIONAL`， 2xx 是 `SUCCESS`， 3xx 是 `REDIRECTION`， 4xx 是 `CLIENT_ERROR`， 5xx 是 `SERVER_ERROR` |
| `status`    | 响应的 HTTP 状态码 (比如， `200` 或者 `500`)                 |
| `uri`       | 应用变量值之前的请求的 URI 模板，如果可能的话 (比如， `/api/person/{id}`) |

为了自定义标签，提供一个实现了 `WebFluxTagsProvider` 接口的 `@Bean` 类。

##### Jersey Server Metrics

当 Micrometer 的`micrometer-jersey2`模块位于类路径上时，自动配置将启用对 Jersey JAX-RS 实现所处理的请求的检测。当 `management.metrics.web.server.request.autotime.enabled` 为 `true` 时，将对所有请求进行检测。另外，当设置为 `false` 时，可以通过在请求处理方法中添加 `@Timed` 来启用检测：

```java
@Component
@Path("/api/people")
@Timed //在资源类上，以对资源中的每个请求处理程序启用计时。
public class Endpoint {
    @GET
    @Timed(extraTags = { "region", "us-east-1" }) //关于启用单个端点的方法。如果您将它放在类中，则不必这样做，但是可以用于进一步为此特定端点自定义计时器。
    @Timed(value = "all.people", longTask = true) //在 longTask = true 的方法上为该方法启用长任务计时器。长任务计时器需要单独的度量标准名称，并且可以与短任务计时器堆叠在一起。
    public List<Person> listPeople() { ... }
}
```

默认情况下，使用名称 `http.server.requests` 生成度量。可以通过设置 `management.metrics.web.server.request.metric-name` 属性来自定义名称。

默认情况下，Jersey 服务器指标带有以下信息：

| Tag         | Description                                                  |
| :---------- | :----------------------------------------------------------- |
| `exception` | 处理请求时引发的任何异常的简单类名。                         |
| `method`    | 请求方法 (比如， `GET` 或者 `POST`)                          |
| `outcome`   | 基于响应状态码的亲求输出。 1xx 是 `INFORMATIONAL`, 2xx 是 `SUCCESS`, 3xx 是 `REDIRECTION`, 4xx `CLIENT_ERROR`, 而 5xx 是 `SERVER_ERROR` |
| `status`    | 响应的 HTTP 状态码 (比如， `200` 或者 `500`)                 |
| `uri`       | 应用变量替换之前的请求 URI 模板，如果可能 (比如， `/api/person/{id}`) |

要自定义标签，提供一个实现了 `JerseyTagsProvider` 的 `@Bean` 。

##### HTTP Client Metrics

Spring Boot Actuator 可以管理 `RestTemplate` 和 `WebClient ` 的检测基础设施。为此，你必须注入相应的构建器并使用它创建实例：

- `RestTemplateBuilder` 用于 `RestTemplate`
- `WebClient.Builder` 用于 `WebClient`

也可以手动应用负责此工具的定制程序，即 `MetricsRestTemplateCustomizer` 和 `MetricsWebClientCustomizer`。

默认情况下，使用名称 `http.client.requests` 生成度量。可以通过设置 `management.metrics.web.client.request.metric-name` 属性来自定义名称。

默认情况下，通过检测的客户端生成的度量标准标记有以下信息：

| Tag          | Description                                                  |
| :----------- | :----------------------------------------------------------- |
| `clientName` | URI 的 Host 部分                                             |
| `method`     | 请求方法 (比如， `GET` 或者 `POST`)                          |
| `outcome`    | 基于响应状态码的请求输出。 1xx 是 `INFORMATIONAL`, 2xx 是 `SUCCESS`, 3xx 是 `REDIRECTION`, 4xx `CLIENT_ERROR`, 而 5xx 是 `SERVER_ERROR`, 否则是 `UNKNOWN` 。 |
| `status`     | 响应的 HTTP 状态码，如果可用 (比如， `200` 或者 `500`)，或者 `IO_ERROR` 如果出现 I/O 问题， 否则是 `CLIENT_ERROR` 。 |
| `uri`        | 应用变量之前的请求 URI 模板，如果可能 (比如， `/api/person/{id}`) |

要根据您选择的客户端自定义标签，可以提供实现 `@RestTemplateExchangeTagsProvider` 或 `WebClientExchangeTagsProvider` 的 `@Bean`。`RestTemplateExchangeTags` 和 `WebClientExchangeTags` 中有便捷的静态函数。

##### Cache Metrics

自动配置可在启动时使用前缀为 `cache` 的指标来检测所有可用的 `Cache`。高速缓存检测针对一组基本指标进行了标准化。还提供其他特定于缓存的指标。

支持下列缓存类库：

- Caffeine
- EhCache 2
- Hazelcast
- 任何兼容 JCache (JSR-107) 实现

Metrics 会被打上标签，该标签来自缓存的名称以及由 bean 名称派生而来的 `CacheManager` 的名称。

> 仅在启动时配置的缓存绑定到注册表。对于未在缓存配置中定义的缓存，例如，在启动阶段即时或以编程方式创建的高速缓存时，需要显式注册。可以使用`CacheMetricsRegistrar` bean 来简化该过程。

##### DataSource Metrics

通过自动配置，可以使用前缀为 `jdbc.connections` 的度量来检测所有可用的 `DataSource` 对象。数据源检测产生的量规表示池中当前活动，空闲，最大允许和最小允许的连接。

度量标准还标有根据 bean 名称计算的 `DataSource` 名称。

> 默认情况下，Spring Boot 为所有支持的数据源提供元数据。如果不支持立即使用您喜欢的数据源，则可以添加其他`DataSourcePoolMetadataProvider` bean。有关示例，请参见 `DataSourcePoolMetadataProvidersConfiguration`。

同样，使用 `hikaricp` 前缀公开特定于 Hikari 的指标。每个度量标准都以池的名称标记（可以通过 `spring.datasource.name` 进行控制）。

##### Hibernate Metrics

通过自动配置，可以检测所有可用的名为 `hibernate` 的统计启用的 Hibernate `EntityManagerFactory` 实例。

度量标准还通过从 Bean 名称派生的 `EntityManagerFactory` 的名称进行标记。

要启用统计信息，必须将标准 JPA 属性 `hibernate.generate_statistics` 设置为 `true`。您可以在自动配置的 `EntityManagerFactory` 上启用该功能，如以下示例所示：

```properties
spring.jpa.properties.hibernate.generate_statistics=true
```

##### RabbitMQ Metrics

自动配置将启用所有名为 `rabbitmq` 的度量标准的 RabbitMQ 连接工厂的检测。

#### 5.6.4. 自定义度量注册

为了注册自定义度量，将 `MeterRegistry` 注入你的组件中，如下面例子所示：

```java
class Dictionary {

    private final List<String> words = new CopyOnWriteArrayList<>();

    Dictionary(MeterRegistry registry) {
        registry.gaugeCollectionSize("dictionary.size", Tags.empty(), this.words);
    }

    // …

}
```

如果你发现在组件或者应用中重复构建一套度量组件，就可以将整套组件封装成为 `MeterBinder` 实现。默认地，来自所有 `MeterBinder` beans 的度量都会自动绑定到 Spring 管理的 `MeterRegistry`。

#### 5.6.5. 自定义单个度量

如果您需要对特定的 `Meter` 实例应用自定义设置，则可以使用 `io.micrometer.core.instrument.config.MeterFilter` 接口。默认情况下，所有的 `MeterFilter` bean 都将自动应用于 micrometer  `MeterRegistry.Config`。

例如，如果要将所有 ID 以 `com.example` 开头的计量表的标签 `mytag.region` 重命名为 `mytag.area`，则可以执行以下操作：

```java
@Bean
public MeterFilter renameRegionTagMeterFilter() {
    return MeterFilter.renameTag("com.example", "mytag.region", "mytag.area");
}
```

##### 通用标签

通用标签通常用于在操作环境（如主机，实例，区域，堆栈等）上进行维度深入分析。通用标签适用于所有仪表，可以按以下示例所示进行配置：

```properties
management.metrics.tags.region=us-east-1
management.metrics.tags.stack=prod
```

上面的示例在所有仪表中分别添加了 `region` 和 `stack` 标签，其值分别为 `us-east-1` 和 `prod`。

> 如果使用 Graphite，则常用标签的顺序很重要。由于使用这种方法不能保证通用标签的顺序，因此建议 Graphite 用户定义一个自定义的 `MeterFilter`。

##### Per-meter 属性

除了 `MeterFilter` bean 外，还可以使用属性在 per-meter 基础上应用一组有限的自定义设置。Per-meter 定制适用于以给定名称开头的所有所有表 ID。例如，以下将禁用任何 ID 以 `example.remote` 开头的仪表：

```properties
management.metrics.enable.example.remote=false
```

下面的属性允许 per-meter 自定义：

| Property                                                     | Description                                              |
| :----------------------------------------------------------- | :------------------------------------------------------- |
| `management.metrics.enable`                                  | 是否拒绝仪表发出任何指标。                               |
| `management.metrics.distribution.percentiles-histogram`      | 是否发布适用于计算可聚集（跨维度）百分位数逼近的直方图。 |
| `management.metrics.distribution.minimum-expected-value`, `management.metrics.distribution.maximum-expected-value` | 通过限制期望值的范围，发布较少的直方图桶。               |
| `management.metrics.distribution.percentiles`                | 发布在应用程序中计算的百分位值。                         |
| `management.metrics.distribution.sla`                        | 发布包含您的 SLA 定义的存储桶的累积直方图。              |

有关 `percentiles-histogram`，`percentiles` 和 `sla` 背后的概念的更多详细信息，请参见 micrometer 文档的 [“直方图和百分位数”部分](https://micrometer.io/docs/concepts#_histograms_and_percentiles) 。

#### 5.6.6. Metrics 端点

Spring Boot 提供了一个  `metrics`  端点，可用于诊断检查应用程序收集的指标。端点默认情况下不可用，必须手动公开，请参阅 [暴露端点](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-endpoints-exposing-endpoints) 以获取更多详细信息。

导航至 `/actuator/metrics` 会显示可用仪表名称的列表。您可以通过提供特定的仪表名称作为选择器来深入查看其相关信息。 比如，`/actuator/metrics/jvm.memory.max`。

> 您在此处使用的名称应与代码中使用的名称相匹配，而不是已针对其出厂的监视系统将其命名惯例标准化后的名称。换句话说，如果在 Prometheus 中 `jvm.memory.max` 由于其蛇形命名约定而显示为 `jvm_memory_max`，则在检查 `metrics` 端点中的仪表时，仍应使用 `jvm.memory.max` 作为选择器。

你也可以添加任意数量的 `tag=KEY:VALUE` 查询参数到 URL 的末尾来钻取某个度量，比如 `/actuator/metrics/jvm.memory.max?tag=area:nonheap`：

> 报告的测量值是与仪表名称和已应用的所有标签相匹配的所有仪表的统计信息的*和*。因此，在上面的示例中，返回的 "Value" 统计量是堆的“代码缓存”，“压缩类空间”和“元空间”区域的最大内存占用量的总和。如果您只想查看“元空间”的最大大小，则可以添加一个额外的 `tag=id:Metaspace`，即 `/actuator/metrics/jvm.memory.max?tag=area:nonheap&tag=id:Metaspace`。

### 5.7. 审计

一旦启动了 Spring Security，Spring Boot Actuator 将具有一个灵活的审计框架，该框架可以发布事件（默认情况下，“身份验证成功”，“失败”和“拒绝访问”异常）。此功能对于报告和基于身份验证失败实施锁定策略非常有用。

可以通过在应用程序的配置中提供类型为 `AuditEventRepository` 的 Bean 来启用审计。为了方便起见，Spring Boot 提供了一个 `InMemoryAuditEventRepository`。`InMemoryAuditEventRepository` 具有有限的功能，我们建议仅将其用于开发环境。对于生产环境，请考虑创建自己的替代 `AuditEventRepository` 实现。

#### 5.7.1. 自定义审计

要自定义已发布的安全事件，可以提供自己的 `AbstractAuthenticationAuditListener` 和 `AbstractAuthorizationAuditListener` 的实现。

您也可以将审计服务用于自己的业务事件。为此，可以将 `AuditEventRepository` bean 注入到您自己的组件中，然后直接使用它，或者通过 Spring `ApplicationEventPublisher`（通过实现 `ApplicationEventPublisherAware`）发布 `AuditApplicationEvent`。

### 5.8. HTTP 跟踪

可以通过在应用程序的配置中提供类型为 `HttpTraceRepository` 的 bean 来启用 HTTP 跟踪。为了方便起见，Spring Boot 默认提供了一个 `InMemoryHttpTraceRepository`，用于存储最近100次请求-响应交互的跟踪。与其他跟踪解决方案相比，`InMemoryHttpTraceRepository` 是受限制的，我们建议仅将其用于开发环境。对于生产环境，建议使用可用于生产的跟踪或可观察性解决方案，例如 Zipkin 或 Spring Cloud Sleuth。或者，创建自己的 `HttpTraceRepository` 来满足您的需求。

`httptrace` 端点可用于获取有关存储在 `HttpTraceRepository` 中的请求-响应交换的信息。

#### 5.8.1. 自定义 HTTP 跟踪

要自定义每个跟踪中包含的项目，请使用`management.trace.http.include`配置属性。对于高级定制，请考虑注册自己的`HttpExchangeTracer`实现。

### 5.9. 进程监控

在 `spring-boot` 模块中，你可以找到两个类用来创建通常对进程监控很有用的文件：

- `ApplicationPidFileWriter` 创建一个包含应用 PID 的文件（默认是在应用目录下，文件名是 `application.pid`）。
- `WebServerPortFileWriter` 创建一个文件（或者多个文件）包含运行 web 服务器的端口（默认实在应用目录下，文件名是 `application.port`）。

默认情况下，这些写入器都没有激活，不过你可以通过一下方式手动启用：

- [通过扩展配置](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-process-monitoring-configuration)
- [编程方式](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-process-monitoring-programmatically)

#### 5.9.1. 扩展配置

在 `META-INF/spring.factories` 文件中，你可以激活写 PID 文件的监听器，如下面例子所示：

```
org.springframework.context.ApplicationListener=\
org.springframework.boot.context.ApplicationPidFileWriter,\
org.springframework.boot.web.context.WebServerPortFileWriter
```

#### 5.9.2. 编程方式

你还可以通过调用 `SpringApplication.addListeners(…)` 方法并出入相应的 `Writer` 对象激活监听器。这种方式也允许你在 `Writer` 构造器中自定义文件名和路径。

### 5.10. Cloud Foundry  支持

Spring Boot 执行器模块包含额外的支持，当你将应用部署到兼容的 Cloud Foundry 实例中时会被激活。`/cloudfoundryapplication` 路径提供了通向所有 `@Endpoint` 的替代安全路由。

扩展支持使 Cloud Foundry 管理 UI（例如可用于查看已部署的应用程序的 Web 应用程序）增加了 Spring Boot 执行器信息。例如，应用程序状态页面可能包含完整的运行状况信息，而不是典型的“正在运行”或“已停止”状态。

>  `/cloudfoundryapplication` 路径并不注解对普通用户开放。为了使用该端点，请求中必须携带有效的 UAA token 。

#### 5.10.1. 禁用扩展 Cloud Foundry 执行器支持

如果你想要完全禁用 `/cloudfoundryapplication` 端点，你可以将下面的设定到你的 `application.properties` 文件中：

**application.properties**

```properties
management.cloudfoundry.enabled=false
```

#### 5.10.2. Cloud Foundry 自签名证书

默认情况下， `/cloudfoundryapplication`  端点的安全性验证会对各种 Cloud Foundry 服务进行 SSL 调用。如果您的 Cloud Foundry UAA 或 Cloud Controller 服务使用自签名证书，则需要设置以下属性：

**application.properties**

```properties
management.cloudfoundry.skip-ssl-validation=true
```

#### 5.10.3. 自定义上下文路径

如果服务器的上下文路径已配置为`/`以外的任何其他值，则 Cloud Foundry 端点在应用程序的根目录将不可用。例如，如果使用 `server.servlet.context-path=/app`，则 Cloud Foundry 端点将位于 `/app/cloudfoundryapplication/*`。

如果您希望 Cloud Foundry 端点始终在 `/cloudfoundryapplication/*` 处可用，而不管服务器的上下文路径如何，那么您将需要在应用程序中显式配置它。配置将根据所使用的 Web 服务器而有所不同。对于 Tomcat，可以添加以下配置：

```java
@Bean
public TomcatServletWebServerFactory servletWebServerFactory() {
    return new TomcatServletWebServerFactory() {

        @Override
        protected void prepareContext(Host host, ServletContextInitializer[] initializers) {
            super.prepareContext(host, initializers);
            StandardContext child = new StandardContext();
            child.addLifecycleListener(new Tomcat.FixContextListener());
            child.setPath("/cloudfoundryapplication");
            ServletContainerInitializer initializer = getServletContextInitializer(getContextPath());
            child.addServletContainerInitializer(initializer, Collections.emptySet());
            child.setCrossContext(true);
            host.addChild(child);
        }

    };
}

private ServletContainerInitializer getServletContextInitializer(String contextPath) {
    return (c, context) -> {
        Servlet servlet = new GenericServlet() {

            @Override
            public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
                ServletContext context = req.getServletContext().getContext(contextPath);
                context.getRequestDispatcher("/cloudfoundryapplication").forward(req, res);
            }

        };
        context.addServlet("cloudfoundry", servlet).addMapping("/*");
    };
}
```

### 5.11. 进一步阅读

你可能会想要了解图形工具，比如 [Graphite](https://graphiteapp.org/)。

或者，你可以继续往下阅读，了解 [‘deployment options’](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#deployment) 或者直接跳到 *[build tool plugins](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#build-tool-plugins)* 以了解有关 Spring Boot 插件构建的深入知识。

## 6. 部署 Spring Boot 应用

在部署应用程序时，Spring Boot 的灵活打包选项提供了很多选择。您可以将 Spring Boot 应用程序部署到各种云平台，容器映像（例如 Docker）或虚拟机/真实机上。

本节介绍一些更常见的部署方案。

### 6.1. 部署到容器

如果从容器中运行应用程序，则可以使用可执行 jar，但是将其解压并以其他方式运行通常也是一个优点。某些 PaaS 实施也可能选择在运行存档之前将其解压缩。例如，Cloud Foundry 以这种方式运行。运行解压缩存档的最简单方法是启动相应的启动器，如下所示：

```
$ jar -xf myapp.jar
$ java org.springframework.boot.loader.JarLauncher
```

实际上，这在启动时（取决于 jar 的大小）比从未解压的存档中运行要快一些。在运行时，您不应期望有任何差异。

解压缩 jar 文件后，您还可以通过使用其“自然”主方法（而不是 ` JarLauncher`）运行应用程序来缩短启动时间。例如：

```
$ jar -xf myapp.jar
$ java -cp BOOT-INF/classes:BOOT-INF/lib/* com.example.MyApplication
```

还可以通过将依赖项作为与应用程序类和资源（通常会更频繁地更改）分开的一层复制到映像中来创建更有效的容器映像。实现这一层分离的方法不止一种。例如，使用 `Dockerfile` 可以将其表示为以下形式：

```
FROM openjdk:8-jdk-alpine AS builder
WORKDIR target/dependency
ARG APPJAR=target/*.jar
COPY ${APPJAR} app.jar
RUN jar -xf ./app.jar

FROM openjdk:8-jre-alpine
VOLUME /tmp
ARG DEPENDENCY=target/dependency
COPY --from=builder ${DEPENDENCY}/BOOT-INF/lib /app/lib
COPY --from=builder ${DEPENDENCY}/META-INF /app/META-INF
COPY --from=builder ${DEPENDENCY}/BOOT-INF/classes /app
ENTRYPOINT ["java","-cp","app:app/lib/*","com.example.MyApplication"]
```

假设上面的 `Dockerfile` 是当前目录，则可以使用 `docker build .`。或可选地指定应用程序 jar 的路径来构建 docker 映像，如以下示例所示：

```
docker build --build-arg APPJAR=path/to/myapp.jar .
```

### 6.2. 部署到云端

Spring Boot 的可执行 jar 已为大多数流行的云 PaaS（平台即服务）提供商准备。这些提供者往往要求您“自带容器”。他们管理应用进程（不是专门用于 Java 应用程序），因此他们需要一个中间层，以使您的应用程序适配运行进程的“云”概念。

两家受欢迎的云提供商，Heroku 和 Cloud Foundry，采用了“ buildpack”方法。 buildpack 将您部署的代码包装在*启动*应用程序所需的任何内容中。它可能是一个 JDK，可能是对 Java，嵌入式 Web 服务器或成熟的应用程序服务器的调用。一个 buildpack 是可插拔的，但是理想情况下，您应该能够通过尽可能少的自定义来获得它。这减少了您无法控制的功能的占用空间。它最大程度地减少了开发和生产环境之间的差异。

理想情况下，您的应用程序像 Spring Boot 可执行 jar 一样，具有打包运行所需的一切。

在本节中，我们研究如何获取在“入门”部分中启动并运行的 [我们开发的简单应用程序](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#getting-started-first-application) 。

#### 6.2.1. Cloud Foundry

如果未指定其他构建包，Cloud Foundry 将提供默认的构建包。 Cloud Foundry [Java buildpack](https://github.com/cloudfoundry/java-buildpack) 对 Spring 应用程序（包括 Spring Boot）具有出色的支持。您可以部署独立的可执行 jar 应用程序以及传统的 `.war` 打包应用程序。

一旦构建了应用程序（例如，使用 `mvn clean package` ），并 [安装了cf命令行工具](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html) ，使用 `cf push` 命令部署您的应用程序，替换为已编译的 `.jar` 的路径。在推送应用程序之前，请确保 [使用您的`cf`命令行客户端登录](https://docs.cloudfoundry.org/cf-cli/getting-started.html#login)。下面的行显示了使用 `cf push` 命令来部署应用程序：

```
$ cf push acloudyspringtime -p target/demo-0.0.1-SNAPSHOT.jar
```

> 在前面的示例中，我们用 `acloudyspringtime` 替换为 `cf` 作为应用程序名称的任何值。

参考 [`cf push` 文档](https://docs.cloudfoundry.org/cf-cli/getting-started.html#push) 了解更多选项。如果该目录下存在 Cloud Foundry [`manifest.yml`](https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html) 文件，它将会生效。

此时， `cf` 开始更新你的应用，产生类似下面的输出：

```
Uploading acloudyspringtime... OK
Preparing to start acloudyspringtime... OK
-----> Downloaded app package (8.9M)
-----> Java Buildpack Version: v3.12 (offline) | https://github.com/cloudfoundry/java-buildpack.git#6f25b7e
-----> Downloading Open Jdk JRE 1.8.0_121 from https://java-buildpack.cloudfoundry.org/openjdk/trusty/x86_64/openjdk-1.8.0_121.tar.gz (found in cache)
       Expanding Open Jdk JRE to .java-buildpack/open_jdk_jre (1.6s)
-----> Downloading Open JDK Like Memory Calculator 2.0.2_RELEASE from https://java-buildpack.cloudfoundry.org/memory-calculator/trusty/x86_64/memory-calculator-2.0.2_RELEASE.tar.gz (found in cache)
       Memory Settings: -Xss349K -Xmx681574K -XX:MaxMetaspaceSize=104857K -Xms681574K -XX:MetaspaceSize=104857K
-----> Downloading Container Certificate Trust Store 1.0.0_RELEASE from https://java-buildpack.cloudfoundry.org/container-certificate-trust-store/container-certificate-trust-store-1.0.0_RELEASE.jar (found in cache)
       Adding certificates to .java-buildpack/container_certificate_trust_store/truststore.jks (0.6s)
-----> Downloading Spring Auto Reconfiguration 1.10.0_RELEASE from https://java-buildpack.cloudfoundry.org/auto-reconfiguration/auto-reconfiguration-1.10.0_RELEASE.jar (found in cache)
Checking status of app 'acloudyspringtime'...
  0 of 1 instances running (1 starting)
  ...
  0 of 1 instances running (1 starting)
  ...
  0 of 1 instances running (1 starting)
  ...
  1 of 1 instances running (1 running)

App started
```

祝贺你！应用已经运行起来了！

一旦应用运行起来，你就可以验证应用的状态，通过使用 `cf apps` 命令，如下所示：

```
$ cf apps
Getting applications in ...
OK

name                 requested state   instances   memory   disk   urls
...
acloudyspringtime    started           1/1         512M     1G     acloudyspringtime.cfapps.io
...
```

一旦 Cloud Foundry 确认已经部署了您的应用程序，您就应该能够在给定的 URI 上找到该应用程序。在前面的示例中，您可以在以下位置找到它 `https://acloudyspringtime.cfapps.io/`。

##### 绑定到服务

默认情况下，有关正在运行的应用程序以及服务连接信息的元数据作为环境变量（例如：`$VCAP_SERVICES`）公开给应用程序。做出此架构决定是由于 Cloud Foundry 具有多种语言（可以将任何语言和平台作为 buildpack 支持）。进程范围的环境变量与语言无关。

环境变量并不总是使用最简单的API，因此 Spring Boot 会自动提取它们并将数据平整为可通过 Spring  `Environment` 抽象访问的属性，如以下示例所示：

```java
@Component
class MyBean implements EnvironmentAware {

    private String instanceId;

    @Override
    public void setEnvironment(Environment environment) {
        this.instanceId = environment.getProperty("vcap.application.instance_id");
    }

    // ...

}
```

所有 Cloud Foundry 属性均以 `vcap` 为前缀。您可以使用 `vcap` 属性来访问应用程序信息（例如应用程序的公共 URL）和服务信息（例如数据库凭据）。有关完整的详细信息，请参见 [`CloudFoundryVcapEnvironmentPostProcessor`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/api//org/springframework/boot/cloud/CloudFoundryVcapEnvironmentPostProcessor.html) Javadoc。

>  [Java CFEnv](https://github.com/pivotal-cf/java-cfenv/) 项目更适合诸如配置数据源之类的任务。

#### 6.2.2. Heroku

Heroku 是另一个流行的 PaaS 平台。要自定义 Heroku 构建，请提供一个 `Procfile`，该文件提供了部署应用程序所需的内容。Heroku 为 Java 应用程序分配一个 `port` 以供使用，然后确保到外部 URI 的路由起作用。

您必须配置您的应用程序以侦听正确的端口。以下示例显示了我们的入门 REST 应用程序的 `Procfile`：

```
web: java -Dserver.port=$PORT -jar target/demo-0.0.1-SNAPSHOT.jar
```

Spring Boot 使 `-D` 参数作为可从 Spring `Environment` 实例访问的属性。 `server.port` 配置属性被馈送到内置的 Tomcat，Jetty 或 Undertow 实例，然后在启动时使用该端口。 `$PORT` 环境变量是由 Heroku PaaS 分配给我们的。

这应该是您需要的一切。Heroku 部署最常见的部署工作流程是将代码 `git push` 到生产中，如以下示例所示：

```
$ git push heroku master

Initializing repository, done.
Counting objects: 95, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (78/78), done.
Writing objects: 100% (95/95), 8.66 MiB | 606.00 KiB/s, done.
Total 95 (delta 31), reused 0 (delta 0)

-----> Java app detected
-----> Installing OpenJDK 1.8... done
-----> Installing Maven 3.3.1... done
-----> Installing settings.xml... done
-----> Executing: mvn -B -DskipTests=true clean install

       [INFO] Scanning for projects...
       Downloading: https://repo.spring.io/...
       Downloaded: https://repo.spring.io/... (818 B at 1.8 KB/sec)
        ....
       Downloaded: https://s3pository.heroku.com/jvm/... (152 KB at 595.3 KB/sec)
       [INFO] Installing /tmp/build_0c35a5d2-a067-4abc-a232-14b1fb7a8229/target/...
       [INFO] Installing /tmp/build_0c35a5d2-a067-4abc-a232-14b1fb7a8229/pom.xml ...
       [INFO] ------------------------------------------------------------------------
       [INFO] BUILD SUCCESS
       [INFO] ------------------------------------------------------------------------
       [INFO] Total time: 59.358s
       [INFO] Finished at: Fri Mar 07 07:28:25 UTC 2014
       [INFO] Final Memory: 20M/493M
       [INFO] ------------------------------------------------------------------------

-----> Discovering process types
       Procfile declares types -> web

-----> Compressing... done, 70.4MB
-----> Launching... done, v6
       https://agile-sierra-1405.herokuapp.com/ deployed to Heroku

To git@heroku.com:agile-sierra-1405.git
 * [new branch]      master -> master
```

您的应用程序现在应该已经在 Heroku 上启动并运行了。有关更多详细信息，请参阅 [将 Spring Boot 应用程序部署到 Heroku](https://devcenter.heroku.com/articles/deploying-spring-boot-apps-to-heroku)。

#### 6.2.3. OpenShift

[OpenShift](https://www.openshift.com/) 是 Red Hat 对 Kubernetes 容器编排平台的公开 (以及商用) 扩展。类似于 Kubernetes，OpenShift 拥有很多用于安装基于 Spring Boot 的应用的选项。

OpenShift 拥有很多描述如何部署 Spring Boot 应用的资源，包括：

- [Using the S2I builder](https://blog.openshift.com/using-openshift-enterprise-grade-spring-boot-deployments/)
- [Architecture guide](https://access.redhat.com/documentation/en-us/reference_architectures/2017/html-single/spring_boot_microservices_on_red_hat_openshift_container_platform_3/)
- [Running as a traditional web application on Wildfly](https://blog.openshift.com/using-spring-boot-on-openshift/)
- [OpenShift Commons Briefing](https://blog.openshift.com/openshift-commons-briefing-96-cloud-native-applications-spring-rhoar/)

#### 6.2.4. Amazon Web Services (AWS)

Amazon Web Services 提供多种方法安装 Spring Boot 应用，可以是传统 web 应用的 war 包形式，也可以是包含内置 web 服务器的可执行 jar 文件形式。选项包括：

- AWS Elastic Beanstalk
- AWS Code Deploy
- AWS OPS Works
- AWS Cloud Formation
- AWS Container Registry

每种都有不同的特性和评价模型。本文档中，我们只描述最简单的选项： AWS Elastic Beanstalk。

##### AWS Elastic Beanstalk

如官方文档 [Elastic Beanstalk Java guide](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/create_deploy_Java.html) 中所述，有两种部署 java 应用的选择。可以选择使用 “Tomcat Platform” 或者 “Java SE platform”。

###### 使用 Tomcat Platform

这种方式将 Spring Boot 项目打包成 war 文件。不需要任何特殊配置。你只需要按照官方向导操作即可。

###### 使用 Java SE Platform

这种方式将 Spring Boot 项目打包成 jar 文件并执行内置的 web 容器。Elastic Beanstalk 环境运行一个 nginx 实例监听 80 端口以代理运行在 5000 端口上的实际的应用。想要配置它，添加下列内容到你的 `application.properties` 文件：

```
server.port=5000
```

> 上传二进制文件而不是源代码
>
> 默认情况下，Elastic Beanstalk 上传源代码并在 AWS 中编译它们。不过，还是上传二进制文件。为了做到这一点，添加类似于下面的内容到你的 `.elasticbeanstalk/config.yml` 文件中：
>
> ```xml
> deploy:
>     artifact: target/demo-0.0.1-SNAPSHOT.jar
> ```

> 通过设定环境类型降低资源消耗
>
> 默认情况下，Elastic Beanstalk 环境是负载均衡的。负载均衡将会带来显著的资源消耗。为了避免此类资源消耗，将环境类型设定为 “Single instance”，如 [the Amazon documentation](https://docs.aws.amazon.com/elasticbeanstalk/latest/dg/environments-create-wizard.html#environments-create-wizard-capacity) 中所述。你也可以通过使用 CLI 命令创建单实例环境：
>
> ```
> eb create -s
> ```

##### 总结

这是使用 AWS 的最简单方法之一，但还有更多内容需要介绍，例如如何将 Elastic Beanstalk 集成到任何 CI / CD 工具中，如何使用 Elastic Beanstalk Maven 插件而不是 CLI 等等。有 [博客帖子](https://exampledriven.wordpress.com/2017/01/09/spring-boot-aws-elastic-beanstalk-example/) 更加详细地介绍了这些主题。

#### 6.2.5. Boxfuse 和 Amazon Web Services

[Boxfuse](https://boxfuse.com/) 的工作原理是将您的 Spring Boot 可执行 jar 或 war 变成一个最小的 VM 映像，该映像可以在 VirtualBox 或 AWS 上不变地部署。Boxfuse 与 Spring Boot 进行了深度集成，并使用 Spring Boot 配置文件中的信息自动配置端口和运行状况检查 URL。Boxfuse 在生成的映像以及它提供的所有资源（实例，安全组，弹性负载均衡器等）中均利用此信息。

创建 [Boxfuse 帐户](https://console.boxfuse.com/) 后，将其连接到您的 AWS 帐户，安装最新版本的 Boxfuse Client，并确保该应用程序是由 Maven 或 Gradle 构建的 （例如，使用 `mvn clean package`），您可以使用类似于以下命令将 Spring Boot 应用程序部署到 AWS：

```
$ boxfuse run myapp-1.0.jar -env=prod
```

参考 [`boxfuse run` documentation](https://boxfuse.com/docs/commandline/run.html) 了解更多选项。如果当前目录下存在 [`boxfuse.conf`](https://boxfuse.com/docs/commandline/#configuration) 文件，它将会生效。

> 默认情况下，Boxfuse 在启动时会激活一个名为 `boxfuse` 的 Spring 配置文件。如果您的可执行 jar 或 war 文件包含 [`application-boxfuse.properties`](https://boxfuse.com/docs/payloads/springboot.html#configuration) 文件，则 Boxfuse 的配置将基于其包含的属性。

此时，`boxfuse` 将为您的应用程序创建一个映像，然后上传该映像，并在 AWS 上配置并启动必要的资源，其输出类似于以下示例：

```
Fusing Image for myapp-1.0.jar ...
Image fused in 00:06.838s (53937 K) -> axelfontaine/myapp:1.0
Creating axelfontaine/myapp ...
Pushing axelfontaine/myapp:1.0 ...
Verifying axelfontaine/myapp:1.0 ...
Creating Elastic IP ...
Mapping myapp-axelfontaine.boxfuse.io to 52.28.233.167 ...
Waiting for AWS to create an AMI for axelfontaine/myapp:1.0 in eu-central-1 (this may take up to 50 seconds) ...
AMI created in 00:23.557s -> ami-d23f38cf
Creating security group boxfuse-sg_axelfontaine/myapp:1.0 ...
Launching t2.micro instance of axelfontaine/myapp:1.0 (ami-d23f38cf) in eu-central-1 ...
Instance launched in 00:30.306s -> i-92ef9f53
Waiting for AWS to boot Instance i-92ef9f53 and Payload to start at https://52.28.235.61/ ...
Payload started in 00:29.266s -> https://52.28.235.61/
Remapping Elastic IP 52.28.233.167 to i-92ef9f53 ...
Waiting 15s for AWS to complete Elastic IP Zero Downtime transition ...
Deployment completed successfully. axelfontaine/myapp:1.0 is up and running at https://myapp-axelfontaine.boxfuse.io/
```

你的应用现在已经部署并运行在 AWS 上。

参考 [deploying Spring Boot apps on EC2](https://boxfuse.com/blog/spring-boot-ec2.html) 以及 [documentation for the Boxfuse Spring Boot integration](https://boxfuse.com/docs/payloads/springboot.html) 开始使用 Maven 构建来运行该应用程序。

#### 6.2.6. Google Cloud

Google Cloud 有几种可用于启动 Spring Boot 应用程序的选项。最容易上手的可能是 App Engine，但您也可以找到在 Container Engine 的容器中或 Compute Engine 的虚拟机上运行 Spring Boot 应用的方法。

要在 App Engine 中运行，您可以先在用户界面中创建一个项目，该项目将为您设置一个唯一的标识符，并还设置 HTTP 路由。将 Java 应用程序添加到项目中，然后将其保留为空，然后使用 [Google Cloud SDK](https://cloud.google.com/sdk/install) 从命令行或 CI 将 Spring Boot 应用程序推送到该插槽中建立。

App Engine Standard 要求您使用 WAR 包装。请按照 [这些步骤](https://github.com/GoogleCloudPlatform/getting-started-java/blob/master/appengine-standard-java8/springboot-appengine-standard/README.md) 将 App Engine Standard 应用程序部署到 Google Cloud。

另外，App Engine Flex 要求您创建一个 `app.yaml` 文件来描述您的应用程序所需的资源。通常，您将此文件放在 `src/main/appengine` 中，它应类似于以下文件：

```yaml
service: default

runtime: java
env: flex

runtime_config:
  jdk: openjdk8

handlers:
- url: /.*
  script: this field is required, but ignored

manual_scaling:
  instances: 1

health_check:
  enable_health_check: False

env_variables:
  ENCRYPT_KEY: your_encryption_key_here
```

您可以通过将项目 ID 添加到构建配置中来部署应用程序（例如，使用 Maven 插件），如以下示例所示：

```xml
<plugin>
    <groupId>com.google.cloud.tools</groupId>
    <artifactId>appengine-maven-plugin</artifactId>
    <version>1.3.0</version>
    <configuration>
        <project>myproject</project>
    </configuration>
</plugin>
```

然后使用 `mvn appengine:deploy` 部署(如果你需要首先进行身份认证，则构建将会失败)。

### 6.3. 安装 Spring Boot 应用

除了通过使用 `java -jar` 运行 Spring Boot 应用程序之外，还可以为 Unix 系统制作完全可执行的应用程序。完全可执行的 jar 可以像其他任何可执行二进制文件一样执行，也可以 [通过 `init.d` 或 `systemd` 注册](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#deployment-service)。这使得在普通生产环境中安装和管理 Spring Boot 应用程序变得非常容易。

> 完全可执行的 jar 通过在文件的开头嵌入一个额外的脚本来工作。当前，某些工具不接受此格式，因此您可能无法始终使用此技术。例如，`jar -xf` 可能会无声地提取无法完全执行的 jar 或 war。建议仅当您打算直接执行 jar 或 war 时才使其完全可执行，而不是使用 `java -jar` 来运行它或将其部署到 servlet 容器中。

> 不能使 zip64 格式的 jar 文件完全可执行。尝试这样做将导致一个 jar 文件，当直接执行该文件或使用 `java -jar` 时，该文件被报告为已损坏。包含一个或多个 zip64 格式嵌套 jar 的标准格式 jar 文件可以完全执行。

要使用 Maven 创建“完全可执行”的 jar，请使用以下插件配置：

```xml
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <configuration>
        <executable>true</executable>
    </configuration>
</plugin>
```

下面的例子展示了等效的 Gradle 配置：

```groovy
bootJar {
    launchScript()
}
```

然后，您可以通过键入 `./my-application.jar` （其中 `my-application` 是你的组件的名称）来运行您的应用程序。包含 jar 的目录用作应用程序的工作目录。

#### 6.3.1. 支持的操作系统

默认脚本支持大部分的 Linux 发布版，在 CentOS 和 Ubuntu 上测试过。其他平台，比如 OS X 和 FreeBSD，需要使用自定义的 `embeddedLaunchScript`。

#### 6.3.2. Unix/Linux 服务

Spring Boot 应用可以很容易地作为 Unix/Linux 服务启动，通过使用 `init.d` 或者 `systemd`。

##### 安装为 `init.d` 服务 (System V)

如果你配置 Spring Boot 的 Maven 或者 Gradle 插件来产生 [fully executable jar](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#deployment-install)，你并没有使用自定义 `embeddedLaunchScript`，你的应用就可以作为 `init.d` 服务使用。要做到这一点，链接该 jar 倒 `init.d` 以支持标准的 `start`， `stop`， `restart`， 以及 `status` 命令。

脚本支持以下特性：

- 以拥有 jar 文件的用户身份启动服务
- 通过使用 `/var/run/<appname>/<appname>.pid` 跟踪应用的 PID 
- 将控制台日志写入 `/var/log/<appname>.log`

假定你的应用安装在 `/var/myapp`，为了将其作为 `init.d` 服务，创建链接，如下：

```
$ sudo ln -s /var/myapp/myapp.jar /etc/init.d/myapp
```

一旦安装，你可以通过通用方式启动和关闭该服务。比如，在基于 Debian 的系统上，你可以通过下面的命令启动它：

```
$ service myapp start
```

> 如果应用没有启动，检查写入 `/var/log/<appname>.log` 的日志。

您还可以使用标准操作系统工具将应用程序标记为自动启动。例如，在 Debian 上，您可以使用以下命令：

```
$ update-rc.d myapp defaults <priority>
```

保护 `init.d` 服务

> 以下是一组有关如何保护作为 `init.d` 服务运行的 Spring Boot 应用程序的准则。它并不旨在详尽列出增强应用程序及其运行环境所需的所有工作。

当以 root 身份执行时（例如使用 root 来启动 `init.d` 服务时），默认的可执行脚本以 `RUN_AS_USER` 环境变量中指定的用户身份运行应用程序。如果未设置环境变量，则使用拥有 jar 文件的用户。您永远不要以 root 用户身份运行 Spring Boot 应用程序，因此 `RUN_AS_USER` 不应该是 root 用户，而应用程序的 jar 文件也不应归 root 用户所有。而是创建一个特定的用户来运行您的应用程序，并设置环境变量 `RUN_AS_USER` 或使用 `chown` 使其成为 jar 文件的所有者，如以下示例所示：

```
$ chown bootapp:bootapp your-app.jar
```

在这种情况下，默认的可执行脚本以 `bootapp` 用户身份运行应用程序。

> 为了减少应用程序的用户帐户被盗的机会，您应该考虑阻止它使用登录 shell。例如，您可以将帐户的 shell 程序设置为 `/usr/sbin/nologin`。

您还应该采取措施防止修改应用程序的 jar 文件。首先，配置其权限，使其不能被写入，只能由其所有者读取或执行，如以下示例所示：

```
$ chmod 500 your-app.jar
```

其次，如果您的应用程序或运行该应用程序的帐户受到威胁，您还应采取措施限制损害。如果攻击者确实获得了访问权限，则他们可以使 jar 文件可写并更改其内容。防止这种情况发生的一种方法是通过使用 `chattr` 使它不变，如以下示例所示：

```
$ sudo chattr +i your-app.jar
```

这将阻止任何用户（包括 root 用户）修改 jar。

如果使用 root 来控制应用程序的服务，并且您 [使用`.conf`文件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#deployment-script-customization-conf-file) 以自定义其启动，root 用户读取并评估 `.conf` 文件。应该相应地对其进行保护。使用 `chmod` 以便文件只能由所有者读取，并使用 `chown` 使 root 用户成为所有者，如以下示例所示：

```
$ chmod 400 your-app.conf
$ sudo chown root:root your-app.conf
```

##### 安装为 `systemd` 服务

`systemd` 是S ystem V init 系统的后继产品，现在被许多现代 Linux 发行版使用。尽管您可以继续将 `init.d` 脚本与 `systemd` 一起使用，但也可以通过使用 `systemd` “service” 脚本来启动 Spring Boot 应用程序。

假设您在 `/var/myapp` 中安装了一个 Spring Boot 应用程序，要将 Spring Boot 应用程序作为 `systemd` 服务安装，请创建一个名为 `myapp.service` 的脚本并将其放置在 `/etc/systemd/system` 目录。以下脚本提供了一个示例：

```
[Unit]
Description=myapp
After=syslog.target

[Service]
User=myapp
ExecStart=/var/myapp/myapp.jar
SuccessExitStatus=143

[Install]
WantedBy=multi-user.target
```

> 记得要修改你的应用的 `Description`， `User`，以及 `ExecStart` 字段。

>  `ExecStart` 字段并未声明脚本动作命令，这意味着默认使用 `run` 命令。

请注意，与作为 `init.d` 服务运行时不同，运行应用程序的用户，PID 文件和控制台日志文件均由 `systemd` 本身管理，因此必须通过使用 ‘service’ 脚本。有关更多详细信息，请查阅 [服务单元配置手册页](https://www.freedesktop.org/software/systemd/man/systemd.service.html) 。

要将应用程序标记为在系统启动时自动启动，请使用以下命令：

```
$ systemctl enable myapp.service
```

参考 `man systemctl` 了解更多细节。

##### 自定义启动脚本

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

##### 推导的"抓取"依赖

标准 Groovy 包含一个 `@Grab` 注解，可让您声明对第三方库的依赖关系。Groovy 可以使用这种有用的技术以与 Maven 或 Gradle 相同的方式下载 jar，而无需使用构建工具。

Spring Boot 进一步扩展了该技术，并尝试根据您的代码推断出要“抓取”哪些库。例如，由于先前显示的 `WebApplication` 代码使用了 `@RestController` 注解，因此 Spring Boot 会获取 “Tomcat” 和 “Spring MVC”。

以下各项用作 “抓取提示”：

| Items                                                      | Grabs                          |
| :--------------------------------------------------------- | :----------------------------- |
| `JdbcTemplate`, `NamedParameterJdbcTemplate`, `DataSource` | JDBC Application.              |
| `@EnableJms`                                               | JMS Application.               |
| `@EnableCaching`                                           | Caching abstraction.           |
| `@Test`                                                    | JUnit.                         |
| `@EnableRabbit`                                            | RabbitMQ.                      |
| extends `Specification`                                    | Spock test.                    |
| `@EnableBatchProcessing`                                   | Spring Batch.                  |
| `@MessageEndpoint` `@EnableIntegration`                    | Spring Integration.            |
| `@Controller` `@RestController` `@EnableWebMvc`            | Spring MVC + Embedded Tomcat.  |
| `@EnableWebSecurity`                                       | Spring Security.               |
| `@EnableTransactionManagement`                             | Spring Transaction Management. |

> 参考 Spring Boot CLI 源代码中 [`CompilerAutoConfiguration`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-cli/src/main/java/org/springframework/boot/cli/compiler/CompilerAutoConfiguration.java) 的子类来准确理解如何进行自定义。

##### 推导的"抓取"坐标

Spring Boot 通过允许您指定没有组或版本的依赖项（例如，`@Grab('freemarker')`）来扩展 Groovy 的标准 `@Grab` 支持。这样做可以参考 Spring Boot 的默认依赖元数据来推断工件的组和版本。

> 默认元数据与您使用的 CLI 版本相关。仅当您移至新版本的 CLI 时，它才会更改，从而使您可以控制依赖项的版本何时更改。可以在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#appendix-dependency-versions) 中找到。

##### 默认导入语句

为了帮助减少 Groovy 代码的大小，会自动包含几个 `import` 语句。注意，前面的示例如何引用 `@Component`，`@RestController` 和 `@RequestMapping`，而无需使用完全限定的名称或 `import` 语句。

> 许多 Spring 注解无需使用 `import` 语句即可工作。在添加导入之前，请尝试运行您的应用程序以查看失败的原因。

##### 自动 Main 方法

与等效的 Java 应用程序不同，您无需在 Groovy 脚本中包含 `public static void main(String[] args)` 方法。`SpringApplication` 是自动创建的，编译后的代码将作为 `source`。

##### 自定义依赖管理

默认情况下，CLI 在解决 `@Grab` 依赖项时会使用在 `spring-boot-dependencies` 中声明的依赖项管理。可以使用 `@DependencyManagementBom` 注解来配置其他的依赖管理，这些依赖管理将覆盖默认的依赖管理。注解的值应指定一个或多个 Maven BOM 的坐标（`groupId:artifactId:version`）。

例如，考虑以下声明：

```groovy
@DependencyManagementBom("com.example.custom-bom:1.0.0")
```

上面的声明在 Maven repository  `com/example/custom-versions/1.0.0/` 下选取了 `custom-bom-1.0.0.pom` 。

指定多个 BOM 时，它们以声明它们的顺序应用，如下例所示：

```java
@DependencyManagementBom(["com.example.custom-bom:1.0.0",
        "com.example.another-bom:1.0.0"])
```

前面的示例表明， `another-bom` 中的依赖项管理会覆盖 `custom-bom` 中的依赖项管理。

您可以在可以使用 `@Grab` 的任何地方使用 `@DependencyManagementBom`。但是，为了确保依赖性管理的顺序一致，您可以在应用程序中最多使用一次 `@DependencyManagementBom`。

#### 7.2.2. 具有多个源文件的应用程序

您可以对所有接受文件输入的命令使用 “shell globbing”。这样可以使您从单个目录使用多个文件，如以下示例所示：

```
$ spring run *.groovy
```

#### 7.2.3. 打包你的应用

您可以使用 `jar` 命令将您的应用程序打包到一个独立的可执行 jar 文件中，如以下示例所示：

```
$ spring jar my-app.jar *.groovy
```

产生的 jar 包含编译应用程序所产生的类以及应用程序的所有依赖关系，以便可以使用 `java -jar` 来运行它。jar 文件还包含来自应用程序的类路径的条目。您可以使用 `--include` 和 `--exclude` 添加和删除 jar 的显式路径。两者都用逗号分隔，并且都接受前缀 “+” 和 “-” 形式，以表示应将其从默认值中删除。默认包括以下内容：

```
public/**, resources/**, static/**, templates/**, META-INF/**, *
```

默认排除项如下：

```
.*, repository/**, build/**, target/**, **/*.jar, **/*.groovy
```

在命令行上输入 `spring help jar` 以获得更多信息。

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

### 7.3. 使用 Groovy Beans DSL 开发应用程序

Spring Framework 4.0 对 `beans{}` “DSL” （从 [Grails](https://grails.org/) 借来）具有本地支持，您可以使用相同的格式将 bean 定义嵌入 Groovy 应用程序脚本中。有时，这是包括外部功能（如中间件声明）的好方法，如以下示例所示：

```groovy
@Configuration(proxyBeanMethods = false)
class Application implements CommandLineRunner {

    @Autowired
    SharedService service

    @Override
    void run(String... args) {
        println service.message
    }

}

import my.company.SharedService

beans {
    service(SharedService) {
        message = "Hello World"
    }
}
```

您可以将类声明与 `beans{}` 混合在同一个文件中，只要它们位于顶层即可；或者，如果愿意，可以将 bean DSL 放在单独的文件中。

### 7.4. 使用 `settings.xml` 配置 CLI 

Spring Boot CLI 使用 Maven 的依赖性解析引擎 Aether 来解决依赖性。 CLI 利用 `~/.m2/settings.xml` 中的 Maven 配置来配置 Aether。CLI 遵循以下配置设置：

- Offline
- Mirrors
- Servers
- Proxies
- Profiles
  - Activation
  - Repositories
- Active profiles

参考 [Maven’s settings documentation](https://maven.apache.org/settings.html) 了解更多信息。

### 7.5. 进一步阅读

您可以使用 GitHub 存储库中的一些 [示例groovy脚本](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-cli/samples) 试用 Spring Boot CLI。 [源代码](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-cli/src/main/java/org/springframework/boot/cli) 中还包含丰富的 javadoc。

如果发现达到了 CLI 工具的极限，则可能需要考虑将应用程序转换为完整的 Gradle 或 Maven 构建的 “Groovy项目”。下一节将介绍 Spring Boot 的 “[构建工具插件](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#build-tool-plugins)”  ，可以与 Gradle 或 Maven 一起使用。

## 8. 构建工具插件

Spring Boot 为 Maven 和 Gradle 提供了构建工具插件。构建工具提供了多种功能特性，包括打包可执行 jar 。本节提供有关这两个插件的更多详细信息，以及在扩展不受支持的构建系统时所需的一些帮助。如果您刚刚入门，则可能需要阅读 “[使用Spring Boot](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot)” 中的 “[构建系统](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-build-systems)” 部分。

### 8.1. Spring Boot Maven 插件

The Spring Boot Maven 插件提供了 Spring Boot 对 Maven 的支持，允许你打包可执行 jar 或者 war 包，并原地运行应用。为了使用它，你必需使用 Maven 3.2 (或者更高版本)。

> 参考 [Spring Boot Maven Plugin Site](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/maven-plugin/) 获取完整的插件文档。

#### 8.1.1. 包含插件

为了使用 Spring Boot Maven 插件，在你的 `pom.xml` 文件的 `plugins` 部分中包含合适的 XML，如下面例子所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <!-- ... -->
    <build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <version>2.2.2.RELEASE</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>repackage</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

前面的配置重新打包了在 Maven 生命周期的 `package` 阶段构建的 jar 或 war。以下示例显示了重新打包的 jar 和位于 `target` 目录中的原始 jar：

```
$ mvn package
$ ls target/*.jar
target/myproject-1.0.0.jar target/myproject-1.0.0.jar.original
```

如上例所示，如果不包含 `<execution/>` 配置，则可以单独运行插件（但也必须使用软件包目标），如以下示例所示：

```
$ mvn package spring-boot:repackage
$ ls target/*.jar
target/myproject-1.0.0.jar target/myproject-1.0.0.jar.original
```

如果使用里程碑或快照发行版，则还需要添加相应的 `pluginRepository` 元素，如以下清单所示：

```xml
<pluginRepositories>
    <pluginRepository>
        <id>spring-snapshots</id>
        <url>https://repo.spring.io/snapshot</url>
    </pluginRepository>
    <pluginRepository>
        <id>spring-milestones</id>
        <url>https://repo.spring.io/milestone</url>
    </pluginRepository>
</pluginRepositories>
```

#### 8.1.2. 打包可执行 jar 和 war 文件

一旦 `spring-boot-maven-plugin` 被包含在你的 `pom.xml` 中，它将会自动尝试通过使用 `spring-boot:repackage` 目标重新打包压缩包来使得它们可执行。你应该通过使用常规的 `packaging` 元素配置你的项目打包为 jar 或者 war ，如下面例子所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <!-- ... -->
    <packaging>jar</packaging>
    <!-- ... -->
</project>
```

Spring 的 `package` 阶段会增强您现有的存档。可以通过使用配置选项来指定要启动的主类，如下所示，也可以通过向清单添加 `Main-Class` 属性来指定。如果您未指定主类，则插件会使用`public static void main(String[] args)` 方法搜索类。

```xml
<plugin>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-maven-plugin</artifactId>
    <configuration>
        <mainClass>com.example.app.Main</mainClass>
    </configuration>
</plugin>
```

为了构建并运行项目组件，使用下面的命令：

```
$ mvn package
$ java -jar target/mymodule-0.0.1-SNAPSHOT.jar
```

要构建既可执行又可部署到外部容器的 war 文件，您需要将嵌入式容器的相关性标记为 “provided”，如以下示例所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
    <!-- ... -->
    <packaging>war</packaging>
    <!-- ... -->
    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
            <scope>provided</scope>
        </dependency>
        <!-- ... -->
    </dependencies>
</project>
```

> 参考 “[Create a Deployable War File](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-create-a-deployable-war-file)” 部分了解创建可部署 war 文件的更多细节。

高级配置选项和示例可以在 [plugin info page](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/maven-plugin/) 上找到。

### 8.2. Spring Boot Gradle 插件

Spring Boot Gradle 插件在 Gradle 中提供了 Spring Boot 支持，可让您打包可执行 jar 或 war 归档文件，运行 Spring Boot 应用程序以及使用 `spring-boot-dependencies` 提供的依赖管理。它需要 Gradle 5.x（也支持4.10，但该支持在将来的版本中将删除）。请参阅插件的文档以了解更多信息：

- 参考文档 ([HTML](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/gradle-plugin/reference/html/) 和 [PDF](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/gradle-plugin/reference/pdf/spring-boot-gradle-plugin-reference.pdf))
- [API](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/gradle-plugin/reference/api/)

### 8.3. Spring Boot AntLib 模块

Spring Boot AntLib 模块为 Apache Ant 提供了基本的 Spring Boot 支持。您可以使用该模块创建可执行 jar。要使用该模块，您需要在 `build.xml` 中声明一个附加的 `spring-boot` 名称空间，如以下示例所示：

```xml
<project xmlns:ivy="antlib:org.apache.ivy.ant"
    xmlns:spring-boot="antlib:org.springframework.boot.ant"
    name="myapp" default="build">
    ...
</project>
```

你需要记住使用 `-lib` 选项启动 Ant ，如下面例子所示：

```
$ ant -lib <folder containing spring-boot-antlib-2.2.2.RELEASE.jar>
```

> “使用Spring Boot” 部分包含 [将 Apache Ant 与 `spring-boot-antlib` 一起使用](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-ant) 的更完整示例。

#### 8.3.1. Spring Boot Ant 任务

一旦 `spring-boot-antlib` 命名空间被声明，下面的附加任务将可用：

- [`spring-boot:exejar`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#spring-boot-ant-exejar)
- [`spring-boot:findmainclass`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#spring-boot-ant-findmainclass)

##### `spring-boot:exejar`

你可以使用 `exejar` 任务创建 Spring Boot 可执行 jar。该任务支持下列属性：

| Attribute     | Description             | Required                                |
| :------------ | :---------------------- | :-------------------------------------- |
| `destfile`    | 需要创建的目标 jar 文件 | Yes                                     |
| `classes`     | Java 类文件的根目录     | Yes                                     |
| `start-class` | 需要运行的应用主类      | No *(默认是找到的第一个声明主方法的类)* |

下面的嵌套元素可以用于该任务：

| Element     | Description                                                  |
| :---------- | :----------------------------------------------------------- |
| `resources` | 一个或者多个 [Resource Collections](https://ant.apache.org/manual/Types/resources.html#collection) 描述一系列 [Resources](https://ant.apache.org/manual/Types/resources.html) 应该被添加到要创建的 jar 文件内容中。 |
| `lib`       | 一个或者多个 [Resource Collections](https://ant.apache.org/manual/Types/resources.html#collection) 应该被添加到组成应用的运行时依赖类路径的 jar 类库集合中。 |

##### 示例

本节展示两个 Ant 任务的示例。

指定启动类

```xml
<spring-boot:exejar destfile="target/my-application.jar"
        classes="target/classes" start-class="com.example.MyApplication">
    <resources>
        <fileset dir="src/main/resources" />
    </resources>
    <lib>
        <fileset dir="lib" />
    </lib>
</spring-boot:exejar>
```

探测启动类

```xml
<exejar destfile="target/my-application.jar" classes="target/classes">
    <lib>
        <fileset dir="lib" />
    </lib>
</exejar>
```

#### 8.3.2. `spring-boot:findmainclass`

`exejar` 在内部使用 `findmainclass` 任务来查找声明 `main` 的类。如有必要，您也可以在构建中直接使用此任务。支持以下属性：

| Attribute     | Description                   | Required                      |
| :------------ | :---------------------------- | :---------------------------- |
| `classesroot` | Java 类文件的根目录           | Yes *(除非指定了主类)*        |
| `mainclass`   | 能够用于短路 `main` 类搜索    | No                            |
| `property`    | 应该与结果一起设置的 Ant 属性 | No *(如果未指定，将记录结果)* |

##### 示例

本节包含三个使用 `findmainclass` 的示例。

查找并记录

```xml
<findmainclass classesroot="target/classes" />
```

查找并设置

```xml
<findmainclass classesroot="target/classes" property="main-class" />
```

覆盖并设置

```xml
<findmainclass mainclass="com.example.MainClass" property="main-class" />
```

### 8.4. 支持其它构建系统

如果要使用 Maven，Gradle 或 Ant 以外的构建工具，则可能需要开发自己的插件。可执行 jar 需要遵循特定的格式，某些条目需要以未压缩的形式编写（请参阅 [可执行 jar 格式](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#executable-jar) ，有关详细信息，请参见附录部分）。

Spring Boot Maven 和 Gradle 插件都使用 `spring-boot-loader-tools` 来实际生成 jar。如果需要，可以直接使用此库。

#### 8.4.1. 重新打包压缩包

要重新打包现有的归档文件，使其成为一个独立的可执行归档文件，请使用 `org.springframework.boot.loader.tools.Repackager`。`Repackager` 类采用单个构造函数参数，该参数引用现有的 jar 或 war 归档文件。使用两个可用的 `repackage()` 方法之一来替换原始文件或写入新目标。在重新打包程序运行之前，还可以在其上配置各种设置。

#### 8.4.2. 嵌套类库

重新打包档案时，可以使用 `org.springframework.boot.loader.tools.Libraries` 接口包含对依赖文件的引用。我们这里没有提供任何 `Libraries` 的具体实现，因为它们通常是特定于构建系统的。

如果您的归档文件中已经包含库，则可以使用 `Libraries.NONE`。

#### 8.4.3. 查找主类

如果您不使用 `Repackager.setMainClass()` 指定主类，则重新包装器将使用 [ASM](https://asm.ow2.io/) 来读取类文件，并尝试使用 `public static void main(String[] args)` 方法查找合适的类。如果找到多个候选者，则会引发异常。

#### 8.4.4. 重新打包实现示例

下面的例子展示了一个典型的重新打包实现：

```java
Repackager repackager = new Repackager(sourceJarFile);
repackager.setBackupSource(false);
repackager.repackage(new Libraries() {
            @Override
            public void doWithLibraries(LibraryCallback callback) throws IOException {
                // Build system specific implementation, callback for each dependency
                // callback.library(new Library(nestedFile, LibraryScope.COMPILE));
            }
        });
```

### 8.5. 进一步阅读

如果您对构建工具插件的工作方式感兴趣，可以查看 GitHub 上的 [`spring-boot-tools`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-tools) 模块。有关可执行 jar 格式的更多技术细节，请参见 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#executable-jar)。

如果您有与构建相关的特定问题，可以查看 "[how-to](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto)" 指南。