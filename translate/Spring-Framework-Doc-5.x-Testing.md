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
- [Context Configuration with Environment Profiles](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-env-profiles)
- [Context Configuration with Test Property Sources](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-property-sources)
- [Loading a `WebApplicationContext`](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-web)
- [Context Caching](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-caching)
- [Context Hierarchies](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-ctx-hierarchies)

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

`@ContextConfiguration` supports boolean `inheritLocations` and `inheritInitializers` attributes that denote whether resource locations or annotated classes and context initializers declared by superclasses should be inherited. The default value for both flags is `true`. This means that a test class inherits the resource locations or annotated classes as well as the context initializers declared by any superclasses. Specifically, the resource locations or annotated classes for a test class are appended to the list of resource locations or annotated classes declared by superclasses. Similarly, the initializers for a given test class are added to the set of initializers defined by test superclasses. Thus, subclasses have the option of extending the resource locations, annotated classes, or context initializers.

If the `inheritLocations` or `inheritInitializers` attribute in `@ContextConfiguration` is set to `false`, the resource locations or annotated classes and the context initializers, respectively, for the test class shadow and effectively replace the configuration defined by superclasses.

In the next example, which uses XML resource locations, the `ApplicationContext` for `ExtendedTest` is loaded from `base-config.xml` and `extended-config.xml`, in that order. Beans defined in `extended-config.xml` can, therefore, override (that is, replace) those defined in `base-config.xml`. The following example shows how one class can extend another and use both its own configuration file and the superclass’s configuration file:

````
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

Similarly, in the next example, which uses annotated classes, the `ApplicationContext` for `ExtendedTest` is loaded from the `BaseConfig` and `ExtendedConfig` classes, in that order. Beans defined in `ExtendedConfig` can, therefore, override (that is, replace) those defined in `BaseConfig`. The following example shows how one class can extend another and use both its own configuration class and the superclass’s configuration class:

````
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

In the next example, which uses context initializers, the `ApplicationContext` for `ExtendedTest` is initialized by using `BaseInitializer` and `ExtendedInitializer`. Note, however, that the order in which the initializers are invoked depends on whether they implement Spring’s `Ordered` interface or are annotated with Spring’s `@Order` annotation or the standard `@Priority` annotation. The following example shows how one class can extend another and use both its own initializer and the superclass’s initializer:

````
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

