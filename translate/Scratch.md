##### 切面

您在 LTW 中使用的切面必须是 AspectJ 切面。您可以使用 AspectJ 语言本身编写它们，也可以使用 @AspectJ 样式编写切面。那么你的切面都是有效的 AspectJ 和 Spring AOP 切面。此外，编译好的切面类需要在类路径上可用。

##### META-INF/aop.xml

通过使用 Java 类路径上的一个或多个 `META-INF/aop.xml` 文件（直接或更常见地，在 jar 文件中）配置 AspectJ  LTW 基础结构。

 [AspectJ reference documentation](https://www.eclipse.org/aspectj/doc/released/devguide/ltw-configuration.html) 的 LTW 部分详细介绍了此文件的结构和内容。因为 `aop.xml` 文件是100％ AspectJ，所以我们在此不再进一步描述。

##### 必需类库 (JARS)

为了使用 Spring Framework 的 AspectJ LTW 支持，你必需以下类库：

- `spring-aop.jar`
- `aspectjweaver.jar`

想要使用 [Spring-provided agent to enable instrumentation](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-aj-ltw-environment-generic)，你还需要：

- `spring-instrument.jar`

##### Spring 配置

Spring 的 LTW 支持的关键组件是 `LoadTimeWeaver` 接口（在`org.springframework.instrument.classloading` 包中），以及随 Spring 发行版一起提供的众多实现。`LoadTimeWeaver` 负责在运行时将一个或多个`java.lang.instrument.ClassFileTransformers` 添加到 `ClassLoader`，这为各种有趣的应用程序打开了大门，其中一个恰好是切面的 LTW。

> 如果您不熟悉运行时类文件转换的概念，请在继续之前查看 `java.lang.instrument` 包的 javadoc API文档。虽然该文档并不全面，但至少可以看到关键接口和类（供您阅读本节时参考）。

为特定的 `ApplicationContext` 配置 `LoadTimeWeaver` 就像添加一行代码一样简单。（请注意，您几乎肯定需要使用 `ApplicationContext` 作为Spring容器 - 通常，`BeanFactory` 是不够的，因为 LTW 支持使用 `BeanFactoryPostProcessors`。）

要启用 Spring Framework 的 LTW 支持，您需要配置 `LoadTimeWeaver`，通常使用 `@EnableLoadTimeWeaving` 注解来完成，如下所示：

```java
@Configuration
@EnableLoadTimeWeaving
public class AppConfig {
}
```

另外，如果你更喜欢基于 XML 的配置，使用 `<context:load-time-weaver/>` 元素。注意该元素定义在 `context` 命名空间中。下面的例子展示了如何使用 `<context:load-time-weaver/>` ：

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

    <context:load-time-weaver/>

</beans>
```

上面的配置为你自动定义并注册一系列的特定于 LTW 的基础设施 beans，比如 `LoadTimeWeaver` 以及 `AspectJWeavingEnabler` 。默认的 `LoadTimeWeaver` 是 `DefaultContextLoadTimeWeaver` 类，试图装饰自动探测到的 `LoadTimeWeaver` 。“自动探测到的” `LoadTimeWeaver` 的精确类型取决于你的运行环境。下表展示了各种 `LoadTimeWeaver` 实现：

| Runtime Environment                      | `LoadTimeWeaver` implementation |
| ---------------------------------------- | ------------------------------- |
| Running in [Apache Tomcat](https://tomcat.apache.org/) | `TomcatLoadTimeWeaver`          |
| Running in [GlassFish](https://glassfish.dev.java.net/) (limited to EAR deployments) | `GlassFishLoadTimeWeaver`       |
| Running in Red Hat’s [JBoss AS](https://www.jboss.org/jbossas/) or [WildFly](https://www.wildfly.org/) | `JBossLoadTimeWeaver`           |
| Running in IBM’s [WebSphere](https://www-01.ibm.com/software/webservers/appserv/was/) | `WebSphereLoadTimeWeaver`       |
| Running in Oracle’s [WebLogic](https://www.oracle.com/technetwork/middleware/weblogic/overview/index-085209.html) | `WebLogicLoadTimeWeaver`        |
| JVM started with Spring `InstrumentationSavingAgent` (`java -javaagent:path/to/spring-instrument.jar`) | `InstrumentationLoadTimeWeaver` |
| Fallback, expecting the underlying ClassLoader to follow common conventions (namely `addTransformer` and optionally a `getThrowawayClassLoader` method) | `ReflectiveLoadTimeWeaver`      |

请注意，该表仅列出使用 `DefaultContextLoadTimeWeaver` 时自动检测的 `LoadTimeWeavers`。您可以准确指定要使用的 `LoadTimeWeaver` 实现。

要使用 Java 配置指定特定的 `LoadTimeWeaver`，请实现 `LoadTimeWeavingConfigurer` 接口并覆盖`getLoadTimeWeaver()` 方法。以下示例指定 `ReflectiveLoadTimeWeaver`：

```java
@Configuration
@EnableLoadTimeWeaving
public class AppConfig implements LoadTimeWeavingConfigurer {

    @Override
    public LoadTimeWeaver getLoadTimeWeaver() {
        return new ReflectiveLoadTimeWeaver();
    }
}
```

如果使用基于 XML 的配置，则可以将完全限定的类名指定为 `<context:load-time-weaver/>` 元素上的 `weaver-class` 属性的值。同样，以下示例指定了 `ReflectiveLoadTimeWeaver`：

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

    <context:load-time-weaver
            weaver-class="org.springframework.instrument.classloading.ReflectiveLoadTimeWeaver"/>

</beans>
```

稍后可以使用众所周知的名称 `loadTimeWeaver` 从 Spring 容器中检索由配置定义和注册的 `LoadTimeWeaver`。请记住，`LoadTimeWeaver` 仅作为 Spring 的 LTW 基础结构添加一个或多个 `ClassFileTransformer` 的机制存在。执行 LTW 的实际 `ClassFileTransformer` 是 `ClassPreProcessorAgentAdapter`（来自 `org.aspectj.weaver.loadtime` 包）类。有关更多详细信息，请参阅 `ClassPreProcessorAgentAdapter` 类的类级javadoc，因为编织实际如何实现的细节超出了本文档的范围。

剩下要讨论的配置有一个`final`属性：`aspectjWeaving`属性（如果使用XML，则为`aspectj-weaving`）。此属性控制是否启用 LTW。它接受三个可能值中的一个，如果该属性不存在，则默认值为`autautodetect`。下表总结了三个可能的值：

| Annotation Value | XML Value    | Explanation                              |
| ---------------- | ------------ | ---------------------------------------- |
| `ENABLED`        | `on`         | AspectJ weaving is on, and aspects are woven at load-time as appropriate. |
| `DISABLED`       | `off`        | LTW is off. No aspect is woven at load-time. |
| `AUTODETECT`     | `autodetect` | If the Spring LTW infrastructure can find at least one `META-INF/aop.xml` file, then AspectJ weaving is on. Otherwise, it is off. This is the default value. |

##### 特定于环境的配置

最后一节包含在应用程序服务器和Web容器等环境中使用Spring的LTW支持时所需的任何其他设置和配置。

###### Tomcat, JBoss, WebSphere, WebLogic

Tomcat，JBoss/WildFly，IBM WebSphere Application Server和Oracle WebLogic Server都提供了一个能够进行本地检测的通用应用程序 `ClassLoader`。Spring的原生LTW可以利用这些`ClassLoader`实现来提供AspectJ编织。您可以简单地启用加载时编织，如前所述。具体来说，您无需修改JVM启动脚本即可添加 `-javaagent:path/to/spring-instrument.jar`。

请注意，在JBoss上，您可能需要禁用应用服务器扫描，以防止它在应用程序实际启动之前加载类。 一个快速的解决方法是向您的工件添加一个名为`WEB-INF/jboss-scanning.xml`的文件，其中包含以下内容：

```xml
<scanning xmlns="urn:jboss:scanning:1.0"/>
```

###### Generic Java Applications

在特定`LoadTimeWeaver`实现不支持的环境中需要类检测时，JVM代理是常规解决方案。对于这种情况，Spring提供了`InstrumentationLoadTimeWeaver`，它需要一个特定于Spring的（但非常通用的）JVM代理`spring-instrument.jar`，由常见的`@EnableLoadTimeWeaving`和`<context:load-time-weaver/>`设置自动检测。

要使用它，必须通过提供以下JVM选项来启动具有Spring代理的虚拟机：

```
-javaagent:/path/to/spring-instrument.jar
```

请注意，这需要修改JVM启动脚本，这可能会阻止您在应用程序服务器环境中使用它（取决于您的服务器和操作策略）。也就是说，对于独立的Spring应用程序等单应用程序的每个JVM部署，您通常可以控制整个JVM设置。

### 5.11 其它资源

有关 AspectJ 的更多信息，请访问 [AspectJ website](https://www.eclipse.org/aspectj).

*Eclipse AspectJ* by Adrian Colyer et. al. (Addison-Wesley, 2005) 提供了 AspectJ 语言的全面介绍和参考。

*AspectJ in Action*, Second Edition by Ramnivas Laddad (Manning, 2009) 强烈推荐。本书的重点是AspectJ，但是同时探索了很多一般的AOP主题（在某种程度上）。