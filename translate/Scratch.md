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

