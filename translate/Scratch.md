##### 附加自动配置和切片

每个切片提供一个或多个 `@ AutoConfigure…` 注解，即定义应包含在切片中的自动配置。可以通过创建自定义的 `@AutoConfigure…` 注解来添加其他自动配置，也可以简单地通过向测试中添加 `@ImportAutoConfiguration` 来添加其他自动配置，如以下示例所示：

```java
@JdbcTest
@ImportAutoConfiguration(IntegrationAutoConfiguration.class)
class ExampleJdbcTests {

}
```

> 确保不要使用常规的 `@Import` 注解来引入自动配置，因为自动配置类由 Spring Boot 通过特殊的方式处理。

##### 用户配置和切片

如果你以明智的方式 [结构化你的代码](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/htmlsingle/#using-boot-structuring-your-code)，则你的 `@SpringBootApplication` 类就会 [默认被用作](https://docs.spring.io/spring-boot/docs/2.2.4.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-detecting-config) 你的测试的配置类。

因此，变得不重要的是，不要使用特定于其功能特定区域的配置设置来丢弃应用程序的主类。

假设您正在使用 Spring Batch，并且依赖于它的自动配置，您可以如下定义您的 `@SpringBootApplication`：

```java
@SpringBootApplication
@EnableBatchProcessing
public class SampleApplication { ... }
```

因为此类是测试的源配置，所以任何切片测试实际上都尝试启动 Spring Batch，这绝对不是您想要执行的操作。推荐的方法是将特定于区域的配置移到与您的应用程序相同级别的单独的 `@Configuration` 类，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
@EnableBatchProcessing
public class BatchConfiguration { ... }
```

> 根据您应用程序的复杂性，您可以为自定义设置一个单独的 `@Configuration` 类，也可以为每个域指定一个类。后一种方法使您可以在其中的一个测试中启用它，并在必要时使用 `@Import` 注解。

测试切片从扫描中排除了 `@Configuration` 类。例如，对于一个 `@WebMvcTest`，以下配置将在测试切片加载的应用程序上下文中不包含给定的 `WebMvcConfigurer` Bean：

```java
@Configuration
public class WebConfiguration {
    @Bean
    public WebMvcConfigurer testConfigurer() {
        return new WebMvcConfigurer() {
            ...
        };
    }
}
```

但是，以下配置将导致测试切片加载自定义的 `WebMvcConfigurer`。

```java
@Component
public class TestWebMvcConfigurer implements WebMvcConfigurer {
    ...
}
```

混乱的另一个来源是类路径扫描。假定在以合理的方式构造代码时，您需要扫描其他程序包。您的应用程序可能类似于以下代码：

```java
@SpringBootApplication
@ComponentScan({ "com.example.app", "org.acme.another" })
public class SampleApplication { ... }
```

这样做有效地覆盖了默认的组件扫描指令，并且具有扫描这两个软件包的副作用，而与您选择的切片无关。例如，一个 `@DataJpaTest` 似乎突然扫描了应用程序的组件和用户配置。同样，将自定义指令移至单独的类是解决此问题的好方法。

> 如果这不是您的选择，则可以在测试层次结构中的某个位置创建一个 `@SpringBootConfiguration`，以便使用它。或者，您可以为测试指定一个源，从而禁用查找默认源的行为。

##### 使用 Spock 测试 Spring Boot 应用

如果您希望使用 Spock 测试 Spring Boot 应用程序，则应在应用程序的构建中添加对 Spock 的 `spock-spring` 模块的依赖。`spock-spring` 将 Spring 的测试框架集成到了 Spock 中。建议您使用 Spock 1.2 或更高版本，以受益于 Spock 的 Spring Framework 和 Spring Boot 集成的许多改进。有关更多详细信息，请参见 [Spock 的 Spring 模块的文档](http://spockframework.org/spock/docs/1.2/modules.html#_spring_module)。