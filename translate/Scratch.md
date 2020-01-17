#### 4.10.6. 使用 jOOQ

jOOQ Object Oriented Querying ([jOOQ](https://www.jooq.org/)) 是一个来自 [Data Geekery](https://www.datageekery.com/) 的非常流行的产品，它可以依据你的数据库生成 Java 代码并帮助你通过它提供的链式 API 构建类型安全的 SQL 查询。商业版和开源版产品都可以在 Spring Boot 中使用。

##### 代码生成

为了使用 jOOQ 类型安全查询，您需要从数据库模式中生成 Java 类。您可以按照 [jOOQ用户手册](https://www.jooq.org/doc/3.12.3/manual-single-page/#jooq-in-7-steps-step3) 中的说明进行操作。如果您使用 `jooq-codegen-maven` 插件，并且还使用 `spring-boot-starter-parent` “父POM”，则可以安全地忽略该插件的 `<version>` 标签。您还可以使用 Spring Boot 定义的版本变量（例如 `h2.version`）来声明插件的数据库依赖项。以下清单显示了一个示例：

```xml
<plugin>
    <groupId>org.jooq</groupId>
    <artifactId>jooq-codegen-maven</artifactId>
    <executions>
        ...
    </executions>
    <dependencies>
        <dependency>
            <groupId>com.h2database</groupId>
            <artifactId>h2</artifactId>
            <version>${h2.version}</version>
        </dependency>
    </dependencies>
    <configuration>
        <jdbc>
            <driver>org.h2.Driver</driver>
            <url>jdbc:h2:~/yourdatabase</url>
        </jdbc>
        <generator>
            ...
        </generator>
    </configuration>
</plugin>
```

##### 使用 DSLContext

jOOQ 提供的链式 API 是通过 `org.jooq.DSLContext` 接口启动的。Spring Boot 将一个 `DSLContext` 自动配置为一个 Spring Bean，并将其连接到您的应用程序 `DataSource`。要使用 `DSLContext`，可以使用 `@Autowire`，如以下示例所示：

```java
@Component
public class JooqExample implements CommandLineRunner {

    private final DSLContext create;

    @Autowired
    public JooqExample(DSLContext dslContext) {
        this.create = dslContext;
    }

}
```

> jOOQ 手册使用名为 `create` 的变量来持有 `DSLContext`。

然后，你可以使用 `DSLContext` 来构建你的查询，如下面例子所示：

```java
public List<GregorianCalendar> authorsBornAfter1980() {
    return this.create.selectFrom(AUTHOR)
        .where(AUTHOR.DATE_OF_BIRTH.greaterThan(new GregorianCalendar(1980, 0, 1)))
        .fetch(AUTHOR.DATE_OF_BIRTH);
}
```

##### jOOQ SQL 方言

除非 `spring.jooq.sql-dialect` 属性已经被配置，Spring Boot 决定用于你的数据库的 SQL 方言。如果 Spring Boot 无法探测到方言，使用 `DEFAULT`。

> Spring Boot 只能自动配置开源版本的 jOOQ 支持的方言。

##### 自定义 jOOQ

可以通过定义自己的 `@Bean` 定义来实现更高级的自定义，这在创建 jOOQ `Configuration` 时使用。您可以为以下 jOOQ 类型定义 bean：

- `ConnectionProvider`
- `ExecutorProvider`
- `TransactionProvider`
- `RecordMapperProvider`
- `RecordUnmapperProvider`
- `Settings`
- `RecordListenerProvider`
- `ExecuteListenerProvider`
- `VisitListenerProvider`
- `TransactionListenerProvider`

如果您想完全控制 jOOQ 配置，也可以创建自己的 `org.jooq.Configuration` `@Bean`。

