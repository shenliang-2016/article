# Testing

**Version 5.1.9.RELEASE**

本章节涵盖 Spring 对集成测试和单元测试最佳实践的支持。Spring 团队推崇测试驱动开发模式（TDD）。Spring 团队已经发现控制反转（IoC）的正确使用是的单元测试和集成测试变得更简单（因为类的`setter`方法和适当的构造函数的存在使它们更容易在测试中连接在一起，而无需设置服务定位器注册表和类似的结构）。

## 1. Spring Testing 介绍

测试是企业软件开发不可或缺的一部分。 本章重点介绍IoC原理对 [unit testing](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#unit-testing) 的好处以及Spring Framework对 [integration testing](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing) 支持的好处。（对企业中的测试进行全面处理超出了本参考手册的范围。）

## 2. 单元测试

与传统的Java EE开发相比，依赖注入应该使您的代码对容器的依赖性降低。构成应用程序的POJO应该在JUnit或TestNG测试中可测试，对象使用`new`运算符实例化，不使用Spring或任何其他容器。您可以使用 [mock objects](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#mock-objects) （与其他有价值的测试技术结合使用）来单独测试代码。如果您遵循Spring的体系结构建议，那么代码库的干净分层和组件化便于单元测试。例如，您可以通过存根或模拟DAO或存储库接口来测试服务层对象，而无需在运行单元测试时访问持久数据。

真正的单元测试通常运行得非常快，因为没有要设置的运行时基础结构。强调真正的单元测试作为开发方法的一部分可以提高您的工作效率。您可能不需要本章节的这一部分来帮助您为基于IoC的应用程序编写有效的单元测试。但是，对于某些单元测试场景，Spring Framework提供了模拟对象和测试支持类，本章将对其进行介绍。

### 2.1. 模拟对象

Spring 包含大量专用于模拟对象的包：

- [Environment](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#mock-objects-env)
- [JNDI](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#mock-objects-jndi)
- [Servlet API](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#mock-objects-servlet)
- [Spring Web Reactive](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#mock-objects-web-reactive)

#### 2.1.1. Environment

`org.springframework.mock.env` 包中包含了 `Enviroment` 和 `PropertySource` 抽象的模拟实现（参考 [Bean Definition Profiles](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-definition-profiles) 和 [`PropertySource` Abstraction](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-property-source-abstraction) ）。`MockEnvironment` 和 `MockPropertySource` 对开发依赖于特定环境属性的代码的容器外测试很有用。

#### 2.1.2. JNDI

`org.springframework.mock.jndi` 包中包含了 JNDI SPI 的实现，你可以用来为测试套件后者独立应用建立一个简单的 JNDI 环境。例如，如果JDBC `DataSource`实例在测试代码中绑定到与Java EE容器中相同的JNDI名称，则可以在测试方案中重用应用程序代码和配置而无需修改。

#### 2.1.3. Servlet API

`org.springframework.mock.web` 包中包含了对 web 上下文，控制器，以及过滤器等测试非常有用的完备的 Servlet API 模拟对象集合。这些模拟对象和 Spring Web 框架结合使用，相对于使用动态模拟对象（比如 [EasyMock](http://easymock.org/) ）或者其它 Servlet API 模拟对象（比如 [MockObjects](http://www.mockobjects.com/) ），使用它们更加方便。

> 从 Spring  Framework 5.0 开始，`org.springframework.mock.web` 中的模拟对象都是基于 Servlet 4.0 API。

Spring MVC Test 框架以模拟 Servlet API 对象为基础，为 Spring MVC 提供集成测试框架。请参阅 [Spring MVC测试框架](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#spring-mvc-test-framework) 。

#### 2.1.4. Spring Web Reactive

`org.springframework.mock.http.server.reactive`包中包含用于 WebFlux 应用程序的`ServerHttpRequest`和`ServerHttpResponse`的模拟实现。`org.springframework.mock.web.server`包中包含一个依赖于那些模拟请求和响应对象的模拟`ServerWebExchange`。

`MockServerHttpRequest`和`MockServerHttpResponse`都从与服务器特定的实现相同的抽象基类扩展，并与它们共享行为。例如，模拟请求一旦创建就是不可变的，但您可以使用`ServerHttpRequest`中的`mutate()`方法创建修改后的实例。

为了使模拟响应正确地实现写入契约并返回写入完成句柄（即`Mono<Void>`），它默认使用带有`cache().then()`的`Flux`，它缓冲数据并使其可用于测试中的断言。应用程序可以设置自定义写入功能（例如，测试无限流）。

[WebTestClient](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#webtestclient)  以模拟请求和响应为基础，为不使用 HTTP 服务器测试 WebFlux 应用程序提供支持。客户端还可以用于正在运行的服务器的端到端测试。

### 2.2. 单元测试支持类

Spring 包含大量的类用来协助单元测试。它们被分为两类：

- [通用测试工具类](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#unit-testing-utilities)
- [Spring MVC 测试工具类](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#unit-testing-spring-mvc)

#### 2.2.1. 通用测试工具类

`org.springframework.test.util` 包中包含了若干通用用途的工具类，用于单元测试和集成测试。

`ReflectionTestUtils` 是一个基于反射的工具方法集合。你可以在那些你需要改变常量值，设置一个非 `public` 字段，调用一个非 `public` `setter` 方法，或者调用一个非 `public` 配置或者生命周期回调方法的测试场景下使用这些方法，具体测试场景如下：

 - 包含`private`或`protected`字段访问的 ORM 框架（例如 JPA 和 Hibernate），而不是域实体中属性的`public` `setter`方法。
 - Spring 的注解支持（例如`@Autowired`，`@Inject`和`@Resource`），它们为`private`或`protected`字段，`setter`方法和配置方法提供依赖注入。
 - 使用`@PostConstruct`和`@PreDestroy`等注解进行生命周期回调方法。

[`AopTestUtils`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/util/AopTestUtils.html)  是 AOP 相关实用程序方法的集合。您可以使用这些方法获取对隐藏在一个或多个 Spring 代理后面的基础目标对象的引用。例如，如果您已使用诸如 EasyMock 或 Mockito 之类的库将 bean 配置为动态模拟，并且模拟包装在 Spring 代理中，则可能需要直接访问底层模拟以配置对它的期望并执行验证。对于 Spring 的核心 AOP 实用程序，请参阅 [`AopUtils`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/aop/support/AopUtils.html)  和 [`AopProxyUtils`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/aop/framework/AopProxyUtils.html) 。

#### 2.2.2. Spring MVC 测试工具类

`org.springframework.test.web` 包中包含了  [`ModelAndViewAssert`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/web/ModelAndViewAssert.html) ，你可以将其与 JUnit，TestNG，或者任何其它测试框架结合使用来进行单元测试，处理 Spring MVC `ModelAndView` 对象。

> Spring MVC 控制器单元测试
>
> 为了将 Spring MVC `Controller` 类作为 POJOs 进行单元测试，使用 `ModelAndViewAssert` 以及 `MockHttpServletRequest` ，`MockHttpSession`，等来自 Spring  [Servlet API mocks](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#mock-objects-servlet) 的工具类。有关 Spring MVC 和 REST `Controller`类的完整集成测试以及 Spring MVC 的 `WebApplicationContext`配置，请使用 [Spring MVC Test Framework](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#spring-mvc-test-framework) 。

## 3. 集成测试

本节（本章的后续部分）涵盖 Spring 应用程序的集成测试。包括以下主题：

- [概述](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#integration-testing-overview)
- [集成测试的目标](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#integration-testing-goals)
- [JDBC 测试支持](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#integration-testing-support-jdbc)
- [注解](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations)
- [Spring TestContext 框架](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-framework)
- [Spring MVC Test 框架](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-mvc-test-framework)

### 3.1. 概述

你的集成测试不需要部署到应用服务器上，也不需要连接到其它基础设施就能独立执行，这种能力非常重要。它允许你测试下面这些东西：

- Spring IoC 容器上下文的正确连接。
- 使用 JDBC 或 ORM 工具进行数据访问。这可以包括诸如 SQL 语句的正确性，Hibernate 查询，JPA 实体映射等等。

Spring Framework 为`spring-test`模块中的集成测试提供了一流的支持。实际 JAR 文件的名称可能包含发行版本号，也可能是长的`org.springframework.test`形式，具体取决于您从何处获取（有关说明，请参阅 [依赖关系管理](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#dependency-management)部分）。该库包含`org.springframework.test`包，其中包含用于使用 Spring 容器进行集成测试的有价值的类。此测试不依赖于应用程序服务器或其他部署环境。这些测试比单元测试运行得慢，但比依赖部署到应用服务器的等效 Selenium（验收？）测试或远程测试快得多。

单元测试和集成测试支持以注解驱动的 [Spring TestContext Framework](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-framework) 的形式提供。TestContext 框架与使用中的实际测试框架无关，它允许在各种环境中插桩测试，包括 JUnit，TestNG 等。

### 3.2. 集成测试的目标

Spring 的集成测试支持有以下几个主要目标：

- 在测试期间管理 [Spring IoC container caching](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testing-ctx-management) 。
- 提供 [Dependency Injection of test fixture instances](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testing-fixture-di).
- 为集成测试提供合适的 [transaction management](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testing-tx) 。
- 提供 [Spring-specific base classes](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testing-support-classes) 辅助开发者编写集成测试。

接下来几个小节介绍每个目标并提供有关实现和配置细节的链接。

#### 3.2.1. 上下文管理和缓存

Spring TestContext 框架提供了 Spring `ApplicationContext` 实例和 `WebApplicationContext` 实例的连贯加载的同时还缓存了那些上下文。支持被加载的上下文的缓存是重要的，因为启动时间可能会成为问题－不是因为 Spring 本身的开销，而是哪些由 Spring 容器实例化的对象的实例化过程需要消耗时间。比如，包含 50 个到 100 个 Hibernate 映射文件的项目可能需要 10 秒到 20 秒时间加载这些映射文件，在每个测试夹具中的每个测试运行之前都执行这个过程将导致测试变慢，从而降低开发效率。

测试类通常声明 XML 或 Groovy 配置元数据的资源位置数组－通常在类路径中－或用于配置应用程序的带注解类的数组。这些位置或类与`web.xml`或生产部署的其他配置文件中指定的位置或类相同或类似。

默认情况下，一旦加载，配置好的`ApplicationContext`将被每个测试重用。因此，每个测试套件仅产生一次设置成本，并且后续测试执行要快得多。在此上下文中，术语“测试套件”表示所有测试都在同一 JVM 中运行－例如，所有测试都是针对给定项目或模块从 Ant，Maven 或 Gradle 构建的。在不太可能的情况下，测试会破坏应用程序上下文并需要重新加载（例如，通过修改 bean 定义或应用程序对象的状态），可以将 TestContext 框架配置为在执行下一个测试之前重新加载配置并重建应用程序上下文。

请参阅 [上下文管理](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management) 和 [上下文缓存](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-caching) 。

#### 3.2.2. 测试夹具的依赖注入

当 TestContext 框架加载你的应用上下文时，它可以通过依赖注入有选择地配置你的测试类实例。这提供了一种方便的机制来使用来自你的应用上下文的预配置的 beans 建立测试夹具。一个显著的好处就是你可以在各种测试场景下重用应用上下文(比如，为了配置 Spring 管理的对象图，事务性代理，`DataSource` 实例，等等)，因此避免了为每个测试用例重复执行复杂的测试夹具初始化工作。

比如，考虑一个场景，我们拥有一个类`HibernateTitleRepository`为`Title`域实体实现了数据访问逻辑。我们想要编写继承测试来覆盖以下区域：

- Spring 配置：基本地，与`HibernateTitleRepository` bean 有关的配置是否存在并且正确？
- Hibernate 映射文件配置：一切都正确映射并且是否正确的设置为延迟加载？
- `HibernateTitleRepository`的逻辑：此类型配置好的实例是否如期望的那样执行操作？

参考 [TestContext framework](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-fixture-di) 的测试夹具的依赖注入。

#### 3.2.3. 事务管理

测试中的一个常见问题就是访问真实数据库将会影响持久化存储的状态。即使你使用的是开发库，状态变化也可能会影响后续的测试。同时，许多操作 - 比如插入或者修改持久化数据 - 不能在事务范围之外执行（或者验证）。

TestContext 框架解决了这个问题。默认的，该框架为每个测试用例创建和回滚事务。你可以在编写代码时假定事务是始终存在的。如果你在测试中调用事务性的代理对象，它们的行为就是正确的，符合它们配置的事务性语义。另外，如果一个测试方法在为该测试用例管理的事务中删除选中表中的内容，事务将会默认回滚，而数据库将会恢复到该测试执行之前的状态。事务支持通过使用定义在测试上下文中的 `PlatformTransactionManager` bean 提供。

如果你希望事务被提交（不常见，但是有时候你希望特定的测试填充或者修改数据库），你可以通过使用 [`@Commit`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations) 注解告诉 TestContext 框架提交事务而不是回滚。

参考使用 [TestContext framework](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-tx) 的事务管理。

#### 3.2.4. 集成测试的支持类

Spring TestContext 框架提供了若干 `abstract` 支持类来简化集成测试的编写。这些基础测试类提供了良好定义的测试框架中的回调以及方便使用的实例变量和方法，允许你访问：

- `ApplicationContext` ，用来执行显式 bean 检索或者作为整体测试上下文的状态。
- `JdbcTemplate` ，用来执行 SQL 语句以查询数据库。你可以是使用这些查询来确认数据库相关代码执行前后数据库的状态。Spring 保证这些查询运行在应用代码相同的事务范围内。当和 ORM 工具结合使用时，请确保避免 [false positives](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-tx-false-positives) 。

另外，你可能会想要使用特定于你的项目的实例变量和方法创建自定义的、应用范围的超类。

参考 [TestContext framework](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-support-classes) 的支持类。

### 3.3. JDBC 测试支持

`org.springframework.test.jdbc` 包中包含 `JdbcTestUtils` ，它是一个 JDBC 相关的工具方法集合，目标是简化标准的数据库测试场景。特别地，`JdbcTestutils` 提供了下面的静态工具方法：

- `countRowsInTable(..)`：给定表中数据行计数。
- `countRowsInTableWhere(..)`：使用给定的 `WHERE` 子句对给定表中的数据行计数。
- `deleteFromTables(..)`：将特定表中所有行删除。
- `deleteFromTableWhere(..)`：使用给定的 `WHERE` 子句删除表中的行。
- `dropTables(..)`：删除特定的表。

> [`AbstractTransactionalJUnit4SpringContextTests`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-support-classes-junit4) 和 [`AbstractTransactionalTestNGSpringContextTests`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-support-classes-testng) 提供了方便的方法委托给前面提到过的 `JdbcTestUtils` 中的方法。`spring-jdbc` 模块提供了配置和启动一个内置数据库的支持，你可以将其用于需要数据库交互的集成测试。更多细节，参考 [Embedded Database Support](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/data-access.html#jdbc-embedded-database-support) 和 [Testing Data Access Logic with an Embedded Database](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/data-access.html#jdbc-embedded-database-dao-testing) 。

### 3.4. 注解

本节涵盖你可以在 Spring 应用测试中使用的注解。包括以下主题：

- [Spring 测试注解](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-spring)
- [标准注解支持](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-standard)
- [Spring JUnit 4 测试注解](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-junit4)
- [Spring JUnit Jupiter 测试注解](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-junit-jupiter)
- [测试的元注解支持](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-meta)

#### 3.4.1. Spring 测试注解

Spring 框架提供了下面这些特定于 Spring 的注解，你可以将它们结合 TestContext 框架用在你的单元测试和集成测试中。参考相关的文档获取更多信息，包含默认属性值，属性别名，等等细节。

Spring 测试注解如下：

- [`@BootstrapWith`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-bootstrapwith)
- [`@ContextConfiguration`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-contextconfiguration)
- [`@WebAppConfiguration`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-webappconfiguration)
- [`@ContextHierarchy`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-contexthierarchy)
- [`@ActiveProfiles`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-activeprofiles)
- [`@TestPropertySource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-testpropertysource)
- [`@DirtiesContext`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-dirtiescontext)
- [`@TestExecutionListeners`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-testexecutionlisteners)
- [`@Commit`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-commit)
- [`@Rollback`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-rollback)
- [`@BeforeTransaction`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-beforetransaction)
- [`@AfterTransaction`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-aftertransaction)
- [`@Sql`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-sql)
- [`@SqlConfig`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-sqlconfig)
- [`@SqlGroup`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-sqlgroup)

##### `@BootstrapWith`

`@BootstrapWith`  是一个类级别的注解，你可以将其用于 Spring TestContext 框架的启动配置。特别地，你可以使用 `BootstrapWith` 来指定一个自定义的 `TestContextBootstrapper` 。参考  [bootstrapping the TestContext framework](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-bootstrapping) 获取更多信息。

##### `@ContextConfiguration`

`@ContextConfiguration` 定义类级别的元数据，该元数据被用于确定如何为集成测试加载和配置一个 `ApplicationContext` 。特别是，`@ContextConfiguration` 声明应用上下文资源 `locations` 或者注解修饰的 `classes` 用于加载上下文。

资源位置典型的就是位于系统类路径中的 XML 配置文件或者 Groovy 脚本，等价的注解修饰的类典型的是 `@Configuration` 类。不过，资源位置也可以表示文件系统中的文件和脚本，注解修饰的类可以是组件类，等等。

下面的例子展示了 `@ContextConfiguration` 注解表示一个 XML 文件：

```java
@ContextConfiguration("/test-config.xml") 
public class XmlApplicationContextTests {
    // class body...
}
```

下面的例子展示了 `@ContextConfiguration` 注解表示一个类：

```java
@ContextConfiguration(classes = TestConfig.class) 
public class ConfigClassApplicationContextTests {
    // class body...
}
```

作为声明资源位置或注解修饰的类的替代或补充，您可以使用`@ContextConfiguration`来声明`ApplicationContextInitializer`类。以下示例显示了这种情况：

```java
@ContextConfiguration(initializers = CustomContextIntializer.class) 
public class ContextInitializerTests {
    // class body...
}
```

您也可以选择使用`@ContextConfiguration`来声明`ContextLoader`策略。但请注意，您通常不需要显式配置加载程序，因为默认加载程序支持初始化程序以及资源位置或注解修饰的类。

以下示例使用位置和加载器：

```java
@ContextConfiguration(locations = "/test-context.xml", loader = CustomContextLoader.class) 
public class CustomLoaderXmlApplicationContextTests {
    // class body...
}
```

> `@ContextConfiguration` 提供了对继承资源位置、配置类、以及由超类声明的上下文初始化器的支持。

See [Context Management](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management) and the `@ContextConfiguration` javadocs for further details.

##### `@WebAppConfiguration`

`@WebAppConfiguration` 是一个类级别注解，你可以用于声明为集成测试加载的 `ApplicationContext` 应该是 `WebApplicationContext` 。仅在测试类上存在`@WebAppConfiguration`可确保为测试加载`WebApplicationContext`，使用默认值`“file:src/main/webapp”`作为 Web 应用程序根目录的路径（即资源基本路径）。资源基本路径被用在创建 `MockServletContext` 的场景中，该类作为测试 `WebApplicationContext` 中的 `ServletContext` 。

下面的例子展示了如何使用 `@WebAppConfiguration` 注解：

```java
@ContextConfiguration
@WebAppConfiguration 
public class WebAppTests {
    // class body...
}
```

为了覆盖默认值，你可以使用隐含的 `value` 属性来指定一个不同的资源基路径。`classpath:` 和 `file:` 资源前缀都是支持的。如果没有提供任何资源前缀，该路径被假定为一个文件系统资源。下面的例子展示了如何指定一个类路径资源：

```java
@ContextConfiguration
@WebAppConfiguration("classpath:test-web-resources") 
public class WebAppTests {
    // class body...
}
```

注意，`@WebAppConfiguration` 必须被与 `@ContextConfiguration` 结合使用，或者在一个单独的测试类中使用，或者在一个测试类层级结构中。参考 [`@WebAppConfiguration`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/test/context/web/WebAppConfiguration.html) 文档获取更多细节。

##### `@ContextHierarchy`

`@ContextHierarchy` 是一个类级别的注解，用来为集成测试定义一个 `ApplicationContext` 实例的层级结构。`@ContextHierarchy` 应该被使用一个或者多个 `@ContextConfiguration` 实例的列表来声明，其中的每个实例都在上下文层级结构中定义了一个层级。下面的例子展示了在单个测试类中如何使用 `@ContextHierarchy` （`@ContextHierarchy` 也可以被用在一个测试类层级结构中）：

```java
@ContextHierarchy({
    @ContextConfiguration("/parent-config.xml"),
    @ContextConfiguration("/child-config.xml")
})
public class ContextHierarchyTests {
    // class body...
}
```

```java
@WebAppConfiguration
@ContextHierarchy({
    @ContextConfiguration(classes = AppConfig.class),
    @ContextConfiguration(classes = WebConfig.class)
})
public class WebIntegrationTests {
    // class body...
}
```

如果你需要在测试类层级中合并或者覆盖上下文层级结构的给定层级的配置，你必须显式指出该层级，通过提供与类层级结构中相应层级中的 `@ContextConfiguration` 中的 `name` 属性相同的值。参考 [Context Hierarchies](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-ctx-hierarchies) 和 [`@ContextHierarchy`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/test/context/ContextHierarchy.html) 文档获取更多细节。

##### `@ActiveProfiles`

`@ActiveProfiles` 是一个类级别的注解，可用于声明在为集成测试加载 `ApplicationContext` 时应该激活哪个 bean 定义配置文件。

下面的例子表示 `dev` 配置应该被激活：

```java
@ContextConfiguration
@ActiveProfiles("dev") 
public class DeveloperTests {
    // class body...
}
```

下面的例子表示 `dev` 和 `integration` 配置文件都应该被激活：

```java
@ContextConfiguration
@ActiveProfiles({"dev", "integration"}) 
public class DeveloperIntegrationTests {
    // class body...
}
```
> `@ActiveProfiles` 默认提供了对继承超类声明的激活的 bean 定义配置的支持。你也可以通过实现自定义的[`ActiveProfilesResolver`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-env-profiles-ActiveProfilesResolver) 并使用 `@ActiverProfiles` 的 `resolver` 属性注册它，来以编程方式解析激活的 bean 定义配置。

参考 [Context Configuration with Environment Profiles](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-env-profiles) 和 [`@ActiveProfiles`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/test/context/ActiveProfiles.html) 文档获取跟多示例和细节。

##### `@TestPropertySource`

`@TestPropertySource` 是一个类级别的注解，你可以用来配置需要添加到为集成测试加载的 `ApplicationContext` 的 `Environment` 中的 `PorpertySources` 集合中的属性文件以及行内属性的位置。

测试属性源相对于那些加载自操作系统环境或者 Java 系统属性的属性，拥有更高优先级。也要比应用通过 `@PropertySource` 声明式或者编程式添加的属性源优先级更高。因此，测试属性源可以被用于有选择地覆盖定义在系统中和应用属性源中定义的属性。进一步地，行内属性的优先级高于从资源位置加载的属性。

下面的例子展示了如何在类路径上声明一个属性文件：

```java
@ContextConfiguration
@TestPropertySource("/test.properties") 
public class MyIntegrationTests {
    // class body...
}
```

下面的例子展示了如何声明行内属性：

```java
@ContextConfiguration
@TestPropertySource(properties = { "timezone = GMT", "port: 4242" }) 
public class MyIntegrationTests {
    // class body...
}
```

##### `@DirtiesContext`

`@DirtiesContext` 表示在执行测试期间底层 Spring `ApplicationContext`已被弄脏（即，测试以某种方式修改或损坏它 - 例如，通过更改单例 bean 的状态）并且应该关闭。当应用程序上下文被标记为脏时，它将从测试框架的缓存中删除并关闭。因此，对于需要具有相同配置元数据的上下文的任何后续测试，都会重建基础 Spring 容器。

您可以将`@DirtiesContext`用作同一类或类层次结构中的类级别和方法级别注解。在这种情况下，`ApplicationContext`在任何此类带注解的方法之前或之后以及当前测试类之前或之后被标记为脏，具体取决于配置的`methodMode`和`classMode`。

以下示例说明了各种配置方案的上下文何时会变脏：

- 当前测试类之前，声明在类模式设置为  `BEFORE_CLASS` 的类上。

  ```java
  @DirtiesContext(classMode = BEFORE_CLASS) 
  public class FreshContextTests {
      // some tests that require a new Spring container
  }
  ```

- 在当前测试类之后，当声明在类模式设置为 `AFTER_CLASS` 的类上（也就是默认类模式）。

  ```java
  @DirtiesContext 
  public class ContextDirtyingTests {
      // some tests that result in the Spring container being dirtied
  }
  ```

- 当前测试类中的每个测试方法之前，当声明在类模式设置为 `BEFORE_EACH_TEST_METHOD` 的类上。

  ```java
  @DirtiesContext(classMode = BEFORE_EACH_TEST_METHOD) 
  public class FreshContextTests {
      // some tests that require a new Spring container
  }
  ```

- 当前测试类中的每个测试方法之后，当声明在类模式设置为 `AFTER_EACH_TEST_METHOD` 的类上。

  ```java
  @DirtiesContext(classMode = AFTER_EACH_TEST_METHOD) 
  public class ContextDirtyingTests {
      // some tests that result in the Spring container being dirtied
  }
  ```

- 当前测试之前，当声明在方法模式设置为 `BEFORE_METHOD` 的方法上。

  ```java
  @DirtiesContext(methodMode = BEFORE_METHOD) 
  @Test
  public void testProcessWhichRequiresFreshAppCtx() {
      // some logic that requires a new Spring container
  }
  ```

- 当前测试之后，当声明在方法模式设置为 `AFTER_METHOD` 的方法上（也就是默认方法模式）。

  ```java
  @DirtiesContext 
  @Test
  public void testProcessWhichDirtiesAppCtx() {
      // some logic that results in the Spring container being dirtied
  }
  ```

如果在测试中使用`@DirtiesContext`，其上下文配置为具有`@ContextHierarchy`的上下文层次结构的一部分，则可以使用`hierarchyMode`标志来控制如何清除上下文缓存。默认情况下，使用详尽的算法来清除上下文缓存，不仅包括当前级别，还包括共享当前测试公共祖先上下文的所有其他上下文层次结构。驻留在公共祖先上下文的子层次结构中的所有`ApplicationContext`实例将从上下文缓存中删除并关闭。如果穷举算法对于特定用例而言有点过犹不及，则可以指定更简单的当前级别算法，如以下示例所示。

```java
@ContextHierarchy({
    @ContextConfiguration("/parent-config.xml"),
    @ContextConfiguration("/child-config.xml")
})
public class BaseTests {
    // class body...
}

public class ExtendedTests extends BaseTests {

    @Test
    @DirtiesContext(hierarchyMode = CURRENT_LEVEL) 
    public void test() {
        // some logic that results in the child context being dirtied
    }
}
```

有关 `EXHAUSTIVE` 和 `CURRENT_LEVEL` 算法的更多细节，参考 [`DirtiesContext.HierarchyMode`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/test/annotation/DirtiesContext.HierarchyMode.html) 文档。

##### `@TestExecutionListeners`

`@TestExecutionListeners`定义了类级元数据，用于配置应该使用`TestContextManager`注册的`TestExecutionListener`实现。通常，`@TestExecutionListeners`与`@ContextConfiguration`一起使用。

以下示例显示如何注册两个`TestExecutionListener`实现：

```java
@ContextConfiguration
@TestExecutionListeners({CustomTestExecutionListener.class, AnotherTestExecutionListener.class}) 
public class CustomTestExecutionListenerTests {
    // class body...
}
```

默认情况下，`@TestExecutionListeners` 支持继承的监听器。参考 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/TestExecutionListeners.html) 获取更多示例和详情。

##### `@Commit`

`@Commit`表示在测试方法完成后应该提交事务性测试方法的事务。您可以使用`@Commit`作为`@Rollback(false)`的直接替代，以更明确地传达代码的意图。类似于`@Rollback`，`@Commit`也可以声明为类级别或方法级别的注解。

以下示例显示了如何使用`@Commit`注解：

```java
@Commit 
@Test
public void testProcessWithoutRollback() {
    // ...
}
```

##### `@Rollback`

`@Rollback`表示在测试方法完成后是否应回滚事务性测试方法的事务。如果为`true`，则回滚事务。否则，提交事务（另见[`@Commit`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-commit)）。即使没有显式声明`@Rollback`，Spring TestContext Framework中的集成测试回滚也默认为`true`。

当声明为类级注解时，`@Rollback`定义测试类层次结构中所有测试方法的默认回滚语义。当声明为方法级注解时，`@Rollback`定义了特定测试方法的回滚语义，可能会覆盖类级别`@Rollback`或`@Commit`语义。

以下示例导致不回滚测试方法的结果（即，结果提交到数据库）：

```java
@Rollback(false) 
@Test
public void testProcessWithoutRollback() {
    // ...
}
```

##### `@BeforeTransaction`

`@BeforeTransaction`表示在启动事务之前应该运行带注解的`void`方法，对于已经配置为使用 Spring 的`@Transactional`注解在事务中运行的测试方法。从Spring Framework 4.3开始，`@BeforeTransaction`方法不需要是`public`，可以在基于Java 8的接口默认方法中声明。

以下示例显示了如何使用`@BeforeTransaction`注释：

```java
@BeforeTransaction 
void beforeTransaction() {
    // logic to be executed before a transaction is started
}
```

##### `@AfterTransaction`

`@AfterTransaction`表示在事务结束后应该运行带注解的`void`方法，对于已经配置为使用 Spring 的`@Transactional`注解在事务中运行的测试方法。从Spring Framework 4.3开始，`@AfterTransaction`方法不需要是`public`，可以在基于Java 8的接口默认方法中声明。

```java
@AfterTransaction 
void afterTransaction() {
    // logic to be executed after a transaction has ended
}
```

##### `@Sql`

`@Sql`用于注解测试类或测试方法，以配置在集成测试期间针对给定数据库运行的SQL脚本。以下示例显示了如何使用它：

```java
@Test
@Sql({"/test-schema.sql", "/test-user-data.sql"}) 
public void userTest {
    // execute code that relies on the test schema and test data
}
```

参考 [Executing SQL scripts declaratively with @Sql](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-executing-sql-declaratively) 获取更多细节。

##### `@SqlConfig`

`@SqlConfig`定义了用于确定如何解析和运行使用`@Sql`注解配置的SQL脚本的元数据。以下示例显示了如何使用它：

```java
@Test
@Sql(
    scripts = "/test-user-data.sql",
    config = @SqlConfig(commentPrefix = "`", separator = "@@") 
)
public void userTest {
    // execute code that relies on the test data
}
```

##### `@SqlGroup`

`@SqlGroup`是一个容器注解，它聚合了几个`@Sql`注解。您可以本地使用`@SqlGroup`来声明几个嵌套的`@Sql`注解，或者您可以将它与 Java 8 的可重复注解一起使用，其中`@Sql`可以在同一个类或方法上多次声明， 隐式生成此容器注解。以下示例显示如何声明SQL组：

```java
@Test
@SqlGroup({ 
    @Sql(scripts = "/test-schema.sql", config = @SqlConfig(commentPrefix = "`")),
    @Sql("/test-user-data.sql")
)}
public void userTest {
    // execute code that uses the test schema and test data
}
```

