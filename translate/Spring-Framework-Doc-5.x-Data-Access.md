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

