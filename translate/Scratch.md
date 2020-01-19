#### 4.11.7. Couchbase

[Couchbase](https://www.couchbase.com/) 是一个开源的，分布式，多模型的 NoSQL 面向文档的数据库，已针对交互式应用程序进行了优化。Spring Boot 提供了对 Couchbase 的自动配置，并由 [Spring Data Couchbase](https://github.com/spring-projects/spring-data-couchbase) 在其之上提供了抽象。有 `spring-boot-starter-data-couchbase` 和 `spring-boot-starter-data-couchbase-reactive` “Starters”，用于以方便的方式收集依赖项。

##### 连接 Couchbase

您可以通过添加 Couchbase SDK 和一些配置来获取 `Bucket` 和 `Cluster`。可以使用 `spring.couchbase.*` 属性来自定义连接。通常，您提供引导主机，存储桶名称和密码，如以下示例所示：

```properties
spring.couchbase.bootstrap-hosts=my-host-1,192.168.1.123
spring.couchbase.bucket.name=my-bucket
spring.couchbase.bucket.password=secret
```

> 您*至少*需要提供引导主机，在这种情况下，存储区名称为 `default` ，密码为空字符串。另外，您可以定义自己的 `org.springframework.data.couchbase.config.CouchbaseConfigurer` `@Bean` 以控制整个配置。

也可以自定义某些 `CouchbaseEnvironment` 设置。例如，以下配置更改了用于打开新的 `Bucket` 并启用 SSL 支持的超时：

```properties
spring.couchbase.env.timeouts.connect=3000
spring.couchbase.env.ssl.key-store=/location/of/keystore.jks
spring.couchbase.env.ssl.key-store-password=secret
```

检查 `spring.couchbase.env.*` 属性获取更多细节。

##### Spring Data Couchbase Repositories

Spring Data 包括对 Couchbase 的存储库支持。有关 Spring Data Couchbase 的完整详细信息，请参考 [参考文档](https://docs.spring.io/spring-data/couchbase/docs/current/reference/html/)。

您可以像使用任何其他 Spring Bean 一样注入自动配置的 `CouchbaseTemplate` 实例，前提是 *default* `CouchbaseConfigurer` 可用（如前所述，启用 Couchbase 支持时会发生这种情况）。

以下示例显示了如何注入 Couchbase bean：

```java
@Component
public class MyBean {

    private final CouchbaseTemplate template;

    @Autowired
    public MyBean(CouchbaseTemplate template) {
        this.template = template;
    }

    // ...

}
```

您可以在自己的配置中定义一些 Bean，以覆盖自动配置提供的那些：

- 一个名为 `CouchbaseTemplate` `@Bean`的名称。

- 名称为 `couchbaseIndexManager的IndexManager` `@Bean`。

- 名称为 `couchbaseCustomConversions` 的 CustomBeans `@Bean`。

为了避免在您自己的配置中对这些名称进行硬编码，您可以重用 Spring Data Couchbase 提供的 `BeanNames`。例如，您可以自定义要使用的转换器，如下所示：

```java
@Configuration(proxyBeanMethods = false)
public class SomeConfiguration {

    @Bean(BeanNames.COUCHBASE_CUSTOM_CONVERSIONS)
    public CustomConversions myCustomConversions() {
        return new CustomConversions(...);
    }

    // ...

}
```

> 如果您想完全绕过Spring Data Couchbase的自动配置，请提供您自己的`org.springframework.data.couchbase.config.AbstractCouchbaseDataConfiguration` 实现。

