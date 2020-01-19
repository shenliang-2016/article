#### 4.11.5. Elasticsearch

[Elasticsearch](https://www.elastic.co/products/elasticsearch) 是一个开源的，分布式，RESTful 搜索和分析引擎。Spring Boot 提供了 Elasticsearch 基本的自动配置。

Spring Boot 支持几种客户端：

- 官方 Java “高级”和“低级” REST 客户端
- 由 Spring Data Elasticsearch 提供的 `ReactiveElasticsearchClient` 

传输客户端仍然可用，但是 [Spring Data Elasticsearch](https://github.com/spring-projects/spring-data-elasticsearch) 和 Elasticsearch 本身已弃用了它的支持。它将在将来的版本中删除。Spring Boot 提供了专用的 “Starter”，即 `spring-boot-starter-data-elasticsearch`。

[Jest](https://github.com/searchbox-io/Jest) 客户端也已被弃用，因为 Elasticsearch 和 Spring Data Elasticsearch 都为 REST 客户端提供了官方支持。

##### 使用 REST 客户端连接 Elasticsearch

Elasticsearch 附带了 [两个不同的 REST 客户端](https://www.elastic.co/guide/en/elasticsearch/client/java-rest/current/index.html)，您可以用来查询集群：“低级"客户端和“高级”客户端。

如果您的类路径具有 `org.elasticsearch.client:elasticsearch-rest-client` 依赖，Spring Boot 将自动配置并注册一个默认情况下以 `localhost:9200` 为目标的 `RestClient` bean。您可以进一步调整 `RestClient` 的配置方式，如以下示例所示：

```properties
spring.elasticsearch.rest.uris=https://search.example.com:9200
spring.elasticsearch.rest.read-timeout=10s
spring.elasticsearch.rest.username=user
spring.elasticsearch.rest.password=secret
```

您还可以注册任意数量的实现 `RestClientBuilderCustomizer` 的 Bean，以进行更高级的自定义。要完全控制注册，请定义一个 `RestClient` bean。

如果您的类路径具有 `org.elasticsearch.client:elasticsearch-rest-high-level-client` 依赖，Spring Boot 将自动配置一个 `RestHighLevelClient`，它包装任何现有的 `RestClient` bean，并复用其 HTTP 配置。

##### 使用 Reactive REST 客户端连接 Elasticsearch

[Spring Data Elasticsearch](https://spring.io/projects/spring-data-elasticsearch) 附带了 `ReactiveElasticsearchClient`，用于以反应方式查询 Elasticsearch 实例。它建立在 `WebFlux的WebClient` 之上，因此 `spring-boot-starter-elasticsearch` 和 `spring-boot-starter-webflux` 依赖对于启用此支持很有用。

默认情况下，Spring Boot 将自动配置并注册一个以 `localhost:9200` 为目标的 `ReactiveElasticsearchClient` bean。您可以进一步调整其配置，如以下示例所示：

```properties
spring.data.elasticsearch.client.reactive.endpoints=search.example.com:9200
spring.data.elasticsearch.client.reactive.use-ssl=true
spring.data.elasticsearch.client.reactive.socket-timeout=10s
spring.data.elasticsearch.client.reactive.username=user
spring.data.elasticsearch.client.reactive.password=secret
```

如果配置属性还不够，并且您想完全控制客户端配置，则可以注册自定义 `ClientConfiguration` bean。

##### 使用 Jest 连接 Elasticsearch

现在，Spring Boot 支持官方的 `RestHighLevelClient`，不建议使用 Jest。

如果您在类路径上具有 `Jest`，则可以注入自动配置的 `JestClient`，默认情况下，其目标是 `localhost:9200`。您可以进一步调整客户端的配置方式，如以下示例所示：

```properties
spring.elasticsearch.jest.uris=https://search.example.com:9200
spring.elasticsearch.jest.read-timeout=10000
spring.elasticsearch.jest.username=user
spring.elasticsearch.jest.password=secret
```

您也可以注册任意数量的实现 `HttpClientConfigBuilderCustomizer` 的 bean，以进行更高级的自定义。以下示例调整其他 HTTP 设置：

```java
static class HttpSettingsCustomizer implements HttpClientConfigBuilderCustomizer {

    @Override
    public void customize(HttpClientConfig.Builder builder) {
        builder.maxTotalConnection(100).defaultMaxTotalConnectionPerRoute(5);
    }

}
```

要完全控制注册，请定义一个 `JestClient` bean。

##### 使用 Spring Data 连接 Elasticsearch

要连接到 Elasticsearch，必须定义一个 `RestHighLevelClient` bean，它由 Spring Boot 自动配置或由应用程序手动提供（请参阅前面的部分）。有了此配置后，可以像其他任何 Spring bean 一样注入 `ElasticsearchRestTemplate`，如以下示例所示：

```java
@Component
public class MyBean {

    private final ElasticsearchRestTemplate template;

    public MyBean(ElasticsearchRestTemplate template) {
        this.template = template;
    }

    // ...

}
```

在存在 `spring-data-elasticsearch` 和使用 `WebClient` 所需的依赖项（通常是 `spring-boot-starter-webflux`）的情况下，Spring Boot 还可以自动配置 [ReactiveElasticsearchClient](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-connecting-to-elasticsearch-reactive-rest)  和一个 `ReactiveElasticsearchTemplate` 作为 bean。它们与其他 REST 客户端是等效的。

##### Spring Data Elasticsearch Repositories

Spring Data 包括对 Elasticsearch 的存储库支持。与前面讨论的 JPA 存储库一样，基本原理是根据方法名称自动为您构造查询。

实际上，Spring Data JPA 和 Spring Data Elasticsearch 共享相同的通用基础架构。您可以从前面的 JPA 示例开始，并假设 `City` 现在是 Elasticsearch `@Document` 类，而不是 JPA `@Entity`，它的工作方式相同。

> 有关 Spring Data Elasticsearch 的完整细节，请参考 [reference documentation](https://docs.spring.io/spring-data/elasticsearch/docs/current/reference/html/) 。

Spring Boot 使用 `ElasticsearchRestTemplate` 或 `ReactiveElasticsearchTemplate` bean 支持经典和反应式 Elasticsearch 存储库。给定所需的依赖项，这些 bean 最有可能由 Spring Boot 自动配置。

如果您希望使用自己的模板来支持 Elasticsearch 存储库，则可以添加自己的 `ElasticsearchRestTemplate` 或 `ElasticsearchOperations` `@Bean`，只要将其命名为 `"elasticsearchTemplate"` 即可。同样的情况也适用于 `ReactiveElasticsearchTemplate` 和 `ReactiveElasticsearchOperations`，bean 名称为 `"reactiveElasticsearchTemplate"`。

您可以选择使用以下属性禁用存储库支持：

```properties
spring.data.elasticsearch.repositories.enabled=false
```

