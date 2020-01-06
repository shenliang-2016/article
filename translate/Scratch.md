##### @ConfigurationProperties 验证

每当使用 Spring 的 `@Validated` 注解进行注释时，Spring Boot 就会尝试验证 `@ConfigurationProperties` 类。您可以在配置类上直接使用 JSR-303 `javax.validation` 约束注解。为此，请确保在类路径上有兼容的 JSR-303 实现，然后将约束注解添加到字段中，如以下示例所示：

```java
@ConfigurationProperties(prefix="acme")
@Validated
public class AcmeProperties {

    @NotNull
    private InetAddress remoteAddress;

    // ... getters and setters

}
```

> 您也可以通过用 `@Validated` 注解创建配置属性的 `@Bean` 方法来触发验证。

为了确保始终为嵌套属性触发验证，即使没有找到属性，相关字段也必须使用 `@Valid` 注解修饰。以下示例以前面的 `AcmeProperties` 示例为基础：

```java
@ConfigurationProperties(prefix="acme")
@Validated
public class AcmeProperties {

    @NotNull
    private InetAddress remoteAddress;

    @Valid
    private final Security security = new Security();

    // ... getters and setters

    public static class Security {

        @NotEmpty
        public String username;

        // ... getters and setters

    }

}
```

您也可以通过创建一个名为 `configurationPropertiesValidator` 的 bean 定义来添加一个自定义的 Spring Validator。`@Bean` 方法应该声明为 `static`。配置属性验证器是在应用程序生命周期的早期创建的，并且将 `@Bean` 方法声明为静态方法可以创建 Bean，而不必实例化 `@Configuration` 类。这样做避免了由早期实例化引起的任何问题。

> `spring-boot-actuator` 模块包括一个端点，该端点公开了所有的 `@ConfigurationProperties` bean。将您的 Web 浏览器指向 `/actuator/configprops` 或使用等效的 JMX 端点。有关详细信息，请参见 [Production ready features](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-endpoints) 部分。

##### @ConfigurationProperties vs. @Value

`@Value` 注解是核心容器功能，它没有提供与类型安全的配置属性相同的功能。下表总结了 `@ConfigurationProperties` 和 `@Value` 支持的功能：

| Feature                                                      | `@ConfigurationProperties` | `@Value` |
| :----------------------------------------------------------- | :------------------------- | :------- |
| [Relaxed binding](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-relaxed-binding) | Yes                        | No       |
| [Meta-data support](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#configuration-metadata) | Yes                        | No       |
| `SpEL` evaluation                                            | No                         | Yes      |

如果您为自己的组件定义了一组配置键，我们建议您将它们组合在一个以 `@ConfigurationProperties` 注解修饰的 POJO 中。您还应该意识到，由于 `@Value` 不支持宽松的绑定，因此如果您需要通过使用环境变量来提供值，则不是一个好的选择。

最后，尽管你能够在 `@Value` 中编写 `SpEL` 表达式，但不会处理来自 [application property files](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-external-config-application-property-files)  的此类表达式。

