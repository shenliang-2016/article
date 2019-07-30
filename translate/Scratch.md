#### 5.4.4 声明增强

增强与切入点表达式相互关联，在由切入点匹配的方法执行之前、之后或者周围执行。切入点表达式可以时一个命名切入点的引用，也可以是在正确的位置声明的切入点表达式。

##### 前置增强

你可以在一个切面中声明前置增强，通过使用`@Before`注解：

```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;

@Aspect
public class BeforeExample {

    @Before("com.xyz.myapp.SystemArchitecture.dataAccessOperation()")
    public void doAccessCheck() {
        // ...
    }

}
```

如果我们使用一个就地切入点表达式，我们就可以重写前面的例子。如下面例子所示：

```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Before;

@Aspect
public class BeforeExample {

    @Before("execution(* com.xyz.myapp.dao.*.*(..))")
    public void doAccessCheck() {
        // ...
    }

}
```

##### 返回之后的增强

返回之后的增强当匹配到的方法执行正常返回之后才会运行。你可以使用`@AfterReturning`注解来声明它：

```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.AfterReturning;

@Aspect
public class AfterReturningExample {

    @AfterReturning("com.xyz.myapp.SystemArchitecture.dataAccessOperation()")
    public void doAccessCheck() {
        // ...
    }

}
```

> 你可以同时拥有多个增强声明（以及其它成员），都存在于同一个切面中。我们在这些例子中只展示一个增强声明以聚焦于单个增强的影响。

有时候，你需要访问增强体内部以获取时机的方法执行返回值。你可以使用绑定返回值的`@AfterReturning`形式来进行访问，如下面例子所示：

```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.AfterReturning;

@Aspect
public class AfterReturningExample {

    @AfterReturning(
        pointcut="com.xyz.myapp.SystemArchitecture.dataAccessOperation()",
        returning="retVal")
    public void doAccessCheck(Object retVal) {
        // ...
    }

}
```

在`returning`属性中使用的名称必须对应于增强方法中的参数名称。当一个方法执行返回，该返回值就会被传递给增强方法作为其中对应参数的值。一个`returning`子句还限制了仅仅匹配那些返回特定类型值的方法执行（这种情况下，`Object`将匹配所有类型返回值）。

请注意，当使用返回后增强时不可能返回完全不同的引用。

##### 抛出异常后增强

抛出异常后增强当匹配的方法执行抛出异常退出后才会执行。你可以通过使用`@AfterThrowing`注解来声明它。如下面例子所示：

```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.AfterThrowing;

@Aspect
public class AfterThrowingExample {

    @AfterThrowing("com.xyz.myapp.SystemArchitecture.dataAccessOperation()")
    public void doRecoveryActions() {
        // ...
    }

}
```

通常，你可能会希望仅仅在给定类型的异常抛出时才执行增强，同时可能还需要再增强体中访问被抛出的异常。你可以使用`throwing`属性来同时限制匹配（如果需要 - 另外使用`Throwable`作为异常类型）和绑定被抛出的异常到一个增强参数。下面的例子展示了这种做法：

```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.AfterThrowing;

@Aspect
public class AfterThrowingExample {

    @AfterThrowing(
        pointcut="com.xyz.myapp.SystemArchitecture.dataAccessOperation()",
        throwing="ex")
    public void doRecoveryActions(DataAccessException ex) {
        // ...
    }

}
```

`throwing`属性中使用的名称必须对应于增强方法中使用的参数名称。当一个方法执行由于抛出异常而退出时，该异常被传递给增强方法作为相应参数的值。`throwing`子句还限制仅仅匹配抛出特定类型异常（例子中是`DataAccessException`）的方法执行。

##### 后置（最终）增强

后置（最终）增强当匹配的方法执行退出后执行。通过`@After`注解声明。后置增强必须准备好处理正常和异常两种返回情况。典型用法是用来释放资源或者类似目的。下面的例子展示了如何使用：

```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.After;

@Aspect
public class AfterFinallyExample {

    @After("com.xyz.myapp.SystemArchitecture.dataAccessOperation()")
    public void doReleaseLock() {
        // ...
    }

}
```

