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

#### 3.4.2. 标准注解支持

对于所有 Spring TestContext 框架的所有配置，下面的注解的标准语义被支持。注意，这些注解并不是特定于测试，还可以用在 Spring 框架中的任何其他地方。

- `@Autowired`
- `@Qualifier`
- `@Resource` (javax.annotation) if JSR-250 is present
- `@ManagedBean` (javax.annotation) if JSR-250 is present
- `@Inject` (javax.inject) if JSR-330 is present
- `@Named` (javax.inject) if JSR-330 is present
- `@PersistenceContext` (javax.persistence) if JPA is present
- `@PersistenceUnit` (javax.persistence) if JPA is present
- `@Required`
- `@Transactional`

> JSR-250 生命周期注解
>
> 在 Spring TestContext 框架中，你可以使用 `@PostConstruct` 和 `@PreDestroy` 的标准语义到 `ApplicationContext` 中配置的任何应用组件之上。不过，这些生命周期注解在具体的测试类中的使用还是有些限制条件。
>
> 如果一个测试类中的方法由 `@PostConstruct` 注解修饰，该方法会在所有测试框架底层的前置方法（比如，使用 Junit Jupiter 的 `@BeforeEach` 注解修饰的方法）之前运行，对测试类中每个测试方法都是如此。另一方面，如果测试类中的一个方法由 `@PreDestroy` 注解修饰，该方法将永远不会运行。因此，在测试类中，我们建议您使用来自底层测试框架的测试生命周期回调，而不是 `@PostConstruct` 和 `@PreDestroy`。

#### 3.4.3. Spring JUnit 4 Testing Annotations

下面的注解只有当结合使用 [SpringRunner](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-junit4-runner), [Spring’s JUnit 4 rules](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-junit4-rules)，或者 [Spring’s JUnit 4 support classes](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-support-classes-junit4) 时才会被支持：

- [`@IfProfileValue`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-junit4-ifprofilevalue)
- [`@ProfileValueSourceConfiguration`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-junit4-profilevaluesourceconfiguration)
- [`@Timed`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-junit4-timed)
- [`@Repeat`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-junit4-repeat)

##### `@IfProfileValue`

`@IfProfileValue` 表示该测试为某个特定 测试环境开启。如果配置的 `ProfileValueSource` 返回与注解给定的 `name ` 匹配的 `vaule` ，该测试开启。否则，该测试不可用，也就是说，被忽略。

你可以将 `@IfProfileValue` 用在类级别，方法级别，或者同时用在两个级别。类级别使用的 `@IfProfileValue` 相对于该测试类中所有方法，以及该类的子类中所有方法，的方法级别的此注解，拥有更高优先级。特别地，一个测试被启用，如果它在类级别和方法级别同时都是被开启的。不存在此注解意味着测试是隐式开启的。此注解的语义近似于 Junit 4 的 `@Ignore` 注解，除了 `@Ignore` 注解始终都会关闭一个测试。

下面的例子展示了此注解的使用：

```java
@IfProfileValue(name="java.vendor", value="Oracle Corporation") 
@Test
public void testProcessWhichRunsOnlyOnOracleJvm() {
    // some logic that should run only on Java VMs from Oracle Corporation
}
```

另外，你可以使用一个 `values` 列表(使用 `OR` 语义)配置 `@IfProfileValue` 来在 Junit 4 环境下获得类－TestNG 的对测试组的支持。考虑下面的例子：

```java
@IfProfileValue(name="test-groups", values={"unit-tests", "integration-tests"}) 
@Test
public void testProcessWhichRunsForUnitOrIntegrationTestGroups() {
    // some logic that should run only for unit and integration test groups
}
```

##### `@ProfileValueSourceConfiguration`

`@ProfileValueSourceConfiguration` 是一个类级注解，它指定在检索通过 `@IfProfileValue` 注解配置的配置文件值时要使用的 `ProfileValueSource` 类型。如果没有为测试声明 `@ProfileValueSourceConfiguration`，则默认使用 `SystemProfileValueSource`。以下示例显示了如何使用`@ProfileValueSourceConfiguration`：

```java
@ProfileValueSourceConfiguration(CustomProfileValueSource.class) 
public class CustomProfileValueSourceTests {
    // class body...
}
```

##### `@Timed`

`@Timed`表示其注解的测试方法必须在指定的时间段内完成执行（以毫秒为单位）。如果测试执行时间超过指定的时间段，则测试失败。

时间段包括运行测试方法本身，任何重复的测试（参见`@Repeat`），以及测试夹具的任何设置或拆除。以下示例显示了如何使用它：

```java
@Timed(millis = 1000) 
public void testProcessWithOneSecondTimeout() {
    // some logic that should not take longer than 1 second to execute
}
```

Spring 的 `@Timed` 注解与 JUnit 4 的 `@Test(timeout=...)`支持有不同的语义。具体来说，取决于 JUnit 4 处理测试执行超时的方式（也就是说，通过在单独的 `Thread` 中执行测试方法），如果测试时间太长，则 `@Test(timeout=...)` 就会先发制人地让测试失败。另一方面，Spring 的 `@Timed` 没有先发制人地让测试失败，而是在失败之前等待测试完成。

##### `@Repeat`

`@Repeed`表示必须重复运行带注解的测试方法。在注解中指定测试方法的执行次数。

要重复的执行范围包括执行测试方法本身以及测试夹具的任何设置或拆除。以下示例显示了如何使用 `@Repeat` 注解：

```java
@Repeat(10) 
@Test
public void testProcessRepeatedly() {
    // ...
}
```

#### 3.4.4. Spring JUnit Jupiter 测试注解

下面的注解只有当同时使用 [`SpringExtension`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-junit-jupiter-extension) 和 JUnit Jupiter (也就是说，也就是说，JUnit 5中的编程模型) 时才会被支持：

- [`@SpringJUnitConfig`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-junit-jupiter-springjunitconfig)
- [`@SpringJUnitWebConfig`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-junit-jupiter-springjunitwebconfig)
- [`@EnabledIf`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-junit-jupiter-enabledif)
- [`@DisabledIf`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-junit-jupiter-disabledif)

##### `@SpringJUnitConfig`

`@SpringJUnitConfig` 是一个组合注解，结合了来自 JUnit Jupiter 的 `@ExtendWith(SpringExtension.class)` 和来自 Spring TestContext 框架的 `@ContextConfiguration` 。它可以用在类级别作为 `@ContextConfiguration` 的插入式替代。关于配置选项，`@ContextConfiguration` 和 `@SpringJUnitConfig` 的唯一区别就是可以使用 `@SpringJUnitConfig` 中的 `value` 属性声明注解修饰的类。

下面的例子展示了如何使用 `@SpringJUnitConfig` 注解来指定配置类：

```java
@SpringJUnitConfig(TestConfig.class) 
class ConfigurationClassJUnitJupiterSpringTests {
    // class body...
}
```

下面的例子展示了如何 使用 `@SpringJUnitConfig` 注解指定配置文件位置：

```java
@SpringJUnitConfig(locations = "/test-config.xml") 
class XmlJUnitJupiterSpringTests {
    // class body...
}
```

参考 [Context Management](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management) 和 [`@SpringJUnitConfig`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/junit/jupiter/SpringJUnitConfig.html) 以及 `@ContextConfiguration` 文档获取更多细节。

##### `@SpringJUnitWebConfig`

`@SpeingJUnitWebConfig` 是一个组合注解，结合了来自 JUnit Jupiter 的 `@ExtendWith(SpringExtension.class)` 和来自 Spring TestContext 框架的 `@ContextConfiguration` 和 `@WebAppConfiguration` 。你可以在类级别使用它作为 `@ContextConfiguration` 和 `@WebAppConfiguration` 的替代品。关于配置选项，`@ContextConfiguration` 和 `@SpringJUnitWebConfig` 的唯一区别就是你可以使用 `@SpringJUnitWebConfig` 中的 `value` 属性声明被注解的类。另外，你只能通过使用 `@SpringJUnitWebConfig` 的 `resourcePath` 覆盖 `@WebAppConfiguration` 中的 `value` 属性。

下面的例子展示了如何使用 `@SpringJUnitWebConfig` 注解指定配置类：

```java
@SpringJUnitWebConfig(TestConfig.class) 
class ConfigurationClassJUnitJupiterSpringWebTests {
    // class body...
}
```

下面的例子展示了如何使用 `@SpringJUnitWebConfig` 注解指定配置文件的位置：

```java
@SpringJUnitWebConfig(locations = "/test-config.xml") 
class XmlJUnitJupiterSpringWebTests {
    // class body...
}
```

参考 [Context Management](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management) 和 [`@SpringJUnitWebConfig`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/junit/jupiter/web/SpringJUnitWebConfig.html), [`@ContextConfiguration`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/ContextConfiguration.html), 以及 [`@WebAppConfiguration`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/web/WebAppConfiguration.html) 的文档获取更多细节。

##### `@EnabledIf`

`@EnabledIf` 用于表示该注解修饰的 JUnit Jupiter 测试类或测试方法已启用，如果提供的 `expression` 计算结果为`true`，则那些测试应该运行。具体来说，如果表达式求值为 `Boolean.TRUE` 或等于 `true` 的 `String`（忽略大小写），则启用测试。在类级别应用时，默认情况下也会自动启用该类中的所有测试方法。

表达式可以是如下之一：

