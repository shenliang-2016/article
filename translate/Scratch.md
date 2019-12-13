#### 3.3.4. Using `MessageListenerAdapter`

`MessageListenerAdapter` 类是 Spring 异步消息支持中的最后一个组件。简而言之，它使您几乎可以将任何类公开为 MDP（尽管存在一些约束）。

考虑以下接口定义：

```java
public interface MessageDelegate {

    void handleMessage(String message);

    void handleMessage(Map message);

    void handleMessage(byte[] message);

    void handleMessage(Serializable message);
}
```

注意，尽管该接口既没有扩展 `MessageListener` 也没有扩展 `SessionAwareMessageListener` 接口，但是您仍然可以通过使用 `MessageListenerAdapter` 类将其用作 MDP。还请注意，如何根据各种消息处理方法可以接收和处理的各种 `Message` 类型的内容来强类型化。

现在考虑以下 `MessageDelegate` 接口的实现：

```java
public class DefaultMessageDelegate implements MessageDelegate {
    // implementation elided for clarity...
}
```

特别要注意的是，前面的 `MessageDelegate` 接口的实现（`DefaultMessageDelegate`类）完全没有 JMS 依赖性。这确实是一个 POJO，我们可以通过以下配置将其制作为 MDP：

```java
<!-- this is the Message Driven POJO (MDP) -->
<bean id="messageListener" class="org.springframework.jms.listener.adapter.MessageListenerAdapter">
    <constructor-arg>
        <bean class="jmsexample.DefaultMessageDelegate"/>
    </constructor-arg>
</bean>

<!-- and this is the message listener container... -->
<bean id="jmsContainer" class="org.springframework.jms.listener.DefaultMessageListenerContainer">
    <property name="connectionFactory" ref="connectionFactory"/>
    <property name="destination" ref="destination"/>
    <property name="messageListener" ref="messageListener"/>
</bean>
```

下一个示例展示另一个 MDP，它只能处理接收 JMS `TextMessage` 消息。请注意，实际上是如何处理消息的方法称为 `receive` （`MessageListenerAdapter` 中消息处理方法的名称默认为 `handleMessage`），但是它是可配置的（如本节后面所述）。还请注意，如何设置强类型的 `receive(..)` 方法以仅接收和响应 JMS `TextMessage` 消息。下面的清单显示了 `TextMessageDelegate` 接口的定义：

```java
public interface TextMessageDelegate {

    void receive(TextMessage message);
}
```

下面的例子展示了实现 `TextMessageDelegate` 接口的类：

```java
public class DefaultTextMessageDelegate implements TextMessageDelegate {
    // implementation elided for clarity...
}
```

相应的 `MessageListenerAdapter` 配置如下：

```xml
<bean id="messageListener" class="org.springframework.jms.listener.adapter.MessageListenerAdapter">
    <constructor-arg>
        <bean class="jmsexample.DefaultTextMessageDelegate"/>
    </constructor-arg>
    <property name="defaultListenerMethod" value="receive"/>
    <!-- we don't want automatic message context extraction -->
    <property name="messageConverter">
        <null/>
    </property>
</bean>
```

请注意，如果 `messageListener` 接收到的不是 `TextMessage` 类型的 JMS `Message`，则抛出 `IllegalStateException` 并随后将其吞下。`MessageListenerAdapter` 类的另一个功能是，如果处理程序方法返回的是非空值，则可以自动发送响应消息。考虑以下接口和类：

```java
public interface ResponsiveTextMessageDelegate {

    // notice the return type...
    String receive(TextMessage message);
}
public class DefaultResponsiveTextMessageDelegate implements ResponsiveTextMessageDelegate {
    // implementation elided for clarity...
}
```

如果您将 `DefaultResponsiveTextMessageDelegate` 与 `MessageListenerAdapter` 结合使用，则在默认配置下，执行 `receive(..)` 方法返回的所有非空值都将转换为`TextMessage。 `。然后将生成的 `TextMessage` 发送到在原始 `Message` 的 JMS `Reply-To` 属性或 `MessageListenerAdapter` 上设置的默认 `Destination` 中定义的 `Destination`（如果已配置）。如果没有找到 `Destination`，则抛出 `InvalidDestinationException`（请注意，该异常不会被吞没，并且会在调用堆栈中传播）。

#### 3.3.5 在事务中处理消息

在事务中调用消息侦听器仅需要重新配置侦听器容器。

您可以通过侦听器容器定义上的 `sessionTransacted` 标志来激活本地资源事务。然后，每个消息侦听器调用都在活动的 JMS 事务中运行，并且在侦听器执行失败的情况下回退消息接收。（通过 `SessionAwareMessageListener`）发送响应消息是同一本地事务的一部分，但是任何其他资源操作（例如数据库访问）都是独立运行的。这通常需要在侦听器实现中进行重复消息检测，以解决数据库处理已提交但消息处理未能提交的情况。

考虑以下 bean 定义：

```xml
<bean id="jmsContainer" class="org.springframework.jms.listener.DefaultMessageListenerContainer">
    <property name="connectionFactory" ref="connectionFactory"/>
    <property name="destination" ref="destination"/>
    <property name="messageListener" ref="messageListener"/>
    <property name="sessionTransacted" value="true"/>
</bean>
```

要参与外部管理的事务，您需要配置一个事务管理器并使用支持外部管理的事务的侦听器容器（通常为 `DefaultMessageListenerContainer`）。

要为 XA 事务参与配置消息侦听器容器，您需要配置一个 `JtaTransactionManager`（默认情况下，它委派给 Java EE 服务器的事务子系统）。请注意，底层的 JMS `ConnectionFactory` 必须具有 XA 功能，并已向您的 JTA 事务协调器正确注册。（检查 Java EE 服务器的 JNDI 资源配置。）这使消息接收和（例如）数据库访问成为同一事务的一部分（具有统一的提交语义，但以 XA 事务日志开销为代价）。

以下 bean 定义创建一个事务管理器：

```xml
<bean id="transactionManager" class="org.springframework.transaction.jta.JtaTransactionManager"/>
```

然后，我们需要将其添加到我们之前的容器配置中。容器负责其余的工作。以下示例显示了如何执行此操作：

```xml
<bean id="jmsContainer" class="org.springframework.jms.listener.DefaultMessageListenerContainer">
    <property name="connectionFactory" ref="connectionFactory"/>
    <property name="destination" ref="destination"/>
    <property name="messageListener" ref="messageListener"/>
    <property name="transactionManager" ref="transactionManager"/> 
</bean>
```

