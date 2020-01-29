##### Using a JNDI ConnectionFactory

If you are running your application in an application server, Spring Boot tries to locate a JMS `ConnectionFactory` by using JNDI. By default, the `java:/JmsXA` and `java:/XAConnectionFactory` location are checked. You can use the `spring.jms.jndi-name` property if you need to specify an alternative location, as shown in the following example:

```properties
spring.jms.jndi-name=java:/MyConnectionFactory
```

##### Sending a Message

Spring’s `JmsTemplate` is auto-configured, and you can autowire it directly into your own beans, as shown in the following example:

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

> [`JmsMessagingTemplate`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/jms/core/JmsMessagingTemplate.html) can be injected in a similar manner. If a `DestinationResolver` or a `MessageConverter` bean is defined, it is associated automatically to the auto-configured `JmsTemplate`.

