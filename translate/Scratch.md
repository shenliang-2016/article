### 4.3.3 声明式事务划分

我们推荐你使用 Spring 的声明式事务支持，它允许你使用 AOP 事务拦截器替换 Java 代码中的显式的事务划分 API 调用。你可以在 Spring 容器中使用 Java 注解或者 XML 配置这种事务拦截器。这种声明式事务能力允许你保持业务服务独立于重复性的事务划分代码，从而集中精力处理业务逻辑，那才是你的应用的真正价值所在。

> 在你继续之前，我们强烈建议你阅读 [声明式事务管理](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative) 。

你可以使用 `@Transactional` 注解修饰你的服务层，指示 Spring 容器发现这些注解并为这些注解修饰的方法提哦功能事务性语义。下面的例子展示了具体做法：

```java
public class ProductServiceImpl implements ProductService {

    private ProductDao productDao;

    public void setProductDao(ProductDao productDao) {
        this.productDao = productDao;
    }

    @Transactional
    public void increasePriceOfAllProductsInCategory(final String category) {
        List productsToChange = this.productDao.loadProductsByCategory(category);
        // ...
    }

    @Transactional(readOnly = true)
    public List<Product> findAllProducts() {
        return this.productDao.findAllProducts();
    }

}
```

在容器内，你需要配置 `PlatformTransactionManager` 实现（作为一个 bean ）以及一个 `<tx:annnotation-driven/>` 实体， 并在运行时选择 `@Transactional` 处理。下面的例子展示了具体做法：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/tx
        https://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- SessionFactory, DataSource, etc. omitted -->

    <bean id="transactionManager"
            class="org.springframework.orm.hibernate5.HibernateTransactionManager">
        <property name="sessionFactory" ref="sessionFactory"/>
    </bean>

    <tx:annotation-driven/>

    <bean id="myProductService" class="product.SimpleProductService">
        <property name="productDao" ref="myProductDao"/>
    </bean>

</beans>
```

### 4.3.4 编程式事务划分

您可以在应用程序的更高级别中划分事务，在跨越任意数量的操作的较低级别数据访问服务之上。对周围业务服务的实施也没有限制。它只需要一个 Spring `PlatformTransactionManager`。同样，后者可以来自任何地方，但最好通过 `setTransactionManager(..)` 方法作为 bean 的引用。同样，应该通过 `setProductDao(..)` 方法设置 `productDAO`。以下几对代码片段展示了 Spring 应用程序上下文中的事务管理器和业务服务定义，以及业务方法实现的示例：

```xml
<beans>

    <bean id="myTxManager" class="org.springframework.orm.hibernate5.HibernateTransactionManager">
        <property name="sessionFactory" ref="mySessionFactory"/>
    </bean>

    <bean id="myProductService" class="product.ProductServiceImpl">
        <property name="transactionManager" ref="myTxManager"/>
        <property name="productDao" ref="myProductDao"/>
    </bean>

</beans>
```

````java
public class ProductServiceImpl implements ProductService {

    private TransactionTemplate transactionTemplate;
    private ProductDao productDao;

    public void setTransactionManager(PlatformTransactionManager transactionManager) {
        this.transactionTemplate = new TransactionTemplate(transactionManager);
    }

    public void setProductDao(ProductDao productDao) {
        this.productDao = productDao;
    }

    public void increasePriceOfAllProductsInCategory(final String category) {
        this.transactionTemplate.execute(new TransactionCallbackWithoutResult() {
            public void doInTransactionWithoutResult(TransactionStatus status) {
                List productsToChange = this.productDao.loadProductsByCategory(category);
                // do the price increase...
            }
        });
    }
}
````

Spring 的 `TransactionInterceptor` 允许将任何已检查的应用程序异常从回调代码中抛出，而 `TransactionTemplate` 则限于回调中的未检查异常。如果未检查的应用程序异常或应用程序将事务标记为仅回滚（通过设置 `TransactionStatus`），则 `TransactionTemplate` 会触发回滚。默认情况下， `TransactionInterceptor` 的行为方式相同，但允许每种方法的可配置的回滚策略。

