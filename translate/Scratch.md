#### 5.10.3 使用 Spring IoC 配置 AspectJ 切面

当你在 Spring 应用中使用 AspectJ 时，很自然地会希望并期待能够使用 Spring 配置这些切面。AspectJ 运行时本身负责切面创建，并且通过 Spring 配置 AspectJ 创建的切面的含义依赖于切面使用的 AspectJ 实例化模型（`per-xxx`子句）。

大部分的 AspectJ 切面是单例模式的切面。配置这些切面很容易。你可以创建一个 bean 定义，正常引用切面类型并包含`factory-method="aspectOf"` bean 属性。这就保证了 Spring 可以通过询问 AspectJ 获取该切面实例，而不需要自己创建切面实例。下面的例子展示了如何使用`factory-method="aspectOf"`属性。

```xml
<bean id="profiler" class="com.xyz.profiler.Profiler"
        factory-method="aspectOf"> <!-- Note the factory-method="aspectOf" attribute -->

    <property name="profilingStrategy" ref="jamonProfilingStrategy"/>
</bean>
```

非单例的切面更难配置。不过，通过创建原型 bean 定义并使用来自`spring-aspects.jar`的`@Configurable`来配置该切面实例是可能的，一旦它们被 AspectJ 运行时创建。

如果你有一些你希望使用 AspectJ 织入（比如，为域模型类型使用加载时织入）的 @AspectJ 切面，另外一些你希望使用 Spring AOP 进行织入，并且这些切面都在 Spring 中配置，你需要告诉 Spring AOP @AspectJ 自动代理支持，它是定义在应该被用于自动代理的配置中的 @AspectJ 切面的子集。你可以这么做，通过在`<aop:aspectj-autoproxy/>`声明内部使用一个或者多个`<include/>`元素。每个`<include/>`元素指定一个名称模式，并且只有名称匹配到至少一个名称模式的 bean 才会被用于 Spring AOP 自动代理配置。下面的例子展示了如何使用`<include/>`元素：

```xml
<aop:aspectj-autoproxy>
    <aop:include name="thisBean"/>
    <aop:include name="thatBean"/>
</aop:aspectj-autoproxy>
```
> 不要被`<aop:aspectj-autoproxy/>`元素的名称误导。使用它会导致创建 Spring AOP 代理。这里使用@AspectJ 样式的方面声明，但不涉及 AspectJ 运行时。

#### 5.10.4 在 Spring 框架中使用 AspectJ 进行加载时织入

加载时编织（LTW）是指在将 AspectJ 切面加载到 Java 虚拟机（JVM）中时将其编织到应用程序的类文件中的过程。本节的重点是在 Spring Framework 的特定上下文中配置和使用 LTW。本节不是 LTW 的一般介绍。有关 LTW 细节的详细信息以及仅使用 AspectJ 配置 LTW（不涉及 Spring），请参阅 [AspectJ开发环境指南的LTW部分](https://www.eclipse.org/aspectj/doc/released/devguide/ltw.html) 。

Spring Framework 为 AspectJ LTW 带来的价值在于对编织过程进行更精细的控制。“Vanilla” AspectJ LTW 通过使用 Java（5+）代理来实现，该代理通过在启动 JVM 时指定 VM 参数来启用。因此，它是一个 JVM 范围的设置，在某些情况下可能很好，但通常有点过于粗糙。支持 Spring 的 LTW 允许您在每个`ClassLoader`的基础上打开 LTW，这更精细，并且在“单 JVM 多应用程序”环境中更有意义（例如在典型的应用程序服务器环境）。

进一步地，在 [某些环境](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-aj-ltw-environments) 下，这种支持启动加载时织入，而不需要修改应用服务器启动脚本，该脚本需要添加 `-javaagent:path/to/aspectjweaver.jar` 或者 `-javaagent:path/to/spring-instrument.jar`。开发者通过配置应用上下文来启用加载时织入，而不需要依赖负责部署配置（比如启动脚本）的应用管理员。

现在初步介绍已经结束，让我们首先介绍使用 Spring 的 AspectJ LTW 的快速示例，然后详细介绍示例中使用的元素。有关完整示例，请参阅 [Petclinic sample application](https://github.com/spring-projects/spring-petclinic) 。

##### 第一个例子

假设您是一名应用程序开发人员，负责诊断系统中某些性能问题。我们将打开一个简单的分析切面，让我们快速获得一些性能指标，而不是直接使用分析工具。然后，我们可以立即将精细的分析工具应用于该特定区域。

> 此处提供的示例使用 XML 配置。您还可以使用[Java configuration](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java) 配置和使用 @AspectJ。具体来说，您可以使用`@EnableLoadTimeWeaving`注解作为`<context:load-time-weaver/>`的替代方法（详见下文）。

