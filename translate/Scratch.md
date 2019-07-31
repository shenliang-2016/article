### 5.5 基于模式的 AOP 支持

如果你更喜欢基于 XML 的格式，Spring 还提供了使用新的`aop`命名空间标签定义切面的支持。这种支持与使用 @AspectJ 风格的切入点表达式和增强类型的支持完全一样。因此，本章节中我们聚焦于新的语法并引导读者参考上一节中的讨论 ([@AspectJ support](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-ataspectj)) 以理解切入点表达式的编写和增强参数绑定。

为了使用本章节中描述的`aop`标签，你需要导入`spring-aop`模式定义，如 [XML Schema-based configuration](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#xsd-schemas) 中所述。参考 [the AOP schema](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#xsd-schemas-aop) 了解如何导入`aop`命名空间中的标签。

在你的 Spring 配置中，所有切面和增强器都必须布置在`<aop:config>`元素中（在一个应用上下文配置中可以存在多个`<aop:config>`元素）。一个`<aop:config>`元素可以包含切入点、增强器以及切面元素（请注意，必须按照此顺序声明这些元素）。

> `<aop:config>` 风格的配置重度使用了 Spring 的 [auto-proxying](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-autoproxy) 机制。这可能会导致问题（这些增强没有被织入）如果你已经通过使用`BeanNameAutoProxyCreator`或者其它类似的技术显式使用自动代理。推荐的使用模式是单独使用 `<aop:config>` 风格或者`AutoProxyCreator`风格而不混合使用它们。

#### 5.5.1 声明一个切面

当你使用模式支持时，一个切面时一个普通的 Java 对象，在你的 Spring 应用上下文中定义为一个 bean 。状态和行为在对象的字段和方法中捕获，切入点和增强信息在 XML 中捕获。

你可以使用 <aop:aspect> 元素声明切面，同时使用`ref`属性引用基础 bean 。如下面例子所示：

```xml
<aop:config>
    <aop:aspect id="myAspect" ref="aBean">
        ...
    </aop:aspect>
</aop:config>

<bean id="aBean" class="...">
    ...
</bean>
```

切面的基础 bean（此例子中是`aBean`）当然可以像其它任何 Spring bean 一样被配置和依赖注入。

