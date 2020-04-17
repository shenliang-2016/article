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

Micrometer provides a hierarchical mapping to [JMX](https://micrometer.io/docs/registry/jmx), primarily as a cheap and portable way to view metrics locally. By default, metrics are exported to the `metrics` JMX domain. The domain to use can be provided using:

```properties
management.metrics.export.jmx.domain=com.example.app.metrics
```

Micrometer provides a default `HierarchicalNameMapper` that governs how a dimensional meter id is [mapped to flat hierarchical names](https://micrometer.io/docs/registry/jmx#_hierarchical_name_mapping).

> To take control over this behaviour, define your `JmxMeterRegistry` and supply your own `HierarchicalNameMapper`. An auto-configured `JmxConfig` and `Clock` beans are provided unless you define your own:

```java
@Bean
public JmxMeterRegistry jmxMeterRegistry(JmxConfig config, Clock clock) {
    return new JmxMeterRegistry(config, clock, MY_HIERARCHICAL_MAPPER);
}
```

##### KairosDB

By default, metrics are exported to [KairosDB](https://micrometer.io/docs/registry/kairos) running on your local machine. The location of the [KairosDB server](https://kairosdb.github.io/) to use can be provided using:

```properties
management.metrics.export.kairos.uri=https://kairosdb.example.com:8080/api/v1/datapoints
```

##### New Relic

New Relic registry pushes metrics to [New Relic](https://micrometer.io/docs/registry/new-relic) periodically. To export metrics to [New Relic](https://newrelic.com/), your API key and account id must be provided:

```properties
management.metrics.export.newrelic.api-key=YOUR_KEY
management.metrics.export.newrelic.account-id=YOUR_ACCOUNT_ID
```

You can also change the interval at which metrics are sent to New Relic:

```properties
management.metrics.export.newrelic.step=30s
```

##### Prometheus

[Prometheus](https://micrometer.io/docs/registry/prometheus) expects to scrape or poll individual app instances for metrics. Spring Boot provides an actuator endpoint available at `/actuator/prometheus` to present a [Prometheus scrape](https://prometheus.io/) with the appropriate format.

> The endpoint is not available by default and must be exposed, see [exposing endpoints](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-endpoints-exposing-endpoints) for more details.

Here is an example `scrape_config` to add to `prometheus.yml`:

```yaml
scrape_configs:
  - job_name: 'spring'
    metrics_path: '/actuator/prometheus'
    static_configs:
      - targets: ['HOST:PORT']
```

For ephemeral or batch jobs which may not exist long enough to be scraped, [Prometheus Pushgateway](https://github.com/prometheus/pushgateway) support can be used to expose their metrics to Prometheus. To enable Prometheus Pushgateway support, add the following dependency to your project:

```xml
<dependency>
    <groupId>io.prometheus</groupId>
    <artifactId>simpleclient_pushgateway</artifactId>
</dependency>
```

When the Prometheus Pushgateway dependency is present on the classpath, Spring Boot auto-configures a `PrometheusPushGatewayManager` bean. This manages the pushing of metrics to a Prometheus Pushgateway. The `PrometheusPushGatewayManager` can be tuned using properties under `management.metrics.export.prometheus.pushgateway`. For advanced configuration, you can also provide your own `PrometheusPushGatewayManager` bean.

##### SignalFx

SignalFx registry pushes metrics to [SignalFx](https://micrometer.io/docs/registry/signalfx) periodically. To export metrics to [SignalFx](https://www.signalfx.com/), your access token must be provided:

```properties
management.metrics.export.signalfx.access-token=YOUR_ACCESS_TOKEN
```

You can also change the interval at which metrics are sent to SignalFx:

```properties
management.metrics.export.signalfx.step=30s
```

##### Simple

Micrometer ships with a simple, in-memory backend that is automatically used as a fallback if no other registry is configured. This allows you to see what metrics are collected in the [metrics endpoint](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#production-ready-metrics-endpoint).

The in-memory backend disables itself as soon as you’re using any of the other available backend. You can also disable it explicitly:

```properties
management.metrics.export.simple.enabled=false
```

##### StatsD

The StatsD registry pushes metrics over UDP to a StatsD agent eagerly. By default, metrics are exported to a [StatsD](https://micrometer.io/docs/registry/statsd) agent running on your local machine. The StatsD agent host and port to use can be provided using:

```properties
management.metrics.export.statsd.host=statsd.example.com
management.metrics.export.statsd.port=9125
```

You can also change the StatsD line protocol to use (default to Datadog):

```properties
management.metrics.export.statsd.flavor=etsy
```

##### Wavefront

Wavefront registry pushes metrics to [Wavefront](https://micrometer.io/docs/registry/wavefront) periodically. If you are exporting metrics to [Wavefront](https://www.wavefront.com/) directly, your API token must be provided:

```properties
management.metrics.export.wavefront.api-token=YOUR_API_TOKEN
```

Alternatively, you may use a Wavefront sidecar or an internal proxy set up in your environment that forwards metrics data to the Wavefront API host:

```properties
management.metrics.export.wavefront.uri=proxy://localhost:2878
```

> If publishing metrics to a Wavefront proxy (as described in [the documentation](https://docs.wavefront.com/proxies_installing.html)), the host must be in the `proxy://HOST:PORT` format.

You can also change the interval at which metrics are sent to Wavefront:

```properties
management.metrics.export.wavefront.step=30s
```