#### 4.11.6. Cassandra

[Cassandra](https://cassandra.apache.org/) 是一个开源的分布式数据库管理系统，旨在处理许多商用服务器上的大量数据。Spring Boot 为 Cassandra 提供自动配置，并由 [Spring Data Cassandra](https://github.com/spring-projects/spring-data-cassandra) 在其之上提供抽象。有一个 `spring-boot-starter-data-cassandra` “Starter”，用于以方便的方式收集依赖项。

##### 连接 Cassandra

您可以像使用其他任何 Spring Bean 一样注入自动配置的 `CassandraTemplate` 或 Cassandra `Session` 实例。`spring.data.cassandra.*` 属性可用于自定义连接。通常，您提供 `keyspace-name` 和 `contact-points` 属性，如以下示例所示：

```properties
spring.data.cassandra.keyspace-name=mykeyspace
spring.data.cassandra.contact-points=cassandrahost1,cassandrahost2
```

您还可以注册任意数量的实现 `ClusterBuilderCustomizer` 的 Bean，以进行更高级的自定义。

以下代码清单显示了如何注入 Cassandra bean：

```java
@Component
public class MyBean {

    private CassandraTemplate template;

    @Autowired
    public MyBean(CassandraTemplate template) {
        this.template = template;
    }

    // ...

}
```

如果添加自己的 `@CassandraTemplate` 类型的 `@Bean`，它将替换默认值。

##### Spring Data Cassandra Repositories

Spring Data 包含对 Cassandra 的基本存储库支持。当前，它比前面讨论的 JPA 存储库受到更多限制，并且需要使用 `@Query` 注解查找器方法。

> 有关 Spring Data Cassandra 的完整细节，请参考 [reference documentation](https://docs.spring.io/spring-data/cassandra/docs/)。

