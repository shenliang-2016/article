##### Kafka Streams

为了使用 Apache Kafka，Spring 提供了一个工厂 bean 来创建 `StreamsBuilder` 对象并管理其流的生命周期。只要在类路径上存在 `kafka-streams`，并且通过 `@EnableKafkaStreams` 注解启用了 Kafka Streams，Spring Boot 就会自动配置所需的 `KafkaStreamsConfiguration` bean。

启用 Kafka Streams 意味着必须设置应用程序 ID 和引导服务器。可以使用 `spring.kafka.streams.application-id` 来配置前者，如果未设置，则默认为 `spring.application.name`。后者可以全局设置，也可以仅针对流进行覆盖。

使用专用属性可以使用几个附加属性。可以使用 `spring.kafka.streams.properties` 命名空间设置其他任意 Kafka 属性。另请参阅 [其他Kafka属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-kafka-extra-props)。

为了使用该工厂 bean，可以简单地将 `StreamsBuilder` 包装进入你的 `@Bean` 类，如下面例子所示：

```java
@Configuration(proxyBeanMethods = false)
@EnableKafkaStreams
public static class KafkaStreamsExampleConfiguration {

    @Bean
    public KStream<Integer, String> kStream(StreamsBuilder streamsBuilder) {
        KStream<Integer, String> stream = streamsBuilder.stream("ks1In");
        stream.map((k, v) -> new KeyValue<>(k, v.toUpperCase())).to("ks1Out",
                Produced.with(Serdes.Integer(), new JsonSerde<>()));
        return stream;
    }

}
```

默认情况下，由它创建的 `StreamBuilder `对象管理的流会自动启动。您可以使用 `spring.kafka.streams.auto-startup` 属性来自定义此行为。

##### 附加 Kafka 属性

自动配置支持的属性展示在 [通用应用程序属性](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#common-application-properties) 中。请注意，在大多数情况下，这些属性（连字符连接的或驼峰记号表示）直接映射到 Apache Kafka 点连接的属性。有关详细信息，请参阅 Apache Kafka 文档。

这些属性的前几个属性适用于所有组件（生产者，使用者，管理器和流），但如果您希望使用不同的值，则可以在组件级别指定。 Apache Kafka 会指定重要性为 HIGH，MEDIUM 或 LOW 的属性。 Spring Boot 自动配置支持所有 HIGH 重要性属性，一些选定的 MEDIUM 和 LOW 属性以及任何没有默认值的属性。

通过 `KafkaProperties` 类可以直接使用 Kafka 支持的属性的子集。如果您希望使用不直接支持的其他属性来配置生产者或使用者，请使用以下属性：

```properties
spring.kafka.properties.prop.one=first
spring.kafka.admin.properties.prop.two=second
spring.kafka.consumer.properties.prop.three=third
spring.kafka.producer.properties.prop.four=fourth
spring.kafka.streams.properties.prop.five=fifth
```

这将常见的 `prop.one` Kafka 属性设置为 `first`（适用于生产者，消费者和管理员），将 `prop.two` admin 属性设置为 `second`，将 `prop.three` 消费者属性设置为 `Third`。将 `prop.four` 生产者属性设置为 `fourth`，将 `prop.five` 流属性设置为 `fifth`。

您还可以如下配置 Spring Kafka `JsonDeserializer`：

```properties
spring.kafka.consumer.value-deserializer=org.springframework.kafka.support.serializer.JsonDeserializer
spring.kafka.consumer.properties.spring.json.value.default.type=com.example.Invoice
spring.kafka.consumer.properties.spring.json.trusted.packages=com.example,org.acme
```

同样，您可以禁用在报头中发送类型信息的 `JsonSerializer` 默认行为：

```properties
spring.kafka.producer.value-serializer=org.springframework.kafka.support.serializer.JsonSerializer
spring.kafka.producer.properties.spring.json.add.type.headers=false
```

> 以这种方式设置的属性将覆盖 Spring Boot 显式支持的任何配置项。

