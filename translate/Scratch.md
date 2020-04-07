##### Auto-configured ReactiveHealthIndicators

The following `ReactiveHealthIndicators` are auto-configured by Spring Boot when appropriate:

| Name                                                         | Description                             |
| :----------------------------------------------------------- | :-------------------------------------- |
| [`CassandraReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/cassandra/CassandraReactiveHealthIndicator.java) | Checks that a Cassandra database is up. |
| [`CouchbaseReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/couchbase/CouchbaseReactiveHealthIndicator.java) | Checks that a Couchbase cluster is up.  |
| [`MongoReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/mongo/MongoReactiveHealthIndicator.java) | Checks that a Mongo database is up.     |
| [`RedisReactiveHealthIndicator`](https://github.com/spring-projects/spring-boot/tree/v2.2.6.RELEASE/spring-boot-project/spring-boot-actuator/src/main/java/org/springframework/boot/actuate/redis/RedisReactiveHealthIndicator.java) | Checks that a Redis server is up.       |

> If necessary, reactive indicators replace the regular ones. Also, any `HealthIndicator` that is not handled explicitly is wrapped automatically.