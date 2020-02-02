### 4.16. 验证

只要 JSR-303 实现（例如 Hibernate 验证器）位于类路径上，就会自动启用 Bean 验证 1.1 支持的方法验证功能。这样就可以在 bean 方法的参数和/或返回值上使用 `javax.validation` 约束对它们进行注解。具有此类注解方法的目标类需要在类型级别使用 `@Validated` 注解进行修饰，以便在其方法中搜索内联约束注解。

例如，以下服务触发第一个参数的验证，确保其大小在 8 到 10 之间：

```java
@Service
@Validated
public class MyBean {

    public Archive findByCodeAndAuthor(@Size(min = 8, max = 10) String code,
            Author author) {
        ...
    }

}
```