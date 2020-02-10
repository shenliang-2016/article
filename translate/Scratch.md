##### 使用模拟环境测试

默认情况下， `@SpringBootTest` 不会启动服务器。如果你希望在模拟环境中测试你的 web 服务端点，你可以如下面例子所示配置 [`MockMvc`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference//testing.html#spring-mvc-test-framework) ：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.AutoConfigureMockMvc;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.web.servlet.MockMvc;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.content;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

@SpringBootTest
@AutoConfigureMockMvc
class MockMvcExampleTests {

    @Test
    void exampleTest(@Autowired MockMvc mvc) throws Exception {
        mvc.perform(get("/")).andExpect(status().isOk()).andExpect(content().string("Hello World"));
    }

}
```

> 如果你希望聚焦于 web 层，并不需要启动一个完整的 `ApplicationContext`，考虑 [使用 `@WebMvcTest` 代替](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-mvc-tests)。

另外，你可以配置 [`WebTestClient`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#webtestclient-tests) ，如下面例子所示：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.reactive.AutoConfigureWebTestClient;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.test.web.reactive.server.WebTestClient;

@SpringBootTest
@AutoConfigureWebTestClient
class MockWebTestClientExampleTests {

    @Test
    void exampleTest(@Autowired WebTestClient webClient) {
        webClient.get().uri("/").exchange().expectStatus().isOk().expectBody(String.class).isEqualTo("Hello World");
    }

}
```

> 在模拟环境中进行测试通常比在完整的 Servlet 容器中运行更快。但是，由于模拟是在 Spring MVC 层进行的，因此无法直接使用 MockMvc 来测试依赖于较低级别 Servlet 容器行为的代码。例如，Spring Boot 的错误处理基于 Servlet 容器提供的“错误页面”支持。这意味着，尽管您可以按预期测试 MVC 层引发和处理异常，但是您无法直接测试特定的 [自定义错误页面](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-error-handling-custom-error-pages) 呈现。如果您需要测试这些较低级别的问题，则可以按照下一节中的描述启动一个完全运行的服务器。

