#### 5.6.5. 自定义单个度量

如果您需要对特定的 `Meter` 实例应用自定义设置，则可以使用 `io.micrometer.core.instrument.config.MeterFilter` 接口。默认情况下，所有的 `MeterFilter` bean 都将自动应用于 micrometer  `MeterRegistry.Config`。

例如，如果要将所有 ID 以 `com.example` 开头的计量表的标签 `mytag.region` 重命名为 `mytag.area`，则可以执行以下操作：

```java
@Bean
public MeterFilter renameRegionTagMeterFilter() {
    return MeterFilter.renameTag("com.example", "mytag.region", "mytag.area");
}
```

##### 通用标签

通用标签通常用于在操作环境（如主机，实例，区域，堆栈等）上进行维度深入分析。通用标签适用于所有仪表，可以按以下示例所示进行配置：

```properties
management.metrics.tags.region=us-east-1
management.metrics.tags.stack=prod
```

上面的示例在所有仪表中分别添加了 `region` 和 `stack` 标签，其值分别为 `us-east-1` 和 `prod`。

> 如果使用 Graphite，则常用标签的顺序很重要。由于使用这种方法不能保证通用标签的顺序，因此建议 Graphite 用户定义一个自定义的 `MeterFilter`。

##### Per-meter 属性

除了 `MeterFilter` bean 外，还可以使用属性在 per-meter 基础上应用一组有限的自定义设置。Per-meter 定制适用于以给定名称开头的所有所有表 ID。例如，以下将禁用任何 ID 以 `example.remote` 开头的仪表：

```properties
management.metrics.enable.example.remote=false
```

下面的属性允许 per-meter 自定义：

| Property                                                     | Description                                              |
| :----------------------------------------------------------- | :------------------------------------------------------- |
| `management.metrics.enable`                                  | 是否拒绝仪表发出任何指标。                               |
| `management.metrics.distribution.percentiles-histogram`      | 是否发布适用于计算可聚集（跨维度）百分位数逼近的直方图。 |
| `management.metrics.distribution.minimum-expected-value`, `management.metrics.distribution.maximum-expected-value` | 通过限制期望值的范围，发布较少的直方图桶。               |
| `management.metrics.distribution.percentiles`                | 发布在应用程序中计算的百分位值。                         |
| `management.metrics.distribution.sla`                        | 发布包含您的 SLA 定义的存储桶的累积直方图。              |

有关 `percentiles-histogram`，`percentiles` 和 `sla` 背后的概念的更多详细信息，请参见 micrometer 文档的 [“直方图和百分位数”部分](https://micrometer.io/docs/concepts#_histograms_and_percentiles) 。