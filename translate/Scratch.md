### 1.12 基于 Java 类的容器配置

本章节介绍如何在你的 Java 代码中使用注解来配置 Spring 容器。包含以下主题：

- [基本概念: `@Bean` 和 `@Configuration`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java-basic-concepts)
- [使用 `AnnotationConfigApplicationContext`实例化 Spring 容器](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java-instantiating-container)
- [使用 `@Bean` 注解](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java-bean-annotation)
- [使用 `@Configuration` 注解](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java-configuration-annotation)
- [构造基于 Java 类的配置](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java-composing-configuration-classes)
- [Bean 定义配置](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-definition-profiles)
- [`PropertySource` 抽象](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-property-source-abstraction)
- [使用 `@PropertySource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-using-propertysource)
- [语句中的占位符解析](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-placeholder-resolution-in-statements)

#### 1.12.1 基本概念：`@Bean` 和 `@Configuration`

Spring 的新 Java 配置支持机制的核心是`@Configuration`注解修饰的类和`@Bean`注解修饰的方法。

`@Bean`注解用于指示一个方法实例化，配置和初始化由Spring IoC容器管理的新对象。对于那些熟悉Spring的`<beans/>` XML配置的人来说，`@Bean`注解扮演的角色与`<bean/>`元素相同。您可以将`@Bean`注解修饰的方法与任何Spring `@Component`一起使用。但是，它们最常用于`@Configuration`bean 中。

使用`@Configuration`注释类表示其主要目的是作为bean定义的源。此外，`@Configuration`类允许通过调用同一个类中的其他`@Bean`方法来定义bean间依赖关系。最简单的`@Configuration`类如下所示：

```java
@Configuration
public class AppConfig {

    @Bean
    public MyService myService() {
        return new MyServiceImpl();
    }
}
```

前面的`AppConfig`类等效于以下Spring `<beans/>` XML：

```xml
<beans>
    <bean id="myService" class="com.acme.services.MyServiceImpl"/>
</beans>
```

> 完整的`@Configuration` VS “精简的” `@Bean`模式？
>
> 当`@Bean`方法在未使用`@Configuration`注解修饰的类中声明时，它们被称为以“精简”模式处理。在`@Component`或甚至普通旧类中声明的Bean方法被认为是“精简的”，包含类的主要目的不同，而`@Bean`方法在那里更像是是一种奖励。例如，服务组件可以通过每个适用的组件类上的附加`@Bean`方法将管理视图公开给容器。在这种情况下，`@Bean`方法是一种通用的工厂方法机制。
>
> 与完整的`@Configuration`不同，精简的`@Bean`方法不能声明bean间依赖关系。相反，它们对其包含组件的内部状态进行操作，并且可选地，对它们可以声明的参数进行操作。因此，这样的`@Bean`方法不应该调用其他`@Bean`方法。每个这样的方法实际上只是特定bean引用的工厂方法，没有任何特殊的运行时语义。这里所谓的积极副作用是不必在运行时应用CGLIB子类，因此在类设计方面没有限制（即，包含类可能是`final`的，等等）。
>
> 在常见的场景中，`@Bean`方法将在`@Configuration`类中声明，确保始终使用“完整”模式，并因此将交叉方法引用重定向到容器的生命周期管理。这可以防止通过常规Java调用意外地调用相同的`@Bean`方法，这有助于减少在“精简”模式下操作时难以跟踪的细微错误。

The `@Bean` and `@Configuration` annotations are discussed in depth in the following sections. First, however, we cover the various ways of creating a spring container using by Java-based configuration.

`@Bean`和`@Configuration`注解将在以下部分中进行深入讨论。首先，我们将介绍使用基于Java的配置创建 Spring 容器的各种方法。