##### 环绕增强

最后一种增强是环绕增强。环绕增强环绕着匹配的方法执行而执行。它有机会同时在方法执行之前和之后执行，同时决定何时、如何以及甚至是方法实际上是否能够真的执行。环绕增强通常被使用在你需要以线程安全的方式在方法执行之前或者之后进行状态共享的情况，比如启动和停止定时器。请记住，始终使用能够满足你真实需求的最小能力的增强形式（也就是说，如果前置增强够用，就不要使用环绕增强）。

环绕增强使用`@Around`注解声明。增强方法的第一个参数必须是`ProceedingJoinPoint`。在增强体内部，在`ProceedingJoinPoint`上调用`proceed()`将导致被增强的方法的执行。该`proceed`方法还可以传入一个`Object[]`。该数组中的值被作为被增强方法执行的参数。

> 使用`Object[]`调用时，`proceed`的行为与由 AspectJ 编译器编译的环绕增强的行为略有不同。对于使用传统 AspectJ 语言编写的环绕增强，传递给`proceed`的参数数量必须与传递给环绕增强的参数数量（不是基础连接点所采用的参数数量）相匹配，并且传递给的值基于给定的参数位置取代了值绑定到的实体的连接点的原始值（如果现在没有意义，请不要担心）。Spring 采用的方法更简单，与其基于代理的仅执行语义更好地匹配。只是在下面情况下才需要了解这种差异：如果编译为 Spring 编写的 @AspectJ 切面并使用 AspectJ 编译器和编织器参数使用`proceed`。有一种方法可以编写在 Spring AOP 和 AspectJ 上100％兼容的切面，这将在下面的 [增强参数](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-ataspectj-advice-params) 部分中讨论。

下面的例子展示了如何使用环绕增强：

```java
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.ProceedingJoinPoint;

@Aspect
public class AroundExample {

    @Around("com.xyz.myapp.SystemArchitecture.businessService()")
    public Object doBasicProfiling(ProceedingJoinPoint pjp) throws Throwable {
        // start stopwatch
        Object retVal = pjp.proceed();
        // stop stopwatch
        return retVal;
    }

}
```

环绕增强的返回值是方法的调用者能够看到的返回值。比如，一个简单的缓存切面能够从缓存返回一个值，如果缓存中有该值。如果缓存中没有则调用`proceed()`方法。注意`proceed`可能被调用一次、多次、或者根本不是在环绕增强的内部。所有这些情况都是合法的。

##### 增强参数

Spring 提供了完整类型的增强，意味着你应该在增强签名中声明你需要的参数类型，而不是始终使用`Object[]`数组。稍后我们将看到如何使得参数和其它上下文值在增强体中可用。首先，我们看看如何编写通用增强，该增强能够查找到目前正在被增强的方法。

###### 访问当前`JoinPoint`

任何增强方法可用声明，作为它的第一个参数，一个`org.aspectj.lang.JoinPoint`类型的参数。注意，环绕增强需要声明第一个参数类型为`ProceedingJoinPoint`，它是`JoinPoint`的子类）。`JoinPoint`接口提供了一些有用的方法：

- `getArgs()`: 返回方法参数。
- `getThis()`: 返回代理对象。
- `getTarget()`: 返回目标对象。
- `getSignature()`: 返回被增强的方法的描述。
- `toString()`: 打印被增强的方法的有用的描述。

