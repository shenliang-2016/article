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

