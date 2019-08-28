#### 6.4.3 基于 JDK 和基于 CGLIB 的代理

本节作为关于`ProxyFactoryBean`如何选择为特定目标对象（将被代理）创建基于 JDK 的代理或基于 CGLIB 的代理的权威文档。

> `ProxyFactoryBean`在创建基于 JDK 或 CGLIB 的代理方面的行为在 Spring 的 1.2.x 和 2.0 版本之间发生了变化。现在，`ProxyFactoryBean`在自动检测接口方面表现出与`TransactionProxyFactoryBean`类相似的语义。

如果要代理的目标对象的类（以下简称为目标类）未实现任何接口，则创建基于 CGLIB 的代理。这是最简单的方案，因为 JDK 代理是基于接口的，没有接口意味着甚至不可能进行 JDK 代理。您可以通过设置 `interceptorNames` 属性来插入目标 bean 并指定拦截器列表。请注意，即使将 `ProxyFactoryBean` 的 `proxyTargetClass` 属性设置为 `false`，也会创建基于 CGLIB 的代理。（这样做没有意义，最好从 bean 定义中删除，因为它最好情况下也是多余的，最坏情况下则会导致混淆。）

如果目标类实现一个（或多个）接口，则创建的代理类型取决于`ProxyFactoryBean`的配置。

如果`ProxyFactoryBean`的`proxyTargetClass`属性已设置为`true`，则会创建基于 CGLIB 的代理。这是有道理的，并且符合最少惊喜的原则。即使`ProxyFactoryBean`的`proxyInterfaces`属性已设置为一个或多个完全限定的接口名称，`proxyTargetClass`属性设置为`true`这一事实也会导致基于 CGLIB 的代理生效。

如果`ProxyFactoryBean`的`proxyInterfaces`属性已设置为一个或多个完全限定的接口名称，则会创建基于 JDK 的代理。创建的代理实现`proxyInterfaces`属性中指定的所有接口。如果目标类碰巧实现了比`proxyInterfaces`属性中指定的接口多得多的接口，那么这一切都很好，但返回的代理不会实现这些额外的接口。

如果尚未设置`ProxyFactoryBean`的`proxyInterfaces`属性，但目标类确实实现了一个（或多个）接口，则`ProxyFactoryBean`会自动检测目标类确实实现至少一个接口的事实，则基于 JDK 的代理被创建。实际代理的接口是目标类实现的所有接口。实际上，这与提供目标类为`proxyInterfaces`属性实现的每个接口的列表相同。但是，它的工作量明显减少，并且不易出现拼写错误。

#### 6.4.4 代理接口

考虑一下`ProxyFactoryBean`的一个简单示例。这个例子涉及：

 - 代理的目标 bean。这是示例中的`personTarget` bean定义。
 - 用于提供增强的`Advisor` 和`Interceptor`。
 - 用于指定目标对象（`personTarget` bean），需要代理的接口以及要应用的增强的 AOP 代理 bean 定义。

以下清单显示了示例：

```xml
<bean id="personTarget" class="com.mycompany.PersonImpl">
    <property name="name" value="Tony"/>
    <property name="age" value="51"/>
</bean>

<bean id="myAdvisor" class="com.mycompany.MyAdvisor">
    <property name="someProperty" value="Custom string property value"/>
</bean>

<bean id="debugInterceptor" class="org.springframework.aop.interceptor.DebugInterceptor">
</bean>

<bean id="person"
    class="org.springframework.aop.framework.ProxyFactoryBean">
    <property name="proxyInterfaces" value="com.mycompany.Person"/>

    <property name="target" ref="personTarget"/>
    <property name="interceptorNames">
        <list>
            <value>myAdvisor</value>
            <value>debugInterceptor</value>
        </list>
    </property>
</bean>
```

请注意，`interceptorNames`属性采用`String`列表，该列表包含当前工厂中拦截器或增强器的 bean 名称。您可以在返回之前、之后使用增强器，拦截器，并抛出增强对象。增强器的顺序很重要。

> 您可能想知道为什么列表不包含 bean 引用。原因是，如果`ProxyFactoryBean`的`singleton`属性设置为`false`，则它必须能够返回独立的代理实例。如果任何增强器本身就是原型，而需要返回一个独立的实例，因此必须能够从工厂获得原型的实例，持有引用是不够的。

