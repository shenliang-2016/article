##### Cache Metrics

自动配置可在启动时使用前缀为 `cache` 的指标来检测所有可用的 `Cache`。高速缓存检测针对一组基本指标进行了标准化。还提供其他特定于缓存的指标。

支持下列缓存类库：

- Caffeine
- EhCache 2
- Hazelcast
- 任何兼容 JCache (JSR-107) 实现

Metrics 会被打上标签，该标签来自缓存的名称以及由 bean 名称派生而来的 `CacheManager` 的名称。

> 仅在启动时配置的缓存绑定到注册表。对于未在缓存配置中定义的缓存，例如，在启动阶段即时或以编程方式创建的高速缓存时，需要显式注册。可以使用`CacheMetricsRegistrar` bean 来简化该过程。

##### DataSource Metrics

通过自动配置，可以使用前缀为 `jdbc.connections` 的度量来检测所有可用的 `DataSource` 对象。数据源检测产生的量规表示池中当前活动，空闲，最大允许和最小允许的连接。

度量标准还标有根据 bean 名称计算的 `DataSource` 名称。

> 默认情况下，Spring Boot 为所有支持的数据源提供元数据。如果不支持立即使用您喜欢的数据源，则可以添加其他`DataSourcePoolMetadataProvider` bean。有关示例，请参见 `DataSourcePoolMetadataProvidersConfiguration`。

同样，使用 `hikaricp` 前缀公开特定于 Hikari 的指标。每个度量标准都以池的名称标记（可以通过 `spring.datasource.name` 进行控制）。

##### Hibernate Metrics

通过自动配置，可以检测所有可用的名为 `hibernate` 的统计启用的 Hibernate `EntityManagerFactory` 实例。

度量标准还通过从 Bean 名称派生的 `EntityManagerFactory` 的名称进行标记。

要启用统计信息，必须将标准 JPA 属性 `hibernate.generate_statistics` 设置为 `true`。您可以在自动配置的 `EntityManagerFactory` 上启用该功能，如以下示例所示：

```properties
spring.jpa.properties.hibernate.generate_statistics=true
```

##### RabbitMQ Metrics

自动配置将启用所有名为 `rabbitmq` 的度量标准的 RabbitMQ 连接工厂的检测。