#### 3.2.1 使用消息转换器

为了方便域模型对象的发送，`JmsTemplate` 具有各种发送方法，这些方法将 Java 对象作为消息数据内容的参数。`JmsTemplate` 中的重载方法 `convertAndSend()` 和 `receiveAndConvert()` 方法将转换过程委托给 `MessageConverter` 接口的一个实例。该接口定义了一个简单的协定，可以在 Java 对象和 JMS 消息之间进行转换。默认实现（ `SimpleMessageConverter` ）支持在 `String` 和 `TextMessage` ，`byte[]` 和 `BytesMesssage` 之间以及 `java.util.Map` 和 `MapMessage` 之间进行转换。通过使用转换器，您和您的应用程序代码可以专注于通过 JMS 发送或接收的业务对象，而不必担心如何将其表示为 JMS 消息。

沙箱当前包含一个 `MapMessageConverter` ，它使用反射在 JavaBean 和 `MapMessage` 之间进行转换。您可能会自己实现的其他流行实现，可以选择是使用现有 XML 编组程序包（例如 JAXB，Castor 或 XStream）创建代表该对象的 `TextMessage` 的转换器。

为了容纳消息属性，标头和正文的设置，而这些属性通常不能封装在转换器类中，`MessagePostProcessor` 接口可让您在消息转换后、但在发送之前访问消息。以下示例显示了在将 `java.util.Map` 转换为消息后如何修改消息头和属性：

```java
public void sendWithConversion() {
    Map map = new HashMap();
    map.put("Name", "Mark");
    map.put("Age", new Integer(47));
    jmsTemplate.convertAndSend("testQueue", map, new MessagePostProcessor() {
        public Message postProcessMessage(Message message) throws JMSException {
            message.setIntProperty("AccountID", 1234);
            message.setJMSCorrelationID("123-00001");
            return message;
        }
    });
}
```

这将产生以下形式的消息：

```javascript
MapMessage={
    Header={
        ... standard headers ...
        CorrelationID={123-00001}
    }
    Properties={
        AccountID={Integer:1234}
    }
    Fields={
        Name={String:Mark}
        Age={Integer:47}
    }
}
```

#### 3.2.2 使用 `SessionCallback` 和 `ProducerCallback`

尽管发送操作涵盖了许多常见的使用场景，但是您有时可能希望对 JMS `Session` 或 `MessageProducer` 执行多个操作。`SessionCallback` 和 `ProducerCallback` 分别公开了 JMS `Session` 和 `Session` / `MessageProducer` 对。`JmsTemplate` 上的 `execute()` 方法执行这些回调方法。

