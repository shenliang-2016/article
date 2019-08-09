为了使其工作，被注解修饰的类型必须使用 AspectJ 织入器织入。你可以在构建期使用 Ant 或者 Maven 任务来实现这一操作（参考  [AspectJ Development Environment Guide](https://www.eclipse.org/aspectj/doc/released/devguide/antTasks.html)），或者进行加载期织入（参考 [Load-time Weaving with AspectJ in the Spring Framework](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-aj-ltw)）。`AnnotationBeanConfigurerAspect`自身许哟啊通过 Spring 配置（为了获得一个将被用来配置新对象的 bean 工厂的引用）。如果你使用基于 Java 的配置，你可以在任意`@Configuration`类上添加`@EnableSpringConfigured`，如下所示：

```java
@Configuration
@EnableSpringConfigured
public class AppConfig {
}
```

如果你更喜欢基于 XML 的配置，Spring  [`context` namespace](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#xsd-schemas-context) 定义了一个方便的`context:spring-configured`元素，你可以如下使用：

```xml
<context:spring-configured/>
```

在配置切面之前创建的`@Configurable`对象的实例会导致向调试日志发出消息，并且不会发生对象的配置。一个示例可能是 Spring 配置中的 bean，它在 Spring 初始化时创建域对象。在这种情况下，您可以使用`depends-on` bean 属性手动指定 bean 依赖于配置切面。以下示例显示了如何使用`depends-on`属性：

```xml
<bean id="myService"
        class="com.xzy.myapp.service.MyService"
        depends-on="org.springframework.beans.factory.aspectj.AnnotationBeanConfigurerAspect">

    <!-- ... -->

</bean>
```

> 不要通过 bean 配置器切面激活`@Configurable`处理，除非你真的想在运行时依赖它的语义。特别是，请确保不要对使用容器注册为常规 Spring bean 的 bean 类使用`@Configurable`。这样做会导致双重初始化，一次通过容器，一次通过切面。

##### 单元测试 `@Configurable` 对象

`@Configurable`支持的目标之一是启用域对象的独立单元测试，而不会遇到与硬编码查找相关的困难。如果 AspectJ 没有织入`@Configurable`类型，则注解在单元测试期间没有影响。您可以在测试对象中设置模拟或存根属性引用，并当作真实对象进行逻辑处理。如果 AspectJ 织入了`@Configurable`类型，您仍然可以正常地在容器外部进行单元测试，但每次构造一个`@Configurable`对象时都会看到一条警告消息，表明它尚未由`Spring`配置。

##### 使用多个应用上下文

用于实现`@Configurable`支持的`AnnotationBeanConfigurerAspect`是 AspectJ 单例切面。单例切面的作用域范围与`static`成员的范围相同：每个类加载器都有一个切面实例来定义类型。这意味着，如果在同一个类加载器层次结构中定义多个应用程序上下文，则需要考虑在哪里定义`@EnableSpringConfigured` bean以及在类路径上放置`spring-aspects.jar`的位置。

考虑一个典型的 Spring Web 应用程序配置，它具有共享的父应用程序上下文，它定义了公共业务服务，支持这些服务所需的一切，以及每个 servlet 的一个子应用程序上下文（包含特定于该 servlet 的定义）。所有这些上下文共存于同一个类加载器层次结构中，因此`AnnotationBeanConfigurerAspect`只能包含对其中一个的引用。在这种情况下，我们建议在共享（父）应用程序上下文中定义`@EnableSpringConfigured` bean。这定义了您可能希望注入域对象的服务。结果是，您无法使用`@Configurable`机制（可能不是您想要执行的操作）来配置域对象，并引用对子（特定于 servlet）上下文中定义的 bean 的引用。

在同一容器中部署多个 Web 应用程序时，请确保每个 Web 应用程序使用自己的类加载器加载`spring-aspects.jar`中的类型（例如，将`spring-aspects.jar`放在`WEB-INF/lib`中）。如果`spring-aspects.jar`仅添加到容器范围的类路径中（因此由共享父类加载器加载），则所有 Web 应用程序共享相同的切面实例（可能不是您想要的）。

#### 5.10.2 AspectJ 的其它 Spring 切面 

除了`@Configurable`切面，`spring-aspects.jar`还包含一个 AspectJ 方面，您可以使用它来为使用`@Transactional`注解修饰的类型和方法驱动 Spring 的事务管理。这主要适用于希望在 Spring 容器之外使用 Spring Framework 的事务支持的用户。

解释`@Transactional`注解的切面是`AnnotationTransactionAspect`。使用此切面时，必须注解实现类（或该类中的方法或两者），而不是类实现的接口（如果有）。AspectJ 遵循 Java 的规则，即接口上的注解不会被继承。

类上的`@Transactional`注解指定了在类中执行任何公共操作的默认事务语义。

类中方法的`@Transactional`注解会覆盖类注解（如果存在）给出的默认事务语义。可以注解任何可见性的方法，包括私有方法。 直接注解非公共方法是获得执行此类方法的事务划分的唯一方法。

> 从 Spring Framework 4.2 开始， `spring-aspects` 提供了一个类似的切面来为标准 `javax.transaction.Transactional` 注解提供完全相同的功能特性。检查 `JtaAnnotationTransactionAspect` 获取更多细节。

对于想要使用 Spring 配置和事务管理支持但不想（或不能）使用注解的 AspectJ 程序员，`spring-aspects.jar`还包含你可以扩展以提供自己的切入点定义的`abstract`切面。有关更多信息，请参阅`AbstractBeanConfigurerAspect`和`AbstractTransactionAspect`方面的源代码。作为示例，以下代码片段显示了如何编写切面来配置域模型中定义的所有对象实例，方法是使用与完全限定类名匹配的原型 bean 定义：

```java
public aspect DomainObjectConfiguration extends AbstractBeanConfigurerAspect {

    public DomainObjectConfiguration() {
        setBeanWiringInfoResolver(new ClassNameBeanWiringInfoResolver());
    }

    // the creation of a new bean (any object in the domain model)
    protected pointcut beanCreation(Object beanInstance) :
        initialization(new(..)) &&
        SystemArchitecture.inDomainModel() &&
        this(beanInstance);
}
```

