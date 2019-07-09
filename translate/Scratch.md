#### 1.10.6 命名被自动探测的组件

当一个组件被自动探测为扫描过程的一部分时，它的 bean 名称由扫描器所知的`BeanNameGenerator`策略产生。默认地，包含一个名称`value`的任何 Spring 构造型注解（`@Component`, `@Repository`, `@Service`, 和 `@Controller`）则会将该名称提供给相应的 bean 定义。

如果这样的注解不包含名称`value` ，或者是通过其它方式被探测到的组件，比如被自定义过滤器发现的那些组件，默认的 bean 名称产生器将返回首字母小写的非限定类名。比如，如果下面的组件类被探测到，则其 bean 名称将分别是 `myMovieLister` 和 `movieFinderImpl` ：

```java
@Service("myMovieLister")
public class SimpleMovieLister {
    // ...
}
@Repository
public class MovieFinderImpl implements MovieFinder {
    // ...
}
```

> 如果您不想依赖默认的bean命名策略，则可以提供自定义bean命名策略。首先，实现`BeanNameGenerator`接口，并确保包含默认的无参数构造函数。然后，在配置扫描程序时提供完全限定的类名，如以下示例注解和bean定义所示：

```java
@Configuration
@ComponentScan(basePackages = "org.example", nameGenerator = MyNameGenerator.class)
public class AppConfig {
    ...
}
<beans>
    <context:component-scan base-package="org.example"
        name-generator="org.example.MyNameGenerator" />
</beans>
```

作为一般规则，考虑在其他组件可能对其进行显式引用时使用注解指定名称。另一方面，只要容器负责装配，自动生成的名称就足够了。

#### 1.10.7 为被探测到的组件提供作用域

与Spring管理的组件一样，自动检测组件的默认和最常见的作用域是单例。但是，有时您需要一个可由`@Scope`注解指定的不同作用域。您可以在注解中提供作用域的名称，如以下示例所示：

```java
@Scope("prototype")
@Repository
public class MovieFinderImpl implements MovieFinder {
    // ...
}
```

> `@Scope`注解仅在具体bean类（对于带注解的组件）或工厂方法（对于`@Bean`方法）上进行了内省。与XML bean定义相比，没有bean定义继承的概念，类级别的继承层次结构与元数据目的无关。

有关特定于Web应用的作用域范围（如Spring上下文中的“request”或“session”）的详细信息，请参阅请 [Request, Session, Application, and WebSocket Scopes](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-other) 。与这些作用域范围的预构建注解一样，您也可以使用Spring的元注解方法编写自己的作用域范围注解：例如，使用`@Scope("prototype")`进行元注解的自定义注解，可能还会声明自定义作用域代理模式。

> 要为作用域范围解析提供自定义策略而不是依赖基于注解的方法，可以实现`ScopeMetadataResolver`接口。请确保包含默认的无参数构造函数。然后，您可以在配置扫描程序时提供完全限定的类名，如以下注解和bean定义示例显示：

```java
@Configuration
@ComponentScan(basePackages = "org.example", scopeResolver = MyScopeResolver.class)
public class AppConfig {
    ...
}
```

```xml
<beans>
    <context:component-scan base-package="org.example" scope-resolver="org.example.MyScopeResolver"/>
</beans>
```

使用某些非单例作用域时，可能需要为作用域对象生成代理。这种推理在 [Scoped Beans as Dependencies](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-other-injection) 中描述。为此，component-scan元素上提供了scoped-proxy属性。三个可能的值是：`no`，`interfaces`和`targetClass`。例如，以下配置导致标准JDK动态代理：

```java
@Configuration
@ComponentScan(basePackages = "org.example", scopedProxy = ScopedProxyMode.INTERFACES)
public class AppConfig {
    ...
}
<beans>
    <context:component-scan base-package="org.example" scoped-proxy="interfaces"/>
</beans>
```

#### 1.10.8 使用注解提供限定符元数据

在 [使用限定符微调基于注解的自动装配](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-autowired-annotation-qualifiers) 中讨论了`@Qualifier`注解。该部分中的示例演示了在解析自动线候选时使用`@Qualifier`注解和自定义限定符注解来提供细粒度控制。因为这些示例基于XML bean定义，所以通过使用XML中`bean`元素的 `qualifier` 或 `meta` 子元素，在候选bean定义上提供限定符元数据。当依靠类路径扫描来自动检测组件时，可以在候选类上使用类型级注解限定符元数据。以下三个示例演示了此技术：

```java
@Component
@Qualifier("Action")
public class ActionMovieCatalog implements MovieCatalog {
    // ...
}
@Component
@Genre("Action")
public class ActionMovieCatalog implements MovieCatalog {
    // ...
}
@Component
@Offline
public class CachingMovieCatalog implements MovieCatalog {
    // ...
}
```

> 与大多数基于注解的备选方案一样，请记住注解元数据绑定到类定义本身，而XML的使用允许多个相同类型的bean在其限定符元数据中提供变体，因为元数据都是为每个实例提供而不是为每个类提供。

#### 1.10.9 生成候选组件索引

虽然类路径扫描速度非常快，但可以通过在编译时创建候选的静态列表来提高大型应用程序的启动性能。在此模式下，所有作为组件扫描目标的模块都必须使用此机制。

> 您现有的`@ComponentScan`或`<context:component-scan>`指令必须保持原样，以请求上下文扫描某些包中的候选组件。当`ApplicationContext`检测到这样的索引时，它会自动使用它而不是扫描类路径。

要生成索引，请为包含组件扫描指令目标的组件的每个模块添加附加依赖项。以下示例显示了如何使用Maven执行此操作：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context-indexer</artifactId>
        <version>5.1.8.RELEASE</version>
        <optional>true</optional>
    </dependency>
</dependencies>
```

使用Gradle 4.5及更早版本时，应在`compileOnly`配置中声明依赖项，如以下示例所示：

```xml
dependencies {
    compileOnly "org.springframework:spring-context-indexer:5.1.8.RELEASE"
}
```

使用Gradle 4.6及更高版本时，应在`annotationProcessor`配置中声明依赖项，如以下示例所示：

```xml
dependencies {
    annotationProcessor "org.springframework:spring-context-indexer:5.1.8.RELEASE"
}
```

该过程生成包含在jar文件中的 `META-INF/spring.components` 文件。

> 在IDE中使用此模式时，必须将`spring-context-indexer`注册为注解处理器，以确保在更新候选组件时索引是最新的。

> 在类路径上找到 `META-INF/spring.components` 时，将自动启用索引。如果索引部分可用于某些库（或用例）但不能为整个应用程序构建，则可以通过将`spring.index.ignore`设置为`true`而回退到常规类路径扫描配置（就好像根本没有索引），无论是作为系统属性还是在类路径根目录下的`spring.properties`文件中。

