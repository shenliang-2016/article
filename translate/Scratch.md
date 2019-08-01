#### 5.5.3 声明增强

基于模式的 AOP 支持使用 @AspectJ 风格支持的相同的 5 种增强，同时它们具有完全相同的语义。

##### 前置增强

前置增强运行在匹配的方法执行之前。它在`<aop:aspect>`元素中使用 <aop:before> 元素声明，如下所示：

```xml
<aop:aspect id="beforeExample" ref="aBean">

    <aop:before
        pointcut-ref="dataAccessOperation"
        method="doAccessCheck"/>

    ...

</aop:aspect>
```

这里，`dataAccessOperation`是定义在顶级（`<aop:config>`）的切入点的`id`。为了以行内形式定义该切入点，以`pointcut`属性替换`pointcut-ref`属性，如下所示：

```xml
<aop:aspect id="beforeExample" ref="aBean">

    <aop:before
        pointcut="execution(* com.xyz.myapp.dao.*.*(..))"
        method="doAccessCheck"/>

    ...

</aop:aspect>
```

如我们在 @AspectJ 风格的讨论中提到的，使用命名的切入点可以显著改善代码的可读性。

`method`属性指示一个方法（`doAccessCheck`），该方法提供增强的主体。该方法必须为包含该增强的切面元素引用的 bean 定义。在数据访问操作执行（由切入点表达式匹配的方法执行连接点）之前，切面 bean 上的`doAccessCheck`方法被调用。

##### 返回之后增强

当匹配到的方法正常执行完成之后才会执行返回之后增强。它的声明方式与前置增强一样。如下面例子所示：

```xml
<aop:aspect id="afterReturningExample" ref="aBean">

    <aop:after-returning
        pointcut-ref="dataAccessOperation"
        method="doAccessCheck"/>

    ...

</aop:aspect>
```

如在 @AspectJ 风格中那样，你可以在增强主体中获取返回值。为了做到这一点，使用`returning`属性来指定返回值应该被传递给的参数的名称，如下面例子所示：

```xml
<aop:aspect id="afterReturningExample" ref="aBean">

    <aop:after-returning
        pointcut-ref="dataAccessOperation"
        returning="retVal"
        method="doAccessCheck"/>

    ...

</aop:aspect>
```

`doAccessCheck`方法必须声明一个参数名`retVal`。该参数的类型如`@AfterReturning`中描述的同样的方式约束匹配。比如，你可以如下声明方法签名：

```java
public void doAccessCheck(Object retVal) {...
```

##### 抛出异常之后增强

匹配的方法执行由于抛出异常而退出之后才会执行这种增强。定义形式如下：

```xml
<aop:aspect id="afterThrowingExample" ref="aBean">

    <aop:after-throwing
        pointcut-ref="dataAccessOperation"
        method="doRecoveryActions"/>

    ...

</aop:aspect>
```

如在 @AspectJ 风格中那样，你可以在增强主体中获取抛出的异常。为了做到这一点，使用`throwing`属性来指定异常应该被传递给的参数的名称，如下面例子所示：

```xml
<aop:aspect id="afterThrowingExample" ref="aBean">

    <aop:after-throwing
        pointcut-ref="dataAccessOperation"
        throwing="dataAccessEx"
        method="doRecoveryActions"/>

    ...

</aop:aspect>
```

`doRecoveryActions`方法必须声明一个参数名`dataAccessEx`。该参数的类型如`@AfterThrowing`中描述的同样的方式约束匹配。比如，你可以如下声明方法签名：

```java
public void doRecoveryActions(DataAccessException dataAccessEx) {...
```

##### 后置（最终）增强

后置（最终）增强无论匹配的方法执行如何退出都会运行。你可以使用`after`元素，如下面例子所示：

```xml
<aop:aspect id="afterFinallyExample" ref="aBean">

    <aop:after
        pointcut-ref="dataAccessOperation"
        method="doReleaseLock"/>

    ...

</aop:aspect>
```

##### 环绕增强

最后一种增强是环绕增强。环绕增强围绕匹配的方法执行运行。它有机会在方法执行之前和之后完成工作，并能够决定方法何时，如何，甚至方法实际上能否执行。环绕增强通常用于以线程安全的方式（例如，启动和停止计时器）在方法执行之前和之后共享状态。始终使用符合您要求的最不强大的增强形式。如果前置增强够用，就不要使用环绕增强。

