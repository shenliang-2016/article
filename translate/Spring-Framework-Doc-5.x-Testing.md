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

接下来几个小姐介绍每个目标并提供有关实现和配置细节的链接。

#### 3.2.1. 上下文管理和缓存

Spring TestContext 框架提供了 Spring `ApplicationContext` 实例和 `WebApp

The Spring TestContext Framework provides consistent loading of Spring `ApplicationContext` instances and `WebApplicationContext` instances as well as caching of those contexts. Support for the caching of loaded contexts is important, because startup time can become an issue — not because of the overhead of Spring itself, but because the objects instantiated by the Spring container take time to instantiate. For example, a project with 50 to 100 Hibernate mapping files might take 10 to 20 seconds to load the mapping files, and incurring that cost before running every test in every test fixture leads to slower overall test runs that reduce developer productivity.

Test classes typically declare either an array of resource locations for XML or Groovy configuration metadata — often in the classpath — or an array of annotated classes that is used to configure the application. These locations or classes are the same as or similar to those specified in `web.xml` or other configuration files for production deployments.

By default, once loaded, the configured `ApplicationContext` is reused for each test. Thus, the setup cost is incurred only once per test suite, and subsequent test execution is much faster. In this context, the term “test suite” means all tests run in the same JVM — for example, all tests run from an Ant, Maven, or Gradle build for a given project or module. In the unlikely case that a test corrupts the application context and requires reloading (for example, by modifying a bean definition or the state of an application object) the TestContext framework can be configured to reload the configuration and rebuild the application context before executing the next test.

See [Context Management](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management) and [Context Caching](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-caching) with the TestContext framework.