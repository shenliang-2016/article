##### 自动配置的 Spring WebFlux 测试

要测试 [Spring WebFlux](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference//web-reactive.html) 控制器是否按预期工作，可以使用 `@WebFluxTest` 注解。`@WebFluxTest` 自动配置 Spring WebFlux 基础结构，并将扫描的 bean 限制为 `@Controller`，`@ControllerAdvice`，`@JsonComponent`，`Converter`，`GenericConverter`，`WebFilter` 和 `WebFluxConfigurer`。使用 `@WebFluxTest` 注解时，不会扫描常规的 `@Component` bean。

> `@WebFluxTest` 能够开启的自动配置设定列表可以在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中找到。

> 如果您需要注册其他组件，例如 Jackson `Module`，则可以在测试中使用 `@Import` 导入其他配置类。

通常，`@WebFluxTest` 仅限于单个控制器，并与 `@MockBean` 注解结合使用，以为所需的协作者提供模拟实现。

`@WebFluxTest` 也会自动配置 [WebTestClient](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#webtestclient)，提供了快速测试 WebFlux 控制器而无需启动完整的 HTTP 服务器的强大方法。

> 您也可以在非 `@WebFluxTest`（例如，`@SpringBootTest`）中自动配置 `WebTestClient`，方法是使用 `@AutoConfigureWebTestClient` 对其进行注解。以下示例显示了同时使用 `@WebFluxTest` 和 `WebTestClient` 的类：

````java
import org.junit.jupiter.api.Test;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.reactive.WebFluxTest;
import org.springframework.http.MediaType;
import org.springframework.test.web.reactive.server.WebTestClient;

@WebFluxTest(UserVehicleController.class)
class MyControllerTests {

    @Autowired
    private WebTestClient webClient;

    @MockBean
    private UserVehicleService userVehicleService;

    @Test
    void testExample() throws Exception {
        given(this.userVehicleService.getVehicleDetails("sboot"))
                .willReturn(new VehicleDetails("Honda", "Civic"));
        this.webClient.get().uri("/sboot/vehicle").accept(MediaType.TEXT_PLAIN)
                .exchange()
                .expectStatus().isOk()
                .expectBody(String.class).isEqualTo("Honda Civic");
    }

}
````

> 只有 WebFlux 应用程序支持此设置，因为在模拟的 web 应用程序中使用 `WebTestClient` 目前仅适用于WebFlux。

> `@WebFluxTest` 无法检测通过功能性 web 框架注册的路由。为了在上下文中测试 `RouterFunction` bean，请考虑自己通过 `@Import` 或使用 `@SpringBootTest` 导入 `RouterFunction`。

> `@WebFluxTest` 无法检测通过 `SecurityWebFilterChain` 类型的 `@Bean` 注册的自定义安全配置。为了将其包含在测试中，您将需要通过 `@Import` 或使用 `@SpringBootTest` 导入用于注册 bean 的配置。

> 有时候编写 Spring WebFlux 测试是不够的；Spring Boot 能够帮助你运行 [实际服务器上完整的端到端测试](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-with-running-server))。

