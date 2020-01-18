##### MongoTemplate

[Spring Data MongoDB](https://spring.io/projects/spring-data-mongodb) 提供了一个 [`MongoTemplate`](https://docs.spring.io/spring-data/mongodb/docs/2.2.3.RELEASE/api/org/springframework/data/mongodb/core/MongoTemplate.html) 类，非常类似于 Spring 的 `JdbcTemplate` 。就像使用 `JdbcTemplate` 那样，Spring Boot 自动为你配置 bean 来注入该模板，如下所示：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.data.mongodb.core.MongoTemplate;
import org.springframework.stereotype.Component;

@Component
public class MyBean {

    private final MongoTemplate mongoTemplate;

    @Autowired
    public MyBean(MongoTemplate mongoTemplate) {
        this.mongoTemplate = mongoTemplate;
    }

    // ...

}
```

参考 [`MongoOperations` Javadoc](https://docs.spring.io/spring-data/mongodb/docs/2.2.3.RELEASE/api/org/springframework/data/mongodb/core/MongoOperations.html) 了解完整细节。

##### Spring Data MongoDB Repositories

Spring Data 包含对 MongoDB 的存储库支持。与前面讨论的 JPA 存储库一样，基本原理是根据方法名称自动构造查询。

实际上，Spring Data JPA 和 Spring Data MongoDB 共享相同的通用基础架构。您可以从前面的 JPA 示例开始，并假设 `City` 现在是 Mongo 数据类，而不是 JPA `@Entity`，它的工作方式相同，如以下示例所示：

```java
package com.example.myapp.domain;

import org.springframework.data.domain.*;
import org.springframework.data.repository.*;

public interface CityRepository extends Repository<City, Long> {

    Page<City> findAll(Pageable pageable);

    City findByNameAndStateAllIgnoringCase(String name, String state);

}
```

> 您可以使用 `@EntityScan` 注解来自定义文档扫描位置。

> 有关 Spring Data MongoDB 的完整详细信息，包括其丰富的对象映射技术，请参阅其 [参考文档](https://spring.io/projects/spring-data-mongodb)。

##### 内置 Mongo

Spring Boot 为 [内置 Mongo](https://github.com/flapdoodle-oss/de.flapdoodle.embed.mongo) 提供了自动配置。要在 Spring Boot 应用程序中使用它，请添加对 `de.flapdoodle.embed:de.flapdoodle.embed.mongo` 的依赖。

可以通过设置 `spring.data.mongodb.port` 属性来配置 Mongo 监听的端口。要使用随机分配的空闲端口，请使用 0 值。由 `MongoAutoConfiguration` 创建的 `MongoClient` 将自动配置为使用随机分配的端口。

> 如果未配置自定义端口，则默认情况下，内置支持会使用随机端口（而不是 27017）。

如果在类路径上有 SLF4J，则 Mongo 产生的输出将自动路由到名为 `org.springframework.boot.autoconfigure.mongo.embedded.EmbeddedMongo` 的记录器。

您可以声明自己的 `IMongodConfig` 和 `IRuntimeConfig` bean，以控制 Mongo 实例的配置和日志记录路由。可以通过声明一个 `DownloadConfigBuilderCustomizer` bean来定制下载配置。

