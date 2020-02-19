###### 自动配置的 Spring REST Docs 测试使用 WebTestClient

`@AutoConfigureRestDocs` 还可以用于 `WebTestClient`。你可以使用 `@Autowired` 注入它在你的测试中，如同通常使用 `@WebFluxTest` 和 Spring REST Docs 那样，如下面例子所示：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.restdocs.AutoConfigureRestDocs;
import org.springframework.boot.test.autoconfigure.web.reactive.WebFluxTest;
import org.springframework.test.web.reactive.server.WebTestClient;

import static org.springframework.restdocs.webtestclient.WebTestClientRestDocumentation.document;

@WebFluxTest
@AutoConfigureRestDocs
class UsersDocumentationTests {

    @Autowired
    private WebTestClient webTestClient;

    @Test
    void listUsers() {
        this.webTestClient.get().uri("/").exchange().expectStatus().isOk().expectBody()
                .consumeWith(document("list-users"));
    }

}
```

如果您需要对 Spring REST Docs 配置进行更多控制，而不是 `@AutoConfigureRestDocs` 属性提供的控制，则可以使用 `RestDocsWebTestClientConfigurationCustomizer` bean，如以下示例所示：

```java
@TestConfiguration(proxyBeanMethods = false)
public static class CustomizationConfiguration implements RestDocsWebTestClientConfigurationCustomizer {

    @Override
    public void customize(WebTestClientRestDocumentationConfigurer configurer) {
        configurer.snippets().withEncoding("UTF-8");
    }

}
```