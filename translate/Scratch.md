#### 4.1.7. Web 环境

`SpringApplication` 试图根据你的行为创建正确类型的 `ApplicationContext` 。用来确定 `WebApplicationType` 的算法相当简单：

- 如果存在 Spring MVC ，使用 `AnnotationConfigServletWebServerApplicationContext` 。
- 如果不存在 Spring MVC，而是存在 Spring WebFlux，使用 `AnnotationConfigReactiveWebServerApplicationContext` 。
- 否则，使用 `AnnotationConfigApplicationContext` 。

这就意味着如果你在同一个应用中使用 Spring MVC 和新的来自 Spring WebFlux 的 `WebClient` ，Spring MVC 将默认被使用。你可以通过调用 `setWebApplicationType(WebApplicationType)` 很容易地覆盖它。

通过调用 `setApplicationContextClass(…)` 对 `ApplicationContext` 类型进行完全控制也是可能的。

> 在 JUnit 测试中使用 `SpringApplication` 时，通常希望调用 `setWebApplicationType(WebApplicationType.NONE)`。

#### 4.1.8. 访问应用参数

如果您需要访问传递给 `SpringApplication.run(…)` 的应用程序参数，则可以注入 `org.springframework.boot.ApplicationArguments` bean。通过 `ApplicationArguments` 接口，可以访问原始的 `String[]` 参数以及已解析的 `option` 和 `non-option` 参数，如以下示例所示：

```java
import org.springframework.boot.*;
import org.springframework.beans.factory.annotation.*;
import org.springframework.stereotype.*;

@Component
public class MyBean {

    @Autowired
    public MyBean(ApplicationArguments args) {
        boolean debug = args.containsOption("debug");
        List<String> files = args.getNonOptionArgs();
        // if run with "--debug logfile.txt" debug=true, files=["logfile.txt"]
    }

}
```

> Spring Boot 还在 Spring `Environment` 中注册了 `CommandLinePropertySource` 。这也使您可以通过使用 `@Value` 注解来注入单个应用程序参数。