- [Spring Expression Language](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#expressions) (SpEL) 表达式。比如： `@EnabledIf("#{systemProperties['os.name'].toLowerCase().contains('mac')}")`
- Spring [`Environment`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-environment) 中可用属性的占位符。比如： `@EnabledIf("${smoke.tests.enabled}")`
- 文本字面量。比如： `@EnabledIf("true")`

但请注意，不是属性占位符动态解析结果的文本文字的实用价值为零，因为`@EnabledIf("false")`等同于`@Disable`和`@EnabledIf("true")`在逻辑上毫无意义。

您可以使用`@EnabledIf`作为元注解来创建自定义组合注解。例如，您可以创建自定义`@EnabledOnMac`注解，如下所示：

```java
@Target({ElementType.TYPE, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@EnabledIf(
    expression = "#{systemProperties['os.name'].toLowerCase().contains('mac')}",
    reason = "Enabled on Mac OS"
)
public @interface EnabledOnMac {}
```

##### `@DisabledIf`

`@DisabledIf` 用于表示该注解修饰的 JUnit Jupiter 测试类或测试方法被禁用，如果提供的`expression`计算结果为`true`，则不应该执行。具体来说，如果表达式求值为`Boolean.TRUE`或等于`true` 的`String` （忽略大小写），则禁用测试。在类级别应用时，该类中的所有测试方法也会自动禁用。

表达式可以是以下任何一种：

 -  [Spring Expression Language](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#expressions)（SpEL）表达式。例如：`@DisabledIf("#{systemProperties['os.name'].toLowerCase().contains('mac')}")`
 -  Spring [`Environment`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-environment) 中可用属性的占位符。例如：`@DisabledIf("${smoke.tests.disabled}")`
 -  文字文字。例如：`@DisabledIf("true")`

但请注意，不是属性占位符的动态解析结果的文本文字没有实用价值，因为`@DisabledIf("true")`相当于`@Disable`和`@DisabledIf("false")` 在逻辑上毫无意义。

您可以使用`@DisabledIf`作为元注解来创建自定义组合注解。例如，您可以创建自定义的`@DisabledOnMac`注解，如下所示：

```java
@Target({ElementType.TYPE, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@DisabledIf(
    expression = "#{systemProperties['os.name'].toLowerCase().contains('mac')}",
    reason = "Disabled on Mac OS"
)
public @interface DisabledOnMac {}
```

#### 3.4.5. 为测试提供的元注解支持

您可以将大多数与测试相关的注解用作 [meta-annotations](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-meta-annotations ) 创建自定义组合注解并减少测试套件中的重复配置。

您可以将以下各项作为元注解与 [TestContext框架](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-framework) 结合使用。

- `@BootstrapWith`
- `@ContextConfiguration`
- `@ContextHierarchy`
- `@ActiveProfiles`
- `@TestPropertySource`
- `@DirtiesContext`
- `@WebAppConfiguration`
- `@TestExecutionListeners`
- `@Transactional`
- `@BeforeTransaction`
- `@AfterTransaction`
- `@Commit`
- `@Rollback`
- `@Sql`
- `@SqlConfig`
- `@SqlGroup`
- `@Repeat` *(only supported on JUnit 4)*
- `@Timed` *(only supported on JUnit 4)*
- `@IfProfileValue` *(only supported on JUnit 4)*
- `@ProfileValueSourceConfiguration` *(only supported on JUnit 4)*
- `@SpringJUnitConfig` *(only supported on JUnit Jupiter)*
- `@SpringJUnitWebConfig` *(only supported on JUnit Jupiter)*
- `@EnabledIf` *(only supported on JUnit Jupiter)*
- `@DisabledIf` *(only supported on JUnit Jupiter)*

考虑下面的例子：

```java
@RunWith(SpringRunner.class)
@ContextConfiguration({"/app-config.xml", "/test-data-access-config.xml"})
@ActiveProfiles("dev")
@Transactional
public class OrderRepositoryTests { }

@RunWith(SpringRunner.class)
@ContextConfiguration({"/app-config.xml", "/test-data-access-config.xml"})
@ActiveProfiles("dev")
@Transactional
public class UserRepositoryTests { }
```

如果我们发现我们在基于 JUnit 4 的测试套件中重复了前面的配置，我们可以通过引入一个自定义组合注解来集中 Spring 的常用测试配置来减少重复，如下所示：

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@ContextConfiguration({"/app-config.xml", "/test-data-access-config.xml"})
@ActiveProfiles("dev")
@Transactional
public @interface TransactionalDevTestConfig { }
```

然后我们可以使用自定义的`@TransactionalDevTestConfig`注解来简化基于JUnit 4的各个测试类的配置，如下所示：

```java
@RunWith(SpringRunner.class)
@TransactionalDevTestConfig
public class OrderRepositoryTests { }

@RunWith(SpringRunner.class)
@TransactionalDevTestConfig
public class UserRepositoryTests { }
```

如果我们编写使用JUnit Jupiter的测试，我们可以进一步减少代码重复，因为JUnit 5中的注解也可以用作元注解。请考虑以下示例：

```java
@ExtendWith(SpringExtension.class)
@ContextConfiguration({"/app-config.xml", "/test-data-access-config.xml"})
@ActiveProfiles("dev")
@Transactional
class OrderRepositoryTests { }

@ExtendWith(SpringExtension.class)
@ContextConfiguration({"/app-config.xml", "/test-data-access-config.xml"})
@ActiveProfiles("dev")
@Transactional
class UserRepositoryTests { }
```

如果我们发现我们在基于JUnit Jupiter的测试套件中重复上述配置，我们可以通过引入一个自定义组合注解来集中Spring和JUnit Jupiter的常用测试配置来减少重复，如下所示：

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@ExtendWith(SpringExtension.class)
@ContextConfiguration({"/app-config.xml", "/test-data-access-config.xml"})
@ActiveProfiles("dev")
@Transactional
public @interface TransactionalDevTestConfig { }
```

然后我们可以使用我们的自定义`@TransactionalDevTestConfig`注解来简化各个基于JUnit Jupiter的测试类的配置，如下所示：

```java
@TransactionalDevTestConfig
class OrderRepositoryTests { }

@TransactionalDevTestConfig
class UserRepositoryTests { }
```

由于JUnit Jupiter支持使用`@Test`，`@RepeatedTest`，`ParameterizedTest`和其他作为元注解，因此您还可以在测试方法级别创建自定义组合注解。例如，如果我们希望创建一个组合注解，它将来自JUnit Jupiter的`@Test`和`@Tag`注解与Spring中的`@Transactional`注解相结合，我们可以创建一个`@TransactionalIntegrationTest`注解，如下所示：

```java
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.RUNTIME)
@Transactional
@Tag("integration-test") // org.junit.jupiter.api.Tag
@Test // org.junit.jupiter.api.Test
public @interface TransactionalIntegrationTest { }
```

然后我们可以使用我们的自定义`@TransactionalIntegrationTest`注解来简化各个基于JUnit Jupiter的测试方法的配置，如下所示：

```java
@TransactionalIntegrationTest
void saveOrder() { }

@TransactionalIntegrationTest
void deleteOrder() { }
```

参考 [Spring Annotation Programming Model](https://github.com/spring-projects/spring-framework/wiki/Spring-Annotation-Programming-Model) 页面获取更多细节。

### 3.5 Spring TestContext 框架

Spring TestContext Framework（位于 `org.springframework.test.context` 包中）提供了通用的，注解驱动的单元测试和集成测试支持，它与使用中的测试框架无关。TestContext 框架也非常重视约定优于配置，合理的默认值可以通过基于注解的配置覆盖。

除了通用测试基础设施之外，TestContext 框架还为 JUnit 4，JUnit Jupiter（AKA JUnit 5）和 TestNG 提供了显式支持。对于 JUnit 4 和 TestNG，Spring 提供了 `abstract` 支持类。此外，Spring 为 JUnit 4 提供了一个自定义 JUnit `Runner`和自定义 JUnit `Rules`，并为 JUnit Jupiter 提供了一个自定义 `Extension`，可以编写所谓的 POJO 测试类。POJO测试类不需要扩展特定的类层次结构，例如 `abstract` 支持类。

以下部分概述了 TestContext 框架的内部结构。如果您只对使用框架感兴趣并且不想使用自己的自定义监听器或自定义加载器扩展它，请随意直接进入配置 ([context management](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management), [dependency injection](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-fixture-di), [transaction management](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-tx)), [support classes](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-support-classes), 和 [annotation support](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations) 部分。

#### 3.5.1. 关键抽象

框架的核心包括 `TestContextManager` 类和 `TestContext`，`TestExecutionListener` 和 `SmartContextLoader` 接口。为每个测试类创建一个 `TestContextManager`（例如，用于在 JUnit Jupiter 中的单个测试类中执行所有测试方法）。反过来，`TestContextManager` 管理一个保存当前测试上下文的 `TestContext` 。随着测试的进行，`TestContextManager` 也会更新 `TestContext` 的状态，并委托给 `TestExecutionListener` 实现，它通过提供依赖注入，管理事务等来检测实际的测试执行。 `SmartContextLoader` 负责为给定的测试类加载 `ApplicationContext` 。参见 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/package-summary.html) 和 Spring 测试套件以获取更多信息和各种实现的示例。

##### `TestContext`

`TestContext` 封装了执行测试的上下文（与使用中的实际测试框架无关），并为其负责的测试实例提供上下文管理和缓存支持。如果请求，`TestContext` 也委托给一个 `SmartContextLoader` 来加载 `ApplicationContext` 。

##### `TestContextManager`

`TestContextManager` 是 Spring TestContext Framework 的主要入口点，负责管理单个 `TestContext` 并在明确定义的测试执行点向每个注册的 `TestExecutionListener` 发送信号事件：

 - 在特定测试框架的任何“before class”或“before all”方法之前。
 - 测试实例后处理。
 - 在特定测试框架的任何“before”或“before each”方法之前。
 - 在执行测试方法之前，但在测试设置之后。
 - 执行测试方法后立即但在测试拆除之前。
 - 在特定测试框架的任何“after”或“after each”方法之后。
 - 在特定测试框架的任何“after class”或“after all”方法之后。

##### `TestExecutionListener`

`TestExecutionListener` 定义了API，用于响应由注册监听器的 `TestContextManager` 发布的测试执行事件。请参阅 [`TestExecutionListener`配置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-tel-config) 。

##### `Context Loaders`

`ContextLoader` 是一个策略接口，用于为 Spring TestContext Framework 管理的集成测试加载 `ApplicationContext` 。您应该实现 `SmartContextLoader` 而不是此接口，以提供对带注解的类，活动 Bean 定义配置文件，测试属性源，上下文层次结构和 `WebApplicationContext` 的支持。

`SmartContextLoader` 是Spring 3.1 中引入的 `ContextLoader` 接口的扩展，取代了最初的最小 `ContextLoader` SPI。具体来说，`SmartContextLoader` 可以选择处理资源位置，带注解的类或上下文初始化器。此外，`SmartContextLoader` 可以在它加载的上下文中设置活动 bean 定义配置文件和测试属性源。

Spring 提供以下实现：

* `DelegatingSmartContextLoader`：两个默认加载器之一，它内部委托给`AnnotationConfigContextLoader`，`GenericXmlContextLoader` 或 `GenericGroovyXmlContextLoader`，具体取决于为测试类声明的配置或默认位置或默认配置类的存在。仅当 Groovy 位于类路径上时才启用 Groovy 支持。

* `WebDelegatingSmartContextLoader`：两个默认加载器之一，它内部委托给`AnnotationConfigWebContextLoader`，`GenericXmlWebContextLoader` 或 `GenericGroovyXmlWebContextLoader`，具体取决于为测试类声明的配置或默认位置或默认配置类的存在。仅当测试类中存在`@WebAppConfiguration`时，才使用 Web `ContextLoader`。仅当 Groovy 位于类路径上时才启用 Groovy 支持。

* `AnnotationConfigContextLoader`：从带注解的类中加载标准`ApplicationContext`。

* `AnnotationConfigWebContextLoader`：从带注解的类中加载`WebApplicationContext`。

* `GenericGroovyXmlContextLoader`：从 Groovy 脚本或 XML 配置文件的资源位置加载标准 `ApplicationContext`。

* `GenericGroovyXmlWebContextLoader`：从 Groovy 脚本或 XML 配置文件的资源位置加载 `WebApplicationContext`。

* `GenericXmlContextLoader`：从 XML 资源位置加载标准 `ApplicationContext`。

* `GenericXmlWebContextLoader`：从 XML 资源位置加载 `WebApplicationContext`。

* `GenericPropertiesContextLoader`：从 Java 属性文件加载标准 `ApplicationContext`。

#### 3.5.2. 引导 TestContext 框架

Spring TestContext Framework 内部的默认配置足以满足所有常见场景。但是，有时开发团队或第三方框架想要更改默认的 `ContextLoader`，实现自定义 `TestContext` 或 `ContextCache`，扩充 `ContextCustomizerFactory` 和 `TestExecutionListener` 实现的默认集，等等。对于 TestContext 框架如何操作的这种低级控制，Spring 提供了一个自举策略。

`TestContextBootstrapper` 定义了用于引导 TestContext 框架的 SPI。 `TestContextBootstrapper`使用 `TestContextBootstrapper` 来加载当前测试的 `TestExecutionListener` 实现并构建它管理的 `TestContext`。您可以使用 `@BootstrapWith` 直接或作为元注解为测试类（或测试类层次结构）配置自定义引导策略。如果没有使用 `@BootstrapWith` 显式配置引导程序，则使用 `DefaultTestContextBootstrapper` 或 `WebTestContextBootstrapper`，具体取决于 `@WebAppConfiguration` 的存在。

由于 `TestContextBootstrapper` SPI 将来可能会发生变化（以适应新的要求），我们强烈建议实现者不要直接实现这个接口，而是扩展 `AbstractTestContextBootstrapper` 或其中一个具体的子类。

#### 3.5.3. `TestExecutionListener` 配置

Spring 提供了严格按照下列顺序默认注册的 `TestExecutionListener` 实现：

- `ServletTestExecutionListener`：为`WebApplicationContext`配置 Servlet API 模拟。
- `DirtiesContextBeforeModesTestExecutionListener`：为 “before” 模式处理 `@DirtiesContext` 注解。
- `DependencyInjectionTestExecutionListener`：为测试实例提供依赖注入。
- `DirtiesContextTestExecutionListener`：为 “after” 模式处理 `@DirtiesContext` 注解。
- `TransactionalTestExecutionListener`：提供事务性测试执行以及默认回滚语义。
- `SqlScriptsTestExecutionListener`：执行使用 `@Sql` 注解配置的 SQL 脚本。

##### 注册自定义 `TestExecutionListener` 实现

你可以使用 `@TestExecutionListeners` 注解为测试类或者它的子类注册自定义 `TestExecutionListener` 实现。参考 [annotation support](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations) 以及 [`@TestExecutionListeners`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/TestExecutionListeners.html) 文档获取更多信息。

##### 默认 `TestExecutionListener` 实现的自动发现

使用 `@TestExecutionListeners` 注册自定义 `TestExecutionListener` 实现适用于在有限测试场景中使用的自定义侦听器。但是，如果需要在测试套件中使用自定义侦听器，则会变得很麻烦。从 Spring Framework 4.1 开始，通过支持通过 `SpringFactoriesLoader` 机制自动发现默认的 `TestExecutionListener` 实现来解决这个问题。

具体来说，`spring-test` 模块在其 `META-INF/spring.factories` 属性文件中的 `org.springframework.test.context.TestExecutionListener` 键下声明所有核心默认的`TestExecutionListener`实现。第三方框架和开发人员可以通过他们自己的 `META-INF/spring.factories` 属性文件以相同的方式将自己的 `TestExecutionListener` 实现贡献给默认侦听器列表。

#####  `TestExecutionListener` 实现排序

当 TestContext 框架通过上述 `SpringFactoriesLoader` 机制发现默认的 `TestExecutionListener` 实现时，实例化的侦听器使用 Spring 的 `AnnotationAwareOrderComparator` 进行排序，它遵循 Spring 的 `Ordered` 接口和 `@Order` 注解进行排序。Spring 提供的 `AbstractTestExecutionListener` 和所有默认的 `TestExecutionListener` 实现都使用适当的值实现 `Ordered`。因此，第三方框架和开发人员应确保通过实现 `Ordered` 或声明 `@Order` 以正确的顺序注册其默认的 `TestExecutionListener` 实现。有关为每个核心侦听器分配的值的详细信息，请参阅核心默认 `TestExecutionListener` 实现的 `getOrder()` 方法文档。

##### 合并 `TestExecutionListener` 实现

如果通过 `@TestExecutionListeners` 注册了自定义 `TestExecutionListener`，则不会注册默认侦听器。在大多数常见的测试场景中，除了任何自定义侦听器之外，这还有效地迫使开发人员手动声明所有默认侦听器。以下清单演示了这种配置风格：

```java
@ContextConfiguration
@TestExecutionListeners({
    MyCustomTestExecutionListener.class,
    ServletTestExecutionListener.class,
    DirtiesContextBeforeModesTestExecutionListener.class,
    DependencyInjectionTestExecutionListener.class,
    DirtiesContextTestExecutionListener.class,
    TransactionalTestExecutionListener.class,
    SqlScriptsTestExecutionListener.class
})
public class MyTest {
    // class body...
}
```

这种方法的挑战在于它要求开发人员确切地知道默认情况下注册了哪些监听器。此外，默认侦听器集可能在不同发行版之间发生变化 - 例如，Spring Framework 4.1 中引入了 `SqlScriptsTestExecutionListener` ，Spring Framework 4.2 中引入了 `DirtiesContextBeforeModesTestExecutionListener`。此外，Spring Security 等第三方框架使用上述 [自动发现机制](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-tel-config-automatic-discovery) 注册了自己的默认 `TestExecutionListener` 实现。

为了避免必须知道并重新声明所有默认侦听器，可以将 `@TestExecutionListeners` 的 `mergeMode` 属性设置为 `MergeMode.MERGE_WITH_DEFAULTS`。 `MERGE_WITH_DEFAULTS` 表示本地声明的侦听器应该与默认侦听器合并。合并算法确保从列表中删除重复项，并根据 `AnnotationAwareOrderComparator` 的语义对生成的合并侦听器集进行排序，如 [`TestExecutionListener`实现排序](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-tel-config-ordering) 中所述。如果一个监听器实现了 `Ordered` 或者使用 `@Order` 进行了注解，它可以影响它与默认值合并的位置。否则，在合并时，本地声明的侦听器将附加到默认侦听器列表中。

例如，如果前一个示例中的 `MyCustomTestExecutionListener` 类将其 `order` 值（例如，`500`）配置为小于 `ServletTestExecutionListener`（恰好是`1000`）的顺序，则 `MyCustomTestExecutionListener` 可以自动与 `ServletTestExecutionListener` 前面的默认列表合并，前面的示例可以替换为以下示例：

```java
@ContextConfiguration
@TestExecutionListeners(
    listeners = MyCustomTestExecutionListener.class,
    mergeMode = MERGE_WITH_DEFAULTS
)
public class MyTest {
    // class body...
}
```

#### 3.5.4. 上下文管理

每个 `TestContext` 都为它负责的测试实例提供上下文管理和缓存支持。测试实例不会自动接收对配置的 `ApplicationContext` 的访问权限。但是，如果测试类实现了 `ApplicationContextAware` 接口，则会向测试实例提供对 `ApplicationContext` 的引用。请注意，`AbstractJUnit4SpringContextTests` 和 `AbstractTestNGSpringContextTests` 实现 `ApplicationContextAware`，因此，自动提供对 `ApplicationContext` 的访问。

> @Autowired ApplicationContext
>
> 作为另一种实现 `ApplicationContextAware` 接口的方法，你可以通过 `@Autowired` 注解将你的测试类的上下文注入到字段或者方法上，如下面例子所示：
>
> ````java
> @RunWith(SpringRunner.class)
> @ContextConfiguration
> public class MyTest {
> 
>     @Autowired 
>     private ApplicationContext applicationContext;
> 
>     // class body...
> }
> ````
>
> 类似地，如果你的测试被配置为加载一个 `WebApplicationContext` ，你可以将该 web 应用上下文注射到你的测试中，如下面例子所示：
>
> ````java
> @RunWith(SpringRunner.class)
> @WebAppConfiguration 
> @ContextConfiguration
> public class MyWebAppTest {
> 
>     @Autowired 
>     private WebApplicationContext wac;
> 
>     // class body...
> }
> ````
>
> 通过使用 `@Autowired` 进行的依赖注入由 `DependencyInjectionTestExecutionListener` 提供，它默认被配置(参考  [Dependency Injection of Test Fixtures](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-fixture-di) )。

使用 TestContext 框架的测试类无需扩展任何特定的类或者实现任何特定的接口以配置它们的应用上下文。相反，配置是通过在类层面声明 `@ContextConfiguration` 注解来获取。如果你的测试类没有显式声明应用上下文资源位置活着注解修饰的类，则配置的 `ContextLoader` 决定如何从默认位置或者默认配置类加载上下文。除了上下文资源位置和注解修饰的类，应用上下文还可以通过应用上下文初始化器配置。

接下来的章节解释如何使用 Spring 的 `@ContextConfiguration` 注解配置测试 `ApplicationContext` ，或者使用 XML 配置文件，Groovy 脚本，注解修饰的类(典型的事 `@Configuration` 类)，或者上下文初始化器。另外，你可以实现并配置你自己的自定义 `SmartContextLoader` 用于高级场景。

- [使用 XML 资源进行上下文配置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-xml)
- [使用 Groovy 脚本进行上下文配置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-groovy)
- [使用注解类进行上下文配置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-javaconfig)
- [混合 XML, Groovy 脚本, 以及注解修饰的类](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-mixed-config)
- [使用上下文初始化器进行上下文配置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-initializers)
- [上下文配置继承](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-inheritance)
- [使用环境配置进行上下文配置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-env-profiles)
- [使用测试属性源进行上下文配置](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-property-sources)
- [加载 `WebApplicationContext`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-web)
- [上下文缓存](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-caching)
- [上下文层级结构](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-ctx-hierarchies)

##### 使用 XML 资源进行上下文配置

要使用 XML 配置文件为测试加载 `ApplicationContext`，请使用 `@IntextConfiguration` 注解修饰测试类，并使用包含 XML 配置元数据的资源位置的数组配置 `locations` 属性。普通路径或相对路径（例如，`context.xml`）被视为相对于定义测试类的包的类路径资源。以斜杠开头的路径被视为绝对类路径位置（例如，`/org/example/config.xml`）。表示资源 URL 的路径（即，以 `classpath:`，`file:`，`http:` 等为前缀的路径）使用原样。

````java
@RunWith(SpringRunner.class)
// ApplicationContext will be loaded from "/app-config.xml" and
// "/test-config.xml" in the root of the classpath
@ContextConfiguration(locations={"/app-config.xml", "/test-config.xml"}) 
public class MyTest {
    // class body...
}
````

`@ContextConfiguration` 通过标准的 Java `value` 属性支持 `locations` 属性的别名。因此，如果您不需要在 `@IntextConfiguration` 中声明其他属性，则可以省略 `locations` 属性名称的声明，并使用以下示例中演示的速记格式声明资源位置：

````java
@RunWith(SpringRunner.class)
@ContextConfiguration({"/app-config.xml", "/test-config.xml"}) 
public class MyTest {
    // class body...
}
````

如果同时省略 `@ContextConfiguration` 注解中的 `locations` 和 `value` 属性，TestContext 框架会尝试检测默认的 XML 资源位置。具体来说，`GenericXmlContextLoader` 和 `GenericXmlWebContextLoader` 根据测试类的名称检测默认位置。如果您的类名为 `com.example.MyTest`，则 `GenericXmlContextLoader` 将从 `"classpath:com/example/MyTest-context.xml"` 中加载您的应用程序上下文。以下示例显示了如何执行此操作：

````java
package com.example;

@RunWith(SpringRunner.class)
// ApplicationContext will be loaded from
// "classpath:com/example/MyTest-context.xml"
@ContextConfiguration 
public class MyTest {
    // class body...
}
````

##### 使用 Groovy 脚本进行上下文配置

通过使用 [Groovy Bean Definition DSL](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#groovy-bean-definition-dsl) 的 Groovy 脚本为测试加载 `ApplicationContext`，您可以使用 `@IntextConfiguration` 注解修饰您的测试类，并使用包含 Groovy 脚本资源位置的数组配置 `locations` 或 `value` 属性。Groovy 脚本的资源查找语义与  [XML configuration files](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-xml) 中描述的相同。

> 启用 Groovy 脚本支持
>
> 如果 Groovy 在类路径上，则自动支持使用 Groovy 脚本在 Spring TestContext Framework 中加载 `ApplicationContext`。

下面的例子展示了如何指定 Groovy 配置文件：

```java
@RunWith(SpringRunner.class)
// ApplicationContext will be loaded from "/AppConfig.groovy" and
// "/TestConfig.groovy" in the root of the classpath
@ContextConfiguration({"/AppConfig.groovy", "/TestConfig.Groovy"}) 
public class MyTest {
    // class body...
}
```

如果同时省略 `@IntextConfiguration` 注解中的 `locations` 和 `value` 属性，TestContext 框架会尝试检测默认的 Groovy 脚本。具体来说，`GenericGroovyXmlContextLoader` 和 `GenericGroovyXmlWebContextLoader` 根据测试类的名称检测默认位置。如果您的类名为 `com.example.MyTest`，则 Groovy 上下文加载器将从 `"classpath:com/example/MyTestContext.groovy"` 中加载您的应用程序上下文。以下示例显示了如何使用默认值：

```java
package com.example;

@RunWith(SpringRunner.class)
// ApplicationContext will be loaded from
// "classpath:com/example/MyTestContext.groovy"
@ContextConfiguration 
public class MyTest {
    // class body...
}
```

> 同时声明 XML 配置和 Groovy 脚本
>
> 您可以使用 `@ContextConfiguration` 的 `locations` 或 `value` 属性同时声明 XML 配置文件和 Groovy 脚本。如果配置的资源位置的路径以 `.xml` 结尾，则使用 `XmlBeanDefinitionReader` 加载它。否则，使用 `GroovyBeanDefinitionReader` 加载它。
>
> 以下清单显示了如何在集成测试中将两者结合使用：
>
> ````java
> @RunWith(SpringRunner.class)
> // ApplicationContext will be loaded from
> // "/app-config.xml" and "/TestConfig.groovy"
> @ContextConfiguration({ "/app-config.xml", "/TestConfig.groovy" })
> public class MyTest {
>     // class body...
> }
> ````

##### 使用注解类进行上下文配置

使用注解修饰的类为测试加载 `ApplicationContext`（参见 [Java-based container configuration](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-java) ），您可以使用 `@ContextConfiguration` 注解修饰您的测试类，并使用包含对注解修饰类的引用的数组配置 `classes` 属性。以下示例显示了如何执行此操作：

````java
@RunWith(SpringRunner.class)
// ApplicationContext will be loaded from AppConfig and TestConfig
@ContextConfiguration(classes = {AppConfig.class, TestConfig.class}) 
public class MyTest {
    // class body...
}
````

> 注解修饰的类
>
> 术语“注解修饰的类”表示如下之一：
>
> - 使用 `@Configuration` 注解修饰的类。
> - 组件 (也就是，使用 `@Component`， `@Service`， `@Repository`，或者其他模版注解)。
> - 兼容 JSR-330 的类，由 `javax.inject` 注解修饰。
> - 包含 `@Bean` 方法的任何其他类。
>
> 参考 [`@Configuration`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/context/annotation/Configuration.html) 和 [`@Bean`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/context/annotation/Bean.html) 文档获取有关注解类的配置和语义的更多信息，请特别注意对 `@Bean` Lite模式的讨论。

如果省略 `@IntextConfiguration` 注解中的 `classes` 属性，TestContext 框架会尝试检测是否存在默认配置类。具体来说，`AnnotationConfigContextLoader` 和 `AnnotationConfigWebContextLoader` 检测满足配置类实现要求的测试类的所有 `static` 嵌套类，如  [`@Configuration`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/context/annotation/Configuration.html)  文档中所述。请注意，配置类的名称是任意的。此外，如果需要，测试类可以包含多个 `static` 嵌套配置类。在下面的示例中，`OrderServiceTest` 类声明了一个名为 `Config` 的 `static` 嵌套配置类，它自动用于加载测试类的 `ApplicationContext`：

````java
@RunWith(SpringRunner.class)
// ApplicationContext will be loaded from the
// static nested Config class
@ContextConfiguration 
public class OrderServiceTest {

    @Configuration
    static class Config {

        // this bean will be injected into the OrderServiceTest class
        @Bean
        public OrderService orderService() {
            OrderService orderService = new OrderServiceImpl();
            // set properties, etc.
            return orderService;
        }
    }

    @Autowired
    private OrderService orderService;

    @Test
    public void testOrderService() {
        // test the orderService
    }

}
````

##### 混合 XML, Groovy 脚本, 以及注解修饰的类

有时可能需要混合 XML 配置文件，Groovy 脚本和注解修饰的类（通常是 `@Configuration` 类）来为您的测试配置 `ApplicationContext`。例如，如果在生产中使用 XML 配置，你可能会决定要使用 `@Configuration` 类为测试配置特定的 Spring 管理的组件，反之亦然。

此外，一些第三方框架（如 Spring Boot）为同时从不同类型的资源加载 `ApplicationContext` 提供了一流的支持（例如，XML 配置文件，Groovy 脚本和 `@Configuration` 类）。历史上，Spring Framework 并未支持这样配置标准部署。因此，Spring Framework 在 `spring-test` 模块中提供的大多数 `SmartContextLoader` 实现仅支持每个测试上下文的一种资源类型。但是，这并不意味着您不能同时使用两者。一般规则的一个例外是 `GenericGroovyXmlContextLoader` 和 `GenericGroovyXmlWebContextLoader` 同时支持 XML 配置文件和 Groovy 脚本。此外，第三方框架可以选择通过 `@ContextConfiguration` 支持 `locations` 和 `classes` 的声明，并且，通过 TestContext 框架中的标准测试支持，您有以下选项。

如果要使用资源位置（例如，XML 或 Groovy）和 `@Configuration` 类来配置测试，则必须选择一个作为入口点，并且必须包含或导入另一个。例如，在 XML 或 Groovy 脚本中，您可以通过使用组件扫描包含 `@Configuration` 类或将它们定义为普通的 Spring bean，而在 `@Configuration` 类中，您可以使用 `@ImportResource` 来导入 XML 配置 文件或 Groovy 脚本。请注意，此行为在语义上等同于您在生产中配置应用程序的方式：在生产配置中，您可以定义一组 XML 或 Groovy 资源位置，或者从中加载生成 `ApplicationContext` 的一组 `@Configuration` 类， 但您仍然可以自由地包含或导入其他类型的配置。

##### 使用上下文初始化器进行上下文配置

要使用上下文初始化程序为测试配置 `ApplicationContext`，请使用 `@IntextConfiguration` 注解修饰您的测试类，并使用包含对实现 `ApplicationContextInitializer` 的类的引用的数组配置 `initializers` 属性。然后使用声明的上下文初始值设定项初始化为测试加载的 `ConfigurableApplicationContext`。请注意，每个声明的初始化程序支持的具体 `ConfigurableApplicationContext` 类型必须与使用中的 `SmartContextLoader` 创建的 `ApplicationContext` 类型兼容（通常是 `GenericApplicationContext`）。此外，调用初始化器的顺序取决于它们是否实现了 Spring 的 `Ordered` 接口，或者是使用 Spring 的 `@Order` 注解，或者使用标准的 `@Priority` 注解进行注释。以下示例显示了如何使用初始化器：

````java
@RunWith(SpringRunner.class)
// ApplicationContext will be loaded from TestConfig
// and initialized by TestAppCtxInitializer
@ContextConfiguration(
    classes = TestConfig.class,
    initializers = TestAppCtxInitializer.class) 
public class MyTest {
    // class body...
}
````

您还可以完全省略 `@IntextConfiguration` 中的 XML 配置文件，Groovy 脚本或注解修饰的类的声明，而是仅声明 `ApplicationContextInitializer` 类，然后负责在上下文中注册 bean  - 例如，通过以编程方式加载 bean XML 文件或配置类中的定义。以下示例显示了如何执行此操作：

````java
@RunWith(SpringRunner.class)
// ApplicationContext will be initialized by EntireAppInitializer
// which presumably registers beans in the context
@ContextConfiguration(initializers = EntireAppInitializer.class) 
public class MyTest {
    // class body...
}
````

##### 上下文配置继承

`@ContextConfiguration` 支持 boolean 类型的 ` inheritLocations` 和 `inheritInitializers` 属性，这些属性表示是否应继承超类声明的资源位置或注解修饰的类和上下文初始化器。两个标志的默认值是 `true`。这意味着测试类继承资源位置或注解修饰的类以及任何超类声明的上下文初始化器。具体而言，测试类的资源位置或注解修饰的类将附加到超类声明的资源位置列表或注解修饰的类。类似地，给定测试类的初始化器被添加到由测试超类定义的初始化器集中。因此，子类可以选择扩展资源位置，注解修饰的类或上下文初始化器。

如果 `@IntextConfiguration` 中的 `inheritLocations` 或 `inheritInitializers` 属性设置为 `false`，则测试类的资源位置或注解修饰的类和上下文初始化器分别替换超类定义的配置。

在下一个使用 XML 资源位置的示例中，`ExtendedTest` 的 `ApplicationContext` 按顺序从 `base-config.xml` 和 `extended-config.xml` 加载。因此，`extended-config.xml` 中定义的 bean 可以覆盖（即替换）`base-config.xml` 中定义的 bean。以下示例显示了一个类如何扩展另一个类并使用其自己的配置文件和超类的配置文件：

````java
@RunWith(SpringRunner.class)
// ApplicationContext will be loaded from "/base-config.xml"
// in the root of the classpath
@ContextConfiguration("/base-config.xml") 
public class BaseTest {
    // class body...
}

// ApplicationContext will be loaded from "/base-config.xml" and
// "/extended-config.xml" in the root of the classpath
@ContextConfiguration("/extended-config.xml") 
public class ExtendedTest extends BaseTest {
    // class body...
}
````

类似地，在下一个使用注解修饰的类的示例中，`ExtendedTest` 的 `ApplicationContext` 按顺序从 `BaseConfig` 和 `ExtendedConfig` 类加载。因此，在 `ExtendedConfig` 中定义的 Bean 可以覆盖（即替换）在 `BaseConfig` 中定义的那些。以下示例显示了一个类如何扩展另一个类并使用它自己的配置类和超类的配置类：

````java
@RunWith(SpringRunner.class)
// ApplicationContext will be loaded from BaseConfig
@ContextConfiguration(classes = BaseConfig.class) 
public class BaseTest {
    // class body...
}

// ApplicationContext will be loaded from BaseConfig and ExtendedConfig
@ContextConfiguration(classes = ExtendedConfig.class) 
public class ExtendedTest extends BaseTest {
    // class body...
}
````

在下一个使用上下文初始化器的示例中，使用 `BaseInitializer` 和 `ExtendedInitializer` 初始化 `ExtendedTest` 的 `ApplicationContext`。但是请注意，调用初始化器的顺序取决于它们是否实现了 Spring 的 `Ordered` 接口，或者是使用 Spring 的 `@Order` 注解还是标准的 `@Priority` 注解进行注释。以下示例显示了一个类如何扩展另一个类并使用它自己的初始化器和超类的初始化器：

````java
@RunWith(SpringRunner.class)
// ApplicationContext will be initialized by BaseInitializer
@ContextConfiguration(initializers = BaseInitializer.class) 
public class BaseTest {
    // class body...
}

// ApplicationContext will be initialized by BaseInitializer
// and ExtendedInitializer
@ContextConfiguration(initializers = ExtendedInitializer.class) 
public class ExtendedTest extends BaseTest {
    // class body...
}
````

##### 使用环境配置进行上下文配置

Spring 3.1在框架中引入了环境和配置文件概念（AKA “bean定义配置文件”）的第一类支持，并且可以配置集成测试以激活各种测试场景的特定 bean 定义配置文件。这是通过使用 `@ActiveProfiles` 注解注释测试类并提供在加载测试的 `ApplicationContext` 时应该激活的配置文件列表来实现的。

> 您可以将 `@ActiveProfiles` 用于新的 `SmartContextLoader` SPI 的任何实现，但是旧的 `ContextLoader`  SPI 的实现不支持 `@ActiveProfiles`。

考虑两个使用 XML 配置和 `@Configuration` 类的示例：

````xml
<!-- app-config.xml -->
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:jdbc="http://www.springframework.org/schema/jdbc"
    xmlns:jee="http://www.springframework.org/schema/jee"
    xsi:schemaLocation="...">

    <bean id="transferService"
            class="com.bank.service.internal.DefaultTransferService">
        <constructor-arg ref="accountRepository"/>
        <constructor-arg ref="feePolicy"/>
    </bean>

    <bean id="accountRepository"
            class="com.bank.repository.internal.JdbcAccountRepository">
        <constructor-arg ref="dataSource"/>
    </bean>

    <bean id="feePolicy"
        class="com.bank.service.internal.ZeroFeePolicy"/>

    <beans profile="dev">
        <jdbc:embedded-database id="dataSource">
            <jdbc:script
                location="classpath:com/bank/config/sql/schema.sql"/>
            <jdbc:script
                location="classpath:com/bank/config/sql/test-data.sql"/>
        </jdbc:embedded-database>
    </beans>

    <beans profile="production">
        <jee:jndi-lookup id="dataSource" jndi-name="java:comp/env/jdbc/datasource"/>
    </beans>

    <beans profile="default">
        <jdbc:embedded-database id="dataSource">
            <jdbc:script
                location="classpath:com/bank/config/sql/schema.sql"/>
        </jdbc:embedded-database>
    </beans>

</beans>
````

````java
package com.bank.service;

@RunWith(SpringRunner.class)
// ApplicationContext will be loaded from "classpath:/app-config.xml"
@ContextConfiguration("/app-config.xml")
@ActiveProfiles("dev")
public class TransferServiceTest {

    @Autowired
    private TransferService transferService;

    @Test
    public void testTransferService() {
        // test the transferService
    }
}
````

当运行 `TransferServiceTest` 时，它的 `ApplicationContext` 是从类路径根目录中的 `app-config.xml` 配置文件加载的。如果你检查 `app-config.xml`，你会发现 `accountRepository`  bean依赖于 `dataSource` bean。但是，`dataSource` 未定义为顶级 bean。相反，`dataSource` 定义了三次：在 `production` 配置文件中，在 `dev` 配置文件中，以及在`default` 配置文件中。

通过使用 `@ActiveProfiles("dev")` 注解修饰 `TransferServiceTest`，我们指示 Spring TestContext Framework 加载 `ApplicationContext`，并将活动的配置文件设置为 `{"dev"}`。因此，创建嵌入式数据库并使用测试数据进行填充，并将 `accountRepository` bean 连接到对开发 `DataSource` 的引用。这可能是我们在集成测试中想要的。

将 bean 分配给 `default` 配置文件有时很有用。仅当没有专门激活其他配置文件时，才会包含默认配置文件中的 Bean。您可以使用它来定义要在应用程序的默认状态中使用的“降级” bean。例如，您可以显式地为 `dev` 和 `production` 配置文件提供数据源，但是当这两个配置文件都不活动时，将内存数据源定义为默认值。

以下代码清单演示了如何使用 `@Configuration` 类而不是 XML 实现相同的配置和集成测试：

````java
@Configuration
@Profile("dev")
public class StandaloneDataConfig {

    @Bean
    public DataSource dataSource() {
        return new EmbeddedDatabaseBuilder()
            .setType(EmbeddedDatabaseType.HSQL)
            .addScript("classpath:com/bank/config/sql/schema.sql")
            .addScript("classpath:com/bank/config/sql/test-data.sql")
            .build();
    }
}
````

````java
@Configuration
@Profile("production")
public class JndiDataConfig {

    @Bean(destroyMethod="")
    public DataSource dataSource() throws Exception {
        Context ctx = new InitialContext();
        return (DataSource) ctx.lookup("java:comp/env/jdbc/datasource");
    }
}
````

````java
@Configuration
@Profile("default")
public class DefaultDataConfig {

    @Bean
    public DataSource dataSource() {
        return new EmbeddedDatabaseBuilder()
            .setType(EmbeddedDatabaseType.HSQL)
            .addScript("classpath:com/bank/config/sql/schema.sql")
            .build();
    }
}
````

````java
@Configuration
public class TransferServiceConfig {

    @Autowired DataSource dataSource;

    @Bean
    public TransferService transferService() {
        return new DefaultTransferService(accountRepository(), feePolicy());
    }

    @Bean
    public AccountRepository accountRepository() {
        return new JdbcAccountRepository(dataSource);
    }

    @Bean
    public FeePolicy feePolicy() {
        return new ZeroFeePolicy();
    }

}
````

````java
package com.bank.service;

@RunWith(SpringRunner.class)
@ContextConfiguration(classes = {
        TransferServiceConfig.class,
        StandaloneDataConfig.class,
        JndiDataConfig.class,
        DefaultDataConfig.class})
@ActiveProfiles("dev")
public class TransferServiceTest {

    @Autowired
    private TransferService transferService;

    @Test
    public void testTransferService() {
        // test the transferService
    }
}
````

在这个变体中，我们将 XML 配置拆分为四个独立的 `@Configuration` 类：

 - `TransferServiceConfig`：使用 `@Autowired` 通过依赖注入获取 `dataSource`。
 - `StandaloneDataConfig`：为适用于开发人员测试的嵌入式数据库定义 `dataSource`。
 - `JndiDataConfig`：定义在生产环境中从 JNDI 检索的 `dataSource`。
 - `DefaultDataConfig`：为默认的嵌入式数据库定义 `dataSource`，以防没有配置文件处于活动状态。

与基于 XML 的配置示例一样，我们仍然使用 `@ActiveProfiles("dev")` 注解修释 `TransferServiceTest`，但这次我们使用 `@ContextConfiguration` 注解指定所有四个配置类。测试类的主体本身保持完全不变。

通常情况下，在给定项目中的多个测试类中使用单组配置文件。因此，为了避免重复声明 `@ActiveProfiles` 注解，可以在基类上声明一次 `@ActiveProfiles`，子类自动从基类继承 `@ActiveProfiles` 配置。在下面的示例中，`@ActiveProfiles`（以及其他注解）的声明已被移动到抽象超类，`AbstractIntegrationTest`：

````java
package com.bank.service;

@RunWith(SpringRunner.class)
@ContextConfiguration(classes = {
        TransferServiceConfig.class,
        StandaloneDataConfig.class,
        JndiDataConfig.class,
        DefaultDataConfig.class})
@ActiveProfiles("dev")
public abstract class AbstractIntegrationTest {
}
````

````java
package com.bank.service;

// "dev" profile inherited from superclass
public class TransferServiceTest extends AbstractIntegrationTest {

    @Autowired
    private TransferService transferService;

    @Test
    public void testTransferService() {
        // test the transferService
    }
}
````

`@ActiveProfiles` 还支持 `inheritProfiles` 属性，可用于禁用活动配置文件的继承，如以下示例所示：

````java
package com.bank.service;

// "dev" profile overridden with "production"
@ActiveProfiles(profiles = "production", inheritProfiles = false)
public class ProductionTransferServiceTest extends AbstractIntegrationTest {
    // test body
}
````

此外，有时需要以编程方式而不是声明性地解析测试的活动配置文件 - 例如，基于：

 - 当前的操作系统。
 - 是否在持续集成构建服务器上执行测试。
 - 存在某些环境变量。
 - 存在自定义类级注解。
 - 其他问题。

要以编程方式解析活动 Bean 定义概要文件，您可以实现自定义 `ActiveProfilesResolver` 并使用 `@ActiveProfiles` 的 `resolver` 属性进行注册。有关详细信息，请参阅相应的 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/ActiveProfilesResolver.html) 。以下示例演示如何实现和注册自定义 `OperatingSystemActiveProfilesResolver`：

````java
package com.bank.service;

// "dev" profile overridden programmatically via a custom resolver
@ActiveProfiles(
    resolver = OperatingSystemActiveProfilesResolver.class,
    inheritProfiles = false)
public class TransferServiceTest extends AbstractIntegrationTest {
    // test body
}
````

````java
package com.bank.service.test;

public class OperatingSystemActiveProfilesResolver implements ActiveProfilesResolver {

    @Override
    String[] resolve(Class<?> testClass) {
        String profile = ...;
        // determine the value of profile based on the operating system
        return new String[] {profile};
    }
}
````

##### 使用测试属性源进行上下文配置

Spring 3.1在框架中引入了具有属性源层次结构的环境概念的第一类支持。从 Spring 4.1 开始，您可以使用特定于测试的属性源配置集成测试。与 `@Configuration` 类上使用的 `@PropertySource` 注解相比，您可以在测试类上声明 `@TestPropertySource` 注解，以声明测试属性文件或内联属性的资源位置。这些测试属性源被添加到 `Environment` 中的 `PropertySources` 集合中，用于为注解的集成测试加载的 `ApplicationContext`。

> 你可以使用 `@TestPropertySource` 和 `SmartContextLoader` SPI 的任何实现，但是旧的 `ContextLoader`  SPI 的实现不支持 `@TestPropertySource`。
>
> `SmartContextLoader` 的实现通过 `MergedContextConfiguration` 中的 `getPropertySourceLocations()` 和 `getPropertySourceProperties()` 方法获得对合并的测试属性源值的访问。

###### 声明测试属性源

您可以使用 `@TestPropertySource` 的 `locations` 或 `value` 属性配置测试属性文件。

支持传统和基于 XML 的属性文件格式 - 例如，`"classpath:/com/example/test.properties"` 或 `"file:///path/to/file.xml"`。

每条路径都被解释为 Spring `Resources`。普通路径（例如，`"test.properties"`）被视为相对于定义测试类的包的类路径资源。以斜杠开头的路径被视为绝对类路径资源（例如：`"/org/example/test.xml"`）。引用 URL 的路径（例如，前缀为 `classpath:`，`file:` 或 `http:` 的路径）通过使用指定的资源协议加载。不允许使用资源位置通配符（例如 `***/**.properties`）：每个位置必须只对应一个 `.properties` 或 `.xml` 资源。

以下示例使用测试属性文件：

````java
@ContextConfiguration
@TestPropertySource("/test.properties") 
public class MyIntegrationTests {
    // class body...
}
````

您可以使用 `@TestPropertySource` 的 `properties` 属性以键值对的形式配置内联属性，如下一个示例所示。所有键值对都被添加到封闭的 `Environment` 中，作为具有最高优先级的单个测试 `PropertySource`。

键值对支持的语法与为 Java 属性文件中的条目定义的语法相同：

- `key=value`
- `key:value`
- `key value`

以下示例设置两个内联属性：

````java
@ContextConfiguration
@TestPropertySource(properties = {"timezone = GMT", "port: 4242"}) 
public class MyIntegrationTests {
    // class body...
}
````

###### 默认属性文件探测

如果 `@TestPropertySource` 被声明为空注解（即，没有 `locations` 或 `properties` 属性的显式值），则尝试检测相对于声明注解的类的默认属性文件。例如，如果注解修饰的测试类是 `com.example.MyTest`，则相应的默认属性文件是 `classpath:com/example/MyTest.properties`。如果无法检测到默认值，则抛出 `IllegalStateException`。

###### 优先级

测试属性源的优先级高于从操作系统环境，Java 系统属性或应用程序通过使用 `@PropertySource` 或以编程方式声明性地添加的属性源的优先级。因此，测试属性源可用于有选择地覆盖系统和应用程序属性源中定义的属性。此外，内联属性的优先级高于从资源位置加载的属性。

在下一个示例中，`timezone` 和 `port` 属性以及 `"/test.properties"` 中定义的任何属性都会覆盖在系统和应用程序属性源中定义的同名属性。此外，如果 `/test.properties` 文件定义 `timezone` 和 `port` 属性的条目，那么这些属性将被使用 `properties` 属性声明的内联属性覆盖。以下示例显示如何在文件和内联中指定属性：

````java
@ContextConfiguration
@TestPropertySource(
    locations = "/test.properties",
    properties = {"timezone = GMT", "port: 4242"}
)
public class MyIntegrationTests {
    // class body...
}
````

###### 继承和覆盖测试属性源

`@TestPropertySource` 支持 boolean 类型的 ` inheritLocations` 和 `inheritProperties` 属性，这些属性表示属性文件的资源位置和超类声明的内联属性是否应该被继承。两个标志的默认值是 `true`。这意味着测试类继承了任何超类声明的位置和内联属性。具体而言，测试类的位置和内联属性将附加到超类声明的位置和内联属性。因此，子类可以选择扩展位置和内联属性。请注意，稍后出现的属性会影响（即覆盖）先前出现的同名属性。此外，上述优先规则也适用于继承的测试属性源。

如果 `@TestPropertySource` 中的 `inheritLocations` 或 `inheritProperties` 属性设置为 `false`，则测试类的位置或内联属性分别影响并有效地替换超类定义的配置。

在下一个例子中，只使用 `base.properties` 文件作为测试属性源加载 `BaseTest` 的 `ApplicationContext`。相反，使用 `base.properties` 和 `extended.properties` 文件作为测试属性源位置来加载 `ExtendedTest` 的 `ApplicationContext`。以下示例显示如何使用 `properties` 文件在子类及其超类中定义属性：

````java
@TestPropertySource("base.properties")
@ContextConfiguration
public class BaseTest {
    // ...
}

@TestPropertySource("extended.properties")
@ContextConfiguration
public class ExtendedTest extends BaseTest {
    // ...
}
````

在下一个示例中，仅使用内联的 `key1` 属性加载 `BaseTest` 的 `ApplicationContext`。相反，`ExtendedTest` 的 `ApplicationContext` 是使用内联的 `key1` 和 `key2` 属性加载的。以下示例显示如何使用内联属性在子类及其超类中定义属性：

````java
@TestPropertySource(properties = "key1 = value1")
@ContextConfiguration
public class BaseTest {
    // ...
}

@TestPropertySource(properties = "key2 = value2")
@ContextConfiguration
public class ExtendedTest extends BaseTest {
    // ...
}
````

##### 加载 `WebApplicationContext`

Spring 3.2 引入了对在集成测试中加载 `WebApplicationContext` 的支持。要指示 TestContext 框架加载 `WebApplicationContext` 而不是标准的 `ApplicationContext`，您可以使用 `@WebAppConfiguration` 注解修饰相应的测试类。

测试类上存在 `@WebAppConfiguration` ，指示 TestContext 框架（TCF）应为您的集成测试加载 `WebApplicationContext`（WAC）。在后台，TCF 确保创建一个 `MockServletContext` 并提供给测试的 WAC。默认情况下，`MockServletContext` 的基本资源路径设置为 `src/main/webapp`。这被解释为相对于 JVM 根目录的路径（通常是项目的路径）。如果您熟悉 Maven 项目中 Web 应用程序的目录结构，您就知道 `src/main/webapp` 是 WAR 根目录的默认位置。如果需要覆盖此缺省值，则可以提供 `@WebAppConfiguration` 注解的备用路径（例如，`@WebAppConfiguration("src/test/webapp")`）。如果您希望从类路径而不是文件系统引用基本资源路径，则可以使用 Spring 的 `classpath:` 前缀。

请注意，Spring 对 `WebApplicationContext` 实现的测试支持与其对标准 `ApplicationContext` 实现的支持相同。使用 `WebApplicationContext` 进行测试时，可以使用 `@ContextConfiguration` 自由声明 XML 配置文件，Groovy 脚本或 `@Configuration` 类。您也可以自由使用任何其他测试注解，例如 `@ActiveProfiles`，`@TestExecutionListeners`，`@Sql`，`@Rollback`等。

本节中的其余示例显示了用于加载 `WebApplicationContext` 的一些配置选项。以下示例显示了 TestContext 框架对约定优于配置的支持：

示例 1. 约定

````java
@RunWith(SpringRunner.class)

// defaults to "file:src/main/webapp"
@WebAppConfiguration

// detects "WacTests-context.xml" in the same package
// or static nested @Configuration classes
@ContextConfiguration

public class WacTests {
    //...
}
````

如果使用 `@WebAppConfiguration` 注解测试类而未指定资源基路径，则资源路径有效地默认为 `file:src/main/ webapp`。类似地，如果你声明 `@IntextConfiguration` 而没有指定资源 `locations`，带注解的 `classes` 或上下文 `initializers`，Spring 会尝试使用约定来检测你的配置是否存在（即 `WacTests-context.xml` 在与 `WacTests` 类或静态嵌套 `@Configuration` 类相同的包中。

以下示例说明如何使用 `@WebAppConfiguration` 显式声明资源基路径，并使用 `@ContextConfiguration` 显式声明 XML 资源位置：

示例 2. 默认资源语义

````java
@RunWith(SpringRunner.class)

// file system resource
@WebAppConfiguration("webapp")

// classpath resource
@ContextConfiguration("/spring/test-servlet-config.xml")

public class WacTests {
    //...
}
````

这里要注意的重要一点是具有这两个注解的路径的不同语义。默认情况下，`@WebAppConfiguration` 资源路径是基于文件系统的，而 `@IntextConfiguration` 资源位置是基于类路径的。

以下示例显示我们可以通过指定 Spring 资源前缀来覆盖两个注解的默认资源语义：

示例 3. 显式资源语义

````java
@RunWith(SpringRunner.class)

// classpath resource
@WebAppConfiguration("classpath:test-web-resources")

// file system resource
@ContextConfiguration("file:src/main/webapp/WEB-INF/servlet-config.xml")

public class WacTests {
    //...
}
````

将此示例中的注解与前一个示例进行对比。

*使用 Web Mocks*

为了提供全面的 Web 测试支持，Spring 3.2 引入了一个默认启用的 `ServletTestExecutionListener`。当针对一个 `WebApplicationContext`，此 [`TestExecutionListener`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-key-abstractions)  在每个测试方法之前使用 Spring Web 的 `RequestContextHolder` 设置默认的线程局部状态，并根据用 `@WebAppConfiguration` 配置的基本资源路径创建一个 `MockHttpServletRequest`，一个 `MockHttpServletResponse` 和一个 `ServletWebRequest`。 `ServletTestExecutionListener` 还确保可以将 `MockHttpServletResponse` 和 `ServletWebRequest` 注入到测试实例中，并且一旦测试完成，它就会清除线程本地状态。

一旦为测试加载了 `WebApplicationContext`，您可能会发现需要与 Web 模拟进行交互 - 例如，设置测试夹具或在调用 Web 组件后执行断言。以下示例显示可以将哪些模拟自动装配到测试实例中。请注意，`WebApplicationContext` 和 `MockServletContext` 都在测试套件中缓存，而其他模拟由 `ServletTestExecutionListener` 按照测试方法进行管理。

示例 4. 注入模拟

````java
@WebAppConfiguration
@ContextConfiguration
public class WacTests {

    @Autowired
    WebApplicationContext wac; // cached

    @Autowired
    MockServletContext servletContext; // cached

    @Autowired
    MockHttpSession session;

    @Autowired
    MockHttpServletRequest request;

    @Autowired
    MockHttpServletResponse response;

    @Autowired
    ServletWebRequest webRequest;

    //...
}
````

##### 上下文缓存

一旦 TestContext 框架为测试加载 `ApplicationContext`（或 `WebApplicationContext`），该上下文就会被缓存并重用于在同一测试套件中声明相同唯一上下文配置的所有后续测试。要了解缓存的工作原理，了解“独特”和“测试套件”的含义非常重要。

可以通过用于加载它的配置参数的组合唯一地标识 `ApplicationContext`。因此，配置参数的唯一组合用于生成用于缓存上下文的键。TestContext 框架使用以下配置参数来构建上下文缓存键：

- `locations` (来自 `@ContextConfiguration`)
- `classes` (来自 `@ContextConfiguration`)
- `contextInitializerClasses` (来自 `@ContextConfiguration`)
- `contextCustomizers` (来自 `ContextCustomizerFactory`)
- `contextLoader` (来自 `@ContextConfiguration`)
- `parent` (来自 `@ContextHierarchy`)
- `activeProfiles` (来自 `@ActiveProfiles`)
- `propertySourceLocations` (来自 `@TestPropertySource`)
- `propertySourceProperties` (来自 `@TestPropertySource`)
- `resourceBasePath` (来自 `@WebAppConfiguration`)

例如，如果 `TestClassA` 为 `@ContextConfiguration` 的 `locations`（或 `value`）属性指定 `{"app-config.xml", "test-config.xml"}`，则 TestContext 框架加载对应的 `ApplicationContext` 并将其存储在仅基于这些位置的键下的 `static` 上下文缓存中。因此，如果 `TestClassB` 还为其位置定义了 `{"app-config.xml", "test-config.xml"}`（通过继承显式或隐式），但没有定义 `@WebAppConfiguration`，则不同的 ` ContextLoader`，不同的活动配置文件，不同的上下文初始化器，不同的测试属性源或不同的父上下文，然后两个测试类共享相同的 `ApplicationContext`。这意味着加载应用程序上下文的设置成本仅产生一次（每个测试套件），并且后续测试执行要快得多。

> 测试套件和分支流程
>
> Spring TestContext 框架将应用程序上下文存储在静态缓存中。这意味着上下文实际上存储在 `static` 变量中。换句话说，如果测试在单独的进程中执行，则在每次测试执行之间清除静态高速缓存，这有效地禁用了高速缓存机制。
>
> 要从缓存机制中受益，所有测试必须在同一进程或测试套件中运行。这可以通过在 IDE 中作为一个组执行所有测试来实现。类似地，当使用诸如 Ant，Maven 或 Gradle 之类的构建框架执行测试时，确保构建框架不在测试之间进行分支是很重要的。例如，如果 Maven Surefire 插件的 [`forkMode`](https://maven.apache.org/plugins/maven-surefire-plugin/test-mojo.html#forkMode) 设置为 `always` 或者 `pertest`，TestContext 框架无法在测试类之间缓存应用程序上下文，因此构建过程运行速度明显更慢。

从 Spring Framework 4.3 开始，上下文缓存的大小受限于默认的最大大小 32 。每当达到最大大小时，最近最少使用（LRU）淘汰策略用于淘汰和关闭过时的上下文。您可以通过设置名为 `spring.test.context.cache.maxSize` 的 JVM 系统属性，从命令行或构建脚本配置最大大小。或者，您可以使用 `SpringProperties` API 以编程方式设置相同的属性。

由于在给定的测试套件中加载大量应用程序上下文会导致套件执行不必要的长时间，因此确切地知道已加载和缓存了多少上下文通常是有益的。要查看基础上下文缓存的统计信息，可以将 `org.springframework.test.context.cache` 日志记录类别的日志级别设置为 `DEBUG`。

在某些特殊的情况下，测试会破坏应用程序上下文并需要重新加载（例如，通过修改 bean 定义或应用程序对象的状态），您可以使用 `@DirtiesContext` 注解测试类或测试方法（请参阅在 [`@DirtiesContext`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-dirtiescontext) 中的 `@DirtiesContext` 的讨论）。这指示 Spring 在运行需要相同应用程序上下文的下一个测试之前从缓存中删除上下文并重建应用程序上下文。请注意，`@DirtiesContext` 注解的支持由 `DirtiesContextBeforeModesTestExecutionListener` 和 `DirtiesContextTestExecutionListener` 提供，它们默认启用。

##### 上下文层级结构

在编写依赖于已加载的 Spring `ApplicationContext` 的集成测试时，通常可以针对单个上下文进行测试。但是，有时候在 `ApplicationContext` 实例的层次结构中进行测试是有益的，甚至是必要的。例如，如果您正在开发 Spring MVC Web 应用程序，那么您通常会有一个由 Spring 的 `ContextLoaderListener` 加载的根 `WebApplicationContext` 和一个由 Spring 的 `DispatcherServlet` 加载的子 `WebApplicationContext`。这将生成父子上下文层次结构，其中共享组件和基础结构配置在根上下文中声明，并由特定于 Web 的组件在子上下文中使用。可以在 Spring Batch 应用程序中找到另一个用例，其中您经常有一个父上下文，它提供共享批处理基础结构的配置，以及一个用于配置特定批处理作业的子上下文。

从 Spring Framework 3.2.2 开始，您可以编写使用上下文层次结构的集成测试，方法是在单个测试类或测试类层次结构中使用 `@ContextHierarchy` 注解声明上下文配置。如果在测试类层次结构中的多个类上声明了上下文层次结构，则还可以合并或覆盖上下文层次结构中特定的命名级别的上下文配置。合并层次结构中给定级别的配置时，配置资源类型（即 XML 配置文件或带注解的类）必须一致。否则，在使用不同资源类型配置的上下文层次结构中具有不同级别是完全可以接受的。

本节中剩余的基于 JUnit 4 的示例显示了需要使用上下文层次结构的集成测试的常见配置方案。

*使用上下文层级结构的单个测试类*

`ControllerIntegrationTests` 表示 Spring MVC Web 应用程序的典型集成测试场景，它声明了一个由两个级别组成的上下文层次结构，一个用于根 `WebApplicationContext`（使用 `TestAppConfig` `@Configuration` 类加载），另一个用于调度servlet `WebApplicationContext`（使用 `WebConfig` `@Configuration` 类加载）。自动装配到测试实例中的 `WebApplicationContext` 是子上下文（即层次结构中最低的上下文）。以下清单显示了此配置方案：

````java
@RunWith(SpringRunner.class)
@WebAppConfiguration
@ContextHierarchy({
    @ContextConfiguration(classes = TestAppConfig.class),
    @ContextConfiguration(classes = WebConfig.class)
})
public class ControllerIntegrationTests {

    @Autowired
    private WebApplicationContext wac;

    // ...
}
````

*具有隐式父上下文的类层次结构*

此示例中的测试类定义测试类层次结构中的上下文层次结构。 `AbstractWebTests` 在 Spring 驱动的 Web 应用程序中声明了根 `WebApplicationContext` 的配置。但请注意，`AbstractWebTests` 不会声明`@ContextHierarchy`。因此，`AbstractWebTests` 的子类可以选择参与上下文层次结构或遵循 `@ContextConfiguration` 的标准语义。 `SoapWebServiceTests` 和 `RestWebServiceTests` 都扩展了 `AbstractWebTests` 并使用 `@ContextHierarchy` 定义了一个上下文层次结构。结果是加载了三个应用程序上下文（一个用于 `@ContextConfiguration` 的每个声明），并且基于 `AbstractWebTests` 中的配置加载的应用程序上下文被设置为为具体子类加载的每个上下文的父上下文。以下清单显示了此配置方案：

````java
@RunWith(SpringRunner.class)
@WebAppConfiguration
@ContextConfiguration("file:src/main/webapp/WEB-INF/applicationContext.xml")
public abstract class AbstractWebTests {}

@ContextHierarchy(@ContextConfiguration("/spring/soap-ws-config.xml")
public class SoapWebServiceTests extends AbstractWebTests {}

@ContextHierarchy(@ContextConfiguration("/spring/rest-ws-config.xml")
public class RestWebServiceTests extends AbstractWebTests {}
````

*具有合并的上下文层次结构配置的类层次*

此示例中的类显示了命名层次结构级别的使用，以便合并上下文层次结构中特定级别的配置。 `BaseTests` 在层次结构中定义了两个级别，`parent` 和 `child`。 `ExtendedTests` 扩展了 `BaseTests` 并指示 Spring TestContext Framework 合并 `child` 层次结构级别的上下文配置，确保在 `@IntextConfiguration` 中 `name` 属性中声明的名称都是 `child`。结果是加载了三个应用程序上下文：一个用于 `/app-config.xml`，一个用于 `/user-config.xml`，另一个用于 `{"/user-config.xml", "/order-config.xml"}`。与前面的示例一样，从 `/app-config.xml` 加载的应用程序上下文被设置为从 `/user-config.xml` 和 `{"/user-config.xml", "/order-config.xml"}` 加载的上下文的父上下文。以下清单显示了此配置方案：

````java
@RunWith(SpringRunner.class)
@ContextHierarchy({
    @ContextConfiguration(name = "parent", locations = "/app-config.xml"),
    @ContextConfiguration(name = "child", locations = "/user-config.xml")
})
public class BaseTests {}

@ContextHierarchy(
    @ContextConfiguration(name = "child", locations = "/order-config.xml")
)
public class ExtendedTests extends BaseTests {}
````

*具有重写的上下文层次结构配置的类层次结构*

与前面的示例相比，此示例演示了如何通过将 `@ContextConfiguration` 中的 `inheritLocations` 标志设置为 `false` 来覆盖上下文层次结构中给定命名级别的配置。因此，`ExtendedTests` 的应用程序上下文仅从 `/test-user-config.xml` 加载，并将其父设置为从 `/app-config.xml` 加载的上下文。以下清单显示了此配置方案：

````java
@RunWith(SpringRunner.class)
@ContextHierarchy({
    @ContextConfiguration(name = "parent", locations = "/app-config.xml"),
    @ContextConfiguration(name = "child", locations = "/user-config.xml")
})
public class BaseTests {}

@ContextHierarchy(
    @ContextConfiguration(
        name = "child",
        locations = "/test-user-config.xml",
        inheritLocations = false
))
public class ExtendedTests extends BaseTests {}
````

> 在上下文层次结构中清理上下文
> 如果在其上下文配置为上下文层次结构的一部分的测试中使用 `@DirtiesContext`，则可以使用 `hierarchyMode` 标志来控制如何清除上下文高速缓存。有关更多详细信息，请参阅 [Spring Testing Annotations](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#spring-testing-annotation-dirtiescontext) 中的 `@DirtiesContext` 和 [`@DirtiesContext`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/annotation/DirtiesContext.html)  javadoc 的讨论。

#### 3.5.5. 测试夹具的依赖注入

当您使用 `DependencyInjectionTestExecutionListener`（默认配置）时，测试实例的依赖项将从您使用 `@ContextConfiguration` 或相关注解配置的应用程序上下文中的 bean 中注入。您可以使用 setter injection，field injection 或同时使用两者，具体取决于您选择的注解以及是否将它们放在 setter 方法或字段上。如果您正在使用 JUnit Jupiter，您也可以选择使用构造函数注入（请参阅 [使用 `SpringExtension` 的依赖注入](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-junit-jupiter-di) ）。为了与 Spring 的基于注解的注入支持保持一致，您还可以使用 Spring 的 `@Autowired` 注解或来自 JSR-330 的 `@Inject` 注解来进行字段和 setter 注入。

> 对于 JUnit Jupiter 以外的测试框架，TestContext 框架不参与测试类的实例化。因此，对构造函数使用 `@Autowired` 或 `@Inject` 对测试类没有影响。

> 虽然在生产代码中不鼓励字段注入，但字段注入在测试代码中实际上非常自然。差异的基本原理是您永远不会直接实例化您的测试类。因此，不需要在测试类上调用 `public` 构造函数或 setter 方法。

因为 `@Autowired` 用于执行 [按类型自动装配](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-factory-autowire ) ，如果你有多个相同类型的 bean 定义，你不能依赖这种方法来处理那些特定的 bean。在这种情况下，您可以将 `@Autowired` 与 `@ Qualifier` 结合使用。从 Spring 3.0 开始，您还可以选择将 `@Inject` 与 `@ Named` 结合使用。或者，如果您的测试类可以访问其 `ApplicationContext`，则可以使用（例如）调用 `applicationContext.getBean("titleRepository", TitleRepository.class)` 来执行显式查找。

如果您不希望将依赖项注入应用于测试实例，请不要使用 `@Autowired` 或 `@Inject` 注解字段或 setter 方法。或者，您可以通过使用 `@TestExecutionListeners` 显式配置您的类并从侦听器列表中省略 `DependencyInjectionTestExecutionListener.class` 来完全禁用依赖注入。

考虑测试 `HibernateTitleRepository` 类的场景，如 [目标](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-goals) 部分中所述。接下来的两个代码清单演示了在字段和 setter 方法中使用 `@Autowired`。在所有示例代码列表之后给出应用程序上下文配置。

> 以下代码清单中的依赖项注入行为并非特定于 JUnit 4。相同的 DI 技术可与任何支持的测试框架结合使用。
>
> 以下示例调用静态断言方法，例如 `assertNotNull()`，但不使用 `Assert` 进行调用。在这种情况下，假设该方法是通过示例中未显示的 `import static` 声明正确导入的。

第一个代码清单显示了一个基于 JUnit 4 的测试类实现，它使用 `@Autowired` 进行字段注入：

````java
@RunWith(SpringRunner.class)
// specifies the Spring configuration to load for this test fixture
@ContextConfiguration("repository-config.xml")
public class HibernateTitleRepositoryTests {

    // this instance will be dependency injected by type
    @Autowired
    private HibernateTitleRepository titleRepository;

    @Test
    public void findById() {
        Title title = titleRepository.findById(new Long(10));
        assertNotNull(title);
    }
}
````

或者，您可以将类配置为使用 `@Autowired` 进行 setter 注入，如下所示：

````java
@RunWith(SpringRunner.class)
// specifies the Spring configuration to load for this test fixture
@ContextConfiguration("repository-config.xml")
public class HibernateTitleRepositoryTests {

    // this instance will be dependency injected by type
    private HibernateTitleRepository titleRepository;

    @Autowired
    public void setTitleRepository(HibernateTitleRepository titleRepository) {
        this.titleRepository = titleRepository;
    }

    @Test
    public void findById() {
        Title title = titleRepository.findById(new Long(10));
        assertNotNull(title);
    }
}
````

前面的代码清单使用 `@IntextConfiguration` 注解引用相同的 XML 上下文配置文件（即 `repository-config.xml`）。以下显示了此配置：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- this bean will be injected into the HibernateTitleRepositoryTests class -->
    <bean id="titleRepository" class="com.foo.repository.hibernate.HibernateTitleRepository">
        <property name="sessionFactory" ref="sessionFactory"/>
    </bean>

    <bean id="sessionFactory" class="org.springframework.orm.hibernate5.LocalSessionFactoryBean">
        <!-- configuration elided for brevity -->
    </bean>

</beans>
````

> 如果你从一个 Spring 提供的测试基类扩展，该类恰巧在其一个 setter 方法上使用 `@Autowired`，你可能在应用程序上下文中定义了多个受影响类型的 bean（例如，多个 `DataSource` bean）。在这种情况下，您可以覆盖 setter 方法并使用 `@Qualifier` 注解来指示特定的目标 bean，如下所示（但请确保也委托给超类中的重写方法）：
>
> ````java
> // ...
> 
>     @Autowired
>     @Override
>     public void setDataSource(@Qualifier("myDataSource") DataSource dataSource) {
>         super.setDataSource(dataSource);
>     }
> 
> // ...
> ````
>
> 指定的限定符值表示要注入的特定 `DataSource` bean，将类型匹配集缩小到特定 bean。它的值与相应的 `<bean>` 定义中的 `<qualifier>` 声明匹配。bean 名称用作"降级"限定符值，因此您可以有效地在那里按名称指向特定的 bean（如前所示，假设 `myDataSource` 是 bean `id`）。

#### 3.5.6. 测试请求和会话范围的Bean

Spring 从早年开始就支持 [请求和会话范围的bean](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-other) 。从 Spring 3.2 开始，您可以按照以下步骤测试请求范围和会话范围的 bean：

 - 确保通过使用 `@WebAppConfiguration` 注解测试类来为测试加载 `WebApplicationContext`。
 - 将模拟请求或会话注入测试实例，并根据需要准备测试夹具。
 - 调用从配置的 `WebApplicationContext` 中检索到的 Web 组件（具有依赖项注入）。
 - 对模拟执行断言。

下一个代码段显示了登录用例的 XML 配置。请注意，`userService` bean 依赖于请求范围的 `loginAction`  bean。此外，`LoginAction` 通过使用 [SpEL表达式](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/core.html#expressions) 来实例化，以检索来自当前 HTTP 请求的用户名和密码。在我们的测试中，我们希望通过 TestContext 框架管理的模拟配置这些请求参数。以下清单显示了此用例的配置：

*示例 5. 请求范围的 bean 配置*

````xml
<beans>

    <bean id="userService" class="com.example.SimpleUserService"
            c:loginAction-ref="loginAction"/>

    <bean id="loginAction" class="com.example.LoginAction"
            c:username="#{request.getParameter('user')}"
            c:password="#{request.getParameter('pswd')}"
            scope="request">
        <aop:scoped-proxy/>
    </bean>

</beans>
````

在 `RequestScopedBeanTests` 中，我们将 `UserService`（即被测试的主题）和 `MockHttpServletRequest` 注入我们的测试实例。在我们的 `requestScope()` 测试方法中，我们通过在提供的 `MockHttpServletRequest` 中设置请求参数来设置我们的测试夹具。当在我们的 `userService` 上调用 `loginUser()` 方法时，我们可以确保用户服务可以访问当前 `MockHttpServletRequest` 的请求范围的 `loginAction`（也就是我们刚设置的那个参数）。然后，我们可以根据用户名和密码的已知输入对结果执行断言。以下清单显示了如何执行此操作：

*示例 6. 请求范围的 bean 测试*

````java
@RunWith(SpringRunner.class)
@ContextConfiguration
@WebAppConfiguration
public class RequestScopedBeanTests {

    @Autowired UserService userService;
    @Autowired MockHttpServletRequest request;

    @Test
    public void requestScope() {
        request.setParameter("user", "enigma");
        request.setParameter("pswd", "$pr!ng");

        LoginResults results = userService.loginUser();
        // assert results
    }
}
````

以下代码片段类似于我们之前针对请求范围的 bean 看到的代码片段。但是，这次，`userService` bean依赖于会话范围的 `userPreferences` bean。请注意，`UserPreferences` bean是使用 SpEL 表达式实例化的，该表达式从当前 HTTP 会话中检索主题。在我们的测试中，我们需要在 TestContext 框架管理的模拟会话中配置主题。以下示例显示了如何执行此操作：

*示例 7. 会话范围的 bean 配置*

````xml
<beans>

    <bean id="userService" class="com.example.SimpleUserService"
            c:userPreferences-ref="userPreferences" />

    <bean id="userPreferences" class="com.example.UserPreferences"
            c:theme="#{session.getAttribute('theme')}"
            scope="session">
        <aop:scoped-proxy/>
    </bean>

</beans>
````

在 `SessionScopedBeanTests` 中，我们将 `UserService` 和 `MockHttpSession` 注入我们的测试实例。在我们的 `sessionScope()` 测试方法中，我们通过在提供的 `MockHttpSession` 中设置预期的 `theme` 属性来设置我们的测试夹具。当我们的 `userService` 上调用 `processUserPreferences()` 方法时，我们可以确保用户服务可以访问当前 `MockHttpSession` 的会话范围的 `userPreferences`，我们可以根据配置的主题对结果执行断言。以下示例显示了如何执行此操作：

*示例 8. 会话范围 bean 测试*

````java
@RunWith(SpringRunner.class)
@ContextConfiguration
@WebAppConfiguration
public class SessionScopedBeanTests {

    @Autowired UserService userService;
    @Autowired MockHttpSession session;

    @Test
    public void sessionScope() throws Exception {
        session.setAttribute("theme", "blue");

        Results results = userService.processUserPreferences();
        // assert results
    }
}
````

#### 3.5.7. 事务管理

在 TestContext 框架中，事务由 `TransactionalTestExecutionListener` 管理，默认情况下配置它，即使您没有在测试类上显式声明 `@TestExecutionListeners`。但是，要启用对事务的支持，必须在 `ApplicationContext` 中配置一个 `PlatformTransactionManager` bean，该 bean 加载了 `@ContextConfiguration` 语义（稍后会提供更多详细信息）。此外，您必须在类或方法级别为测试声明 Spring 的 `@Transactional` 注解。

##### 测试管理的事务

测试管理的事务是通过使用 `TransactionalTestExecutionListener` 以编程方式管理的事务，或者通过使用 `TestTransaction`（稍后描述）以编程方式管理的事务。您不应该将这些事务与 Spring 管理的事务（在为测试加载的 `ApplicationContext` 中直接由 Spring 管理的事务）或应用程序管理的事务（在测试调用的应用程序代码中以编程方式管理的事务）混淆。Spring 管理和应用程序管理的事务通常参与测试管理的事务。但是，如果 Spring 管理或应用程序管理的事务配置了除 `REQUIRED` 或 `SUPPORTS` 以外的任何传播类型，则应谨慎使用（请参阅[事务传播](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#tx-propagation) 获取有关详细信息）。

> *抢先超时和测试管理的事务*
>
> 当将来自测试框架的任何形式的抢先超时与 Spring 的测试管理事务结合使用时，必须小心。
>
> 具体来说，在调用当前测试方法之前，Spring 的测试支持将事务状态绑定到当前线程（通过 `java.lang.ThreadLocal` 变量）。如果测试框架在新线程中调用当前测试方法以支持抢占超时，则在测试管理的事务中将不会调用在当前测试方法中执行的任何操作。因此，任何此类操作的结果都不会与测试管理的事务一起回滚。相反，即使测试管理的事务由 Spring 正确回滚，这些操作也将被提交到持久存储 - 例如，关系数据库。
>
> 可能发生的情况包括但不限于以下情况。
>
>  -  JUnit 4 的 `@Test(timeout = ...)` 支持和 `TimeOut` 规则
>  -  JUnit Jupiter 在 `org.junit.jupiter.api.Assertions` 类中的 `assertTimeoutPreemptively(...)` 方法
>  -  TestNG 的 `@Test(timeOut = ...)` 支持

##### 开启和关闭事务

使用 `@Transactional` 注解修饰测试方法会导致测试在一个事务中运行，该事务默认情况下会在测试完成后自动回滚。如果测试类使用 `@Transactional` 注解修饰，则该类层次结构中的每个测试方法都在事务中运行。未使用 `@Transactional`（在类或方法级别）注解修饰的测试方法不在事务中运行。此外，使用 `@Transactional` 注解但将 `propagation` 类型设置为 `NOT_SUPPORTED` 的测试不在事务中运行。

注意 [`AbstractTransactionalJUnit4SpringContextTests`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-support-classes-junit4) 和 [`AbstractTransactionalTestNGSpringContextTests`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-support-classes-testng) 被预配置为在类级别支持事务。

下面的例子展示了一个常见的基于 Hibernate 的 `UserRepository` 的集成测试类：

````java
@RunWith(SpringRunner.class)
@ContextConfiguration(classes = TestConfig.class)
@Transactional
public class HibernateUserRepositoryTests {

    @Autowired
    HibernateUserRepository repository;

    @Autowired
    SessionFactory sessionFactory;

    JdbcTemplate jdbcTemplate;

    @Autowired
    public void setDataSource(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    @Test
    public void createUser() {
        // track initial state in test database:
        final int count = countRowsInTable("user");

        User user = new User(...);
        repository.save(user);

        // Manual flush is required to avoid false positive in test
        sessionFactory.getCurrentSession().flush();
        assertNumUsers(count + 1);
    }

    protected int countRowsInTable(String tableName) {
        return JdbcTestUtils.countRowsInTable(this.jdbcTemplate, tableName);
    }

    protected void assertNumUsers(int expected) {
        assertEquals("Number of rows in the [user] table.", expected, countRowsInTable("user"));
    }
}
````

如 [Transaction Rollback and Commit Behavior](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-tx-rollback-and-commit-behavior) 中所述，在 `createUser()` 方法运行之后没有必要清理数据库，因为所有对数据库的修改都会自动被 `TransactionalTestExecutionListener` 回滚。

##### 事务回滚和提交行为

默认情况下，测试事务将在测试执行完成之后自动回滚。不过，事务提交和回滚行为可以通过 `@Commit` 和 `@Rollback` 注解进行声明式配置。参考 [annotation support](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations) 部分中的相应内容获取更多细节。

##### 编程式事务管理

从 Spring Framework 4.1开始，你可以通过编程方式与测试管理的事务交互，使用 `static` 方法 `TestTransaction` 。比如，你可以在测试方法中，测试方法前，或者测试方法后使用 `TestTransaction` ，以开始活着结束当前测试管理的事务活着配置当前测试管理的事务的回滚或者提交行为。当 `TransactionalTestExecutionListener` 启用时对 `TestTransaction` 的支持自动可用。

下面的例子展示了 `TestTransaciton` 的一些特性。参考 [`TestTransaction`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/transaction/TestTransaction.html) 文档获取更多细节。

````java
@ContextConfiguration(classes = TestConfig.class)
public class ProgrammaticTransactionManagementTests extends
        AbstractTransactionalJUnit4SpringContextTests {

    @Test
    public void transactionalTest() {
        // assert initial state in test database:
        assertNumUsers(2);

        deleteFromTables("user");

        // changes to the database will be committed!
        TestTransaction.flagForCommit();
        TestTransaction.end();
        assertFalse(TestTransaction.isActive());
        assertNumUsers(0);

        TestTransaction.start();
        // perform other actions against the database that will
        // be automatically rolled back after the test completes...
    }

    protected void assertNumUsers(int expected) {
        assertEquals("Number of rows in the [user] table.", expected, countRowsInTable("user"));
    }
}
````

##### 执行事务之外的代码

有时，您可能需要在事务性测试方法之前或之后，但在事务上下文之外执行某些代码 - 例如，在运行测试之前验证初始数据库状态或在测试运行后验证预期的事务提交行为（如果测试配置为提交事务）。对于这种情况，`TransactionalTestExecutionListener` 支持 `@BeforeTransaction` 和 `@AfterTransaction` 注解。您可以使用其中一个注解在测试类或测试接口中的任何 `void` 默认方法或者任何 `void` 方法，并且 `TransactionalTestExecutionListener` 确保您的事务之前的方法或事务方法在适当的时间运行。

> 任何前置方法（例如使用 JUnit Jupiter 的 `@BeforeEach` 注解修饰的方法）和任何后置方法（例如使用 JUnit Jupiter 的 `@AfterEach` 注解修饰的方法）都在事务中运行。此外，对于未配置为在事务中运行的测试方法，不会运行使用 `@BeforeTransaction` 或 `@AfterTransaction` 注解修饰的方法。

##### 配置事务管理器

`TransactionalTestExecutionListener` 期望在 Spring `ApplicationContext` 中定义一个 `PlatformTransactionManager` bean 用于测试。如果在测试的 `ApplicationContext` 中有多个 `PlatformTransactionManager` 实例，你可以使用 `@Transactional("myTxMgr")` 或 `@Transactional(transactionManager = "myTxMgr")` 或 `TransactionManagementConfigurer` 来声明一个限定符，由 `@Configuration` 类实现。请参阅  [`TestContextTransactionUtils.retrieveTransactionManager()`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/transaction/TestContextTransactionUtils.html#retrieveTransactionManager-org.springframework.test.context.TestContext-java.lang.String-)  文档了解用于在测试的 `ApplicationContext` 中查找事务管理器的算法的详细信息。

##### 演示所有与事务相关的注释

以下基于 JUnit 4 的示例显示了一个虚构的集成测试场景，该场景突出显示了所有与事务相关的注解。该示例不是为了演示最佳实践，而是为了演示如何使用这些注解。有关更多信息和配置示例，请参阅 [annotation support](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations) 部分。 [Transaction management for `@Sql`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-executing-sql-declaratively-tx) 包含一个使用 `@Sql` 进行声明性 SQL 脚本执行的附加示例，其中包含默认事务回滚语义。以下示例显示了相关注解：

````java
@RunWith(SpringRunner.class)
@ContextConfiguration
@Transactional(transactionManager = "txMgr")
@Commit
public class FictitiousTransactionalTest {

    @BeforeTransaction
    void verifyInitialDatabaseState() {
        // logic to verify the initial state before a transaction is started
    }

    @Before
    public void setUpTestDataWithinTransaction() {
        // set up test data within the transaction
    }

    @Test
    // overrides the class-level @Commit setting
    @Rollback
    public void modifyDatabaseWithinTransaction() {
        // logic which uses the test data and modifies database state
    }

    @After
    public void tearDownWithinTransaction() {
        // execute "tear down" logic within the transaction
    }

    @AfterTransaction
    void verifyFinalDatabaseState() {
        // logic to verify the final state after transaction has rolled back
    }

}
````

> *在测试ORM代码时避免误报*
>
> 当您测试操作 Hibernate 会话或 JPA 持久性上下文的状态的应用程序代码时，请确保在运行该代码的测试方法中刷新基础工作单元。未能刷新基础工作单元可能会产生误报：您的测试通过，但相同的代码会在生产环境中引发异常。请注意，这适用于维护内存工作单元的任何 ORM 框架。在下面基于 Hibernate 的示例测试用例中，一个方法演示了误报，另一个方法正确地暴露了刷新会话的结果：
>
> ````java
> // ...
> 
> @Autowired
> SessionFactory sessionFactory;
> 
> @Transactional
> @Test // no expected exception!
> public void falsePositive() {
>     updateEntityInHibernateSession();
>     // False positive: an exception will be thrown once the Hibernate
>     // Session is finally flushed (i.e., in production code)
> }
> 
> @Transactional
> @Test(expected = ...)
> public void updateWithSessionFlush() {
>     updateEntityInHibernateSession();
>     // Manual flush is required to avoid false positive in test
>     sessionFactory.getCurrentSession().flush();
> }
> 
> // ...
> ````
>
> 下面的例子展示了 JPA 中对应的方法：
>
> ````java
> // ...
> 
> @PersistenceContext
> EntityManager entityManager;
> 
> @Transactional
> @Test // no expected exception!
> public void falsePositive() {
>     updateEntityInJpaPersistenceContext();
>     // False positive: an exception will be thrown once the JPA
>     // EntityManager is finally flushed (i.e., in production code)
> }
> 
> @Transactional
> @Test(expected = ...)
> public void updateWithEntityManagerFlush() {
>     updateEntityInJpaPersistenceContext();
>     // Manual flush is required to avoid false positive in test
>     entityManager.flush();
> }
> 
> // ...
> ````

#### 3.5.8. 执行 SQL 脚本

当为关系数据库编写集成测试时，执行 SQL 脚本修改数据库模式或者向数据库表中插入测试数据通常是很有用的。`spring-jdbc` 模块提供了在 Spring `ApplicationContext` 被加载时初始化一个内置数据库或者现有数据库的支持。参考 [Embedded database support](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-embedded-database-support) 和 [Testing data access logic with an embedded database](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/data-access.html#jdbc-embedded-database-dao-testing) 了解更多细节。

尽管在 `ApplicationContext` 被加载时为测试初始化一次数据库是很有用的，有时候在集成测试期间能够修改数据库是完全必要的。下面的场景解释了如何在集成测试期间以编程方式和声明方式执行 SQL 脚本。

##### 编程方式执行 SQL 脚本

Spring 提供了下面的选项在集成测试方法中以编程方式执行 SQL 脚本：

- `org.springframework.jdbc.datasource.init.ScriptUtils`
- `org.springframework.jdbc.datasource.init.ResourceDatabasePopulator`
- `org.springframework.test.context.junit4.AbstractTransactionalJUnit4SpringContextTests`
- `org.springframework.test.context.testng.AbstractTransactionalTestNGSpringContextTests`

`ScriptUtils` 提供了用于处理 SQL 脚本的静态实用程序方法的集合，主要用于框架内部。但是，如果您需要完全控制 SQL 脚本的解析和执行方式，则 `ScriptUtils` 可能比稍后介绍的其他一些替代方法更适合您的需求。请参阅 `ScriptUtils` 中的各个方法的 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jdbc/datasource/init/ScriptUtils.html) 了解更多细节。

`ResourceDatabasePopulator` 提供了一个基于对象的 API，可通过使用外部资源中定义的 SQL 脚本以编程方式填充，初始化或清理数据库。 `ResourceDatabasePopulator` 提供了一些选项，用于配置在解析和运行脚本时使用的字符编码，语句分隔符，注解定界符和错误处理标志。每个配置选项都有一个合理的默认值。有关默认的详细信息，请参见 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/jdbc/datasource/init/ResourceDatabasePopulator.html) 。要运行在 `ResourceDatabasePopulator` 中配置的脚本，可以调用 `populate(Connection)` 方法来针对 ` java.sql.Connection` 来执行填充器，或者可以通过 `execute(DataSource)` 方法来针对其执行填充器，一个 `javax.sql.DataSource`。以下示例为测试模式和测试数据指定 SQL 脚本，将语句分隔符设置为 `@@`，然后针对 `DataSource` 执行脚本：

````java
@Test
public void databaseTest {
    ResourceDatabasePopulator populator = new ResourceDatabasePopulator();
    populator.addScripts(
            new ClassPathResource("test-schema.sql"),
            new ClassPathResource("test-data.sql"));
    populator.setSeparator("@@");
    populator.execute(this.dataSource);
    // execute code that uses the test schema and data
}
````

注意，`ResourceDatabasePopulator` 内部委托给 `ScriptUtils` 来解析和运行 SQL 脚本。类似地，[`AbstractTransactionalJUnit4SpringContextTests`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-support-classes-junit4) 和[`AbstractTransactionalTestNGSpringContextTests`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-support-classes-testng) 中的 `executeSqlScript(..)` 方法在内部使用 `ResourceDatabasePopulator` 运行 SQL 脚本。有关更多详细信息，请参见Javadoc中的各种 `executeSqlScript(..)` 方法。

##### 使用 @Sql 声明式执行 SQL 脚本

除了上述用于以编程方式运行 SQL 脚本的机制之外，您还可以在 Spring TestContext Framework 中声明性地配置 SQL 脚本。具体来说，您可以在测试类或测试方法上声明 `@Sql` 注解，以配置应在集成测试方法之前或之后针对给定数据库运行的 SQL 脚本的资源路径。请注意，方法级别的声明会覆盖类级别的声明，并且 `SqlScriptsTestExecutionListener` 会默认开启对 `@Sql` 的支持。

###### 路径资源语义

每个路径都被解释为 Spring `Resource`。普通路径（例如 `"schema.sql"`）被视为相对于定义测试类的包的路径的类路径资源。以斜杠开头的路径被视为绝对类路径资源（例如，`"/org/example/schema.sql"`）。通过使用指定的资源协议来加载引用 URL 的路径（例如，以 `classpath:`，`file:`，`http:` 开头的路径）。

以下示例显示了如何在基于 JUnit Jupiter 的集成测试类中的类级别和方法级别使用 `@Sql`：

````java
@SpringJUnitConfig
@Sql("/test-schema.sql")
class DatabaseTests {

    @Test
    void emptySchemaTest {
        // execute code that uses the test schema without any test data
    }

    @Test
    @Sql({"/test-schema.sql", "/test-user-data.sql"})
    void userTest {
        // execute code that uses the test schema and test data
    }
}
````

###### 默认脚本探测

如果没有指定 SQL 脚本，框架就会试图探测所谓的 `default` 脚本，取决于声明 `@Sql` 的位置。如果默认脚本没有探测到，将会抛出一个 `IllegalStateException` 。

- 类级别的声明：如果注解修饰的测试类是 `com.example.MyTest`，对应的默认脚本就是 `classpath:com/example/MyTest.sql`。
- 方法级别声明：如果注解修饰的测试类由 `testMethod()` 命名，并声明在类 `com.example.MyTest` 中，对应的默认脚本就是 `classpath:com/example/MyTest.testMethod.sql`。

###### 声明多个 `@Sql` 集合

如果您需要为给定的测试类或测试方法配置多组 SQL 脚本，但使用不同的语法配置，不同的错误处理规则或每组不同的执行阶段，则可以声明多个 `@Sql` 实例。在 Java 8 中，您可以将 `@Sql` 用作可重复的注解。否则，您可以使用 `@SqlGroup` 注解作为显式容器来声明多个 `@Sql` 实例。

以下示例显示了如何在 Java 8 中将 `@Sql` 用作可重复注解：

````java
@Test
@Sql(scripts = "/test-schema.sql", config = @SqlConfig(commentPrefix = "`"))
@Sql("/test-user-data.sql")
public void userTest {
    // execute code that uses the test schema and test data
}
````

在以上示例中呈现的场景中，`test-schema.sql` 脚本对单行注解使用了不同的语法。

除了与 Java 6 和 Java 7 兼容之外，以下示例与上述示例相同，不同之处在于在 `@SqlGroup` 中将 `@Sql` 声明分组在一起。

````java
@Test
@SqlGroup({
    @Sql(scripts = "/test-schema.sql", config = @SqlConfig(commentPrefix = "`")),
    @Sql("/test-user-data.sql")
)}
public void userTest {
    // execute code that uses the test schema and test data
}
````

###### 脚本执行阶段

默认情况下，SQL 脚本在相应的测试方法之前执行。但是，如果需要在测试方法之后运行一组特定的脚本（例如，清理数据库状态），则可以使用 `@Sql` 中的 `executionPhase` 属性，如以下示例所示：

````java
@Test
@Sql(
    scripts = "create-test-data.sql",
    config = @SqlConfig(transactionMode = ISOLATED)
)
@Sql(
    scripts = "delete-test-data.sql",
    config = @SqlConfig(transactionMode = ISOLATED),
    executionPhase = AFTER_TEST_METHOD
)
public void userTest {
    // execute code that needs the test data to be committed
    // to the database outside of the test's transaction
}
````

注意 `ISOLATED` 和 `AFTER_TEST_METHOD` 是分别从 `Sql.TransactionMode` 和 `Sql.ExecutionPhase` 静态导入的。

###### 使用 `@SqlConfig` 进行脚本配置

您可以使用 `@SqlConfig` 注解配置脚本解析和错误处理。`@SqlConfig` 在声明为集成测试类的类级别注解时，将用作测试类层次结构中所有 SQL 脚本的全局配置。如果直接使用 `@Sql` 注解的 `config` 属性来声明，则 `@SqlConfig` 用作在 `@Sql` 注解中声明的 SQL 脚本的本地配置。`@SqlConfig` 中的每个属性都有一个隐式默认值，该默认值记录在相应属性的 javadoc 中。不幸的是，由于 Java 语言规范中为注解属性定义了规则，因此无法为注解属性分配 `null` 值。因此，为了支持覆盖继承的全局配置，`@SqlConfig` 属性的显式默认值为 `""`（对于字符串）或 `DEFAULT`（对于枚举）。这种方法通过提供除 `""` 或 `"DEFAULT"` 以外的其他值，从而使 `@SqlConfig` 的本地声明选择性地覆盖 `@SqlConfig` 的全局声明中的各个属性。只要本地 `@SqlConfig` 属性不提供除 `""` 或 `"DEFAULT"` 以外的显式值，就会继承全局 `@SqlConfig` 属性。因此，显式本地配置将覆盖全局配置。

由 `@Sql` 和 `@SqlConfig` 提供的配置选项等价于 `ScriptUtils` 和 `ResourceDatabasePopulator` 提供的支持，但是却是 `<jdbc:initialize-database/>` XML 命名空间元素提供的选项的超集。参考 [`@Sql`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/jdbc/Sql.html) 和 [`@SqlConfig`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/jdbc/SqlConfig.html) 文档获取更多细节。

**@Sql 的事务管理**

默认情况下，`SqlScriptsTestExecutionListener` 会为使用 `@Sql` 配置的脚本推断所需的事务语义。具体来说，SQL 脚本在没有事务的情况下运行，而是在现有的 Spring 管理的事务中运行（例如，由 ` TransactionalTestExecutionListener` 管理的事务对带有 `@Transactional` 注解的测试进行管理），或者在隔离的事务中运行，具体取决于配置 `@SqlConfig` 中的 `transactionMode` 属性的值，以及测试的 `ApplicationContext` 中是否存在 `PlatformTransactionManager`。不过，最低限度是，测试的 `ApplicationContext` 中必须存在一个 `javax.sql.DataSource`。

如果 `SqlScriptsTestExecutionListener` 用来检测 `DataSource` 和 `PlatformTransactionManager` 并推断事务语义的算法不符合您的需要，则可以通过设置 `@SqlConfig` 的 `dataSource` 和 `transactionManager` 属性来显式指定名称。此外，您可以通过设置 `@SqlConfig` 的 `transactionMode` 属性来控制事务传播行为（例如，是否应在隔离的事务中运行脚本）。尽管对使用 `@Sql` 进行事务管理的所有受支持选项的详尽讨论超出了本参考手册的范围，但是 [`@SqlConfig`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/jdbc/SqlConfig.html) 和 [`SqlScriptsTestExecutionListener`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/jdbc/SqlScriptsTestExecutionListener.html) 文档提供了详细信息，下面的示例显示了一个典型的测试场景，该场景使用 JUnit Jupiter 和带有 `@Sql` 的事务测试：

````java
@SpringJUnitConfig(TestDatabaseConfig.class)
@Transactional
class TransactionalSqlScriptsTests {

    final JdbcTemplate jdbcTemplate;

    @Autowired
    TransactionalSqlScriptsTests(DataSource dataSource) {
        this.jdbcTemplate = new JdbcTemplate(dataSource);
    }

    @Test
    @Sql("/test-data.sql")
    void usersTest() {
        // verify state in test database:
        assertNumUsers(2);
        // execute code that uses the test data...
    }

    int countRowsInTable(String tableName) {
        return JdbcTestUtils.countRowsInTable(this.jdbcTemplate, tableName);
    }

    void assertNumUsers(int expected) {
        assertEquals(expected, countRowsInTable("user"),
            "Number of rows in the [user] table.");
    }
}
````

注意，在运行 `usersTest()` 方法后，无需清理数据库，因为对数据库所做的任何更改（在 test 方法内或在 `/test-data.sql` 脚本内）都是会自动通过 `TransactionalTestExecutionListener` 回滚的。有关详细信息，请参阅 [transaction management](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-tx) 。

#### 3.5.9. 并行测试执行

当使用 Spring TestContext Framework 时，Spring Framework 5.0 引入了对在单个 JVM 中并行执行测试的基本支持。通常，这意味着大多数测试类或测试方法可以并行执行，而无需更改测试代码或配置。

> 配置并行测试执行的细节，参考你的测试框架的文档，或者构建工具或者 IDE 的文档。

请记住，将并发引入测试套件可能会导致意外的副作用，奇怪的运行时行为以及间歇性或看似随机失败的测试。因此，对于何时不并行执行测试，Spring 团队提供了以下一般准则。

如果测试符合以下条件，则不要并行执行测试：

- 使用 Spring 的 `@DirtiesContext` 支持。
- 使用 JUnit 4 的 `@FixMethodOrder` 支持或旨在确保测试方法按特定顺序运行的任何测试框架功能。但是请注意，如果整个测试类是并行执行的，则此方法不适用。
- 更改共享服务或系统（如数据库，消息代理，文件系统等）的状态。这适用于内存系统和外部系统。

> 如果并行测试执行失败，并指出当前测试的 `ApplicationContext` 不再处于活动状态，则这通常意味着 `ApplicationContext` 已从另一个线程中的 `ContextCache` 中删除。
>
> 这可能是由于使用了 `@DirtiesContext` 或来自 `ContextCache` 的自动逐出。如果 `@DirtiesContext` 是罪魁祸首，则您需要找到一种避免使用 `@DirtiesContext` 的方法，或者从并行执行中排除此类测试。如果超过了 `ContextCache` 的最大大小，则可以增加缓存的最大大小。有关详细信息，请参见 [context caching](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-caching) 的讨论。
>
> 仅当基础的 `TestContext` 实现提供副本构造函数时，才能在 Spring TestContext Framework 中并行执行测试，如 [`TestContext`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/context/TestContext.html) 。在 Spring 中使用的 `DefaultTestContext` 提供了这样的构造函数。但是，如果您使用提供自定义 `TestContext` 实现的第三方库，则需要验证它是否适合并行测试执行。

#### 3.5.10. TestContext Framework 支持类

本节描述了支持 Spring TestContext Framework 的各种类。

##### Spring JUnit 4 Runner

Spring TestContext Framework 通过自定义运行程序（在 JUnit 4.12 或更高版本上受支持）提供了与 JUnit 4 的完全集成。通过使用 `@RunWith(SpringJUnit4ClassRunner.class)` 或更短的 `@RunWith(SpringRunner.class)` 变体对测试类进行注解，开发人员可以实现基于 JUnit 4 的标准单元测试和集成测试，同时获得 TestContext 框架的好处， 例如对加载应用程序上下文的支持，对测试实例的依赖项注入， 事务性测试方法执行等。如果您想将Spring TestContext Framework 与备用运行程序（例如 JUnit 4 的 `Parameterized` 运行程序）或第三方运行程序（例如 `MockitoJUnitRunner` ）一起使用，则可以选择使用 [Spring 对 JUnit 规则的支持](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-junit4-rules) 代替。

下面的代码展示了将测试类配置为使用自定义的 Spring `Runner` 执行所需有的最小需求：

````java
@RunWith(SpringRunner.class)
@TestExecutionListeners({})
public class SimpleTest {

    @Test
    public void testMethod() {
        // execute test logic...
    }
}
````

上面的例子中，`@TestExecutionListeners` 被配置了一个空列表，来禁用默认的监听器，这些默认的监听器将需要通过 `@ContextConfiguration` 配置的 `ApplicationContext`。

##### Spring JUnit 4 Rules

 `org.springframework.test.context.junit4.rules` 包提供了如下的 JUnit 4 规则 (JUnit 4.12 或更高版本支持)：

- `SpringClassRule`
- `SpringMethodRule`

`SpringClassRule` 是支持 Spring TestContext Framework 的类级功能的 JUnit `TestRule`，而 `SpringMethodRule` 是支持 Spring TestContext Framework 的实例级和方法级功能的 JUnit `MethodRule`。

与 `SpringRunner` 相比，Spring 基于规则的 JUnit 支持具有独立于任何 `org.junit.runner.Runner` 实现的优点，因此可以与现有的替代运行器（例如 JUnit 4 的 `Parameterized` ）或第三方组件（例如 `MockitoJUnitRunner`）结合使用。

为了支持 TestContext 框架的全部功能，必须将 `SpringClassRule` 与 `SpringMethodRule` 结合使用。以下示例显示了在集成测试中声明这些规则的正确方法：

```java
// Optionally specify a non-Spring Runner via @RunWith(...)
@ContextConfiguration
public class IntegrationTest {

    @ClassRule
    public static final SpringClassRule springClassRule = new SpringClassRule();

    @Rule
    public final SpringMethodRule springMethodRule = new SpringMethodRule();

    @Test
    public void testMethod() {
        // execute test logic...
    }
}
```

##### JUnit 4 Support Classes

 `org.springframework.test.context.junit4` 包为基于 JUnit 4 的测试用例提供了下列支持类 (JUnit 4.12 或更高版本支持)：

- `AbstractJUnit4SpringContextTests`
- `AbstractTransactionalJUnit4SpringContextTests`

`AbstractJUnit4SpringContextTests` 是一个抽象的基础测试类，它在 JUnit 4 环境中将 Spring TestContext Framework 与显式的 `ApplicationContext` 测试支持集成在一起。扩展 `AbstractJUnit4SpringContextTests` 时，您可以访问受保护的 `applicationContext` 实例变量，该变量可用于执行显式 bean 查找或测试整个上下文的状态。

`AbstractTransactionalJUnit4SpringContextTests` 是 `AbstractJUnit4SpringContextTests` 的抽象事务扩展，为 JDBC 访问添加了一些便利功能。此类要求在 `ApplicationContext` 中定义一个 `javax.sql.DataSource` Bean 和一个 `PlatformTransactionManager` Bean。扩展 `AbstractTransactionalJUnit4SpringContextTests` 时，可以访问受保护的 `jdbcTemplate` 实例变量，该实例变量可用于运行 SQL 语句来查询数据库。您可以在运行与数据库相关的应用程序代码之前和之后使用此类查询来确认数据库状态，并且 Spring 确保此类查询在与应用程序代码相同的事务范围内运行。与 ORM 工具结合使用时，请确保避免 [误报](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-tx-false-positives) 。如 [JDBC测试支持](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-support-jdbc) 中所述，`AbstractTransactionalJUnit4SpringContextTests ` 还提供了方便的方法，通过使用上述 `jdbcTemplate` 委派给 `JdbcTestUtils` 中的方法。此外，`AbstractTransactionalJUnit4SpringContextTests` 提供了一种 `executeSqlScript(..)` 方法，用于针对已配置的 `DataSource` 运行 SQL 脚本。

> 这些类为扩展提供了便利。如果您不希望将测试类绑定到特定于 Spring 的类层次结构，则可以使用 `@RunWith(SpringRunner.class)` 或 [Spring的JUnit规则](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-junit4-rules) 。

##### SpringExtension for JUnit Jupiter

Spring TestContext Framework 提供了与 JUnit 5 中引入的 JUnit Jupiter 测试框架的完全集成。通过使用 `@ExtendWith（SpringExtension.class）` 注解测试类，您可以实现基于 JUnit Jupiter 的标准单元测试和集成测试，并同时获得 TestContext 框架的好处，例如支持加载应用程序上下文，测试实例的依赖注入，事务性测试方法执行等。

此外，得益于 JUnit Jupiter 中丰富的扩展API，Spring 在支持 JUnit 4 和 TestNG 的功能集之外提供了以下功能：

- 对测试构造函数，测试方法和测试生命周期回调方法的依赖注入。有关更多信息，请参见 [使用`SpringExtension`进行依赖注入](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-junit-jupiter-di) 细节。
- 基于 SpEL 表达式，环境变量，系统属性等，对 [条件测试执行](https://junit.org/junit5/docs/current/user-guide/#extensions-conditions) 的强大支持。请参阅 [Spring JUnit Jupiter测试注释](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-junit-jupiter) 中的 `@EnabledIf` 和 `@DisabledIf` 文档以获取更多详细信息和示例。
- 定制组合注解，结合了 Spring和JUnit Jupiter 的注解。请参阅 [测试的元注释支持](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-meta) 中的 `@TransactionalDevTestConfig` 和 `@TransactionalIntegrationTest` 示例以获取更多详细信息。

以下代码清单显示了如何配置测试类以将 `SpringExtension` 与 `@ContextConfiguration` 结合使用：

```java
// Instructs JUnit Jupiter to extend the test with Spring support.
@ExtendWith(SpringExtension.class)
// Instructs Spring to load an ApplicationContext from TestConfig.class
@ContextConfiguration(classes = TestConfig.class)
class SimpleTests {

    @Test
    void testMethod() {
        // execute test logic...
    }
}
```

由于您还可以在 JUnit 5 中使用注解作为元注解，因此 Spring 提供了由 `@SpringJUnitConfig` 和 `@SpringJUnitWebConfig` 组成的注解，以简化测试 `ApplicationContext` 和 JUnit Jupiter的配置。

以下示例使用 `@SpringJUnitConfig` 来减少前一示例中使用的配置量：

```java
// Instructs Spring to register the SpringExtension with JUnit
// Jupiter and load an ApplicationContext from TestConfig.class
@SpringJUnitConfig(TestConfig.class)
class SimpleTests {

    @Test
    void testMethod() {
        // execute test logic...
    }
}
```

同样，以下示例使用 `@SpringJUnitWebConfig` 创建用于 JUnit Jupiter 的 `WebApplicationContext`：

```java
// Instructs Spring to register the SpringExtension with JUnit
// Jupiter and load a WebApplicationContext from TestWebConfig.class
@SpringJUnitWebConfig(TestWebConfig.class)
class SimpleWebTests {

    @Test
    void testMethod() {
        // execute test logic...
    }
}
```

请参阅 [Spring JUnit Jupiter测试注释](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-annotations-junit-jupiter) 中的 `@SpringJUnitConfig` 和 `@SpringJUnitWebConfig` 文档以获取更多详细信息。

##### 使用 `SpringExtension` 进行依赖注入

`SpringExtension` 实现了来自 JUnit Jupiter 的 [`ParameterResolver`](https://junit.org/junit5/docs/current/user-guide/#extensions-parameter-resolution) 扩展API，它使 Spring 为测试提供依赖注入 构造函数，测试方法和测试生命周期回调方法。

具体来说，`SpringExtension` 可以将测试的 `ApplicationContext` 中的依赖项注入到以 `@BeforeAll`，`@AfterAll`，`@BeforeEach`，`@AfterEach`，`@Test`，`@RepeatedTest`， `@ParameterizedTest` 进行注解的测试构造函数和方法中。

###### 构造器注入

如果 JUnit Jupiter 测试类的构造函数中的参数的类型为 `ApplicationContext`（或其子类型），或者使用 `@Autowired`，`@Qualifier` 或 `@Value` 进行注解或元注解， Spring 使用来自测试的 `ApplicationContext` 中的相应 bean 注入该特定参数的值。如果所有参数都应由 Spring 提供，您也可以使用 `@Autowired` 直接注解测试构造函数。

> 如果测试类的构造函数本身带有 `@Autowired` 注解，则 Spring 负责解析构造函数中的*所有*参数。因此，在 JUnit Jupiter 中注册的其他 `ParameterResolver` 无法解析此类构造函数的参数。

> 如果在测试方法之前或之后使用 `@DirtiesContext` 来关闭测试的 `ApplicationContext`，则不得与 JUnit Jupiter 的 `@TestInstance(PER_CLASS)` 支持一起用于测试类的构造函数注入。
>
> 原因是 `@TestInstance(PER_CLASS)` 指示 JUnit Jupiter 在测试方法调用之间缓存测试实例。因此，测试实例将保留对最初从 `ApplicationContext` 注入的 bean 的引用，该 `ApplicationContext` 随后会被关闭。由于在这种情况下测试类的构造函数将仅被调用一次，因此依赖注入不会再次发生，并且后续测试将与关闭的 `ApplicationContext` 中的 bean 进行交互，这可能会导致错误。
>
> 若要将 `@DirtiesContext` 与 `@TestInstance(PER_CLASS)` 结合使用在“测试方法之前”或“测试方法之后”模式，必须配置 Spring 的依赖项，以通过字段或 `setter` 注入来提供，以便可以在测试方法调用之间重新注入它们。

在下面的例子中，Spring 将由 `ApplicationContext` 从 `TestConfig.class` 加载的 `OrderService` 注入 `OrderServiceIntegrationTests` 构造器。

```java
@SpringJUnitConfig(TestConfig.class)
class OrderServiceIntegrationTests {

    private final OrderService orderService;

    @Autowired
    OrderServiceIntegrationTests(OrderService orderService) {
        this.orderService = orderService.
    }

    // tests that use the injected OrderService
}
```

请注意，此功能使测试依赖项为 `final` ，因此是不可变的。

###### 方法注入

如果 JUnit Jupiter 测试方法或测试生命周期回调方法中的参数是 `ApplicationContext` 类型（或其子类型），或者使用 `@Autowired`，`@Qualifier` 或 `@Value` 进行注解或元注解。Spring 会使用测试的 `ApplicationContext` 中的相应 bean 注入该特定参数的值。

在下面的示例中，Spring 将 `ApplicationContext` 从 `TestConfig.class` 加载的 `OrderService` 注入到 `deleteOrder()` 测试方法中：

```java
@SpringJUnitConfig(TestConfig.class)
class OrderServiceIntegrationTests {

    @Test
    void deleteOrder(@Autowired OrderService orderService) {
        // use orderService from the test's ApplicationContext
    }
}
```

由于 JUnit Jupiter 中对 `ParameterResolver` 支持的强大功能，您不仅可以从 Spring 中，而且可以从 JUnit Jupiter 本身或其他第三方扩展中，将多个依赖项注入到单个方法中。

下面的示例演示如何让 Spring 和 JUnit Jupiter 同时将依赖项注入到 `placeOrderRepeatedly()` 测试方法中。

```java
@SpringJUnitConfig(TestConfig.class)
class OrderServiceIntegrationTests {

    @RepeatedTest(10)
    void placeOrderRepeatedly(RepetitionInfo repetitionInfo,
            @Autowired OrderService orderService) {

        // use orderService from the test's ApplicationContext
        // and repetitionInfo from JUnit Jupiter
    }
}
```

注意，通过使用 JUnit Jupiter 中的 `@RepeatedTest`，测试方法可以访问 `RepetitionInfo`。

##### TestNG 支持类

 `org.springframework.test.context.testng` 包为基于 TestNG 的测试提供了下列支持类：

- `AbstractTestNGSpringContextTests`
- `AbstractTransactionalTestNGSpringContextTests`

`AbstractTestNGSpringContextTests` 是一个抽象的基础测试类，它将 Spring TestContext Framework 与 TestNG 环境中的显式 `ApplicationContext` 测试支持集成在一起。当扩展 `AbstractTestNGSpringContextTests` 时，可以访问一个 `protected` 的 `applicationContext` 实例变量，该变量可用于执行显式 bean 查找或测试整个上下文的状态。

`AbstractTransactionalTestNGSpringContextTests` 是 `AbstractTestNGSpringContextTests` 的抽象事务扩展，为 JDBC 访问添加了一些便利功能。此类要求在 `ApplicationContext` 中定义一个 `javax.sql.DataSource` Bean 和一个 `PlatformTransactionManager` Bean。扩展 `AbstractTransactionalTestNGSpringContextTests` 时，可以访问受保护的 `jdbcTemplate` 实例变量，该变量可用于执行 SQL 语句来查询数据库。您可以在运行与数据库相关的应用程序代码之前和之后使用此类查询来确认数据库状态，并且 Spring 确保此类查询在与应用程序代码相同的事务范围内运行。与 ORM 工具结合使用时，请确保避免 [误报](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-tx-false-positives) 。如 [JDBC测试支持](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing-support-jdbc) 中所述，`AbstractTransactionalTestNGSpringContextTests ` 还提供了方便的方法，通过使用上述 `jdbcTemplate` 委派给 `JdbcTestUtils` 中的方法。此外，`AbstractTransactionalTestNGSpringContextTests` 提供了一种 `executeSqlScript(..)` 方法，用于针对已配置的 `DataSource` 运行 SQL 脚本。

> 这些类为扩展提供了便利。如果您不希望将测试类绑定到特定于 Spring 的类层次结构，则可以通过使用 `@ContextConfiguration`，`@TestExecutionListeners` 等来配置自己的自定义测试类，并通过手动方式对测试类进行检测 一个 `TestContextManager`。有关如何检测您的测试类的示例，请参见 `AbstractTestNGSpringContextTests` 的源代码。

### 3.6. Spring MVC 测试框架

The Spring MVC Test framework provides first class support for testing Spring MVC code with a fluent API that you can use with JUnit, TestNG, or any other testing framework. It is built on the [Servlet API mock objects](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/mock/web/package-summary.html) from the `spring-test` module and, hence, does not use a running Servlet container. It uses the `DispatcherServlet` to provide full Spring MVC runtime behavior and provides support for loading actual Spring configuration with the TestContext framework in addition to a standalone mode, in which you can manually instantiate controllers and test them one at a time.

Spring MVC Test also provides client-side support for testing code that uses the `RestTemplate`. Client-side tests mock the server responses and also do not use a running server.

> Spring Boot provides an option to write full, end-to-end integration tests that include a running server. If this is your goal, see the [Spring Boot reference page](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-testing.html#boot-features-testing-spring-boot-applications). For more information on the differences between out-of-container and end-to-end integration tests, see [Spring MVC Test vs End-to-End Tests](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#spring-mvc-test-vs-end-to-end-integration-tests).

#### 3.6.1. 服务端测试

您可以使用 JUnit 或 TestNG 为 Spring MVC 控制器编写一个普通的单元测试。为此，实例化控制器，向其注入模拟或存根依赖，然后调用其方法（根据需要传递 `MockHttpServletRequest`，`MockHttpServletResponse` 和其他组件）。但是，在编写这样的单元测试时，仍有很多未经测试的内容：例如，请求映射，数据绑定，类型转换，验证等等。此外，其他控制器方法（例如，`@InitBinder`，`@ModelAttribute` 和 `@ExceptionHandler`）也可以作为请求处理生命周期的一部分来调用。

Spring MVC Test 的目标是通过执行请求并通过实际的 `DispatcherServlet` 生成响应来提供一种测试控制器的有效方法。

Spring MVC 测试类基于似于在 spring-test 模块中可用的 [Servlet API 的 mock 实现](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#mock-objects-servlet)  建立。这允许执行请求和生成响应，而无需在 Servlet 容器中运行。在大多数情况下，一切都应像在运行时一样工作，但有一些值得注意的例外，如 [Spring MVC测试与端到端测试](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#spring-mvc-test-vs-end-to-end-integration-tests) 。以下基于 JUnit Jupiter 的示例使用 Spring MVC Test：

```java
import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@SpringJUnitWebConfig(locations = "test-servlet-context.xml")
class ExampleTests {

    private MockMvc mockMvc;

    @BeforeEach
    void setup(WebApplicationContext wac) {
        this.mockMvc = MockMvcBuilders.webAppContextSetup(wac).build();
    }

    @Test
    void getAccount() throws Exception {
        this.mockMvc.perform(get("/accounts/1")
                .accept(MediaType.parseMediaType("application/json;charset=UTF-8")))
            .andExpect(status().isOk())
            .andExpect(content().contentType("application/json"))
            .andExpect(jsonPath("$.name").value("Lee"));
    }
}
```

前面的测试依赖于 TestContext 框架对 `WebApplicationContext` 的支持，以从与测试类位于同一包中的 XML 配置文件加载 Spring 配置，但是还支持基于 Java 和基于 Groovy 的配置。参见这些 [样本测试](https://github.com/spring-projects/spring-framework/tree/master/spring-test/src/test/java/org/springframework/test/web/servlet/samples/context) 。

`MockMvc` 实例用于执行对 `/accounts/1` 的 `GET` 请求，并验证结果响应的状态为 `200`，内容类型为 `application/json`，响应主体具有名为 `name` 的 JSON 属性值为 `Lee`。 Jayway [JsonPath project](https://github.com/jayway/JsonPath) 支持 `jsonPath` 语法。本文档后面将讨论用于验证执行请求结果的许多其他选项。

##### 静态导入

[上一部分](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#spring-mvc-test-server) 中的示例中的 API 需要一些静态导入，例如 `MockMvcRequestBuilders.*` ，`MockMvcResultMatchers.*` 和 `MockMvcBuilders.*`。查找这些类的一种简单方法是搜索与 `MockMvc *` 相匹配的类型。如果您使用 Eclipse 或基于 Eclipse 的 Spring Tool Suite，请确保在 " Java→编辑器→Content Assist→收藏夹" 下的 Eclipse 首选项中将它们添加为“收藏的静态成员”。这样，您可以在键入静态方法名称的第一个字符后使用内容辅助。其他 IDE（例如 IntelliJ）可能不需要任何其他配置。检查对静态成员的代码完成的支持。

##### 配置选择

创建 `MockMvc` 实例的主要方法有两个。首先是通过 TestContext 框架加载 Spring MVC 配置，该框架加载 Spring 配置并将 `WebApplicationContext` 注入测试以用于构建 `MockMvc` 实例。以下示例显示了如何执行此操作：

```java
@RunWith(SpringRunner.class)
@WebAppConfiguration
@ContextConfiguration("my-servlet-context.xml")
public class MyWebTests {

    @Autowired
    private WebApplicationContext wac;

    private MockMvc mockMvc;

    @Before
    public void setup() {
        this.mockMvc = MockMvcBuilders.webAppContextSetup(this.wac).build();
    }

    // ...

}
```

您的第二个选择是在不加载 Spring 配置的情况下手动创建控制器实例。而是自动创建了基本的默认配置，该配置与 MVC JavaConfig 或 MVC 命名空间大致相当。您可以在一定程度上对其进行自定义。以下示例显示了如何执行此操作：

```java
public class MyWebTests {

    private MockMvc mockMvc;

    @Before
    public void setup() {
        this.mockMvc = MockMvcBuilders.standaloneSetup(new AccountController()).build();
    }

    // ...

}
```

你应该使用哪些配置选项？

`webAppContextSetup` 加载您的实际 Spring MVC 配置，从而进行更完整的集成测试。由于 TestContext 框架缓存了已加载的 Spring 配置，因此即使您在测试套件中引入了更多测试，它也有助于保持测试的快速运行。此外，您可以通过 Spring 配置将模拟服务注入控制器中，以继续专注于测试 Web 层。下面的示例使用 Mockito 声明一个模拟服务：

```xml
<bean id="accountService" class="org.mockito.Mockito" factory-method="mock">
    <constructor-arg value="org.example.AccountService"/>
</bean>
```

然后，您可以将模拟服务注入测试中，以设置和验证您的期望，如以下示例所示：

```java
@RunWith(SpringRunner.class)
@WebAppConfiguration
@ContextConfiguration("test-servlet-context.xml")
public class AccountTests {

    @Autowired
    private WebApplicationContext wac;

    private MockMvc mockMvc;

    @Autowired
    private AccountService accountService;

    // ...

}
```

另一方面，`standaloneSetup` 更接近于单元测试。它一次测试一个控制器。您可以手动注入具有模拟依赖项的控制器，并且不涉及加载 Spring 配置。这样的测试更多地集中在样式上，使查看被测试的控制器是否需要任何特定的 Spring MVC 配置等工作变得更加容易。`standaloneSetup` 也是编写临时测试以验证特定行为或调试问题的一种非常方便的方法。

与大多数“集成与单元测试”辩论一样，没有正确或错误的答案。但是，使用 `standaloneSetup` 确实意味着需要额外的 `webAppContextSetup` 测试来验证您的 Spring MVC 配置。另外，您可以使用 `webAppContextSetup` 编写所有测试，以便始终针对实际的 Spring MVC 配置进行测试。

##### 配置特性

无论使用哪种 MockMvc 构建器，所有 `MockMvcBuilder` 实现都提供一些常见且非常有用的功能。例如，您可以为所有请求声明一个 `Accept` 首部，并在所有响应中期望状态为 200 以及一个 `Content-Type` 首部，如下所示：

```java
// static import of MockMvcBuilders.standaloneSetup

MockMvc mockMvc = standaloneSetup(new MusicController())
        .defaultRequest(get("/").accept(MediaType.APPLICATION_JSON))
        .alwaysExpect(status().isOk())
        .alwaysExpect(content().contentType("application/json;charset=UTF-8"))
        .build();
```

另外，第三方框架（和应用程序）可以预先打包安装说明，例如 `MockMvcConfigurer` 中的安装说明。Spring 框架具有一个这样的内置实现，可帮助保存和重用跨请求的 HTTP 会话。您可以按以下方式使用它：

```java
// static import of SharedHttpSessionConfigurer.sharedHttpSession

MockMvc mockMvc = MockMvcBuilders.standaloneSetup(new TestController())
        .apply(sharedHttpSession())
        .build();

// Use mockMvc to perform requests...
```

参考 [`ConfigurableMockMvcBuilder`](https://docs.spring.io/spring-framework/docs/5.1.9.RELEASE/javadoc-api/org/springframework/test/web/servlet/setup/ConfigurableMockMvcBuilder.html) 文档以获得所有 MockMvc 构建器功能的列表，或使用 IDE 探索可用选项。

##### 执行请求

你可以执行使用任何 HTTP 方法的请求，如下面例子所示：

```java
mockMvc.perform(post("/hotels/{id}", 42).accept(MediaType.APPLICATION_JSON));
```

您也可以执行内部使用 `MockMultipartHttpServletRequest` 的文件上传请求，这样就不会对多部分请求进行实际解析。相反，您必须将其设置为类似于以下示例：

```java
mockMvc.perform(multipart("/doc").file("a1", "ABC".getBytes("UTF-8")));
```

您可以使用 URI 模板样式指定查询参数，如以下示例所示：

```java
mockMvc.perform(get("/hotels?thing={thing}", "somewhere"));
```

您还可以添加代表查询或表单参数的 Servlet 请求参数，如以下示例所示：

```java
mockMvc.perform(get("/hotels").param("thing", "somewhere"));
```

如果应用程序代码依赖 Servlet 请求参数，并且没有显式检查查询字符串（通常是这种情况），则使用哪个选项都没有关系。但是请记住，URI 模板提供的查询参数已被解码，而通过 `param(…)` 方法提供的请求参数预计已被解码。

在大多数情况下，最好将上下文路径和Servlet路径保留在请求URI之外。 如果必须使用完整的请求URI进行测试，请确保相应地设置`contextPath`和`servletPath`，以便请求映射起作用，如以下示例所示：

```java
mockMvc.perform(get("/app/main/hotels/{id}").contextPath("/app").servletPath("/main"))
```

在前面的示例中，为每个执行的请求设置 `contextPath` 和 `servletPath` 将很麻烦。相反，您可以设置默认请求属性，如以下示例所示：

```java
public class MyWebTests {

    private MockMvc mockMvc;

    @Before
    public void setup() {
        mockMvc = standaloneSetup(new AccountController())
            .defaultRequest(get("/")
            .contextPath("/app").servletPath("/main")
            .accept(MediaType.APPLICATION_JSON)).build();
    }
```

前面的属性会影响通过 `MockMvc` 实例执行的每个请求。如果在给定请求上也指定了相同的属性，则它将覆盖默认值。这就是默认请求中的 HTTP 方法和 URI 无关紧要的原因，因为必须在每个请求中都指定它们。

##### 定义期望

您可以通过在执行请求后附加一个或多个 `.andExpect(..)` 调用来定义期望，如以下示例所示：

```java
mockMvc.perform(get("/accounts/1")).andExpect(status().isOk());
```

`MockMvcResultMatchers.*` 提供了一些期望，其中一些期望被进一步封装在其它更精细的期望中。

期望分为两大类。第一类断言验证响应的属性（例如，响应状态，标头和内容）。这些是要断言的最重要的结果。

第二类断言超出了响应范围。这些断言使您可以检查 Spring MVC 的特定方面，例如哪种控制器方法处理了请求，是否引发和处理了异常，模型的内容是什么，选择了哪种视图，添加了哪些瞬态属性（flash attributes），等等。它们还使您可以检查 Servlet 的特定方面，例如请求和会话属性。

以下测试断言绑定或验证失败：

```java
mockMvc.perform(post("/persons"))
    .andExpect(status().isOk())
    .andExpect(model().attributeHasErrors("person"));
```

很多时候，编写测试时，转储已执行请求的结果很有用。您可以按照以下方式进行操作，其中 `print()` 是来自 `MockMvcResultHandlers` 的静态导入：

```java
mockMvc.perform(post("/persons"))
    .andDo(print())
    .andExpect(status().isOk())
    .andExpect(model().attributeHasErrors("person"));
```

只要请求处理不会引起未处理的异常，`print()` 方法会将所有可用的结果数据打印到 `System.out`。Spring Framework 4.2 引入了 `log()` 方法和 `print()` 方法的两个附加变体，一个接受 `OutputStream`，另一个接受 `Writer`。例如，调用 `print(System.err)` 将结果数据打印到 `System.err`，而调用 `print(myWriter)` 将结果数据打印到自定义编写器。如果您希望记录结果数据而不是打印结果，则可以调用 `log()` 方法，该方法将结果数据记录为 `org.springframework.test.web.servlet.result` 日志记录类别下的一条 `DEBUG` 消息。

在某些情况下，您可能需要直接访问结果并验证无法通过其他手段验证的内容。可以通过在所有其他期望之后附加 `.andReturn()` 来实现，如以下示例所示：

```java
MvcResult mvcResult = mockMvc.perform(post("/persons")).andExpect(status().isOk()).andReturn();
// ...
```

如果所有测试使用相同的期望，你可以在创建 `MockMvc` 实例时统一配置通用期望。如下面例子所示：

```java
standaloneSetup(new SimpleController())
    .alwaysExpect(status().isOk())
    .alwaysExpect(content().contentType("application/json;charset=UTF-8"))
    .build()
```

注意，通用的期望总是被应用，除非创建一个单独的 `MockMvc` 实例，否则不能被覆盖。

当 JSON 响应内容包含使用  [Spring HATEOAS](https://github.com/spring-projects/spring-hateoas) 创建的超链接时，可以使用 JsonPath 表达式来验证结果链接，如以下示例所示：

```java
mockMvc.perform(get("/people").accept(MediaType.APPLICATION_JSON))
    .andExpect(jsonPath("$.links[?(@.rel == 'self')].href").value("http://localhost:8080/people"));
```

当XML响应内容包含使用  [Spring HATEOAS](https://github.com/spring-projects/spring-hateoas) 创建的超媒体链接时，您可以使用 XPath 表达式来验证生成的链接：

```java
Map<String, String> ns = Collections.singletonMap("ns", "http://www.w3.org/2005/Atom");
mockMvc.perform(get("/handle").accept(MediaType.APPLICATION_XML))
    .andExpect(xpath("/person/ns:link[@rel='self']/@href", ns).string("http://localhost:8080/people"));
```

##### 异步请求

Servlet 3.0 异步请求，[在 Spring MVC 中受支持](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web.html#mvc-ann-async) ，通过退出 Servlet 容器线程并允许应用程序异步计算响应，然后进行异步调度以完成对 Servlet 容器线程的处理。

在 Spring MVC Test 中，可以通过以下方法测试异步请求：首先声明产生的异步值，然后手动执行异步分派，最后验证响应。下面是对返回 `DeferredResult`，`Callable` 或反应式类型（例如 Reactor `Mono`）的控制器方法的测试示例：

```java
@Test
public void test() throws Exception {
    MvcResult mvcResult = this.mockMvc.perform(get("/path"))
        .andExpect(status().isOk()) 
        .andExpect(request().asyncStarted()) 
        .andExpect(request().asyncResult("body")) 
        .andReturn();

    this.mockMvc.perform(asyncDispatch(mvcResult)) 
        .andExpect(status().isOk()) 
        .andExpect(content().string("body"));
}
```

##### 流式响应

Spring MVC Test 中没有内置选项可用于流式响应的无容器测试。使用 [Spring MVC流式传输](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/web.html#mvc-ann-async-http-streaming) 选项的应用程序可以使用 [WebTestClient](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#webtestclient-stream) 执行端到端 ，针对正在运行的服务器进行集成测试。Spring Boot 也支持此功能，您可以在其中使用 `WebTestClient`  [测试正在运行的服务器](https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#boot-features-testing-spring-boot-applications-testing-with-running-server) 。一个额外的优势是可以使用 Reactor 项目中的 `StepVerifier`，从而可以声明对数据流的期望。

##### 过滤器注册

当我们配置 `MockMvc` 实例时，你可以注册一个或者多个 Servlet `Filter` 实例，如下面例子所示：

```java
mockMvc = standaloneSetup(new PersonController()).addFilters(new CharacterEncodingFilter()).build();
```

已注册的过滤器通过 `spring-test` 中的 `MockFilterChain` 调用，最后一个过滤器委托给 `DispatcherServlet`。

##### Spring MVC 测试 vs 端到端测试

Spring MVC Test 基于 `spring-test` 模块中的 Servlet API 模拟实现而构建，并且不依赖于运行中的容器。因此，与使用实际客户端和实时服务器运行的完整端到端集成测试相比，存在一些差异。

考虑这一点的最简单方法是从空白的 `MockHttpServletRequest` 开始。您添加到其中的内容就是请求的内容。可能令您感到惊讶的是，默认情况下没有上下文路径。没有 `jsessionid` cookie；没有转发，错误或异步调度；因此，没有实际的 JSP 呈现。取而代之的是，“转发” 和 “重定向” URL 保存在 `MockHttpServletResponse` 中，并且可以按预期进行断言。

这意味着，如果您使用 JSP，则可以验证将请求转发到的 JSP 页面，但不会呈现 HTML。换句话说，不调用 JSP。但是请注意，不依赖转发的所有其他渲染技术（例如 Thymeleaf 和 Freemarker）都可以按预期将 HTML 渲染到响应主体。通过 `@ResponseBody` 方法呈现 JSON，XML 和其他格式也是如此。

或者，您可以考虑使用 `@WebIntegrationTest` 从 Spring Boot 获得完整的端到端集成测试支持。请参阅 [Spring Boot参考指南](https://docs.spring.io/spring-boot/docs/current/reference/html/boot-features-testing.html#boot-features-testing-spring-boot-applications) 。

每种方法都各有利弊。从经典的单元测试到全面的集成测试，Spring MVC Test 中提供的选项在规模上是不同的。可以肯定的是，Spring MVC Test 中的所有选项都不属于经典单元测试的范畴，但与之接近。例如，您可以通过将模拟服务注入到控制器中来隔离 Web 层，在这种情况下，您仅通过 `DispatcherServlet` 并使用实际的 Spring 配置来测试 Web 层，因为您可能会在与它上面这些层隔离的情况下测试数据访问层。另外，您可以使用独立设置，一次只关注一个控制器，然后手动提供使其工作所需的配置。

使用 Spring MVC Test 时的另一个重要区别是，从概念上讲，此类测试是服务器端的，因此您可以检查使用了哪个处理程序，如果使用 `HandlerExceptionResolver` 处理了异常，则模型的内容是什么，绑定错误是什么？还有其他细节。这意味着编写期望值更容易，因为服务器不是一个黑盒子，就像通过实际的 HTTP 客户端对其进行测试时那样。通常，这是经典单元测试的一个优势：编写，推理和调试更容易，但不能代替完全集成测试。同时，重要的是不要忽略检查响应是最重要的。简而言之，即使在同一项目中，也可以选择多种样式和测试策略。

##### 更对示例

框架自己的测试包括 [许多示例测试](https://github.com/spring-projects/spring-framework/tree/master/spring-test/src/test/java/org/springframework/test/web/servlet/samples) ，旨在展示如何使用 Spring MVC Test。您可以浏览这些示例以获取更多的点子。另外，[`spring-mvc-showcase`](https://github.com/spring-projects/spring-mvc-showcase) 项目具有基于 Spring MVC Test 的完整测试覆盖范围。

