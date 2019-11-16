### 1.4.7 事务传播

本节描述 Spring 中的一些事务传播语义。注意，本节并不是真正地介绍事务传播，它仅仅是一些语义细节，而不关注 Spring 中实际的事务传播。

在 Spring 管理的事务中，注意区别逻辑事务和物理事务，以及事务传播设定应用于两者的不同。

##### 理解 `PROPAGATION_REQUIRED`

![tx prop required](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/images/tx_prop_required.png)

`PROPAGATION_REQUIRED` 强制执行一个物理事务，如果目前不存在事务，则是当前作用域内的局部事务，要么作为一个更大的作用域下的现有的外部事务的成员。这是通常分配给同一线程的调用栈（例如，委派给几种存储库方法的服务门面，所有基础资源都必须参与服务级事务）中的优良默认设置。

> 默认地，一个成员事务加入外部作用域的特性，静默地忽略局部的隔离级别、超时时间、或者只读标记(如果存在)。考虑切换事务管理器上的 `validateExisitingTransactions` 标记为 `true` ，如果你希望当成为不同隔离级别的现存事务的成员时隔离级别声明被拒绝。这种非宽容模式还拒绝只读不匹配项（即，内部读写事务试图参与只读外部作用域）。

当传播设定为 `PROPAGATION_REQUIRED`，为该设定应用到的每个方法创建逻辑事务作用域。每个这种逻辑事务作用域能够独立决定只回滚状态，因为外部事务作用域和内部事务作用域是逻辑独立的。在标准 `PROPAGATION_REQUIRED` 行为的情况下，所有这些作用域都被影射到相同的物理事务。因此一个内部事务作用域的只回滚标记会影响外部事务的实际提交。

不过，在内部事务作用域设定只回滚标记情况下，外部事务自身并未决定回滚，因此回滚(由内部事务作用域触发的)是不希望发生的。一个相应的 `UnexpectedRollbackException` 在这个时候被抛出。这是期望的行为，因而事务的调用着在事务没有正确提交情况下永远不会被误导而假定事务被正确提交。因此，如果一个内部事务(外部调用者不敏感)静默地将事务标记为只回滚，外部调用着仍然调用提交。外部调用着需要接受一个 `UnexpectedRollbackException` 来清楚地表示实际上发生了回滚。

##### 理解 `PROPAGATION_REQUIRES_NEW`

![tx prop requires new](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/images/tx_prop_requires_new.png)

`PROPAGATION_REQUIRES_NEW`，相对于 `PROPAGATION_REQUIRED`，永远为每个不同的事务作用域使用独立的物理事务，永远不参与外部作用的现有事务。这种编排情况下，基础资源事务时不同的，因此，可以独立地提交或者回滚。外部事务不会被内部事务的回滚状态或者在内部事务完成时立即释放锁影响。这样的独立内部事务也可以声明它自己的隔离级别、超时时间、以及制度设定等，而不集成外部事务的特性。

##### 理解 `PROPAGATION_NESTED`

`PROPAGATION_NESTED` 使用一个物理事务，拥有多个可以回滚到的保存点。这种部分回滚允许一个内部事务作用域为它自己的作用域触发回滚，而外部作用域可以继续执行它的物理事务，而不在乎某些操作已经回滚。这种设定典型地影射到 JDBC 保存点，因此只可以用于 JDBC 资源事务。参考 Spring 的 [`DataSourceTransactionManager`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jdbc/datasource/DataSourceTransactionManager.html)。

