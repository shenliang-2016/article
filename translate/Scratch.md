##### Bean 条件

通过使用 `@ConditionalOnBean` 和 `@ConditionalOnMissingBean` 注解，可以根据是否存在特定的 bean 来包含 bean。您可以使用 `value` 属性按类型指定 bean，或使用 `name` 按名称指定 bean。使用 `search` 属性可以限制在搜索 bean 时应考虑的 `ApplicationContext` 层次结构。

当放在 `@Bean` 方法上时，目标类型默认为方法的返回类型，如以下示例所示：

```java
@Configuration(proxyBeanMethods = false)
public class MyAutoConfiguration {

    @Bean
    @ConditionalOnMissingBean
    public MyService myService() { ... }

}
```

前面的例子中， `myService` bean 将被创建，如果类型为 `MyService` 的 bean 尚未包含在 `ApplicationContext` 中时。

> 您需要非常注意添加 bean 定义的顺序，因为这些条件是根据到目前为止已处理的内容来评估的。因此，我们建议在自动配置类上仅使用 `@ConditionalOnBean` 和 `@ConditionalOnMissingBean` 注解（保证在添加任何用户定义的 Bean 定义后将加载这些注解）。

> `@ConditionalOnBean` 和 `@ConditionalOnMissingBean` 不会阻止创建 `@Configuration` 类。在类级别使用这些条件与使用注解标记每个包含的 `@Bean` 方法之间的唯一区别是，如果条件不匹配，则前者会阻止将 `@Configuration` 类注册为 bean。