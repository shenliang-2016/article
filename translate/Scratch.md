#### 4.10.2. 使用 JdbcTemplate

Spring 的 `JdbcTemplate` 和 `NamedParameterJdbcTemplate` 类都会被自动配置，你可以使用 `@Autowire` 直接将它们注入你的 beans，如下面例子所示：

```java
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.jdbc.core.JdbcTemplate;
import org.springframework.stereotype.Component;

@Component
public class MyBean {

    private final JdbcTemplate jdbcTemplate;

    @Autowired
    public MyBean(JdbcTemplate jdbcTemplate) {
        this.jdbcTemplate = jdbcTemplate;
    }

    // ...

}
```

你可以自定义该模板的一些属性，通过使用 `spring.jdbc.template.*` 属性，如下面例子所示：

```properties
spring.jdbc.template.max-rows=500
```

>  `NamedParameterJdbcTemplate` 内部复用了相同的 `JdbcTemplate` 实例。如果不只一个 `JdbcTemplate` 被定义而又不存在主要的候选者， `NamedParameterJdbcTemplate` 就不会被自动配置。

