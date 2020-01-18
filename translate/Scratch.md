#### 4.11.3. Neo4j

[Neo4j](https://neo4j.com/) 是一种开源的 NoSQL 图数据库，使用丰富的数据模型，该模型由通过第一类关系相互连接的节点组成，这种模型相对于传统 RDBMS 方式更加适合相互关联的大数据。Spring Boot 提供了一系列方便的工具来使用 Neo4j，包括 `spring-boot-starter-data-neo4j` “Starter”。

##### 连接到 Neo4j 数据库

为了访问 Neo4j 服务器，你可以注入一个自动配置的 `org.neo4j.ogm.session.Session`。默认情况下，实例尝试使用 Bolt 协议通过 `localhost:7687` 连接 Neo4j 服务器。下面的例子展示了如何注入 Neo4j `Session` ：

```java
@Component
public class MyBean {

    private final Session session;

    @Autowired
    public MyBean(Session session) {
        this.session = session;
    }

    // ...

}
```

你可以通过设定 `spring.data.neo4j.*` 属性配置需要使用的 url 和身份凭证，如下面例子所示：

```properties
spring.data.neo4j.uri=bolt://my-server:7687
spring.data.neo4j.username=neo4j
spring.data.neo4j.password=secret
```

你可以通过添加 `org.neo4j.ogm.config.Configuration` bean 或者 `org.neo4j.ogm.session.SessionFactory` bean 获取对会话创建的完全控制。

##### 使用内置模式

如果你添加 `org.neo4j:neo4j-ogm-embedded-driver` 到你的应用依赖中，Spring Boot 将自动配置一个同进程的内置 Neo4j 实例，你的应用关闭时不会有任何数据被持久化。

> 由于嵌入式 Neo4j OGM 驱动程序本身不提供 Neo4j 内核，因此您必须自己声明 `org.neo4j:neo4j` 作为依赖项。有关兼容版本的列表，请参阅 [Neo4j OGM文档](https://neo4j.com/docs/ogm-manual/current/reference/#reference:getting-started) 。

当类路径上有多个驱动程序时，内置驱动程序优先于其他驱动程序。您可以通过设置 `spring.data.neo4j.embedded.enabled=false` 显式禁用内置模式。

如果内置驱动程序和 Neo4j 内核位于上述类路径上，则 [Data Neo4j Tests](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-autoconfigured-neo4j-test) 会自动使用内置 Neo4j 实例。

> 您可以通过在配置中提供数据库文件的路径来启用内置模式的持久性。比如 `spring.data.neo4j.uri=file://var/tmp/graph.db`。

##### 使用本地类型

Neo4j-OGM 可以将某些类型（例如，`java.time.*` 中的类型）映射到基于 `String` 的属性或 Neo4j 提供的本地类型之一。出于向后兼容的原因，Neo4j-OGM 的默认设置是使用基于字符串的表示形式。要使用本地类型，请添加对 `org.neo4j:neo4j-ogm-bolt-native-types` 或 `org.neo4j:neo4j-ogm-embedded-native-types` 的依赖，并配置 `spring.data.neo4j.use-native-types` 属性，如以下示例所示：

```properties
spring.data.neo4j.use-native-types=true
```

##### Neo4jSession

默认情况下，如果您正在运行 Web 应用程序，则会话将绑定到线程以进行请求的整个处理（即，它使用“在视图中打开会话”模式）。如果您不希望出现这种情况，请将以下行添加到您的 `application.properties` 文件中：

```properties
spring.data.neo4j.open-in-view=false
```

##### Spring Data Neo4j Repositories

Spring Data 包括对 Neo4j 的存储库支持。

Spring Data Neo4j 与许多其他 Spring Data 模块一样，与 Spring Data JPA 共享公共基础结构。您可以以前面的 JPA 示例为例，将 `City` 定义为 Neo4j OGM `@NodeEntity` 而不是 JPA `@Entity`，并且存储库抽象以相同的方式工作，如以下示例所示：

```java
package com.example.myapp.domain;

import java.util.Optional;

import org.springframework.data.neo4j.repository.*;

public interface CityRepository extends Neo4jRepository<City, Long> {

    Optional<City> findOneByNameAndState(String name, String state);

}
```

`spring-boot-starter-data-neo4j` “Starter” 可启用存储库支持以及事务管理。您可以通过在 `@Configuration` bean上分别使用 `@EnableNeo4jRepositories` 和 `@EntityScan` 来定制位置以查找存储库和实体。

> 有关 Spring Data Neo4j 的完整详细信息，包括其对象映射技术，请参阅 [参考文档](https://docs.spring.io/spring-data/neo4j/docs/5.2.3.RELEASE/reference/html/ )。

