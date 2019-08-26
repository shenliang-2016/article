## 6. Spring AOP APIs

前一章描述了 Spring 使用 @AspectJ 和基于模式的切面定义对 AOP 的支持。在本章中，我们将讨论较低级别的Spring AOP API。对于常见应用程序，我们建议使用带有 AspectJ 切入点的 Spring AOP，如前一章所述。

### 6.1 Spring 中的 Pointcut API

本节描述了 Spring 如何处理关键的切入点概念。

#### 6.1.1 概念

Spring 的切入点模型使切入点可以独立于增强类型重用。您可以使用相同的切入点来定位不同的增强。

`org.springframework.aop.Pointcut`接口是核心接口，用于将增强定位到特定的类和方法。完整的接口如下：

```java
public interface Pointcut {

    ClassFilter getClassFilter();

    MethodMatcher getMethodMatcher();

}
```

将`Pointcut`接口拆分为两部分允许重用类和方法匹配部分以及细粒度合成操作（例如与另一个方法匹配器执行“联合”）。

`ClassFilter`接口用于将切入点限制为给定的一组目标类。如果`matches()`方法始终返回`true`，则匹配所有目标类。以下清单显示了`ClassFilter`接口定义：

```java
public interface ClassFilter {

    boolean matches(Class clazz);
}
```

 `MethodMatcher` 接口通常更重要。完整的接口如下：

```java
public interface MethodMatcher {

    boolean matches(Method m, Class targetClass);

    boolean isRuntime();

    boolean matches(Method m, Class targetClass, Object[] args);
}
```

`matches(Method, Class)` 方法用于测试此切入点是否与目标类上的给定方法匹配。可以在创建AOP代理时执行此评估，以避免需要对每个方法调用进行测试。如果双参数`matches`方法对给定方法返回`true`，并且`MethodMatcher`的`isRuntime()`方法返回`true`，则在每个方法调用上调用三参数 `matches` 方法。这使得切入点可以在执行目标增强之前立即查看传递给方法调用的参数。

大多数`MethodMatcher`实现都是静态的，这意味着它们的`isRuntime()`方法返回`false`。在这种情况下，永远不会调用三参数 `matches` 方法。

> 如果可能，尝试使切入点成为静态，允许AOP框架在创建AOP代理时缓存切入点评估的结果。

