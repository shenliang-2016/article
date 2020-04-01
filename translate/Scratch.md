#### 4.28.3. 条件注解

你几乎永远都希望在自动配置类中包含一个或者多个 `@Conditional` 注解。`@ConditionalOnMissingBean`  注解是一个常用的例子，用来允许开发者在某些不符合默认条件的情况下覆盖自动配置。

Spring Boot 包含大量的 `@Conditional` 注解，你可以在你的代码中注解 `@Configuration` 类或者单个的 `@Bean` 方法。这些注解包括：

- [Class 条件](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-class-conditions)
- [Bean 条件](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-bean-conditions)
- [Property 条件](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-property-conditions)
- [Resource 条件](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-resource-conditions)
- [Web Application 条件](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-web-application-conditions)
- [SpEL Expression 条件](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#boot-features-spel-conditions)

##### Class 条件

`@ConditionalOnClass` 和 `@ConditionalOnMissingClass` 注解允许根据特定类的存在或不存在来包含 `@Configuration` 类。由于注解元数据是使用 [ASM](https://asm.ow2.org/) 进行解析的，因此即使该类实际上可能不会出现在运行的应用程序类路径上，也可以使用`value`属性来引用真实的类。如果您更愿意通过使用`String`值来指定类名，那么也可以使用`name`属性。

这种机制不适用于通常使用返回类型作为条件的目标的 `@Bean` 方法：在方法的条件适用之前，JVM 将加载该类和可能经过处理的方法引用，如果该类不存在，则该方法将失败。

为了处理这种情况，可以使用一个单独的 `@Configuration` 类来隔离条件，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
// Some conditions
public class MyAutoConfiguration {

    // Auto-configured beans

    @Configuration(proxyBeanMethods = false)
    @ConditionalOnClass(EmbeddedAcmeService.class)
    static class EmbeddedConfiguration {

        @Bean
        @ConditionalOnMissingBean
        public EmbeddedAcmeService embeddedAcmeService() { ... }

    }

}
```

> 如果你使用 `@ConditionalOnClass` 或者 `@ConditionalOnMissingClass` 作为部分元注解来组成你的组合注解，你必须使用 `name` 作为这种情况下未被处理的类的引用。