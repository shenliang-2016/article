### 6.8 使用 "auto-proxy" 设施

目前为止，我们已经学会了使用 `ProxyFactoryBean` 或者类似的工厂 bean 显式创建 AOP 代理。

Spring 还允许我们使用“自动代理” bean 定义，它可以自动代理选择的 bean 定义。该机制够在在 Spring 的“bean 后处理器”基础设施中，该基础设施允许在容器加载时修改任何 bean 定义。

在这个模型中，你在你的 XML bean 定义文件中配置一些特殊 bean 定义来配置自动代理基础设施。这允许你声明自动代理的备选目标。你不需要使用 `ProxyFactoryBean` 。

下面是两种方法：

- 通过使用表示当前上下文中一个特殊 bean 的自动代理创建器。
- 自动代理创建的一个特例值得单独考虑：由源代码级元数据属性驱动的自动代理创建。

#### 6.8.1 自动代理 Bean 定义

本章节介绍 `org.springframework.aop.framework.autoproxy` 包提供的自动代理创建器。

##### `BeanNameAutoProxyCreator`

 `BeanNameAutoProxyCreator` 是一个 `BeanPostProcessor` ，为那些名称匹配到通配符字面值的 bean 自动创建 AOP 代理。下面的例子展示如何创建 `BeanNameAutoProxyCreator` bean :

```xml
<bean class="org.springframework.aop.framework.autoproxy.BeanNameAutoProxyCreator">
    <property name="beanNames" value="jdk*,onlyJdk"/>
    <property name="interceptorNames">
        <list>
            <value>myInterceptor</value>
        </list>
    </property>
</bean>
```

和 `ProxyFactoryBean` 一样，存在一个 `interceptorNames` 属性而不是拦截器列表，允许原型增强器的准确行为。名为“interceptors”的可以是增强器或者任何增强类型。

和通用的自动代理一样，使用 `BeanNameAutoProxyCreator` 的主要目的是将同一套配置一致性地应用于多个对象，同时保持最小化配置。这是将声明式事务应用于多个对象时的流行做法。

名称匹配的 Bean 定义（例如前面示例中的`jdkMyBean`和`onlyJdk`）是具有目标类型的普通旧 bean 定义。`BeanNameAutoProxyCreator`自动创建 AOP 代理。相同的增强适用于所有匹配的 bean。请注意，如果使用增强器（而不是前面示例中的拦截器），则切入点可能会以不同方式应用于不同的 bean。

##### `DefaultAdvisorAutoProxyCreator`

更通用且非常强大的自动代理创建器是 `DefaultAdvisorAntoProxyCreator` 。这个类自动应用当前上下文中的候选增强器，不需要再自动代理增强器 bean 定义中包含特殊的 bean 名称。它提供与`BeanNameAutoProxyCreator`一样的一致配置和避免重复的优点。

使用此机制涉及到：

- 指定一个 `DefaultAdvisorAutoProxyCreator` bean 定义。
- 指定相同或者相关上下文中的任意数量的增强器。注意必须是增强器，不能是拦截器或者别的增强。这是必需的，因为必须存在一个切入点来评估，以检查每个增强对候选 bean 定义的合格性。

`DefaultAdvisorAutoProxyCreator` 自动评估每个增强器包含的切入点，以确定哪个增强应该被应用于每个业务对象（比如例子中的 `businessObject1` 和 `businessObject2` ）。

这意味着可以自动将任意数量的增强器应用于每个业务对象。如果任何增强器中的切入点与业务对象中的任何方法都不匹配，则不会代理该对象。当为新业务对象添加 bean 定义时，如果必要就会自动代理它们。

自动代理通常具有使调用者或依赖者无法获得未被增强的对象的优点。在此`ApplicationContext`上调用`getBean(“businessObject1”)`将返回 AOP 代理，而不是目标业务对象。（前面所示的“inner bean”术语也提供了这种好处。）

以下示例创建一个`DefaultAdvisorAutoProxyCreator` bean以及本节中讨论的其他元素：

```xml
<bean class="org.springframework.aop.framework.autoproxy.DefaultAdvisorAutoProxyCreator"/>

<bean class="org.springframework.transaction.interceptor.TransactionAttributeSourceAdvisor">
    <property name="transactionInterceptor" ref="transactionInterceptor"/>
</bean>

<bean id="customAdvisor" class="com.mycompany.MyAdvisor"/>

<bean id="businessObject1" class="com.mycompany.BusinessObject1">
    <!-- Properties omitted -->
</bean>

<bean id="businessObject2" class="com.mycompany.BusinessObject2"/>
```

