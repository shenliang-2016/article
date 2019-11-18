## 2.2 用于配置 DAO 或者 Repository 类的注解

保证你的数据访问对象或者仓库类提供异常转化的最好方法就是使用 `@Repository` 注解。该注解同时允许组件扫描支持发现并配置你的 DAOs 和仓库类，而不需要为它们提供 XML 配置文件入口。下面的例子展示了如何使用 `@Repository` 注解：

```java
@Repository 
public class SomeMovieFinder implements MovieFinder {
    // ...
}
```

任何需要访问持久化资源的 DAO 或者仓库类实现都依赖于所使用的持久化技术。比如，基于 JDBC 的仓库需要访问 JDBC `DataSource`，而基于 JPA 的仓库类需要访问 `EntityManager` 。实现这一点的最简单方式就是使用 `@Autowired`, `@Inject`, `@Resource` 或者 `@PersistenceContext` 注解之一进行资源的依赖注入。下面的例子用于 JPA 仓库类：

```java
@Repository
public class JpaMovieFinder implements MovieFinder {

    @PersistenceContext
    private EntityManager entityManager;

    // ...

}
```

如果你使用经典的 Hibernate APIs，你可以如下注入 `SessionFactory`：

```java
@Repository
public class HibernateMovieFinder implements MovieFinder {

    private SessionFactory sessionFactory;

    @Autowired
    public void setSessionFactory(SessionFactory sessionFactory) {
        this.sessionFactory = sessionFactory;
    }

    // ...

}
```

最后一个例子关于典型的 JDBC 支持。你已经在初始化方法中注入一个 `DataSource` ，然后你使用该 `DataSource` 创建 `JdbcTempalte` 及其他数据访问支持类(比如 `SimpleJdbcCall` )。下面的例子自动装配 `DataSource`：

```java
@Repository
public class JdbcMovieFinder implements MovieFinder {

    private JdbcTemplate jdbcTemplate;

    @Autowired
    public void init(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    // ...

}
```

> 有关如何配置应用程序上下文以利用这些注解的详细信息，请参见每种持久性技术的专门介绍。

