##### 使用运行服务器测试

如果需要启动完全运行的服务器，建议您使用随机端口。如果使用 `@SpringBootTest(webEnvironment=WebEnvironment.RANDOM_PORT)`，则每次运行测试时都会随机选择一个可用端口。

`@LocalServerPort` 注解可用于 [注入使用的实际端口](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-discover-the-http-port-at-runtime) 进入测试。为了方便起见，需要对启动的服务器进行 REST 调用的测试可以另外使用 `@Autowire` 一个 [`WebTestClient`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#webtestclient-tests)，它解析到正在运行的服务器的相对链接，并带有用于验证响应的专用 API，如以下示例所示：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.context.SpringBootTest.WebEnvironment;
import org.springframework.test.web.reactive.server.WebTestClient;

@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
class RandomPortWebTestClientExampleTests {

    @Test
    void exampleTest(@Autowired WebTestClient webClient) {
        webClient.get().uri("/").exchange().expectStatus().isOk().expectBody(String.class).isEqualTo("Hello World");
    }

}
```

这种设置需要在类路径上使用 `spring-webflux`。如果您无法或不会添加 webflux，则 Spring Boot 还提供了 `TestRestTemplate` 工具：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.context.SpringBootTest.WebEnvironment;
import org.springframework.boot.test.web.client.TestRestTemplate;

import static org.assertj.core.api.Assertions.assertThat;

@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
class RandomPortTestRestTemplateExampleTests {

    @Test
    void exampleTest(@Autowired TestRestTemplate restTemplate) {
        String body = restTemplate.getForObject("/", String.class);
        assertThat(body).isEqualTo("Hello World");
    }

}
```