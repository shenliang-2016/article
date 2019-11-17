#### 1.4.9. 通过 AspectJ 使用 `@Transactional` 

你也可以在 Spring 容器之外通过 AspectJ 切面来使用 Spring 框架的 `@Transactional` 支持。为了做到这一点，首先用 `@Transactional` 注解修饰你的类（并选择性修饰该类的方法），然后将你的应用链接 (编织) 到定义在 `spring-aspects.jar` 文件中的 `org.springframework.transaction.aspectJ.AnnotationTransactionAspect` 。你必须同时为该切面配置事务管理器。你可以使用 Spring 框架的 IoC 容器进行切面的依赖注入。配置事务管理切面的最简单方式就是使用 `<tx:annotation-driven/>` 元素并指定 `aspectJ` 的 `mode` 属性，如 [Using `@Transactional`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative-annotations) 中所述。由于我们这里关注的是在 Spring 容器之外运行的应用，我们向你展示如何通过编程方式做到这一点。

> 继续之前，你可能希望阅读 [Using `@Transactional`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative-annotations) 和 [AOP](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop) 。

下面的例子展示了如何创建事务管理器并配置 `AnnotationTransactionAspect` 来使用它：

```java
// construct an appropriate transaction manager
DataSourceTransactionManager txManager = new DataSourceTransactionManager(getDataSource());

// configure the AnnotationTransactionAspect to use it; this must be done before executing any transactional methods
AnnotationTransactionAspect.aspectOf().setTransactionManager(txManager);
```

> 当你使用该切面时，你必须用注解修饰实现类 (或者实现类的方法) ，而不是修饰该类实现的接口 (如果存在)。AspectJ 遵循 Java 语言的规则，接口上的注解是不会被继承的。

类上的 `@Transactional` 注解指定了类中所有 public 方法执行的默认事务语义。

类中方法上的 `@Transactional` 注解覆盖了类注解（如果存在）指定的默认事务语义。你可以注解任何方法，不必关心方法可见性。

为了将你的应用编织到 `AnnotationTransactionAspect` ，你必须要么使用 AspectJ 创建你的应用 (参考 [AspectJ Development Guide](https://www.eclipse.org/aspectj/doc/released/devguide/index.html) )，或者使用加载时编织。参考 [Load-time weaving with AspectJ in the Spring Framework](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-aj-ltw) 了解有关使用 AspectJ 的加载时编织的讨论。

