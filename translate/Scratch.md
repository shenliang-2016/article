#### 5.6.6. Metrics 端点

Spring Boot 提供了一个  `metrics`  端点，可用于诊断检查应用程序收集的指标。端点默认情况下不可用，必须手动公开，请参阅 [暴露端点](https://docs.spring.io/spring-boot/docs/2.2.6.RELEASE/reference/htmlsingle/#production-ready-endpoints-exposing-endpoints) 以获取更多详细信息。

导航至 `/actuator/metrics` 会显示可用仪表名称的列表。您可以通过提供特定的仪表名称作为选择器来深入查看其相关信息。 比如，`/actuator/metrics/jvm.memory.max`。

> 您在此处使用的名称应与代码中使用的名称相匹配，而不是已针对其出厂的监视系统将其命名惯例标准化后的名称。换句话说，如果在 Prometheus 中 `jvm.memory.max` 由于其蛇形命名约定而显示为 `jvm_memory_max`，则在检查 `metrics` 端点中的仪表时，仍应使用 `jvm.memory.max` 作为选择器。

你也可以添加任意数量的 `tag=KEY:VALUE` 查询参数到 URL 的末尾来钻取某个度量，比如 `/actuator/metrics/jvm.memory.max?tag=area:nonheap`：

> 报告的测量值是与仪表名称和已应用的所有标签相匹配的所有仪表的统计信息的*和*。因此，在上面的示例中，返回的 "Value" 统计量是堆的“代码缓存”，“压缩类空间”和“元空间”区域的最大内存占用量的总和。如果您只想查看“元空间”的最大大小，则可以添加一个额外的 `tag=id:Metaspace`，即 `/actuator/metrics/jvm.memory.max?tag=area:nonheap&tag=id:Metaspace`。