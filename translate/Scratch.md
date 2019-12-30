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

