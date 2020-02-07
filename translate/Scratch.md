### 4.25. 测试

Spring Boot 提供了许多实用程序和注解，可以在测试应用程序时提供帮助。测试支持由两个模块提供：`spring-boot-test` 包含核心项，`spring-boot-test-autoconfigure` 支持测试的自动配置。

大多数开发人员使用 `spring-boot-starter-test` “Starter”，它会导入 Spring Boot 测试模块以及 JUnit Jupiter，AssertJ，Hamcrest 和许多其他有用的库。

> 启动程序还带来了老式引擎，因此您可以运行 JUnit 4 和 JUnit 5 测试。如果已将测试迁移到 JUnit 5，则应排除对 JUnit 4 的支持，如以下示例所示：
>
> ````
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
> ````

