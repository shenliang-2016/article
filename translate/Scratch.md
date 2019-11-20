##### 查询 (`SELECT`)

下面的查询获取一个关系中的行数：

```java
int rowCount = this.jdbcTemplate.queryForObject("select count(*) from t_actor", Integer.class);
```

下面的查询使用一个绑定变量：

```java
int countOfActorsNamedJoe = this.jdbcTemplate.queryForObject(
        "select count(*) from t_actor where first_name = ?", Integer.class, "Joe");
```

下面的查询寻找一个 `String` ：

```java
String lastName = this.jdbcTemplate.queryForObject(
        "select last_name from t_actor where id = ?",
        new Object[]{1212L}, String.class);
```

下面的查询查找并填充单独一个域对象：

```java
Actor actor = this.jdbcTemplate.queryForObject(
        "select first_name, last_name from t_actor where id = ?",
        new Object[]{1212L},
        new RowMapper<Actor>() {
            public Actor mapRow(ResultSet rs, int rowNum) throws SQLException {
                Actor actor = new Actor();
                actor.setFirstName(rs.getString("first_name"));
                actor.setLastName(rs.getString("last_name"));
                return actor;
            }
        });
```

下面的查询查找并填充一系列域对象：

```java
List<Actor> actors = this.jdbcTemplate.query(
        "select first_name, last_name from t_actor",
        new RowMapper<Actor>() {
            public Actor mapRow(ResultSet rs, int rowNum) throws SQLException {
                Actor actor = new Actor();
                actor.setFirstName(rs.getString("first_name"));
                actor.setLastName(rs.getString("last_name"));
                return actor;
            }
        });
```

如果上面的两个代码片段出现在同一个应用中，则可以删除两个 `RowMapper` 中的匿名内部类，并抽取它们到一个单独的类(典型地，一个 `static` 嵌套类) 而可以被所有需要的 DAO 方法引用。如下面的写法：

```java
public List<Actor> findAllActors() {
    return this.jdbcTemplate.query( "select first_name, last_name from t_actor", new ActorMapper());
}

private static final class ActorMapper implements RowMapper<Actor> {

    public Actor mapRow(ResultSet rs, int rowNum) throws SQLException {
        Actor actor = new Actor();
        actor.setFirstName(rs.getString("first_name"));
        actor.setLastName(rs.getString("last_name"));
        return actor;
    }
}
```

##### 更新 (`INSERT`, `UPDATE`, and `DELETE`) 

你可以使用 `update(..)` 方法来执行插入、更新、以及删除操作。参数值通常以变量参数或者对象数组的形式提供。

下面的例子插入一个新的数据实体：

```java
this.jdbcTemplate.update(
        "insert into t_actor (first_name, last_name) values (?, ?)",
        "Leonor", "Watling");
```

下面的例子更新一个已经存在的数据实体：

```java
this.jdbcTemplate.update(
        "update t_actor set last_name = ? where id = ?",
        "Banjo", 5276L);
```

下面的例子删除一个数据实体：

```java
this.jdbcTemplate.update(
        "delete from actor where id = ?",
        Long.valueOf(actorId));
```

##### 其他 `JdbcTemplate` 操作

你可以使用 `execute(..)` 方法执行任意 SQL。因此，该方法通常被用于 DDL 语句。它有各种增强变体，如携带回调接口，绑定变量数组等等。下面的例子创建一张表：

```java
this.jdbcTemplate.execute("create table mytable (id integer, name varchar(100))");
```

下面的例子调用一个存储过程：

```java
this.jdbcTemplate.update(
        "call SUPPORT.REFRESH_ACTORS_SUMMARY(?)",
        Long.valueOf(unionId));
```

更复杂的存储过程支持参考 [covered later](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-StoredProcedure) 。

##### `JdbcTemplate` 最佳实践

一旦被配置，`JdbcTemplate` 类实例就是线程安全的。这一点很重要，因为这意味着你可以仅配置一个 `JdbcTemplate` 实例然后安全地将其作为共享引用注入多个 DAOs 或者仓库类。`JdbcTemplate` 是有状态的，因为它维护了一个 `DataSource` 引用，不过这里的状态并不是传统意义上的状态。

常见的 `JdbcTemplate` 类（以及配合的 [`NamedParameterJdbcTemplate`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-NamedParameterJdbcTemplate) 类）的使用方法是在你的 Spring 配置文件中配置一个 `DataSource` 然后将该共享 `DataSource` bean 注入你的 DAO 类中。`JdbcTemplate` 在 `DataSource` 的设定器方法中被创建。这产生类似于以下内容的DAO：

```java
public class JdbcCorporateEventDao implements CorporateEventDao {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    // JDBC-backed implementations of the methods on the CorporateEventDao follow...
}
```

下面的例子展示对应的 XML 配置：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <bean id="corporateEventDao" class="com.example.JdbcCorporateEventDao">
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
        <property name="driverClassName" value="${jdbc.driverClassName}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

    <context:property-placeholder location="jdbc.properties"/>

</beans>
```

另一种显式配置的方法是使用组件扫描和依赖注入的注解支持。这种情况下，你可以使用 `@Repository` 注解修饰你的类(将该类标记为组件扫描的候选者)，并使用 `@Autowired` 注解修饰 `DataSource` 的设定器方法。下面的例子展示了这样的做法：

```java
@Repository 
public class JdbcCorporateEventDao implements CorporateEventDao {

    private JdbcTemplate jdbcTemplate;

    @Autowired 
    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource); 
    }

    // JDBC-backed implementations of the methods on the CorporateEventDao follow...
}
```

下面的例子展示了对应的 XML 配置：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <!-- Scans within the base package of the application for @Component classes to configure as beans -->
    <context:component-scan base-package="org.springframework.docs.test" />

    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
        <property name="driverClassName" value="${jdbc.driverClassName}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

    <context:property-placeholder location="jdbc.properties"/>

</beans>
```

如果你使用 Spring 的 `JdbcDaoSupport` 类，你的各种基于 JDBC 的 DAO 类都从它扩展而来，你的子类从 `JdbcDaoSupport` 类继承了 `setDataSource(..)` 方法。你可以选择是否继承该方法。 `JdbcDaoSupport` 类仅仅为方便而提供。

无论你选择使用上述何种模板初始化方式，你应该都不需要在每次执行 SQL 时创建一个新的 `JdbcTemplate` 类的实例。一旦配置，`JdbcTemplate` 实例就是线程安全的。如果你的应用访问多个数据库，你可能希望拥有多个 `JdbcTemplate` 实例，这就需要多个 `DataSource` ，进一步的，需要多个不同配置的 `JdbcTemplate` 实例。

