### 3.3 接收消息

本节介绍如何使用 Spring 中的 JMS 接收消息。

#### 3.3.1 同步接收

虽然 JMS 通常与异步处理相关联，但是您可以同步使用消息。重载的 `receive(..)` 方法提供了此功能。在同步接收期间，调用线程将阻塞，直到消息可用为止。这可能是危险的操作，因为调用线程可能会无限期地被阻塞。`receiveTimeout` 属性指定接收者在放弃等待消息之前应该等待多长时间。

#### 3.3.2 异步接收：消息驱动的 POJOs

> Spring 还通过使用 `@JmsListener` 注解来支持带注解的侦听器端点，并提供了开放的基础设施来以编程方式注册端点。到目前为止，这是设置异步接收器的最便捷方法。有关更多详细信息，请参见 [启用侦听器端点注解](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-annotated-support) 。

消息驱动 POJO（MDP）以类似于 EJB 世界中的消息驱动 Bean（MDB）的方式充当 JMS 消息的接收者。MDP 的一个限制（请参阅 [使用`MessageListenerAdapter`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#jms-receiving-async-message-listener-adapter) ）是它必须实现 `javax.jms.MessageListener `接口。请注意，如果您的 POJO 在多个线程上接收消息，则重要的是要确保您的实现是线程安全的。

下面的例子展示了一个简单的 MDP 实现：

```java
import javax.jms.JMSException;
import javax.jms.Message;
import javax.jms.MessageListener;
import javax.jms.TextMessage;

public class ExampleListener implements MessageListener {

    public void onMessage(Message message) {
        if (message instanceof TextMessage) {
            try {
                System.out.println(((TextMessage) message).getText());
            }
            catch (JMSException ex) {
                throw new RuntimeException(ex);
            }
        }
        else {
            throw new IllegalArgumentException("Message must be of type TextMessage");
        }
    }
}
```

一旦你实现了你的 `MessageListener` ，就是时候创建一个消息监听器容器了。

以下示例显示了如何定义和配置 Spring 附带的消息侦听器容器之一（在本例中为 `DefaultMessageListenerContainer` ）：

```xml
<!-- this is the Message Driven POJO (MDP) -->
<bean id="messageListener" class="jmsexample.ExampleListener"/>

<!-- and this is the message listener container -->
<bean id="jmsContainer" class="org.springframework.jms.listener.DefaultMessageListenerContainer">
    <property name="connectionFactory" ref="connectionFactory"/>
    <property name="destination" ref="destination"/>
    <property name="messageListener" ref="messageListener"/>
</bean>
```

请参阅各种消息侦听器容器的 Spring Javadoc（所有容器都实现 [MessageListenerContainer](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jms/listener/MessageListenerContainer.html) ），以获取每个实现所支持功能的完整说明。

#### 3.3.3 使用 `SessionAwareMessageListener` 接口

`SessionAwareMessageListener` 接口是特定于 Spring 的接口，它提供与 JMS `MessageListener` 接口相似的协定，但也使消息处理方法可以访问从其接收 `Message` 的 JMS `Session`。以下清单显示了 `SessionAwareMessageListener` 接口的定义：

```java
package org.springframework.jms.listener;

public interface SessionAwareMessageListener {

    void onMessage(Message message, Session session) throws JMSException;
}
```

如果希望 MDP 能够响应任何接收到的消息（通过使用 `onMessage(Message, Session)` 中提供的 `Session`），则可以选择让 MDP 实现此接口（优先于标准 JMS `MessageListener` 接口）。Spring 附带的所有消息侦听器容器实现都支持实现 `MessageListener` 或 `SessionAwareMessageListener` 接口的 MDP。实现 `SessionAwareMessageListener` 的类带有警告，它们随后通过接口绑定到 Spring。是否使用它的选择完全由您作为应用程序开发人员或架构师来决定。

注意，`SessionAwareMessageListener` 接口的 `onMessage(..)` 方法抛出 `JMSException`。与标准的 JMS  `MessageListener` 接口相反，当使用 `SessionAwareMessageListener` 接口时，客户端代码负责处理任何抛出的异常。

