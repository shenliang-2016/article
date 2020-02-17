##### 自动配置的 Data MongoDB 测试

您可以使用 `@DataMongoTest` 来测试 MongoDB 应用程序。默认情况下，它配置内存嵌入式 MongoDB（如果可用），配置 `MongoTemplate`，扫描 `@Document` 类，并配置 Spring Data MongoDB 存储库。常规的 `@Component` Bean不会加载到 `ApplicationContext` 中。（有关将 MongoDB 与 Spring Boot 结合使用的更多信息，参见在本章前面的 [MongoDB](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-mongodb) ）

> 由 `@DataMongoTest` 开启的自动配置设定列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

下面的类展示了 `@DataMongoTest` 注解的使用：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.data.mongo.DataMongoTest;
import org.springframework.data.mongodb.core.MongoTemplate;

@DataMongoTest
class ExampleDataMongoTests {

    @Autowired
    private MongoTemplate mongoTemplate;

    //
}
```

内存嵌入式 MongoDB 通常运行良好，不需要任何开发人员安装，因此通常可以很好地用于测试。但是，如果您希望对真实的 MongoDB 服务器运行测试，则应排除嵌入式 MongoDB 自动配置，如以下示例所示：

```java
import org.springframework.boot.autoconfigure.mongo.embedded.EmbeddedMongoAutoConfiguration;
import org.springframework.boot.test.autoconfigure.data.mongo.DataMongoTest;

@DataMongoTest(excludeAutoConfiguration = EmbeddedMongoAutoConfiguration.class)
class ExampleDataMongoNonEmbeddedTests {

}
```