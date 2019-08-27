### 6.2 Spring 中的 Advice API

仙子啊我们来分析 Spring AOP 是如何处理增强的。

#### 6.2.1 Advice 生命周期

每个增强都是一个 Spring bean，一个增强实例可以在所有被增强的对象之间共享，或者专用于每个被增强对象。对应于 `per-class` 或者 `per-instance` 增强。

`per-class` 增强更常用。它适用于通用增强，比如事务增强器。这不依赖被代理的对象的状态或者添加新的状态。此类增强很少用于方法或者参数。

`per-instance` 增强适用于引介，以支持 minxins。这种情况下，增强会添加状态到被代理的对象。

您可以在同一个AOP代理中混合使用共享和 `per-instance` 的增强。

#### 6.2.2 Spring 中的 Advice Types

Spring 提供了多种增强类型，并可以扩展支持任意增强类型。本章节描述相关基本概念和标准增强类型。

##### 拦截环绕 Advice

Spring 中最基础的增强类型就是拦截环绕增强。

Spring 兼容 AOP `Alliance` 接口，可以提供使用方法拦截的增强。实现了 `MethodInterceptor` 的类以及实现了环绕增强的类应该同时实现如下接口：

```java
public interface MethodInterceptor extends Interceptor {

    Object invoke(MethodInvocation invocation) throws Throwable;
}
```

`invoke()` 方法的 `MethodInvocation` 参数暴露了正在被调用的方法，目标连接点，AOP 代理，以及方法的参数。`invoke()` 方法应该返回调用的结果，也就是连接点的返回值。

下面的例子展示了一个简单的 `MethodInterceptor` 实现：

```java
public class DebugInterceptor implements MethodInterceptor {

    public Object invoke(MethodInvocation invocation) throws Throwable {
        System.out.println("Before: invocation=[" + invocation + "]");
        Object rval = invocation.proceed();
        System.out.println("Invocation returned");
        return rval;
    }
}
```

注意对 `MethodInvocation` 的 `proceed()` 方法的调用。该方法将执行连接点的拦截器链。大多数拦截器调用此方法并返回它的返回值。不过，`MethodInterceptor` ，像任何环绕增强，可以返回一个不同的值，或者抛出一个异常，而不是调用该 `proceed` 方法。不过，如果没有特别的原因，你应该不会这么做。

> `MethodInterceptor` 实现提供了与其它 AOP `Alliance` 兼容的 AOP 实现的互操作性。本章节剩余部分讨论的其它增强类型以特定于 Spring 的形式实现通用 AOP 概念。尽管使用最精准的增强类型是有好处的，如果你希望在别的 AOP 框架中运行切面，则应该坚持使用 `MethodInterceptor` 环绕增强。注意切入点目前并不能跨框架互操作，而且 AOP Allicance 目前并没有定义切入点接口。

##### 前置 Advice

前置增强相对更加简单。不需要 `MethodInvocation` 对象，因为它仅仅会在进入方法之前被调用。

前置增强的主要优点在于，不需要调用 `proceed()` 方法，因而不存在无意中无法沿着拦截链继续前进的可能性。

下面的例子展示了 `MethodBeforeAdvice` 接口：

```java
public interface MethodBeforeAdvice extends BeforeAdvice {

    void before(Method m, Object[] args, Object target) throws Throwable;
}
```

（Spring API 设计允许字段前置增强，尽管通常对象用于字段拦截，Spring 也不太可能实现它。）

注意返回类型是 `void` 。前置增强可以在连接点执行之前插入自定义行为，但是不能修改返回值。如果一个前置增强抛出异常，它就会阻止拦截器链的继续执行。该异常会反向传播到拦截器链。如果它是不受检查的或者是在被调用的方法签名中声明的，它就会被直接传递给客户端。否则，它会被 AOP 代理包装为一个不受检查的异常。

下面是一个 Spring 中的前置增强的例子，它统计所有方法调用数：

```java
public class CountingBeforeAdvice implements MethodBeforeAdvice {

    private int count;

    public void before(Method m, Object[] args, Object target) throws Throwable {
        ++count;
    }

    public int getCount() {
        return count;
    }
}
```

> 前置增强可以被用于所有切入点。

##### 抛出 Advice

