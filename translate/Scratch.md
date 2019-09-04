### Event 和服务提供者包

**Event 包**

 [`javax.naming.event`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/package-summary.html) 包中包含用于支持命名和目录服务中的事件通知的类和接口。事件通知在 [Event Notification](https://docs.oracle.com/javase/tutorial/jndi/overview/event.html) 中详细描述。

 - 事件
      [`NamingEvent`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/NamingEvent.html) 表示由命名/目录服务生成的事件。该事件包含标识事件类型的类型。例如，事件类型分为影响命名空间的事件类型，例如“对象被添加”，和不影响命名空间的事件类型，例如“对象已更改”。
 - 监听器
      [`NamingListener`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/NamingListener.html) 是一个监听`NamingEvents`的对象。每种类型的事件类型都有相应类型的`NamingListener`。例如， [`NamespaceChangeListener`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/NamespaceChangeListener.html) 表示对命名空间更改事件感兴趣的侦听器， [`ObjectChangeListener`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/ObjectChangeListener.html) 表示对对象更改事件感兴趣的侦听器。

要接收事件通知，必须使用 [`EventContext`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/EventContext.html) 或 [`EventDirContext`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/EventDirContext.html) 注册侦听器。注册后，当命名/目录服务中发生相应的更改时，侦听器将接收事件通知。有关事件通知的详细信息，请参阅 [JNDI Tutorial](https://docs.oracle.com/javase/jndi/tutorial/beyond/event/index.html) 。

**服务提供者包**

 [`javax.naming.spi`](https://docs.oracle.com/javase/8/docs/api/javax/naming/spi/package-summary.html) 包提供了不同命名/目录服务提供者的开发人员可以开发和连接其实现的方法，以便可以从使用JNDI的应用程序访问相应的服务。

 - 插件架构
     `javax.naming.spi`包允许动态插入不同的实现。这些实现包括 [initial context](https://docs.oracle.com/javase/tutorial/jndi/ops/index.html) 和可以从初始上下文到达的上下文的实现。
 - Java对象支持
     `javax.naming.spi`包支持 [lookup](https://docs.oracle.com/javase/tutorial/jndi/ops/lookup.html) 和相关方法的实现，以返回Java程序员自然而直观的Java对象。例如，如果从目录中查找打印机名称，那么您可能希望找回要在其上运行的打印机对象。这种支持以对象工厂的形式提供。该软件包还支持反向操作。也就是说， [`Context.bind()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Context.html#bind-javax.naming.Name-java.lang.Object-) 和相关方法的实现者可以接受Java对象并以底层命名/目录服务可接受的格式存储对象。这种支持以 [state factories](https://docs.oracle.com/javase/tutorial/jndi/objects/index.html#STATEFAC) 的形式提供。
 - 多个命名系统（联合）
     JNDI操作允许应用程序提供跨多个命名系统的名称。在完成操作的过程中，一个服务提供者可能需要与另一个服务提供者交互，例如传递要在下一个命名系统中继续的操作。该软件包支持不同的提供商合作完成JNDI操作。

有关服务提供者机制的详细信息，请参阅 [JNDI Tutorial](https://docs.oracle.com/javase/jndi/tutorial/provider/index.html) 。

