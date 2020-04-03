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