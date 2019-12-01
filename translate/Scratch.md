## 4.3 Hibernate

我们从在 Spring 环境中介绍 [Hibernate 5](https://hibernate.org/) 开始，使用它来演示 Spring 集成 OR 映射器所采用的方法。本节详细讨论了许多问题，并展示了 DAO 实现和事务划分的不同变体。这些模式中的大多数都可以直接转换为所有其他受支持的 ORM 工具。然后，本章后面的部分将介绍其他 ORM 技术，并展示一些简短的示例。

> 从 Spring Framework 5.0 开始，Spring 需要 Hibernate ORM 4.3 或更高版本才能提供 JPA 支持，甚至需要 Hibernate ORM 5.0+ 才能针对本机 Hibernate Session API 进行编程。请注意，Hibernate 团队不再维护 5.1 之前的任何版本，并且可能很快会专注于 5.3+。

### 4.3.1 Spring 容器中的 `SessionFactory` 配置

为了避免将应用程序对象与硬编码的资源查找逻辑绑定在一起，可以在 Spring 容器中将资源（例如 JDBC `DataSource` 或 Hibernate `SessionFactory`）定义为 bean。需要访问资源的应用程序对象通过 bean 引用接收对此类预定义实例的引用，如 [下一节](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#orm-hibernate-straight) 所述。

以下 XML 应用程序上下文定义片段展示了如何在其之上设置 JDBC `DataSource` 和 Hibernate `SessionFactory`：

```xml
<beans>

    <bean id="myDataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
        <property name="driverClassName" value="org.hsqldb.jdbcDriver"/>
        <property name="url" value="jdbc:hsqldb:hsql://localhost:9001"/>
        <property name="username" value="sa"/>
        <property name="password" value=""/>
    </bean>

    <bean id="mySessionFactory" class="org.springframework.orm.hibernate5.LocalSessionFactoryBean">
        <property name="dataSource" ref="myDataSource"/>
        <property name="mappingResources">
            <list>
                <value>product.hbm.xml</value>
            </list>
        </property>
        <property name="hibernateProperties">
            <value>
                hibernate.dialect=org.hibernate.dialect.HSQLDialect
            </value>
        </property>
    </bean>

</beans>
```

从本地 Jakarta Commons DBCP `BasicDataSource` 切换到 JNDI 的 `DataSource`（通常由应用服务器管理）仅是配置问题，如以下示例所示：

```xml
<beans>
    <jee:jndi-lookup id="myDataSource" jndi-name="java:comp/env/jdbc/myds"/>
</beans>
```

您还可以使用 Spring 的 `JndiObjectFactoryBean` / `<jee:jndi-lookup>` 获取和暴露它，访问 JNDI 的 SessionFactory。但是，这通常在 EJB 上下文之外并不常见。

> Spring 还提供了 `LocalSessionFactoryBuilder` 变体，与 `@Bean` 风格配置和编程设置无缝集成（不涉及 `FactoryBean`）。
>
> `LocalSessionFactoryBean` 和 `LocalSessionFactoryBuilder` 都支持后台引导，并且 Hibernate 初始化与给定的引导执行器（例如 `SimpleAsyncTaskExecutor`）上的应用程序引导线程并行运行。在 `LocalSessionFactoryBean` 上，可以通过 `bootstrapExecutor` 属性获得。在程序化的 `LocalSessionFactoryBuilder` 上，有一个重载的 `buildSessionFactory` 方法，该方法带有引导执行程序参数。
>
> 从 Spring Framework 5.1 开始，这样的本地 Hibernate 设置还可以在本地 Hibernate 访问之外公开用于标准 JPA 交互的 JPA `EntityManagerFactory`。有关详细信息，请参见 [JPA 的本地 Hibernate 设置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#orm-jpa-hibernate) 。

