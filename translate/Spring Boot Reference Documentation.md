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

