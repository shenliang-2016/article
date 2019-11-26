# Data Access

**Version 5.1.9 RELEASE**

此部分文档聚焦于数据访问以及数据访问层和业务层或者服务层之间的交互。

Spring 的全面事务管理支持包含若干部分，同时结合了各种 Spring 框架集成的数据访问框架和技术的内容。

# 1. 事务管理

全面事务管理支持时使用 Spring 框架的核心吸引力之一。Spring 框架为事务管理提供了一种一致性抽象，提供了如下好处：

* 不同事务管理 APIs 拥有一致的编程模型，比如 Java Transaction API (JTA)，JDBC，Hiberante，以及 Java Persistence API (API)。
* [声明式事务管理](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative) 支持
* 相对于负责的事务管理 API，比如 JTA，更加简单的 [编程式](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-programmatic) 事务管理 API。
* 与 Spring 数据访问抽象的完美集成。

下面章节描述了 Spring 框架的事务特性和技术：

* [Spring 框架事务支持模型的优点](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-motivation) 描述了为什么你会想要使用 Spring 框架的事务抽象替代 EJB 容器管理的事务 (CMT) ，或者选择通过专用 API ，比如 Hibernate，来驱动本地事务。
* [理解 Spring 框架事务抽象](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-strategies) 强调了核心类，同时描述如何配置并获取各种数据源的 `DataSource` 实例。
* [使用事务同步资源](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#tx-resource-synchronization) 描述应用代码如何确保资源被合适地创建、重用以及清理。
* [声明式事务管理](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative) 描述声明式事务管理支持。
* [编程式事务管理](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-programmatic) 介绍编程式事务管理支持。
* [事务内部事件](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-event) 描述如何在事务中使用应用事件。

本章节还包含了有关最佳实践的讨论，[应用服务集成](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-application-server-integration)，以及 [通用问题解决方案](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-solutions-to-common-problems)。

## 1.1 Spring 框架的事务支持模型的优点

传统上，Java EE 开发者进行事务管理有两种选择：全局事务或者局部事务，两者都有明显局限性。全局和局部事务管理将在接下来两节中介绍。随后介绍 Spring 框架的事务管理支持如何解决全局和局部事务模型的局限性。

### 1.1.1 全局事务

全局事务允许你使用多种事务性资源，典型的如关系数据库和消息队列。应用服务器通过 JTA 管理全局事务，它是一个笨重的 API (部分缘于它的异常模型)。此外，一个 JTA `UserTransaction` 通常需要来自JNDI，这意味着你需要为了使用 JTA 而同时使用 JNDI。全局事务的使用限制了任何潜在的应用代码的复用，因为 JTA 通常只在应用服务器环境下可用。

之前，使用全局事务的更好选择是通过 EJB CMT (容器管理的事务)。CMT 是一种声明式事务的形式（区别于编程式事务管理）。EJB CMT 不需要事务相关的 JNDI lookups，尽管 EJB 本身仍然需要使用 JNDI。它大部分情况下不需要编写 Java 代码来控制事务。这样做的显著缺陷是 CMT 被绑定到 JTA 和应用服务器环境。同时，只有当开发者选择在 EJBs (或者至少在事务性 EJB 门面之后) 实现业务逻辑时 CMT 才是可用的。EJB 的负面影响是如此显著，因而在选择声明式事务管理时这绝对不是什么好的方案。

### 1.1.2 局部事务

局部事务是特定于资源的，比如关联与一个 JDBC 连接的事务。局部事务可能更容易使用，但是具有明显缺陷：它们不能处理跨多种资源的事务。比如，通过使用 JDBC 连接管理事务的代码不能运行在全局 JTA 事务中。由于应用服务器并未卷入事务管理，它不能帮助确保多种资源的正确性。(值得注意的是，大部分应用都只使用单一一种事务性资源。) 另一个缺点是局部事务会侵入编程模型。

### 1.1.3 Spring 框架的一致性编程模型

Spring 解决了全局和局部事务的弊端。它使应用程序开发人员可以在任何环境中使用一致的编程模型。您只需编写一次代码，即可在不同环境中受益于不同的事务管理策略。Spring 框架提供了声明式和编程式事务管理。大多数用户喜欢声明式事务管理，在大多数情况下我们建议这样做。

使用编程式事务管理，开发人员可以使用 Spring Framework 事务抽象，该抽象可以在任何基础事务基础架构上运行。使用首选的声明性模型，开发人员通常只需编写很少或完全不需要编写与事务管理相关的代码，因此，它们不依赖于 Spring Framework 事务 API 或任何其他事务 API。

> 你是否需要应用服务器以进行事务管理？
>
> Spring 框架的事务管理支持改变了企业级 Java 应用何时需要应用服务器的传统的判断准则。
>
> 特别地，如果仅仅是通过 EJBs 声明事务，你不需要应用服务器。事实上，即使你的应用服务器拥有强大的 JTA 能力，你仍然可以选择使用 Spring 框架的声明式事务提供相比于 EJB CMT 更加强大、更加具有生产力的编程模型。
>
> 通常，仅当您的应用程序需要处理跨多个资源的事务时才需要应用程序服务器的 JTA 功能，而这并不是许多应用程序所必需的。许多高端应用程序都使用单个高度可扩展的数据库（例如 Oracle RAC）。独立事务管理器（例如 [Atomikos Transactions](https://www.atomikos.com/) 和 [JOTM](http://jotm.objectweb.org/)）是其他选择。当然，您可能需要其他应用程序服务器功能，例如 Java消息服务（JMS）和 Java EE 连接器体系结构（JCA）。
>
> Spring 框架使您可以选择何时将应用程序扩展到完全加载的应用程序服务器。不再使用 EJB CMT 或 JTA 的唯一选择是使用局部事务（例如 JDBC 连接上的事务）编写代码，并且如果您需要使代码在全局的，容器管理的事务中运行，则面临大量的返工。使用Spring 框架，仅需要更改配置文件中的某些 Bean 定义（而不是代码）。

## 1.2 理解 Spring 框架的事务抽象

Spring 事务抽象的关键是事务策略的概念。事务策略由 `org.springframework.transaction.PlatformTransactionManager` 接口定义，下面是代码：

````java
public interface PlatformTransactionManager {
  TransactionStatus getTransaction(TransactionDefinition definition) throws TransactionException;
  void commit(TransactionStatus status) throws TransactionException;
  void rollback(TransactionStatus status) throws TransactionException;
}
````

这主要是一个服务提供者接口(SPI)，尽管你可以在你的应用代码中[编程式](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-programmatic-ptm)使用它。由于 `PlatformTransactionManager` 是一个接口，必要的时候它可以很容易地被模拟或者代理。它并未绑定到 lookup 策略，比如 JNDI。`PlatformTransactionManager` 实现像其他 Spring 框架 IoC 容器内的对象(或者 bean)那样被定义。这一点使得 Spring 框架的事务成为一种很有价值的抽象，即使在你使用 JTA 时。相对于直接使用 JTA，测试事务性代码将会容易地多。

同时，为了遵循 Spring 设计哲学，`PlatformTransactionManager`  接口的所有方法都可能抛出 的 `TransactionException` 是不受检查的(也就是说，它扩展了 `java.lang.RuntimeException` 类)。事务基础设施失败几乎总是致命的。极少情况下，应用代码可以从事务失败中恢复，应用开发者仍然能够选择捕获并处理 `TransactionException` 。显然地，开发者不是必须这么做。

`getTransaction(..)` 方法返回一个 `TransactionStatus` 对象，依赖于 `TransactionDefinition` 参数。返回的 `TransactionStatus` 可能表示一个新的事务，也可以表示一个已经存在的事务，如果一个匹配的事务存在于当前调用栈中。后者的意义在于，就像在 Java EE 事务上下文中那样，一个 `TransactionStatus` 关联到一个执行线程。

`TransactionDefinition` 接口指出：

* 传播：典型的，在一个事务作用域中执行的所有代码都运行在该事务中。不过，如果一个事务性的方法在一个事务上下文已经存在的情况下执行时，你可以指定其行为。比如，代码可以继续运行在现有的事务中(通常情况下)，或者现存的事务可以被阻塞，同时一个新的事务被创建。Spring 提供了类似于 EJB CMT 的所有事务传播选项。要了解 Spring 中的事务传播语义，参考[事务传播](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#tx-propagation)。

* 隔离：一个事务与其他事务的工作内容的隔离程度。比如，一个事务能否看到其他事务尚未提交的写入？
* 超时：超时之前一个事务可以运行多久，超时之后会自动被潜在的事务基础设施回滚。
* 只读状态：当你的代码只读取而不会修改数据时，你可以使用只读事务。只读事务在某些情况下是一种很有用的优化，比如当你使用 Hibernate 时。

这些设置反映了标准的事务性概念。如果必要，请参考讨论事务隔离级别以及其他核心事务概念的文档资源。理解这些概念是使用 Spring 框架或者其他任何事务管理方案的基础。

`TransactionStatus` 接口提供了一种简单的方式编写事务性代码以控制事务执行并查询事务状态。这些概念都是类似的，对所有事务 APIs 都是通用的。下面的代码展示了 `TransactionStatus` 接口：

````java
public interface TransactionStatus extends SavepointManager {
  
  boolean isNewTransaction();
  
  boolean hasSavepoint();
  
  void setRollbackOnly();
  
  boolean isRollbackOnly();
  
  void flush();
  
  boolean isCompleted();
  
}
````

无论你选择在 Spring 中使用声明式事务还是编程式事务，定义合适的 `PlatformTransactionManager` 实现是最基础的。典型的定义是通过依赖注入。

`PlatformTransactionManager` 实现通常需要获取它们运行环境的信息：JDBC，JTA，Hibernate 等等。下面的例子展示了如何定义一个局部的 `PlatformTransactionManager` 实现(这里使用原生 JDBC)。

你可以定义一个 JDBC `DataSource` ，通过下面这样创建一个 bean ：

````xml
<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
    <property name="driverClassName" value="${jdbc.driverClassName}" />
    <property name="url" value="${jdbc.url}" />
    <property name="username" value="${jdbc.username}" />
    <property name="password" value="${jdbc.password}" />
</bean>
````

相关的 `PlatformTransactionManager` bean 定义就拥有了一个 `DataSource` 定义的引用。类似下面的例子：

````xml
<bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
  <property name="dataSource" ref="dataSource"/>
</bean>
````

如果你在 Java EE 容器中使用 JTA，然后你使用容器 `DataSource` ，通过 JNDI 获取，结合 Spring 的 `JtaTransactionManager` 。下面的例子展示了 JTA 和 JNDI lookup 可能的样子：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:jee="http://www.springframework.org/schema/jee"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/jee
        https://www.springframework.org/schema/jee/spring-jee.xsd">

    <jee:jndi-lookup id="dataSource" jndi-name="jdbc/jpetstore"/>

    <bean id="txManager" class="org.springframework.transaction.jta.JtaTransactionManager" />

    <!-- other <bean/> definitions here -->

</beans>
````

`JtaTransactionManager` 不需要了解 `DataSource` (或者任何其他特定资源)，因为它使用容器的全局事务管理基础设施。

> 前面的 `dataSource` 定义使用了来自 `jee` 明明空间的 `<jndi-lookup/>` 标签。更多相关信息，参考 [The JEE Schema](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/integration.html#xsd-schemas-jee)。

你还可以简单地使用 Hibernate 局部事务，如下面例子所示。这种情况下，你需要定义一个 Hibernate `LocalSessionFactoryBean` ，你的应用代码可以使用它来获取 Hibernate `Session` 实例。

`DataSource` bean 定义类似于前面 JDBC 例子中所示，在下面例子中省略。

> 如果 `DataSource` (由任何非-JTA事务管理器使用) 通过 JNDI 查找，并由 Java EE 容器管理，它就应该是非事务性的，因为 Spring 框架 (而不是 Java EE 容器) 管理该事务。

`txManager` bean 在这种情况下是 `HibernateTransactionManager` 类型。类似于 `DataSourceTransactionManager` 需要 `DataSource` 的引用，`HibernateTransactionManager` 需要 `SessionFactory` 的引用。下面的例子声明了 `sessionFactory` 和 `txManager` beans ：

```xml
<bean id="sessionFactory" class="org.springframework.orm.hibernate5.LocalSessionFactoryBean">
    <property name="dataSource" ref="dataSource"/>
    <property name="mappingResources">
        <list>
            <value>org/springframework/samples/petclinic/hibernate/petclinic.hbm.xml</value>
        </list>
    </property>
    <property name="hibernateProperties">
        <value>
            hibernate.dialect=${hibernate.dialect}
        </value>
    </property>
</bean>

<bean id="txManager" class="org.springframework.orm.hibernate5.HibernateTransactionManager">
    <property name="sessionFactory" ref="sessionFactory"/>
</bean>
```

如果你使用 Hibernate 和 Java EE 容器管理的 JTA 事务，你应该使用与上面用于 JDBC 的 JTA 例子中相同的 `JtaTransactionManager` ，如下面例子所示：

````xml
<bean id="txManager" class="org.springframework.transaction.jta.JtaTransactionManager"/>
````

> 如果你使用 JTA，你的事务管理器定义应该看起来一样，无论你使用何种数据访问技术，JDBC，Hibernate JPA，或者任何其他支持的技术。这一点基于 JTA 事务是全局事务，因而可以管理任何事务性资源这一事实。

所有这些情况下，应用代码都不需要修改。你仅仅通过修改配置就可以改变事务管理，即使配置的修改意味着从局部事务切换到全局事务，或者相反。

## 1.3 将资源与事务同步

如何创建不同的事务管理器，如何将它们关联到相关的需要与事务保持同步的资源（比如 JDBC `DataSource` 的 `DataSourceTransactionManager` ，Hibernate `SessionFactory` 的 `HibernateTransactionManager` ，等等）链接起来，现在应该都清楚了。本节描述应用代码如何 (直接或者间接，通过使用持久化 API 比如 JDBC，Hibernate ，或者 JPA) 确保这些资源被合适地创建、复用以及清理。同时讨论如何通过相关的 `PlatformTransactionManager` 触发事务同步 (可选的)。

### 1.3.1 高级同步方式

首选的方式是使用基于 Spring 的顶级模版的持久化集成 APIs，或者使用本地 ORM APIs 和事务敏感的 beans 工厂，或者代理本地资源工厂的管理。这些事务敏感的解决方案内部处理资源创建和复用，清理，可选的资源的事务同步，以及异常映射等。因此，用户的数据访问代码不需要负责这些任务，只需要聚焦于核心的持久化逻辑。通常，你使用本地 ORM API 或者模版方式进行 JDBC 访问，通过使用 `JdbcTemplate` 。这些解决方案将在后续章节中详细介绍。

### 1.3.2 低级同步方式

诸如 `DataSourceUtils` (JDBC) ，`EntityManagerFactoryUtils` (JPA)，`SessionFactoryUtils` (Hibernate)，等等，存在于更低的层级。当你希望应用代码直接使用本地持久化 APIs 处理某些类型的资源，你可以使用这些类来确保合适的 Spring 框架管理的实例可获取，事务被同步(可选)，同时过程中发生的异常会被适当地映射到一致性 API。

例如，在 JDBC 的情况下，除了在 `DataSource` 上调用 `getConnection()` 方法这种传统 JDBC 方式之外，你可以使用 Spring 的 `org.springframework.jdbc.datasource.DataSourceUtils` 类，如下：

````java
Connection conn = DataSourceUtils.getConnection(dataSource);
````

如果现存的事务已经拥有了与之同步的连接，该连接实例会被返回。否则，该方法调用触发新的连接的创建，它 (可选地) 与任何现存的事务同步，同时对同一个事务中的后续复用是可用的。如前所述，任何 `SQLException` 都被包装为 Spring 框架的 `CannotGetJdbcConnectionException` ，这是一个 Spring 框架的不受检查的 `DataAccessException` 异常类型的类型体系的一员。这种方式使你可以获取相比从 `SQLException` 中获取的信息更多的信息，同时保证了跨数据库、甚至跨持久化技术的可能性。

这种方式不需要 Spring 事务管理 (事务同步是可选的)，因此无论是否使用 Spring 进行事务管理，你都可以使用这种方式。

当然，一旦你已经使用了 Spring 的 JDBC 支持，JPA 支持，或者 Hibernate 支持，你通常不会希望使用 `DataSourceUtils` 或者其他帮助类，因为你已经发现通过 Spring 的抽闲进行事务管理要比直接使用相关 APIs 要轻松愉快的多。比如，如果你的使用 Spring `JdbcTemplate` 或者 `jdbc.object` 包来简化你的 JDBC 使用，正确的连接检索在后台进行，而你不需要编写任何特定代码。

### 1.3.3 `TransactionAwareDataSourceProxy`

在最低层级的是 `TransactionAwareDataSourceProxy` 类。这是一个目标 `DataSource` 的代理，包装了目标 `DataSource` 以添加 Spring 管理的事务的敏感性。从这层面看，它类似于由 Java EE 服务器提供的传统的 JNDI `DataSource` 。

你可能永远不需要也不想要使用这个类，除非现存的代码必须传入一个标准的 JDBC `DataSource` 接口实现。那种情况下，这些代码可能可用，但参与了 Spring 管理的事务。您可以使用前面提到的高级抽象来编写新代码。

## 1.4 声明式事务管理

> 大部分 Spring 用户会选择声明式事务管理。这种方式可以最小程度地影响应用代码，因而，最符合非侵入式的轻量级容器理念。

Spring 框架的声明式事务管理基于 Spring 的面向切面编程 (AOP)。不过，由于传统的切面代码都随着 Spring 框架一起发布，而且通常以固定模版的方式使用，因而有效使用这些代码并不一定需要理解 AOP 的概念。

Spring 框架的声明式事务管理类似于 EJB CMT。你可以细粒度到方法级别为每个方法指定事务行为。如果有必要，你可以在事务上下文中进行 `setRollbackOnly()` 调用。这两种事务管理的区别在于：

* 不同于 EJB CMT 绑定到 JTA，Spring 框架的声明式事务管理可以在任何环境下工作。它可以使用 JTA 事务，或者通过调整配置文件，通过使用 JDBC，JPA，或者 Hibernate 来使用局部事务。

* 你可以将 Spring 框架的声明式事务管理应用于任何类，不仅仅是特定的类，比如 EJBs。
* Spring 框架提供了声明式[回滚规则](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative-rolling-back) ，该特性没有 EJB 等价物。Spring 同时提供了编程式和声明式的回滚规则支持。
* Spring 框架允许你通过使用 AOP 自定义事务性行为。比如，你可以在事务回滚的情况下插入自定义行为。你还可以随着事务性增强添加任意增强。使用 EJB CMT，你不能影响容器的事务管理，除了使用 `setRollbackOnly()`。
* Spring 框架没有支持跨远程调用的上下文中的事务传播，如顶层的应用服务器那样。如果你需要该特性，我们推荐你使用 EJB。然而，在使用该特性之前需要谨慎考虑，因为，正常情况下，我们不会希望事务跨越远程调用。

回滚规则的概念非常重要。它们允许你指定何种异常 (或者 `throwable`) 应该导致自动回滚。你可以声明式指定，在配置文件中，而不是以 Java 代码的形式。因此，尽管你可以在 `TransactionStatus` 对象上调用 `setRollbackOnly()` 方法来回滚当前事务，大部分情况下你可以指定一个规则，`MyApplicationException` 必须永远导致回滚。这样做的显著优势就是业务对象不会依赖事务基础设施。比如，典型地，它们不需要引入 Spring 事务 APIs 或者其他 Spring APIs。

尽管 EJB 容器的默认行为会在系统异常（通常是运行时异常）时自动回滚事务，但是 EJB CMT不会在应用程序异常（即 `java.rmi.RemoteException` 以外的已检查异常）下自动回滚事务。尽管 Spring 声明式事务管理的默认行为遵循 EJB 约定（仅针对未检查的异常会自动回滚），但自定义此行为通常很有用。

### 1.4.1 理解 Spring 框架的声明式事务实现

只告诉你用 `@Transactional` 注解修饰你的类，添加 `@EnableTransactionManagement` 到你的配置文件，就期望你能理解它们是如何工作的，显然是远远不够的。为了深入理解，本节解释在事务相关场景下的 Spring 框架声明式事务基础设施的内部工作原理。

掌握 Spring 框架的声明式事务支持的最重要的概念是：该支持是基于 [ AOP 代理](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-understanding-aop-proxies)  ，事务性增强由元数据（目前是 XML 或者基于注解）驱动。AOP 和事务性元数据的结合生成了一个 AOP 代理，该代理使用一个 `TransactionInterceptor` ，结合一个合适的 `PlatformTransactionManager` 实现，来驱动环绕方法调用的事务。

> Spring AOP 在 [the AOP section](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop) 中介绍。

下图展示了调用一个事务性代理上的方法的概念视图：

![tx](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/images/tx.png)

### 1.4.2 声明式事务的实现示例

考虑下面的借口和它的实现。这个例子使用了 `Foo` 和 `Bar` 类作为占位符，由此你可以专注于事务使用而不必关系特定的领域模型。为了达成示例的目的，`DefaultFooService` 类在每个实现的方法体中抛出 `UnsupportedOperationException` 实例是正确的。该行为允许你看到事务被创建，然后作为对 `UnsupportedOperationException` 实例的响应而被回滚。下面的代码展示了 `FooService` 接口：

````java
// the service interface that we want to make transactional

package x.y.service;

public interface FooService {

    Foo getFoo(String fooName);

    Foo getFoo(String fooName, String barName);

    void insertFoo(Foo foo);

    void updateFoo(Foo foo);

}
````

下面是该接口的实现示例：

````java
package x.y.service;

public class DefaultFooService implements FooService {

    public Foo getFoo(String fooName) {
        throw new UnsupportedOperationException();
    }

    public Foo getFoo(String fooName, String barName) {
        throw new UnsupportedOperationException();
    }

    public void insertFoo(Foo foo) {
        throw new UnsupportedOperationException();
    }

    public void updateFoo(Foo foo) {
        throw new UnsupportedOperationException();
    }

}
````

假定 `FooService` 接口的前面两个方法，`getFoo(String)` 以及 `getFoo(String, String)`，必须在只读语义的事务上下文中执行，另外的方法，`insertFoo(Foo)` 和 `updateFoo(Foo)` ，必须在读写语义的事务上下文中执行。下面的配置将在后续几个段落中解释：

````xml
<!-- from the file 'context.xml' -->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/tx
        https://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- this is the service object that we want to make transactional -->
    <bean id="fooService" class="x.y.service.DefaultFooService"/>

    <!-- the transactional advice (what 'happens'; see the <aop:advisor/> bean below) -->
    <tx:advice id="txAdvice" transaction-manager="txManager">
        <!-- the transactional semantics... -->
        <tx:attributes>
            <!-- all methods starting with 'get' are read-only -->
            <tx:method name="get*" read-only="true"/>
            <!-- other methods use the default transaction settings (see below) -->
            <tx:method name="*"/>
        </tx:attributes>
    </tx:advice>

    <!-- ensure that the above transactional advice runs for any execution
        of an operation defined by the FooService interface -->
    <aop:config>
        <aop:pointcut id="fooServiceOperation" expression="execution(* x.y.service.FooService.*(..))"/>
        <aop:advisor advice-ref="txAdvice" pointcut-ref="fooServiceOperation"/>
    </aop:config>

    <!-- don't forget the DataSource -->
    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
        <property name="driverClassName" value="oracle.jdbc.driver.OracleDriver"/>
        <property name="url" value="jdbc:oracle:thin:@rj-t42:1521:elvis"/>
        <property name="username" value="scott"/>
        <property name="password" value="tiger"/>
    </bean>

    <!-- similarly, don't forget the PlatformTransactionManager -->
    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <!-- other <bean/> definitions here -->

</beans>
````

检查上面的配置。它假定你希望是一个服务对象，`fooService` bean，成为事务性的。将要应用的事务语义被封装在 `<tx:advice/>` 定义中。该 `<tx:advice/>` 定义看起来就像是说：方法名以 `get` 开头的所有方法，都在只读事务上下文中执行，所有其他方法都在默认事务语义上下文中执行。`<tx:advice/>` 标签的 `transaction-manager` 属性被设定为 `PlatformTransactionManager` bean 的名字，该 bean 将驱动事务(这种情况下，就是 `txManager` bean)。

> 你可以忽略事务性增强 `<tx:advice/>` 中的 `transaction-manager` 属性，如果你希望写入其中的 `PlatformTransactionManager` 的名字就是 `transactionManager` 。如果该 `PlatformTransactionManager` bean 是任何其他名字，你就必须像上面例子那样显式使用 `transaction-manager` 属性。

`<aop:config/>` 定义可确保由 `txAdvice` bean定义的事务性增强在程序的适当位置执行。首先，定义一个切入点，该切入点与 `FooService` 接口（`fooServiceOperation`）中定义的任何操作的执行相匹配。然后，使用增强器将切入点与 `txAdvice` 关联。结果表明，在执行 `fooServiceOperation` 时，将运行由 `txAdvice` 定义的增强。

 `<aop:pointcut/>` 元素中定义的表达式是一个 AspectJ 切入点表达式。参考 [the AOP section](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop) 获取有关 Spring 中的切入点表达式的更多信息。

常见的情形是我们需要将整个的服务层都改为事务性的。最好的方式是修改该切入点表达式，匹配服务层中的所有操作。下面的例子展示了如何做：

````xml
<aop:config>
    <aop:pointcut id="fooServiceMethods" expression="execution(* x.y.service.*.*(..))"/>
    <aop:advisor advice-ref="txAdvice" pointcut-ref="fooServiceMethods"/>
</aop:config>
````

> 上面的例子中，假定你所有的服务接口都定义在 `x.y.service` 包中。参考 [the AOP section](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop) 获取更多细节。

现在，我们已经分析了配置，您可能会问自己：“所有这些配置实际上是做什么的？”

前面显示的配置用于创建事务代理围绕从 `fooService` bean 定义创建的对象。代理配置有事务增强，以便在代理上调用适当的方法时，根据与该方法相关联的事务配置，事务将被启动，挂起，标记为只读等。考虑下面的程序，该程序测试驱动前面展示的配置：

````java
public final class Boot {

    public static void main(final String[] args) throws Exception {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("context.xml", Boot.class);
        FooService fooService = (FooService) ctx.getBean("fooService");
        fooService.insertFoo (new Foo());
    }
}
````

运行上述程序的输出应类似于以下内容（为清晰起见，由 `DefaultFooService` 类的 `insertFoo(..)` 方法抛出的 `UnsupportedOperationException` 的 Log4J 输出和堆栈跟踪已被截断）：

````shell
<!-- the Spring container is starting up... -->
[AspectJInvocationContextExposingAdvisorAutoProxyCreator] - Creating implicit proxy for bean 'fooService' with 0 common interceptors and 1 specific interceptors

<!-- the DefaultFooService is actually proxied -->
[JdkDynamicAopProxy] - Creating JDK dynamic proxy for [x.y.service.DefaultFooService]

<!-- ... the insertFoo(..) method is now being invoked on the proxy -->
[TransactionInterceptor] - Getting transaction for x.y.service.FooService.insertFoo

<!-- the transactional advice kicks in here... -->
[DataSourceTransactionManager] - Creating new transaction with name [x.y.service.FooService.insertFoo]
[DataSourceTransactionManager] - Acquired Connection [org.apache.commons.dbcp.PoolableConnection@a53de4] for JDBC transaction

<!-- the insertFoo(..) method from DefaultFooService throws an exception... -->
[RuleBasedTransactionAttribute] - Applying rules to determine whether transaction should rollback on java.lang.UnsupportedOperationException
[TransactionInterceptor] - Invoking rollback for transaction on x.y.service.FooService.insertFoo due to throwable [java.lang.UnsupportedOperationException]

<!-- and the transaction is rolled back (by default, RuntimeException instances cause rollback) -->
[DataSourceTransactionManager] - Rolling back JDBC transaction on Connection [org.apache.commons.dbcp.PoolableConnection@a53de4]
[DataSourceTransactionManager] - Releasing JDBC Connection after transaction
[DataSourceUtils] - Returning JDBC Connection to DataSource

Exception in thread "main" java.lang.UnsupportedOperationException at x.y.service.DefaultFooService.insertFoo(DefaultFooService.java:14)
<!-- AOP infrastructure stack trace elements removed for clarity -->
at $Proxy0.insertFoo(Unknown Source)
at Boot.main(Boot.java:11)
````

### 1.4.3 回滚一个声明式事务

上一节概述了如何在应用程序中声明性地指定类（通常是服务层类）的事务性设置的基础。本节介绍如何以简单的声明方式控制事务的回滚。

指示 Spring Framework 的事务基础设施要回滚事务的推荐方法是从事务上下文中当前正在执行的代码抛出 `Exception`。 Spring Framework 的事务基础设施代码捕获所有未处理的 `Exception`，因为它在调用堆栈中逐层上浮，并确定是否将事务标记为回滚。

在默认配置下，Spring 框架的事务基础设施代码仅在运行时、未检查的异常情况下将事务标记为回滚。即，当抛出的异常是 `RuntimeException` 的实例或子类时。（默认情况下，`Error` 实例也会导致回滚）。从事务方法引发的已检查异常不会导致默认配置中的回滚。

您可以准确配置哪些异常类型将事务标记为回滚，包括已检查的异常。以下 XML 片段演示了如何为已检查的，特定于应用程序的异常类型配置回滚：

````xml
<tx:advice id="txAdvice" transaction-manager="txManager">
    <tx:attributes>
    <tx:method name="get*" read-only="true" rollback-for="NoProductInStockException"/>
    <tx:method name="*"/>
    </tx:attributes>
</tx:advice>
````

如果你不希望在抛出异常时事务被回滚，你也可以指定不回滚规则：下面的例子告诉 Spring 框架的事务基础设施即使有未处理的 `InstrumentNotFoundException` 也要提交当前事务：

````xml
<tx:advice id="txAdvice">
    <tx:attributes>
    <tx:method name="updateStock" no-rollback-for="InstrumentNotFoundException"/>
    <tx:method name="*"/>
    </tx:attributes>
</tx:advice>
````

当 Spring 框架的事务基础设施捕获到一个异常，就会参照配置的回滚规则去定是否应该把事务标记为回滚，最强的匹配规则生效。因此，在下面配置的情况下，除了 `InstrumentNotFoundException` 之外的所有异常都会导致当前事务的回滚。

````xml
<tx:advice id="txAdvice">
    <tx:attributes>
    <tx:method name="*" rollback-for="Throwable" no-rollback-for="InstrumentNotFoundException"/>
    </tx:attributes>
</tx:advice>
````

你也可以通过编程方式指定必需的回滚。尽管很简单，该过程是相当侵入式的，因而会讲你的代码绑定到 Spring 框架的事务基础设施。下面的例子展示了如何编程式指定必需的回滚。

````java
public void resolvePosition() {
    try {
        // some business logic...
    } catch (NoProductInStockException ex) {
        // trigger rollback programmatically
        TransactionAspectSupport.currentTransactionStatus().setRollbackOnly();
    }
}
````

强烈建议尽可能使用声明式回滚。如果确实需要，你也可以使用编程式回滚，但是在面对实现干净的基于 POJO 的体系结构时，它的用法就不那么理想了。

### 1.4.4 为不同的 Beans 配置不同的事务性语义

考虑这样的场景，你拥有大量的服务层对象，同时你希望为每个对象应用完全不同的事务性配置。你可以定义包含不同的 `pointcut` 和 `advice-ref` 属性值的不同的 `<aop:advisor/>` 元素来实现这一点。

作为比较，首先假定所有的服务层类都定义在同一个根 `x.y.service` 包中。为了将默认事务性配置应用到所有定义在这个包以及它的子包中，并且类名以 `Service` 结尾的类对应的 beans 上，你可以像下面这样编写配置文件：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/tx
        https://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <aop:config>

        <aop:pointcut id="serviceOperation"
                expression="execution(* x.y.service..*Service.*(..))"/>

        <aop:advisor pointcut-ref="serviceOperation" advice-ref="txAdvice"/>

    </aop:config>

    <!-- these two beans will be transactional... -->
    <bean id="fooService" class="x.y.service.DefaultFooService"/>
    <bean id="barService" class="x.y.service.extras.SimpleBarService"/>

    <!-- ... and these two beans won't -->
    <bean id="anotherService" class="org.xyz.SomeService"/> <!-- (not in the right package) -->
    <bean id="barManager" class="x.y.service.SimpleBarManager"/> <!-- (doesn't end in 'Service') -->

    <tx:advice id="txAdvice">
        <tx:attributes>
            <tx:method name="get*" read-only="true"/>
            <tx:method name="*"/>
        </tx:attributes>
    </tx:advice>

    <!-- other transaction infrastructure beans such as a PlatformTransactionManager omitted... -->

</beans>
````

下面的例子展示了如何为两个不同的 beans 配置完全不同的事务性设定：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/tx
        https://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <aop:config>

        <aop:pointcut id="defaultServiceOperation"
                expression="execution(* x.y.service.*Service.*(..))"/>

        <aop:pointcut id="noTxServiceOperation"
                expression="execution(* x.y.service.ddl.DefaultDdlManager.*(..))"/>

        <aop:advisor pointcut-ref="defaultServiceOperation" advice-ref="defaultTxAdvice"/>

        <aop:advisor pointcut-ref="noTxServiceOperation" advice-ref="noTxAdvice"/>

    </aop:config>

    <!-- this bean will be transactional (see the 'defaultServiceOperation' pointcut) -->
    <bean id="fooService" class="x.y.service.DefaultFooService"/>

    <!-- this bean will also be transactional, but with totally different transactional settings -->
    <bean id="anotherFooService" class="x.y.service.ddl.DefaultDdlManager"/>

    <tx:advice id="defaultTxAdvice">
        <tx:attributes>
            <tx:method name="get*" read-only="true"/>
            <tx:method name="*"/>
        </tx:attributes>
    </tx:advice>

    <tx:advice id="noTxAdvice">
        <tx:attributes>
            <tx:method name="*" propagation="NEVER"/>
        </tx:attributes>
    </tx:advice>

    <!-- other transaction infrastructure beans such as a PlatformTransactionManager omitted... -->

</beans>
````

### 1.4.5 `<tx:advice>` 设定

本节概述你可以使用 `<tx:advice>` 标签指定的各种事务性设定。默认的 `<tx:advice>` 设定为：

*  [propagation setting](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#tx-propagation) 是 `REQUIRED`。
* 隔离级别是 `DEFAULT` 。
* 事务是 读－写 式的。
* 事务的超时时间默认为底层的事务系统的默认超市时间，如果事务系统不支持超市，则为空。
* 任何 `RuntimeException` 触发回滚，而任何受检查的 `Exception` 不会。

你可以修改这些默认设定。下表概述了 `<tx:advice>` 和 `<tx:attributes>` 标签中包含的  `<tx:method>` 标签的各种属性值。

| Attribute         | Required? | Default    | Description                                                  |
| :---------------- | :-------- | :--------- | :----------------------------------------------------------- |
| `name`            | Yes       |            | 事务属性关联到的方法的名称。通配符 (\*) 字符可以被用来讲一个事务属性设定到多个方法 (比如， `get*`， `handle*`， `on*Event`， 等等). |
| `propagation`     | No        | `REQUIRED` | 事务传播行为。                                               |
| `isolation`       | No        | `DEFAULT`  | 事务隔离级别。仅仅适用于 `REQUIRED` 或者 `REQUIRES_NEW` 传播设定。 |
| `timeout`         | No        | -1         | 事务超时时间（秒）。仅仅适用于 `REQUIRED` 或者 `REQUIRES_NEW` 传播设定。 |
| `read-only`       | No        | false      | 读－写 与 只读 事务。仅仅适用于 `REQUIRED` 或者 `REQUIRES_NEW`. |
| `rollback-for`    | No        |            | 逗号分隔的可以触发回滚的 `Exception` 实例列表，比如  `com.foo.MyBusinessException,ServletException.` |
| `no-rollback-for` | No        |            | 逗号分隔的不会触发回滚的 `Exception` 实例列表，比如`com.foo.MyBusinessException,ServletException.` |

### 1.4.6 使用 `@Transactional`

除了基于 XML 的声明式事务配置，你还可以使用基于注解的方式。在 Java 源代码中直接声明事务语义让声明更加靠近受影响的代码。不存在过多耦合的危险，因为原本打算以事务方式使用的代码几乎总是以这种方式部署。

> 标准的 `javax.transaction.Tansactional` 注解被作为 Spring 自己的注解的插入式替代支持。请参考 JTA 1.2 文档获取更多细节。

最好举例说明 `@Transactional` 注解带来的易用性，下面的例子说明了这一点。考虑下面的类定义：

````java
// the service class that we want to make transactional
@Transactional
public class DefaultFooService implements FooService {

    Foo getFoo(String fooName);

    Foo getFoo(String fooName, String barName);

    void insertFoo(Foo foo);

    void updateFoo(Foo foo);
}
````

被用在类级别时，此注解表示被声明的类（以及它的子类）的所有方法默认都是事务性的。或者，每个方法可以被分别注解。注意，一个类级别的注解不会作用到类集成体系中的祖先，这种场景下，方法需要呗局部重新声明以便成为子类级别的注解的参与者。

当一个 POJO 类，比如上面定义为 Spring 上下文中的  bean 的类，你可以通过在 `@Configuration` 类中使用 `@EnableTransactionManagement` 注解来将该 bean 实例标记为事务性的。参考 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/transaction/annotation/EnableTransactionManagement.html) 获取更多细节。

在 XML 配置文件中，`<tx:annotation-driven/>` 标签提供了类似的便利性：

```xml
<!-- from the file 'context.xml' -->
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/tx
        https://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- this is the service object that we want to make transactional -->
    <bean id="fooService" class="x.y.service.DefaultFooService"/>

    <!-- enable the configuration of transactional behavior based on annotations -->
    <tx:annotation-driven transaction-manager="txManager"/><!-- a PlatformTransactionManager is still required --> 

    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <!-- (this dependency is defined somewhere else) -->
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <!-- other <bean/> definitions here -->

</beans>
```

> 你可以忽略 `<tx:annotation-driven/>` 标签中的 `transaction-manager` 属性，如果你希望写入其中的 `PlatformTransactionManager` 的名字就是 `transactionManager` 。如果你希望注入的 `PlatformTransactionManager` bean 是任何其他名字，你就必须像上面例子那样显式使用 `transaction-manager` 属性。

> 方法可见性和 `@Transactional` 
>
> 当你使用代理时，你应该仅仅将 `@Transactional` 注解应用于可见性为 public 的方法。如果你使用 `@Transactional` 注解了 protected、private 或者包可见方法，不会发生错误，但是被注解的方法并不会展示出配置的事务性设定。如果你需要注解非 public 方法，考虑使用 AspectJ (后面介绍)。

你可以将 `@Transactional` 注解应用于接口定义、接口中的方法、类定义、或者类中的 public 方法。不过，仅仅只有 `@Transactional` 注解并不足够触发事务性行为。`@Transactional` 注解仅仅是元数据，能够被一些`@Transactional` 敏感的运行时基础设施消费，这些基础设施能够使用这些元数据配置适当 beans 的事务性行为。在前面的例子中，`<tx:annotation-driven/>` 元素开启事务性行为。

> Spring 团队推荐你只将 `@Transactional` 注解应用于具体类(以及具体类的方法)，而不用于接口。你当然可以将用该注解修饰接口和接口方法，但是这样的注解就只有在你使用基于接口的代理时才会生效。Java 注解不会被从接口继承的事实意味着，如果你使用基于类对代理 (`proxy-target-class="true"`) 或者基于编织的切面 (`mode="aspect"`) ，代理或者编织基础设施就无法识别事务设定，该对象就不会被包装进入事务性代理。

> 在代理模式中 (默认情况)，只有通过代理进入的外部方法调用才会被拦截。这意味着自身调用 (也就是说，目标对象内部方法之间的互相调用) 在运行时就不会导致实际的事务，即使被调用的方法被 `@Transactional` 注解修饰。同时，该代理必须被完全初始化以提供期望的行为，因此你不应该依赖你的初始化代码（`@PostConstruct`）的这个特性。

如果你希望字调用同样被事务包装请考虑使用 AspectJ 模式 (参考下表中的 `mode` 属性)。这种情况下，首先是没有代理。其次，目标类被编织 (它的字节码被修改) ，`@Transactional` 行为被加入所有类型方法的运行时行为。

| XML Attribute         | Annotation Attribute                                         | Default                     | Description                                                  |
| :-------------------- | :----------------------------------------------------------- | :-------------------------- | :----------------------------------------------------------- |
| `transaction-manager` | N/A (see [`TransactionManagementConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/transaction/annotation/TransactionManagementConfigurer.html) javadoc) | `transactionManager`        | 使用的事务管理器的名称。只有当事务管理器的名称不是 `transactionManager` 时才是必需的。 |
| `mode`                | `mode`                                                       | `proxy`                     | 处理被注解的、将要被代理的 beans 的默认模式 (`proxy`) ，这些 beans 通过使用 Spring AOP 框架进行代理（符合前文所述的代理语义，仅仅作用于通过代理进入的方法调用）。另一种模式 (`aspectj`) 使用 Spring 的 AsprctJ 事务切面编织受影响的类，修改目标类的字节码，将事务应用于所有类型的方法调用。AspectJ 编织需要 `spring-aspects.jar` 在类路径上，同时需要启用加载时编织（或者编译期编织）。 (参考 [Spring configuration](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-aj-ltw-spring) 获取关于加载时编织设置的更多细节) |
| `proxy-target-class`  | `proxyTargetClass`                                           | `false`                     | 仅适用于 `proxy` 模式。控制为 `@Transactional` 注解修饰的类创建何种类型的事务性代理。如果 `proxy-target-class` 数据被设置为 `true`，则创建基于类的代理。如果 `proxy-target-class` 是 `false` 或者该属性被省略，则创建标准的 JDK 基于接口的代理。 (参考 [Proxying Mechanisms](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-proxying) 获取有关不同代理类型的更多信息。) |
| `order`               | `order`                                                      | `Ordered.LOWEST_PRECEDENCE` | 定义应用于 `@Transactional` 注解修饰的 beans 的事务增强的顺序。(更多关于 AOP 增强排序规则的信息，参考 [Advice Ordering](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-ataspectj-advice-ordering)) 没有特别制定顺序就意味着由 AOP 子系统决定增强的顺序。 |

> 处理 `@Transactional` 注解的默认增强模式是 `proxy`，它只允许拦截通过代理的方法调用。同一个类中的本地调用不能通过这种方式被拦截。需要更先进的拦截模式，考虑切换到 `aspectj` 模式并结合使用编译期或者加载期编织。

> `proxy-target-class` 属性控制为 `@Transactional` 注解修饰的类创建何种类型的事务性代理。如果 `proxy-target-class` 数据被设置为 `true`，则创建基于类的代理。如果 `proxy-target-class` 是 `false` 或者该属性被省略，则创建标准的 JDK 基于接口的代理。(参考 [[aop-proxying\]](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#aop-proxying) 获取跟多不同代理类型的讨论)

> `@EnableTransactionManagement` 和 `<tx:annotation-driven/>` 仅仅在它们自身被定义的应用上下文中寻找 beans 上的 `@Transactional` 。这就意味着，如果你为一个 `DispatchServlet` 在 `WebApplicationContext` 中配置了注解驱动，它只会检查你的 controllers 中的 `@Transactional` beans ，而不管你的 services 类。参考 [MVC](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web.html#mvc-servlet) 获取更多细节。

在评估方法的事务设置时，最派生（最细粒度）的位置优先。在下面的示例中，`DefaultFooService` 类在类级别使用只读事务的设置进行注解，但是同一类中 `updateFoo(Foo)` 方法上的 `@Transactional` 注解优先于类上定义的事务设置。

```java
@Transactional(readOnly = true)
public class DefaultFooService implements FooService {

    public Foo getFoo(String fooName) {
        // do something
    }

    // these settings have precedence for this method
    @Transactional(readOnly = false, propagation = Propagation.REQUIRES_NEW)
    public void updateFoo(Foo foo) {
        // do something
    }
}
```

##### `@Transactional` 设定

`@Transactional` 注解时一个元数据，用来指定一个接口，类或者方法必须拥有事务性语义 (比如，"当方法被调用时开启一个新的只读事务，阻塞任何现有事务")。默认的 `@Transactional` 注解设定如下：

- 传播设定是 `PROPAGATION_REQUIRED`。
- 隔离级别是 `ISOLATION_DEFAULT`。
- 事务是 读－写 的。
- 事务的超时时间默认是底层的事务系统的默认超时时间，如果底层事务系统不支持超时，则超时时间为空。
- 任何 `RuntimeException` 都会触发回滚，任何受检查的 `Exception` 不会。

你可以改变这些默认设定。下表概括了 `@Transactional` 注解的各种属性：

| Property                                                     | Type                                                         | Description                                                  |
| :----------------------------------------------------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| [value](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#tx-multiple-tx-mgrs-with-attransactional) | `String`                                                     | 可选限定词指定要使用的事务管理器。                           |
| [propagation](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#tx-propagation) | `enum`: `Propagation`                                        | 可选的传播设定。                                             |
| `isolation`                                                  | `enum`: `Isolation`                                          | 可选的隔离级别。仅仅应用于传播设置 `REQUIRED` 或者 `REQUIRES_NEW`。 |
| `timeout`                                                    | `int` (in seconds of granularity)                            | 可选的事务超时时间。仅仅应用于传播设置 `REQUIRED` 或者 `REQUIRES_NEW`。 |
| `readOnly`                                                   | `boolean`                                                    | 读－写 或者 只读 事务。仅仅适用于传播设置 `REQUIRED` 或者 `REQUIRES_NEW`。 |
| `rollbackFor`                                                | Array of `Class` objects, which must be derived from `Throwable.` | 可选的必须导致回滚的异常类型数组。                           |
| `rollbackForClassName`                                       | Array of class names. The classes must be derived from `Throwable.` | 可选的必须导致回滚的异常名称数组。                           |
| `noRollbackFor`                                              | Array of `Class` objects, which must be derived from `Throwable.` | 可选的绝对不能导致回滚的异常类型数组。                       |
| `noRollbackForClassName`                                     | Array of `String` class names, which must be derived from `Throwable.` | 可选的绝对不能导致回滚的异常名称数组。                       |

目前，你不能显式控制事务的名称，也就是出现在兼容的 (比如，WebLogic 事务监视器) 事务监视器上表示事务名称的 `name` ，同时会记录在日志输出中。对声明式事务，事务名称永远都是全限定类名 ＋ `.` + 事务性增强的方法名称。比如，如果 `BusinessService` 类的 `handlePayment(..)` 方法启动一个事务，该事务的名称将是 `com.example.BusinessService.handlePayment`。

##### `@Transactional` 的多个事务管理器

大多数的 Spring 应用只需要一个事务管理器，不过有时候你可能会在一个应用中需要多个相互独立的事务管理器。你可使用 `@Transactional` 的 `value` 属性可选地指定使用的 `PlatformTransactionManager` 的标示符。该标示符可以是事务管理器 bean 的名称或者限定符值。比如，使用限定符记号，你可以将下面的代码和应用上下文中声明的事务管理器 bean 结合起来：

```java
public class TransactionalService {

    @Transactional("order")
    public void setSomething(String name) { ... }

    @Transactional("account")
    public void doSomething() { ... }
}
```

下面是 bean 声明：

```xml
<tx:annotation-driven/>

    <bean id="transactionManager1" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        ...
        <qualifier value="order"/>
    </bean>

    <bean id="transactionManager2" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        ...
        <qualifier value="account"/>
    </bean>
```

这种情况下，`TransactionalService` 中的两个方法运行在独立的事务管理器下，通过 `order` 和 `account` 限定符区别。仍然使用默认的 `<tx:annotation-driven>` 目标 bean 名称，`TransactionManager` 。除非找到特殊限定的 `PlatformTransactionManager` bean。

##### 自定义快捷注解

如果你发现你在多个不同的方法上重复使用相同的 `@Transactional` 属性，[Spring’s meta-annotation support](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-meta-annotations) 允许你为特定的使用场景定义自定义的快捷注解。比如，考虑下面的注解定义：

```java
@Target({ElementType.METHOD, ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Transactional("order")
public @interface OrderTx {
}

@Target({ElementType.METHOD, ElementType.TYPE})
@Retention(RetentionPolicy.RUNTIME)
@Transactional("account")
public @interface AccountTx {
}
```

上面的注解允许我们如下重写上一节中的例子：

```java
public class TransactionalService {

    @OrderTx
    public void setSomething(String name) { ... }

    @AccountTx
    public void doSomething() { ... }
}
```

在上面的例子中，我们使用该语法定义事务管理器限定符，不过，我们还可以包含传播行为，回滚规则，超时时间，以及其他特性。

### 1.4.7 事务传播

本节描述 Spring 中的一些事务传播语义。注意，本节并不是真正地介绍事务传播，它仅仅是一些语义细节，而不关注 Spring 中实际的事务传播。

在 Spring 管理的事务中，注意区别逻辑事务和物理事务，以及事务传播设定应用于两者的不同。

##### 理解 `PROPAGATION_REQUIRED`

![tx prop required](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/images/tx_prop_required.png)

`PROPAGATION_REQUIRED` 强制执行一个物理事务，如果目前不存在事务，则是当前作用域内的局部事务，要么作为一个更大的作用域下的现有的外部事务的成员。这是通常分配给同一线程的调用栈（例如，委派给几种存储库方法的服务门面，所有基础资源都必须参与服务级事务）中的优良默认设置。

> 默认地，一个成员事务加入外部作用域的特性，静默地忽略局部的隔离级别、超时时间、或者只读标记(如果存在)。考虑切换事务管理器上的 `validateExisitingTransactions` 标记为 `true` ，如果你希望当成为不同隔离级别的现存事务的成员时隔离级别声明被拒绝。这种非宽容模式还拒绝只读不匹配项（即，内部读写事务试图参与只读外部作用域）。

当传播设定为 `PROPAGATION_REQUIRED`，为该设定应用到的每个方法创建逻辑事务作用域。每个这种逻辑事务作用域能够独立决定只回滚状态，因为外部事务作用域和内部事务作用域是逻辑独立的。在标准 `PROPAGATION_REQUIRED` 行为的情况下，所有这些作用域都被影射到相同的物理事务。因此一个内部事务作用域的只回滚标记会影响外部事务的实际提交。

不过，在内部事务作用域设定只回滚标记情况下，外部事务自身并未决定回滚，因此回滚(由内部事务作用域触发的)是不希望发生的。一个相应的 `UnexpectedRollbackException` 在这个时候被抛出。这是期望的行为，因而事务的调用着在事务没有正确提交情况下永远不会被误导而假定事务被正确提交。因此，如果一个内部事务(外部调用者不敏感)静默地将事务标记为只回滚，外部调用着仍然调用提交。外部调用着需要接受一个 `UnexpectedRollbackException` 来清楚地表示实际上发生了回滚。

##### 理解 `PROPAGATION_REQUIRES_NEW`

![tx prop requires new](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/images/tx_prop_requires_new.png)

`PROPAGATION_REQUIRES_NEW`，相对于 `PROPAGATION_REQUIRED`，永远为每个不同的事务作用域使用独立的物理事务，永远不参与外部作用的现有事务。这种编排情况下，基础资源事务时不同的，因此，可以独立地提交或者回滚。外部事务不会被内部事务的回滚状态或者在内部事务完成时立即释放锁影响。这样的独立内部事务也可以声明它自己的隔离级别、超时时间、以及制度设定等，而不集成外部事务的特性。

##### 理解 `PROPAGATION_NESTED`

`PROPAGATION_NESTED` 使用一个物理事务，拥有多个可以回滚到的保存点。这种部分回滚允许一个内部事务作用域为它自己的作用域触发回滚，而外部作用域可以继续执行它的物理事务，而不在乎某些操作已经回滚。这种设定典型地影射到 JDBC 保存点，因此只可以用于 JDBC 资源事务。参考 Spring 的 [`DataSourceTransactionManager`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jdbc/datasource/DataSourceTransactionManager.html)。

### 1.4.8 Advising Transactional Operations

假定你希望执行事务性操作的同时执行一些其他的基本剖析增强。如何在 `<tx:annotation-drivene/>` 上下文中做到这一点？

当你调用 `updateFoo(Foo)` 方法时，你希望看到下列行为：

- 配置的剖析切面启动。
- 事务性增强执行。
- 被增强的对象上的方法执行。
- 事务提交。
- 剖析切面报告整个事务性方法调用的额外执行时间。

> 本章节不专门解释 AOP 的任何细节 (除了它应用于事务) 。参考 [AOP](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop) 了解有关 AOP 配置和使用的更多细节。

下面的代码展示了前面讨论的简单的剖析切面：

```java
package x.y;

import org.aspectj.lang.ProceedingJoinPoint;
import org.springframework.util.StopWatch;
import org.springframework.core.Ordered;

public class SimpleProfiler implements Ordered {

    private int order;

    // allows us to control the ordering of advice
    public int getOrder() {
        return this.order;
    }

    public void setOrder(int order) {
        this.order = order;
    }

    // this method is the around advice
    public Object profile(ProceedingJoinPoint call) throws Throwable {
        Object returnValue;
        StopWatch clock = new StopWatch(getClass().getName());
        try {
            clock.start(call.toShortString());
            returnValue = call.proceed();
        } finally {
            clock.stop();
            System.out.println(clock.prettyPrint());
        }
        return returnValue;
    }
}
```

增强的顺序通过 `Ordered` 接口控制。有关增强顺序的完整细节，参考 [Advice ordering](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-ataspectj-advice-ordering) 。

下面的配置创建一个 `fooService` bean，拥有按照期望顺序应用于其上的剖析和事务性切面：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/tx
        https://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <bean id="fooService" class="x.y.service.DefaultFooService"/>

    <!-- this is the aspect -->
    <bean id="profiler" class="x.y.SimpleProfiler">
        <!-- execute before the transactional advice (hence the lower order number) -->
        <property name="order" value="1"/>
    </bean>

    <tx:annotation-driven transaction-manager="txManager" order="200"/>

    <aop:config>
            <!-- this advice will execute around the transactional advice -->
            <aop:aspect id="profilingAspect" ref="profiler">
                <aop:pointcut id="serviceMethodWithReturnValue"
                        expression="execution(!void x.y..*Service.*(..))"/>
                <aop:around method="profile" pointcut-ref="serviceMethodWithReturnValue"/>
            </aop:aspect>
    </aop:config>

    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
        <property name="driverClassName" value="oracle.jdbc.driver.OracleDriver"/>
        <property name="url" value="jdbc:oracle:thin:@rj-t42:1521:elvis"/>
        <property name="username" value="scott"/>
        <property name="password" value="tiger"/>
    </bean>

    <bean id="txManager" class="org.springframework.jdbc.datasource.DataSourceTransactionManager">
        <property name="dataSource" ref="dataSource"/>
    </bean>

</beans>
```

你可以通过类似方式配置任意数量的附加切面。

下面的示例创建与上面两个例子相同的设定，不过使用了纯 XML 的声明方式：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xmlns:tx="http://www.springframework.org/schema/tx"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/tx
        https://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <bean id="fooService" class="x.y.service.DefaultFooService"/>

    <!-- the profiling advice -->
    <bean id="profiler" class="x.y.SimpleProfiler">
        <!-- execute before the transactional advice (hence the lower order number) -->
        <property name="order" value="1"/>
    </bean>

    <aop:config>
        <aop:pointcut id="entryPointMethod" expression="execution(* x.y..*Service.*(..))"/>
        <!-- will execute after the profiling advice (c.f. the order attribute) -->

        <aop:advisor advice-ref="txAdvice" pointcut-ref="entryPointMethod" order="2"/>
        <!-- order value is higher than the profiling aspect -->

        <aop:aspect id="profilingAspect" ref="profiler">
            <aop:pointcut id="serviceMethodWithReturnValue"
                    expression="execution(!void x.y..*Service.*(..))"/>
            <aop:around method="profile" pointcut-ref="serviceMethodWithReturnValue"/>
        </aop:aspect>

    </aop:config>

    <tx:advice id="txAdvice" transaction-manager="txManager">
        <tx:attributes>
            <tx:method name="get*" read-only="true"/>
            <tx:method name="*"/>
        </tx:attributes>
    </tx:advice>

    <!-- other <bean/> definitions such as a DataSource and a PlatformTransactionManager here -->

</beans>
```

前面配置的结果是一个 `fooService` bean，拥有按照期望顺序应用于其上的剖析和事务性切面。如果你希望该剖析切面在方法调用方向上在事务性增强之后执行，同时在方法返回方向上在事务性增强之前执行，你可以互换剖析切面 bean 的 `order` 属性，让它高于事务性增强的排序值。

你可以通过类似方式配置附加切面。

### 1.4.9 通过 AspectJ 使用 `@Transactional` 

你也可以在 Spring 容器之外通过 AspectJ 切面来使用 Spring 框架的 `@Transactional` 支持。为了做到这一点，首先用 `@Transactional` 注解修饰你的类（并选择性修饰该类的方法），然后将你的应用链接 (编织) 到定义在 `spring-aspects.jar` 文件中的 `org.springframework.transaction.aspectJ.AnnotationTransactionAspect` 。你必须同时为该切面配置事务管理器。你可以使用 Spring 框架的 IoC 容器进行切面的依赖注入。配置事务管理切面的最简单方式就是使用 `<tx:annotation-driven/>` 元素并指定 `aspectJ` 的 `mode` 属性，如 [Using `@Transactional`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative-annotations) 中所述。由于我们这里关注的是在 Spring 容器之外运行的应用，我们向你展示如何通过编程方式做到这一点。

> 继续之前，你可能希望阅读 [Using `@Transactional`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative-annotations) 和 [AOP](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop) 。

下面的例子展示了如何创建事务管理器并配置 `AnnotationTransactionAspect` 来使用它：

```java
// construct an appropriate transaction manager
DataSourceTransactionManager txManager = new DataSourceTransactionManager(getDataSource());

// configure the AnnotationTransactionAspect to use it; this must be done before executing any transactional methods
AnnotationTransactionAspect.aspectOf().setTransactionManager(txManager);
```

> 当你使用该切面时，你必须用注解修饰实现类 (或者实现类的方法) ，而不是修饰该类实现的接口 (如果存在)。AspectJ 遵循 Java 语言的规则，接口上的注解是不会被继承的。

类上的 `@Transactional` 注解指定了类中所有 public 方法执行的默认事务语义。

类中方法上的 `@Transactional` 注解覆盖了类注解（如果存在）指定的默认事务语义。你可以注解任何方法，不必关心方法可见性。

为了将你的应用编织到 `AnnotationTransactionAspect` ，你必须要么使用 AspectJ 创建你的应用 (参考 [AspectJ Development Guide](https://www.eclipse.org/aspectj/doc/released/devguide/index.html) )，或者使用加载时编织。参考 [Load-time weaving with AspectJ in the Spring Framework](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#aop-aj-ltw) 了解有关使用 AspectJ 的加载时编织的讨论。

## 1.5. 编程式事务管理

Spring 框架提供了两种手段进行编程式事务管理，通过使用：

- `TransactionTemplate`
- 直接使用 `PlatformTransactionManager` 实现

Spring 团队通常推荐使用 `TransactionTemplate` 进行编程式事务管理。第二种方法类似于使用 JTA `UserTransaction` API，尽管异常处理有些麻烦。

### 1.5.1 使用 `TransactionTemplate`

`TransactionTemplate` 采用了类似于其它 Spring 模板的使用方式，比如 `JdbcTemplate`。它使用一个回调方法 (为了将应用代码从无聊的锁定和释放事务资源的工作中解脱出来) 使得代码成为意图驱动的，你的代码可以单纯地聚焦于处理业务需求。

> 如下面例子所示，使用 `TransactionTemplate` 绝对会将你绑定到 Spring 的事务基础设施和 APIs。在开发中是否使用编程式事务管理取决于你的需求，完全由你自己决定。

必须在事务上下文中执行的业务代码以及显式使用 `TransactionTemplate` 的代码组成了下一个例子。作为应用开发者，你可以编写 `TransactionCallback` 实现 (通常表现为匿名内部类) ，其中包含你需要在事务上下文中执行的代码。然后你可减奖你的自定义的 `TransactionCallback` 实例传入 `TransactionTemplate` 暴露出来的 `execute(..)` 方法。下面的例子展示了这个过程：

```java
public class SimpleService implements Service {

    // single TransactionTemplate shared amongst all methods in this instance
    private final TransactionTemplate transactionTemplate;

    // use constructor-injection to supply the PlatformTransactionManager
    public SimpleService(PlatformTransactionManager transactionManager) {
        this.transactionTemplate = new TransactionTemplate(transactionManager);
    }

    public Object someServiceMethod() {
        return transactionTemplate.execute(new TransactionCallback() {
            // the code in this method executes in a transactional context
            public Object doInTransaction(TransactionStatus status) {
                updateOperation1();
                return resultOfUpdateOperation2();
            }
        });
    }
}
```

如果不存在返回值，你可以使用便捷的 `TransactionCallbackWithoutResult` 类：

```java
transactionTemplate.execute(new TransactionCallbackWithoutResult() {
    protected void doInTransactionWithoutResult(TransactionStatus status) {
        updateOperation1();
        updateOperation2();
    }
});
```

回调中的代码能够回滚事务，通过调用给定的 `TransactionStatus` 对象上的 `setRollbackOnly()` 方法，如下：

```java
transactionTemplate.execute(new TransactionCallbackWithoutResult() {

    protected void doInTransactionWithoutResult(TransactionStatus status) {
        try {
            updateOperation1();
            updateOperation2();
        } catch (SomeBusinessException ex) {
            status.setRollbackOnly();
        }
    }
});
```

##### 指定事务设定

你可以在 `TransactionTemplate` 上指定事务设定 (比如传播模式，隔离级别，超时时间等等) ，通过编程方式或者配置文件。默认地，`TransactionTemplate` 实例拥有 [default transactional settings](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-declarative-txadvice-settings) 。下面的例子展示了编程方式自定义特定 `TransactionTemplate` 的事务设定：

```java
public class SimpleService implements Service {

    private final TransactionTemplate transactionTemplate;

    public SimpleService(PlatformTransactionManager transactionManager) {
        this.transactionTemplate = new TransactionTemplate(transactionManager);

        // the transaction settings can be set here explicitly if so desired
        this.transactionTemplate.setIsolationLevel(TransactionDefinition.ISOLATION_READ_UNCOMMITTED);
        this.transactionTemplate.setTimeout(30); // 30 seconds
        // and so forth...
    }
}
```

下面的例子展示了通过使用 Spring XML 配置文件使用一些自定义事务设定定义一个 `TransactionTemplate` ：

```xml
<bean id="sharedTransactionTemplate"
        class="org.springframework.transaction.support.TransactionTemplate">
    <property name="isolationLevelName" value="ISOLATION_READ_UNCOMMITTED"/>
    <property name="timeout" value="30"/>
</bean>"
```

然后你就可以将 `sharedTransactionTemplate` 注入到任意多个需要它的服务类中。

最后，`TransactionTemplate` 类实例时线程安全的，该实例中没有维护任何会话状态。不过，`TransactionTemplate` 实例维护了配置状态。因此，当多个类可能共享一个 `TransactionTemplate` 实例时，如果一个类需要使用包含不同设定的 `TransactionTemplate` (比如，不同的隔离级别)，你需要创建两个不同的 `TransactionTemplate` 实例。

### 1.5.2 使用 `PlatformTransactionManager`

你还可以直接使用 `org.springframework.transaction.PlatformTransactionManager` 管理你的事务。为了这样做，通过 bean 引用传递你使用的 `PlatformTransactionManager` 实现给你的 bean。然后，通过使用 `TransactionDefinition` 和 `TransactionStatus` 对象，你可以初始化事务，回滚，以及提交。下面的例子展示了这个过程：

```java
DefaultTransactionDefinition def = new DefaultTransactionDefinition();
// explicitly setting the transaction name is something that can be done only programmatically
def.setName("SomeTxName");
def.setPropagationBehavior(TransactionDefinition.PROPAGATION_REQUIRED);

TransactionStatus status = txManager.getTransaction(def);
try {
    // execute your business logic here
}
catch (MyException ex) {
    txManager.rollback(status);
    throw ex;
}
txManager.commit(status);
```

## 1.6 选择编程式还是声明式事务管理

仅当您执行少量事务操作时，编程式事务管理通常是一个好主意。例如，如果您的 Web 应用程序仅要求对某些更新操作进行事务处理，则可能不希望通过使用 Spring 或任何其他技术来设置事务代理。在这种情况下，使用 `TransactionTemplate` 可能是一个好方法。能够显式设置事务名称的方法也只能通过使用编程方法进行事务管理来完成。

另一方面，如果您的应用程序具有大量事务操作，则声明式事务管理通常是值得的。它使事务管理脱离业务逻辑，并且不难配置。当使用 Spring 框架而不是 EJB CMT 时，声明式事务管理的配置成本大大降低了。

## 1.7 事务绑定事件

在 Spring 4.2 中，事件监听器可以被绑定到事务的某个阶段。典型的例子是处理事务彻底完成时的事件。这样做使得事件的使用更加灵活，当当前事务的结果确实会影响到监听器时。

你可以使用 `@EventListener` 注解注册一个常规的事件监听器。如果你需要将它绑定到事务，使用 `@TransactionalEventListener` 。当你这么做时，该监听器就会被默认绑定到事务的提交阶段。

下面的例子展示了这个概念。假定某个组建发布一个订单创建事件，我们希望定义一个监听器，仅仅处理该事件一次，一旦该事件发布则表示订单创建事务已经提交成功。下面的例子展示了如何设置这样的事件监听器：

```java
@Component
public class MyComponent {

    @TransactionalEventListener
    public void handleOrderCreatedEvent(CreationEvent<Order> creationEvent) {
        ...
    }
}
```

`@TransactionalEventListener` 注解暴露了一个 `phase` 属性，允许你自定义该监听器应该绑定到事务的哪个阶段。有效的阶段有 `BEFORE_COMMIT`，`AFTER_COMMIT`(默认的)，`AFTER_ROLLBACK`，以及 `AFTER_COMPLETION`（笼统表示事务完成，提交或者回滚）。

如果没有事务在运行，监听器就完全不会被调用，因为我们不能遵循必需的语义。但是，你仍然可以通过将注解的 `fallbackExecution` 属性设定为 `true` 来覆盖该行为。

## 1.8 Application server-specific integration

Spring 的事务抽象基本上是与应用服务器无关的。此外，Spring 的 `JtaTransactionManager` 类 (可以有选择地执行 JNDI lookup 为了 JTA `UserTransaction` 和 `JtaTransactionManager` 对象) 自动探测后续类的位置，该位置不同应用服务器不尽相同。可以访问 JTA `TransactionManager` 允许增强事务语义－特别地，支持事务挂起。参考 [`JtaTransactionManager`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/transaction/jta/JtaTransactionManager.html) 文档获取更多细节。

Spring 的 `JtaTransactionManager` 是运行在 Java EE 应用服务器上的标准选择，被认为可以工作在所有常见服务器上。高级功能，比如事务挂起，也可以在许多服务器上的工作 (包括 GlassFish, JBoss, 以及 Geronimo) 而不需要任何特殊配置。不过，为了事务挂起和更多高级集成的完整支持，Spring 包含了为 WebLogic Server 和 WebSphere 专门提供的特殊适配器。这些适配器将在随后章节中讨论。

对标准场景来所，包含 WebLogic Server 和 WebSphere ，考虑使用方便的 `<tx:jta-transaction-manager/>` 配置元素。当配置该元素时，它会自动探测底层的服务器并选择该平台上最佳的可用事务管理器。这就意味着你不需要显式配置特定于服务器的适配器类 (接下来的章节中讨论)。它们是会被自动选择的，如果没有合适的选择，标准的 `JtaTransactionManager` 就会作为默认的降级后备。

### 1.8.1 IBM WebSphere

在 WebSphere 6.1.0.9 以及更高版本的服务器上，推荐使用的 Spring JTA 事务管理器是 `WebSphereUowTransactionManager` 。这个特殊的适配器使用 IBM 的 `UOWManager` API，它在 WebSphere Application Server 6.1.0.9 及更高版本上可用。使用该适配器，Spring 驱动的事务挂起 (挂起以及由 `PROPAGATION_REQUIRES_NEW` 恢复为初始化状态) 得到 IBM 的官方支持。

### 1.8.2 Oracle WebLogic Server

在 WebLogic Server 9.0 及更高版本服务器上，我们通常使用 `WebLogicJtaTransactionManager` 替代 `JtaTransactionManager` 类。这个特定于 WebLogic 的 `JtaTansactionManager` 类的子类在 WebLogic 管理的事务环境下支持 Spring 的事务定义的完整能力，而不仅限于标准的 JTA 语义。包含事务名称，每个事务的隔离级别，以及在所有情况下正确地恢复事务。

## 1.9 常见问题解决方案

本节描述一些常见问题的解决方案。

### 1.9.1 为特定 `DataSource` 使用错误的事务管理器

基于你的事务性技术选择和实际需求使用正确的 `PlatformTransactionManager` 实现。使用正确的情况下，Spring 框架仅仅提供直截了当和可移植的抽象。如果你使用全局事务，你必须使用 `org.springframework.transaction.jta.JtaTransactionManager` 类 (或者它的 [application server-specific subclass](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#transaction-application-server-integration) 的子类) 来执行所有事务性操作。否则，事务基础设施尝试在此类资源上执行局部事务，比如容器 `DataSource` 实例。此类局部事务没有意义，良好的应用服务器将它们当作是错误。

## 1.10 更多资源

有关 Spring 框架事务支持的更多信息，参考：

- [Distributed transactions in Spring, with and without XA](https://www.javaworld.com/javaworld/jw-01-2009/jw-01-spring-transactions.html) 是 JavaWorld 的一个演示，Spring 的 David Syer 指导您完成 Spring 应用程序中七个分布式事务模式，其中三个使用 XA，四个不使用 XA。
- [*Java Transaction Design Strategies*](https://www.infoq.com/minibooks/JTDS) 是 [InfoQ](https://www.infoq.com/) 上的一本书，其中提供了有关 Java 事务的详细介绍。 它还包括有关如何通过 Spring Framework 和 EJB3 配置和使用事务的端到端示例。

# 2 DAO 支持

Spring 中的数据访问对象(DAO)支持的目标是使得可以很简单地以一致的方法使用数据访问技术，比如 JDBC，Hibernate 或者 JPA。这就允许你可以相当容易地在上述持久化技术之间进行切换，还允许你的代码无需考虑捕获特定于每种技术的异常。

## 2.1 一致性异常体系

Spring 提供了一种从特定技术的异常，比如 `SQLException` 向它自己的异常类体系转化的方便方式。Spring 的标准数据访问异常体系以 `DataAccessException` 为根异常。这些异常包装原始的异常，因此你不会有丢失任何具体错误信息的风险。

除了 JDBC 异常，Spring 还可以包装特定于 JPA 和 Hibernate 的异常，将它们转化到一个运行时异常集合。这就允许你在合适的层次处理大部分的不可恢复持久化异常，而不需要在你的 DAOs 中添加大量的异常声明和异常处理代码（不过，你当然可以在你需要的地方自行处理异常）。如前所属，JDBC 异常(包括特定于数据库方言的异常)都被转化到相同的异常体系，这就意味着你可以在一致性的编程模型下之行一些 JDBC 操作。

上面的讨论同样适用于各种 Spring 对各种 ORM 框架提供的支持中的各种模版类。如果你使用基于拦截器的类，应用必须自行处理 `HibernateExceptions` 和 `PersistenceExceptions` ，而不是将该任务委托给 `SessionFactoryUtils` 的 `convertHibernateAccessException(..)` 或者 `convertJpaAccessException()` 方法。这些方法将初始异常转化为兼容 `org.springframework.dao` 异常体系的异常。因为 `PersistenceException` 是不受检查的，它们也可以被抛出(不过，在异常方面牺牲了通用 DAO 抽象)。

下图展示了 Spring 提供的异常体系。(请注意，图中详细描述的类层次结构仅显示整个 `DataAccessException` 层次结构的子集)

![DataAccessException](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/images/DataAccessException.png)

## 2.2 用于配置 DAO 或者 Repository 类的注解

保证你的数据访问对象或者仓库类提供异常转化的最好方法就是使用 `@Repository` 注解。该注解同时允许组件扫描支持发现并配置你的 DAOs 和仓库类，而不需要为它们提供 XML 配置文件入口。下面的例子展示了如何使用 `@Repository` 注解：

```java
@Repository 
public class SomeMovieFinder implements MovieFinder {
    // ...
}
```

任何需要访问持久化资源的 DAO 或者仓库类实现都依赖于所使用的持久化技术。比如，基于 JDBC 的仓库需要访问 JDBC `DataSource`，而基于 JPA 的仓库类需要访问 `EntityManager` 。实现这一点的最简单方式就是使用 `@Autowired`, `@Inject`, `@Resource` 或者 `@PersistenceContext` 注解之一进行资源的依赖注入。下面的例子用于 JPA 仓库类：

```java
@Repository
public class JpaMovieFinder implements MovieFinder {

    @PersistenceContext
    private EntityManager entityManager;

    // ...

}
```

如果你使用经典的 Hibernate APIs，你可以如下注入 `SessionFactory`：

```java
@Repository
public class HibernateMovieFinder implements MovieFinder {

    private SessionFactory sessionFactory;

    @Autowired
    public void setSessionFactory(SessionFactory sessionFactory) {
        this.sessionFactory = sessionFactory;
    }

    // ...

}
```

最后一个例子关于典型的 JDBC 支持。你已经在初始化方法中注入一个 `DataSource` ，然后你使用该 `DataSource` 创建 `JdbcTempalte` 及其他数据访问支持类(比如 `SimpleJdbcCall` )。下面的例子自动装配 `DataSource`：

```java
@Repository
public class JdbcMovieFinder implements MovieFinder {

    private JdbcTemplate jdbcTemplate;

    @Autowired
    public void init(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    // ...

}
```

> 有关如何配置应用程序上下文以利用这些注解的详细信息，请参见每种持久性技术的专门介绍。

# 3 使用 JDBC 访问数据

下表中概述的操作可能最好地显示了 Spring Framework JDBC 抽象提供的价值。该表显示了 Spring 负责哪些操作以及哪些操作是您的责任。

| 动作                           | Spring | You  |
| :----------------------------- | :----- | :--- |
| 定义连接参数                   |        | X    |
| 打开连接                       | X      |      |
| 指定 SQL 语句                  |        | X    |
| 声明参数并提供参数值           |        | X    |
| 准备并执行语句                 | X      |      |
| 设置循环便利结果集（如果存在） | X      |      |
| 处理每次迭代数据               |        | X    |
| 处理所有异常                   | X      |      |
| 处理事务                       | X      |      |
| 关闭连接，语句，以及结果集     | X      |      |

Spring 框架负责了所有 JDBC 中乏味的底层细节。

## 3.1 选择 JDBC 数据库访问方式

你可以在几种方法中选择一种来形成你的基本 JDBC 数据库访问逻辑。除了三种常用的 `JdbcTemplate` ，一种新的 `SimpleJdbcInsert` 和 `SimpleJdbcCall` 方法优化了数据库元数据，同时，RDBMS 对象风格使用了更加面向对象的方式，类似于 JDO 查询设计。一旦你开始使用这些方法，你还可以混合来自不同方法的功能特性。所有的这些方法都需要 JDBC 2.0 兼容的驱动，某些高级特性需求 JDBC 3.0 驱动。

- `JdbcTemplate` 是经典的和最流行的 Spring JDBC 方式。这是最底层的方式，其他所有方式内部都是使用 `JdbcTemplate` 。
- `NamedParameterJdbcTemplate` 包装 `JdbcTemplate` 以提供命名参数，来替代传统的 JDBC `?` 占位符。这种方式提供更好的可读性和易用性，尤其是当你在一条 SQL 语句中使用多个参数时。
- `SimpleJdbcInsert` 和 `SimpleJdbcCall` 优化数据库元数据以限制必要配置的数量。这种方式简化了编码，你只需要提供数据库表名称或者存储过程的名称，以及参数与数据库列名之间的映射关系。这种方式需要数据库提供充足的元数据信息。如果数据库无法提供必需的元数据，你就必须显式提供参数的配置。
- RDBMS 对象，包含 `MappingSqlQuery`，`SqlUpdate` 和 `StoredProcedure`，需要你在初始化你的数据访问层过程中创建可重用且线程安全的对象。此方式对 JDO 查询建模，你在其中定义了你的查询字符串，声明参数，并编译查询。一旦你这么做了，可执行方法就可以携带不同的参数值被调用多次。

## 3.2 包层级

Spring 框架的 JDBC 抽象框架由以下四个包组成：

- `core`:  `org.springframework.jdbc.core` 包含 `JdbcTemplate` 类以及它的各种回调接口，以及各种相关的类。子包 `org.springframework.jdbc.core.simple` 包含 `SimpleJdbcInsert` 和 `SimpleJdbcCall` 类。另一个子包 `org.springframework.jdbc.core.namedparam` 包含 `NamedParameterJdbcTemplate` 类和有关的支持类。参考 [Using the JDBC Core Classes to Control Basic JDBC Processing and Error Handling](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-core), [JDBC Batch Operations](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-advanced-jdbc) ，和 [Simplifying JDBC Operations with the `SimpleJdbc` Classes](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-simple-jdbc) 。
- `datasource`:  `org.springframework.jdbc.datasource` 包含一系列工具类，这些类简化了 `DataSource` 访问，并提供了各种简单的 `DataSource` 实现，你可以使用这些类进行测试或者在 Java EE 容器之外运行固定的 JDBC 代码。子包 `org.springfamework.jdbc.datasource.embedded` 提供了通过使用 Java 数据库引擎（HSQL，H2，以及 Derby）创建内置数据库的支持。参考 [Controlling Database Connections](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-connections) 和 [Embedded Database Support](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-embedded-database-support) 。
- `object`:  `org.springframework.jdbc.object` 包含表示 RDBMS 查询、更新、以及存储过程的线程安全的、可复用的对象。参考 [Modeling JDBC Operations as Java Objects](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-object)。这种方式由 JDO 建模，虽然查询返回的对象是与数据库断开连接的。这种 JDBC 的高级抽象依赖于 `org.springframework.jdbc.core` 包中的低级抽象。
- `support`:  `org.springframework.jdbc.support` 提供了 `SQLException` 转化功能以及一些工具类。JDBC 处理中抛出的异常呗转化为 `org.springframework.dao` 包中定义的异常。这就意味着使用 Spring JDBC 抽象层的代码不需要实现 JDBC 或者特定于 RDBMS 的异常处理。所有被转化的异常都是不受检查的，这样你就可以捕获可恢复异常的同时让其他异常传播给调用者。参考 [Using `SQLExceptionTranslator`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-SQLExceptionTranslator) 获取更多信息。

## 3.3 使用 JDBC 核心类控制基本 JDBC 处理和 Error 处理

本节涵盖如何使用 JDBC 核心类控制基本 JDBC 处理，包含错误处理。包括以下主题：

- [使用 `JdbcTemplate`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-JdbcTemplate)
- [使用 `NamedParameterJdbcTemplate`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-NamedParameterJdbcTemplate)
- [使用 `SQLExceptionTranslator`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-SQLExceptionTranslator)
- [运行语句](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-statements-executing)
- [运行查询](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-statements-querying)
- [更新数据库](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-updates)
- [检索自动生成的键](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-auto-generated-keys)

### 3.3.1 使用 `JdbcTemplate`

`JdbcTemplate` 是 JDBC 核心包中的核心类。它处理资源的创建和释放，帮助你避免常见错误，比如忘记关闭连接。它执行核心 JDBC 流程的基本任务 (比如语句创建和执行等) ，应用代码提供 SQL 并提取结果。`JdbcTemplate` 类：

- 运行 SQL 查询
- 更新语句和存储过程调用
- 在 `ResultSet` 实例上执行迭代器，提取返回的参数
- 捕获 JDBC 异常并将它们转化为范型的，携带更多信息的，定义在 `org.springframework.dao` 包中的异常。(参考 [Consistent Exception Hierarchy](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#dao-exceptions) )

当你的代码使用 `JdbcTemplate` 时，你只需要实现回调接口，给予它们清楚定义的契约。由 `JdbcTemplate` 给定 `Connection` 后，`PreparedStatementCreator` 回调接口创建一个准备语句，提供 SQL 和所有必需的参数。`CallableStatementCreator` 接口完整类似的操作，它创建可调用语句。`RowCallbackHandler` 即可从 `ResultSet` 中提取值。

你可以直接使用 `DataSource` 引用实例化 `JdbcTemplate` 并在 DAO 实现中使用，还可以将它配置到 Spring IoC 容器中，并将其作为 bean 引用提供给 DAOs。

> `DataSource` 应该始终被配置为 Spring IoC 容器中的 bean 。在第一种情况下该 bean 被直接提供给服务。第二种情况，它被提供给准备模板。

由此类发出的所有 SQL 都会被记录在 `DEBUG` 级别的日志中，位于对应于模板实例的全限定类名的类别下 (典型地，`JdbcTempalte` ，但是如果你使用了自定义的 `JdbcTemplate` 子类，则会有所不同)。

后续的章节提供了一些使用 `JdbcTemplate` 的例子。这些例子并没有展示 `JdbcTemplate` 暴露出来的所有功能。参考 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jdbc/core/JdbcTemplate.html) 获取更多信息。

##### 查询 (`SELECT`)

下面的查询获取一个关系中的行数：

```java
int rowCount = this.jdbcTemplate.queryForObject("select count(*) from t_actor", Integer.class);
```

下面的查询使用一个绑定变量：

```java
int countOfActorsNamedJoe = this.jdbcTemplate.queryForObject(
        "select count(*) from t_actor where first_name = ?", Integer.class, "Joe");
```

下面的查询寻找一个 `String` ：

```java
String lastName = this.jdbcTemplate.queryForObject(
        "select last_name from t_actor where id = ?",
        new Object[]{1212L}, String.class);
```

下面的查询查找并填充单独一个域对象：

```java
Actor actor = this.jdbcTemplate.queryForObject(
        "select first_name, last_name from t_actor where id = ?",
        new Object[]{1212L},
        new RowMapper<Actor>() {
            public Actor mapRow(ResultSet rs, int rowNum) throws SQLException {
                Actor actor = new Actor();
                actor.setFirstName(rs.getString("first_name"));
                actor.setLastName(rs.getString("last_name"));
                return actor;
            }
        });
```

下面的查询查找并填充一系列域对象：

```java
List<Actor> actors = this.jdbcTemplate.query(
        "select first_name, last_name from t_actor",
        new RowMapper<Actor>() {
            public Actor mapRow(ResultSet rs, int rowNum) throws SQLException {
                Actor actor = new Actor();
                actor.setFirstName(rs.getString("first_name"));
                actor.setLastName(rs.getString("last_name"));
                return actor;
            }
        });
```

如果上面的两个代码片段出现在同一个应用中，则可以删除两个 `RowMapper` 中的匿名内部类，并抽取它们到一个单独的类(典型地，一个 `static` 嵌套类) 而可以被所有需要的 DAO 方法引用。如下面的写法：

```java
public List<Actor> findAllActors() {
    return this.jdbcTemplate.query( "select first_name, last_name from t_actor", new ActorMapper());
}

private static final class ActorMapper implements RowMapper<Actor> {

    public Actor mapRow(ResultSet rs, int rowNum) throws SQLException {
        Actor actor = new Actor();
        actor.setFirstName(rs.getString("first_name"));
        actor.setLastName(rs.getString("last_name"));
        return actor;
    }
}
```

##### 更新 (`INSERT`, `UPDATE`, and `DELETE`) 

你可以使用 `update(..)` 方法来执行插入、更新、以及删除操作。参数值通常以变量参数或者对象数组的形式提供。

下面的例子插入一个新的数据实体：

```java
this.jdbcTemplate.update(
        "insert into t_actor (first_name, last_name) values (?, ?)",
        "Leonor", "Watling");
```

下面的例子更新一个已经存在的数据实体：

```java
this.jdbcTemplate.update(
        "update t_actor set last_name = ? where id = ?",
        "Banjo", 5276L);
```

下面的例子删除一个数据实体：

```java
this.jdbcTemplate.update(
        "delete from actor where id = ?",
        Long.valueOf(actorId));
```

##### 其他 `JdbcTemplate` 操作

你可以使用 `execute(..)` 方法执行任意 SQL。因此，该方法通常被用于 DDL 语句。它有各种增强变体，如携带回调接口，绑定变量数组等等。下面的例子创建一张表：

```java
this.jdbcTemplate.execute("create table mytable (id integer, name varchar(100))");
```

下面的例子调用一个存储过程：

```java
this.jdbcTemplate.update(
        "call SUPPORT.REFRESH_ACTORS_SUMMARY(?)",
        Long.valueOf(unionId));
```

更复杂的存储过程支持参考 [covered later](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-StoredProcedure) 。

##### `JdbcTemplate` 最佳实践

一旦被配置，`JdbcTemplate` 类实例就是线程安全的。这一点很重要，因为这意味着你可以仅配置一个 `JdbcTemplate` 实例然后安全地将其作为共享引用注入多个 DAOs 或者仓库类。`JdbcTemplate` 是有状态的，因为它维护了一个 `DataSource` 引用，不过这里的状态并不是传统意义上的状态。

常见的 `JdbcTemplate` 类（以及配合的 [`NamedParameterJdbcTemplate`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-NamedParameterJdbcTemplate) 类）的使用方法是在你的 Spring 配置文件中配置一个 `DataSource` 然后将该共享 `DataSource` bean 注入你的 DAO 类中。`JdbcTemplate` 在 `DataSource` 的设定器方法中被创建。这产生类似于以下内容的DAO：

```java
public class JdbcCorporateEventDao implements CorporateEventDao {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    // JDBC-backed implementations of the methods on the CorporateEventDao follow...
}
```

下面的例子展示对应的 XML 配置：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <bean id="corporateEventDao" class="com.example.JdbcCorporateEventDao">
        <property name="dataSource" ref="dataSource"/>
    </bean>

    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
        <property name="driverClassName" value="${jdbc.driverClassName}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

    <context:property-placeholder location="jdbc.properties"/>

</beans>
```

另一种显式配置的方法是使用组件扫描和依赖注入的注解支持。这种情况下，你可以使用 `@Repository` 注解修饰你的类(将该类标记为组件扫描的候选者)，并使用 `@Autowired` 注解修饰 `DataSource` 的设定器方法。下面的例子展示了这样的做法：

```java
@Repository 
public class JdbcCorporateEventDao implements CorporateEventDao {

    private JdbcTemplate jdbcTemplate;

    @Autowired 
    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource); 
    }

    // JDBC-backed implementations of the methods on the CorporateEventDao follow...
}
```

下面的例子展示了对应的 XML 配置：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <!-- Scans within the base package of the application for @Component classes to configure as beans -->
    <context:component-scan base-package="org.springframework.docs.test" />

    <bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
        <property name="driverClassName" value="${jdbc.driverClassName}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

    <context:property-placeholder location="jdbc.properties"/>

</beans>
```

如果你使用 Spring 的 `JdbcDaoSupport` 类，你的各种基于 JDBC 的 DAO 类都从它扩展而来，你的子类从 `JdbcDaoSupport` 类继承了 `setDataSource(..)` 方法。你可以选择是否继承该方法。 `JdbcDaoSupport` 类仅仅为方便而提供。

无论你选择使用上述何种模板初始化方式，你应该都不需要在每次执行 SQL 时创建一个新的 `JdbcTemplate` 类的实例。一旦配置，`JdbcTemplate` 实例就是线程安全的。如果你的应用访问多个数据库，你可能希望拥有多个 `JdbcTemplate` 实例，这就需要多个 `DataSource` ，进一步的，需要多个不同配置的 `JdbcTemplate` 实例。

### 3.3.2 使用 `NamedParameterJdbcTemplate`

 `NamedParameterJdbcTemplate` 类相对于传统的编程式 JDBC 语句仅仅使用占位符 `'?'` 参数，支持了编程式 JDBC 语句使用命名参数的支持。 `NamedParameterJdbcTemplate` 类包装了一个 `JdbcTemplate` 并将很多工作委托给该 `JdbcTemplate` 。本节仅仅描述了 `NamedParameterJdbcTemplate` 区别于 `JdbcTemplate` 本身的部分－也就是，在编程式 JDBC 语句中使用命名参数。下面的例子展示了如何使用 `NamedParameterJdbcTemplate` ：

```java
// some JDBC-backed DAO class...
private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

public void setDataSource(DataSource dataSource) {
    this.namedParameterJdbcTemplate = new NamedParameterJdbcTemplate(dataSource);
}

public int countOfActorsByFirstName(String firstName) {

    String sql = "select count(*) from T_ACTOR where first_name = :first_name";

    SqlParameterSource namedParameters = new MapSqlParameterSource("first_name", firstName);

    return this.namedParameterJdbcTemplate.queryForObject(sql, namedParameters, Integer.class);
}
```

注意命名参数记号在配置给 `sql` 变量的值中和插入 `namedParameters` 变量的相映的值（类型是 `MapSqlParameterSource`）中的使用。

或者，你可以使用基于 `Map` 的形式将命名参数和相应的值传入 `NamedParameterJdbcTemplate` 实例。 `NamedParameterJdbcOperations` 暴露出来并由 `NamedParameterJdbcTemplate` 类实现的其他方法遵循相似的模式，不在这里讨论。

下面的例子展示了基于 `Map` 形式的使用：

```java
// some JDBC-backed DAO class...
private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

public void setDataSource(DataSource dataSource) {
    this.namedParameterJdbcTemplate = new NamedParameterJdbcTemplate(dataSource);
}

public int countOfActorsByFirstName(String firstName) {

    String sql = "select count(*) from T_ACTOR where first_name = :first_name";

    Map<String, String> namedParameters = Collections.singletonMap("first_name", firstName);

    return this.namedParameterJdbcTemplate.queryForObject(sql, namedParameters,  Integer.class);
}
```

有关 `NamedParameterJdbcTemplate` （以及同一个 Java 包中的其他类）的一个很好的特性是 `SqlParameterSource` 接口。你已经看到过一个该接口的实现的示例(`MapSqlParameterJdbcTemplate` 类) 。一个 `SqlParameterSource` 是一个 `NamedParameterJdbcTemplate` 中命名参数值的来源。`MapSqlParameterSource` 类是一个实现，是一个 `java.util.Map` 的适配器，其中的键是参数名称而值是参数值。

另一个 `SqlParameterSource` 实现是 `BeanPropertySqlParameterSource` 类。这个类包装任意 JavaBean (也就是一个遵循 [the JavaBean conventions](https://www.oracle.com/technetwork/java/javase/documentation/spec-136004.html) 的类的实例)，并且使用该被包装的 JavaBean 的属性作为命名参数值的来源。

下面的例子展示了一个典型的 JavaBean：

```java
public class Actor {

    private Long id;
    private String firstName;
    private String lastName;

    public String getFirstName() {
        return this.firstName;
    }

    public String getLastName() {
        return this.lastName;
    }

    public Long getId() {
        return this.id;
    }

    // setters omitted...

}
```

下面的例子使用 `NamedParameterJdbcTemplate` 来返回前面例子中展示的类的成员的数量：

```java
// some JDBC-backed DAO class...
private NamedParameterJdbcTemplate namedParameterJdbcTemplate;

public void setDataSource(DataSource dataSource) {
    this.namedParameterJdbcTemplate = new NamedParameterJdbcTemplate(dataSource);
}

public int countOfActors(Actor exampleActor) {

    // notice how the named parameters match the properties of the above 'Actor' class
    String sql = "select count(*) from T_ACTOR where first_name = :firstName and last_name = :lastName";

    SqlParameterSource namedParameters = new BeanPropertySqlParameterSource(exampleActor);

    return this.namedParameterJdbcTemplate.queryForObject(sql, namedParameters, Integer.class);
}
```

记住， `NamedParameterJdbcTemplate` 类包装了一个经典的 `JdbcTemplate` 模版。如果你需要访问该包装的 `JdbcTemplate` 实例以访问只存在于该类中的功能，你可以使用 `getJdbcOperations()` 方法来通过 `JdbcOperations` 接口访问该包装的 `JdbcTemplate` 。

参考 [`JdbcTemplate` Best Practices](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-JdbcTemplate-idioms) 获取更多有关在应用上下文中使用 `NamedParameterJdbcTemplate` 类的指引。

### 3.3.3 使用 `SQLExceptionTranslator`

`SQLExceptionTranslator` 是一个接口，被那些可以将 `SQLExceptions` 转化为 Spring 自己的 `org.springframework.dao.DataAccessException` 的类实现，这些类并不了解数据访问策略。这些实现可以是宽泛的 (比如，使用 JDBC 的 SQLState 编码) 或者是更精确的 (比如，使用 Oracle 错误编码)。

`SQLErrorCodeSQLExceptionTranslator` 是默认使用的 `SQLExceptionTranslator` 实现。该实现使用特定的提供者 (vendor) 编码。它比 `SQLState` 实现更加精确。错误编码转换基于一个名为 `SQLErrorCodes` 的 JavaBean 类持有的编码。该类由 `SQLErrorCodesFactory` 创建并填充，该类 (顾名思义) 就是一个基于名为 `sql-error-codes.xml` 的配置文件的内容创建 `SQLErrorCodes` 的工厂。该文件基于提供者编码和来自 `DatabaseMetaData` 的 `DatabaseProductName` 填充。你正在使用的具体数据库的编码会被使用。

`SQLErrorCodeSQLExceptionTranslator` 按照下列顺序应用匹配的规则：

1. 由子类实现的所有自定义转换。通常，会使用提供的具体 `SQLErrorCodeSQLExceptionTranslator` ，因此本规则不会应用。本规则只有当你确实提供了一个子类实现时才会应用。
2. 被作为 `SQLErrorCodes` 类的 `customSqlExceptionTranslator` 属性提供的任何自定义 `SQLExceptionTranslator` 实现。
3. 为一个匹配搜索 `CustomSQLErrorCodesTranslation` 类实例列表 (作为 `SQLErrorCodes` 类的 `customTranslations` 属性提供) 。
4. 错误编码匹配被应用。
5. 使用降级的转换器。`SQLExceptionSubclassTranslator` 是默认的降级转换器。如果该转换器不可用，下一个降级转换器是 `SQLStateSQLExceptionTranslator` 。

> 默认使用 `SQLErrorCodesFactory` 来定义 `Error` 编码和自定义的异常转换。它们被从类路径下的名为 `sql-error-codes.xml` 的文件中查找，匹配到的 `SQLErrorCodes` 实例的位置基于来自所使用的数据库的元数据的数据库名称。

你可以扩展 `SQLErrorCodeSQLExceptionTranslator`，如下面例子所示：

```java
public class CustomSQLErrorCodesTranslator extends SQLErrorCodeSQLExceptionTranslator {

    protected DataAccessException customTranslate(String task, String sql, SQLException sqlex) {
        if (sqlex.getErrorCode() == -12345) {
            return new DeadlockLoserDataAccessException(task, sqlex);
        }
        return null;
    }
}
```

前面的例子中，特定的错误编码 (`-12345`) 被转换，其他的错误由默认的转换器实现转换。为了使用该自定义转换器，你必须通过方法 `setExceptionTranslator` 将其传递给 `JdbcTemplate` ，同时你必须使用该 `JdbcTemplate` 进行所有需要转换器的数据访问过程。下面的例子展示了如何使用自定义转换器：

```java
private JdbcTemplate jdbcTemplate;

public void setDataSource(DataSource dataSource) {

    // create a JdbcTemplate and set data source
    this.jdbcTemplate = new JdbcTemplate();
    this.jdbcTemplate.setDataSource(dataSource);

    // create a custom translator and set the DataSource for the default translation lookup
    CustomSQLErrorCodesTranslator tr = new CustomSQLErrorCodesTranslator();
    tr.setDataSource(dataSource);
    this.jdbcTemplate.setExceptionTranslator(tr);

}

public void updateShippingCharge(long orderId, long pct) {
    // use the prepared JdbcTemplate for this update
    this.jdbcTemplate.update("update orders" +
        " set shipping_charge = shipping_charge * ? / 100" +
        " where id = ?", pct, orderId);
}
```

数据源被传递给自定义转换器以便于在 `sql-error-codes.xml` 文件中查找错误编码。

### 3.3.4 运行语句

运行一条 SQL 语句只需要很少的代码。你需要一个 `DataSource` 和一个 `JdbcTemplate` ，包括连同后者一起提供的方便方法。下面的例子展示了创建一张新表的最小需求但是功能完备的类：

```java
import javax.sql.DataSource;
import org.springframework.jdbc.core.JdbcTemplate;

public class ExecuteAStatement {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public void doExecute() {
        this.jdbcTemplate.execute("create table mytable (id integer, name varchar(100))");
    }
}
```

### 3.3.5 运行查询

一些查询方法返回单独的一个值。为了从一行中检索特定值的数量，使用 `queryForObject(..)`。该方法将返回的 JDBC `Type` 转化为作为参数传入的 Java 类。如果类型转换不可用，则抛出 `InvalidDataAccessApiUsageException` 。下面的例子包含两个查询方法，一个用来查询一个 `int` ，另一个查询一个 `String` ：

```java
import javax.sql.DataSource;
import org.springframework.jdbc.core.JdbcTemplate;

public class RunAQuery {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public int getCount() {
        return this.jdbcTemplate.queryForObject("select count(*) from mytable", Integer.class);
    }

    public String getName() {
        return this.jdbcTemplate.queryForObject("select name from mytable", String.class);
    }
}
```

除了单个结果的查询方法，若干方法返回一个列表，其中每个实体都是查询返回的一行数据。最通用的方法是 `queryForList(..)` ，它返回一个 `List` ，其中每个元素都是包含每个表列的数据实体的 `Map` ，使用表列名作为键。如果你为上面例子添加一个查询所有行的列表的方法，可能如下所示：

```java
private JdbcTemplate jdbcTemplate;

public void setDataSource(DataSource dataSource) {
    this.jdbcTemplate = new JdbcTemplate(dataSource);
}

public List<Map<String, Object>> getList() {
    return this.jdbcTemplate.queryForList("select * from mytable");
}
```

返回的列表将被构造如下：

```
[{name=Bob, id=1}, {name=Mary, id=2}]
```

### 3.3.6 更新数据库

下面的例子根据某个主键更新某一字段值：

```java
import javax.sql.DataSource;
import org.springframework.jdbc.core.JdbcTemplate;

public class ExecuteAnUpdate {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public void setName(int id, String name) {
        this.jdbcTemplate.update("update mytable set name = ? where id = ?", name, id);
    }
}
```

在上面的例子中，SQL 语句中的占位符作为行参数。你可以传递变量或者对象数组作为该参数的值。因此，你应该将基本数据类型显式包装为相应的包装类，或者使用自动装箱。

### 3.3.7 检索自增键

一个 `update()` 便捷方法支持由数据库产生的主键的检索。这种支持是 JDBC 3.0 标准的一部分。参考规范文档 13.6 章节了解更多细节。该方法将 `PreparedStatementCreator` 作为它的第一个参数，这也是插入语句所需的特定方式。另外的参数是一个 `KeyHolder` ，包含从更新操作正确返回的产生的主键。创建合适的 `PreparedStatement` 没有标准的唯一方式 (解释为什么该方法签名会是这个样子) 。下面的例子在 Oracle 平台上运行，其他平台不一定可行。

```java
final String INSERT_SQL = "insert into my_test (name) values(?)";
final String name = "Rob";

KeyHolder keyHolder = new GeneratedKeyHolder();
jdbcTemplate.update(
    new PreparedStatementCreator() {
        public PreparedStatement createPreparedStatement(Connection connection) throws SQLException {
            PreparedStatement ps = connection.prepareStatement(INSERT_SQL, new String[] {"id"});
            ps.setString(1, name);
            return ps;
        }
    },
    keyHolder);

// keyHolder.getKey() now contains the generated key
```

## 3.4 控制数据库连接

本节涵盖：

- [使用 `DataSource`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-datasource)
- [使用 `DataSourceUtils`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-DataSourceUtils)
- [实现 `SmartDataSource`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-SmartDataSource)
- [扩展 `AbstractDataSource`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-AbstractDataSource)
- [使用 `SingleConnectionDataSource`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-SingleConnectionDataSource)
- [使用 `DriverManagerDataSource`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-DriverManagerDataSource)
- [使用 `TransactionAwareDataSourceProxy`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-TransactionAwareDataSourceProxy)
- [使用 `DataSourceTransactionManager`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-DataSourceTransactionManager)

### 3.4.1 使用 `DataSource`

Spring 通过 `DataSource` 获取数据库连接。`DataSource` 是 JDBC 规范的一部分，同时是一个通用的连接工厂。它允许容器或者框架向应用代码隐藏连接池和事务管理问题。作为开发者，你不需要了解数据库连接的具体细节。这是配置数据库的管理员的职责。你必须完成开发并测试代码的任务，但是你没有必要了解生产数据源是如何配置的。

当你使用 Spring 的 JDBC 层时，你可以从 JNDI 获取数据源，或者你可以配置第三方提供的连接池实现。流行的实现是 Apache Jakarta Commons DBCP 和 C3P0。Spring 发行版中的实现仅仅用于测试目的，并且没有提供池化实现。

本节使用 Spring 的 `DriverManagerDataSource` 实现，后续介绍另外几种实现。

> 你应该仅将 `DriverManagerDataSource` 类用于测试目的，因为它并未提供池化实现，因而当一个连接上到来多个请求时性能很差。

为了配置 `DriverManagerDataSource`：

1. 从 `DriverManagerDataSource` 获取一个连接，类似于你典型地获取一个 JDBC 连接那样。
2. 指定 JDBC 驱动的全限定类名以便于 `DriverManager` 可以加载该驱动类。
3. 提供一个特定于不同 JDBC 驱动的 URL。（参考你使用的驱动文档获取正确的值）
4. 提供用户名和密码以连接数据库。

下面的例子展示了如何在 Java 中配置 `DriverManagerDataSource` ：

```java
DriverManagerDataSource dataSource = new DriverManagerDataSource();
dataSource.setDriverClassName("org.hsqldb.jdbcDriver");
dataSource.setUrl("jdbc:hsqldb:hsql://localhost:");
dataSource.setUsername("sa");
dataSource.setPassword("");
```

下面的例子展示了对应的 XML 配置：

```xml
<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
    <property name="driverClassName" value="${jdbc.driverClassName}"/>
    <property name="url" value="${jdbc.url}"/>
    <property name="username" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>

<context:property-placeholder location="jdbc.properties"/>
```

下面两个例子展示了 DBCP 和 C3P0 的连接性和配置。为了学习更多选项以控制连接池特性，参考相应连接池实现的产品文档。

下面的例子展示了 DBCP 配置：

```xml
<bean id="dataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
    <property name="driverClassName" value="${jdbc.driverClassName}"/>
    <property name="url" value="${jdbc.url}"/>
    <property name="username" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>

<context:property-placeholder location="jdbc.properties"/>
```

下面的例子展示了 C3P0 配置：

```xml
<bean id="dataSource" class="com.mchange.v2.c3p0.ComboPooledDataSource" destroy-method="close">
    <property name="driverClass" value="${jdbc.driverClassName}"/>
    <property name="jdbcUrl" value="${jdbc.url}"/>
    <property name="user" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>

<context:property-placeholder location="jdbc.properties"/>
```

### 3.4.2 使用 `DataSourceUtils`

`DataSourceUtils` 类是一个方便而且强大的帮助类，提供了 `static` 方法来从 JNDI 获取连接，如果需要，关闭连接。它支持线程绑定的连接以及，例如，`DataSourceTransactionManager` 。

### 3.4.3 实现 `SmartDataSource`

`SmartDataSource` 接口应该被那些能够提供关系数据库连接的类实现。它扩展 `DataSource` 接口以允许使用它的类查询给定的操作完成之后连接是否应该被关闭。当你需要复用连接是这种用法的有效的。

### 3.4.4 扩展 `AbstractDataSource`

`AbstractDataSource` 是一个Spring 的 `DataSource` 实现的 `abstract` 基类。它实现了所有 `DataSource` 实现的通用部分。你应该扩展 `AbstractDataSource` 类，如果你编写自己的 `DataSource` 实现。

### 3.4.5 使用 `SingleConnectionDataSource`

`SingleConnectionDataSource` 类是 `SmartDataSource` 接口的实现，包装了一个使用后不会被关闭的 `Connection` 。但是不具有多线程能力。

如果任何客户端代码调用假想中的池化连接（与使用持久化工具时一样）上的 `close` 方法，你应该将 `suppressClose` 属性设定为 `true` 。该设定返回一个关闭压抑 (close-suppressing) 代理包装物理连接。注意，此时你就不再能够将其转化为一个原生的 Oracle `Connection` 或者类似的对象。

`SingleConnectionDataSource` 主要是一个测试类。比如，它允许在应用服务器之外，结合一个简单的 JNDI 环境方便地编写测试代码。相对于 `DriverManagerDataSource` ，它始终复用相同的连接，避免了物理连接的额外创建。

### 3.4.6 使用 `DriverManagerDataSource`

`DriverManagerDataSource` 类是标准 `DataSource` 接口的实现，该接口通过 bean 属性配置普通的 JDBC 驱动程序，并每次都返回一个新的 `Connection`。

此实现对于 Java EE 容器外部的测试和独立部署环境非常有用，可以作为 Spring IoC 容器中的 `DataSource` Bean或与简单的 JNDI 环境结合使用。假想池的 `Connection.close()` 调用会关闭连接，因此任何 `DataSource` 感知的持久性代码都应该起作用。然而，即使在测试环境中，使用 JavaBean 风格的连接池（例如 `commons-dbcp`）也是如此容易，以至于总是比在 `DriverManagerDataSource` 上使用这样的连接池更为可取。

### 3.4.7 使用 `TransactionAwareDataSourceProxy`

`TransactionAwareDataSourceProxy` 是目标 `DataSource` 的代理。该代理包装目标 `DataSource` 以添加 Spring 管理的事务的敏感性。这个层面上，它类似于 Java EE 服务器提供的事务性的 `DataSource` 。

> 很少需要使用此类，除非必须调用已经存在的代码并传入标准的 JDBC `DataSource` 接口实现。在这种情况下，您仍然可以使该代码可用，同时使该代码参与 Spring 托管的事务。通常最好使用更高级别的资源管理抽象来编写自己的新代码，例如 `JdbcTemplate` 或 `DataSourceUtils`。

参考 [`TransactionAwareDataSourceProxy`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jdbc/datasource/TransactionAwareDataSourceProxy.html) 文档获取更多细节。

### 3.4.8 使用 `DataSourceTransactionManager`

`DataSourceTransactionManager` 类是用于单个 JDBC 数据源的 `PlatformTransactionManager` 实现。它将 JDBC 连接从指定的数据源绑定到当前正在执行的线程，可能允许每个数据源一个线程连接。

应用程序代码需要通过 `DataSourceUtils.getConnection(DataSource)` 来检索 JDBC 连接，而不是 Java EE 的标准 `DataSource.getConnection` 。它抛出未经检查的 `org.springframework.dao` 异常，而不是`SQLExceptions` 。所有框架类（例如 `JdbcTemplate`）都隐式使用此策略。如果不与该事务管理器一起使用，则查找策略的行为与普通策略完全相同。因此，可以在任何情况下使用它。

`DataSourceTransactionManager` 类支持自定义隔离级别和超时，这些级别和超时将作为适当的 JDBC 语句查询超时而应用。为了支持后者，应用程序代码必须使用 `JdbcTemplate` 或为每个创建的语句调用 `DataSourceUtils.applyTransactionTimeout(..)` 方法。

在单资源情况下，您可以使用此实现代替 `JtaTransactionManager`，因为它不需要容器支持 JTA。您可以坚持需要的连接查找模式，因为在两者之间进行切换只是配置问题。JTA不支持自定义隔离级别。

## 3.5 JDBC 批量操作

大多数 JDBC 驱动提供更高的性能，如果你将多个调用合并为批量准备语句。通过将多个更新语句编组进入批量操作，你减少了通向数据库的往返路程。

### 3.5.1  `JdbcTemplate` 基本批量操作

你通过实现特定接口的两个方法来实现 `JdbcTemplate` 批量处理，`BatchPreparedStatementSetter`，同时将该实现作为你的 `batchUpdate` 方法调用的第二个参数。你可以使用 `getBatchSize` 方法来提供当前批量的尺寸。你可以使用 `setValues` 方法来设定准备语句的参数值。该方法被调用的次数就是你在 `getBatchSize` 调用中指定的值。下面的例子基于一个列表中的实体来更新 `actor` 表，实体列表用于批量操作：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public int[] batchUpdate(final List<Actor> actors) {
        return this.jdbcTemplate.batchUpdate(
                "update t_actor set first_name = ?, last_name = ? where id = ?",
                new BatchPreparedStatementSetter() {
                    public void setValues(PreparedStatement ps, int i) throws SQLException {
                        ps.setString(1, actors.get(i).getFirstName());
                        ps.setString(2, actors.get(i).getLastName());
                        ps.setLong(3, actors.get(i).getId().longValue());
                    }
                    public int getBatchSize() {
                        return actors.size();
                    }
                });
    }

    // ... additional methods
}
```

如果你处理一个更新或者读取文件的流，你可能有偏好的批量处理尺寸，不过最后一次的批量操作可能没有足够数量的实体。这种情况下，你可以使用 `InterruptibleBatchPreparedStatementSetter` 接口，它允许你打断批量处理，一旦输入数据耗尽。`isBatchExhausted` 方法允许你标记批量操作的结束。

### 3.5.2 对象列表的批量操作

`JdbcTemplate` 和 `NamedParameterJdbcTemplate` 都提供了不同的方法用来进行批量更新。不同于实现特定的批量接口，你在方法调用中使用一个列表提供所有的参数值。该框架遍历这些值并使用一个内部的准备语句设定器方法。不同的 API，取决于你是否使用命名参数。为了命名参数，你提供一个 `SqlParameterSource` 数组，数组中的实体就是批量处理的成员。你可以使用方便方法 `SqlParameterSourceUtils.createBatch` 创建这样的数组，将其作为 bean 形式的对象（携带对应于参数的 getter 方法），或者键为 `String` 的 `Map` 实例（包含对应的参数作为的值）的数组进行传递，或者两者混合使用。

下面的例子展示了使用命名参数的批量更新：

```java
public class JdbcActorDao implements ActorDao {

    private NamedParameterTemplate namedParameterJdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.namedParameterJdbcTemplate = new NamedParameterJdbcTemplate(dataSource);
    }

    public int[] batchUpdate(List<Actor> actors) {
        return this.namedParameterJdbcTemplate.batchUpdate(
                "update t_actor set first_name = :firstName, last_name = :lastName where id = :id",
                SqlParameterSourceUtils.createBatch(actors));
    }

    // ... additional methods
}
```

对于使用经典的 `?` 占位符的 SQL 语句，你传入一个包含携带更新值的对象数组。该对象数组必须为 SQL 语句中每个占位符提供一个数据实体，而且它们必须遵循它们在 SQL 语句中定义的顺序。

下面的例子与之前的例子相同，处理它使用了经典的 JDBC `?` 占位符：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public int[] batchUpdate(final List<Actor> actors) {
        List<Object[]> batch = new ArrayList<Object[]>();
        for (Actor actor : actors) {
            Object[] values = new Object[] {
                    actor.getFirstName(), actor.getLastName(), actor.getId()};
            batch.add(values);
        }
        return this.jdbcTemplate.batchUpdate(
                "update t_actor set first_name = ?, last_name = ? where id = ?",
                batch);
    }

    // ... additional methods
}
```

我们前面介绍的所有批处理更新方法都返回一个 `int` 数组，其中包含每个批处理条目的受影响行数。此计数由 JDBC 驱动程序报告。如果该计数不可用，则 JDBC 驱动程序将返回值 `-2`。

> 在这种情况下，通过基础 `PreparedStatement` 上的自动设定，需要从给定的 Java 类型派生每个值的对应 JDBC 类型。尽管这通常效果很好，但是存在潜在的问题（例如，`Map` 包含的 `null` 值）。在这种情况下，Spring 默认情况下会调用 `ParameterMetaData.getParameterType`，这对于您的 JDBC 驱动程序可能会相当费用高昂。如果遇到以下情况，则应使用最新的驱动程序版本，并考虑将 `spring.jdbc.getParameterType.ignore` 属性设置为 `true`（作为 JVM 系统属性或在类路径根目录中的 `spring.properties` 文件中）。性能问题-例如，关于Oracle 12c（SPR-16139）的报告。
>
> 或者，您可以考虑通过 `BatchPreparedStatementSetter`（如前所示），通过为基于 `List<Object[]>` 的调用提供的显式类型数组，通过在服务器上的 `registerSqlType` 调用来显式指定相应的 JDBC 类型。自定义 `MapSqlParameterSource` 实例，或者通过 `BeanPropertySqlParameterSource` 实例从 Java 声明的属性类型中获取 SQL 类型，即使对于 `null` 值也是如此。

### 3.5.3 多个批量的批量操作

前面的批处理更新示例处理的批处理过大，您想将它们分解成几个较小的批处理。您可以通过多次调用 `batchUpdate` 方法来使用前面提到的方法来执行此操作，但是现在有了一个更方便的方法。除了 SQL 语句外，此方法还包含对象的 `Collection` ，其中包含参数，每个批处理要进行的更新次数以及 `ParameterizedPreparedStatementSetter` 来设置准备语句的参数值。框架遍历提供的值，并将更新调用分成指定大小的批处理。

下面的例子展示了使用批量尺寸为 100  的批量更新：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    public int[][] batchUpdate(final Collection<Actor> actors) {
        int[][] updateCounts = jdbcTemplate.batchUpdate(
                "update t_actor set first_name = ?, last_name = ? where id = ?",
                actors,
                100,
                new ParameterizedPreparedStatementSetter<Actor>() {
                    public void setValues(PreparedStatement ps, Actor argument) throws SQLException {
                        ps.setString(1, argument.getFirstName());
                        ps.setString(2, argument.getLastName());
                        ps.setLong(3, argument.getId().longValue());
                    }
                });
        return updateCounts;
    }

    // ... additional methods
}
```

这里调用的批处理更新方法返回一个 `int` 数组，其中包含每个批处理的数组条目以及每次更新受影响的行数的数组。顶层数组的长度指示已执行的批处理数量，第二层数组的长度指示该批处理中的更新数量。每个批次中的更新数量应该是为所有批次提供的批次大小（最后一个可能更少），这取决于所提供的更新对象的总数。每个更新语句的更新计数是 JDBC 驱动程序报告的计数。如果该计数不可用，则 JDBC 驱动程序将返回值 `-2`。

## 3.6 使用 `SimpleJdbc` 类简化 JDBC 操作

得益于可以通过 JDBC 检索得到的数据库元数据的优点， `SimpleJdbcInsert` 和 `SimpleJdbcCall` 类提供了简化的配置。这就意味着你需要的配置更好。不过，你当然可以关闭这种元数据处理，如果你希望在你的代码中配置所有细节。

### 3.6.1 使用 `SimpleJdbcInsert` 插入数据

首先，我们查看具有最少配置选项的 `SimpleJdbcInsert` 类。你应该在数据访问层的实例化方法中实例化 `SimpleJdbcInsert` 。对本示例而言，初始化方法就是 `setDataSource` 。你不需要子类化 `SimpleJdbcInsert` 类，相反，你可以创建一个新的实例并使用 `withTableName` 方法设定表名。这个类的配置方法遵循 `fluid` 风格，返回 `SimpleJdbcInsert` 实例，它允许你串联起所有的配置方法。下面的例子只使用一个配置方法，稍后我们将展示使用多个方法的例子。

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;
    private SimpleJdbcInsert insertActor;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
        this.insertActor = new SimpleJdbcInsert(dataSource).withTableName("t_actor");
    }

    public void add(Actor actor) {
        Map<String, Object> parameters = new HashMap<String, Object>(3);
        parameters.put("id", actor.getId());
        parameters.put("first_name", actor.getFirstName());
        parameters.put("last_name", actor.getLastName());
        insertActor.execute(parameters);
    }

    // ... additional methods
}
```

这里使用的 `execute` 方法采用普通的 `java.util.Map` 作为它唯一的参数。这里需要注意的重要的事情是，使用的 `Map` 的键必须匹配定义在数据库中的表的列名。这是因为我们读取元数据来构造实际的插入语句。

### 3.6.2 使用 `SimpleJdbcInsert` 检索自动生成的键

下一个例子使用相同的插入语句，不同的是，不是传入 `id` ，它检索自动生成的主键并将它设置到新的 `Actor` 对象上。当它创建 `SimpleJdbcInsert` 时，除了指定表名，它还通过 `usingGeneratedKeyColumns` 方法指定产生主键列名。下面的例子展示了如何做：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;
    private SimpleJdbcInsert insertActor;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
        this.insertActor = new SimpleJdbcInsert(dataSource)
                .withTableName("t_actor")
                .usingGeneratedKeyColumns("id");
    }

    public void add(Actor actor) {
        Map<String, Object> parameters = new HashMap<String, Object>(2);
        parameters.put("first_name", actor.getFirstName());
        parameters.put("last_name", actor.getLastName());
        Number newId = insertActor.executeAndReturnKey(parameters);
        actor.setId(newId.longValue());
    }

    // ... additional methods
}
```

使用第二种方法运行插入的主要区别在于，您没有将 `id` 添加到 `Map` 中，而是调用了 `executeAndReturnKey` 方法。这将返回一个 `java.lang.Number` 对象，您可以使用该对象创建域类中使用的数字类型的实例。您不能依赖所有数据库在这里返回特定的 Java 类。`java.lang.Number` 是您可以依赖的基类。如果您有多个自动生成的列或生成的值是非数字的，则可以使用从 `executeAndReturnKeyHolder` 方法返回的 `KeyHolder`。

### 3.6.3 为 `SimpleJdbcInsert` 指定列名

你可以使用 `usingColumns` 方法指定列名列表来限制一条插入语句的列，如下面例子所示：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;
    private SimpleJdbcInsert insertActor;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
        this.insertActor = new SimpleJdbcInsert(dataSource)
                .withTableName("t_actor")
                .usingColumns("first_name", "last_name")
                .usingGeneratedKeyColumns("id");
    }

    public void add(Actor actor) {
        Map<String, Object> parameters = new HashMap<String, Object>(2);
        parameters.put("first_name", actor.getFirstName());
        parameters.put("last_name", actor.getLastName());
        Number newId = insertActor.executeAndReturnKey(parameters);
        actor.setId(newId.longValue());
    }

    // ... additional methods
}
```

插入的执行与依靠元数据确定要使用的列的执行相同。

### 3.6.4 使用 `SqlParameterSource` 提供参数值

使用 `Map` 提供参数值很好，但是并不是最方便的用法。Spring 提供了 `SqlParameterSource` 接口的两种实现，你也可以使用。第一种是 `BeanPropertySqlParameterSource` ，如果你用一个 JavaBean 兼容的类来装载你的参数值，这种实现将很方便。它使用相应的 `getter` 方法提取参数值。下面的例子展示了如何使用：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;
    private SimpleJdbcInsert insertActor;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
        this.insertActor = new SimpleJdbcInsert(dataSource)
                .withTableName("t_actor")
                .usingGeneratedKeyColumns("id");
    }

    public void add(Actor actor) {
        SqlParameterSource parameters = new BeanPropertySqlParameterSource(actor);
        Number newId = insertActor.executeAndReturnKey(parameters);
        actor.setId(newId.longValue());
    }

    // ... additional methods
}
```

另一种选择是 `MapSqlParameterSource` ，组装一个 `Map` 并提供了更加方便的 `addValue` 方法，该方法可以链式调用。下面的例子展示了如何使用：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;
    private SimpleJdbcInsert insertActor;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
        this.insertActor = new SimpleJdbcInsert(dataSource)
                .withTableName("t_actor")
                .usingGeneratedKeyColumns("id");
    }

    public void add(Actor actor) {
        SqlParameterSource parameters = new MapSqlParameterSource()
                .addValue("first_name", actor.getFirstName())
                .addValue("last_name", actor.getLastName());
        Number newId = insertActor.executeAndReturnKey(parameters);
        actor.setId(newId.longValue());
    }

    // ... additional methods
}
```

如你所见，两种方式的配置是相同的。唯一不同的可执行代码是输入类型的不同。

### 3.6.5 使用 `SimpleJdbcCall` 调用存储过程

`SimpleJdbcCall` 类使用数据库中的元数据来查找 `in` 和 `out` 参数的名称，因此你不需要显式声明它们。如果你喜欢，仍然可以显式声明它们，或者你的参数 (比如 `ARRAY` 或者 `STRUCT`) 无法自动影射到 Java 类。下面的第一个累字展示了一个简单的存储过程，从 MySQL 数据库返回 `VARCHAR` 和 `DATE` 格式的标量值。示例存储过程读取特定 actor 实体并以 `out` 参数的形式返回 `first_name`，`last_name`，以及 `birth_date` 列。下面的列表展示了第一个例子：

```sql
CREATE PROCEDURE read_actor (
    IN in_id INTEGER,
    OUT out_first_name VARCHAR(100),
    OUT out_last_name VARCHAR(100),
    OUT out_birth_date DATE)
BEGIN
    SELECT first_name, last_name, birth_date
    INTO out_first_name, out_last_name, out_birth_date
    FROM t_actor where id = in_id;
END;
```

`in_id` 参数包含你寻找的 actor 的 `id` 。`out` 参数返回从表里读取的数据。

你可以像声明 `SimpleJdbcInsert` 那样声明 `SimpleJdbcCall` 。你应该在你的数据访问层的实例化方法中实例化并配置该类。相比于 `StoredProcedure` 类，你不需要创建子类，也不需要声明那些可以在数据库元数据中找到的参数。下面的 `SimpleJdbcCall` 配置的例子使用了上面的存储过程(其中仅有的配置选项，除了 `DataSource` ，另外一个就是存储过程的名称)：

```java
public class JdbcActorDao implements ActorDao {

    private JdbcTemplate jdbcTemplate;
    private SimpleJdbcCall procReadActor;

    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
        this.procReadActor = new SimpleJdbcCall(dataSource)
                .withProcedureName("read_actor");
    }

    public Actor readActor(Long id) {
        SqlParameterSource in = new MapSqlParameterSource()
                .addValue("in_id", id);
        Map out = procReadActor.execute(in);
        Actor actor = new Actor();
        actor.setId(id);
        actor.setFirstName((String) out.get("out_first_name"));
        actor.setLastName((String) out.get("out_last_name"));
        actor.setBirthDate((Date) out.get("out_birth_date"));
        return actor;
    }

    // ... additional methods
}
```

你用来执行该调用的代码涉及到创建一个包含 IN 参数的 `SqlParameterSource` 。你必须匹配给定的输入值的名称到在存储过程中声明的参数名称。如果你使用元数据确定数据库对象应该如何对应到存储过程，则不需要这个匹配过程。源中为存储过程指定的内容不一定是存储过程在数据库中存储的方式。某些数据库将所有名称都转换为大写，有些使用小写，还有的使用指定的本来形式。

`execute` 方法使用 IN 参数并返回包含所有 `out` 参数的 `Map` ，其中参数名称为影射的键，如存储过程中指定的那样。这种情况下，它们是 `out_first_name`，`out_last_name`，和 `out_birth_date`。

`execute` 方法的最后一部分创建一个 `Actor` 实例，使用数据检索返回的数据。再一次地，使用 `out` 参数在存储过程中声明的名称是很重要的。同样，结果映射中存储的 `out` 参数名称的大小写与数据库中`out`参数名称的大小写匹配，这在不同数据库中可能会有所不同。为了使你的代码具有更好的可移植性，你应该使用大小写敏感的查找策略，或者指示 Spring 使用 `LinkedCaseInsensitiveMap` 。为了实现后者，你可以创建自己的 `JdbcTemplate` 并设定其 `setResultsMapCaseInsensitive` 属性为 `true` 。然后你可以将这个自定义的 `JdbcTemplate` 实例传入你的 `SimpleJdbcCall` 的构造器中。下面的例子展示了该配置：

```java
public class JdbcActorDao implements ActorDao {

    private SimpleJdbcCall procReadActor;

    public void setDataSource(DataSource dataSource) {
        JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
        jdbcTemplate.setResultsMapCaseInsensitive(true);
        this.procReadActor = new SimpleJdbcCall(jdbcTemplate)
                .withProcedureName("read_actor");
    }

    // ... additional methods
}
```

通过执行此操作，可以避免在用于返回的 `out` 参数名称的情况下发生冲突。

### 3.6.6 显式声明用于 `SimpleJdbcCall` 的参数

前文中，我们描述了如何从元数据推导出参数，但是如果需要，可以显式声明它们。您可以通过使用 `declareParameters` 方法创建和配置 `SimpleJdbcCall` 来实现，该方法采用可变数量的 `SqlParameter` 对象作为输入。请参阅 [下一节](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-params) 了解有关如何定义 `SqlParameter` 。

> 如果您使用的数据库不是 Spring 支持的数据库，则必须进行显式声明。当前，Spring 支持针对以下数据库的存储过程调用的元数据查找：Apache Derby，DB2，MySQL，Microsoft SQL Server，Oracle 和 Sybase。我们还支持MySQL，Microsoft SQL Server 和 Oracle 存储函数的元数据查找。

您可以选择显式声明一个，一些或所有参数。在未显式声明参数的地方，仍使用参数元数据。要绕过对潜在参数的元数据查找的所有处理，并且仅使用声明的参数，可以在声明中调用方法 `withoutProcedureColumnMetaDataAccess`。假设您为数据库函数声明了两个或多个不同的调用签名。在这种情况下，您调用 `useInParameterNames` 来指定要包含在给定签名中的 IN 参数名称列表。

下面的例子展示了完整的声明的存储过程调用，并使用了前面例子中的信息：

```java
public class JdbcActorDao implements ActorDao {

    private SimpleJdbcCall procReadActor;

    public void setDataSource(DataSource dataSource) {
        JdbcTemplate jdbcTemplate = new JdbcTemplate(dataSource);
        jdbcTemplate.setResultsMapCaseInsensitive(true);
        this.procReadActor = new SimpleJdbcCall(jdbcTemplate)
                .withProcedureName("read_actor")
                .withoutProcedureColumnMetaDataAccess()
                .useInParameterNames("in_id")
                .declareParameters(
                        new SqlParameter("in_id", Types.NUMERIC),
                        new SqlOutParameter("out_first_name", Types.VARCHAR),
                        new SqlOutParameter("out_last_name", Types.VARCHAR),
                        new SqlOutParameter("out_birth_date", Types.DATE)
                );
    }

    // ... additional methods
}
```

两个例子执行的结果是一样的。第二个例子显式指定了所有细节，而没有依赖元数据。

