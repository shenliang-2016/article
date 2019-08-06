### 5.8 代理机制

Spring AOP 使用 JDK 动态代理或者 CGLIB 来创建给定目标对象的代理。JDK 动态代理被构建在 JDK 中，而 CGLIB 是通用开源类定义类库（被重新包装进入`spring-core`中）。

如果需要代理的目标对象实现至少一个接口，一个 JDK 动态代理就会被使用。目标类型实现的所有接口都会被代理。如果该目标对象没有实现任何接口，则会创建一个 CGLIB 代理。

如果你希望强行使用 CGLIB 代理（比如，代理为目标对象定义的每个方法，而不仅仅是被它的接口实现的那些方法），你可以这么做。不过，你需要注意以下问题：

* 使用 CGLIB，`final`方法不能被增强，因为他们不能被在运行时产生的子类中覆盖。
* 从 Spring 4.0 开始，代理对象的构造函数不再被调用两次，因为 CGLIB 代理实例是通过 [Objenesis]([http://objenesis.org/index.html](http://objenesis.org/index.html)) 创建的。 只有当您的JVM不允许构造函数绕过时，您才会看到 Spring 的 AOP 支持中的双重调用和相应的调试日志条目。

为了强行使用 CGLIB 代理，设置`<aop:config>`元素中的`proxy-target-class`属性的值为`true`。如下所示：

```xml
<aop:config proxy-target-class="true">
    <!-- other beans defined here... -->
</aop:config>
```

要在使用 @AspectJ 自动代理支持时强制使用 CGLIB 代理，请将`<aop:aspectj-autoproxy>`元素的`proxy-target-class`属性设置为`true`，如下所示：

```xml
<aop:aspectj-autoproxy proxy-target-class="true"/>
```

> 多个`<aop:config/>`部分在运行时折叠成一个统一的自动代理创建器，它应用任何`<aop:config/>`部分（通常来自不同的XML bean 定义文件）指定的*最强*代理设置。这也适用于`<tx:annotation-driven/>`和`<aop:aspectj-autoproxy/>`元素。
>
> 要清楚，在`<tx:annotation-driven/>`，`<aop:aspectj-autoproxy/>`或`<aop:config/>`元素上使用`proxy-target-class =“true”` 强制使用 CGLIB 代理*用于所有这三个*。

#### 5.8.1 理解 AOP 代理

Spring AOP 是基于代理的。在编写自己的切面或使用 Spring Framework 提供的任何基于 Spring AOP 的切面之前，理解每个语句实际意味着什么的语义是非常重要的。

首先考虑一下你有一个普通的，无代理的，没有特定于它的，直接对象引用的场景，如下面的代码片段所示：

```java
public class SimplePojo implements Pojo {

    public void foo() {
        // this next method invocation is a direct call on the 'this' reference
        this.bar();
    }

    public void bar() {
        // some logic...
    }
}
```

如果你调用一个对象引用上的方法，该方法被直接在对象引用上调用，如下面图片和列表所示：

![aop proxy plain pojo call](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/images/aop-proxy-plain-pojo-call.png)

```java
public class Main {

    public static void main(String[] args) {
        Pojo pojo = new SimplePojo();
        // this is a direct method call on the 'pojo' reference
        pojo.foo();
    }
}
```

当客户端代码具有的引用是代理时，事情会稍微不同。请考虑以下图表和代码段：

![aop proxy call](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/images/aop-proxy-call.png)

```java
public class Main {

    public static void main(String[] args) {
        ProxyFactory factory = new ProxyFactory(new SimplePojo());
        factory.addInterface(Pojo.class);
        factory.addAdvice(new RetryAdvice());

        Pojo pojo = (Pojo) factory.getProxy();
        // this is a method call on the proxy!
        pojo.foo();
    }
}
```