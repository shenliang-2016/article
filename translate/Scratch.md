### 3.3. 配置类

Spring 更喜欢基于 Java 的配置。尽管通过 XML 源文件使用 `SpringApplication` 也是可能的，我们还是推荐你将主要的配置源写成一个单独的 `@Configuration` 类。通常，定义 `main` 方法的类就是这个主 `@Configuration` 的理想选择。

> 许多已经发布到网上的 Spring 配置示例都使用了 XML 配置。如果可能，请始终使用等效的基于 Java 的配置。搜索 `Enable*` 注解将是一个很好的切入点。

#### 3.3.1. 引入额外的配置类

你不需要将所有的 `@Configuration` 都放在同一个类里。`@Import` 注解可以被用来引入另外的配置类。此外，你可以使用 `@ComponentScen` 自动获取所有的 Spring 组件，包括 `@Configuration` 类。

#### 3.3.2. 引入 XML 配置

如果你必须使用基于 XML 的配置，我们推荐你仍然从 `@Configuration` 类开始。你可以在其中使用 `@ImportResource` 注解加载 XML 配置文件。

### 3.4. 自动配置

Spring Boot 自动配置试图基于你已经添加的 jar 依赖自动配置你的 Spring 应用。比如，如果 `HSQLDB` 在你的类路径上，而你并没有手动配置任何数据库连接 beans ，则 Spring Boot 就会自动配置一个内存数据库。

你需要通过将 `@EnableAutoConfiguration` 或者 `@SpringBootApplication` 注解添加到其中一个你的 `@Configuration` 类中来选择加入自动配置。

> 您应该只添加一个 `@SpringBootApplication` 或 `@EnableAutoConfiguration` 注解。我们通常建议您仅将其中一个添加到您的主要 `@Configuration` 类中。

#### 3.4.1. 逐步替换自动配置

自动配置是非侵入性的。在任何时候，您都可以开始定义自己的配置，以替换自动配置的特定部分。例如，如果您添加自己的 `DataSource` bean，则默认的内置数据库支持将退出。

如果您需要找出当前正在应用的自动配置以及原因，请使用 `--debug` 开关参数启动您的应用程序。这样做可以启用调试日志以供选择核心记录器，并将条件报告记录到控制台。

#### 3.4.2. 禁用特定的自动配置类

如果你发现不想某个特定的自动配置类被应用，你可以使用 `@EnableAutoConfiguration` 注解的 `exclude` 属性来禁用它。如下面例子所示：

```java
import org.springframework.boot.autoconfigure.*;
import org.springframework.boot.autoconfigure.jdbc.*;
import org.springframework.context.annotation.*;

@Configuration(proxyBeanMethods = false)
@EnableAutoConfiguration(exclude={DataSourceAutoConfiguration.class})
public class MyConfiguration {
}
```

如果类不在类路径下，你可以使用注解的 `excludeName` 属性并指定全限定名。你也可以通过使用 `spring.autoconfigure.exclude` 属性控制需要禁用的自动配置类列表。

> 您可以在注解级别和使用属性来定义排除项。

> 即使自动配置类是 `public` 的，该类的唯一被认为是公共 API 的方面是可用于禁用自动配置的类的名称。这些类的实际内容（例如嵌套配置类或 bean 方法）仅供内部使用，我们不建议直接使用它们。

