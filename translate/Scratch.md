#### 5.6.5. Customizing individual metrics

If you need to apply customizations to specific `Meter` instances you can use the `io.micrometer.core.instrument.config.MeterFilter` interface. By default, all `MeterFilter` beans will be automatically applied to the micrometer `MeterRegistry.Config`.

For example, if you want to rename the `mytag.region` tag to `mytag.area` for all meter IDs beginning with `com.example`, you can do the following:

```java
@Bean
public MeterFilter renameRegionTagMeterFilter() {
    return MeterFilter.renameTag("com.example", "mytag.region", "mytag.area");
}
```

##### Common tags

Common tags are generally used for dimensional drill-down on the operating environment like host, instance, region, stack, etc. Commons tags are applied to all meters and can be configured as shown in the following example:

```properties
management.metrics.tags.region=us-east-1
management.metrics.tags.stack=prod
```

The example above adds `region` and `stack` tags to all meters with a value of `us-east-1` and `prod` respectively.

> The order of common tags is important if you are using Graphite. As the order of common tags cannot be guaranteed using this approach, Graphite users are advised to define a custom `MeterFilter` instead.

##### Per-meter properties

In addition to `MeterFilter` beans, it’s also possible to apply a limited set of customization on a per-meter basis using properties. Per-meter customizations apply to any all meter IDs that start with the given name. For example, the following will disable any meters that have an ID starting with `example.remote`

```properties
management.metrics.enable.example.remote=false
```

The following properties allow per-meter customization:

| Property                                                     | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| `management.metrics.enable`                                  | Whether to deny meters from emitting any metrics.            |
| `management.metrics.distribution.percentiles-histogram`      | Whether to publish a histogram suitable for computing aggregable (across dimension) percentile approximations. |
| `management.metrics.distribution.minimum-expected-value`, `management.metrics.distribution.maximum-expected-value` | Publish less histogram buckets by clamping the range of expected values. |
| `management.metrics.distribution.percentiles`                | Publish percentile values computed in your application       |
| `management.metrics.distribution.sla`                        | Publish a cumulative histogram with buckets defined by your SLAs. |

For more details on concepts behind `percentiles-histogram`, `percentiles` and `sla` refer to the ["Histograms and percentiles" section](https://micrometer.io/docs/concepts#_histograms_and_percentiles) of the micrometer documentation.