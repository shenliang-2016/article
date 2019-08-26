#### 6.1.2 Pointcuts 上的操作

Spring支持切入点上的操作（特别是并集和交集）。

并集表示任何一个切入点匹配的方法。交集表示两个切入点同时匹配的方法。并集通常更有用。您可以使用`org.springframework.aop.support.Pointcuts`类中的静态方法或使用在同一个包中的`ComposablePointcut`类来编写切入点。但是，使用AspectJ切入点表达式通常是一种更简单的方法。

#### 6.1.3 AspectJ 表达式 Pointcuts

从2.0开始，Spring使用的最重要的切入点类型是`org.springframework.aop.aspectj.AspectJExpressionPointcut`。这是一个切入点，它使用AspectJ提供的库来解析AspectJ切入点表达式字符串。

有关受支持的AspectJ切入点元语的讨论，请参阅 [previous chapter](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop) 。

#### 6.1.4 方便的 Pointcut 实现

Spring提供了几种方便的切入点实现。您可以直接使用其中一些。其他用于在特定于应用程序的切入点中进行子类化。

##### 静态 Pointcuts

静态切入点基于方法和目标类，不能考虑方法的参数。对于大多数用途，静态切入点足够 - 并且最好。当首次调用方法时，Spring只能评估一次静态切入点。之后，无需再次使用每个方法调用来评估切入点。

本节的其余部分描述了Spring中包含的一些静态切入点实现。

###### 正则表达式 Pointcuts

指定静态切入点的一种显而易见的方法是正则表达式。除了Spring之外的几个AOP框架使得这一点成为可能。`org.springframework.aop.support.JdkRegexpMethodPointcut`是一个通用的正则表达式切入点，它使用JDK中的正则表达式支持。

使用`JdkRegexpMethodPointcut`类，您可以提供模式字符串列表。如果其中任何一个匹配，则切入点评估为`true`。（因此，结果实际上是这些切入点的并集。）

以下示例显示如何使用`JdkRegexpMethodPointcut`：

```xml
<bean id="settersAndAbsquatulatePointcut"
        class="org.springframework.aop.support.JdkRegexpMethodPointcut">
    <property name="patterns">
        <list>
            <value>.*set.*</value>
            <value>.*absquatulate</value>
        </list>
    </property>
</bean>
```

Spring提供了一个名为`RegexpMethodPointcutAdvisor`的便利类，它让我们也可以引用一个`Advice`（记住`Advice`可以是一个拦截器，前置增强，抛出增强等等）。在幕后，Spring使用了`JdkRegexpMethodPointcut`。 使用`RegexpMethodPointcutAdvisor`简化了织入，因为一个bean封装了切入点和增强，如下例所示：

```xml
<bean id="settersAndAbsquatulateAdvisor"
        class="org.springframework.aop.support.RegexpMethodPointcutAdvisor">
    <property name="advice">
        <ref bean="beanNameOfAopAllianceInterceptor"/>
    </property>
    <property name="patterns">
        <list>
            <value>.*set.*</value>
            <value>.*absquatulate</value>
        </list>
    </property>
</bean>
```

您可以将`RegexpMethodPointcutAdvisor`与任何`Advice`类型一起使用。

###### 属性驱动的 Pointcuts

一种重要的静态切入点是元数据驱动的切入点。这使用元数据属性的值（通常是源级元数据）。

##### 动态 pointcuts

与静态切入点相比，动态切入点的评估成本更高。它们考虑了方法参数以及静态信息。这意味着必须使用每个方法调用来评估它们，并且不能缓存结果，因为参数会有所不同。

主要的例子是 `control flow` 切入点。

###### 控制流 Pointcuts

Spring控制流切入点在概念上类似于AspectJ `cflow` 切入点，虽然功能较弱。（目前无法指定切入点在由另一个切入点匹配的连接点下方执行。）控制流切入点与当前调用堆栈匹配。例如，如果连接点是由`com.mycompany.web`包中的方法或`SomeCaller`类调用的，则可能会触发它。使用`org.springframework.aop.support.ControlFlowPointcut`类指定控制流切入点。

> 在运行时评估控制流切入点的成本远远高于其他动态切入点。在Java 1.4中，成本大约是其他动态切入点的五倍。

#### 6.1.5 Pointcut 超类

Spring提供了有用的切入点超类来帮助您实现自己的切入点。

因为静态切入点最有用，所以你应该继承`StaticMethodMatcherPointcut`。这需要只实现一个抽象方法（尽管您可以覆盖其他方法来自定义行为）。以下示例显示如何子类化`StaticMethodMatcherPointcut`：

```java
class TestStaticPointcut extends StaticMethodMatcherPointcut {

    public boolean matches(Method m, Class targetClass) {
        // return true if custom criteria match
    }
}
```

还有动态切入点的超类。您可以将自定义切入点与任何增强类型一起使用。

#### 6.1.6 自定义 Pointcuts

因为Spring AOP中的切入点是Java类而不是语言功能（如在AspectJ中），所以您可以声明自定义切入点，无论是静态还是动态。Spring中的自定义切入点可以是任意复杂的。但是，如果可以，我们建议使用AspectJ切入点表达式语言。

> 更高版本的Spring可能为JAC提供的“语义切入点”提供支持 - 例如，“所有改变目标对象中实例变量的方法”。

