##### 使用 JNDI ConnectionFactory

如果你要在应用服务器上运行你的应用，Spring Boot 就会尝试使用 JNDI 寻找 JMS `ConnectionFactory` 。默认情况下，会检查 `java:/JmsXA` 和 `java:/XAConnectionFactory` 这两个位置。你可以使用 `spring.jms.jndi-name` 属性来指定别的位置。如下面例子所示：

```properties
spring.jms.jndi-name=java:/MyConnectionFactory
```

##### 发送消息

Spring 的 `JmsTemplate` 会被自动配置，你可以直接将其注入自己的 beans，如下面例子所示：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jms.core.JmsTemplate;
import org.springframework.stereotype.Component;

@Component
public class MyBean {

    private final JmsTemplate jmsTemplate;

    @Autowired
    public MyBean(JmsTemplate jmsTemplate) {
        this.jmsTemplate = jmsTemplate;
    }

    // ...

}
```

> [`JmsMessagingTemplate`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/jms/core/JmsMessagingTemplate.html) 能够通过类似的方式注入。如果定义了 `DestinationResolver` 或者 `MessageConverter` bean，它们就会自动联系到自动配置的 `JmsTemplate`。

