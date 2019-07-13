### 1.13 环境抽象

[`Environment`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/core/env/Environment.html) 接口是集成在容器内部的一个抽象，对应用环境的两个关键方面进行了建模： [profiles](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-definition-profiles) 和 [properties](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-property-source-abstraction).

配置文件是仅在给定配置文件处于活动状态时才向容器注册的bean定义的命名的逻辑组。可以将Bean分配给配置文件，无论该配置文件是以XML还是使用注解定义。与配置文件相关的`Environment`对象的作用是确定哪些配置文件（如果有）当前处于活动状态，以及默认情况下哪些配置文件（如果有）应该处于活动状态。

属性在几乎所有应用程序中都发挥着重要作用，可能源自各种来源：属性文件，JVM系统属性，系统环境变量，JNDI，servlet上下文参数，ad-hoc `Properties` 对象，`Map`对象等等。与属性相关的 `Environment` 对象的作用是为用户提供方便的服务界面，用于配置属性源和从中解析属性。

#### 1.13.1 Bean 定义配置

Bean定义配置文件在核心容器中提供了一种机制，允许在不同环境中注册不同的bean。“环境”这个词对不同的用户来说意味着不同的东西，这个功能在很多场景下都很有帮助，包括：

 - 在开发过程中使用内存中的数据源，而在QA或生产环境中通过JNDI查找相同的数据源。
 - 仅在将应用程序部署到性能环境时注册监控基础设施。
 - 为客户A和客户B部署注册各自的bean的自定义实施。

考虑一个场景，实际应用程序中需要一个`DataSource`。在测试环境中，配置可能类似于以下内容：

```java
@Bean
public DataSource dataSource() {
    return new EmbeddedDatabaseBuilder()
        .setType(EmbeddedDatabaseType.HSQL)
        .addScript("my-schema.sql")
        .addScript("my-test-data.sql")
        .build();
}
```

现在考虑如何将此应用程序部署到QA或生产环境中，假设应用程序的数据源已在生产应用程序服务器的JNDI目录中注册。我们的`dataSource` bean现在看起来如下：

```java
@Bean(destroyMethod="")
public DataSource dataSource() throws Exception {
    Context ctx = new InitialContext();
    return (DataSource) ctx.lookup("java:comp/env/jdbc/datasource");
}
```

问题是如何根据当前环境在使用这两种变体之间切换。随着时间的推移，Spring用户已经设计了许多方法来完成这项工作，通常依赖于系统环境变量和XML`<import/>`语句的组合，这些语句包含根据环境变量的值可以解析为正确配置文件路径的`${placeholder}`占位符。Bean定义配置文件是核心容器功能，可为此问题提供解决方案。

如果我们概括了前面的特定于环境的bean定义示例中展示的用例，我们最终需要在某些上下文中注册某些bean定义，而在其他上下文中则不需要。您可以说您希望在情境A中注册特定的bean定义配置文件，在情况B中注册不同的配置文件。我们首先更新配置以反映此需求。

