### 4.3. Profiles

Spring Profiles 提供了隔离你的应用的配置部分并使得它们只在特定环境下可用的方法。所有的 `@Component` ，`@Configuration` ，或者 `@ConfigurationProperties` 都能够使用 `@Profile` 标记以限制它们何时加载。如下面例子所示：

```java
@Configuration(proxyBeanMethods = false)
@Profile("production")
public class ProductionConfiguration {

    // ...

}
```

> 如果通过 `@EnableConfigurationProperties` 注册了 `@ConfigurationProperties` bean而不是通过自动扫描进行注册，则需要在具有 `@EnableConfigurationProperties` 注解的 `@Configuration` 类上指定 `@Profile` 注解。在扫描 `@ConfigurationProperties` 的情况下，可以在 `@ConfigurationProperties` 类本身上指定 `@ Profile`。

您可以使用 `spring.profiles.active` 环境属性来指定哪些配置文件处于活动状态。您可以通过本章前面介绍的任何方式指定属性。例如，您可以将其包含在 `application.properties` 中，如以下示例所示：

```properties
spring.profiles.active=dev,hsqldb
```

你也可以在命令行中指定它，通过使用开关： `--spring.profiles.active=dev,hsqldb`。

