### 5.6. Metrics

Spring Boot Actuator provides dependency management and auto-configuration for [Micrometer](https://micrometer.io/), an application metrics facade that supports numerous monitoring systems, including:

- [AppOptics](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-appoptics)
- [Atlas](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-atlas)
- [Datadog](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-datadog)
- [Dynatrace](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-dynatrace)
- [Elastic](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-elastic)
- [Ganglia](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-ganglia)
- [Graphite](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-graphite)
- [Humio](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-humio)
- [Influx](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-influx)
- [JMX](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-jmx)
- [KairosDB](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-kairos)
- [New Relic](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-newrelic)
- [Prometheus](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-prometheus)
- [SignalFx](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-signalfx)
- [Simple (in-memory)](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-simple)
- [StatsD](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-statsd)
- [Wavefront](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-export-wavefront)

> To learn more about Micrometer’s capabilities, please refer to its [reference documentation](https://micrometer.io/docs), in particular the [concepts section](https://micrometer.io/docs/concepts).

#### 5.6.1. Getting started

Spring Boot auto-configures a composite `MeterRegistry` and adds a registry to the composite for each of the supported implementations that it finds on the classpath. Having a dependency on `micrometer-registry-{system}` in your runtime classpath is enough for Spring Boot to configure the registry.

Most registries share common features. For instance, you can disable a particular registry even if the Micrometer registry implementation is on the classpath. For example, to disable Datadog:

```properties
management.metrics.export.datadog.enabled=false
```

Spring Boot will also add any auto-configured registries to the global static composite registry on the `Metrics` class unless you explicitly tell it not to:

```properties
management.metrics.use-global-registry=false
```

You can register any number of `MeterRegistryCustomizer` beans to further configure the registry, such as applying common tags, before any meters are registered with the registry:

```java
@Bean
MeterRegistryCustomizer<MeterRegistry> metricsCommonTags() {
    return registry -> registry.config().commonTags("region", "us-east-1");
}
```

You can apply customizations to particular registry implementations by being more specific about the generic type:

```java
@Bean
MeterRegistryCustomizer<GraphiteMeterRegistry> graphiteMetricsNamingConvention() {
    return registry -> registry.config().namingConvention(MY_CUSTOM_CONVENTION);
}
```

With that setup in place you can inject `MeterRegistry` in your components and register metrics:

```java
@Component
public class SampleBean {

    private final Counter counter;

    public SampleBean(MeterRegistry registry) {
        this.counter = registry.counter("received.messages");
    }

    public void handleMessage(String message) {
        this.counter.increment();
        // handle message implementation
    }

}
```

Spring Boot also [configures built-in instrumentation](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-meter) (i.e. `MeterBinder` implementations) that you can control via configuration or dedicated annotation markers.