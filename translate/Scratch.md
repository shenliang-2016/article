### 1.15 `ApplicationContext`的附加功能

如在 [章节介绍](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans) 中所述， `org.springframework.beans.factory` 包提供了基本的管理和操作 beans 的功能，包括编程方式。`org.springframework.context` 包添加了[`ApplicationContext`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/context/ApplicationContext.html) 接口，扩展了`BeanFactory`接口，同时继承了其它接口来通过面向应用框架的方式提供额外的功能性。很多人采用完全的声明式形式使用`ApplicationContext`，而不是通过编程方式创建它，而是依赖于`ContextLoader`等支持类来自动实例化`ApplicationContext`，作为Java EE Web应用程序正常启动过程的一部分。

要以更加面向框架的方式增强`BeanFactory`的功能性，`org.springframework.context`包也提供了下面的功能：

 - 通过`MessageSource`接口访问i18n风格的消息。
 - 通过`ResourceLoader`接口访问URL和文件等资源。
 - 事件发布，即通过使用`ApplicationEventPublisher`接口实现`ApplicationListener`接口的bean。
 - 加载多个（分层）上下文，让每个上下文通过`HierarchicalBeanFactory`接口聚焦于一个特定层，例如应用程序的Web层。

