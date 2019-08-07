在这里，需要理解的关键是，`Main`类中的`main(..)`方法中的客户端代码持有一个代理的引用。这就意味着对象引用上的方法调用是在代理上调用的。这样的结果是，代理可以委托给所有的与特定方法调用相关的拦截器(增强)。不过，一旦该调用最终到达目标对象(这个例子中是`SimplePojo`对象引用)，所有它可能做出的自身上的方法调用，比如`this.bar()`或者`this.foo()`，都将使用`this`引用调用，而不是使用代理。这一点有重要影响。这意味着自我调用不会导致与方法调用相关的增强有机会执行。

好的，那么该怎么办呢？最好的方法（术语“最好”，在这里松散地使用）是重构你的代码，这样就不会发生自我调用。这确实需要您做一些工作，但这是最好的，最少侵入性的方法。接下来的方法是绝对可怕的，我们毫不犹豫地指出它，正是因为它是如此可怕。您可以（对我们来说很痛苦）将类中的逻辑完全绑定到 Spring AOP，如下例所示：

```java
public class SimplePojo implements Pojo {

    public void foo() {
        // this works, but... gah!
        ((Pojo) AopContext.currentProxy()).bar();
    }

    public void bar() {
        // some logic...
    }
}
```

这完全将您的代码耦合到 Spring AOP，它使类本身意识到它正在 AOP 上下文中使用，它在 AOP 面前飞行。在创建代理时，还需要一些其他配置，如以下示例所示：

```java
public class Main {

    public static void main(String[] args) {
        ProxyFactory factory = new ProxyFactory(new SimplePojo());
        factory.adddInterface(Pojo.class);
        factory.addAdvice(new RetryAdvice());
        factory.setExposeProxy(true);

        Pojo pojo = (Pojo) factory.getProxy();
        // this is a method call on the proxy!
        pojo.foo();
    }
}
```

最后，必须注意的是 AspectJ 没有这种自调用问题，因为它不是基于代理的 AOP 框架。

### 5.9 编程方式创建 @AspectJ 代理

除了使用`<aop:config>`或`<aop:aspectj-autoproxy>`在配置文件中声明切面之外，还可以以编程方式创建增强目标对象的代理。有关 Spring 的 AOP API 的完整详细信息，请参阅[下一章](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-api) 。在这里，我们希望关注使用 @AspectJ 切面自动创建代理的能力。

您可以使用`org.springframework.aop.aspectj.annotation.AspectJProxyFactory`类为一个或多个 @AspectJ 切面增强的目标对象创建代理。此类的基本用法非常简单，如以下示例所示：

```java
// create a factory that can generate a proxy for the given target object
AspectJProxyFactory factory = new AspectJProxyFactory(targetObject);

// add an aspect, the class must be an @AspectJ aspect
// you can call this as many times as you need with different aspects
factory.addAspect(SecurityManager.class);

// you can also add existing aspect instances, the type of the object supplied must be an @AspectJ aspect
factory.addAspect(usageTracker);

// now get the proxy object...
MyInterfaceType proxy = factory.getProxy();
```

参考 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/aop/aspectj/annotation/AspectJProxyFactory.html) 获取更多信息。