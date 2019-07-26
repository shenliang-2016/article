### 5.2 Spring AOP 能力和目标

Spring AOP 由纯 Java 语言实现。不需要特殊的汇编过程。Spring AOP 不需要控制类加载器层级结构，因而适用于 servlet 容器或者应用服务器。

Spring AOP 目前仅仅支持方法执行连接点（增强 Spring beans 上的方法执行）。字段拦截没有实现，尽管对字段拦截的支持可以在不妨碍核心 Spring AOP APIs 前提下添加。如果你需要增强字段访问以及更新连接点，考虑类似于 AspectJ 的语言。

Spring AOP 的 AOP 方式不同于大K部分其他 AOP 框架。它的目标不是要提供最完整的 AOP 实现（尽管 Spring AOP 已经相当强大），它的目标是提供 AOP 实现和 Spring IoC 之间的紧密集成，以帮助解决企业级应用中的常见问题。

因此，比如，Spring 框架的 AOP 功能通常用在 Spring IoC 容器中。切面通过使用正常 bean 定义语法配置（尽管这允许强大的“自动代理”能力）。这是 Spring AOP 与其他 AOP 实现的关键差异。有些事情你使用 Spring AOP 不会很容易和高效，比如增强细粒度的对象（典型的，域对象）。AspectJ 在这种情况下是最佳选择。不过，我们的经验是 Spring AOP 为适合 AOP 的企业级 Java 应用中的大部分问题提供了出色的解决方案。

Spring AOP 从未试图与 AspectJ 竞争，以提供全面的 AOP 解决方案。我们相信，基于代理的框架（如Spring AOP）和完整的框架（如AspectJ）都很有价值，而且它们是互补的，而不是竞争。Spring 将 Spring AOP 和 IoC 与 AspectJ 无缝集成，以在一致的基于 Spring 的应用程序架构中实现 AOP 的所有使用。此集成不会影响 Spring AOP API 或 AOP 同盟 API。Spring AOP仍然向后兼容。有关 Spring AOP API 的讨论，请参见 [下一章节](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-api) 。

> Spring框架的核心原则之一是非侵入性。这个想法是，您不应该被迫在您的业务或域模型中引入特定于框架的类和接口。但是，在某些地方，Spring Framework确实为您提供了将Spring Framework特定的依赖项引入代码库的选项。为您提供此类选项的基本原理是，在某些情况下，以这种方式阅读或编写某些特定功能可能更容易。但是，Spring Framework（几乎）总是为您提供选择：您可以自由决定哪种选项最适合您的特定用例或场景。
>
> 与本章相关的一个选择是选择哪种AOP框架（以及哪种AOP样式）。您可以选择AspectJ，Spring AOP或两者。您还可以选择@AspectJ注解样式方法或Spring XML配置样式方法。本章选择首先介绍@ AspectJ风格的方法，这一事实不应被视为Spring团队倾向于采用Spring XML配置风格的@AspectJ注释风格方法。
>
> 请参阅 [选择使用哪种AOP声明样式](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-choosing) 以获得更完整的讨论每种风格的“为什么和如何做”。

### 5.3 AOP 代理

Spring AOP 默认使用标准 JDK 动态代理来实现 AOP 代理。这就使得任何接口（或者接口集合）都能够被代理。

Spring AOP 也可以使用 CGLIB 代理。为了代理接口之外的类时，这就是必要的。默认情况下，CGLIB 在业务对象没有实现一个接口时使用。基于接口编程而不是基于实现编程是一种好的实践，业务类通常都会实现一个或者多个业务接口。 [强制使用 CGLIB](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-proxying) 是可能的，我们希望这种情况很少出现，当你需要增强没有在接口中声明的方法时，或者你需要将一个被代理的对象作为一个具体类型传递给一个方法时。

掌握Spring AOP是基于代理的这一事实非常重要。请参阅 [了解AOP代理](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-understanding-aop-proxies) 以全面了解这个实现细节究竟意味着什么。

### 5.4 @AspectJ 支持

@AspectJ 指的是将切面声明为使用注解修饰的常规Java类的样式。作为AspectJ 5版本的一部分，[AspectJ项目](https://www.eclipse.org/aspectj) 引入了@AspectJ样式。Spring使用AspectJ提供的库解释与AspectJ 5相同的注解，用于切入点解析和匹配。但是，AOP运行时仍然是纯Spring AOP，并且不依赖于AspectJ编译器或者编织器。

> 使用AspectJ编译器和编织器可以使用完整的AspectJ语言，并在 [在 Spring 应用中使用AspectJ](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-using-aspectj) 中讨论。