抛出增强在连接点返回之后，并且连接点抛出异常时被调用。Spring 提供了类型化的抛出增强。注意，这意味着 `org.springframework.aop.ThrowsAdvicee` 接口不包含任何方法。它只是一个标记接口，表示给定对象实现了一个或者多个类型化的抛出增强方法。形式如下：

```java
afterThrowing([Method, args, target], subclassOfThrowable)
```

只有最后一个参数是必需的。方法签名可以拥有一个或者四个参数，取决于增强方法是否对方法和参数感兴趣。接下来两个例子展示了抛出增强的使用。

下面的增强当 `RemoteException` 或者其子类型的异常被抛出时被调用：

```java
public class RemoteThrowsAdvice implements ThrowsAdvice {

    public void afterThrowing(RemoteException ex) throws Throwable {
        // Do something with remote exception
    }
}
```

不同于前置增强，下面的例子声明四个参数，因此它可以访问被调用的方法，方法参数以及目标对象。下面的增强当 `ServletException` 被抛出时被调用：

```java
public class ServletThrowsAdviceWithArguments implements ThrowsAdvice {

    public void afterThrowing(Method m, Object[] args, Object target, ServletException ex) {
        // Do something with all arguments
    }
}
```

最后的例子展示这两个方法如何放在同一个类中，该类可以同时处理 `RemoteException` 和 `ServletException` 。任意数量的抛出增强方法都可以被组合进入一个类中。下面的例子展示了这种情况：

```java
public static class CombinedThrowsAdvice implements ThrowsAdvice {

    public void afterThrowing(RemoteException ex) throws Throwable {
        // Do something with remote exception
    }

    public void afterThrowing(Method m, Object[] args, Object target, ServletException ex) {
        // Do something with all arguments
    }
}
```

> 如果抛出增强方法本身抛出异常，该异常将会覆盖原始异常（也就是说，它改变了本来要抛给用户的异常）。该异常典型的会是 `RuntimeException`，可以与任何方法签名兼容。不过如果抛出增强方法抛出一个受检查的异常，该异常就必需匹配目标方法声明的异常，并且，因此就会某种程度上耦合到特定的目标方法签名。*永远不要抛出与目标方法签名不兼容的未声明的受检查的异常！*

> 抛出增强可以用于任何切入点。

##### 返回之后 Advice

Spring 中的返回之后增强必须实现 `org.springframework.aop.AfterReturningAdvice` 接口，如下面例子所示：

```java
public interface AfterReturningAdvice extends Advice {

    void afterReturning(Object returnValue, Method m, Object[] args, Object target)
            throws Throwable;
}
```

返回之后增强可以访问返回值（但是它不能修改），被调用的方法，被调用方法的参数，以及目标。

下面的返回之后增强统计所有没有抛出异常的成功的方法调用：

```java
public class CountingAfterReturningAdvice implements AfterReturningAdvice {

    private int count;

    public void afterReturning(Object returnValue, Method m, Object[] args, Object target)
            throws Throwable {
        ++count;
    }

    public int getCount() {
        return count;
    }
}
```

此增强不会改变执行路径。如果它抛出一个异常，则它将抛出拦截器链而不是返回值。

> 返回之后增强可用于任何切入点。

##### 引介 Advice

Spring 将引介增强作为一种特殊的拦截增强。

引介需要 `IntroductionAdvisor` 和 `IntrodctionInterceptor` ，实现下面的接口：

```java
public interface IntroductionInterceptor extends MethodInterceptor {

    boolean implementsInterface(Class intf);
}
```

从AOP Alliance `MethodInterceptor`接口继承的`invoke()`方法必须实现引介。也就是说，如果调用的方法在引介的接口上，则引介拦截器负责处理方法调用 - 它不能调用`proceed()`。

引介增强不能与任何切入点一起使用，因为它仅适用于类级别，而不是方法级别。您只能通过`IntroductionAdvisor`使用引介增强，其中包含以下方法：

```java
public interface IntroductionAdvisor extends Advisor, IntroductionInfo {

    ClassFilter getClassFilter();

    void validateInterfaces() throws IllegalArgumentException;
}

public interface IntroductionInfo {

    Class[] getInterfaces();
}
```

没有`MethodMatcher`，因此没有与引介增强相关的`Pointcut`。只有类过滤是合乎逻辑的。

`getInterfaces()` 方法返回此增强器引入的接口。