前面显示的`person` bean 定义可以用来代替`Person`实现，如下所示：

```java
Person person = (Person) factory.getBean("person");
```

与普通 Java 对象一样，同一 IoC 上下文中的其他 bean 可以表达对它的强类型依赖。以下示例显示了如何执行此操作：

```xml
<bean id="personUser" class="com.mycompany.PersonUser">
    <property name="person"><ref bean="person"/></property>
</bean>
```

此示例中的`PersonUser`类公开`Person`类型的属性。就其而言，可以透明地使用 AOP 代理来代替“真实”的`Person`实现。但是，它的类将是一个动态代理类。可以将其转型到`Advised`接口（稍后讨论）。

您可以使用匿名内部 bean 隐藏目标和代理之间的区别。只有`ProxyFactoryBean`定义是不同的。其中的增强仅用于完整性。以下示例显示如何使用匿名内部 bean：

```xml
<bean id="myAdvisor" class="com.mycompany.MyAdvisor">
    <property name="someProperty" value="Custom string property value"/>
</bean>

<bean id="debugInterceptor" class="org.springframework.aop.interceptor.DebugInterceptor"/>

<bean id="person" class="org.springframework.aop.framework.ProxyFactoryBean">
    <property name="proxyInterfaces" value="com.mycompany.Person"/>
    <!-- Use inner bean, not local reference to target -->
    <property name="target">
        <bean class="com.mycompany.PersonImpl">
            <property name="name" value="Tony"/>
            <property name="age" value="51"/>
        </bean>
    </property>
    <property name="interceptorNames">
        <list>
            <value>myAdvisor</value>
            <value>debugInterceptor</value>
        </list>
    </property>
</bean>
```

使用匿名内部 bean 的优点是只有一个`Person`类型的对象。如果我们想要阻止应用程序上下文的用户获取对未增强对象的引用或者需要避免 Spring IoC 自动装配的任何歧义，这将非常有用。可以说，还有一个优点是`ProxyFactoryBean`定义是自包含的。但是，有时能够从工厂获得未增强的目标实际上可能是一个优势（例如，在某些测试场景中）。

#### 6.4.5 代理类

如果您需要代理一个类而不是一个或多个接口，该怎么办？

想象一下，在我们之前的例子中，没有`Person`接口。我们需要增强一个名为`Person`的类，它没有实现任何业务接口。在这种情况下，您可以将 Spring 配置为使用 CGLIB 代理而不是动态代理。为此，请将前面展示的`ProxyFactoryBean`上的`proxyTargetClass`属性设置为`true`。虽然最好是面向接口而不是类编程，但在使用遗留代码时，增强不实现接口的类的能力会很有用。（一般来说，Spring不是规定性的。虽然它可以很容易地应用好的实践，但它避免强制使用特定的方法。）

如果您愿意，即使您有接口，也可以在任何情况下强制使用 CGLIB。

CGLIB 代理通过在运行时生成目标类的子类来工作。Spring 配置此生成的子类以将方法调用委托给原始目标。子类用于实现`Decorator`模式，织入到增强中。

CGLIB 代理通常应对用户透明。但是，有一些问题需要考虑：

 - 不能增强`final`方法，因为它们不能被覆盖。
 - 无需将 CGLIB 添加到类路径中。从 Spring 3.2 开始，CGLIB 被重新打包并包含在`spring-core` JAR中。换句话说，基于 CGLIB 的 AOP “开箱即用”，JDK 动态代理也是如此。

CGLIB 代理和动态代理之间几乎没有性能差异。在这种情况下，性能不应该是决定性的考虑因素。

#### 6.4.6 使用 “Global” 增强器

通过在拦截器名称后附加星号，将所有与星号前面的部分匹配的 bean 名称的增强器添加到增强器链中。如果您需要添加一组标准的“全局”增强器，这可以派上用场。以下示例定义了两个全局增强器：

```xml
<bean id="proxy" class="org.springframework.aop.framework.ProxyFactoryBean">
    <property name="target" ref="service"/>
    <property name="interceptorNames">
        <list>
            <value>global*</value>
        </list>
    </property>
</bean>

<bean id="global_debug" class="org.springframework.aop.interceptor.DebugInterceptor"/>
<bean id="global_performance" class="org.springframework.aop.interceptor.PerformanceMonitorInterceptor"/>
```

