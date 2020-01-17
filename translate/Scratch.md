### 4.11. 使用 NoSQL 技术

Spring Data 提供了其他项目来帮助您访问各种 NoSQL 技术，包括：

- [MongoDB](https://spring.io/projects/spring-data-mongodb)
- [Neo4J](https://spring.io/projects/spring-data-neo4j)
- [Elasticsearch](https://spring.io/projects/spring-data-elasticsearch)
- [Solr](https://spring.io/projects/spring-data-solr)
- [Redis](https://spring.io/projects/spring-data-redis)
- [GemFire](https://spring.io/projects/spring-data-gemfire) or [Geode](https://spring.io/projects/spring-data-geode)
- [Cassandra](https://spring.io/projects/spring-data-cassandra)
- [Couchbase](https://spring.io/projects/spring-data-couchbase)
- [LDAP](https://spring.io/projects/spring-data-ldap)

Spring Boot 为 Redis，MongoDB，Neo4j，Elasticsearch，Solr Cassandra，Couchbase 和 LDAP 提供自动配置。您可以使用其他项目，但必须自己进行配置。请参阅 [spring.io/projects/spring-data](https://spring.io/projects/spring-data) 上的相应参考文档。

#### 4.11.1. Redis

[Redis](https://redis.io/) 是一个缓存，消息代理，以及一个拥有丰富特性的键值存储。Spring Boot 为 [Lettuce](https://github.com/lettuce-io/lettuce-core/) 和 [Jedis](https://github.com/xetorthio/jedis/) 客户端类库提供了基本的自动配置，并通过 [Spring Data Redis](https://github.com/spring-projects/spring-data-redis) 提供了它们之上的抽象。

有一个 `spring-boot-starter-data-redis` `Starter`，用于以方便的方式收集依赖项。默认情况下，它使用 [Lettuce](https://github.com/lettuce-io/lettuce-core/)。该启动程序可以处理传统应用程序和响应式应用程序。

> 我们还提供了一个 `spring-boot-starter-data-redis-reactive` `Starter`，以与其他具有反应性支持的存储保持一致。

##### 连接到 Redis

您可以像其他任何 Spring Bean 一样注入自动配置的 `RedisConnectionFactory`，`StringRedisTemplate` 或普通的 `RedisTemplate` 实例。默认情况下，该实例尝试连接到 Redis 服务器的 `localhost:6379`。下面的清单显示了这种 Bean 的示例：

```java
@Component
public class MyBean {

    private StringRedisTemplate template;

    @Autowired
    public MyBean(StringRedisTemplate template) {
        this.template = template;
    }

    // ...

}
```

> 您还可以注册任意数量的实现 `LettuceClientConfigurationBuilderCustomizer` 的 bean，以进行更高级的自定义。如果您使用 Jedis，`JedisClientConfigurationBuilderCustomizer` 也可用。

如果您添加自己的任何自动配置类型的 `@Bean`，它将替换默认值（除非排除是基于 bean 名称 `redisTemplate`而不是其类型的 `RedisTemplate` 除外） 。默认情况下，如果 `commons-pool2` 在类路径中，则将得到一个池化连接工厂。

