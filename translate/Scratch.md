##### EhCache 2.x

如果在类路径根目录找到名为 `ehcache.xml` 的文件 [EhCache](https://www.ehcache.org/) 2.x 就会被使用， `EhCacheCacheManager` 由 `spring-boot-starter-cache` “Starter” 提供，用于引导缓存管理器。也可以提供如下的另外一种形式的配置文件：

```properties
spring.cache.ehcache.config=classpath:config/another-config.xml
```

##### Hazelcast

Spring Boot 提供了 [对 Hazelcast 的通用支持](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-hazelcast)。如果已经自动配置了 `HazelcastInstance` ，它就会被自动包装为 `CacheManager`。

##### Infinispan

[Infinispan](https://infinispan.org/) 没有默认的配置文件位置，因此必须显式指定。否则将使用默认引导：

```properties
spring.cache.infinispan.config=infinispan.xml
```

通过设定 `spring.cache.cache-names` 属性，缓存可以在启动期间创建。如果自定义了 `ConfigurationBuilder` bean，它就会被用于自定义缓存。

> Spring Boot 对 Infinispan 的支持仅限于嵌入式模式，并且非常基础。如果您需要更多选择，则应该使用官方的 Infinispan Spring Boot starter。有关更多详细信息，请参见 [Infinispan 文档](https://github.com/infinispan/infinispan-spring-boot)。

##### Couchbase

如果 [Couchbase](https://www.couchbase.com/) Java 客户端和 `couchbase-spring-cache` 实现可用，并且 Couchbase 已 [配置](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-couchbase)，则会自动配置 `CouchbaseCacheManager` 。也可以通过设置 `spring.cache.cache-names` 属性来在启动时创建其他缓存。这些缓存在自动配置的 `Bucket` 上运行。您还可以定制在另一个 `Bucket` 上创建其他缓存。假设您在主 `Bucket` 上需要两个缓存（ `cache1` 和 `cache2`），并且在另一个 `Bucket` 上需要一个（自定义生存时间）为2秒的（ `cache3` ）缓存。您可以通过配置创建前两个缓存，如下所示：

```properties
spring.cache.cache-names=cache1,cache2
```

然后你就可以定义 `@Configuration` 类来配置额外的 `Bucket` 和 `cache3` 缓存，如下所示：

```java
@Configuration(proxyBeanMethods = false)
public class CouchbaseCacheConfiguration {

    private final Cluster cluster;

    public CouchbaseCacheConfiguration(Cluster cluster) {
        this.cluster = cluster;
    }

    @Bean
    public Bucket anotherBucket() {
        return this.cluster.openBucket("another", "secret");
    }

    @Bean
    public CacheManagerCustomizer<CouchbaseCacheManager> cacheManagerCustomizer() {
        return c -> {
            c.prepareCache("cache3", CacheBuilder.newInstance(anotherBucket())
                    .withExpiration(2));
        };
    }

}
```

这个示例配置服用了通过自动配置创建的 `Cluster` 。

##### Redis

如果 [Redis](https://redis.io/) 可用并已配置，则将自动配置 `RedisCacheManager`。通过设置 `spring.cache.cache-names` 属性可以在启动时创建其他缓存，并且可以使用 `spring.cache.redis.*` 属性配置缓存默认值。例如，以下配置将创建 `cache1` 和 `cache2` 缓存，其“生存时间”为10分钟：

```properties
spring.cache.cache-names=cache1,cache2
spring.cache.redis.time-to-live=600000
```

> 默认情况下，会自动添加 key 前缀，以便如果两个单独的缓存使用相同的 key，Redis 中也不会有相同的 key，也不会返回无效值。如果您创建自己的 `RedisCacheManager`，我们强烈建议将此设置保持启用状态。

> 您可以通过添加自己的 `RedisCacheConfiguration` `@Bean` 来完全控制配置。如果您要自定义序列化策略，这可能会很有用。

