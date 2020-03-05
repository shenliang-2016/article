#### 4.25.4. 测试工具

一些通用的测试工具类作为其一部分打包在 `spring-boot` 中。

##### ConfigFileApplicationContextInitializer

`ConfigFileApplicationContextInitializer` 是一个 `ApplicationContextInitializer` ，你可以用在你的测试中用来加载 Spring Boot `application.properties` 文件。当你不需要使用 `@SpringBootTest` 提供的完整的特性集合的情况下可以使用它，如下面例子所示：

```java
@ContextConfiguration(classes = Config.class,
    initializers = ConfigFileApplicationContextInitializer.class)
```

> 单独使用 `ConfigFileApplicationContextInitializer` 不会提供对 `@Value("${…}")` 注入的支持。它仅仅保证 `application.properties` 文件被加载进入 Spring’s `Environment`。为了 `@Value` 支持，你需要要么额外配置一个 `PropertySourcesPlaceholderConfigurer` 或者使用 `@SpringBootTest`，它会自动为你配置一个。

##### TestPropertyValues

`TestPropertyValues` 帮助你快速地添加属性到 `ConfigurableEnvironment` 或者 `ConfigurableApplicationContext`。你可以通过 `key=value` 字符串调用它，如下：

```java
TestPropertyValues.of("org=Spring", "name=Boot").applyTo(env);
```

##### OutputCapture

`OutputCapture` 是一个 JUnit `Extension` ，可以用来捕获 `System.out` 和 `System.err` 输出。为你的测试类的构造函数添加 `@ExtendWith(OutputCaptureExtension.class)` 并注入 `CapturedOutput` 作为构造函数或者测试方法的一个参数，如下所示：

```java
@ExtendWith(OutputCaptureExtension.class)
class OutputCaptureTests {

    @Test
    void testName(CapturedOutput output) {
        System.out.println("Hello World!");
        assertThat(output).contains("World");
    }

}
```

##### TestRestTemplate

`TestRestTemplate` 是 Spring’s `RestTemplate` 的方便的替代品，在集成测试中非常有用。你可以获得一个普通的模板或者发送 Basic HTTP 认证 (使用用户名和密码) 的模板。无论哪种情况，该模板都会以测试友好的方式工作，而不会抛出服务端错误异常。

> Spring Framework 5.0 提供了一个新的 `WebTestClient` 用于 [WebFlux 集成测试](https://docs.spring.io/spring-boot/docs/2.2.5.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-webflux-tests) 和 [WebFlux 和 MVC 端到端测试](https://docs.spring.io/spring-boot/docs/2.2.5.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-with-running-server)。它提供了链式的 API 用于断言，这一点不同于 `TestRestTemplate`。

推荐。而非强制要求，使用 Apache HTTP Client (version 4.3.2 或更高)。如果你的类路径上存在，则 `TestRestTemplate` 就会作为你合理配置客户端的响应。如果你没有使用 Apache’s HTTP client，则有其它测试友好的特性可用：

- Redirects 不被允许 (因此你可以断言相应位置)。
- Cookies 被忽略 (因此该模板是无状态的)。

`TestRestTemplate` 可以在你的集成测试中直接被实例化，如下面例子所示：

```java
public class MyTest {

    private TestRestTemplate template = new TestRestTemplate();

    @Test
    public void testRequest() throws Exception {
        HttpHeaders headers = this.template.getForEntity(
                "https://myhost.example.com/example", String.class).getHeaders();
        assertThat(headers.getLocation()).hasHost("other.example.com");
    }

}
```

另外，如果您结合 `WebEnvironment.RANDOM_PORT` 或 `WebEnvironment.DEFINED_PORT` 使用 `@SpringBootTest` 注解，则可以注入完全配置的 `TestRestTemplate` 并开始使用它。如有必要，可以通过 `RestTemplateBuilder` bean 来应用其他定制。未指定主机和端口的所有 URL 都会自动连接到嵌入式服务器，如以下示例所示：

```java
@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
class SampleWebClientTests {

    @Autowired
    private TestRestTemplate template;

    @Test
    void testRequest() {
        HttpHeaders headers = this.template.getForEntity("/example", String.class).getHeaders();
        assertThat(headers.getLocation()).hasHost("other.example.com");
    }

    @TestConfiguration(proxyBeanMethods = false)
    static class Config {

        @Bean
        RestTemplateBuilder restTemplateBuilder() {
            return new RestTemplateBuilder().setConnectTimeout(Duration.ofSeconds(1))
                    .setReadTimeout(Duration.ofSeconds(1));
        }

    }

}
```