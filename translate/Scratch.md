##### 自动配置反应式健康指标

下面的 `ReactiveHealthIndicators` 在适当的时候会由 Spring Boot 自动配置：

| Name                                                         | Description                     |
| :----------------------------------------------------------- | :------------------------------ |
| [`CassandraReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/cassandra/CassandraReactiveHealthIndicator.java) | 检查 Cassandra 数据库已经启动。 |
| [`CouchbaseReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/couchbase/CouchbaseReactiveHealthIndicator.java) | 检查 Couchbase 集群已经启动。   |
| [`MongoReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/mongo/MongoReactiveHealthIndicator.java) | 检查 Mongo 数据库已经启动。     |
| [`RedisReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/redis/RedisReactiveHealthIndicator.java) | 检查 Redis 服务器已经启动。     |

> 如果必要，反应式指标会替换普通的指标。同时所有未被显式处理的指标都会被自动包装。