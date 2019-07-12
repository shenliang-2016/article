#### 1.12.5 构造基于 Java 的配置

Spring 基于 Java 的配置特性使得你可以组合注解，那样做可以降低你的配置的复杂度。

##### 使用 `@Import` 注解

就像在Spring XML文件中使用 `<import/>` 元素来帮助模块化配置一样，`@Import`注解允许从另一个配置类加载`@Bean`定义，如下例所示：

```java
@Configuration
public class ConfigA {

    @Bean
    public A a() {
        return new A();
    }
}

@Configuration
@Import(ConfigA.class)
public class ConfigB {

    @Bean
    public B b() {
        return new B();
    }
}
```

现在，在实例化上下文时，不需要同时指定`ConfigA.class`和`ConfigB.class`，只需显式提供`ConfigBneeds`，如下例所示：

```java
public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(ConfigB.class);

    // now both beans A and B will be available...
    A a = ctx.getBean(A.class);
    B b = ctx.getBean(B.class);
}
```

这种方法简化了容器实例化，只需要使用一个类，而不需要你在构造过程中记忆可能存在的大量`@Configuration`类。

> 从Spring Framework 4.2开始，`@Import`还支持引用常规组件类，类似于`AnnotationConfigApplicationContext.register`方法。如果要避免组件扫描，这一点特别有用，可以使用一些配置类作为明确定义所有组件的入口点。

###### Injecting Dependencies on Imported `@Bean` Definitions

前面简化的例子可以工作。在大多数实际场景中，beans 会依赖其它跨配置类的 bean。在使用 XML 配置文件时，这不是问题，因为这不涉及编译器，同时你可以声明`ref="someBean"`并相信 Spring 在容器初始化过程中解析它。当使用`@Configuration`类时，编译器会在配置模型上施加约束，此时对其它 beans 的引用必须是合法的 Java 语法。

幸运的是，解决这个问题其实很简单。如我们已经讨论过的，`@Bean` 方法可以拥有任意多个参数来描述 bean 依赖。考虑下面这个更接近现实的场景，其中包含多个`@Configuration`类，它们相互依赖对方声明的 beans ：

```java
@Configuration
public class ServiceConfig {

    @Bean
    public TransferService transferService(AccountRepository accountRepository) {
        return new TransferServiceImpl(accountRepository);
    }
}

@Configuration
public class RepositoryConfig {

    @Bean
    public AccountRepository accountRepository(DataSource dataSource) {
        return new JdbcAccountRepository(dataSource);
    }
}

@Configuration
@Import({ServiceConfig.class, RepositoryConfig.class})
public class SystemTestConfig {

    @Bean
    public DataSource dataSource() {
        // return new DataSource
    }
}

public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(SystemTestConfig.class);
    // everything wires up across configuration classes...
    TransferService transferService = ctx.getBean(TransferService.class);
    transferService.transfer(100.00, "A123", "C456");
}
```

还有另外一种方法可以得到同样的效果。其实`@Configuration`类说到底也只是容器中的另一种 bean，这就意味着它们也可以像任何其它 bean 一样享受`@Autowired`和`@Value`注入和其它特性的好处。

> 确保以这种方式注入的依赖项只是最简单的类型。`@Configuration`类在上下文初始化期间很早就被处理，并且强制以这种方式注入依赖项可能导致意外的早期初始化。尽可能采用基于参数的注入，如前面的示例所示。
>
> 另外，需要特别注意通过`@Bean`对`BeanPostProcessor`和`BeanFactoryPostProcessor`的定义。这些通常应该声明为静态`@Bean`方法，而不是触发包含它们的配置类的实例化。否则，`@Autowired`和`@Value`不能在配置类本身上工作，因为它过早地被创建为bean实例。

以下示例显示了如何将一个bean自动装配到另一个bean：

```java
@Configuration
public class ServiceConfig {

    @Autowired
    private AccountRepository accountRepository;

    @Bean
    public TransferService transferService() {
        return new TransferServiceImpl(accountRepository);
    }
}

@Configuration
public class RepositoryConfig {

    private final DataSource dataSource;

    @Autowired
    public RepositoryConfig(DataSource dataSource) {
        this.dataSource = dataSource;
    }

    @Bean
    public AccountRepository accountRepository() {
        return new JdbcAccountRepository(dataSource);
    }
}

@Configuration
@Import({ServiceConfig.class, RepositoryConfig.class})
public class SystemTestConfig {

    @Bean
    public DataSource dataSource() {
        // return new DataSource
    }
}

public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(SystemTestConfig.class);
    // everything wires up across configuration classes...
    TransferService transferService = ctx.getBean(TransferService.class);
    transferService.transfer(100.00, "A123", "C456");
}
```

