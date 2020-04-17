#### 5.6.2. 支持的监控系统

##### AppOptics

默认情况下，AppOptics 注册会将度量值周期性推送到 `api.appoptics.com/v1/measurements` 。为了将度量值导出给 SaaS [AppOptics](https://micrometer.io/docs/registry/appoptics) ，你必须提供 API token：

```properties
management.metrics.export.appoptics.api-token=YOUR_TOKEN
```

##### Atlas

默认情况下，度量值被暴露给运行在你本地的 [Atlas](https://micrometer.io/docs/registry/atlas) 。要使用的 [Atlas server](https://github.com/Netflix/atlas) 的位置可以通过下面方式提供：

```properties
management.metrics.export.atlas.uri=https://atlas.example.com:7101/api/v1/publish
```

##### Datadog

Datadog 注册将度量值周期性推送至 [datadoghq](https://www.datadoghq.com/) 。为了导出度量值到 [Datadog](https://micrometer.io/docs/registry/datadog)，必需提供你的 API key：

```properties
management.metrics.export.datadog.api-key=YOUR_KEY
```

你也可以修改度量值向 Datadog 推送的时间间隔：

```properties
management.metrics.export.datadog.step=30s
```

##### Dynatrace

Dynatrace 注册周期性地将度量值推动到配置的 URI 。为了导出度量值到 [Dynatrace](https://micrometer.io/docs/registry/dynatrace) ，必需提供 API token，设备 ID，以及 URI ：

```properties
management.metrics.export.dynatrace.api-token=YOUR_TOKEN
management.metrics.export.dynatrace.device-id=YOUR_DEVICE_ID
management.metrics.export.dynatrace.uri=YOUR_URI
```

你也可以修改向 Dynatrace 推送度量值的时间间隔：

```properties
management.metrics.export.dynatrace.step=30s
```

##### Elastic

默认情况下，度量值被导出至你本地机器上运行的 [Elastic](https://micrometer.io/docs/registry/elastic) 。要使用的 Elastic server 的地址可以通过以下方式指定：

```properties
management.metrics.export.elastic.host=https://elastic.example.com:8086
```

##### Ganglia

默认情况下，度量值被导出至你本地机器上运行的 [Ganglia](https://micrometer.io/docs/registry/ganglia) 。要使用的 [Ganglia server](http://ganglia.sourceforge.net/) 的地址和端口可以通过以下方式指定：

```properties
management.metrics.export.ganglia.host=ganglia.example.com
management.metrics.export.ganglia.port=9649
```

##### Graphite

默认情况下，度量值被导出至你本地机器上运行的 [Graphite](https://micrometer.io/docs/registry/graphite) 。要使用的 [Graphite server](https://graphiteapp.org/) 的地址和端口可以通过以下方式指定：

```properties
management.metrics.export.graphite.host=graphite.example.com
management.metrics.export.graphite.port=9004
```

Micrometer 提供了默认的 `HierarchicalNameMapper` 用来管理如何将空间尺度 id [映射到平面层级名称](https://micrometer.io/docs/registry/graphite#_hierarchical_name_mapping)。

> 为了控制该映射行为，定义你自己的 `GraphiteMeterRegistry` 并提供相应的 `HierarchicalNameMapper`。一个自动配置的 `GraphiteConfig` 和 `Clock` beans 也会被提供，除非你定义自己的：

```java
@Bean
public GraphiteMeterRegistry graphiteMeterRegistry(GraphiteConfig config, Clock clock) {
    return new GraphiteMeterRegistry(config, clock, MY_HIERARCHICAL_MAPPER);
}
```

##### Humio

默认情况下，Humio 注册会将度量值周期性推送到 [cloud.humio.com](https://cloud.humio.com/) 。为了将度量值导出给 SaaS [Humio](https://micrometer.io/docs/registry/humio)，你必须提供 API token：

```properties
management.metrics.export.humio.api-token=YOUR_TOKEN
```

你还应该配置一个或者多个标签来标示将被推送的度量值的数据源：

```properties
management.metrics.export.humio.tags.alpha=a
management.metrics.export.humio.tags.bravo=b
```

##### Influx

默认情况下，度量值被导出至你本地机器上运行的 [Influx](https://micrometer.io/docs/registry/influx) 。要使用的 [Influx server](https://www.influxdata.com/) 的地址可以通过以下方式指定：

```properties
management.metrics.export.influx.uri=https://influx.example.com:8086
```

##### JMX

Micrometer 提供了到 [JMX](https://micrometer.io/docs/registry/jmx) 的层次结构映射，主要是作为一种便宜且可移植的方式在本地查看度量。默认情况下，指标被导出到 `metrics` JMX 域。可以使用以下方式提供要使用的域：

```properties
management.metrics.export.jmx.domain=com.example.app.metrics
```

Micrometer 提供了一个默认的 `HierarchicalNameMapper` 负责管理将空间尺度 id [映射到平面层级名称](https://micrometer.io/docs/registry/jmx#_hierarchical_name_mapping)。

> 为了控制这种映射行为，定义你自己的 `JmxMeterRegistry` 并提供相应的 `HierarchicalNameMapper`，一个自动配置的 `JmxConfig` 和 `Clock` beans 会被自动提供，除非你自己定义它们：

```java
@Bean
public JmxMeterRegistry jmxMeterRegistry(JmxConfig config, Clock clock) {
    return new JmxMeterRegistry(config, clock, MY_HIERARCHICAL_MAPPER);
}
```

##### KairosDB

默认情况下，度量值被导出至你本地机器上运行的 [KairosDB](https://micrometer.io/docs/registry/kairos) 。要使用的 [KairosDB server](https://kairosdb.github.io/) 的地址可以通过以下方式指定：

```properties
management.metrics.export.kairos.uri=https://kairosdb.example.com:8080/api/v1/datapoints
```

##### New Relic

New Relic 注册将度量值周期性推送至 [New Relic](https://micrometer.io/docs/registry/new-relic) 。为了导出度量值到 [New Relic](https://micrometer.io/docs/registry/new-relic) ，必需提供你的 API key 和账户 id ：

```properties
management.metrics.export.newrelic.api-key=YOUR_KEY
management.metrics.export.newrelic.account-id=YOUR_ACCOUNT_ID
```

你也可以修改度量值推送到 New Relic 的时间间隔：

```properties
management.metrics.export.newrelic.step=30s
```

##### Prometheus

[Prometheus](https://micrometer.io/docs/registry/prometheus) 希望抓取或轮询单个应用程序实例以获取指标。Spring Boot 在 `/actuator/prometheus` 提供了一个执行器端点，以适当格式显示 [Prometheus scrape](https://prometheus.io/)。

> 该端点默认不可用，需要手动暴露。更多相关细节请参考 [exposing endpoints](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-endpoints-exposing-endpoints) 。

这里是需要添加到 `prometheus.yml` 中的 `scrape_config` 的例子：

```yaml
scrape_configs:
  - job_name: 'spring'
    metrics_path: '/actuator/prometheus'
    static_configs:
      - targets: ['HOST:PORT']
```

对于可能不存在足够长的时间而无法被废弃的临时或批处理作业，可以使用 [Prometheus Pushgateway](https://github.com/prometheus/pushgateway) 支持将其指标暴露给 Prometheus。要启用 Prometheus Pushgateway 支持，请将以下依赖项添加到您的项目中：

```xml
<dependency>
    <groupId>io.prometheus</groupId>
    <artifactId>simpleclient_pushgateway</artifactId>
</dependency>
```

当在类路径上存在 Prometheus Pushgateway 依赖项时，Spring Boot 会自动配置一个 `PrometheusPushGatewayManager` bean。这可以管理将指标推送到 Prometheus Pushgateway。可以使用 `management.metrics.export.prometheus.pushgateway` 下的属性来调整 `PrometheusPushGatewayManager`。 对于高级配置，您还可以提供自己的 `PrometheusPushGatewayManager` bean。

##### SignalFx

SignalFx 注册将度量值周期性推送至 [SignalFx](https://micrometer.io/docs/registry/signalfx) 。为了导出度量值到 [SignalFx](https://micrometer.io/docs/registry/signalfx) ，必需提供你的访问 token：

```properties
management.metrics.export.signalfx.access-token=YOUR_ACCESS_TOKEN
```

你也可以修改度量值推送到 SignalFx 的时间间隔：

```properties
management.metrics.export.signalfx.step=30s
```

##### Simple

Micrometer 附带一个简单的内存后端，如果未配置其他注册表，该后端将自动用作后备。这使您可以查看在 [metrics endpoint](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-endpoint) 中收集了哪些指标。

使用任何其他可用后端时，内存中后端都会自行禁用。您也可以显式禁用它：

```properties
management.metrics.export.simple.enabled=false
```

##### StatsD

StatsD 注册急切地通过 UDP 将度量推送到 StatsD 代理。默认情况下，指标会导出到本地计算机上运行的 [StatsD](https://micrometer.io/docs/registry/statsd) 代理中。可以使用以下方式提供要使用的 StatsD 代理主机和端口：

```properties
management.metrics.export.statsd.host=statsd.example.com
management.metrics.export.statsd.port=9125
```

您还可以更改要使用的 StatsD 线路协议（默认为 Datadog）：

```properties
management.metrics.export.statsd.flavor=etsy
```

##### Wavefront

Wavefront 注册将度量值周期性推送至 [Wavefront](https://micrometer.io/docs/registry/wavefront) 。为了直接导出度量值到 [Wavefront](https://micrometer.io/docs/registry/wavefront) ，必需提供你的 API token：

```properties
management.metrics.export.wavefront.api-token=YOUR_API_TOKEN
```

或者，您可以使用在您的环境中设置的 Wavefront 辅助工具或内部代理，将指标数据转发到 Wavefront API 主机：

```properties
management.metrics.export.wavefront.uri=proxy://localhost:2878
```

> 如果将指标发布到Wavefront代理（如 [文档](https://docs.wavefront.com/proxies_installing.html) 中所述），则主机必须为 `proxy://HOST:PORT` 格式。

你也可以修改度量值推送到 Wavefront 的时间间隔：

```properties
management.metrics.export.wavefront.step=30s
```

