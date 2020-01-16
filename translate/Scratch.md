#### 4.10.3. JPA 和 Spring Data JPA

Java Persistence API 是一种标准技术，允许你将对象映射到关系数据库。`spring-boot-starter-data-jpa` POM 提供了一种快捷的入手方式。它提供了下面的关键依赖：

- Hibernate: 一种最流行的 JPA 实现。
- Spring Data JPA: 使基于 JPA 的存储库的实现变得容易。
- Spring ORMs: Spring Framework 中的核心 ORM 支持。

> 本章节我们并不深入太多 JPA 或者 [Spring Data](https://spring.io/projects/spring-data) 的细节。你可以参考 [spring.io](https://spring.io/) 上的 [“Accessing Data with JPA”](https://spring.io/guides/gs/accessing-data-jpa/) 文档以及 [Spring Data JPA](https://spring.io/projects/spring-data-jpa) 和 [Hibernate](https://hibernate.org/orm/documentation/) 参考文档。

##### Entity 类

传统上，JPA “Entity” 类是在 `persistence.xml` 文件中指定的。在 Spring Boot 中，此文件不是必需的，而是使用 “实体扫描”。默认情况下，将搜索主配置类（用 `@EnableAutoConfiguration` 或 `@SpringBootApplication` 注解修饰的软件包）下的所有软件包。

任何带有 `@Entity`，`@Embeddable` 或 `@MappedSuperclass` 注解修饰的类。典型的实体类类似于以下示例：

```java
package com.example.myapp.domain;

import java.io.Serializable;
import javax.persistence.*;

@Entity
public class City implements Serializable {

    @Id
    @GeneratedValue
    private Long id;

    @Column(nullable = false)
    private String name;

    @Column(nullable = false)
    private String state;

    // ... additional members, often include @OneToMany mappings

    protected City() {
        // no-args constructor required by JPA spec
        // this one is protected since it shouldn't be used directly
    }

    public City(String name, String state) {
        this.name = name;
        this.state = state;
    }

    public String getName() {
        return this.name;
    }

    public String getState() {
        return this.state;
    }

    // ... etc

}
```

> 你可以自定义实体扫描位置，通过使用 `@EntityScan` 注解。参考 “[Separate @Entity Definitions from Spring Configuration](https://docs.spring.io/spring-boot/docs/2.2.2.RELEASE/reference/htmlsingle/#howto-separate-entity-definitions-from-spring-configuration)” 了解如何做。

