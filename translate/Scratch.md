## 3.9 内置数据库支持

`org.springframework.jdbc.datasource.embedded` 包提供了对内置 Java 数据库引擎的支持。提供了 [HSQL](http://www.hsqldb.org/), [H2](https://www.h2database.com/), 和 [Derby](https://db.apache.org/derby) 的原生支持。你也可以使用可扩展的 API 来插入新的内置数据库类型和 `DataSource` 实现。

### 3.9.1 为什么使用内置数据库？

由于其天然的轻量级特性，内置数据库在开发阶段是非常有用的。好处包括方便的配置，快速启动，可测试性，以及在开发期间频繁修改 SQL 的能力。

### 3.9.2 使用 Spring XML 创建内置数据库

如果你想要在 Spring `ApplicationContext` 中作为 bean 暴露内置数据库实例，你可以使用 `spring-jdbc` 命名空间中的 `embedded-database` 标签：

```xml
<jdbc:embedded-database id="dataSource" generate-name="true">
    <jdbc:script location="classpath:schema.sql"/>
    <jdbc:script location="classpath:test-data.sql"/>
</jdbc:embedded-database>
```

上面的配置创建一个内置 HSQL 数据库，由来自位于类路径的根目录下的 `schema.sql` 和 `test-data.sql` 资源文件中的 SQL 填充。此外，作为最佳实践，内置数据库被分配一个唯一的名称。内置数据库作为 Spring 容器中的 `javax.sql.DataSource` 类型的 bean，然后可以被按需注入数据访问对象中。

### 3.9.3 编程方式创建内置数据库

`EmbeddedDatabaseBuilder` 类提供一系列 API 用来以编程方式构造内置数据库。当你需要在独立的环境或者独立的集成测试环境中创建内置数据库时可以使用这些 API，如下面例子所示：

```java
EmbeddedDatabase db = new EmbeddedDatabaseBuilder()
        .generateUniqueName(true)
        .setType(H2)
        .setScriptEncoding("UTF-8")
        .ignoreFailedDrops(true)
        .addScript("schema.sql")
        .addScripts("user_data.sql", "country_data.sql")
        .build();

// perform actions against the db (EmbeddedDatabase extends javax.sql.DataSource)

db.shutdown()
```

参考 [javadoc for `EmbeddedDatabaseBuilder`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jdbc/datasource/embedded/EmbeddedDatabaseBuilder.html) 获取所有支持的选项。

你也可以使用 `EmbeddedDatabaseBuilder` 来创建内置数据库，使用 Java 配置。如下面例子所示：

```java
@Configuration
public class DataSourceConfig {

    @Bean
    public DataSource dataSource() {
        return new EmbeddedDatabaseBuilder()
                .generateUniqueName(true)
                .setType(H2)
                .setScriptEncoding("UTF-8")
                .ignoreFailedDrops(true)
                .addScript("schema.sql")
                .addScripts("user_data.sql", "country_data.sql")
                .build();
    }
}
```

### 3.9.4 选择内置数据库类型

本节介绍如何选择 Spring 支持的三种内置数据库。包括如下主题：

- [使用 HSQL](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-embedded-database-using-HSQL)
- [使用 H2](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-embedded-database-using-H2)
- [使用 Derby](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-embedded-database-using-Derby)

##### 使用 HSQL

Spring 支持 HSQL 1.8.0 及更高版本。如果未明确指定类型，则 HSQL 是默认的嵌入式数据库。要显式指定 HSQL，请将 `embedded-database` 标签的 `type` 属性设置为 `HSQL` 。如果您使用构建器 API，请通过 `EmbeddedDatabaseType.HSQL` 调用 `setType(EmbeddedDatabaseType)` 方法。

##### 使用 H2

Spring 支持 H2 数据库。要启用 H2，请将 `embedded-database` 标签的 `type` 属性设置为 `H2`。如果您使用构建器 API，请使用 `EmbeddedDatabaseType.H2` 调用 `setType(EmbeddedDatabaseType)` 方法。

##### 使用 Derby

Spring 支持 Apache Derby 10.5 及更高版本。要启用 Derby，请将 `embedded-database` 标签的 `type` 属性设置为 `DERBY`。如果使用构建器 API，请通过 `EmbeddedDatabaseType.DERBY` 调用 `setType(EmbeddedDatabaseType)` 方法。

### 3.9.5 使用内置数据库测试数据访问逻辑

嵌入式数据库提供了一种轻量级的方法来测试数据访问代码。下一个示例是使用嵌入式数据库的数据访问集成测试模板。当嵌入式数据库不需要在测试类之间重用时，使用这种模板可以一次性使用。但是，如果您希望创建在测试套件内共享的嵌入式数据库，请考虑使用 [Spring TestContext Framework](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-framework) ，并按照 [Creating an Embedded Database by Using Spring XML](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-embedded-database-xml) 和 [Creating an Embedded Database Programmatically](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-embedded-database-java) 中的描述，在Spring `ApplicationContext `中将嵌入式数据库配置为 Bean。以下清单显示了测试模板：

```java
public class DataAccessIntegrationTestTemplate {

    private EmbeddedDatabase db;

    @Before
    public void setUp() {
        // creates an HSQL in-memory database populated from default scripts
        // classpath:schema.sql and classpath:data.sql
        db = new EmbeddedDatabaseBuilder()
                .generateUniqueName(true)
                .addDefaultScripts()
                .build();
    }

    @Test
    public void testDataAccess() {
        JdbcTemplate template = new JdbcTemplate(db);
        template.query( /* ... */ );
    }

    @After
    public void tearDown() {
        db.shutdown();
    }

}
```

### 3.9.6 为内置数据库生成唯一名称

如果开发团队的测试套件无意中尝试重新创建同一数据库的其他实例，则经常会遇到错误。如果 XML 配置文件或 `@Configuration` 类负责创建嵌入式数据库，然后在同一测试套件（即，同一 JVM 进程中）的多个测试场景中重用相应的配置，则这种情况很容易发生 - 例如，针对嵌入式数据库的集成测试，该嵌入式数据库的 `ApplicationContext` 配置仅在哪些 bean 定义配置文件处于活动状态方面有所不同。

此类错误的根本原因是，如果没有另外指定，Spring 的 `EmbeddedDatabaseFactory`（由 XML 命名空间元素 `<jdbc:embedded-database>` 和 Java 配置的 `EmbeddedDatabaseBuilder` 内部使用）将嵌入式数据库的名称设置为 `testdb`。对于 `<jdbc:embedded-database>`，嵌入式数据库通常被分配一个与 bean 的 `id` 相同的名称（通常是类似于 `dataSource` 的名称）。因此，随后创建嵌入式数据库的尝试不会产生新的数据库。取而代之的是，相同的 JDBC 连接 URL 被重用，并且尝试创建新的嵌入式数据库实际上指向的是从相同配置创建的现有嵌入式数据库。

为了解决这类普遍问题，Spring 框架 4.2 提供了为内置数据库生成唯一名称的支持。为了启用名称生成，使用如下选项：

- `EmbeddedDatabaseFactory.setGenerateUniqueDatabaseName()`
- `EmbeddedDatabaseBuilder.generateUniqueName()`
- `<jdbc:embedded-database generate-name="true" … >`

### 3.9.7 扩展内置数据库支持

你可以通过两种方式扩展 Spring JDBC 内置数据库支持：

- 实现 `EmbeddedDatabaseConfigurer` 以支持新的内置数据库类型。
- 实现 `DataSourceFactory` 来支持新的 `DataSource` 实现，比如一个连接池来管理内置数据库连接。

我们鼓励您通过 [GitHub Issues](https://github.com/spring-projects/spring-framework/issues) 向 Spring 社区贡献新的扩展。

