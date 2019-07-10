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

> Full @Configuration vs “lite” @Bean mode?
>
> When `@Bean` methods are declared within classes that are not annotated with `@Configuration`, they are referred to as being processed in a “lite” mode. Bean methods declared in a `@Component` or even in a plain old class are considered to be “lite”, with a different primary purpose of the containing class and a `@Bean` method being a sort of bonus there. For example, service components may expose management views to the container through an additional `@Bean` method on each applicable component class. In such scenarios, `@Bean` methods are a general-purpose factory method mechanism.
>
> Unlike full `@Configuration`, lite `@Bean` methods cannot declare inter-bean dependencies. Instead, they operate on their containing component’s internal state and, optionally, on arguments that they may declare. Such a `@Bean` method should therefore not invoke other `@Bean` methods. Each such method is literally only a factory method for a particular bean reference, without any special runtime semantics. The positive side-effect here is that no CGLIB subclassing has to be applied at runtime, so there are no limitations in terms of class design (that is, the containing class may be `final` and so forth).
>
> In common scenarios, `@Bean` methods are to be declared within `@Configuration` classes, ensuring that “full” mode is always used and that cross-method references therefore get redirected to the container’s lifecycle management. This prevents the same `@Bean` method from accidentally being invoked through a regular Java call, which helps to reduce subtle bugs that can be hard to track down when operating in “lite” mode.

The `@Bean` and `@Configuration` annotations are discussed in depth in the following sections. First, however, we cover the various ways of creating a spring container using by Java-based configuration.