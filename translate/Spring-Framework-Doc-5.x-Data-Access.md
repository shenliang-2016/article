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

