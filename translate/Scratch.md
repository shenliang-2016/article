### 7.3. 对调度和异步执行的注解支持

Spring 同时提供了对调度和异步方法执行的注解支持。

#### 7.3.1. 启用调度注解

为了开启对 `@Scheduled` 和 `@Async` 注解的支持，你可以添加 `@EnableScheduling` 和 `@EnableAsync` 到你的任何一个 `@Configuration` 类中，如下面例子所示：

```java
@Configuration
@EnableAsync
@EnableScheduling
public class AppConfig {
}
```

你可以为你的应用挑选相关注解。比如，如果你只需要 `@Scheduled` 支持，你就可以省略 `@EnableAsync` 注解。为了进行更加精细的控制，你可以额外实现 `SchedulingConfigurer` 接口，或者 `AsyncConfigurer` 接口，或者同时实现两者。参考 [`SchedulingConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/scheduling/annotation/SchedulingConfigurer.html) 和 [`AsyncConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/scheduling/annotation/AsyncConfigurer.html) 文档获取更多细节。

如果你更喜欢 XML 配置，你可以使用 `<task:annotation-driven>` 元素，如下面例子所示：

```xml
<task:annotation-driven executor="myExecutor" scheduler="myScheduler"/>
<task:executor id="myExecutor" pool-size="5"/>
<task:scheduler id="myScheduler" pool-size="10"/>
```

注意，在上面的 XML 中，给定一个执行器引用来处理其中对应于 `@Async` 注解修饰的方法的任务，而给定的调度器引用管理 `@Scheduled` 注解修饰的方法 。

> 处理 `@Async` 注解的默认增强模式是 `proxy`（代理），它仅允许通过代理来拦截调用。同一类内的本地调用无法以这种方式被拦截。对于更高级的拦截模式，请考虑结合编译时或加载时编织切换到 `aspectj` 模式。

#### 7.3.2.  `@Scheduled` 注解

您可以将 `@Scheduled` 注解以及触发器元数据添加到方法上。例如，以下方法每隔五秒钟以固定的延迟被调用一次，这意味着该时间段是从每个先前调用的完成时间开始计算的：

```java
@Scheduled(fixedDelay=5000)
public void doSomething() {
    // something that should execute periodically
}
```

如果需要固定速率执行，则可以更改注解中指定的属性名称。每五秒钟调用一次以下方法（在每次调用的连续开始时间之间测量时间间隔）：

```java
@Scheduled(fixedRate=5000)
public void doSomething() {
    // something that should execute periodically
}
```

对于固定延迟和固定速率的任务，可以通过指示在第一次执行该方法之前要等待的毫秒数来指定初始延迟，如下面的 `fixedRate` 示例所示：

```java
@Scheduled(initialDelay=1000, fixedRate=5000)
public void doSomething() {
    // something that should execute periodically
}
```

如果简单的周期性调度不足以满足需求，则可以提供 cron 表达式。例如，以下仅在工作日执行：

```java
@Scheduled(cron="*/5 * * * * MON-FRI")
public void doSomething() {
    // something that should execute on weekdays only
}
```

> 你还可以使用 `zone` 属性来指定 cron 表达式应该在哪个时区被解析。

请注意，要调度的方法必须具有空返回值，并且不能期望任何参数。如果该方法需要与应用程序上下文中的其他对象进行交互，则通常将通过依赖项注入来提供这些对象。

> 从 Spring Framework 4.3 开始，任何作用域范围的 bean 都支持 `@Scheduled` 方法。
>
> 确保不要在运行时初始化同一个 `@Scheduled` 注解类的多个实例，除非您确实希望为每个此类实例安排回调。与此相关的是，请确保不要在以 `@Scheduled` 注解并已在容器中注册为常规 Spring bean 的 bean 类上使用 `@ Configurable`。否则，您将获得双重初始化（一次通过容器，一次通过 `@Configurable` 切面），结果每个 `@Scheduled` 方法被调用两次。

