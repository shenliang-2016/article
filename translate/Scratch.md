##### Spring Data JPA Repositories

[Spring Data JPA](https://spring.io/projects/spring-data-jpa) 存储库是可以定义以访问数据的接口。JPA 查询是根据您的方法名称自动创建的。例如， `CityRepository` 接口可能会声明 `findAllByState(String state)` 方法以查找处于给定状态的所有城市。

对于更复杂的查询，您可以使用 Spring Data 的 [`Query`](https://docs.spring.io/spring-data/jpa/docs/2.2.3.RELEASE/api/org/springframework/data/jpa/repository/Query.html) 注解。

Spring Data 存储库通常从 [`Repository`](https://docs.spring.io/spring-data/commons/docs/2.2.3.RELEASE/api/org/springframework/data/repository/Repository.html ) 或 [`CrudRepository`](https://docs.spring.io/spring-data/commons/docs/2.2.3.RELEASE/api/org/springframework/data/repository/CrudRepository.html) 接口。如果您使用自动配置，则会从包含您的主要配置类（用 `@EnableAutoConfiguration` 或 `@SpringBootApplication` 注解的类）的包中搜索存储库。

以下示例显示了典型的 Spring Data 存储库接口定义：

```java
package com.example.myapp.domain;

import org.springframework.data.domain.*;
import org.springframework.data.repository.*;

public interface CityRepository extends Repository<City, Long> {

    Page<City> findAll(Pageable pageable);

    City findByNameAndStateAllIgnoringCase(String name, String state);

}
```

Spring Data JPA 存储库支持三种不同的引导模式：默认，延迟和惰性。要启用延迟引导或惰性引导，请将 `spring.data.jpa.repositories.bootstrap-mode` 属性分别设置为 `deferred` 或 `lazy`。当使用延迟或惰性引导时，自动配置的 `EntityManagerFactoryBuilder` 将使用上下文的 `AsyncTaskExecutor`（如果有）作为引导执行器。如果存在多个，将使用一个名为 `applicationTaskExecutor` 的应用。

> 我们仅仅是走马观花一般概述 Spring Data JPA 的表面特性。完整的细节，请参考 [Spring Data JPA reference documentation](https://docs.spring.io/spring-data/jdbc/docs/1.1.3.RELEASE/reference/html/) 。

##### 创建和丢弃 JPA Databases

默认情况下，仅当您使用内置数据库（H2，HSQL 或 Derby），才会自动创建 JPA 数据库。您可以通过使用 `spring.jpa.*` 属性显式配置 JPA 设置。例如，要创建和删除表，可以在 `application.properties` 中添加以下行：

```
spring.jpa.hibernate.ddl-auto=create-drop
```

> Hibernate 自己的内部属性名称（如果您记得更好的话）是 `hibernate.hbm2ddl.auto`。您可以通过使用 `spring.jpa.properties.*`（在将前缀添加到实体管理器之前删除前缀）来设置它以及其他 Hibernate 本地属性。下面的行显示了为 Hibernate 设置 JPA 属性的示例：

```
spring.jpa.properties.hibernate.globally_quoted_identifiers=true
```

前面示例中的行将 `hibernate.globally_quoted_identifiers` 属性的值 `true` 传递给 Hibernate 实体管理器。

默认情况下，DDL 执行（或验证）推迟到 `ApplicationContext` 启动之前。还有一个 `spring.jpa.generate-ddl` 标志，但是如果启用了休眠自动配置，则不会使用它，因为 `ddl-auto` 设置更细粒度。

##### 在视图中打开 EntityManager

如果您正在运行 Web 应用程序，则 Spring Boot 默认会注册 [`OpenEntityManagerInViewInterceptor`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/orm/jpa/support/OpenEntityManagerInViewInterceptor.html) 以应用“在视图中打开 EntityManager”模式，以允许在 Web 视图中进行惰性加载。如果您不希望出现这种情况，则应在 `application.properties` 中将 `spring.jpa.open-in-view` 设置为 `false`。

