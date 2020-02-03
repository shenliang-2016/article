#### 4.18.4. 混合 XA 和非 XA JMS 连接

当使用 JTA 时，主要的 JMS `ConnectionFactory` bean 是 XA 感知的，并参与分布式事务。在某些情况下，您可能想通过使用非 XA `ConnectionFactory` 处理某些 JMS 消息。例如，您的 JMS 处理逻辑可能需要比 XA 超时更长的时间。

如果要使用非 XA 的 `ConnectionFactory`，则可以注入 `nonXaJmsConnectionFactory` bean 而不是 `@Primary` `jmsConnectionFactory` bean。为了保持一致性，还使用 bean 别名 `xaJmsConnectionFactory` 提供了 `jmsConnectionFactory` bean。

以下示例显示了如何注入 `ConnectionFactory` 实例：

```java
// Inject the primary (XA aware) ConnectionFactory
@Autowired
private ConnectionFactory defaultConnectionFactory;

// Inject the XA aware ConnectionFactory (uses the alias and injects the same as above)
@Autowired
@Qualifier("xaJmsConnectionFactory")
private ConnectionFactory xaConnectionFactory;

// Inject the non-XA aware ConnectionFactory
@Autowired
@Qualifier("nonXaJmsConnectionFactory")
private ConnectionFactory nonXaConnectionFactory;
```

#### 4.18.5. 支持替代嵌入式事务管理器

[`XAConnectionFactoryWrapper`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jms/XAConnectionFactoryWrapper.java) 和 [`XADataSourceWrapper`](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jdbc/XADataSourceWrapper.java) 接口可用于支持其他嵌入式事务管理器。这些接口负责包装 `XAConnectionFactory` 和 `XADataSource` bean，并将它们作为常规的 `ConnectionFactory` 和 `DataSource` bean公开，它们透明地注册在分布式事务中。数据源和 JMS 自动配置使用 JTA 变体，前提是您具有 `JtaTransactionManager` bean 和在 `ApplicationContext` 中注册的适当 XA 包装 bean。

[BitronixXAConnectionFactoryWrapper](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jta/bitronix/BitronixXAConnectionFactoryWrapper.java) 和 [BitronixXADataSourceWrapper](https://github.com/spring-projects/spring-boot/tree/v2.2.2.RELEASE/spring-boot-project/spring-boot/src/main/java/org/springframework/boot/jta/bitronix/BitronixXADataSourceWrapper.java) 提供了有关如何编写 XA 包装器的良好示例。

