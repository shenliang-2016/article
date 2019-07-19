#### 1.15.2 标准事件和自定义事件

`ApplicationContext`中的事件处理通过`ApplicationEvent`类和`ApplicationListener`接口提供。如果一个实现了`ApplicationListener`接口的 bean 部署到上下文中，每当有`ApplicationEvent`被发布到`ApplicationContext`中时，该 bean 就会被通知到。本质上，这就是一个标准的观察者设计模式。

> 在 Spring 4.2 中，事件基础设施已经被显著改进，提供了一个 [annotation-based model](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#context-functionality-events-annotation) 和发布任意事件的能力 (也就是说，事件对象甚至都不需要扩展自 `ApplicationEvent`)。当这种对象被发布，Spring 会将它包装成一个事件。

下表描述了 Spring 提供的标准事件：

| Event                   | Explanation                              |
| ----------------------- | ---------------------------------------- |
| `ContextRefreshedEvent` | 初始化或刷新`ApplicationContext`时发布（例如，通过使用`ConfigurableApplicationContext`接口上的`refresh()`方法）。这里，“已初始化”意味着加载所有bean，检测并激活后处理器bean，预先实例化单例，并且`ApplicationContext`对象已准备好使用。只要上下文尚未关闭，而所选的`ApplicationContext`实际支持这种“热”刷新，就可以多次触发刷新。例如，`XmlWebApplicationContext`支持热刷新，但`GenericApplicationContext`不支持。 |
| `ContextStartedEvent`   | 通过使用`ConfigurableApplicationContext`接口上的`start()`方法启动`ApplicationContext`时发布。这里，“已启动”表示所有`Lifecycle`bean都会收到明确的启动信号。通常，此信号用于在显式停止后重新启动Bean，但它也可用于启动尚未为自动启动配置的组件（例如，尚未在初始化时启动的组件）。 |
| `ContextStoppedEvent`   | 通过使用`ConfigurableApplicationContext`接口上的`stop()`方法停止`ApplicationContext`时发布。这里，“已停止”表示所有`Lifecycle`bean都会收到明确的停止信号。可以通过`start()`调用重新启动已停止的上下文。 |
| `ContextClosedEvent`    | 通过使用`ConfigurableApplicationContext`接口上的`close()`方法关闭`ApplicationContext`时发布。这里，“关闭”意味着所有单例bean都被销毁。封闭的环境达到了生命的终点。它无法刷新或重新启动。 |
| `RequestHandledEvent`   | 一个特定于Web的事件，告诉所有bean已经为HTTP请求提供服务。请求完成后发布此事件。此事件仅适用于使用Spring的`DispatcherServlet`的Web应用程序。 |

你还可以创建并发布自定义事件，下面的例子展示了一个简单的类，它扩展了 Spring 的`ApplicationEvent`基类：

```java
public class BlackListEvent extends ApplicationEvent {

    private final String address;
    private final String content;

    public BlackListEvent(Object source, String address, String content) {
        super(source);
        this.address = address;
        this.content = content;
    }

    // accessor and other methods...
}
```

为了发布一个自定义`ApplicationEvent`，请调用`ApplicationEventPublisher`上的`publishEvent`方法。典型地，这通过创建一个实现`ApplicationEventPublisherAware`接口并将其注册为 Spring 的 bean 的方式来实现。下面的例子展示了这样一个类：

```java
public class EmailService implements ApplicationEventPublisherAware {

    private List<String> blackList;
    private ApplicationEventPublisher publisher;

    public void setBlackList(List<String> blackList) {
        this.blackList = blackList;
    }

    public void setApplicationEventPublisher(ApplicationEventPublisher publisher) {
        this.publisher = publisher;
    }

    public void sendEmail(String address, String content) {
        if (blackList.contains(address)) {
            publisher.publishEvent(new BlackListEvent(this, address, content));
            return;
        }
        // send email...
    }
}
```

在配置时，Spring容器检测到`EmailService`实现`ApplicationEventPublisherAware`并自动调用`setApplicationEventPublisher()`。实际上，传入的参数是Spring容器本身。您正在通过其`ApplicationEventPublisher`接口与应用程序上下文进行交互。

要接收自定义`ApplicationEvent`，您可以创建一个实现`ApplicationListener`的类并将其注册为Spring bean。 以下示例显示了这样一个类：

```java
public class BlackListNotifier implements ApplicationListener<BlackListEvent> {

    private String notificationAddress;

    public void setNotificationAddress(String notificationAddress) {
        this.notificationAddress = notificationAddress;
    }

    public void onApplicationEvent(BlackListEvent event) {
        // notify appropriate parties via notificationAddress...
    }
}
```

请注意，`ApplicationListener`通常使用自定义事件的类型进行参数化（前面示例中为`BlackListEvent`）。这意味着`onApplicationEvent()`方法可以保持类型安全，从而避免任何向下转换的需要。您可以根据需要注册任意数量的事件侦听器，但请注意，默认情况下，事件侦听器会同步接收事件。这意味着`publishEvent()`方法将阻塞，直到所有侦听器都已完成对事件的处理。这种同步和单线程方法的一个优点是，当侦听器接收到事件时，如果事务上下文可用，它将在发布者的事务上下文内运行。如果需要另一个事件发布策略，请参阅Spring的 [`ApplicationEventMulticaster`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/context/event/ApplicationEventMulticaster.html) 接口的javadoc。

以下示例显示了用于注册和配置上述每个类的bean定义：

```xml
<bean id="emailService" class="example.EmailService">
    <property name="blackList">
        <list>
            <value>known.spammer@example.org</value>
            <value>known.hacker@example.org</value>
            <value>john.doe@example.org</value>
        </list>
    </property>
</bean>

<bean id="blackListNotifier" class="example.BlackListNotifier">
    <property name="notificationAddress" value="blacklist@example.org"/>
</bean>
```

总而言之，当调用`emailService` bean的`sendEmail()`方法时，如果有任何应列入黑名单的电子邮件消息，则会发布`BlackListEvent`类型的自定义事件。`blackListNotifier` bean注册为`ApplicationListener`，并接收`BlackListEvent`，此时它可以通知相关方。

> Spring的事件机制是为在同一应用程序上下文中的Spring bean之间的简单通信而设计的。但是，对于更复杂的企业集成需求，单独维护的 [Spring Integration](https://projects.spring.io/spring-integration/) 项目为构建基于众所周知的Spring编程模型的轻量级，[pattern-oriented](https://www.enterpriseintegrationpatterns.com/)，事件驱动的体系结构提供了完整的支持。

##### 基于注解的事件监听器

从Spring 4.2开始，您可以使用`EventListener`注解在托管bean的任何公共方法上注册事件侦听器。`BlackListNotifier`可以重写如下：

```java
public class BlackListNotifier {

    private String notificationAddress;

    public void setNotificationAddress(String notificationAddress) {
        this.notificationAddress = notificationAddress;
    }

    @EventListener
    public void processBlackListEvent(BlackListEvent event) {
        // notify appropriate parties via notificationAddress...
    }
}
```

方法签名再次声明它侦听的事件类型，但这次使用灵活的名称并且没有实现特定的侦听器接口。只要实际事件类型在其实现层次结构中解析通用参数，也可以通过泛型缩小事件类型范围。

如果您的方法应该监听多个事件，或者您不想根据参数进行定义，那么也可以在注解本身上指定事件类型。以下示例显示了如何执行此操作：

```java
@EventListener({ContextStartedEvent.class, ContextRefreshedEvent.class})
public void handleContextStart() {
    ...
}
```

还可以通过使用定义 [`SpEL`expression](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#expressions) 的注解的`condition`属性来添加额外的运行时过滤，该属性应匹配以实际调用特定事件的方法。

以下示例显示了仅当事件的`content`属性等于`my-event`时，才能重写我们的通知程序以进行调用：

```java
@EventListener(condition = "#blEvent.content == 'my-event'")
public void processBlackListEvent(BlackListEvent blEvent) {
    // notify appropriate parties via notificationAddress...
}
```

每个`SpEL`表达式都针对专用上下文进行评估。下表列出了可用于上下文的项目，以便您可以将它们用于条件事件处理：

| Name            | Location           | Description                              | Example                                  |
| --------------- | ------------------ | ---------------------------------------- | ---------------------------------------- |
| Event           | root object        | 实际的 `ApplicationEvent` 。                 | `#root.event`                            |
| Arguments array | root object        | 用来调用目标的参数（作为数组）。                         | `#root.args[0]`                          |
| *Argument name* | evaluation context | 所有方法参数的名称。如果，由于某种原因，该名称不可用（比如，不存在调试信息），该参数名称也可以在`#a<#arg>`下面找到，其中`#arg`代表参数下标（从0开始）。 | `#blEvent` 或者 `#a0` (你也可以使用 `#p0` 或者 `#p<#arg>`记号作为别名) |

请注意，即使您的方法签名实际引用已发布的任意对象， `#root.event` 也允许您访问基础事件。

如果您需要发布作为处理其他事件的结果的事件，则可以更改方法签名以返回应发布的事件，如以下示例所示：

```java
@EventListener
public ListUpdateEvent handleBlackListEvent(BlackListEvent event) {
    // notify appropriate parties via notificationAddress and
    // then publish a ListUpdateEvent...
}
```

>   [异步监听器](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#context-functionality-events-async) 不支持此功能。

这个新方法为上面方法处理的每个`BlackListEvent`发布一个新的`ListUpdateEvent`。如果需要发布多个事件，则可以返回事件集合。

##### 异步监听器

如果你希望特定监听器异步处理事件，可以复用 [regular `@Async` support](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/integration.html#scheduling-annotation-support-async) 。下面是例子：

```java
@EventListener
@Async
public void processBlackListEvent(BlackListEvent event) {
    // BlackListEvent is processed in a separate thread
}
```

使用异步监听器时注意以下限制：

- 如果事件监听器抛出 `Exception`，它并不会传播给调用者。参考 `AsyncUncaughtExceptionHandler` 获取更多细节。
- 这种事件监听器不能发送回复。如果你需要发送另外一个事件作为某个事件处理的结果，注入[`ApplicationEventPublisher`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/aop/interceptor/AsyncUncaughtExceptionHandler.html) 来手动发送它。

##### 监听器排序

如果需要在另一个侦听器之前调用一个侦听器，则可以将`@Order`注解添加到方法声明中，如以下示例所示：

```java
@EventListener
@Order(42)
public void processBlackListEvent(BlackListEvent event) {
    // notify appropriate parties via notificationAddress...
}
```

##### 泛型事件

您还可以使用泛型来进一步定义事件的结构。考虑使用`EntityCreatedEvent <T>`，其中`T`是创建的实际实体的类型。例如，您可以创建以下侦听器定义以仅接收`Person`的`EntityCreatedEvent`：

```java
@EventListener
public void onPersonCreated(EntityCreatedEvent<Person> event) {
    ...
}
```

由于类型擦除，仅当被触发的事件解析了事件侦听器过滤器的泛型参数时（即类`PersonCreatedEvent`类扩展了`EntityCreatedEvent <Person> {...}`），这才起作用。

在某些情况下，如果所有事件都遵循相同的结构，这可能会变得相当繁琐（前面示例中的事件应该如此）。在这种情况下，您可以实现`ResolvableTypeProvider`来在超出运行时环境提供的范围时指导框架。以下事件显示了如何执行此操作：

```java
public class EntityCreatedEvent<T> extends ApplicationEvent implements ResolvableTypeProvider {

    public EntityCreatedEvent(T entity) {
        super(entity);
    }

    @Override
    public ResolvableType getResolvableType() {
        return ResolvableType.forClassWithGenerics(getClass(), ResolvableType.forInstance(getSource()));
    }
}
```

> 这不仅可以用于 `ApplicationEvent` ，还可以用于任何你作为事件发送的对象。

