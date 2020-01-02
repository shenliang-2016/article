#### 4.1.6. 应用事件和监听器

除了通常的 Spring 框架事件，比如 [`ContextRefreshedEvent`](https://docs.spring.io/spring/docs/5.2.2.RELEASE/javadoc-api/org/springframework/context/event/ContextRefreshedEvent.html)，`SpringApplication` 还发送一些别的应用事件。

> 有些事件实际上是在创建 `ApplicationContext` 之前触发的，因此您不能将这些事件的监听器注册为 `@Bean`。您可以使用 `SpringApplication.addListeners(…)` 方法或 `SpringApplicationBuilder.listeners(…)` 方法注册它们。
>
> 如果您希望这些侦听器自动注册，而不管创建应用程序的方式如何，都可以将 `META-INF/spring.factories` 文件添加到您的项目中，并使用 `org.springframework.context.ApplicationListener` 键引用您的侦听器 。如以下示例所示：
>
> ```
> org.springframework.context.ApplicationListener=com.example.project.MyListener
> ```

当你的应用运行时，应用事件按照下面的顺序发送：

1. `ApplicationStartingEvent` 在运行开始时发送，但在进行任何处理之前（侦听器和初始化器的注册除外）发送。

2. 当已知要在上下文中使用的 `Environment` 但在创建上下文之前，发送 `ApplicationEnvironmentPreparedEvent`。

3. 在准备好 `ApplicationContext` 并调用 `ApplicationContextInitializers` 之后，但在加载任何 bean 定义之前，将发送一个 `ApplicationContextInitializedEvent`。

4. 在刷新开始之前，但在加载了 bean 定义之后，发送一个 `ApplicationPreparedEvent`。

5. 在刷新上下文之后，但在调用任何应用程序和命令行运行程序之前，将发送 `ApplicationStartedEvent`。

6. 在调用了任何应用程序和命令行运行程序之后，将发送 `ApplicationReadyEvent`。它指示该应用程序已准备就绪，可以处理请求。

7. 如果启动时发生异常，则发送一个 `ApplicationFailedEvent`。

上面的列表仅包含与 `SpringApplication` 绑定的 `SpringApplicationEvent`。除此之外，以下事件还会在 `ApplicationPreparedEvent` 之后和 `ApplicationStartedEvent` 之前发布：

1. 当刷新 `ApplicationContext` 时，发送 `ContextRefreshedEvent`。

2. 在准备好 WebServer 之后，发送一个 `WebServerInitializedEvent`。`ServletWebServerInitializedEvent` 和 `ServletWebServerInitializedEvent` 分别是 servlet 和反应式变体。

> 您通常不需要使用应用程序事件，但是很容易知道它们的存在。在内部，Spring Boot 使用事件来处理各种任务。

应用程序事件是通过使用 Spring Framework 的事件发布机制发送的。此机制的一部分确保在子级上下文中发布给侦听器的事件也在任何祖先上下文中也发布给侦听器。结果，如果您的应用程序使用 `SpringApplication` 实例的层次结构，则侦听器可能会收到同一类型的应用程序事件的多个实例。

为了使您的侦听器能够区分其上下文的事件和后代上下文的事件，它应请求注入其应用程序上下文，然后将注入的上下文与事件的上下文进行比较。可以通过实现 `ApplicationContextAware` 来注入上下文，或者如果侦听器是 bean，则可以通过使用 `@Autowired` 注入上下文。

