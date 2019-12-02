##### 从 JNDI 获取 EntityManagerFactory

当应用部署到 Java EE 服务器上时，你可以使用这种方法。参考你的服务器文档了解如何部署自定义 JPA 提供者到你的服务器，也就是部署服务器默认的提供者之外的 JPA 提供者。

从 JNDI 获取 `EntityManagerFactory` (比如在 Java EE 环境中) ，涉及到修改 XML 配置。如下面例子所示：

```xml
<beans>
    <jee:jndi-lookup id="myEmf" jndi-name="persistence/myPersistenceUnit"/>
</beans>
```

此操作假定标准 Java EE 引导。Java EE 服务器自动检测持久化单元（实际上是应用程序 jar 中的 `META-INF/persistence.xml` 文件）和 Java EE 部署描述符中的 `persistence-unit-ref` 条目（例如，`web.xml`） ），并为这些持久化单元定义环境命名上下文位置。

在这种情况下，整个持久化单元部署，包括持久化类的编织（字节码转换），都取决于 Java EE 服务器。JDBC `DataSource` 是通过 `MEA-INF/persistence.xml` 文件中的 JNDI 位置定义的。 `EntityManager` 事务与服务器的 JTA 子系统集成在一起。Spring 仅使用获得的 `EntityManagerFactory`，通过依赖注入将其传递给应用程序对象，并管理持久化单元的事务（通常通过 `JtaTransactionManager`）。

如果在同一应用程序中使用多个持久化单元，则此类 JNDI 检索的持久化单元的 Bean 名称应与应用程序用来引用它们的持久化单元（例如，在 `@PersistenceUnit` 和 `@PersistenceContext` 注解中 ）名称相匹配。

