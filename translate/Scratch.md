> 什么时候需要加载时织入？
>
> 并不是所有的 JPA 提供者程序都需要 JVM agent，Hibernate 就是一个例子。如果你的 JPA 提供者不需要 agent ，或者你有其他选择，比如通过自定义的编译器或者 Ant 任务进行构建期增强，你就不应该使用加载时织入。

`LoadTimeWeaver` 接口是 Spring 提供的类，用来以特定方式插入 JPA `ClassTransformer` 实例，具体方式取决于环境是 web 容器还是应用服务器。通过 [agent](https://docs.oracle.com/javase/6/docs/api/java/lang/instrument/package-summary.html) 关联 `ClassTransformers` 是常用做法，不过效率不高。其中 agents 为整个虚拟机工作，检查它所加载的所有类，我们通常不希望这发生在生产环境服务器上。

Spring 为各种环境提供了若干 `LoadTimeWeaver` 实现，允许 `ClassTransformer` 只被应用于单个类加载器，而不是虚拟机。

参考 AOP 章节中的 [Spring configuration](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-aj-ltw-spring) 了解更多有关 `LoadTimeWeaver` 实现以及设置的细节，包括通用的和特定于各种平台的（比如 Tomcat，JBoss 以及 WebSphere）。

如  [Spring configuration](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-aj-ltw-spring) 中所述，你可以通过使用 `context:load-time-weaver` XML 元素的 `@EnableLoadTimerWeaving` 注解配置一个上下文范围的 `LoadTimeWeaver` 。这样的全局编织器会由所有 JPA `LocalContainerEntityManagerFactoryBean` 实例自动选择。以下示例显示了设置加载时编织器，提供对平台的自动检测（例如 Tomcat 的具有编织功能的类加载器或 Spring 的 JVM agent）以及将编织器自动传播到所有可感知编织器的 bean 的首选方法：

```xml
<context:load-time-weaver/>
<bean id="emf" class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
    ...
</bean>
```

不过，如果需要，你也可以通过 `loadTimerWeaver` 属性手动指定专用编织器。如下面例子所示：

```xml
<bean id="emf" class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
    <property name="loadTimeWeaver">
        <bean class="org.springframework.instrument.classloading.ReflectiveLoadTimeWeaver"/>
    </property>
</bean>
```

无论 LTW 的配置方式如何，通过使用此技术，依赖于检测的 JPA 应用程序都可以在目标平台（例如 Tomcat）中运行，而无需代理。当托管应用程序依赖于不同的 JPA 实现时，这尤其重要，因为 JPA 转换器仅在类加载器级别应用，因此彼此隔离。

##### 处理多个持久化单元

对于依赖多个持久化单元位置（例如，存储在类路径中的各种 JARS 中）的应用程序，Spring 提供了 `PersistenceUnitManager` 作为中央存储库并避免了持久化单元发现过程，这可能是代价高昂的。默认实现允许指定多个位置。解析这些位置，然后通过持久化单元名称进行检索。（默认情况下，在类路径中搜索 `META-INF/persistence.xml` 文件。）以下示例配置多个位置：

```xml
<bean id="pum" class="org.springframework.orm.jpa.persistenceunit.DefaultPersistenceUnitManager">
    <property name="persistenceXmlLocations">
        <list>
            <value>org/springframework/orm/jpa/domain/persistence-multi.xml</value>
            <value>classpath:/my/package/**/custom-persistence.xml</value>
            <value>classpath*:META-INF/persistence.xml</value>
        </list>
    </property>
    <property name="dataSources">
        <map>
            <entry key="localDataSource" value-ref="local-db"/>
            <entry key="remoteDataSource" value-ref="remote-db"/>
        </map>
    </property>
    <!-- if no datasource is specified, use this one -->
    <property name="defaultDataSource" ref="remoteDataSource"/>
</bean>

<bean id="emf" class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
    <property name="persistenceUnitManager" ref="pum"/>
    <property name="persistenceUnitName" value="myCustomUnit"/>
</bean>
```

默认实现允许以声明方式（通过其影响所有托管单元的属性）或以编程方式（通过允许持久化单元选择的 `PersistenceUnitPostProcessor`）自定义 `PersistenceUnitInfo` 实例（在将其馈送到 JPA 提供程序之前）。如果没有指定 `PersistenceUnitManager`，`LocalContainerEntityManagerFactoryBean` 将在内部创建和使用。

##### 后台引导

`LocalContainerEntityManagerFactoryBean` 支持通过 `bootstrapExecutor` 属性进行后台引导，如下面例子所示：

```xml
<bean id="emf" class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
    <property name="bootstrapExecutor">
        <bean class="org.springframework.core.task.SimpleAsyncTaskExecutor"/>
    </property>
</bean>
```

实际的 JPA 提供程序引导将移交给指定的执行程序，然后并行运行到应用程序引导线程。暴露的 `EntityManagerFactory` 代理可以注入到其他应用程序组件中，甚至可以响应 `EntityManagerFactoryInfo` 配置检查。但是，一旦实际的 JPA 提供程序被其他组件访问（例如，调用 `createEntityManager`），这些调用就会阻塞，直到后台引导完成为止。特别是，当您使用 Spring Data JPA 时，请确保还为其存储库设置了延迟引导。

