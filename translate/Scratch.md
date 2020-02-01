##### 使用嵌入式 Kafka 进行测试

Spring 为 Apache Kafka 提供了一种使用嵌入式 Apache Kafka 代理测试项目的便捷方法。要使用此功能，请用 `spring-kafka-test` 模块的 `@EmbeddedKafka` 注解测试类。有关更多信息，请参见 [Spring for Apache Kafka 参考手册](https://docs.spring.io/spring-kafka/docs/current/reference/html/#embedded-kafka-annotation)。

要使 Spring Boot 自动配置与上述嵌入式 Apache Kafka 代理一起使用，您需要将嵌入式代理地址（由 `EmbeddedKafkaBroker` 填充）的系统属性重新映射到 Apache Kafka 的 Spring Boot 配置属性中。有几种方法可以做到这一点：

- 提供一个系统属性，以将嵌入式代理地址映射到测试类中的 `spring.kafka.bootstrap-servers` 中：

```java
static {
    System.setProperty(EmbeddedKafkaBroker.BROKER_LIST_PROPERTY, "spring.kafka.bootstrap-servers");
}
```

- 在 `@EmbeddedKafka` 注解上配置属性名称：

```java
@EmbeddedKafka(topics = "someTopic",
        bootstrapServersProperty = "spring.kafka.bootstrap-servers")
```

- 在配置属性中使用占位符：

```properties
spring.kafka.bootstrap-servers=${spring.embedded.kafka.brokers}
```

