##### Caffeine

[Caffeine](https://github.com/ben-manes/caffeine) 是对 Guava 缓存的 Java 8 重写，取代了对 Guava 的支持。如果存在 Caffeine，则会自动配置 `CaffeineCacheManager`（由 `spring-boot-starter-cache` “Starter” 提供）。缓存可以在启动时通过设置 `spring.cache.cache-names` 属性来创建，并且可以通过以下方式之一自定义（按指示的顺序）：

1. 由 `spring.cache.caffeine.spec` 定义的缓存规范

2. 定义了一个 `com.github.benmanes.caffeine.cache.CaffeineSpec` bean

3. 定义了一个 `com.github.benmanes.caffeine.cache.Caffeine` bean

例如，以下配置将创建 `cache1` 和 `cache2` 缓存，最大大小为 500，并且“生存时间”为 10 分钟。

```properties
spring.cache.cache-names=cache1,cache2
spring.cache.caffeine.spec=maximumSize=500,expireAfterAccess=600s
```

如果定义了 `com.github.benmanes.caffeine.cache.CacheLoader` Bean，它将自动与 `CaffeineCacheManager` 关联。由于 `CacheLoader` 将与由缓存管理器管理的所有缓存相关联，因此必须将其定义为 `CacheLoader<Object, Object>`。自动配置将忽略任何其他通用类型。

##### 简单缓存

如果找不到其他提供者，则配置一个使用 `ConcurrentHashMap` 作为缓存存储的简单实现。如果您的应用程序中没有缓存库，则这是默认设置。默认情况下，根据需要创建缓存，但是您可以通过设置 `cache-names` 属性来限制可用缓存的列表。例如，如果只需要 `cache1` 和 `cache2` 缓存，则按如下所示设置 `cache-names` 属性：

```properties
spring.cache.cache-names=cache1,cache2
```

如果这样做，并且您的应用程序使用了未列出的缓存，那么当需要该缓存时，它将在运行时失败，但不会在启动时失败。这类似于使用未声明的缓存时“实际”缓存提供程序的行为。

##### 无缓存

当您的配置中存在 `@EnableCaching` 时，也需要合适的缓存配置。如果需要在某些环境中完全禁用缓存，请强制将缓存类型设置为 `none` 以使用无操作实现，如以下示例所示：

```properties
spring.cache.type=none
```