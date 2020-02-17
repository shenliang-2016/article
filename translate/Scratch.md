##### 自动配置的 jOOQ 测试

您可以使用与 `@JdbcTest` 类似的方式来使用 `@JooqTest`，但是可以进行与 jOOQ 相关的测试。由于 jOOQ 严重依赖与数据库模式相对应的基于 Java 的模式，因此将使用现有的 `DataSource`。如果要用内存数据库替换它，则可以使用 `@AutoConfigureTestDatabase` 覆盖那些设置。（有关将 jOOQ 与 Spring Boot 结合使用的更多信息，请参阅本章的前面的 “ [使用jOOQ](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-jooq) “。）常规的 `@Component` Bean不会加载到 `ApplicationContext` 中。

> 由 `@JooqTest` 开启的自动配置列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

`@JooqTest` 配置一个 `DSLContext`。普通的 `@Component` beans 不会被加载进入 `ApplicationContext`。下面的例子展示了 `@JooqTest` 注解使用：

```java
import org.jooq.DSLContext;
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.autoconfigure.jooq.JooqTest;

@JooqTest
class ExampleJooqTests {

    @Autowired
    private DSLContext dslContext;
}
```

JOOQ 测试是事务性的，每个测试结束之后就会回滚。如果这不是你想要的，可以为单个测试用例或者整个测试类关闭事务管理，如 [JDBC 示例](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-jdbc-test) 中所示。

