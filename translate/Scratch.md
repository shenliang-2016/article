##### 通用缓存

如果上下文至少定义了一个 `org.springframework.cache.Cache` bean，则使用通用缓存。创建一个 `CacheManager`，包装所有该类型的 bean。

##### JCache (JSR-107)

[JCache](https://jcp.org/en/jsr/detail?id=107) 通过类路径上的 `javax.cache.spi.CachingProvider` （即类路径上存在的兼容 JSR-107 规范的缓存类库）进行引导，而 `JCacheCacheManager` 由 `spring-boot-starter-cache` “Starter” 提供。提供了各种兼容的库，Spring Boot 为 Ehcache 3，Hazelcast 和 Infinispan 提供了依赖管理。也可以添加任何其他兼容的库。

可能会出现多个提供者，在这种情况下，必须明确指定提供者。即使 JSR-107 标准没有强制采用标准化的方式来定义配置文件的位置，Spring Boot 也会尽其所能以设置带有实现细节的缓存，如以下示例所示：

```properties
# Only necessary if more than one provider is present
spring.cache.jcache.provider=com.acme.MyCachingProvider
spring.cache.jcache.config=classpath:acme.xml
```

> 当缓存库同时提供本机实现和 JSR-107 支持时，Spring Boot 会首选 JSR-107 支持，因此如果您切换到其他 JSR-107 实现，则可以使用相同的功能。

> Spring Boot 具有 [Hazelcast的一般支持](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-hazelcast)。如果单个 `HazelcastInstance` 可用，则除非指定了 `spring.cache.jcache.config` 属性，否则它也会自动被 `CacheManager` 重用。

有两种方法可以自定义基础的 `javax.cache.cacheManager`：

- 可以在启动时通过设置 `spring.cache.cache-names` 属性来创建缓存。如果定义了自定义的 `javax.cache.configuration.Configuration` bean，则用于自定义它们。

- 使用 `CacheManager` 的引用调用 `org.springframework.boot.autoconfigure.cache.JCacheManagerCustomizer` bean 进行完全定制。

> 如果定义了标准的 `javax.cache.CacheManager` bean，它将自动包装在抽象期望的 `org.springframework.cache.CacheManager` 实现中。不再对其进行定制。

