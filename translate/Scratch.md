### 4.3.2 Implementing DAOs Based on the Plain Hibernate API

Hibernate 具有一种称为上下文会话的功能，其中 Hibernate 本身在每个事务中管理一个当前的 `Session` 。这大致相当于 Spring 在每个事务中同步一个 Hibernate `Session`。基于简单的 Hibernate API，相应的 DAO 实现类似于以下示例：

```java
public class ProductDaoImpl implements ProductDao {

    private SessionFactory sessionFactory;

    public void setSessionFactory(SessionFactory sessionFactory) {
        this.sessionFactory = sessionFactory;
    }

    public Collection loadProductsByCategory(String category) {
        return this.sessionFactory.getCurrentSession()
                .createQuery("from test.Product product where product.category=?")
                .setParameter(0, category)
                .list();
    }
}
```

这种样式类似于 Hibernate 参考文档和示例，除了在实例变量中保留 `SessionFactory` 之外。我们强烈建议您在 Hibernate 的 `CaveatEmptor` 示例应用程序中的老式 `static` `HibernateUtil` 类上使用基于实例的设置。（通常，除非绝对必要，否则不要在 `static` 变量中保留任何资源。）

前面的 DAO 示例遵循依赖项注入模式。它可以很好地适合 Spring IoC 容器，就像针对 Spring 的 `HibernateTemplate` 进行编码一样。您还可以在纯 Java 中设置这种 DAO（例如，在单元测试中）。为此，将其实例化并使用所需的工厂引用调用 `setSessionFactory(..)`。作为 Spring bean 的定义，DAO 类似于以下内容：

```xml
<beans>

    <bean id="myProductDao" class="product.ProductDaoImpl">
        <property name="sessionFactory" ref="mySessionFactory"/>
    </bean>

</beans>
```

这种 DAO 样式的主要优点是它仅依赖于 Hibernate API。不需要导入任何 Spring 类。从非侵入性的角度来看，这很有吸引力，并且对于 Hibernate 开发人员而言可能更自然。

但是，DAO 会抛出普通的 `HibernateException`（未经检查，因此不必声明或捕获），这意味着调用方只能将异常视为一般致命的消息 - 除非他们希望依赖于 Hibernate 自己的异常层次结构。如果不将调用者与实现策略联系在一起，则无法捕获特定原因（例如乐观锁定失败）的异常。这种权衡对于强依赖 Hibernate 的，或者不需要任何特殊异常处理，或两个特性兼有应用程序都可以接受。

幸运的是，Spring 的 `LocalSessionFactoryBean` 为任何 Spring 事务策略支持 Hibernate 的 `SessionFactory.getCurrentSession()` 方法，甚至可以使用 `HibernateTransactionManager` 返回当前的 Spring 管理的事务性 `Session`。该方法的标准行为仍然是返回与正在进行的 JTA 事务相关联的当前 `Session`（如果有）。无论您使用 Spring 的 `JtaTransactionManager`，EJB 容器管理的事务（CMT）还是 JTA，此行为均适用。

总之，您可以基于普通的 Hibernate API 实现 DAO，同时仍然能够参与 Spring 管理的事务。

