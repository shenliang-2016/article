下面的例子展示了配置切面，它是有用的。他是一个基于时间的配置器，使用 @AspectJ 风格的切面声明：

```java
package foo;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Aspect;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Pointcut;
import org.springframework.util.StopWatch;
import org.springframework.core.annotation.Order;

@Aspect
public class ProfilingAspect {

    @Around("methodsToBeProfiled()")
    public Object profile(ProceedingJoinPoint pjp) throws Throwable {
        StopWatch sw = new StopWatch(getClass().getSimpleName());
        try {
            sw.start(pjp.getSignature().getName());
            return pjp.proceed();
        } finally {
            sw.stop();
            System.out.println(sw.prettyPrint());
        }
    }

    @Pointcut("execution(public * foo..*.*(..))")
    public void methodsToBeProfiled(){}
}
```

我们还需要创建一个 `META-INF/aop.xml` 文件，告知 AspectJ 编织器我们想要将 `ProfilingAspect` 织入我们自己的类中。此文件约定，在 Java 类路径中存在名为 `META-INF/aop.xml` 的文件（或多个文件）是标准的 AspectJ。下面的例子展示了 `aop.xml` 文件：

```xml
<!DOCTYPE aspectj PUBLIC "-//AspectJ//DTD//EN" "https://www.eclipse.org/aspectj/dtd/aspectj.dtd">
<aspectj>

    <weaver>
        <!-- only weave classes in our application-specific packages -->
        <include within="foo.*"/>
    </weaver>

    <aspects>
        <!-- weave in just this aspect -->
        <aspect name="foo.ProfilingAspect"/>
    </aspects>

</aspectj>
```

现在我们可以继续介绍特定于 Spring 的配置部分。我们需要配置一个 `LoadTimeWeaver` （稍后解释）。此加载期编织器是基本的组件，负责将一个或者多个 `META-INF/aop.xml` 文件中配置的切面织入到你的应用中的类中。好消息是它不需要大量配置（你可以指定其它一些选项，后续介绍），如下面例子所示：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <!-- a service object; we will be profiling its methods -->
    <bean id="entitlementCalculationService"
            class="foo.StubEntitlementCalculationService"/>

    <!-- this switches on the load-time weaving -->
    <context:load-time-weaver/>
</beans>
```

现在，所有必须的工件（切面，`META-INF/aop.xml` 文件，以及 Spring 配置）都已到位，我们可以使用 `main(..)` 方法创建下面的驱动类，以演示 LTW 运行过程：

```java
package foo;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public final class Main {

    public static void main(String[] args) {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("beans.xml", Main.class);

        EntitlementCalculationService entitlementCalculationService =
                (EntitlementCalculationService) ctx.getBean("entitlementCalculationService");

        // the profiling aspect is 'woven' around this method execution
        entitlementCalculationService.calculateEntitlement();
    }
}
```

我们还有最后一件事要做。本节的介绍确实说可以在 Spring 的基础上有选择地在每个 `ClassLoader` 的基础上打开 LTW，这是事实。但是，对于此示例，我们使用 Java 代理（随 Spring 提供）来打开 LTW。我们使用以下命令来运行前面显示的 `Main` 类：

```
java -javaagent:C:/projects/foo/lib/global/spring-instrument.jar foo.Main
```

`-javaagent`是一个标志，用于指定和启用代理程序来检测在 JVM 上运行的程序。Spring Framework附带了一个代理程序`InstrumentationSavingAgent`，它包装在`spring-instrument.jar`中，该函数作为前面示例中`-javaagent`参数的值提供。

执行`Main`程序的输出类似于下一个示例。（我在`calculateEntitlement()`实现中引入了一个`Thread.sleep(..)`语句，以便探查器实际捕获0毫秒以外的东西（`01234`毫秒不是AOP引入的开销）。下面的清单显示了运行我们的探查器时得到的输出：

```
Calculating entitlement

StopWatch 'ProfilingAspect': running time (millis) = 1234
------ ----- ----------------------------
ms     %     Task name
------ ----- ----------------------------
01234  100%  calculateEntitlement
```

由于LTW是通过使用成熟的AspectJ实现的，因此我们不仅限于为Spring bean提供增强。`Main`程序的以下细微变化产生相同的结果：

```java
package foo;

import org.springframework.context.support.ClassPathXmlApplicationContext;

public final class Main {

    public static void main(String[] args) {
        new ClassPathXmlApplicationContext("beans.xml", Main.class);

        EntitlementCalculationService entitlementCalculationService =
                new StubEntitlementCalculationService();

        // the profiling aspect will be 'woven' around this method execution
        entitlementCalculationService.calculateEntitlement();
    }
}
```

请注意，在前面的程序中，我们如何引导Spring容器，然后在Spring的上下文之外创建一个新的`StubEntitlementCalculationService`实例。剖析增强仍编织其中。

不可否认，这个例子很简单。 但是，Spring中LTW支持的基础知识已在前面的示例中引入，本节的其余部分详细说明了每个配置和使用位置背后的“原因”。

> 本例中使用的`ProfilingAspect`可能是基本的，但它非常有用。这是开发人员在开发期间可以使用的开发期切面的一个很好的示例，然后可以轻松地从部署到UAT或生产中的应用程序的构建中排除。

