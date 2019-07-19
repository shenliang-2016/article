#### 1.15.3 低级资源的方便访问

为了优化对应用上下文的理解和使用，你应该熟悉 Spring 的`Resource`抽象，如 [Resources](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources) 中所描述。

一个应用上下文是一个`ResourceLoader`，它可以被用来加载`Resource`对象。`Resource`对象本质上是功能丰富版本的 JDK `java.net.URL`类。事实上，`Resource`的实现适当地包装了一个`java.net.URL`实例。`Resource`对象能够从几乎任何地方透明地获取低级资源，包括从类路径、文件系统位置、任何以标准 URL 或者其它变体描述的位置。如果资源位置字符串是一个简单路径，没有任何特殊前缀，那么这些资源的来源就是特定的，而且适合于实际应用的上下文类型。

你可以配置一个部署到应用上下文中的 bean 来实现特殊的回调接口，`ResourceLoaderAware`，会在初始化时刻被自动回调，此时应用上下文本身被作为`ResourceLoader`被传入。你也可以暴露`Resource`类型的属性，以便访问静态资源。它们像其它所有属性一样被注入。您可以为这些`Resource`属性指定简单的`String`路径，并在部署Bean时依赖从这些文本字符串到实际`Resource`对象的自动转换。

提供给`ApplicationContext`构造器的位置路径是实际的资源字符串，或者是其简单形式，根据特定的上下文实现，各种形式都会被恰当地处理。比如，`ClassPathXmlApplicationContext`将简单位置路径作为类路径位置。你也可以在位置路径（资源字符串）上使用特定的前缀来强制定义从类路径或者 URL 加载，而不管实际的上下文类型。

#### 1.15.4 Web 应用的 ApplicationContext 方便实例化

您可以使用例如`ContextLoader`以声明方式创建`ApplicationContext`实例。当然，您也可以使用其中一个`ApplicationContext`实现以编程方式创建`ApplicationContext`实例。

您可以使用`ContextLoaderListener`注册`ApplicationContext`，如以下示例所示：

```xml
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>/WEB-INF/daoContext.xml /WEB-INF/applicationContext.xml</param-value>
</context-param>

<listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
```

侦听器检查`contextConfigLocation`参数。如果参数不存在，则侦听器将`/WEB-INF/applicationContext.xml`用作默认值。当参数确实存在时，侦听器使用预定义的分隔符（逗号，分号和空格）分隔`String`，并将值用作搜索应用程序上下文的位置。同时还支持Ant样式的路径模式。示例是`/WEB-INF/*Context.xml`（对于名称以`Context.xml`结尾且位于`WEB-INF`目录中的所有文件）和`/WEB-INF/**/*Context.xml`（对于所有 `WEB-INF`的任何子目录中的此类文件）。

#### 1.15.5 以 Java EE RAR 文件形式部署 Spring `ApplicationContext` 

可以将Spring `ApplicationContext`部署为RAR文件，将上下文及其所有必需的bean类和库JAR封装在Java EE RAR部署单元中。这相当于引导能够访问Java EE服务器设施的独立`ApplicationContext`（仅托管在Java EE环境中）。RAR部署是部署无头WAR文件的一种更自然的替代方案 - 实际上是一个没有任何HTTP入口点的WAR文件，仅用于在Java EE环境中引导Spring `ApplicationContext`。

RAR部署非常适用于不需要HTTP入口点但仅包含消息端点和预定作业的应用程序上下文。在这样的上下文中，Bean可以使用应用程序服务器资源，例如JTA事务管理器和JNDI绑定的JDBC `DataSource`实例以及JMS `ConnectionFactory`实例，并且还可以通过Spring的标准事务管理以及JNDI和JMX支持工具向平台的JMX服务器注册。应用程序组件还可以通过Spring的`TaskExecutor`抽象与应用程序服务器的JCA `WorkManager`进行交互。

有关RAR部署中涉及的配置详细信息，请参阅 [`SpringContextResourceAdapter`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/jca/context/SpringContextResourceAdapter.html) 类的javadoc。

对于将Spring `ApplicationContext`简单部署为Java EE RAR文件：

1. 将所有应用程序类打包到一个RAR文件（这是一个具有不同文件扩展名的标准JAR文件）。将所有必需的库JAR添加到RAR存档的根目录中。添加`META-INF/ra.xml`部署描述符（如 [javadoc for `SpringContextResourceAdapter`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/jca/context/SpringContextResourceAdapter.html) 所示）和相应的Spring XML bean定义文件（通常是`META-INF/applicationContext.xml`）。
2. 将生成的RAR文件放入应用程序服务器的部署目录中。

> 这种RAR部署单元通常是独立的。它们不会将组件暴露给外部世界，甚至不会暴露给同一应用程序的其他模块。与基于RAR的`ApplicationContext`的交互通常通过与其他模块共享的JMS目标进行。例如，基于RAR的`ApplicationContext`还可以调度一些作业或对文件系统（或类似物）中的新文件作出反应。如果它需要允许来自外部的同步访问，它可以（例如）导出RMI端点，这可以由同一台机器上的其他应用程序模块使用。