> 仅在Spring Framework 4.3中支持`@Configuration`类中的构造函数注入。另请注意，如果目标bean仅定义了一个构造函数，则无需指定`@Autowired`。在前面的示例中，`RepositoryConfig`构造函数中不需要`@Autowired`。

**完全限定导入 beans 以便于导航**

在前面的场景中，使用`@Autowired`可以很好地工作并提供所需的模块化，但确定声明自动装配的bean定义的确切位置仍然有些模棱两可。例如，作为一名查看`ServiceConfig`的开发人员，您如何确切地知道`@Autowired`的 `AccountRepository ` bean的声明位置？ 它在代码中并不明确，不过可能还好。请记住， [Spring Tool Suite](https://spring.io/tools/sts) 提供的工具可以呈现图形，显示所有内容的连线方式，这可能就是您所需要的。此外，您的Java IDE可以轻松找到`AccountRepository`类型的所有声明和用法，并快速显示返回该类型的`@Bean`方法的位置。

如果这种歧义不可接受并且您希望在IDE中从一个`@Configuration`类直接导航到另一个`@Configuration`类，请考虑自行装配配置类本身。以下示例显示了如何执行此操作：

```java
@Configuration
public class ServiceConfig {

    @Autowired
    private RepositoryConfig repositoryConfig;

    @Bean
    public TransferService transferService() {
        // navigate 'through' the config class to the @Bean method!
        return new TransferServiceImpl(repositoryConfig.accountRepository());
    }
}
```

在前面的情况中，定义`AccountRepository`是完全明确的。但是，`ServiceConfig`现在与`RepositoryConfig`紧密耦合。这是一种权衡的结果。通过使用基于接口的或基于类的抽象`@Configuration`类，可以在某种程度上减轻这种紧密耦合。请考虑以下示例：

```java
@Configuration
public class ServiceConfig {

    @Autowired
    private RepositoryConfig repositoryConfig;

    @Bean
    public TransferService transferService() {
        return new TransferServiceImpl(repositoryConfig.accountRepository());
    }
}

@Configuration
public interface RepositoryConfig {

    @Bean
    AccountRepository accountRepository();
}

@Configuration
public class DefaultRepositoryConfig implements RepositoryConfig {

    @Bean
    public AccountRepository accountRepository() {
        return new JdbcAccountRepository(...);
    }
}

@Configuration
@Import({ServiceConfig.class, DefaultRepositoryConfig.class})  // import the concrete config!
public class SystemTestConfig {

    @Bean
    public DataSource dataSource() {
        // return DataSource
    }

}

public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(SystemTestConfig.class);
    TransferService transferService = ctx.getBean(TransferService.class);
    transferService.transfer(100.00, "A123", "C456");
}
```

现在，`ServiceConfig`与具体的`DefaultRepositoryConfig`松散耦合，内置的IDE工具仍然很有用：您可以轻松获得`RepositoryConfig`实现的类型层次结构。通过这种方式，导航`@Configurationclasses`及其依赖项与导航基于接口的代码的常规过程没有什么不同。

> 如果要影响某些bean的启动创建顺序，请考虑将其中一些声明为`@Lazy`（用于在首次访问时创建而不是在启动时）或`@DependsOn`某些其他bean（确保在创建当前的bean之前创建特定的其他bean，超出两者的直接依赖性所暗示的）。

##### 有条件地包含`@Configuration`类或`@Bean`方法

基于某些任意系统状态，有条件地启用或禁用整个的`@Configuration`类甚至单个`@Bean`方法通常很有用。一个常见的例子是，只有在Spring `Environment` 中启用了特定的配置文件时才使用`@Profile`注解来激活bean（有关详细信息，请参阅[Bean定义配置文件](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-definition-profiles) ）。

`@Profile`注解实际上是通过使用更灵活的注解 [`@Conditional`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/context/annotation/Conditional.html) 实现的。`@Conditional`注解表示在注册`@Bean`之前应该参考的特定`org.springframework.context.annotation.Condition`实现。

`Condition`接口的实现提供了一个返回`true`或`false`的`matches(...)`方法。例如，以下列表显示了用于`@Profile`的实际`Condition`实现：

```java
@Override
public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
    if (context.getEnvironment() != null) {
        // Read the @Profile annotation attributes
        MultiValueMap<String, Object> attrs = metadata.getAllAnnotationAttributes(Profile.class.getName());
        if (attrs != null) {
            for (Object value : attrs.get("value")) {
                if (context.getEnvironment().acceptsProfiles(((String[]) value))) {
                    return true;
                }
            }
            return false;
        }
    }
    return true;
}
```

参考 [`@Conditional`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/context/annotation/Conditional.html) 文档获取更多细节。

##### 结合 Java 和 XML 配置

Spring的`@Configuration`类支持并非旨在成为Spring XML的100％完全替代品。某些工具，如Spring XML命名空间，仍然是配置容器的理想方法。在XML方便或必要的情况下，您可以选择：使用例如`ClassPathXmlApplicationContext`以“以XML为中心”的方式实例化容器，或者使用`AnnotationConfigApplicationContext`，并使用`@ImportResource`注解，根据需要导入XML，以“以Java为中心”的方式实例化它。

###### 以XML为中心使用`@Configuration`类

最好从XML引导Spring容器，并以ad-hoc方式包含`@Configuration`类。例如，在使用Spring XML的大型现有代码库中，可以根据需要更轻松地创建`@Configuration`类，并将其包含在现有XML文件中。在本节的后面部分，我们将介绍在这种“以XML为中心”的情况下使用`@Configuration`类的选项。

将`@Configuration`类声明为普通的Spring `<bean/>`元素

请记住，`@Configuration`类是容器中最终的bean定义。在本系列示例中，我们创建一个名为`AppConfig`的`@Configuration`类，并将其作为`<bean/>`定义包含在`system-test-config.xml`中。由于`<context:annotation-config/>`已打开，容器会识别`@Configuration`注解并正确处理`AppConfig`中声明的`@Bean`方法。

以下示例显示了Java中的普通配置类：

```java
@Configuration
public class AppConfig {

    @Autowired
    private DataSource dataSource;

    @Bean
    public AccountRepository accountRepository() {
        return new JdbcAccountRepository(dataSource);
    }

    @Bean
    public TransferService transferService() {
        return new TransferService(accountRepository());
    }
}
```

以下示例显示了示例`system-test-config.xml`文件的一部分：

```xml
<beans>
    <!-- enable processing of annotations such as @Autowired and @Configuration -->
    <context:annotation-config/>
    <context:property-placeholder location="classpath:/com/acme/jdbc.properties"/>

    <bean class="com.acme.AppConfig"/>

    <bean class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>
</beans>
```

以下示例显示了可能的`jdbc.properties`文件：

```
jdbc.url=jdbc:hsqldb:hsql://localhost/xdb
jdbc.username=sa
jdbc.password=
```

```java
public static void main(String[] args) {
    ApplicationContext ctx = new ClassPathXmlApplicationContext("classpath:/com/acme/system-test-config.xml");
    TransferService transferService = ctx.getBean(TransferService.class);
    // ...
}
```

> 在`system-test-config.xml`文件中，`AppConfig` `<bean/>`不声明id元素。虽然这样做是可以接受的，但是没有必要，因为没有其他bean引用它，并且不太可能通过名称从容器中明确地获取它。类似地，`DataSource` bean只是按类型自动装配，因此不严格要求显式的bean id。

使用 <context:component-scan/> 获取 `@Configuration` 类

因为`@Configuration`是使用`@Component`进行元注解的，所以`@Configuration`注解类自动成为组件扫描的候选者。使用与前一个示例中描述的相同的方案，我们可以重新定义`system-test-config.xml`以利用组件扫描。请注意，在这种情况下，我们不需要显式声明`<context:annotation-config/>`，因为`<context:annotation-config/>`启用相同的功能。

以下示例显示了已修改的`system-test-config.xml`文件：

```xml
<beans>
    <!-- picks up and registers AppConfig as a bean definition -->
    <context:component-scan base-package="com.acme"/>
    <context:property-placeholder location="classpath:/com/acme/jdbc.properties"/>

    <bean class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>
</beans>
```

###### `@Configuration` 类为中心使用 XML 和 `@ImportResource`

在`@Configuration`类是配置容器的主要机制的应用程序中，仍然可能需要使用一些XML。在这些场景中，您可以使用`@ImportResource`并根据需要定义尽可能多的XML。这样做可以实现“以Java为中心”的方法来配置容器并将XML保持在最低限度。以下示例（包括配置类，定义bean的XML文件，属性文件和`main`类）显示了如何使用`@ImportResource`注解来实现根据需要使用XML的“以Java为中心”的配置：

```java
@Configuration
@ImportResource("classpath:/com/acme/properties-config.xml")
public class AppConfig {

    @Value("${jdbc.url}")
    private String url;

    @Value("${jdbc.username}")
    private String username;

    @Value("${jdbc.password}")
    private String password;

    @Bean
    public DataSource dataSource() {
        return new DriverManagerDataSource(url, username, password);
    }
}
```

```xml
properties-config.xml
<beans>
    <context:property-placeholder location="classpath:/com/acme/jdbc.properties"/>
</beans>
```
````
jdbc.properties
jdbc.url=jdbc:hsqldb:hsql://localhost/xdb
jdbc.username=sa
jdbc.password=
````

````java
public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(AppConfig.class);
    TransferService transferService = ctx.getBean(TransferService.class);
    // ...
}
````

