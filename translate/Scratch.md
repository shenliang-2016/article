##### 自动配置的 Data Redis 测试

你可以使用 `@DataRedisTest` 来测试 Redis 应用程序。默认情况下，它会扫描 `@RedisHash` 类并配置 Spring Data Redis 存储库。常规的 `@Component` Bean 不会加载到 `ApplicationContext` 中。（有关将 Redis 与 Spring Boot 结合使用的更多信息，参见 [Redis](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-redis) 。）

> 由 `@DataRedisTest` 开启的自动配置设定列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

下面的例子展示了 `@DataRedisTest` 注解的使用：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.data.redis.DataRedisTest;

@DataRedisTest
class ExampleDataRedisTests {

    @Autowired
    private YourRepository repository;

    //
}
```

