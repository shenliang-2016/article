# 目录

----

## Overview

history, design philosophy,feedback, getting started.

## Core

IoC container, Events, Resources, i18n, Validation, Data Binding, Type Conversion, SpEL, AOP.

## Testing

Mock objects, TestContext framework, Spring MVC Test, WebTestClient.

## Data Access

Transactions, DAO support, JDBC, ORM, Marshalling XML.

## Web Servlet

Spring MVC, WebSocket, SockJS, STOMP messaging.

## Web Reactive

Spring WebFlux, WebClient, WebSocket.

## Integration

Remoting, JMS, JCA, JMX, Email, Tasks, Scheduling, Cache.

## Languages

Kotlin, Groovy, Dynamic languages.

----

# 概述

----

Spring 使得创建 Java 企业级应用成为一项令人愉快的工作。它提供了你在企业级环境下应用 Java 语言所需要的一切，支持包括 Groovy、Kotlin 等备选 JVM 语言，支持根据应用需要灵活创建不同的技术架构的扩展性。作为框架的5.0版本，需要 JDK 8+ 环境，同时框架已经提供了 JDK 9 的开箱即用的支持。

Spring 支持非常广泛的应用场景。大型企业应用经常需要运行很长时间，而 JDK 和应用服务器的更新周期并不在开发者控制下。另外一些应用可以作为服务器内置的插件 jar 形式运行，可能就是在云环境中。还有一些作为独立服务运行甚至都不需要服务器软件环境。

Spring 是开源框架。背靠庞大而活跃的社区，随时收到来自全球各种真实应用环境的改进建议。这些帮助 Spring 在相当长的时期内不断进化完善。

## 1. Spring  是什么意思

Spring 这个词在不同的语境下有不同的含义。可以用于指代 Spring 框架本身，这也是它的最初含义。随着时间推移，其它的  Spring 项目基于 Spring 框架逐步构建起来。但多数情况下，人们谈到 Spring ，指的其实是整个项目家族。本参考文档只关注基础，Spring 框架本身。

Spring 框架被分为多个模块。应用可以各取所需。处于核心地位的是所谓的核心容器，包括一个配置模型和一套依赖注入机制。在此之外，框架提供了对多种不同应用技术架构的基础支持，包括消息、数据事务和持久化以及 web 。框架还包括基于 Servlet 的 Spring MVC web 框架，以及与之平行的，Spring WebFlux 响应式 web 框架。

关于模块的说明：

Spring 框架的 jar 包可以部署到 JDK 9 的模块路径（“Jigsaw”）下。当然，框架的模块在 JDK 8 和 JDK 9 的 classpath 下都可以正常工作。

## 2. Spring 和 Spring 框架的历史

Spring 作为对早期 J2EE 规范复杂性的反击，诞生于2003年。尽管通常被认为与 Java EE 是竞争关系，实际上，Spring 在很大程度上正是 Java EE 规范的实现。Spring 的编程模型不符合 Java EE 平台规范，不过，它却很谨慎地集成了越来越多来自 EE 范畴的技术规范。

