### 5.6. Metrics

Spring Boot Actuator 为 [Micrometer](https://micrometer.io/) 提供了依赖管理和自动配资，一个应用度量门面，支持各种监控系统，包括：

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

> 为了进一步了解 Micrometer’s 能力，请参考相应的 [参考文档](https://micrometer.io/docs)，特别是 [概念章节](https://micrometer.io/docs/concepts).

#### 5.6.1. 起步

Spring Boot 自动配置一个复合 `MeterRegistry`，并为它在类路径中找到的每个受支持的实现向复合添加一个注册表。在运行时类路径中具有对 `micrometer-registry-{system}` 的依赖就足以让 Spring Boot 配置注册表。

大多数注册表具有共同的特征。例如，即使 Micrometer 注册表实现位于类路径中，您也可以禁用特定的注册表。例如，禁用 Datadog：

```properties
management.metrics.export.datadog.enabled=false
```

Spring Boot 还会将任何自动配置的注册表添加到 `Metrics` 类的全局静态复合注册表中，除非您明确告知不要这么做：

```properties
management.metrics.use-global-registry=false
```

您可以注册任意数量的 `MeterRegistryCustomizer` bean 来进一步配置注册表，例如在将任何计量表注册到注册表之前应用通用标签：

```java
@Bean
MeterRegistryCustomizer<MeterRegistry> metricsCommonTags() {
    return registry -> registry.config().commonTags("region", "us-east-1");
}
```

您可以通过更详细地了解通用类型，将自定义项应用于特定的注册表实现：

```java
@Bean
MeterRegistryCustomizer<GraphiteMeterRegistry> graphiteMetricsNamingConvention() {
    return registry -> registry.config().namingConvention(MY_CUSTOM_CONVENTION);
}
```

有了该设置后，您可以在组件中注入 `MeterRegistry` 并注册指标：

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

Spring Boot 还可以[配置内置工具](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-meter)（即 `MeterBinder` 实现) 您可以通过配置或专用注释标记来控制这些实现。

