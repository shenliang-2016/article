## 7 Null-安全性

尽管 Java 不允许您使用其类型系统表示 null 安全性，但 Spring Framework 现在在`org.springframework.lang`包中提供以下注解，以便您声明 API 和字段的可空性：

- [`@Nullable`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/lang/Nullable.html): 表示特定参数、返回值、或者字段可以是`null`。
- [`@NonNull`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/lang/NonNull.html): 表示特定参数、返回值、或者字段不能是`null` （如果参数、返回值或者字段上已经用了 `@NonNullApi` 和 `@NonNullFields` 则此注解不再需要）。
- [`@NonNullApi`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/lang/NonNullApi.html): 在包层面声明参数和返回值非空的默认语义。
- [`@NonNullFields`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/lang/NonNullFields.html): 在包层面声明字段非空的默认语义。

Spring Framework 本身利用了这些注解，但它们也可以在任何基于 Spring 的 Java 项目中使用，以声明空安全 API 和可选的空安全字段。尚未支持泛型类型参数，可变参数和数组元素可空性，但应在即将发布的版本中支持，请参阅 [SPR-15942](https://jira.spring.io/browse/SPR-15942) 以获取最新信息。预计可以在Spring Framework版本（包括次要版本）升级过程中对可空性声明进行微调。方法体内使用的类型的可空性超出了此功能的范围。

> 其他常见的库（如 Reactor 和 Spring Data）提供了使用类似的可空性配置的空安全 API，为 Spring 应用程序开发人员提供了一致的整体体验。

### 7.1 使用场景

除了提供 Spring Framework API 可空性的显式声明之外，IDE（例如 IDEA 或 Eclipse）可以使用这些注解来提供与 null 安全相关的有用警告，以避免在运行时出现`NullPointerException`。

它们还用于在 Kotlin 项目中保证 Spring API 的 null 安全性，因为 Kotlin 本身支持 null 安全性。更多详细信息可在 [Kotlin支持文档](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/languages.html#kotlin-null-safety) 中找到。

### 7.2 JSR-305 元注解

Spring 注解是使用 [JSR 305](https://jcp.org/en/jsr/detail?id=305) 注解进行元注解的（休眠但广泛传播的 JSR）。JSR-305 元注解允许 IDEA 或 Kotlin 等工具供应商以通用方式提供空安全支持，而无需对 Spring 注解进行硬编码支持。

没有必要也不建议将 JSR-305 依赖项添加到项目类路径中以利用 Spring null 安全性 API。只有在其代码库中使用空安全注解的基于 Spring 的库等项目才能添加`com.google.code.findbugs:jsr305:3.0.2`和`compileOnly` Gradle 配置或 Maven `provided` scope 以避免编译警告。