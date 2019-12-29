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

