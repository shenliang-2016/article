### 6.3 Spring 中的 Advisor API 

在 Spring 中，Advisor 是一个切面，它只包含与切入点表达式关联的单个增强对象。

除了引介的特殊情况，任何增强器都可以与任何增强一起使用。`org.springframework.aop.support.DefaultPointcutAdvisor` 是最常用的增强器类。它可以与`MethodInterceptor`，`BeforeAdvice`或`ThrowsAdvice`一起使用。

可以在同一个 AOP 代理中混合 Spring 中的增强器和增强类型。例如，您可以在一个代理配置中使用拦截增强，抛出增强和前置增强。Spring 自动创建必要的拦截器链。

