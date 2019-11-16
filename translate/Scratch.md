##### `@Transactional` 的多个事务管理器

大多数的 Spring 应用只需要一个事务管理器，不过有时候你可能会在一个应用中需要多个相互独立的事务管理器。你可使用 `@Transactional` 的 `value` 属性可选地指定使用的 `PlatformTransactionManager` 的标示符。该标示符可以是事务管理器 bean 的名称或者限定符值。比如，使用限定符记号，你可以将下面的代码和应用上下文中声明的事务管理器 bean 结合起来：

```java
public class TransactionalService {

    @Transactional("order")
    public void setSomething(String name) { ... }

    @Transactional("account")
    public void doSomething() { ... }
}
```

下面是 bean 声明：

```xml
<tx:annotation-driven/>

    <bean id="transactionManager1" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        ...
        <qualifier value="order"/>
    </bean>

    <bean id="transactionManager2" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        ...
        <qualifier value="account"/>
    </bean>
```

这种情况下，`TransactionalService` 中的两个方法运行在独立的事务管理器下，通过 `order` 和 `account` 限定符区别。仍然使用默认的 `<tx:annotation-driven>` 目标 bean 名称，`TransactionManager` 。除非找到特殊限定的 `PlatformTransactionManager` bean。

##### 自定义快捷注解

如果你发现你在多个不同的方法上重复使用相同的 `@Transactional` 属性，[Spring’s meta-annotation support](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-meta-annotations) 允许你为特定的使用场景定义自定义的快捷注解。比如，考虑下面的注解定义：

```java
@Target({ElementType.METHOD, ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Transactional("order")
public @interface OrderTx {
}

@Target({ElementType.METHOD, ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Transactional("account")
public @interface AccountTx {
}
```

上面的注解允许我们如下重写上一节中的例子：

```java
public class TransactionalService {

    @OrderTx
    public void setSomething(String name) { ... }

    @AccountTx
    public void doSomething() { ... }
}
```

在上面的例子中，我们使用该语法定义事务管理器限定符，不过，我们还可以包含传播行为，回滚规则，超时时间，以及其他特性。

