### 1.5.2 使用 `PlatformTransactionManager`

你还可以直接使用 `org.springframework.transaction.PlatformTransactionManager` 管理你的事务。为了这样做，通过 bean 引用传递你使用的 `PlatformTransactionManager` 实现给你的 bean。然后，通过使用 `TransactionDefinition` 和 `TransactionStatus` 对象，你可以初始化事务，回滚，以及提交。下面的例子展示了这个过程：

```java
DefaultTransactionDefinition def = new DefaultTransactionDefinition();
// explicitly setting the transaction name is something that can be done only programmatically
def.setName("SomeTxName");
def.setPropagationBehavior(TransactionDefinition.PROPAGATION_REQUIRED);

TransactionStatus status = txManager.getTransaction(def);
try {
    // execute your business logic here
}
catch (MyException ex) {
    txManager.rollback(status);
    throw ex;
}
txManager.commit(status);
```