`validateInterfaces()`方法在内部用于查看引入的接口是否可以由配置的`IntroductionInterceptor`实现。

考虑 Spring 测试套件中的一个示例，假设我们要将以下接口引入一个或多个对象：

```java
public interface Lockable {
    void lock();
    void unlock();
    boolean locked();
}
```

本例子展示了一个 mixin。我们希望可以将被增强的对象转化为 `Lockable` 的，不在乎它的类型以及调用 `lock` 和 `unlock` 方法。如果我们调用 `lock()` 方法，我们希望所有的 `setter` 方法抛出 `LockedException` 。因此，我们可以通过添加一个切面来提供对象不可变的能力，同时对象本身并不知情。这是 AOP 的一个很好的例子。

首先，我们需要 `IntroductionInterceptor` 来完成繁重的工作。这种情况下，我们扩展 `org.springframework.aop.support.DelegatingIntroductionInterceptor` 方便类。我们可以直接实现 `IntroductionInterceptor` ，但是大多数情况下使用 `DelegatingIntroductionInterceptor` 是最佳选择。

`DelegatingIntroductionInterceptor`旨在委托对引入的接口的实际实现的引介，隐藏拦截的使用。您可以使用构造函数参数将委托设置为任何对象。默认委托（当使用无参数构造函数时）就是`this`。因此，在下一个示例中，委托是`DelegatingIntroductionInterceptor`的`LockMixin`子类。给定委托（默认情况下，自身），`DelegatingIntroductionInterceptor`实例查找委托实现的所有接口（除了`IntroductionInterceptor`）并支持对其中任何接口的引介。`LockMixin`类的子类可以调用`suppressInterface(Class intf)`方法来抑制不应该公开的接口。但是，无论`IntroductionInterceptor`准备支持多少接口，使用`IntroductionAdvisor`来控制实际公开的接口。引入的接口隐藏了目标对同一接口的任何实现。

因此，`LockMixin`扩展了`DelegatingIntroductionInterceptor`并实现了`Lockable`本身。超类自动选择可以支持`Lockable`的引介，因此我们不需要指定。我们可以用这种方式引入任意数量的接口。

注意使用`locked`实例变量。这有效地将附加状态添加到目标对象中保存的状态。

以下示例显示了示例`LockMixin`类：

```java
public class LockMixin extends DelegatingIntroductionInterceptor implements Lockable {

    private boolean locked;

    public void lock() {
        this.locked = true;
    }

    public void unlock() {
        this.locked = false;
    }

    public boolean locked() {
        return this.locked;
    }

    public Object invoke(MethodInvocation invocation) throws Throwable {
        if (locked() && invocation.getMethod().getName().indexOf("set") == 0) {
            throw new LockedException();
        }
        return super.invoke(invocation);
    }

}
```

通常，您不需要覆盖`invoke()`方法。`DelegatingIntroductionInterceptor`实现（如果是被引入的方法则调用 `delegate` 方法，否则进入连接点）通常就足够了。在本例中，我们需要添加一个检查：如果处于锁定模式，则不能调用`setter`方法。

所需的引介只需要保存一个不同的`LockMixin`实例并指定引入的接口（在这种情况下，只能是`Lockable`的）。一个更复杂的例子可能会引用引介拦截器（它将被定义为原型）。在这种情况下，没有与`LockMixin`相关的配置，因此我们使用`new`创建它。以下示例显示了我们的`LockMixinAdvisor`类：

```java
public class LockMixinAdvisor extends DefaultIntroductionAdvisor {

    public LockMixinAdvisor() {
        super(new LockMixin(), Lockable.class);
    }
}
```

我们可以非常简单地应用这个增强器，因为它不需要配置。（但是，没有`IntroductionAdvisor`就不可能使用`IntroductionInterceptor`。）与引介一样，增强器必须是`per-instance` 的，因为它是有状态的。对于每个被增强的对象，我们需要一个不同的`LockMixinAdvisor`实例，因此需要`LockMixin`。增强器构成被增强对象的状态的一部分。

我们可以像其他任何增强器一样，通过在 XML 配置中或（推荐方式）以编程方式通过使用 `Advised.addAdvisor()` 方法应用此增强器。下面讨论的所有代理创建选项，包括“自动代理创建器”，正确处理引介和有状态的混合（stateful mixins）。

