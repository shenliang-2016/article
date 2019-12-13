### 3.2 发送消息

`JmsTemplate` 包含许多方便方法来发送消息。`send` 方法通过 `javax.jms.Destination` 对象指定目的地。其他方法在 JNDI 查找中使用 `String` 来指定目的地。不是用目的地参数的 `send` 方法使用默认目的地。

下面的例子使用 `MessageCreator` 回调来从给定的 `Session` 对象创建一条文本消息：

```java
import javax.jms.ConnectionFactory;
import javax.jms.JMSException;
import javax.jms.Message;
import javax.jms.Queue;
import javax.jms.Session;

import org.springframework.jms.core.MessageCreator;
import org.springframework.jms.core.JmsTemplate;

public class JmsQueueSender {

    private JmsTemplate jmsTemplate;
    private Queue queue;

    public void setConnectionFactory(ConnectionFactory cf) {
        this.jmsTemplate = new JmsTemplate(cf);
    }

    public void setQueue(Queue queue) {
        this.queue = queue;
    }

    public void simpleSend() {
        this.jmsTemplate.send(this.queue, new MessageCreator() {
            public Message createMessage(Session session) throws JMSException {
                return session.createTextMessage("hello queue world");
            }
        });
    }
}
```

上面的例子中，`JmsTemplate` 通过传递一个引用给 `ConnectionFactory` 来构造。作为备用方案，一个无参构造器和 `connectionFactory` 可以被用来构造 JavaBean 风格（使用 `BeanFactory` 或者普通 Java 代码）的实例。另外，请考虑从 Spring 的 `JmsGatewaySupport` 便利性基类派生，该类为 JMS 配置提供了预先构建的 bean 属性。

`send(String destinationName, MessageCreator creator)` 方法允许你通过使用目的地的名称字符串发送消息。如果目的地名称被注册在 JNDI 中，你应该设置 `JndiDestinationResolver` 实例模板的 `destinationResolver` 属性。

如果你创建 `JmsTemplate` 并指定默认目的地，则 `send(MessageCreator c)` 向目的地发送消息。

