#### 7.3.4. 使用 `@Async` 的执行器资格

默认情况下，当在方法上指定 `@Async` 注解时，使用的执行器就必须是 [启用异步支持时被配置的](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#scheduling-enable-annotation-support)，比如，如果你使用 XML，执行器就应该是 `annotation-driven` 元素，或者其本身是 `AsyncConfigurer` 实现，如果存在。不过，当你需指示执行给定方法，应使用默认值以外的执行器时，你可以使用 `@Async` 注解的 `value` 属性。下面的例子展示了具体做法：

```java
@Async("otherExecutor")
void doSomething(String s) {
    // this will be executed asynchronously by "otherExecutor"
}
```

在这种情况下，`otherExecutor` 可以是 Spring 容器中任何 `Executor` bean的名称，也可以是与任何 `Executor` 相关联的限定词的名称（例如，由 `<qualifier>` 元素或 Spring 的 `@Qualifier` 注解指定的）。

#### 7.3.5. 使用 `@Async` 时的异常管理

当 `@Async` 方法的返回值类型为 `Future` 时，很容易管理在方法执行过程中引发的异常，因为在对 `Future` 结果调用 `get` 时会引发该异常。但是，对于 `void` 返回类型，该异常是未捕获的，无法传输。您可以提供一个 `AsyncUncaughtExceptionHandler` 来处理此类异常。以下示例显示了如何执行此操作：

```java
public class MyAsyncUncaughtExceptionHandler implements AsyncUncaughtExceptionHandler {

    @Override
    public void handleUncaughtException(Throwable ex, Method method, Object... params) {
        // handle exception
    }
}
```

默认情况下，仅记录异常。您可以使用 `AsyncConfigurer` 或 `<task:annotation-driven/>` XML 元素来定义自定义的 `AsyncUncaughtExceptionHandler`。

