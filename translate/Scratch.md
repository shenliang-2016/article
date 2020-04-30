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

