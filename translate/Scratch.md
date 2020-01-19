#### 4.11.4. Solr

[Apache Solr](https://lucene.apache.org/solr/) 是一个搜索引擎。Spring Boot 为 Solr 5 客户端库提供了基本的自动配置，并由 [Spring Data Solr](https://github.com/spring-projects/spring-data-solr) 在其之上提供了抽象。`spring-boot-starter-data-solr` "Starter" 是用来集合所需依赖的便捷方式。

##### 连接到 Solr

您可以像注入其他任何 Spring Bean 一样注入自动配置的 `SolrClient` 实例。默认情况下，该实例尝试连接到位于 `localhost:8983/solr` 的服务器。下面的示例显示如何注入 Solr bean：

```java
@Component
public class MyBean {

    private SolrClient solr;

    @Autowired
    public MyBean(SolrClient solr) {
        this.solr = solr;
    }

    // ...

}
```

如果你添加自己的 `SolrClient` 类型的 `@Bean` ，它将替换默认的实例。

##### Spring Data Solr Repositories

Spring Data 包含对 Apache Solr 的存储库支持。与前面讨论的 JPA 存储库一样，基本原理是根据方法名称自动为您构建查询。

实际上，Spring Data JPA 和 Spring Data Solr 共享相同的通用基础结构。您可以从以前的 JPA 示例开始，并假定 `City` 现在是 `@SolrDocument` 类，而不是 JPA `@Entity`，它的工作方式相同。

Spring Data Solr 的完整细节，请参考 [reference documentation](https://docs.spring.io/spring-data/solr/docs/4.1.3.RELEASE/reference/html/)。

