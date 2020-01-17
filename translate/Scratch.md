#### 4.10.4. Spring Data JDBC

Spring Data 包括对 JDBC 的存储库支持，并将自动为 `CrudRepository` 上的方法生成 SQL。对于更高级的查询，提供了一个 `@Query` 注解。

当必要的依赖项位于类路径上时，Spring Boot 将自动配置 Spring Data 的 JDBC 存储库。可以将它们添加到您的项目中，而只需依赖于 `spring-boot-starter-data-jdbc`。如有必要，您可以通过向应用程序添加 `@EnableJdbcRepositories` 注解或 `JdbcConfiguration` 子类来控制 Spring Data JDBC 的配置。

> 关于 Spring Data JDBC 的完整细节，请参考 [reference documentation](https://docs.spring.io/spring-data/jdbc/docs/1.1.3.RELEASE/reference/html/) 。

#### 4.10.5. 使用 H2 的 Web 控制台

[H2 database](https://www.h2database.com/) 提供一个 [browser-based console](https://www.h2database.com/html/quickstart.html#h2_console) ，Spring Boot 能够为你自动配置。当下列条件满足时该控制台会被自动配置：

- 你在开发的是基于 servlet 的 web 应用。
- `com.h2database:h2` 在类路径上。
- 你正在使用 [Spring Boot’s developer tools](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#using-boot-devtools) 。

> 如果你没有使用 Spring Boot 的开发工具，仍然可以使用 H2 的控制台，你可以将 `spring.h2.console.enabled` 属性设置为 `true`。

> H2 控制台应该仅在开发过程中使用，因此，你需要保证生产环境中 `spring.h2.console.enabled` 属性没有设定为 `true` 。

##### 修改 H2 控制台路径

默认情况下，控制台的访问路径是 `/h2-console`。你可以通过使用 `spring.h2.console.path` 属性来自定义控制台访问路径。