如果要将相同的增强一致地应用于许多业务对象，则`DefaultAdvisorAutoProxyCreator`非常有用。基础结构定义到位后，您可以添加新的业务对象，而不需要特定的代理配置。您还可以轻松地删除其他切面（例如，跟踪或性能监视切面），只需对配置进行最小的更改。

`DefaultAdvisorAutoProxyCreator`提供过滤支持（通过使用命名约定，以便仅评估某些增强器，允许在同一工厂中使用多个不同配置的`AdvisorAutoProxyCreators`）和排序。如果这是一个问题，增强器可以实现`org.springframework.core.Ordered`接口以确保正确的排序。上例中使用的`TransactionAttributeSourceAdvisor`具有可配置的顺序值，默认设置是无序的。

### 6.9 使用 `TargetSource` 实现

Spring 提供了 `TargetSource` 的概念，体现在 `org.springframework.aop.TargetSource` 接口中。该接口负责返回实现了连接点的“目标对象”。`TargetSource` 实现每当 AOP 代理处理一个方法调用时就会请求一个目标实例。

使用 Spring AOP 的开发者正常情况下不需要直接使用 `TargetSource` 实现，但是这一点提供了对某些复杂目标的强大支持，诸如池化，热替换等等。例如，一个池化的 `TargetSource` 能够通过使用一个池管理实例，为每次调用返回不同的目标实例。

如果你没有指定一个 `TargetSource` ，则一个默认实现就会被用于包装一个局部对象。该的目标每次调用都被返回（如你所愿）。

本章节的剩余部分描述 Spring 提供的标准的目标源，以及如何使用它们。

> 使用自定义目标源时，目标通常需要是原型而不是单例 bean 定义。这允许 Spring 在需要时创建新的目标实例。

#### 6.9.1 可热替换的目标源

`org.springframework.aop.target.HotSwappableTargetSource`允许切换 AOP 代理的目标，同时让调用者保持对它的引用。

更改目标源的目标会立即生效。`HotSwappableTargetSource`是线程安全的。

您可以使用`HotSwappableTargetSource`上的`swap()`方法更改目标，如以下示例所示：

```java
HotSwappableTargetSource swapper = (HotSwappableTargetSource) beanFactory.getBean("swapper");
Object oldTarget = swapper.swap(newTarget);
```

下面的例子展示了所需要的 XML 定义：

```xml
<bean id="initialTarget" class="mycompany.OldTarget"/>

<bean id="swapper" class="org.springframework.aop.target.HotSwappableTargetSource">
    <constructor-arg ref="initialTarget"/>
</bean>

<bean id="swappable" class="org.springframework.aop.framework.ProxyFactoryBean">
    <property name="targetSource" ref="swapper"/>
</bean>
```

前面的`swap()`调用更改了可替换 bean 的目标。持有对该 bean 的引用的客户端不知道该更改但立即开始命中新目标。

虽然这个例子没有添加任何增强（没有必要添加增强来使用`TargetSource`），但任何`TargetSource`都可以与任意增强一起使用。

#### 6.9.2 池化 Target Sources

使用池化目标源提供了类似于无状态会话 EJB 的编程模型，其中维护了相同实例的池，方法调用将释放池中的空闲对象。

Spring 池和 SLSB 池之间的一个重要区别是 Spring 池可以应用于任何 POJO。与 Spring 一样，此服务可以以非侵入方式应用。

Spring 为 Commons Pool 2.2 提供支持，它提供了一个相当有效的池实现。您需要在应用程序的类路径上添加`commons-pool` Jar才能使用此功能。您还可以使用子类化`org.springframework.aop.target.AbstractPoolingTargetSource`来支持任何其他池化 API。

> Commons Pool 1.5+也受支持，但自Spring Framework 4.2起不推荐使用。

下面的例子展示了一个示例配置：

```xml
<bean id="businessObjectTarget" class="com.mycompany.MyBusinessObject"
        scope="prototype">
    ... properties omitted
</bean>

<bean id="poolTargetSource" class="org.springframework.aop.target.CommonsPool2TargetSource">
    <property name="targetBeanName" value="businessObjectTarget"/>
    <property name="maxSize" value="25"/>
</bean>

<bean id="businessObject" class="org.springframework.aop.framework.ProxyFactoryBean">
    <property name="targetSource" ref="poolTargetSource"/>
    <property name="interceptorNames" value="myInterceptor"/>
</bean>
```

