### 4.2.2 异常转换

在 DAO 中使用 Hibernate 或 JPA 时，必须决定如何处理持久性技术的原生异常类。根据技术的不同，DAO 会抛出 `HibernateException` 或 `PersistenceException` 的子类。这些异常都是运行时异常，不必声明或捕获。您可能还必须处理 `IllegalArgumentException` 和 `IllegalStateException`。这意味着调用者只能将一般的异常都视为致命的，除非他们想依赖于持久性技术自己的异常结构。如果不将调用者与实现策略联系在一起，则无法捕获特定原因（例如乐观锁定失败）。这种权衡可能对于基于 ORM 的应用程序或不需要任何特殊异常处理（或两者）都可以接受。但是，Spring 允许通过 `@Repository` 注解透明地进行异常转换。以下示例（一个用于 Java 配置，一个用于 XML 配置）显示了如何执行此操作：

```java
@Repository
public class ProductDaoImpl implements ProductDao {

    // class body here...

}
<beans>

    <!-- Exception translation bean post processor -->
    <bean class="org.springframework.dao.annotation.PersistenceExceptionTranslationPostProcessor"/>

    <bean id="myProductDao" class="product.ProductDaoImpl"/>

</beans>
```

后处理器自动查找所有异常翻译器（`PersistenceExceptionTranslator` 接口的实现），并增强所有标有 `@Repository` 注解的 bean，以便发现的翻译器可以拦截并对抛出的异常应用适当的转换。

总之，您可以基于纯持久性技术的 API 和注解来实现 DAO，同时仍然可以从 Spring 管理的事务，依赖注入和透明异常转换（如果需要）到 Spring 的自定义异常层次结构中受益。

