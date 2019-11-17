## 1.7 事务绑定事件

在 Spring 4.2 中，事件监听器可以被绑定到事务的某个阶段。典型的例子是处理事务彻底完成时的事件。这样做使得事件的使用更加灵活，当当前事务的结果确实会影响到监听器时。

你可以使用 `@EventListener` 注解注册一个常规的事件监听器。如果你需要将它绑定到事务，使用 `@TransactionalEventListener` 。当你这么做时，该监听器就会被默认绑定到事务的提交阶段。

下面的例子展示了这个概念。假定某个组建发布一个订单创建事件，我们希望定义一个监听器，仅仅处理该事件一次，一旦该事件发布则表示订单创建事务已经提交成功。下面的例子展示了如何设置这样的事件监听器：

```java
@Component
public class MyComponent {

    @TransactionalEventListener
    public void handleOrderCreatedEvent(CreationEvent<Order> creationEvent) {
        ...
    }
}
```

`@TransactionalEventListener` 注解暴露了一个 `phase` 属性，允许你自定义该监听器应该绑定到事务的哪个阶段。有效的阶段有 `BEFORE_COMMIT`，`AFTER_COMMIT`(默认的)，`AFTER_ROLLBACK`，以及 `AFTER_COMPLETION`（笼统表示事务完成，提交或者回滚）。

如果没有事务在运行，监听器就完全不会被调用，因为我们不能遵循必需的语义。但是，你仍然可以通过将注解的 `fallbackExecution` 属性设定为 `true` 来覆盖该行为。

