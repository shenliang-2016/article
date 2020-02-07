#### 4.25.3. 测试 Spring Boot 应用

一个 Spring Boot 应用就是一个 Spring `ApplicationContext`，因此，相比于传统的 Spring context 的测试，测试 Spring Boot 应用时，你不需要做任何特殊的额外操作。

> 默认情况下，仅当使用 `SpringApplication` 创建 Spring Boot 的外部属性，日志记录和其他功能时，才将其安装在上下文中。

Spring Boot 提供了一个 `@SpringBootTest` 注解，当你需要使用 Spring Boot 特性时，该注解可以替代标准的 `spring-test` `@ContextConfiguration` 注解用于测试。该注解通过 [creating the `ApplicationContext` used in your tests through `SpringApplication`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-detecting-config) 工作。除了 `@SpringBootTest` 之外，还提供了许多其他注解来 [测试更具体的切片](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-tests) 。

> 如果您使用的是 JUnit 4，请不要忘记在测试中也添加 `@RunWith(SpringRunner.class)`，否则注解将被忽略。如果您使用的是 JUnit 5，则无需在 `@SpringBootTest` 中添加等效的 `@ExtendWith(SpringExtension.class)` 和其他 `@…Test` 注解。

默认情况下，`@SpringBootTest` 将不会启动服务器。您可以使用 `@SpringBootTest` 的 `webEnvironment` 属性来进一步完善测试的运行方式：

- `MOCK`(默认) : 加载 Web `ApplicationContext` 并提供模拟 Web 环境。使用此注解时，不会启动嵌入式服务器。如果您的类路径中没有 Web 环境，则此模式将透明地降级到创建常规的非 Web `ApplicationContext`。它可以与 [`@AutoConfigureMockMvc` 或 `@AutoConfigureWebTestClient`](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-with-mock-environment)结合使用，用于对 Web 应用程序进行基于模拟的测试。
- `RANDOM_PORT`: 加载一个 `WebServerApplicationContext` 并提供一个真实的 Web 环境。嵌入式服务器将启动并在随机端口上侦听。
- `DEFINED_PORT`: 加载一个 `WebServerApplicationContext` 并提供一个真实的 Web 环境。嵌入式服务器启动并在定义的端口（来自 `application.properties` ）或默认端口 `8080` 上侦听。
- `NONE`: 使用 `SpringApplication` 加载 `ApplicationContext`，但不提供任何 Web 环境（模拟或其他方式）。

> 如果您的测试是 `@Transactional`，则默认情况下它将在每个测试方法的末尾回滚事务。但是，由于将这种安排与 `RANDOM_PORT` 或 `DEFINED_PORT` 一起使用隐式提供了一个真实的 Servlet 环境，因此 HTTP 客户端和服务器在单独的线程中运行，因此在单独的事务中运行。在这种情况下，服务器上启动的任何事务都不会回滚。

> 如果您的应用程序对管理服务器使用不同的端口，则将带有 `WebEnvironment = WebEnvironment.RANDOM_PORT` 的 `@SpringBootTest` 还将在单独的随机端口上启动管理服务器。

