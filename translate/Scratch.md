##### 自动配置的 Spring REST Docs 测试

您可以在 Mock MVC，REST Assured 或 WebTestClient 的测试中使用 `@AutoConfigureRestDocs` 来使用 [Spring REST Docs](https://spring.io/projects/spring-restdocs)。它消除了 Spring REST Docs 中对 JUnit 扩展的需求。

可以使用 `@AutoConfigureRestDocs` 覆盖默认输出目录（如果使用 Maven，则使用 `target/generated-snippets`；如果使用 Gradle，则使用 `build/generated-snippets`）。它也可以用于配置出现在任何记录的 URI 中的主机，模式和端口。

##### 自动配置的 Spring REST Docs 测试使用 Mock MVC

`@AutoConfigureRestDocs` 定制 `MockMvc` bean 使用 Spring REST Docs。您可以使用 `@Autowired` 注入它，并像通常使用 Mock MVC 和 Spring REST Docs 一样在测试中使用它。如下面例子所示：

```java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;

import static org.springframework.restdocs.mockmvc.MockMvcRestDocumentation.document;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@WebMvcTest(UserController.class)
@AutoConfigureRestDocs
class UserDocumentationTests {

    @Autowired
    private MockMvc mvc;

    @Test
    void listUsers() throws Exception {
        this.mvc.perform(get("/users").accept(MediaType.TEXT_PLAIN))
                .andExpect(status().isOk())
                .andDo(document("list-users"));
    }

}
```

如果您需要对 Spring REST Docs 配置的控制多于 `@AutoConfigureRestDocs` 的属性所提供的控制，则可以使用 `RestDocsMockMvcConfigurationCustomizer` bean，如以下示例所示：

```java
@TestConfiguration
static class CustomizationConfiguration
        implements RestDocsMockMvcConfigurationCustomizer {

    @Override
    public void customize(MockMvcRestDocumentationConfigurer configurer) {
        configurer.snippets().withTemplateFormat(TemplateFormats.markdown());
    }

}
```

如果您想使用 Spring REST Docs 对参数化输出目录的支持，则可以创建一个 `RestDocumentationResultHandler` bean。自动配置使用此结果处理程序调用 `alwaysDo`，从而使每个 `MockMvc` 调用自动生成默认代码段。以下示例显示了一个已定义的 `RestDocumentationResultHandler`：

```java
@TestConfiguration(proxyBeanMethods = false)
static class ResultHandlerConfiguration {

    @Bean
    public RestDocumentationResultHandler restDocumentation() {
        return MockMvcRestDocumentation.document("{method-name}");
    }

}
```