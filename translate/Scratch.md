### 5.10 在 Spring 应用中使用 AspectJ

目前为止，本章中我们讨论的内容都是纯 Spring AOP。本节中，我们看看如何使用 AspectJ 编译器或者织入器替换或者增强 Spring AOP ，如果你的需求超出了 Spring AOP 提供的支持。

Spring 包含了一个精简的 AspectJ 切面库，作为`spring-aspects.jar`可以在你的发布版本中独立使用。你需要将其添加到你的类路径中以便使用其中的切面。[Using AspectJ to Dependency Inject Domain Objects with Spring](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-atconfigurable) 和 [Other Spring aspects for AspectJ](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-ajlib-other) 讨论该库的内容以及如何使用。[Configuring AspectJ Aspects by Using Spring IoC](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-aj-configure) 讨论如何依赖注入使用 AspectJ 编译器织入的 AspectJ 切面。最后，[Load-time Weaving with AspectJ in the Spring Framework](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-aj-ltw) 介绍使用 AspectJ 的 Spring 应用的加载时织入。

