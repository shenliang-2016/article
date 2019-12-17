#### 7.3.3.  `@Async` 注解

您可以在方法上提供 `@Async` 注解，以便异步调用该方法。换句话说，调用者在调用时立即返回，而方法的实际执行发生在已提交给 Spring `TaskExecutor` 的任务中。在最简单的情况下，可以将注解应用于返回 `void` 的方法，如以下示例所示：

```java
@Async
void doSomething() {
    // this will be executed asynchronously
}
```

与用 `@Scheduled` 注解注释的方法不同，这些方法可以使用参数，因为它们在运行时由调用者以“常规”方式调用，而不是从容器管理的计划任务中调用。例如，以下代码是 `@Async` 注解的合法应用程序：

```java
@Async
void doSomething(String s) {
    // this will be executed asynchronously
}
```

即使有返回值的方法也可以异步调用。但是，要求此类方法具有 `Future` 类型的返回值。这仍然提供了异步执行的好处，以便调用者可以在对该 `Future` 调用 `get()` 之前执行其他任务。以下示例说明如何在有返回值的方法上使用 `@Async`：

```java
@Async
Future<String> returnSomething(int i) {
    // this will be executed asynchronously
}
```

> `@Async` 方法不仅可以声明常规的 `java.util.concurrent.Future` 返回类型，还可以声明 Spring 的 `org.springframework.util.concurrent.ListenableFuture`，或者从 Spring 4.2 起声明 JDK 8 的 `java.util.parallel.CompletableFuture`，用于与异步任务进行更丰富的交互，并与进一步的处理步骤立即进行合成。

您不能将 `@Async` 与生命周期回调（如 `@PostConstruct` ）结合使用。要异步初始化 Spring Bean，当前必须使用单独的初始化 Spring Bean，然后在目标上调用带有 `@Async` 注解的方法，如以下示例所示：

```java
public class SampleBeanImpl implements SampleBean {

    @Async
    void doSomething() {
        // ...
    }

}

public class SampleBeanInitializer {

    private final SampleBean bean;

    public SampleBeanInitializer(SampleBean bean) {
        this.bean = bean;
    }

    @PostConstruct
    public void initialize() {
        bean.doSomething();
    }

}
```

> `@Async` 没有直接的 XML 等效项，因为此类方法应首先设计用于异步执行，而不是在外部重新声明为异步。不过，您可以结合使用自定义切入点，通过 Spring AOP 手动设置 Spring 的 `AsyncExecutionInterceptor`。

