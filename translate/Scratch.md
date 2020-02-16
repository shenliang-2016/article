##### 自动配置的 Spring MVC 测试

要测试 Spring MVC 控制器是否按预期工作，请使用 `@WebMvcTest` 注解。`@WebMvcTest` 自动配置 Spring MVC 基础结构并将扫描的 bean 限制为 `@Controller`，`@ControllerAdvice`，`@JsonComponent`，`Converter`，`GenericConverter`，`Filter`，`HandlerInterceptor`，`WebMvcConfigurer` 和 `HandlerMethodArgumentResolver`。使用此注解时，不会扫描常规的 `@Component` Bean。

> `@WebMvcTest` 能够开启的自动配置设定的列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

> 如果你需要注册额外组件，比如 Jackson `Module` ，你可以通过使用 `@Import` 将额外的配置类导入你的测试中。

通常，`@WebMvcTest` 仅限于单个控制器，并与 `@MockBean` 结合使用以为所需的协作者提供模拟实现。

`@WebMvcTest` 还可以自动配置 `MockMvc`。Mock MVC 提供了一种强大的方法来快速测试 MVC 控制器，而无需启动完整的 HTTP 服务器。

> 您还可以通过在非 `@WebMvcTest`（例如，`@SpringBootTest`）中自动配置 `MockMvc`，方法是使用 `@AutoConfigureMockMvc` 对其进行注解。以下示例使用 `MockMvc`：

```java
import org.junit.jupiter.api.*;
import org.springframework.beans.factory.annotation.*;
import org.springframework.boot.test.autoconfigure.web.servlet.*;
import org.springframework.boot.test.mock.mockito.*;

import static org.assertj.core.api.Assertions.*;
import static org.mockito.BDDMockito.*;
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@WebMvcTest(UserVehicleController.class)
class MyControllerTests {

    @Autowired
    private MockMvc mvc;

    @MockBean
    private UserVehicleService userVehicleService;

    @Test
    void testExample() throws Exception {
        given(this.userVehicleService.getVehicleDetails("sboot"))
                .willReturn(new VehicleDetails("Honda", "Civic"));
        this.mvc.perform(get("/sboot/vehicle").accept(MediaType.TEXT_PLAIN))
                .andExpect(status().isOk()).andExpect(content().string("Honda Civic"));
    }

}
```

> 如果您需要配置自动配置的元素（例如，当应该应用 servlet 过滤器时），则可以使用 `@AutoConfigureMockMvc` 注解中的属性。

如果使用 HtmlUnit 或 Selenium，则自动配置还会提供 HtmlUnit `WebClient` bean 和/或 Selenium `WebDriver` bean。以下示例使用 HtmlUnit：

```java
import com.gargoylesoftware.htmlunit.*;
import org.junit.jupiter.api.*;
import org.springframework.beans.factory.annotation.*;
import org.springframework.boot.test.autoconfigure.web.servlet.*;
import org.springframework.boot.test.mock.mockito.*;

import static org.assertj.core.api.Assertions.*;
import static org.mockito.BDDMockito.*;

@WebMvcTest(UserVehicleController.class)
class MyHtmlUnitTests {

    @Autowired
    private WebClient webClient;

    @MockBean
    private UserVehicleService userVehicleService;

    @Test
    void testExample() throws Exception {
        given(this.userVehicleService.getVehicleDetails("sboot"))
                .willReturn(new VehicleDetails("Honda", "Civic"));
        HtmlPage page = this.webClient.getPage("/sboot/vehicle.html");
        assertThat(page.getBody().getTextContent()).isEqualTo("Honda Civic");
    }

}
```

> 默认情况下，Spring Boot 将 `WebDriver` bean 放在一个特殊的“作用域”中，以确保驱动程序在每次测试后退出并注入新实例。如果您不希望出现这种情况，则可以将 `@Scope("singleton")` 添加到您的 `WebDriver`  `@Bean` 定义中。

> 由 Spring Boot 创建的 `webDriver` 作用域将替换任何用户定义的同名作用域。如果您定义自己的 `webDriver` 范围，则可能会在使用 `@WebMvcTest` 时发现它停止工作。

如果您在类路径上具有 Spring Security，则 `@WebMvcTest` 还将扫描 `WebSecurityConfigurer` Bean。您可以使用 Spring Security 的测试支持来代替完全禁用此类测试的安全性。有关如何使用 Spring Security 的 `MockMvc` 支持的更多详细信息，请参见 *使用Spring Security测试* 方法部分。

> 有时编写 Spring MVC 测试是不够的。Spring Boot 可以帮助您运行 [使用实际服务器进行全面的端到端测试](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-with-running-server)。

