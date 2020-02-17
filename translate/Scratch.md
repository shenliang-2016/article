##### 自动配置的 Data Neo4j 测试

您可以使用 `@DataNeo4jTest` 来测试 Neo4j 应用程序。默认情况下，它使用内存中嵌入式 Neo4j（如果有嵌入式驱动程序可用），扫描 `@NodeEntity` 类，并配置 Spring Data Neo4j 存储库。常规的 `@Component` Bean 不会加载到 `ApplicationContext` 中。（有关将 Neo4J 与 Spring Boot 结合使用的更多信息，请参阅在本章前面的 [Neo4j](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-neo4j)）

> 由 `@DataNeo4jTest` 开启的自动配置设定列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

下面的例子展示了在 Spring Boot 中使用 Neo4J 测试的典型设定：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.data.neo4j.DataNeo4jTest;

@DataNeo4jTest
class ExampleDataNeo4jTests {

    @Autowired
    private YourRepository repository;

    //
}
```

默认情况下，Data Neo4j 测试是事务性的，并在每次测试结束时回滚。请参阅 Spring Framework 参考文档中的 [相关部分](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#testcontext-tx-enabling-transactions) 有关更多详细信息。如果这不是您想要的，则可以为测试或整个类禁用事务管理，如下所示：

```java
import org.springframework.boot.test.autoconfigure.data.neo4j.DataNeo4jTest;
import org.springframework.transaction.annotation.Propagation;
import org.springframework.transaction.annotation.Transactional;

@DataNeo4jTest
@Transactional(propagation = Propagation.NOT_SUPPORTED)
class ExampleNonTransactionalTests {

}
```