##### 自动配置的 JDBC 测试

`@JdbcTest` 与 `@DataJpaTest` 类似，但适用于仅需要 `DataSource` 且不使用 Spring Data JDBC 的测试。默认情况下，它配置一个内存嵌入式数据库和一个 `JdbcTemplate`。常规的 `@Component` Bean 不会加载到 `ApplicationContext` 中。

> `@JdbcTest` 能够开启的自动配置设定列表参见 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 。

缺省情况下，JDBC 测试是事务性的，并在每次测试结束时回滚。请参阅 Spring Framework 参考文档中的 [相关部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#testcontext-tx-enabling-transactions) 了解更多详细信息。如果这不是您想要的，则可以为测试或整个类禁用事务管理，如下所示：

```java
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.autoconfigure.jdbc.JdbcTest;
import org.springframework.transaction.annotation.Propagation;
import org.springframework.transaction.annotation.Transactional;

@JdbcTest
@Transactional(propagation = Propagation.NOT_SUPPORTED)
class ExampleNonTransactionalTests {

}
```

如果您希望测试针对真实数据库运行，则可以使用 `@AutoConfigureTestDatabase` 注解，方法与对 `DataJpaTest` 的方法相同。（请参阅 “[自动配置的 Data JPA 测试](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-jpa-test)”）

