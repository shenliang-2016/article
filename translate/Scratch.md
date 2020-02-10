##### 探测 Web 应用类型

如果 Spring MVC 可用，则配置基于常规 MVC 的应用程序上下文。如果您只有 Spring WebFlux，我们将检测到该情况并配置基于 WebFlux 的应用程序上下文。

如果两者都存在，则 Spring MVC 优先。如果要在这种情况下测试反应式 Web 应用程序，则必须设置 `spring.main.web-application-type` 属性：

```java
@SpringBootTest(properties = "spring.main.web-application-type=reactive")
class MyWebFluxTests { ... }
```

##### 探测测试配置

如果您熟悉 Spring Test Framework，可能会习惯于使用 `@ContextConfiguration(classes=…)` 来指定要加载哪个 Spring `@Configuration`。另外，您可能经常在测试中使用嵌套的 `@Configuration` 类。

在测试 Spring Boot 应用程序时，通常不需要这样做。只要您没有明确定义，Spring Boot 的 `@*Test` 注解就会自动搜索您的主要配置。

搜索算法从包含测试的程序包开始工作，直到找到带有 `@SpringBootApplication` 或 `@SpringBootConfiguration` 注解的类。只要您以明智的方式 [结构化代码](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-structuring-your-code)，通常可以找到您的主要配置。

> 如果您使用 [测试注解来测试应用程序的特定部分](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-tests) ，则应避免在 [包含 main 方法的应用类](https://docs.spring.io/spring-boot/) 上添加特定于特定区域的配置设置。`@SpringBootApplication` 的底层组件扫描配置定义了排除过滤器，这些过滤器用于确保切片效果符合预期。如果在 `@SpringBootApplication` 注解的类上使用显式的 `@ComponentScan` 指令，请注意那些过滤器将被禁用。如果使用切片，则应重新定义它们。

如果要自定义主要配置，则可以使用嵌套的 `@TestConfiguration` 类。与将使用嵌套的 `@Configuration` 类而不是应用程序的主要配置不同的是，除了使用应用程序的主要配置之外，还使用嵌套的 `@TestConfiguration` 类。

> Spring 的测试框架会在测试之间缓存应用程序上下文。因此，只要您的测试共享相同的配置（无论如何发现），加载上下文的潜在耗时过程就只会发生一次。