请注意，目标对象（前面示例中的`businessObjectTarget`）必须是原型模式的。这使得`PoolingTargetSource`实现可以创建目标的新实例，以根据需要扩充池。请参阅 [javadoc of`AbstractPoolingTargetSource`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframeworkaop/target/AbstractPoolingTargetSource.html) 以及您希望用于获取有关其属性的信息的具体子类。`maxSize`是最基本的，并且始终保证存在。

在这种情况下，`myInterceptor`是需要在同一 IoC 上下文中定义的拦截器的名称。但是，您无需指定拦截器来使用池。如果您只想要池化而没有其他增强，请不要设置`interceptorNamesproperty`。

您可以将 Spring 配置为能够将任何池化对象转换为`org.springframework.aop.target.PoolingConfig`接口，该接口通过引介公开有关池的配置和当前大小的信息。您需要定义类似于以下内容的增强器：

```xml
<bean id="poolConfigAdvisor" class="org.springframework.beans.factory.config.MethodInvokingFactoryBean">
    <property name="targetObject" ref="poolTargetSource"/>
    <property name="targetMethod" value="getPoolingConfigMixin"/>
</bean>
```

通过在`AbstractPoolingTargetSource`类上调用便捷方法获得此增强器，因此使用`MethodInvokingFactoryBean`。此增强器的名称（`poolConfigAdvisor`）必须位于用于公开池对象的`ProxyFactoryBean`中的拦截器名称列表中。

转型定义如下：

```java
PoolingConfig conf = (PoolingConfig) beanFactory.getBean("businessObject");
System.out.println("Max pool size is " + conf.getMaxSize());
```

> 通常不需要池化无状态服务对象。我们不相信它应该是默认选择，因为大多数无状态对象自然是线程安全的，并且如果资源被缓存，实例池也是有问题的。

通过使用自动代理可以实现更简单的池化。您可以设置任何自动代理创建器使用的`TargetSource`实现。

#### 6.9.3 原型 Target Sources

设置“原型”目标源类似于设置池化`TargetSource`。在这种情况下，将在每次方法调用时创建目标的新实例。虽然在现代 JVM 中创建新对象的成本并不高，但连接新对象（满足其 IoC 依赖性）的成本可能更高。因此，如果没有充分的理由，就不应该使用这种方法。

为此，您可以修改前面展示的`poolTargetSource`定义，如下所示（为清晰起见，我们还更改了名称）：

```xml
<bean id="prototypeTargetSource" class="org.springframework.aop.target.PrototypeTargetSource">
    <property name="targetBeanName" ref="businessObjectTarget"/>
</bean>
```

唯一的属性是目标 bean 的名称。`TargetSource`实现中使用继承来确保一致的命名。与池化目标源一样，目标 bean 必须是原型 bean 定义。

#### 6.9.4 `ThreadLocal` Target Sources

如果您需要为每个传入请求创建一个对象（每个线程），`ThreadLocal`目标源很有用。`ThreadLocal`的概念提供了一个JDK范围的工具，可以为线程透明地存储资源。设置`ThreadLocalTargetSource`与设置其他类型的目标源几乎相同，如下例所示：

```xml
<bean id="threadlocalTargetSource" class="org.springframework.aop.target.ThreadLocalTargetSource">
    <property name="targetBeanName" value="businessObjectTarget"/>
</bean>
```

> 在多线程和多类加载器环境中错误地使用`ThreadLocal`实例时，它们会出现严重问题（可能导致内存泄漏）。您应该始终考虑将`threadlocal`包装在其他类中，并且永远不要直接使用`ThreadLocal`本身（包装类除外）。此外，您应该始终记住正确设置和取消设置（后者只需要调用`ThreadLocal.set(null)`）线程的本地资源。在任何情况下都应该进行取消，因为不取消它可能会导致有问题的行为。Spring 的`ThreadLocal`支持为您完成此操作，应始终考虑使用`ThreadLocal`实例而不使用其他正确的处理代码。

### 6.10 定义新的增强类型

Spring AOP 旨在可扩展。虽然拦截实现策略目前在内部使用，但除了环绕增强的拦截，前置，抛出增强以及返回之后增强，还可以支持任意增强类型。

`org.springframework.aop.framework.adapter`包是一个 SPI 包，可以在不更改核心框架的情况下添加对新自定义增强类型的支持。自定义增强类型的唯一约束是它必须实现`org.aopalliance.aop.Advice`标记接口。

有关详细信息，请参阅 [`org.springframework.aop.framework.adapter`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/aop/framework/adapter/package-frame.html) 文档。