参考 [javadoc](https://www.eclipse.org/aspectj/doc/released/runtime-api/org/aspectj/lang/JoinPoint.html) 获取更多细节。

###### 传递参数给增强

我们已经看到如何绑定返回值或者异常值（使用返回后或者抛出后增强）。为了使得参数值对增强体可用，你可以使用`args`绑定形式。如果你使用参数名称替换参数表达式中的一个类型名称，则当增强被调用时，相应的参数被作为参数值传递。举个例子说明这种情况。假定你希望增强采用`Account`对象作为第一个参数的`DAO`操作的执行，同时你需要访问增强体中的账户数据。你可以像下面例子这样做：

```java
@Before("com.xyz.myapp.SystemArchitecture.dataAccessOperation() && args(account,..)")
public void validateAccount(Account account) {
    // ...
}
```

切入点表达式的`args(account...)`部分服务于两个目的。首先，它限制仅匹配那些携带至少一个参数的方法的执行，同时对应于该形式参数的实际参数就是`Account`实例。其次，它通过参数`account`使得实际的`Account`对象对增强是可用的。

另外一种写法是声明当它匹配到一个连接点时“提供”该`Account`对象值的切入点，然后而可以从增强引用命名的切入点。如下面例子所示：

```java
@Pointcut("com.xyz.myapp.SystemArchitecture.dataAccessOperation() && args(account,..)")
private void accountDataAccessOperation(Account account) {}

@Before("accountDataAccessOperation(account)")
public void validateAccount(Account account) {
    // ...
}
```

参考 AspectJ 编程向导获取更多细节。

代理对象(`this`)，目标对象(`target`)，以及注解(`@within`，`@target`，`@annotation`，以及`@args`)都能以类似的方式绑定。接下来的两个例子展示了如何匹配由`@Auditable`注解修饰的方法的执行并提取审计代码：

两个例子中的第一个展示了`@Auditable`注解的定义：

```java
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
public @interface Auditable {
    AuditCode value();
}
```

第二个例子展示了匹配`@Auditable`方法执行的增强：

```java
@Before("com.xyz.lib.Pointcuts.anyPublicMethod() && @annotation(auditable)")
public void audit(Auditable auditable) {
    AuditCode code = auditable.value();
    // ...
}
```

###### 增强参数和泛型

Spring AOP 能够处理类声明和方法参数中使用的泛型。假设你如下的泛型类型：

Spring AOP can handle generics used in class declarations and method parameters. Suppose you have a generic type like the following:

```java
public interface Sample<T> {
    void sampleGenericMethod(T param);
    void sampleGenericCollectionMethod(Collection<T> param);
}
```

你可以限制拦截的方法的类型为某种参数类型，通过类型化增强参数为你想要拦截的方法的参数类型：

```java
@Before("execution(* ..Sample+.sampleGenericMethod(*)) && args(param)")
public void beforeSampleMethod(MyType param) {
    // Advice implementation
}
```

这种方法对泛型集合无效。因此你可以如下定义一个切入点：

```java
@Before("execution(* ..Sample+.sampleGenericCollectionMethod(*)) && args(param)")
public void beforeSampleMethod(Collection<MyType> param) {
    // Advice implementation
}
```

为了使这种写法可以工作，我们必须检查集合的每个元素，看看哪个是无意义的，因为我们也没办法确定应该如何处理`null`值。为了得到类似的效果，你必须类型化`Collection<?>`参数并手动检查元素类型。

###### 确定参数名称

增强调用中绑定的参数取决于在声明增强中和切入点方法签名中声明参数名称的切入点表达式中使用的匹配到的名称。参数名称无法通过 Java 反射获取，因此 Spring AOP 使用下面的策略来确定参数名称：

- 如果参数名称已经由用户显式指出，则使用指定的参数名称。增强和切入点注解都拥有可选的`argNames`属性，你可以使用它来指定被注解修饰的方法的参数名称。这些参数名称在运行时可用。下面的例子展示了如何使用`argNames`属性：

  ```java
  @Before(value="com.xyz.lib.Pointcuts.anyPublicMethod() && target(bean) && @annotation(auditable)",
          argNames="bean,auditable")
  public void audit(Object bean, Auditable auditable) {
      AuditCode code = auditable.value();
      // ... use code and bean
  }
  ```

  如果第一个参数是`JoinPoint`，`ProceedingJoinPoint`，或者`JoinPoint.Staticpart`类型，你就可以忽略来自`argNames`属性的参数名称。比如，如果你修改上面的增强来接受连接点对象，则`argNames`属性不需要包含它：

  ```java
  @Before(value="com.xyz.lib.Pointcuts.anyPublicMethod() && target(bean) && @annotation(auditable)",
          argNames="bean,auditable")
  public void audit(JoinPoint jp, Object bean, Auditable auditable) {
      AuditCode code = auditable.value();
      // ... use code, bean, and jp
  }
  ```

  给与类型为`JoinPoint`，`ProceedingJoinPoint`，以及`JoinPoint.StaticPart`的第一个参数特殊对待，对那些不收集任何其它连接点上下文的增强实例特别方便。这种情况下，你可以忽略`argNames`属性。比如，下面的增强不需要声明`argNames`属性：

  ```java
  @Before("com.xyz.lib.Pointcuts.anyPublicMethod()")
  public void audit(JoinPoint jp) {
      // ... use jp
  }
  ```

- 使用`argNames`属性有点笨拙，因此如果未指定`argNames`属性，Spring AOP 会查看该类的调试信息，并尝试从局部变量表中确定参数名称。只要已使用调试信息（至少为`-g:vars`）编译类，就会显示此信息。使用此标志进行编译的后果是：（1）您的代码稍微容易理解（逆向工程），（2）类文件大小略大（通常无关紧要），（3）删除未使用的本地变量的优化未由编译器执行。换句话说，通过使用此标志构建，您应该不会遇到任何困难。

> 如果一个 @AspectJ 切面已经由 AspectJ 编译器（ajc）编译，即使没有调试信息，你也不需要添加`argNames`属性，因为编译器维护了必需的信息。

- If the code has been compiled without the necessary debug information, Spring AOP tries to deduce the pairing of binding variables to parameters (for example, if only one variable is bound in the pointcut expression, and the advice method takes only one parameter, the pairing is obvious). If the binding of variables is ambiguous given the available information, an `AmbiguousBindingException` is thrown.如果代码编译时没有必要的调试信息，Spring AOP会尝试推断绑定变量与参数的配对（例如，如果只有一个变量绑定在切入点表达式中，并且增强方法只接受一个参数，那么配对很明显）。如果给定可用信息中变量的绑定是不明确的，则抛出`AmbiguousBindingException`。
- 如果上面所有的策略都失败，则抛出`IllegalArgumentException`异常。

###### 继续论证

我们之前讨论过，我们将描述如何使用在Spring AOP和AspectJ中一致工作的参数编写一个`proceed`调用。解决方案是确保增强签名按顺序绑定每个方法参数。以下示例显示了如何执行此操作：

```java
@Around("execution(List<Account> find*(..)) && " +
        "com.xyz.myapp.SystemArchitecture.inDataAccessLayer() && " +
        "args(accountHolderNamePattern)")
public Object preProcessQueryPattern(ProceedingJoinPoint pjp,
        String accountHolderNamePattern) throws Throwable {
    String newPattern = preProcess(accountHolderNamePattern);
    return pjp.proceed(new Object[] {newPattern});
}
```

很多情况下，你无论如何都要执行这种绑定（如上面例子所示）。

##### 增强排序

当多条增强都想在同一个连接点运行时会发生什么？Spring AOP遵循与AspectJ相同的优先级规则来确定增强执行的顺序。在连接点的执行入口处，最高优先级的增强首先开始执行（因此，给出两条前置增强，优先级最高的增强首先运行）。在连接点执行出口处，最高优先级增强最后运行（因此，给定两条后置增强，具有最高优先级的增强将后运行）。

当在不同切面定义的两条增强都需要在同一个连接点上运行时，除非另行指定，否则执行顺序是不确定的。您可以通过指定优先级来控制执行顺序。这是通过在方法类中实现`org.springframework.core.Ordered`接口或使用`@Order`注解对其进行修饰来以常规Spring方式完成的。给定两个切面，从`Ordered.getValue()`（或注解值）返回较低值的切面具有较高的优先级。

当在同一切面中定义的两条增强都需要在同一个连接点上运行时，排序是未定义的（因为无法通过反射为`javac`编译的类检索声明顺序）。考虑将这些增强方法折叠到每个切面类中每个连接点的一个增强方法中，或者将这些增强重构为可以在切面级别排序的单独切面类。