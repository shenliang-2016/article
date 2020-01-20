#### 4.12.1. 支持的缓存提供程序

缓存抽象不提供实际的存储，而是依赖于由 `org.springframework.cache.Cache` 和 `org.springframework.cache.CacheManager` 接口实现的抽象。

如果尚未定义类型为 `CacheManager` 或名为 `CacheResolver` 的 `CacheResolver` 的 Bean（请参见 [`CachingConfigurer`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/cache/annotation/CachingConfigurer.html)），Spring Boot 会尝试检测以下提供程序（按指示的顺序）：

1. [Generic](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-generic)
2. [JCache (JSR-107)](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-jcache) (EhCache 3, Hazelcast, Infinispan, and others)
3. [EhCache 2.x](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-ehcache2)
4. [Hazelcast](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-hazelcast)
5. [Infinispan](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-infinispan)
6. [Couchbase](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-couchbase)
7. [Redis](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-redis)
8. [Caffeine](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-caffeine)
9. [Simple](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-simple)

> 也可以通过设置 `spring.cache.type` 属性来强制特定的缓存提供程序。在某些环境中（例如测试环境），如果您需要 [完全禁用缓存](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-caching-provider-none)，请使用此属性。

> 使用 `spring-boot-starter-cache` “Starter”快速添加基本的缓存依赖项。该启动器引入了 `spring-context-support`。如果手动添加依赖项，则必须包含 `spring-context-support` 才能使用 JCache，EhCache 2.x 或 Caffeine 支持。

如果 `CacheManager` 是由 Spring Boot 自动配置的，则可以通过暴露一个实现 `CacheManagerCustomizer` 接口的 bean，在完全初始化之前进一步调整其配置。下面的示例设置一个标志，表示应将 `null` 值向下传递给基础映射：

```java
@Bean
public CacheManagerCustomizer<ConcurrentMapCacheManager> cacheManagerCustomizer() {
    return new CacheManagerCustomizer<ConcurrentMapCacheManager>() {
        @Override
        public void customize(ConcurrentMapCacheManager cacheManager) {
            cacheManager.setAllowNullValues(false);
        }
    };
}
```

> 在前面的示例中，应该使用自动配置的 `ConcurrentMapCacheManager`。如果不是这种情况（您提供了自己的配置，或者自动配置了其他缓存提供程序），则根本不会调用定制程序。您可以根据需要设置任意数量的定制器，也可以使用 `@Order` 或 `Ordered` 对其进行排序。

