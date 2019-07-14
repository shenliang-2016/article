##### XML Bean 定义配置

XML中的对应物是`<beans>`元素的`profile`属性。我们之前的示例配置可以在两个XML文件中重写，如下所示：

```xml
<beans profile="development"
    xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:jdbc="http://www.springframework.org/schema/jdbc"
    xsi:schemaLocation="...">

    <jdbc:embedded-database id="dataSource">
        <jdbc:script location="classpath:com/bank/config/sql/schema.sql"/>
        <jdbc:script location="classpath:com/bank/config/sql/test-data.sql"/>
    </jdbc:embedded-database>
</beans>
<beans profile="production"
    xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:jee="http://www.springframework.org/schema/jee"
    xsi:schemaLocation="...">

    <jee:jndi-lookup id="dataSource" jndi-name="java:comp/env/jdbc/datasource"/>
</beans>
```

也可以避免在同一文件中拆分和嵌套`<beans/>`元素，如下例所示：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:jdbc="http://www.springframework.org/schema/jdbc"
    xmlns:jee="http://www.springframework.org/schema/jee"
    xsi:schemaLocation="...">

    <!-- other bean definitions -->

    <beans profile="development">
        <jdbc:embedded-database id="dataSource">
            <jdbc:script location="classpath:com/bank/config/sql/schema.sql"/>
            <jdbc:script location="classpath:com/bank/config/sql/test-data.sql"/>
        </jdbc:embedded-database>
    </beans>

    <beans profile="production">
        <jee:jndi-lookup id="dataSource" jndi-name="java:comp/env/jdbc/datasource"/>
    </beans>
</beans>
```

`spring-bean.xsd`已被约束为仅允许这些元素作为文件中的最后一个元素。这应该有助于提供灵活性，而不会在XML文件中引起混乱。

> XML副本不支持前面描述的配置文件表达式。但是，可以通过使用`!`运算符来否定配置文件。也可以通过嵌套配置文件来应用逻辑“与”，如以下示例所示：
>
> ```xml
> <beans xmlns="http://www.springframework.org/schema/beans"
>     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>     xmlns:jdbc="http://www.springframework.org/schema/jdbc"
>     xmlns:jee="http://www.springframework.org/schema/jee"
>     xsi:schemaLocation="...">
> 
>     <!-- other bean definitions -->
> 
>     <beans profile="production">
>         <beans profile="us-east">
>             <jee:jndi-lookup id="dataSource" jndi-name="java:comp/env/jdbc/datasource"/>
>         </beans>
>     </beans>
> </beans>
> ```
>
> 在前面的示例中，如果`production`和`us-east`配置文件都处于活动状态，则会暴露`dataSource` bean。

##### 激活一个配置

现在我们已经更新了配置，我们仍然需要指示Spring哪个配置文件处于活动状态。如果我们现在开始我们的示例应用程序，我们会看到抛出一个`NoSuchBeanDefinitionException`，因为容器找不到名为`dataSource`的Spring bean。

激活配置文件可以通过多种方式完成，但最直接的方法是以编程方式对可通过`ApplicationContext`提供的`Environment` API进行操作。以下示例显示了如何执行此操作：

```java
AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext();
ctx.getEnvironment().setActiveProfiles("development");
ctx.register(SomeConfig.class, StandaloneDataConfig.class, JndiDataConfig.class);
ctx.refresh();
```

此外，您还可以通过`spring.profiles.active`属性声明性地激活配置文件，该属性可以通过系统环境变量，JVM系统属性，`web.xml`中的servlet上下文参数指定，甚至可以作为JNDI中的条目指定（参见 [`PropertySource` Abstraction](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-property-source-abstraction) ）。在集成测试中，可以使用`spring-test`模块中的`@ActiveProfiles`注释声明活动配置文件（请参阅 [context configuration with environment profiles](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-env-profiles) ）。

请注意，配置文件不是“要么 - 要么”命题。您可以一次激活多个配置文件。在编程方式中，您可以为`setActiveProfiles()`方法提供多个配置文件名称，该方法接受`String...`可变参数。以下示例激活多个配置文件：

```java
ctx.getEnvironment().setActiveProfiles("profile1", "profile2");
```

声明性地，`spring.profiles.active`可以接受以逗号分隔的配置文件名列表，如以下示例所示：

```
-Dspring.profiles.active="profile1,profile2"
```

##### 默认配置

默认配置文件表示默认启用的配置文件。 请考虑以下示例：

```java
@Configuration
@Profile("default")
public class DefaultDataConfig {

    @Bean
    public DataSource dataSource() {
        return new EmbeddedDatabaseBuilder()
            .setType(EmbeddedDatabaseType.HSQL)
            .addScript("classpath:com/bank/config/sql/schema.sql")
            .build();
    }
}
```

如果没有激活配置文件，则创建`dataSource`。您可以将此视为一种为一个或多个bean提供默认定义的方法。如果启用了任何配置文件，则默认配置文件不适用。

您可以使用`Environment`上的`setDefaultProfiles()`或者声明性地使用`spring.profiles.default`属性来更改默认配置文件的名称。

