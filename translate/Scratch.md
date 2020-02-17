##### 自动配置的 Data JDBC 测试

`@DataJdbcTest` 类似于 `@JdbcTest` ，不过是用于使用 Spring Data JDBC 存储仓库的测试。默认情况下，它配置一个内存嵌入式数据库，一个 `JdbcTemplate`，以及 Spring Data JDBC 存储仓库。普通的 `@Component` beans 不会被加载进入 `ApplicationContext`。

> 由 `@DataJdbcTest` 开启的自动配置列表放在 [附录](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#test-auto-configuration) 中。

默认地，Data JDBC 测试是事务性的，会在每个测试结束之后回滚。参考 Spring Framework 参考文档的 [相关章节](https://docs.spring.io/spring/docs/5.2.2.RELEASE/spring-framework-reference/testing.html#testcontext-tx-enabling-transactions) 获取更多细节。如果这不是你希望的，你可以为单个测试用例或者整个测试类关闭事务管理，如 [JDBC 示例](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-jdbc-test) 中所示。

如果你想要你的测试运行在真实的数据库上，你可以使用 `@AutoConfigureTestDatabase` 注解，以与 `DataJpaTest` 相同的方式。 (参考 "[自动配置的 Data JPA 测试](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-jpa-test)".)

