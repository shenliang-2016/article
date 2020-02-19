###### 自动配置的 Spring REST Docs 测试使用 REST Assured

`@AutoConfigureRestDocs` 使可配置为使用 Spring REST Docs 的 `RequestSpecification` bean 可供您的测试使用。可以使用 `@Autowired` 注入它，并像使用 REST Assured 和 Spring REST Docs 一样，在测试中使用它，如以下示例所示：

```java
import io.restassured.specification.RequestSpecification;
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.restdocs.AutoConfigureRestDocs;
import org.springframework.boot.test.context.SpringBootTest;
import org.springframework.boot.test.context.SpringBootTest.WebEnvironment;
import org.springframework.boot.web.server.LocalServerPort;

import static io.restassured.RestAssured.given;
import static org.hamcrest.Matchers.is;
import static org.springframework.restdocs.restassured3.RestAssuredRestDocumentation.document;

@SpringBootTest(webEnvironment = WebEnvironment.RANDOM_PORT)
@AutoConfigureRestDocs
class UserDocumentationTests {

    @Test
    void listUsers(@Autowired RequestSpecification documentationSpec, @LocalServerPort int port) {
        given(documentationSpec).filter(document("list-users")).when().port(port).get("/").then().assertThat()
                .statusCode(is(200));
    }

}
```

如果您需要对 Spring REST Docs 配置进行更多控制，而不是通过 `@AutoConfigureRestDocs` 属性来提供更多控制，则可以使用 `RestDocsRestAssuredConfigurationCustomizer` bean，如以下示例所示：

```java
@TestConfiguration(proxyBeanMethods = false)
public static class CustomizationConfiguration implements RestDocsRestAssuredConfigurationCustomizer {

    @Override
    public void customize(RestAssuredRestDocumentationConfigurer configurer) {
        configurer.snippets().withTemplateFormat(TemplateFormats.markdown());
    }

}
```