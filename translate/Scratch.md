#### 4.25.1. 测试范围依赖

`spring-boot-starter-test` “Starter” (处于 `test` `scope` 中) 提供了下列类库：

- [JUnit 5](https://junit.org/junit5)（包括用于与 JUnit 4 向后兼容的老式引擎）：用于 Java 应用程序单元测试的事实上的标准。
- [Spring Test](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#integration-testing) & Spring Boot Test: 对 Spring Boot 应用程序的实用程序和集成测试支持。
- [AssertJ](https://joel-costigliola.github.io/assertj/): 流利的断言库。
- [Hamcrest](https://github.com/hamcrest/JavaHamcrest): 匹配器对象（也称为约束或谓词）库。
- [Mockito](https://mockito.github.io/): Java 模拟框架。
- [JSONassert](https://github.com/skyscreamer/JSONassert): JSON 的断言库。
- [JsonPath](https://github.com/jayway/JsonPath): JSON 的 XPath。

通常，我们发现这些通用库在编写测试时很有用。如果这些库不满足您的需求，则可以添加自己的其他测试依赖项。

