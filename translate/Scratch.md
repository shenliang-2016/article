### 3.4. Support for JCA Message Endpoints

从 2.5 版本开始，Spring 还提供了对基于 JCA 的 `MessageListener` 容器的支持。 `JmsMessageEndpointManager` 会尝试从提供者的 `ResourceAdapter` 类名称中自动确定 `ActivationSpec` 类名称。因此，通常可以提供 Spring 的通用 `JmsActivationSpecConfig`，如以下示例所示：

```xml
<bean class="org.springframework.jms.listener.endpoint.JmsMessageEndpointManager">
    <property name="resourceAdapter" ref="resourceAdapter"/>
    <property name="activationSpecConfig">
        <bean class="org.springframework.jms.listener.endpoint.JmsActivationSpecConfig">
            <property name="destinationName" value="myQueue"/>
        </bean>
    </property>
    <property name="messageListener" ref="myMessageListener"/>
</bean>
```

或者，您可以使用给定的 `ActivationSpec` 对象设置 `JmsMessageEndpointManager`。`ActivationSpec` 对象也可以来自 JNDI 查找（使用 `<jee:jndi-lookup>`）。以下示例显示了如何执行此操作：

```xml
<bean class="org.springframework.jms.listener.endpoint.JmsMessageEndpointManager">
    <property name="resourceAdapter" ref="resourceAdapter"/>
    <property name="activationSpec">
        <bean class="org.apache.activemq.ra.ActiveMQActivationSpec">
            <property name="destination" value="myQueue"/>
            <property name="destinationType" value="javax.jms.Queue"/>
        </bean>
    </property>
    <property name="messageListener" ref="myMessageListener"/>
</bean>
```

使用 Spring 的 `ResourceAdapterFactoryBean`，你可以在本地配置目标 `ResourceAdapter` ，如下面例子所示：

```xml
<bean id="resourceAdapter" class="org.springframework.jca.support.ResourceAdapterFactoryBean">
    <property name="resourceAdapter">
        <bean class="org.apache.activemq.ra.ActiveMQResourceAdapter">
            <property name="serverUrl" value="tcp://localhost:61616"/>
        </bean>
    </property>
    <property name="workManager">
        <bean class="org.springframework.jca.work.SimpleTaskWorkManager"/>
    </property>
</bean>
```

指定的 `WorkManager` 还可以指向特定于环境的线程池-通常通过 `SimpleTaskWorkManager` 实例的 `asyncTaskExecutor` 属性来指向。如果您碰巧使用多个适配器，请考虑为所有 `ResourceAdapter` 实例定义一个共享线程池。

在某些环境（例如 WebLogic 9 或更高版本）中，您可以改为从 JNDI 获取整个 `ResourceAdapter` 对象（使用 `<jee:jndi-lookup>`）。然后，基于 Spring 的消息侦听器就可以与服务器托管的 `ResourceAdapter` 进行交互，后者也使用服务器的内置 `WorkManager`。

参考 [`JmsMessageEndpointManager`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jms/listener/endpoint/JmsMessageEndpointManager.html)， [`JmsActivationSpecConfig`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jms/listener/endpoint/JmsActivationSpecConfig.html)，以及 [`ResourceAdapterFactoryBean`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jca/support/ResourceAdapterFactoryBean.html) 文档获取更多细节。

Spring 还提供了与 JMS 无关的通用 JCA 消息端点管理器： `org.springframework.jca.endpoint.GenericMessageEndpointManager`。该组件允许使用任何消息侦听器类型（例如 CCI `MessageListener`）和任何提供程序特定的 `ActivationSpec` 对象。请参阅 JCA 提供者的文档以了解连接器的实际功能，并查看 [`GenericMessageEndpointManager`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jca/endpoint/GenericMessageEndpointManager.html) javadoc，以了解特定于 Spring 的配置详细信息。

> 基于 JCA 的消息端点管理与 EJB 2.1 消息驱动 Bean 非常相似。它使用相同的基础资源提供者契约。与 EJB 2.1 MDB 一样，您也可以在 Spring 上下文中使用 JCA 提供程序支持的任何消息侦听器接口。但是，由于 JMS 是与 JCA 端点管理协定一起使用的最常见的端点 API，因此 Spring 为 JMS 提供了显式的“便利”支持。

