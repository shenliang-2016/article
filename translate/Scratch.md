### 4.4.2 基于 JPA: `EntityManagerFactory` 和 `EntityManager` 实现 DAOs

> 尽管 `EntityManagerFactory` 实例是线程安全的，`EntityManager` 实例却不是。注入的 JPA `EntityManager` 的行为类似于从应用服务器的 JNDI 环境获取的 `EntityManager` 实例，如 JPA 规范中所定义。它将所有调用委托给当前事务性的 `EntityManager` ，如果存在。否则，它降级为每个操作创建一个新的 `EntityManager` 实例，实际上使它的使用成为线程安全的。

直接面向原生 JPA 编写代码而不是用任何 Spring 依赖是可能的，通过使用注入的 `EntityManagerFactory` 或者 `EntityManager` 。Spring 可以理解字段上和方法上的 `@PersistenceUnit` 和 `@PersistenceContext` 注解，如果启用了 `PersistenceAnnotationBeanPostProcessor` 。下面的例子展示了一个原生 JPA DAO 实现，使用了 `@PersistenceUnit` 注解：

```java
public class ProductDaoImpl implements ProductDao {

    private EntityManagerFactory emf;

    @PersistenceUnit
    public void setEntityManagerFactory(EntityManagerFactory emf) {
        this.emf = emf;
    }

    public Collection loadProductsByCategory(String category) {
        try (EntityManager em = this.emf.createEntityManager()) {
            Query query = em.createQuery("from Product as p where p.category = ?1");
            query.setParameter(1, category);
            return query.getResultList();
        }
    }
}
```

前面的 DAO 不依赖于 Spring，并且仍然非常适合 Spring 应用程序上下文。此外，DAO 利用注解的优势，要求注入默认的 `EntityManagerFactory`，如以下示例 Bean 定义所示：

```xml
<beans>

    <!-- bean post-processor for JPA annotations -->
    <bean class="org.springframework.orm.jpa.support.PersistenceAnnotationBeanPostProcessor"/>

    <bean id="myProductDao" class="product.ProductDaoImpl"/>

</beans>
```

作为显式定义 `PersistenceAnnotationBeanPostProcessor` 的替代方法，请考虑在应用程序上下文配置中使用 Spring `context:annotation-config` XML 元素。这样做会自动注册所有 Spring 标准后处理器以进行基于注释的配置，包括 `CommonAnnotationBeanPostProcessor` 等。

考虑下面的例子：

```xml
<beans>

    <!-- post-processors for all standard config annotations -->
    <context:annotation-config/>

    <bean id="myProductDao" class="product.ProductDaoImpl"/>

</beans>
```

这种 DAO 的主要问题在于，它总是在工厂中始终创建一个新的 `EntityManager`。您可以通过请求注入事务型 `EntityManager`（也称为“共享的EntityManager”，因为它是实际事务型 `EntityManager` 的共享的线程安全代理）来代替工厂注入，从而避免了这种情况。以下示例显示了如何执行此操作：

```java
public class ProductDaoImpl implements ProductDao {

    @PersistenceContext
    private EntityManager em;

    public Collection loadProductsByCategory(String category) {
        Query query = em.createQuery("from Product as p where p.category = :category");
        query.setParameter("category", category);
        return query.getResultList();
    }
}
```

`@PersistenceContext` 注解具有一个称为 `type` 的可选属性，默认为 `PersistenceContextType.TRANSACTION`。您可以使用此默认值来接收共享的 `EntityManager` 代理。替代方法 `PersistenceContextType.EXTENDED` 是完全不同的事情。这导致了所谓的扩展的 `EntityManager`，它不是线程安全的，因此不能在并发访问的组件（例如 Spring 管理的单例 bean）中使用。扩展的 `EntityManager` 实例仅应用于有状态的组件中，例如，驻留在会话中的状态组件，其 `EntityManager` 的生命周期不依赖于当前事务，而是完全取决于应用程序。

> 方法层面和字段层面的注入
>
> 您可以在类中的字段或方法上应用指示依赖项注入的注解（例如，`@PersistenceUnit` 和 `@PersistenceContext`），也就是所谓的“方法级注入”和“字段级注入”。字段级注解简洁明了，易于使用，而方法级注解则允许对注入的依赖项进行进一步处理。在这两种情况下，成员的可见性（public，protected 或 private）都无关紧要。
>
> 类层面的注解呢？
>
> 在 Java EE 平台上，它们只是用于依赖声明，并不用于资源注入。

注入的 `EntityManager` 是 Spring 管理的（感知到正在进行的事务）。即使新的 DAO 实现使用方法级别的 `EntityManager` 而非 `EntityManagerFactory` 注入，由于注解的使用，应用程序上下文 XML 也不需要更改。

这种 DAO 样式的主要优点是它仅取决于 Java Persistence API。不需要导入任何 Spring 类。此外，由于可以理解 JPA 注解，因此 Spring 容器会自动应用注入。从非侵入性的角度来看，这是有吸引力的，并且对于 JPA 开发人员而言，感觉会更自然。

