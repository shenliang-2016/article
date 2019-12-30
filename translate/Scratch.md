### 3.3. 配置类

Spring 更喜欢基于 Java 的配置。尽管通过 XML 源文件使用 `SpringApplication` 也是可能的，我们还是推荐你将主要的配置源写成一个单独的 `@Configuration` 类。通常，定义 `main` 方法的类就是这个主 `@Configuration` 的理想选择。

> 许多已经发布到网上的 Spring 配置示例都使用了 XML 配置。如果可能，请始终使用等效的基于 Java 的配置。搜索 `Enable*` 注解将是一个很好的切入点。

#### 3.3.1. 引入额外的配置类

你不需要将所有的 `@Configuration` 都放在同一个类里。`@Import` 注解可以被用来引入另外的配置类。此外，你可以使用 `@ComponentScen` 自动获取所有的 Spring 组件，包括 `@Configuration` 类。

#### 3.3.2. 引入 XML 配置

如果你必须使用基于 XML 的配置，我们推荐你仍然从 `@Configuration` 类开始。你可以在其中使用 `@ImportResource` 注解加载 XML 配置文件。

### 3.4. Auto-configuration

Spring Boot auto-configuration attempts to automatically configure your Spring application based on the jar dependencies that you have added. For example, if `HSQLDB` is on your classpath, and you have not manually configured any database connection beans, then Spring Boot auto-configures an in-memory database.

You need to opt-in to auto-configuration by adding the `@EnableAutoConfiguration` or `@SpringBootApplication` annotations to one of your `@Configuration` classes.

> You should only ever add one `@SpringBootApplication` or `@EnableAutoConfiguration` annotation. We generally recommend that you add one or the other to your primary `@Configuration` class only.

#### 3.4.1. Gradually Replacing Auto-configuration

Auto-configuration is non-invasive. At any point, you can start to define your own configuration to replace specific parts of the auto-configuration. For example, if you add your own `DataSource` bean, the default embedded database support backs away.

If you need to find out what auto-configuration is currently being applied, and why, start your application with the `--debug` switch. Doing so enables debug logs for a selection of core loggers and logs a conditions report to the console.

#### 3.4.2. Disabling Specific Auto-configuration Classes

If you find that specific auto-configuration classes that you do not want are being applied, you can use the exclude attribute of `@EnableAutoConfiguration` to disable them, as shown in the following example:

```java
import org.springframework.boot.autoconfigure.*;
import org.springframework.boot.autoconfigure.jdbc.*;
import org.springframework.context.annotation.*;

@Configuration(proxyBeanMethods = false)
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
public class MyConfiguration {
}
```

If the class is not on the classpath, you can use the `excludeName` attribute of the annotation and specify the fully qualified name instead. Finally, you can also control the list of auto-configuration classes to exclude by using the `spring.autoconfigure.exclude` property.

> You can define exclusions both at the annotation level and by using the property.

> Even though auto-configuration classes are `public`, the only aspect of the class that is considered public API is the name of the class which can be used for disabling the auto-configuration. The actual contents of those classes, such as nested configuration classes or bean methods are for internal use only and we do not recommend using those directly.