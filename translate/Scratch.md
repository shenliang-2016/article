#### 5.5.4 引入

引入（在 AspectJ 中被称为类型间声明）允许切面声明被增强的对象实现一个给定的接口并代表那些对象提供该接口的实现。

你可以在`aop:aspect`中使用`aop:declare-parents`元素来创建一个引入。你可以使用`aop:declare-parents`元素来声明匹配类型拥有一个新的父类（通过名称）。比如，给定一个名为`UsageTracked`以及一个名为`DefaultUsageTracked`接口的实现。下面的切面声明所有服务接口的实现同时也实现了接口`UsageTracked`。（例如为了通过 JMX 暴露统计信息）

```xml
<aop:aspect id="usageTrackerAspect" ref="usageTracking">

    <aop:declare-parents
        types-matching="com.xzy.myapp.service.*+"
        implement-interface="com.xyz.myapp.service.tracking.UsageTracked"
        default-impl="com.xyz.myapp.service.tracking.DefaultUsageTracked"/>

    <aop:before
        pointcut="com.xyz.myapp.SystemArchitecture.businessService()
            and this(usageTracked)"
            method="recordUsage"/>

</aop:aspect>
```

对应于`usageTracking`bean 的类将包含下面的方法：

```java
public void recordUsage(UsageTracked usageTracked) {
    usageTracked.incrementUseCount();
}
```

将要被实现的接口由`implement-interface`属性确定。`types-matching`属性的值是一个 AspectJ 类型模式。匹配类型的任何 bean 都实现了`UsageTracked`接口。注意，在上面例子中的前置增强中，服务 beans 能够直接被作为`UsageTracked`接口的实现使用。为了以编程方式访问 bean，你可以如下写：

```java
UsageTracked usageTracked = (UsageTracked) context.getBean("myService");
```

#### 5.5.5 切面实例化模型

单例模型是唯一被支持的基于模式的切面的实例化模型。将来版本中可能会提供其它实例化模型的支持。

#### 5.5.6 增强器

来自 Spring 中定义的 AOP 支持的“增强器”的概念并不直接等价于 AspectJ 中的概念。增强器类似于一个效地自包含的切面，只包含单一增强。该增强自己由一个 bean 表示，同时必须实现 [Advice Types in Spring](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-api-advice-types) 中描述的增强接口之一。增强器可以享受到 AspectJ 切入点表达式的优点。

Spring 通过`<aop:advisor>`元素支持增强器概念。你大部分情况下会发现它跟事务性增强结合使用，事务性增强在 Spring 中也有自己的命名空间支持。下面的例子展示了一个增强器：

```xml
<aop:config>

    <aop:pointcut id="businessService"
        expression="execution(* com.xyz.myapp.service.*.*(..))"/>

    <aop:advisor
        pointcut-ref="businessService"
        advice-ref="tx-advice"/>

</aop:config>

<tx:advice id="tx-advice">
    <tx:attributes>
        <tx:method name="*" propagation="REQUIRED"/>
    </tx:attributes>
</tx:advice>
```

如同前面例子中的`pointcut-ref`属性的使用，你也可以使用`pointcut`属性来定义一个内联切入点表达式。

为了定义增强器的优先级以便增强可以参与排序，使用`order`属性来定义增强器的`Ordered`值。

#### 5.5.7 AOP 模式示例

本节展示如何使用模式支持重写来自 [An AOP Example](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-ataspectj-example) 的并发锁失败重试示例。

业务服务的执行有时候会由于并发问题而失败（比如，死锁失败者）。如果该操作被重试，下一次很可能就会成功。对那些在这种情况下适合重试的业务服务（幂等操作，不需要将结果返回给用户以解决冲突），我们希望透明重试从而避免客户端看到`PessimisticLockingFailureException`。这是一个显然需要横切一个服务层中多个服务的需求，因此，可以通过一个切面来实现。

因为我们希望重试操作，我们需要使用环绕增强以便我们可以多次调用`proceed`方法。下面的例子展示了基本的切面实现（它是一个使用了模式支持的常规 Java 类）：

```java
public class ConcurrentOperationExecutor implements Ordered {

    private static final int DEFAULT_MAX_RETRIES = 2;

    private int maxRetries = DEFAULT_MAX_RETRIES;
    private int order = 1;

    public void setMaxRetries(int maxRetries) {
        this.maxRetries = maxRetries;
    }

    public int getOrder() {
        return this.order;
    }

    public void setOrder(int order) {
        this.order = order;
    }

    public Object doConcurrentOperation(ProceedingJoinPoint pjp) throws Throwable {
        int numAttempts = 0;
        PessimisticLockingFailureException lockFailureException;
        do {
            numAttempts++;
            try {
                return pjp.proceed();
            }
            catch(PessimisticLockingFailureException ex) {
                lockFailureException = ex;
            }
        } while(numAttempts <= this.maxRetries);
        throw lockFailureException;
    }

}
```

注意该切面实现了`Ordered`接口，因此我们可以设定该切面的优先级高于事务增强（我们希望每次重试都有一个新的事务）。其中`maxRetries`和`order`属性都由 Spring 配置。主要的动作发生在`doConcurrentOperation`环绕增强方法中。我们尝试执行，如果发生`PessimistickLockingFailureException`而失败，我们重试，除非已经耗尽和全部的重试次数。

> 该类与 @AspectJ 示例中使用的类相同，但删除了注释。

相应的 Spring 配置如下：

```xml
<aop:config>

    <aop:aspect id="concurrentOperationRetry" ref="concurrentOperationExecutor">

        <aop:pointcut id="idempotentOperation"
            expression="execution(* com.xyz.myapp.service.*.*(..))"/>

        <aop:around
            pointcut-ref="idempotentOperation"
            method="doConcurrentOperation"/>

    </aop:aspect>

</aop:config>

<bean id="concurrentOperationExecutor"
    class="com.xyz.myapp.service.impl.ConcurrentOperationExecutor">
        <property name="maxRetries" value="3"/>
        <property name="order" value="100"/>
</bean>
```

请注意，目前为止，我们假设所有业务服务都是幂等的。如果不是这种情况，我们可以通过引入`Idempotent`注解并使用该注解来修饰服务操作的实现来优化切面，使其仅重试真正的幂等操作，如以下示例所示：

```java
@Retention(RetentionPolicy.RUNTIME)
public @interface Idempotent {
    // marker annotation
}
```

对切面进行更改以仅重试幂等操作涉及改进切入点表达式，以便只有`@Idempotent`操作匹配，如下所示：

```xml
<aop:pointcut id="idempotentOperation"
        expression="execution(* com.xyz.myapp.service.*.*(..)) and
        @annotation(com.xyz.myapp.service.Idempotent)"/>
```