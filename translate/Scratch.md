#### 4.13.3. Apache Kafka 支持

[Apache Kafka](https://kafka.apache.org/) 通过提供 `spring-kafka` 项目的自动配置而被支持。

Kafka 配置由 `spring.kafka.*` 中的外部配置属性控制。比如，你可能会在 `application.properties` 中声明下面的内容：

```properties
spring.kafka.bootstrap-servers=localhost:9092
spring.kafka.consumer.group-id=myGroup
```

> 想要在启动时创建主题，请添加一个 `NewTopic` 类型的 bean。如果该主题已经存在，该 bean 就会被忽略。

参考 [`KafkaProperties`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-autoconfigure/src/main/java/org/springframework/boot/autoconfigure/kafka/KafkaProperties.java) 了解更多支持的选项。

##### 发送消息

Spring 的 `KafkaTemplate` 自动配置，你可以直接将其注入自己的 beans 中，如下面例子所示：

```java
@Component
public class MyBean {

    private final KafkaTemplate kafkaTemplate;

    @Autowired
    public MyBean(KafkaTemplate kafkaTemplate) {
        this.kafkaTemplate = kafkaTemplate;
    }

    // ...

}
```

> 如果定义了 `spring.kafka.producer.transaction-id-prefix` 属性， `KafkaTransactionManager` 就会被自动配置。同时，如果定义了 `RecordMessageConverter` bean，它就会自动关联到自动配置好的 `KafkaTemplate`。

##### 接收消息

存在 Apache Kafka 基础结构时，可以使用 `@KafkaListener` 注解任何 bean，以创建侦听器端点。如果未定义 `KafkaListenerContainerFactory`，则会使用 `spring.kafka.listener.*` 中定义的键自动配置默认值。

以下组件在 `someTopic` 主题上创建侦听器端点：

```java
@Component
public class MyBean {

    @KafkaListener(topics = "someTopic")
    public void processMessage(String content) {
        // ...
    }

}
```

如果定义了 `KafkaTransactionManager` bean，它将自动与容器工厂关联。类似地，如果定义了 `ErrorHandler`，`AfterRollbackProcessor` 或 `ConsumerAwareRebalanceListener` bean，它将自动与默认工厂关联。

根据侦听器的类型，`RecordMessageConverter` 或 `BatchMessageConverter` Bean与默认工厂关联。如果批处理侦听器仅存在一个 `RecordMessageConverter` Bean，则将其包装在 `BatchMessageConverter` 中。

> 自定义的 `ChainedKafkaTransactionManager` 必须标记为 `@Primary`，因为它通常引用自动配置的 `KafkaTransactionManager` bean。

