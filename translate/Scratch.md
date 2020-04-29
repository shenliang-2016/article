##### 推导的"抓取"依赖

标准 Groovy 包含一个 `@Grab` 注解，可让您声明对第三方库的依赖关系。Groovy 可以使用这种有用的技术以与 Maven 或 Gradle 相同的方式下载 jar，而无需使用构建工具。

Spring Boot 进一步扩展了该技术，并尝试根据您的代码推断出要“抓取”哪些库。例如，由于先前显示的 `WebApplication` 代码使用了 `@RestController` 注解，因此 Spring Boot 会获取 “Tomcat” 和 “Spring MVC”。

以下各项用作 “抓取提示”：

| Items                                                      | Grabs                          |
| :--------------------------------------------------------- | :----------------------------- |
| `JdbcTemplate`, `NamedParameterJdbcTemplate`, `DataSource` | JDBC Application.              |
| `@EnableJms`                                               | JMS Application.               |
| `@EnableCaching`                                           | Caching abstraction.           |
| `@Test`                                                    | JUnit.                         |
| `@EnableRabbit`                                            | RabbitMQ.                      |
| extends `Specification`                                    | Spock test.                    |
| `@EnableBatchProcessing`                                   | Spring Batch.                  |
| `@MessageEndpoint` `@EnableIntegration`                    | Spring Integration.            |
| `@Controller` `@RestController` `@EnableWebMvc`            | Spring MVC + Embedded Tomcat.  |
| `@EnableWebSecurity`                                       | Spring Security.               |
| `@EnableTransactionManagement`                             | Spring Transaction Management. |

> 参考 Spring Boot CLI 源代码中 [`CompilerAutoConfiguration`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-cli/src/main/java/org/springframework/boot/cli/compiler/CompilerAutoConfiguration.java) 的子类来准确理解如何进行自定义。

