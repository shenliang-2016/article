##### 组合切入点表达式

你可以通过使用`&&`，`||`以及`!`组合切入点表达式。你还可以使用名称指代切入点表达式。下面的例子展示了 3 个切入点表达式：

```java
@Pointcut("execution(public * *(..))")
private void anyPublicOperation() {} 

@Pointcut("within(com.xyz.someapp.trading..*)")
private void inTrading() {} 

@Pointcut("anyPublicOperation() && inTrading()")
private void tradingOperation() {} 

```

* `anyPublicOperation` 如果方法执行连接点表示所有公共方法的执行则匹配成功。
* `inTrading` 如果方法执行在`trading`模块中则匹配成功。
* `tradingOperation` 如果方法执行表示任何`trading`模块中公共方法则匹配成功。

如前所示，最好从较小的命名组件构建更复杂的切入点表达式。当按名称引用切入点时，将应用常规Java可见性规则（您可以看到相同类型的`private`切入点，层次结构中的受`protected`切入点，任何位置的`public`切入点等）。可见性不会影响切入点匹配。

##### 共享通用切入点定义

在使用企业应用程序时，开发人员通常希望从几个方面引用应用程序的模块和特定的操作集。我们建议定义一个“SystemArchitecture”切面，捕获为此目的常见的切入点表达式。这样的切面通常类似于以下示例：

```java
package com.xyz.someapp;

import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Pointcut;

@Aspect
public class SystemArchitecture {

    /**
     * A join point is in the web layer if the method is defined
     * in a type in the com.xyz.someapp.web package or any sub-package
     * under that.
     */
    @Pointcut("within(com.xyz.someapp.web..*)")
    public void inWebLayer() {}

    /**
     * A join point is in the service layer if the method is defined
     * in a type in the com.xyz.someapp.service package or any sub-package
     * under that.
     */
    @Pointcut("within(com.xyz.someapp.service..*)")
    public void inServiceLayer() {}

    /**
     * A join point is in the data access layer if the method is defined
     * in a type in the com.xyz.someapp.dao package or any sub-package
     * under that.
     */
    @Pointcut("within(com.xyz.someapp.dao..*)")
    public void inDataAccessLayer() {}

    /**
     * A business service is the execution of any method defined on a service
     * interface. This definition assumes that interfaces are placed in the
     * "service" package, and that implementation types are in sub-packages.
     *
     * If you group service interfaces by functional area (for example,
     * in packages com.xyz.someapp.abc.service and com.xyz.someapp.def.service) then
     * the pointcut expression "execution(* com.xyz.someapp..service.*.*(..))"
     * could be used instead.
     *
     * Alternatively, you can write the expression using the 'bean'
     * PCD, like so "bean(*Service)". (This assumes that you have
     * named your Spring service beans in a consistent fashion.)
     */
    @Pointcut("execution(* com.xyz.someapp..service.*.*(..))")
    public void businessService() {}

    /**
     * A data access operation is the execution of any method defined on a
     * dao interface. This definition assumes that interfaces are placed in the
     * "dao" package, and that implementation types are in sub-packages.
     */
    @Pointcut("execution(* com.xyz.someapp.dao.*.*(..))")
    public void dataAccessOperation() {}

}
```

您可以在需要切入点表达式的任何位置引用此类切面中定义的切入点。例如，要使服务层成为事务性的，您可以编写以下内容：

```xml
<aop:config>
    <aop:advisor
        pointcut="com.xyz.someapp.SystemArchitecture.businessService()"
        advice-ref="tx-advice"/>
</aop:config>

<tx:advice id="tx-advice">
    <tx:attributes>
        <tx:method name="*" propagation="REQUIRED"/>
    </tx:attributes>
</tx:advice>
```

