##### 自动配置的 Data JPA 测试

您可以使用 `@DataJpaTest` 注解来测试 JPA 应用程序。默认情况下，它扫描 `@Entity` 类并配置 Spring Data JPA 存储库。如果在类路径上有嵌入式数据库，它也会配置一个。常规的 `@Component` Bean不会加载到 `ApplicationContext` 中。

> `@DataJpaTest` 能够开启的自动配置设定列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

默认情况下，数据 JPA 测试是事务性的，并在每次测试结束时回滚。请参阅 Spring Framework 参考文档中的 [相关部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#testcontext-tx-enabling-transactions) 了解更多详细信息。如果这不是您想要的，则可以按以下方式禁用测试或整个类的事务管理：

```java
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.autoconfigure.orm.jpa.DataJpaTest;
import org.springframework.transaction.annotation.Propagation;
import org.springframework.transaction.annotation.Transactional;

@DataJpaTest
@Transactional(propagation = Propagation.NOT_SUPPORTED)
class ExampleNonTransactionalTests {

}
```

数据 JPA 测试也可以注入 [`TestEntityManager`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot-test-autoconfigure/src/main/java/org/springframework/boot/test/autoconfigure/orm/jpa/TestEntityManager.java) bean，它提供了专门为测试设计的标准 JPA `EntityManager` 的替代方案。如果您要在 `@DataJpaTest` 实例之外使用 `TestEntityManager`，则还可以使用 `@AutoConfigureTestEntityManager` 注解。如果需要，也可以使用 `JdbcTemplate`。以下示例显示了使用中的 `@DataJpaTest` 注解：

```java
import org.junit.jupiter.api.Test;
import org.springframework.boot.test.autoconfigure.orm.jpa.*;

import static org.assertj.core.api.Assertions.*;

@DataJpaTest
class ExampleRepositoryTests {

    @Autowired
    private TestEntityManager entityManager;

    @Autowired
    private UserRepository repository;

    @Test
    void testExample() throws Exception {
        this.entityManager.persist(new User("sboot", "1234"));
        User user = this.repository.findByUsername("sboot");
        assertThat(user.getUsername()).isEqualTo("sboot");
        assertThat(user.getVin()).isEqualTo("1234");
    }

}
```

内存嵌入式数据库通常运行良好，不需要任何安装，因此通常可以很好地进行测试。但是，如果您希望对真实数据库运行测试，则可以使用 `@AutoConfigureTestDatabase` 注解，如以下示例所示：

```java
@DataJpaTest
@AutoConfigureTestDatabase(replace=Replace.NONE)
class ExampleRepositoryTests {

    // ...

}
```

