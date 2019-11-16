> 处理 `@Transactional` 注解的默认增强模式是 `proxy`，它只允许拦截通过代理的方法调用。同一个类中的本地调用不能通过这种方式被拦截。需要更先进的拦截模式，考虑切换到 `aspectj` 模式并结合使用编译期或者加载期编织。

> `proxy-target-class` 属性控制为 `@Transactional` 注解修饰的类创建何种类型的事务性代理。如果 `proxy-target-class` 数据被设置为 `true`，则创建基于类的代理。如果 `proxy-target-class` 是 `false` 或者该属性被省略，则创建标准的 JDK 基于接口的代理。(参考 [[aop-proxying\]](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#aop-proxying) 获取跟多不同代理类型的讨论)

> `@EnableTransactionManagement` 和 `<tx:annotation-driven/>` 仅仅在它们自身被定义的应用上下文中寻找 beans 上的 `@Transactional` 。这就意味着，如果你为一个 `DispatchServlet` 在 `WebApplicationContext` 中配置了注解驱动，它只会检查你的 controllers 中的 `@Transactional` beans ，而不管你的 services 类。参考 [MVC](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web.html#mvc-servlet) 获取更多细节。

在评估方法的事务设置时，最派生（最细粒度）的位置优先。在下面的示例中，`DefaultFooService` 类在类级别使用只读事务的设置进行注解，但是同一类中 `updateFoo(Foo)` 方法上的 `@Transactional` 注解优先于类上定义的事务设置。

````java
@Transactional(readOnly = true)
public class DefaultFooService implements FooService {

    public Foo getFoo(String fooName) {
        // do something
    }

    // these settings have precedence for this method
    @Transactional(readOnly = false, propagation = Propagation.REQUIRES_NEW)
    public void updateFoo(Foo foo) {
        // do something
    }
}
````

##### `@Transactional` 设定

`@Transactional` 注解时一个元数据，用来指定一个接口，类或者方法必须拥有事务性语义 (比如，"当方法被调用时开启一个新的只读事务，阻塞任何现有事务")。默认的 `@Transactional` 注解设定如下：

* 传播设定是 `PROPAGATION_REQUIRED`。
* 隔离级别是 `ISOLATION_DEFAULT`。
* 事务是 读－写 的。
* 事务的超时时间默认是底层的事务系统的默认超时时间，如果底层事务系统不支持超时，则超时时间为空。
* 任何 `RuntimeException` 都会触发回滚，任何受检查的 `Exception` 不会。

你可以改变这些默认设定。下表概括了 `@Transactional` 注解的各种属性：

| Property                                                     | Type                                                         | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| [value](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#tx-multiple-tx-mgrs-with-attransactional) | `String`                                                     | 可选限定词指定要使用的事务管理器。                           |
| [propagation](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#tx-propagation) | `enum`: `Propagation`                                        | 可选的传播设定。                                             |
| `isolation`                                                  | `enum`: `Isolation`                                          | 可选的隔离级别。仅仅应用于传播设置 `REQUIRED` 或者 `REQUIRES_NEW`。 |
| `timeout`                                                    | `int` (in seconds of granularity)                            | 可选的事务超时时间。仅仅应用于传播设置 `REQUIRED` 或者 `REQUIRES_NEW`。 |
| `readOnly`                                                   | `boolean`                                                    | 读－写 或者 只读 事务。仅仅适用于传播设置 `REQUIRED` 或者 `REQUIRES_NEW`。 |
| `rollbackFor`                                                | Array of `Class` objects, which must be derived from `Throwable.` | 可选的必须导致回滚的异常类型数组。                           |
| `rollbackForClassName`                                       | Array of class names. The classes must be derived from `Throwable.` | 可选的必须导致回滚的异常名称数组。                           |
| `noRollbackFor`                                              | Array of `Class` objects, which must be derived from `Throwable.` | 可选的绝对不能导致回滚的异常类型数组。                       |
| `noRollbackForClassName`                                     | Array of `String` class names, which must be derived from `Throwable.` | 可选的绝对不能导致回滚的异常名称数组。                       |

目前，你不能显式控制事务的名称，也就是出现在兼容的 (比如，WebLogic 事务监视器) 事务监视器上表示事务名称的 `name` ，同时会记录在日志输出中。对声明式事务，事务名称永远都是全限定类名 ＋ `.` + 事务性增强的方法名称。比如，如果 `BusinessService` 类的 `handlePayment(..)` 方法启动一个事务，该事务的名称将是 `com.example.BusinessService.handlePayment`。