`<aop:config>` and `<aop:advisor>`元素在 [Schema-based AOP Support](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-schema) 中讨论。事务元素在 [Transaction Management](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/data-access.html#transaction) 中讨论、

##### 例子

Spring AOP 用户大部分情况下会可能使用 `execution` 切入点指示符。执行表达式的格式如下：

```
execution(modifiers-pattern? ret-type-pattern declaring-type-pattern?name-pattern(param-pattern)
            throws-pattern?)
```

除了返回类型模式（前面代码片段中的`ret-type-pattern`），名称模式和参数模式之外的所有部分都是可选的。返回类型模式确定方法的返回类型必须是什么才能匹配连接点。`*`最常用作返回类型模式。它匹配任何返回类型。仅当方法返回给定类型时，完全限定类型名称才匹配。名称模式与方法名称匹配。您可以使用`*`通配符作为名称模式的全部或部分。如果指定声明类型模式，请包含一个尾随的`.`以将其连接到名称模式组件。参数模式稍微复杂一些：`()`匹配一个不带参数的方法，而`(..)`匹配任何数量（零个或多个）参数。`(*)`模式匹配一个采用任何类型的一个参数的方法。 `(*，String)`匹配一个带两个参数的方法。第一个可以是任何类型，而第二个必须是`String`。有关详细信息，请参阅AspectJ编程指南的 [语言语义](https://www.eclipse.org/aspectj/doc/released/progguide/semantics-pointcuts.html) 部分。

下面的例子展示了一些常见的切入点表达式：

- 任何`public`方法的执行：

  ```java
  execution(public * *(..))
  ```

- 任何方法名以`set`开头的方法的执行：

  ```java
  execution(* set*(..))
  ```

- 任何由`AccountService`接口定义的方法的执行：

  ```java
  execution(* com.xyz.service.AccountService.*(..))
  ```

- 在`service`包中定义的任何方法的执行：

  ```java
  execution(* com.xyz.service.*.*(..))
  ```

- 在`service`包及其子包中定义的任何方法的执行：

  ```java
  execution(* com.xyz.service..*.*(..))
  ```

- `service`包内部任何连接点（仅 Spring AOP 中的方法执行）：

  ```java
  within(com.xyz.service.*)
  ```

- `service`包及其子包内部任何连接点（仅 Spring AOP 中的方法执行）：

  ```java
  within(com.xyz.service..*)
  ```

- 实现了`AccountService`接口的代理中的任何连接点（仅 Spring AOP 中的方法执行）：

  ```java
  this(com.xyz.service.AccountService)
  ```
  
> `this`更常用于绑定形式。有关如何在增强体中使得代理对象可用，请参阅 [声明增强](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-advice) 部分。

* 目标对象实现了`AccountService`接口的任何连接点（仅 Spring AOP 中的方法执行）：

  ```java
  target(com.xyz.service.AccountService)
  ```

> 您还可以在以绑定形式使用“@target”。有关如何在增强体中使得注解对象可用，请参阅 [声明增强](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-advice) 部分。

- 声明的目标对象类型拥有`@Transactional`注解的任何连接点（仅 Spring AOP 中的方法执行）：

  ```java
  @within(org.springframework.transaction.annotation.Transactional)
  ```

> 您还可以在以绑定形式使用“@within”。有关如何在增强体中使得注解对象可用，请参阅 [声明增强](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-advice) 部分。

- 执行的方法拥有`@Transactional`注解的任何连接点（仅 Spring AOP 中的方法执行）：

  ```java
  @annotation(org.springframework.transaction.annotation.Transactional)
  ```

> 您还可以在以绑定形式使用“@annotation”。有关如何在增强体中使得注解对象可用，请参阅 [声明增强](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-advice) 部分。

- 携带单独一个参数，该参数的运行时类型拥有`@Classified`注解的任何连接点（仅 Spring AOP 中的方法执行）：

  ```java
  @args(com.xyz.security.Classified)
  ```

> 您还可以在以绑定形式使用“@args”。有关如何在增强体中使得注解对象可用，请参阅 [声明增强](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-advice) 部分。

- 名为`tradeServcie`的 Spring bean 上的任何连接点（仅 Spring AOP 中的方法执行）：

  ```java
  bean(tradeService)
  ```

- 名称匹配到通配符表达式`*Service`的 Spring bean 上的任何连接点（仅 Spring AOP 中的方法执行）：

  ```java
  bean(*Service)
  ```

##### 编写好的切入点

在编译期，AspectJ处理切入点以优化匹配性能。检查代码并确定每个连接点是否（静态地或动态地）匹配给定切入点是一个代价高昂的过程。（动态匹配意味着无法通过静态分析完全确定匹配，并且在代码中放置测试以确定代码运行时是否存在实际匹配）。在第一次遇到切入点声明时，AspectJ会将其重写为匹配过程的最佳形式。这是什么意思？基本上，切入点在 DNF（析取范式）中重写，并且切入点的组件被排序，以便首先检查那些评估更方便的组件。这意味着您不必担心了解各种切入点指示符的性能，并且可以在切入点声明中以任何顺序提供它们。

但是，AspectJ只能使用它所被告知的内容。为了获得最佳匹配性能，您应该考虑它们要实现的目标，并在定义中尽可能缩小匹配的搜索空间。现有的指示符自然分为三组：`kinded`，`scoping`和`contextual`：

- Kinded 指示符选择特定类型的连接点: `execution`, `get`, `set`, `call`, 和 `handler`。
- Scoping 指示符选择一组感兴趣的连接点，可能包含许多类: `within` 和 `withincode`。
- Contextual 指示符基于上下文匹配（以及可选绑定）: `this`, `target`, 和 `@annotation`。

一个写得很好的切入点应至少包括前两种类型（`kinded`和`scoping`）。您可以包含上下文指示符以基于连接点上下文进行匹配，或者绑定该上下文以在增强中使用。由于额外的处理和分析，仅提供一个`kinded`指示符或仅提供上下文指示符，但可能会影响编织性能（使用的时间和内存）。范围界定指示符非常快速匹配，使用它们意味着AspectJ可以非常快速地解除不应进一步处理的连接点组。如果可能，一个好的切入点应该总是包含一个。