您可以使用`<aop:around>`元素声明环绕增强。`advice`方法的第一个参数必须是`ProceedingJoinPoint`类型。在增强的主体内，在`ProceedingJoinPoint`上调用`proceed()`会导致执行基础方法。也可以使用`Object[]`调用`proceed`方法。数组中的值在进行时用作方法执行的参数。有关使用`Object[]`调用`proceed`的说明，请参阅 [Around Advice](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-ataspectj-around-advice) 。以下示例显示如何在XML中声明环绕增强：

```xml
<aop:aspect id="aroundExample" ref="aBean">

    <aop:around
        pointcut-ref="businessService"
        method="doBasicProfiling"/>

    ...

</aop:aspect>
```

`doBasicProfiling`增强的实现可以和 @AspectJ 例子中完全一样（当然是要去掉注解），如下面例子所示：

```java
public Object doBasicProfiling(ProceedingJoinPoint pjp) throws Throwable {
    // start stopwatch
    Object retVal = pjp.proceed();
    // stop stopwatch
    return retVal;
}
```

##### 增强参数

基于模式的声明样式支持完全类型化的增强，方法与@AspectJ支持描述的方式相同 - 通过名称将切入点参数与增强方法参数相匹配。有关详细信息，请参阅 [Advice Parameters](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-ataspectj-advice-params) 。如果您希望显式指定增强方法的参数名称（不依赖于前面描述的检测策略），可以使用`advice`元素的`arg-names`属性来实现，在增强注解中（如  [Determining Argument Names](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-ataspectj-advice-params-names) 中所述），该属性的处理方式与`argNames`属性相同。以下示例显示如何在XML中指定参数名称：

```xml
<aop:before
    pointcut="com.xyz.lib.Pointcuts.anyPublicMethod() and @annotation(auditable)"
    method="audit"
    arg-names="auditable"/>
```

`arg-names`属性接受一个逗号分隔的参数名称列表。

以下稍微涉及的基于XSD的方法示例显示了一些与一系列强类型参数一起使用的环绕增强：

```java
package x.y.service;

public interface PersonService {

    Person getPerson(String personName, int age);
}

public class DefaultFooService implements FooService {

    public Person getPerson(String name, int age) {
        return new Person(name, age);
    }
}
```

接下来是切面。请注意，`profile(..)`方法接受多个强类型参数，第一个参数恰好是用于执行方法调用的连接点。此参数的存在表示 `profile(..)` 将被用作`around`增强，如以下示例所示：

```java
package x.y;

import org.aspectj.lang.ProceedingJoinPoint;
import org.springframework.util.StopWatch;

public class SimpleProfiler {

    public Object profile(ProceedingJoinPoint call, String name, int age) throws Throwable {
        StopWatch clock = new StopWatch("Profiling for '" + name + "' and '" + age + "'");
        try {
            clock.start(call.toShortString());
            return call.proceed();
        } finally {
            clock.stop();
            System.out.println(clock.prettyPrint());
        }
    }
}
```

最后，以下示例XML配置会影响特定连接点的上面这个增强的执行：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop https://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- this is the object that will be proxied by Spring's AOP infrastructure -->
    <bean id="personService" class="x.y.service.DefaultPersonService"/>

    <!-- this is the actual advice itself -->
    <bean id="profiler" class="x.y.SimpleProfiler"/>

    <aop:config>
        <aop:aspect ref="profiler">

            <aop:pointcut id="theExecutionOfSomePersonServiceMethod"
                expression="execution(* x.y.service.PersonService.getPerson(String,int))
                and args(name, age)"/>

            <aop:around pointcut-ref="theExecutionOfSomePersonServiceMethod"
                method="profile"/>

        </aop:aspect>
    </aop:config>

</beans>
```

请考虑以下驱动程序脚本：

```java
import org.springframework.beans.factory.BeanFactory;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import x.y.service.PersonService;

public final class Boot {

    public static void main(final String[] args) throws Exception {
        BeanFactory ctx = new ClassPathXmlApplicationContext("x/y/plain.xml");
        PersonService person = (PersonService) ctx.getBean("personService");
        person.getPerson("Pengo", 12);
    }
}
```

使用这样的`Boot`类，我们将在标准输出上获得类似于以下内容的输出：

```
StopWatch 'Profiling for 'Pengo' and '12'': running time (millis) = 0
-----------------------------------------
ms     %     Task name
-----------------------------------------
00000  ?  execution(getFoo)
```

##### 增强顺序

当多个增强需要在同一个连接点（执行方法）执行时，排序规则如 [Advice Ordering](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-ataspectj-advice-ordering) 中所述。切面之间的优先级是通过将`Order`注解添加到支持该切面的 bean 上或通过让 bean 实现`Ordered`接口来确定的。

