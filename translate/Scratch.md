启用 @AspectJ 支持之后，在你的应用上下文中定义的任何对应于 @AspectJ 切面的类的 bean (被 `@AspectJ`注解修饰)都会被 Spring 自动检测并被用于配置 Spring AOP。下面两个例子展示了一个切面的最小定义需求。

第一个例子展示了应用上下文中的一个普通 bean 定义，该定义指向一个由`@Aspect`注解修饰的类：

```xml
<bean id="myAspect" class="org.xyz.NotVeryUsefulAspect">
    <!-- configure properties of the aspect here -->
</bean>
```

第二个例子展示了`NotVeryUsefulAspect`类定义，由`org.aspectj.lang.annotation.Aspect`注解修饰：

```java
package org.xyz;
import org.aspectj.lang.annotation.Aspect;

@Aspect
public class NotVeryUsefulAspect {

}
```

切面（由`@Aspect`注解修饰的类）能够拥有方法和字段，与其他所有类一样。它们也能够包含切入点、增强，以及引介（跨类型）声明。

> 通过组件扫描自动探测切面
>
> 你可以在你的 Spring XML 配置中作为普通 beans 注册切面类，或者通过类路径扫描自动探测它们 - 就像其他任何由 Spring 管理的 bean。然而，注意`@Aspect`和`@Component`。

> 用切面来增强切面？
>
> 在 Spring AOP 中，切面自身不能作为其他切面的增强目标。一个类上的`@Aspect`注解将该类标记为一个切面，同时，也将该类排除在自动代理范围之外。

#### 5.4.3 声明切入点

切入点确定感兴趣的连接点，从而使我们能够控制增强何时执行。Spring AOP仅支持Spring bean的方法执行连接点，因此您可以将切入点视为匹配Spring bean上方法的执行。切入点声明有两个部分：一个包含名称和任何参数的签名，以及一个精确确定我们感兴趣的方法执行的切入点表达式。在AOP的@AspectJ注解样式中，切入点签名由常规方法定义提供 ，并使用`@Pointcut`注解指示切入点表达式（用作切入点签名的方法必须具有`void`返回类型）。

一个例子可以让这种切入点签名和切入点表达式的讨论更加清晰一些。下面的例子定义一个名为`anyOldTransfer`的切入点，它匹配所有名为`transfer`的方法的执行：

An example may help make this distinction between a pointcut signature and a pointcut expression clear. The following example defines a pointcut named `anyOldTransfer` that matches the execution of any method named `transfer`:

```java
@Pointcut("execution(* transfer(..))")// the pointcut expression
private void anyOldTransfer() {}// the pointcut signature
```

形成`@Pointcut`注解值的切入点表达式是一个常规的AspectJ 5切入点表达式。有关AspectJ切入点语言的完整讨论，请参阅 [AspectJ编程指南](https://www.eclipse.org/aspectj/doc/released/progguide/index.html)（对于扩展，参考 [AspectJ 5 Developer's Notebook](https://www.eclipse.org/aspectj/doc/released/adk15notebook/index.html)）或关于AspectJ的书籍之一（例如*Eclipse AspectJ*，Colyer等人著，或*AspectJ in Action*，作者：Ramnivas Laddad）。

##### 支持的切入点指示符

Spring AOP 支持下列 AspectJ 切入点指示符（PCD）用在切入点表达式中：

- `execution`: 匹配方法执行连接点。这是使用 Spring AOP 时主要的切入点指示符。
- `within`: 限制匹配某些类型中的连接点（使用Spring AOP时在匹配类型中声明的方法的执行）。
- `this`: 限制与连接点的匹配（使用Spring AOP时的方法执行），其中bean引用（Spring AOP代理）是给定类型的实例。
- `target`: 限制匹配连接点（使用Spring AOP时的方法执行），其中目标对象（被代理的应用程序对象）是给定类型的实例。
- `args`: 限制与连接点的匹配（使用Spring AOP时方法的执行），其中参数是给定类型的实例。
- `@target`: 限制与连接点的匹配（使用Spring AOP时方法的执行），其中执行对象的类具有给定类型的注释。
- `@args`: 限制与连接点的匹配（使用Spring AOP时方法的执行），其中传递的实际参数的运行时类型具有给定类型的注释。
- `@within`: 限制与具有给定注解的类型中的连接点的匹配（使用Spring AOP时在具有给定注解的类型中声明的方法的执行）。
- `@annotation`: 限制连接点的匹配，其中连接点的主题（在Spring AOP中执行的方法）具有给定的注释。

> 其他切入点类型
>
> 完整的 AspectJ 切入点语言支持 Spring 不支持的额外的切入点指示符： `call`, `get`, `set`, `preinitialization`, `staticinitialization`, `initialization`, `handler`, `adviceexecution`, `withincode`, `cflow`,`cflowbelow`, `if`, `@this`, 以及 `@withincode` 。在Spring AOP解释的切入点表达式中使用这些切入点指示符会导致抛出`IllegalArgumentException`。
>
> Spring AOP支持的切入点指示符集可以在将来的版本中进行扩展，以支持更多的AspectJ切入点指示符。

