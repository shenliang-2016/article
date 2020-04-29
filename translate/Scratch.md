##### Deduced “grab” Dependencies

Standard Groovy includes a `@Grab` annotation, which lets you declare dependencies on third-party libraries. This useful technique lets Groovy download jars in the same way as Maven or Gradle would but without requiring you to use a build tool.

Spring Boot extends this technique further and tries to deduce which libraries to “grab” based on your code. For example, since the `WebApplication` code shown previously uses `@RestController` annotations, Spring Boot grabs "Tomcat" and "Spring MVC".

The following items are used as “grab hints”:

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

> See subclasses of [`CompilerAutoConfiguration`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-cli/src/main/java/org/springframework/boot/cli/compiler/CompilerAutoConfiguration.java) in the Spring Boot CLI source code to understand exactly how customizations are applied.

