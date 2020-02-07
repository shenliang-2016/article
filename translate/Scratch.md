#### 4.25.2. 测试 Spring 应用

依赖注入的主要优点之一是，它应该使您的代码更易于进行单元测试。您可以使用 `new` 运算符实例化对象，甚至不需要使用 Spring。您也可以使用 *mock objects* 代替真正的依赖。

通常，您需要超越单元测试并开始集成测试（使用 Spring `ApplicationContext`）。能够进行集成测试而无需部署应用程序或连接到其他基础结构是很有用的。

Spring 框架包括用于此类集成测试的专用测试模块。您可以直接向 `org.springframework:spring-test` 声明一个依赖项，也可以使用 `spring-boot-starter-test` “Starter”将其引入。

如果您以前没有使用过 `spring-test` 模块，则应先阅读 [相关部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#testing) 。