- Servlet API ([JSR 340](https://jcp.org/en/jsr/detail?id=340))
- WebSocket API ([JSR 356](https://www.jcp.org/en/jsr/detail?id=356))
- Concurrency Utilities ([JSR 236](https://www.jcp.org/en/jsr/detail?id=236))
- JSON Binding API ([JSR 367](https://jcp.org/en/jsr/detail?id=367))
- Bean Validation ([JSR 303](https://jcp.org/en/jsr/detail?id=303))
- JPA ([JSR 338](https://jcp.org/en/jsr/detail?id=338))
- JMS ([JSR 914](https://jcp.org/en/jsr/detail?id=914))
- as well as JTA/JCA setups for transaction coordination, if necessary.

Spring 框架也支持依赖注入 ([JSR 330](https://www.jcp.org/en/jsr/detail?id=330)) 和通用注解 ([JSR 250](https://jcp.org/en/jsr/detail?id=250)) 规范，因此应用开发者可以选择它们代替 Spring 框架提供的特有实现机制。

作为 Spring 框架的5.0版本，最低需要 Java EE 7 水平 (e.g. Servlet 3.1+, JPA 2.1+) 的支持，当然框架同时提供了在运行时开箱即用即成更高版本 APIs 的能力，比如 Java EE 8 (e.g. Servlet 4.0, JSON Binding API) 。这就保证了 Spring 可以完美兼容 Tomcat 8 和 9 ，WebSphere 9 以及 JBoss EAP 7 。

时光荏苒，Java EE 在应用开发中的角色也早已今非昔比。在 Java EE 和 Spring 的早期，人们开发的应用都是部署在应用服务器上。如今，在 Spring Boot 的帮助下，人们采用所谓的 “开发－运维－云” 友好的方式创建应用，同时内置 Servlet 容器。采用此版本的框架，WebFlux 应用甚至都不再使用 Servlet API ，而是能够直接运行在非 Servlet 容器的服务器上。

Spring 仍在持续进化和完善。除了 Spring 框架本身，还有大量其它项目，Spring Boot, Spring Security, Spring Data, Spring Cloud, Spring Batch，等等。需要注意的是，每个项目都有自己独立的代码仓库、问题跟踪以及发布节奏。在  [spring.io/projects](https://spring.io/projects) 可以找到所有的项目列表。

## 3. 设计哲学

学习一个框架，重要的不仅是了解它都做了什么，更重要的是把握它所遵循的基本原则。Spring 框架的指导思想如下：

* 提供各个层面的选择。Spring 支持你尽可能晚地做出设计决策。例如，你可以通过修改配置文件的方式切换持久化提供者，而不需要修改代码。类似的做法也适用于很多其它的基础组件和第三方 APIs 的集成。
* 不同角度的协调。Spring 提供丰富的扩展性，但是并不替你做任何决定。它从不同角度提供了很广泛的应用需求支持。
* 保持向后兼容。Spring 的进化很谨慎，尽可能少地在新版本中改变已有功能特性的修改。同时，很谨慎地选择 JDK 版本和第三方库，便于基于 Spring 的应用和库的维护。
* 谨慎的 API 设计。Spring 团队投入了大量的精力和时间进行 API 设计，尽力在所有版本中始终保持 API 的直观性。
* 重视代码质量。Spring 框架投入大量努力保持文档的清晰精确并及时更新。同时，它也是为数不多的几个敢于公开声称拥有干净的代码结构而绝对不存在包的循环依赖的项目之一。

## 4. 反馈和贡献

## 5. 新手上路

----

# 核心技术

----

这一部分涵盖了 Spring 框架必需的所有技术。

所有核心技术中最重要的就是所谓的控制反转 IoC 容器。为了对 Spring 框架的 IoC 容器进行彻底的分析，我们将全面介绍 Spring 的面向切面编程（AOP）技术。Spring Framework 有自己的 AOP 框架，它在概念上易于理解，并且成功地覆盖了 Java 企业编程中 AOP 的80％的应用场景。

同时提供了 Spring 与 AspectJ，目前在功能层面最丰富的 Java 企业级领域最成熟的 AOP 实现，的技术支持。

## 1. IoC 容器

本章介绍 Spring 的控制反转（IoC）容器。

### 1.1 Spring IoC容器和Bean简介

本章介绍了控制反转（IoC）技术的 Spring Framework 实现。（参见[控制反转](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/overview.html#background-ioc)。）IoC 也称为依赖注入（DI）。这是一个过程，通过这个过程，对象只能通过构造函数参数，工厂方法的参数或在从工厂方法构造或返回的对象实例上设置的属性来定义它们的依赖关系（即，它们使用的其他对象）。 然后容器在创建 bean 时注入这些依赖项。这个过程基本上是 bean 本身通过使用类的直接构造或诸如服务定位器模式之类的机制来控制其依赖关系的实例化或位置的逆（因此被称作控制反转）。

`org.springframework.beans`和`org.springframework.context`包是 Spring 框架的 IoC 容器的基础。其中的 [`BeanFactory`](https://docs.spring.io/spring-framework/docs/5.1.3.RELEASE/javadoc-api/org/springframework/beans/factory/BeanFactory.html) 接口提供了一种能够管理任何类型对象的高级配置机制。 [`ApplicationContext`](https://docs.spring.io/spring-framework/docs/5.1.3.RELEASE/javadoc-api/org/springframework/context/ApplicationContext.html) 是一个`BeanFactory`的子接口。它添加了以下方法：

* 更加简单的与 Spring AOP 特性集成
* 消息资源处理（以便于在国际化中使用）
* 事件发布
* 应用层特定的上下文，以便于在 web 应用中使用，比如````WebApplicationContext````

简单说，````BeanFactory````提供了配置框架和基本功能，而````ApplicationContext````添加了更多企业级特定的功能。后者是前者的完整超集，而且被专门用在描述 Spring IoC 容器的章节中。更多有关使用````BeanFactory````的信息参见 [The `BeanFactory`](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-beanfactory)

在 Spring 中，构成你的应用骨架而又由 Spring IoC 容器管理的对象被称为 beans 。bean 是由 Spring IoC 容器实例化、装配并管理的对象。同时，bean 又是你的应用内各种对象之中很简单的一类。Beans 和它们之间的依赖关系都反映在容器所使用的配置元数据中。

### 1.2 容器概述

````org.springframework.context.ApplicationContext````接口表示 Spring IoC 容器，负责 beans 的实例化、配置和装配。容器从配置元数据中读取对象实例化、配置和装配的说明。该配置元数据可以是 XML 文件、Java 注解或者 Java 代码形式。它允许你表达构成你应用的各种对象以及它们之间丰富的依赖关系。

Spring 提供了几种````ApplicationContext````接口的实现。在独立安装的应用中，通常会创建一个 [`ClassPathXmlApplicationContext`](https://docs.spring.io/spring-framework/docs/5.1.4.RELEASE/javadoc-api/org/springframework/context/support/ClassPathXmlApplicationContext.html) 或者 [`FileSystemXmlApplicationContext`](https://docs.spring.io/spring-framework/docs/5.1.4.RELEASE/javadoc-api/org/springframework/context/support/FileSystemXmlApplicationContext.html) 的实例。因为 XML 文件是定义配置元数据的传统格式，你可以通过一个简短的 XML 配置文件来宣布容器支持 Java 注解或者代码形式的配置元数据，然后你就可以使用这些额外的形式来声明配置元数据了。

在大部分应用场景下，通过显式的用户代码来实例化一个或者多个 Spring IoC 容器不是必需的。比如，在一个 web 应用中，一个简单的 8 行（大约）的通用模板 web 描述符 XML 位于````web.xml````文件中就是够用的（参考 [Convenient ApplicationContext Instantiation for Web Applications](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#context-create)）。如果你使用 [Spring Tool Suite](https://spring.io/tools/sts) ，你就可以通过该工具很简单地自动生成该模板配置文件。

下图展示了一个 Spring 工作原理的高层视图。你的应用中的类基于配置元数据被如此组合起来，在````ApplicationContext````被创建和初始化之后，你就拥有了一个配置完善而且可执行的系统或者应用。

![img](file:///C:\Users\liang.shen\AppData\Roaming\Tencent\Users\61856119\QQ\WinTemp\RichOle\3G8L@JY2X2CXY2YPJ$1}{DX.png)

#### 1.2.1 配置元数据

如上图所示，Spring IoC 容器消费一个配置元数据形式。该配置元数据表示你将如何，作为一个应用开发者，告诉 Spring 容器实例化、配置以及装配应用中的对象。

配置元数据传统上以简单的 XML 格式给出，本章节中也使用这种形式来说明 Spring IoC 容器的关键概念和特性。

> 基于 XML 的元数据并不是唯一允许的配置元数据形式。Spring IoC 容器自身与具体的配置元数据的格式完全隔离。近来，越来越多的开发者选择在他们的 Spring 应用中使用 [Java-based configuration](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-java) 。

获取更多有关使用其它元数据形式的信息参见：

* [Annotation-based configuration](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-annotation-config)：Spring 2.5 引入了基于注解的配置元数据形式支持。
* [Java-based configuration](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-java)：从 Spring 3.0 开始，来自 Spring JavaConfig 项目的许多特性成为 Spring 核心框架的一部分。因此，你可以使用 Java 代码定义应用中的 bean，而不是使用 XML 文件。使用这些新特性，参考 [`@Configuration`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Configuration.html), [`@Bean`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Bean.html), [`@Import`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/Import.html), 和 [`@DependsOn`](https://docs.spring.io/spring-framework/docs/current/javadoc-api/org/springframework/context/annotation/DependsOn.html) 注解。

Spring 配置包含至少一个，通常是多个容器必须管理的 bean 定义。XML 形式的配置元数据文件在顶级````<beans/>````元素中以````<bean/>````元素形式配置它们。Java 代码配置方式通常在````@Configuration````注解的类中使用````@Bean````注解的方法来声明它们。

这些 bean 定义对应于构成你的应用的具体对象。典型地，你定义服务层对象、数据访问对象 DAOs 、表示对象，比如 Structs Action 实例、基础设施对象，比如 Hibernate ````SessionFactories````，JMS````Queues````，等等。典型地，开发者通常不会在容器中配置细粒度的域对象，因为创建和加载域对象通常是 DAOs 和业务逻辑的任务。然而，你可以将 AspectJ集成到 Spring 中来以配置那些在容器控制之外创建的对象。参考 [Using AspectJ to dependency-inject domain objects with Spring](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#aop-atconfigurable)。

下面是一个 XML 配置元数据的例子：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd">
  <bean id="..." class="...">
    <!-- bean 的协作者和配置放在这里 -->
  </bean>
  <bean id="..." class="...">
    <!-- bean 的协作者和配置放在这里 -->
  </bean>
  <!-- 更多 bean 的定义放在这里 -->
</beans>
````

其中的：

````id````属性是 bean 定义的字符串形式的唯一标识符。

````class````属性是 bean 定义使用的类型的全限定类名。

````id````属性的值指的是协作的对象。关于协作对象的 XML 并没有在例子中体现，参考 [Dependencies](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-dependencies) 获取更多信息。

#### 1.2.2 实例化一个容器

提供给````ApplicationContext````构造器的路径集合是资源字符串，该字符串指导容器从各种外部资源加载配置元数据，比如从本地文件系统，Java ````CLASSPATH````，等等。

````java
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");
````

> 学习 Spring IoC 容器之后，你可能会想要更多了解 Spring 的资源抽象（在 [Resources](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#resources) 中描述），它提供了一套从 URI 语法定义的资源位置中读取一个输入流的方便机制。特别地，````Resource````路径被用于构建应用上下文，就像 [Application Contexts and Resource Paths](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#resources-app-ctx) 中描述的那样。

下面的例子展示了服务层对象````services.xml````配置文件：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <!-- services -->

    <bean id="petStore" class="org.springframework.samples.jpetstore.services.PetStoreServiceImpl">
        <property name="accountDao" ref="accountDao"/>
        <property name="itemDao" ref="itemDao"/>
        <!-- additional collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions for services go here -->

</beans>
````

下面的例子展示了数据访问对象````daos.xml````配置文件：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="accountDao"
        class="org.springframework.samples.jpetstore.dao.jpa.JpaAccountDao">
        <!-- additional collaborators and configuration for this bean go here -->
    </bean>

    <bean id="itemDao" class="org.springframework.samples.jpetstore.dao.jpa.JpaItemDao">
        <!-- additional collaborators and configuration for this bean go here -->
    </bean>

    <!-- more bean definitions for data access objects go here -->

</beans>
````

