#### 4.11.2. MongoDB

[MongoDB](https://www.mongodb.com/) 是一个开源 NoSQL 文档数据库，它使用类似 JSON 的数据结构而不是传统的基于表的关系数据。Spring Boot 为使用 MongoDB 提供了许多便利，包括 `spring-boot-starter-data-mongodb` 和 `spring-boot-starter-data-mongodb-active` “Starters”。

##### 连接到 MongoDB 数据库

要访问 Mongo 数据库，您可以注入自动配置的 `org.springframework.data.mongodb.MongoDbFactory` 。默认情况下，该实例尝试通过 `mongodb://localhost/test` 连接到 MongoDB 服务器。以下示例显示了如何连接到 MongoDB 数据库：

```java
import org.springframework.data.mongodb.MongoDbFactory;
import com.mongodb.DB;

@Component
public class MyBean {

    private final MongoDbFactory mongo;

    @Autowired
    public MyBean(MongoDbFactory mongo) {
        this.mongo = mongo;
    }

    // ...

    public void example() {
        DB db = mongo.getDb();
        // ...
    }

}
```

您可以设置 `spring.data.mongodb.uri` 属性来更改 URL 并配置其他设置，例如*数据库副本集*，如以下示例所示：

```properties
spring.data.mongodb.uri=mongodb://user:secret@mongo1.example.com:12345,mongo2.example.com:23456/test
```

另外，只要您使用 Mongo 2.x，就可以指定一个 `host`/`port`。例如，您可以在 `application.properties` 中声明以下设置：

```properties
spring.data.mongodb.host=mongoserver
spring.data.mongodb.port=27017
```

如果定义了自己的 `MongoClient`，它将用于自动配置合适的 `MongoDbFactory`。`com.mongodb.MongoClient` 和 `com.mongodb.client.MongoClient` 均受支持。

> 如果您使用 Mongo 3.0 Java 驱动程序，则不支持 `spring.data.mongodb.host` 和 `spring.data.mongodb.port`。在这种情况下，应使用 `spring.data.mongodb.uri` 来提供所有配置。

> 如果未指定 `spring.data.mongodb.port`，则使用默认值 `27017`。您可以从前面展示的示例中删除此行。

> 如果您不使用 Spring Data Mongo，则可以注入 `com.mongodb.MongoClient` bean而不是使用 `MongoDbFactory`。如果您想完全控制建立 MongoDB 连接的方式，还可以声明自己的 `MongoDbFactory` 或 `MongoClient` bean。

> 如果您使用反应式驱动程序，则 SSL 需要 Netty。如果可以使用 Netty 并且尚未自定义要使用的工厂，则自动配置会自动配置该工厂。

