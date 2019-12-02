##### 使用 `LocalContainerEntityManagerFactoryBean`

您可以在基于 Spring 的应用程序环境中将此选项用于完整的 JPA 功能。这包括 Web 容器（例如 Tomcat），独立应用程序以及具有复杂持久化要求的集成测试。

> 如果您要专门配置 Hibernate 设置，则直接选择使用 Hibernate 5.2 或 5.3 并设置本机 Hibernate `LocalSessionFactoryBean`，而不是普通的 JPA `LocalContainerEntityManagerFactoryBean`，使其与 JPA 访问代码以及本机 Hibernate 访问代码交互。有关详细信息，请参见 [用于JPA交互的本地 Hibernate 设置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#orm-jpa-hibernate) 。

`LocalContainerEntityManagerFactoryBean` 可以完全控制 `EntityManagerFactory` 的配置，适用于需要细粒度自定义的环境。`LocalContainerEntityManagerFactoryBean` 基于 `persistence.xml` 文件，提供的 `dataSourceLookup` 策略和指定的 `loadTimeWeaver` 创建一个 `PersistenceUnitInfo` 实例。因此，可以在 JNDI 之外使用自定义数据源并控制编织过程。以下示例显示了 `LocalContainerEntityManagerFactoryBean` 的典型 bean 定义：

```xml
<beans>
    <bean id="myEmf" class="org.springframework.orm.jpa.LocalContainerEntityManagerFactoryBean">
        <property name="dataSource" ref="someDataSource"/>
        <property name="loadTimeWeaver">
            <bean class="org.springframework.instrument.classloading.InstrumentationLoadTimeWeaver"/>
        </property>
    </bean>
</beans>
```

下面的例子展示了一个典型的 `persistence.xml` 文件：

```xml
<persistence xmlns="http://java.sun.com/xml/ns/persistence" version="1.0">
    <persistence-unit name="myUnit" transaction-type="RESOURCE_LOCAL">
        <mapping-file>META-INF/orm.xml</mapping-file>
        <exclude-unlisted-classes/>
    </persistence-unit>
</persistence>
```

> `<exclude-unlisted-classes/>` 快捷方式表示不应对带注解的实体类进行扫描。显式的 `true` 值（`<exclude-unlist-classes>true</exclude-unlisted-classes/>`）也表示不进行扫描。`<exclude-unlisted-classes>false</exclude-unlisted-classes/>` 确实会触发扫描。但是，如果您希望进行实体类扫描，建议您省略 `exclude-unlisted-classes`元素。

使用 `LocalContainerEntityManagerFactoryBean` 是最强大的 JPA 设置选项，允许在应用程序中进行灵活的本地配置。它支持到现有 JDBC `DataSource` 的链接，同时支持本地和全局事务，等等。但是，这也对运行时环境提出了要求。例如，如果持久化提供程序要求字节码转换，则需要具有可编织特性的类加载器。

此选项可能与 Java EE 服务器的内置 JPA 功能冲突。在完整的 Java EE 环境中，请考虑从 JNDI 获取您的 `EntityManagerFactory`。或者，在您的 `LocalContainerEntityManagerFactoryBean` 定义上指定一个自定义的 `persistenceXmlLocation` （例如，`META-INF/my-persistence.xml`），并在应用程序 jar 文件中仅包含具有该名称的描述符。由于 Java EE 服务器仅查找默认的 `META-INF/persistence.xml` 文件，因此它会忽略此类自定义持久化单元，因此避免了与 Spring 预先驱动的 JPA 设置发生冲突。（例如，这适用于 Resin 3.1。）

