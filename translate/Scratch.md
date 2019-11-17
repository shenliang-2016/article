## 1.5. 编程式事务管理

Spring 框架提供了两种手段进行编程式事务管理，通过使用：

* `TransactionTemplate`
* 直接使用 `PlatformTransactionManager` 实现

Spring 团队通常推荐使用 `TransactionTemplate` 进行编程式事务管理。第二种方法类似于使用 JTA `UserTransaction` API，尽管异常处理有些麻烦。

### 1.5.1 使用 `TransactionTemplate`

`TransactionTemplate` 采用了类似于其它 Spring 模板的使用方式，比如 `JdbcTemplate`。它使用一个回调方法 (为了将应用代码从无聊的锁定和释放事务资源的工作中解脱出来) 使得代码成为意图驱动的，你的代码可以单纯地聚焦于处理业务需求。

> 如下面例子所示，使用 `TransactionTemplate` 绝对会将你绑定到 Spring 的事务基础设施和 APIs。在开发中是否使用编程式事务管理取决于你的需求，完全由你自己决定。

必须在事务上下文中执行的业务代码以及显式使用 `TransactionTemplate` 的代码组成了下一个例子。作为应用开发者，你可以编写 `TransactionCallback` 实现 (通常表现为匿名内部类) ，其中包含你需要在事务上下文中执行的代码。然后你可减奖你的自定义的 `TransactionCallback` 实例传入 `TransactionTemplate` 暴露出来的 `execute(..)` 方法。下面的例子展示了这个过程：

```java
public class SimpleService implements Service {

    // single TransactionTemplate shared amongst all methods in this instance
    private final TransactionTemplate transactionTemplate;

    // use constructor-injection to supply the PlatformTransactionManager
    public SimpleService(PlatformTransactionManager transactionManager) {
        this.transactionTemplate = new TransactionTemplate(transactionManager);
    }

    public Object someServiceMethod() {
        return transactionTemplate.execute(new TransactionCallback() {
            // the code in this method executes in a transactional context
            public Object doInTransaction(TransactionStatus status) {
                updateOperation1();
                return resultOfUpdateOperation2();
            }
        });
    }
}
```

如果不存在返回值，你可以使用便捷的 `TransactionCallbackWithoutResult` 类：

```java
transactionTemplate.execute(new TransactionCallbackWithoutResult() {
    protected void doInTransactionWithoutResult(TransactionStatus status) {
        updateOperation1();
        updateOperation2();
    }
});
```

回调中的代码能够回滚事务，通过调用给定的 `TransactionStatus` 对象上的 `setRollbackOnly()` 方法，如下：

```java
transactionTemplate.execute(new TransactionCallbackWithoutResult() {

    protected void doInTransactionWithoutResult(TransactionStatus status) {
        try {
            updateOperation1();
            updateOperation2();
        } catch (SomeBusinessException ex) {
            status.setRollbackOnly();
        }
    }
});
```

##### 指定事务设定

你可以在 `TransactionTemplate` 上指定事务设定 (比如传播模式，隔离级别，超时时间等等) ，通过编程方式或者配置文件。默认地，`TransactionTemplate` 实例拥有 [default transactional settings](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative-txadvice-settings) 。下面的例子展示了编程方式自定义特定 `TransactionTemplate` 的事务设定：

```java
public class SimpleService implements Service {

    private final TransactionTemplate transactionTemplate;

    public SimpleService(PlatformTransactionManager transactionManager) {
        this.transactionTemplate = new TransactionTemplate(transactionManager);

        // the transaction settings can be set here explicitly if so desired
        this.transactionTemplate.setIsolationLevel(TransactionDefinition.ISOLATION_READ_UNCOMMITTED);
        this.transactionTemplate.setTimeout(30); // 30 seconds
        // and so forth...
    }
}
```

下面的例子展示了通过使用 Spring XML 配置文件使用一些自定义事务设定定义一个 `TransactionTemplate` ：

```xml
<bean id="sharedTransactionTemplate"
        class="org.springframework.transaction.support.TransactionTemplate">
    <property name="isolationLevelName" value="ISOLATION_READ_UNCOMMITTED"/>
    <property name="timeout" value="30"/>
</bean>"
```

然后你就可以将 `sharedTransactionTemplate` 注入到任意多个需要它的服务类中。

最后，`TransactionTemplate` 类实例时线程安全的，该实例中没有维护任何会话状态。不过，`TransactionTemplate` 实例维护了配置状态。因此，当多个类可能共享一个 `TransactionTemplate` 实例时，如果一个类需要使用包含不同设定的 `TransactionTemplate` (比如，不同的隔离级别)，你需要创建两个不同的 `TransactionTemplate` 实例。

