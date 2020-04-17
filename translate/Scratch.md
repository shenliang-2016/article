#### 5.6.2. Supported monitoring systems

##### AppOptics

By default, the AppOptics registry pushes metrics to `api.appoptics.com/v1/measurements` periodically. To export metrics to SaaS [AppOptics](https://micrometer.io/docs/registry/appoptics), your API token must be provided:

```properties
management.metrics.export.appoptics.api-token=YOUR_TOKEN
```

##### Atlas

By default, metrics are exported to [Atlas](https://micrometer.io/docs/registry/atlas) running on your local machine. The location of the [Atlas server](https://github.com/Netflix/atlas) to use can be provided using:

```properties
management.metrics.export.atlas.uri=https://atlas.example.com:7101/api/v1/publish
```

##### Datadog

Datadog registry pushes metrics to [datadoghq](https://www.datadoghq.com/) periodically. To export metrics to [Datadog](https://micrometer.io/docs/registry/datadog), your API key must be provided:

```properties
management.metrics.export.datadog.api-key=YOUR_KEY
```

You can also change the interval at which metrics are sent to Datadog:

```properties
management.metrics.export.datadog.step=30s
```

##### Dynatrace

Dynatrace registry pushes metrics to the configured URI periodically. To export metrics to [Dynatrace](https://micrometer.io/docs/registry/dynatrace), your API token, device ID, and URI must be provided:

```properties
management.metrics.export.dynatrace.api-token=YOUR_TOKEN
management.metrics.export.dynatrace.device-id=YOUR_DEVICE_ID
management.metrics.export.dynatrace.uri=YOUR_URI
```

You can also change the interval at which metrics are sent to Dynatrace:

```properties
management.metrics.export.dynatrace.step=30s
```

##### Elastic

By default, metrics are exported to [Elastic](https://micrometer.io/docs/registry/elastic) running on your local machine. The location of the Elastic server to use can be provided using the following property:

```properties
management.metrics.export.elastic.host=https://elastic.example.com:8086
```

##### Ganglia

By default, metrics are exported to [Ganglia](https://micrometer.io/docs/registry/ganglia) running on your local machine. The [Ganglia server](http://ganglia.sourceforge.net/) host and port to use can be provided using:

```properties
management.metrics.export.ganglia.host=ganglia.example.com
management.metrics.export.ganglia.port=9649
```

##### Graphite

By default, metrics are exported to [Graphite](https://micrometer.io/docs/registry/graphite) running on your local machine. The [Graphite server](https://graphiteapp.org/) host and port to use can be provided using:

```properties
management.metrics.export.graphite.host=graphite.example.com
management.metrics.export.graphite.port=9004
```

Micrometer provides a default `HierarchicalNameMapper` that governs how a dimensional meter id is [mapped to flat hierarchical names](https://micrometer.io/docs/registry/graphite#_hierarchical_name_mapping).

> To take control over this behaviour, define your `GraphiteMeterRegistry` and supply your own `HierarchicalNameMapper`. An auto-configured `GraphiteConfig` and `Clock` beans are provided unless you define your own:

```java
@Bean
public GraphiteMeterRegistry graphiteMeterRegistry(GraphiteConfig config, Clock clock) {
    return new GraphiteMeterRegistry(config, clock, MY_HIERARCHICAL_MAPPER);
}
```

##### Humio

By default, the Humio registry pushes metrics to [cloud.humio.com](https://cloud.humio.com/) periodically. To export metrics to SaaS [Humio](https://micrometer.io/docs/registry/humio), your API token must be provided:

```properties
management.metrics.export.humio.api-token=YOUR_TOKEN
```

You should also configure one or more tags to identify the data source to which metrics will be pushed:

```properties
management.metrics.export.humio.tags.alpha=a
management.metrics.export.humio.tags.bravo=b
```

##### Influx

By default, metrics are exported to [Influx](https://micrometer.io/docs/registry/influx) running on your local machine. The location of the [Influx server](https://www.influxdata.com/) to use can be provided using:

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