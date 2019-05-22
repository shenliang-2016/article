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

![spring ioc container](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/spring/image-20190202210745626.png)

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

上面的例子中，服务层由````PetStoreServiceImpl````类以及两个数据访问对象，类型分别为````JpaAccountDao````和````JpaItemDao````（基于 JPA 对象-关系映射标准）组成。````property name````元素指的是 JavaBean 属性的名称，````ref````元素指的是另一个 bean 定义的名字。````id````元素和````ref````元素之间的联系表达了协作对象之间的依赖关系。更多有关配置对象依赖关系的信息参见 [Dependencies](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-dependencies)。

##### 组成基于 XML 的配置元数据

bean 定义可以横跨多个 XML 文件是很有用的。通常，每个单独的 XML 配置文件都表示你的架构中一个逻辑层次或者模块。

你可以使用应用上下文构造器从所有这些 XML 片段中加载 bean 定义。该构造器持久多个````Resource````位置，就像上一节中描述的那样。另外，还使用一个或者多个````<import/>````元素从另外的文件中加载 bean 定义。下面是一个例子：

````xml
<beans>
  <import resource="services.xml"/>
  <import resource="resources/messageSource.xml"/>
  <import resource="/resources/themeSource.xml"/>
  
  <bean id="bean1" class="..."/>
  <bean id="bean2" class="..."/>
</beans>
````

上面的例子中，外部的 bean 定义从三个文件中加载：````services.xml````、````messageSource.xml````和````themeSource.xml````。所有的位置路径都是相对于执行导入操作的定义文件，因此````services.xml````文件必须位于执行导入操作的定义文件的相同目录或者 classpath 位置下，而````messageSource.xml````和````themeSource.xml````文件必须位于执行导入操作的文件所在目录的````resources````子目录中。正如你所看到的，路径开头的斜杠可以被忽略。然而，由于给出的都是相对路径，更好的做法是完全不使用斜杠。被导入的文件内容，包含顶层的````<beans/>````元素，必须是合法的 XML bean 定义，基于 Spring 规范。

> 有可能可行，然而并不推荐的做法是使用相对路径````../````来引用父目录中的文件。这样做可以创建对当前应用之外的文件的依赖。特别的，这种引用不推荐用在````classpath````URLs（比如````classpath:../services.xml````），此时运行时解析过程会选择最近的 classpath 根目录然后进入它的父目录查找。Classpath 配置的变化就会导致该选择发生变化从而进入错误的目录。
>
> 你永远可以使用全限定的资源位置，而不是相对路径。比如````file:C:/config/services.xml````或者````classpath:/config/services.xml````。不过，这样也就把你的应用的配置耦合到了某些特定的绝对位置。通常更好的做法是保持一定程度的相对性，比如通过````${...}````占位符，该占位符被运行时用来解析 JVM 系统属性。

命名空间本身提供了导入命令特性。除了普通的 bean 定义，高级的配置特性可以通过在 Spring 提供的 XML 命名空间中选择。比如````context````和````util````命名空间。

##### Groovy Bean 定义 DSL

作为外部配置元数据的高级例子，还可以通过 Spring's Groovy Bean Definition DSL 进行 bean 定义，就像在 Grails 框架中那样。典型地，这种配置存在于````.groovy````文件中，结构如下面例子所示：

````groovy
beans {
    dataSource(BasicDataSource) {
        driverClassName = "org.hsqldb.jdbcDriver"
        url = "jdbc:hsqldb:mem:grailsDB"
        username = "sa"
        password = ""
        settings = [mynew:"setting"]
    }
    sessionFactory(SessionFactory) {
        dataSource = dataSource
    }
    myService(MyService) {
        nestedBean = { AnotherBean bean ->
            dataSource = dataSource
        }
    }
}
````

这种配置形式基本上等价于 XML bean 定义，甚至都支持 Spring 的 XML 配置命名空间。同时，它也允许通过````importBeans````命令导入 XML bean 定义文件。

#### 1.2.3 使用容器

````ApplicationContext````是一个接口，作为一个先进的工厂，具有保持不同 beans 和它们之间的依赖关系的注册数据的能力。通过使用````getBean(String name, Class<T> requiredType)````方法，你可以或族群你的 beans 的实例。

````ApplicationContext````允许你读取和使用 bean 定义，如下面例子所示：

````java
// create and configure beans
ApplicationContext context = new ClassPathXmlApplicationContext("services.xml", "daos.xml");

// retrieve configured instance
PetStoreService service = context.getBean("petStore", PetStoreService.class);

// use configured instance
List<String> userList = service.getUsernameList();
````

使用 Groovy 配置时，步骤看起来非常类似。区别在于不同的上下文实现类是 Groovy 敏感的（同样理解 XML bean 定义）。下面例子展示使用 Groovy 配置时的情形：

````java
ApplicationContext context = new GenericGroovyApplicationContext("services.groovy", "daos.groovy");
````

最灵活的变体时结合使用````GenericApplicationContext````和读取代理，比如````XmlBeanDefinitionReader````用于读取 XML 文件，如下面例子所示：

````java 
GenericApplicationContext context = new GenericApplicationContext();
new XmlBeanDefinitionReader(context).loadBeanDefinitions("services.xml", "daos.xml");
context.refresh();
````

你也可以使用````GroovyBeanDefinitionReader````来读取 Groovy 文件，如下所示：

````java
GenericApplicationContext context = new GenericApplicationContext();
new GroovyBeanDefinitionReader(context).loadBeanDefinitions("services.groovy", "daos.groovy");
context.refresh();
````

你可以混合使用这些读取代理到同一个````ApplicationContext````上，从各种不同的配置源读取 bean 定义。

接下来你可以使用````getBean````方法获取 beans 实例。````ApplicationContext````接口也提供了少量几个获取 beans 的方法。但是，理论上，你的应用代码不能使用它们。事实上，你的应用代码中绝对不应该出现````getBean()````方法调用，因此也就不会对 Spring API 产生任何依赖。比如，Spring 与 web 框架的集成机制提供了依赖注入机制为各种 web 框架组件使用，比如 controllers 和 JSF-managed beans ，允许你通过元数据声明对某个特定 bean 的依赖（比如 autowiring 注解）。

### 1.3 Bean 概述

一个 Spring IoC 容器管理一个或者多个 beans 。这些 beans 基于你提供给容器的配置元数据（比如，以 XML 形式）创建。

在容器自身内容，这些 beans 定义表现为````BeanDefinition````对象，其中包含下列元数据（当前还有其它信息）：

* 一个包限定了类名：典型的，就是被定义的 bean 的具体实现类。
* Bean 动作配置元素，表示 bean 在容器中的行为（作用域、生命周期回调等等）。
* 该 bean 完成它的工作所需要的其它 beans 的引用。这些引用也被称为协作者或者依赖。
* 其它在创建新的对象时需要的配置设定。比如，管理连接池的 bean 使用的连接池的大小限制或者连接数限制。

这些元数据转换成每个 bean 定义的属性集合。下表描述了这些属性：

| 属性                       | 解释                                       |
| ------------------------ | ---------------------------------------- |
| Class                    | [Instantiating Beans](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-class) |
| Name                     | [Naming Beans](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-beanname) |
| Scope                    | [Bean Scopes](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-scopes) |
| Constructor arguments    | [Dependency Injection](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-collaborators) |
| Properties               | [Dependency Injection](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-collaborators) |
| Autowiring mode          | [Autowiring Collaborators](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-autowire) |
| Lazy initialization mode | [Lazy-initialized Beans](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-lazy-init) |
| Initialization method    | [Initialization Callbacks](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-initializingbean) |
| Destruction method       | [Destruction Callbacks](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-disposablebean) |

除了包含如何创建特定 bean 的信息的 bean 定义之外，````ApplicationContext````实现也允许在容器之外由用户创建的已经存在的对象注册。此特性的实现过程为：访问````ApplicationContext````的````getBeanFactory()````方法以获取````BeanFactory````的实现类````DefaultListableBeanFactory````。````DefaultListableBeanFactory````通过````registerSingleton(...)````和````registerBeanDefinition(...)````方法支持这种对象注册。然而，典型情况下应用通常仅仅使用通过 bean 定义元数据定义的 beans 工作。

> Bean 元数据和手工提供的单例实例需要被尽早注册，为了保证容器可以正确理解它们并在自动装配和其它自省过程中使用。尽管某种程度上覆盖现有的元数据和单例实例是支持的，运行时新 beans 注册（与 beans 工厂的正常访问并发）却并没有被官方支持，可能会导致并发访问异常，bean 容器内状态不一致，或者两者兼有。

#### 1.3.1 Beans 命名

每个 bean 都有一个或者多个标识符，这些标识符必须是容器范围唯一的。通常一个 bean 只有一个标识符。然而，如果真的需要另外的标识符，则其它的都会被当作是别名。

基于 XML 的配置元数据中，你使用````id````属性，````name````属性，或者同时使用两者来作为特定 bean 的标识符。````id````属性使得你可以指定一个特定的 id。方便起见，这些名称都是字母组成的，不过它们也可以包含特殊字符。如果你想为该 bean 添加其它别名，你可以通过````name````属性指定，多个别名通过逗号、分号或者空格分隔。作为历史记录，在 Spring 3.1 之前的版本中，````id````属性被定义为````xsd:ID````类型，因而限制了可用的字符。在 3.1 版本中，它被定义为````xsd:string````类型。注意，bean ````id````的唯一性仍然将由容器来保证，而不再通过 XML 解析器保证。

你不一定要为 bean 提供一个````name````或者````id````，这并不是强制的。如果你没有显式提供````name````或者````id````，容器就会为 bean 产生一个唯一的名称。然而，如果你希望可以通过名字引用到 bean，通过使用````ref````元素或者 [Service Locator](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-servicelocator) 形式的搜索，你就必须提供一个名字。不提供名称的动机主要是使用 [inner beans](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-inner-beans) 和 [autowiring collaborators](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-autowire) 。

**Bean 命名传统**

Bean 命名的传统是遵循 Java 实例变量命名规范。也就是说，bean 的名字以小写字母开头，并且是驼峰写法。比如 accountManager，userDao 等等。

规范命名将使得你的配置文件简单易懂，同时，如果你使用 Spring AOP，它将在你将所谓的增强应用到名称关联的 beans 集合时会有很大帮助。

> 在 classpath 中扫描组件的同时，Spring 会为尚未命名的组件生成 bean 名称，遵循上面描述的规则，基本上地，采用简单类名，将首字母小写。然而，某些特殊情况下，当存在多个字符而且第一个字符和第二个字符都是大写时，这个原始形式就会被保留。此规则与````java.beans.Introspector.decapitalize````中定义的相同。

##### 在 Bean 定义之外指定别名

在 bean 定义中，你可以为 bean 提供一个或者多个名字，通过结合使用````id````属性中指定一个名称，同时在````name````属性中指定任意多个其它名字的方式。这些名字作为同一个 bean 的等价别名，在很多情况下都是非常有用的，比如允许应用中的每个组件持有一个公共依赖的引用，通过它们自身特定的 bean 别名。

在 bean 定义时指定所有的别名并不是所有情况下都合适，有时候我们会想要为在别处定义的 bean 添加别名。这种情况在那种配置分散在大量子系统的大型系统中普遍存在，每个子系统都有自己的对象定义集合。在基于 XML 的配置元数据中，你可以使用````<alias/>````元素来实现此目的。下面是个例子：

````xml
<alias name="fromName" alias="toName"/>
````

这种情况下，一个 bean （同一个容器内）可能也叫做````fromName````，在此别名定义被使用之后，将被通过````toName````引用。

比如，子系统 A 的配置元数据通过名字````subsystemA-dataSource````引用一个数据源。子系统 B 使用名字````subsystemB-dataSource````引用一个数据源。当构成同时使用这两个子系统的主应用时，该主应用通过名字````myApp-dataSource````引用该数据源。为了保证所有三个名字都能够引用同一个对象，你可以在配置元数据中添加以下别名定义：

````xml
<alias name="myApp-dataSource" alias="subsystemA-dataSource"/>
<alias name="myApp-dataSource" alias="subsystemB-dataSource"/>
````

现在每个组件和主应用就都可以通过各自唯一的名字引用数据源，而且可以保证不会与任何其它定义冲突（事实上是创建了一个命名空间），同时它们引用的还是同一个 bean 。

**Java 配置**

如果你使用的是基于 Java 代码的配置，则````@Bean````注解可以用于指定别名。参考 [Using the `@Bean` Annotation](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-java-bean-annotation) 获取更多细节。

#### 1.3.2 实例化 Beans

Bean 定义是创建一个或者多个对象的根本食谱。当需要使用包装在 bean 定义中的配置元数据时，容器在其中查找命名的 bean 信息来创建或者获取一个具体的对象。

如果你使用基于 XML 的配置元数据，你需要在````<bean/>````元素的````class````属性中指定将被实例化的对象的类型。该````class````属性（在内部，是````BeanDefinition````实例的````Class````属性）通常是强制的（例外的情况，参见 [Instantiation by Using an Instance Factory Method](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-class-instance-factory-method) 和 [Bean Definition Inheritance](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-child-bean-definitions)）。可以通过以下两种方式使用````Class````属性：

* 典型的，指定 bean 将被构造的类型然后容器就可以通过反射调用该类型的构造器直接创建该 bean ，某种程度上等价于 Java 代码中使用````new````操作符。
* 指定包含````static````工厂方法的具体类型，调用该方法可以创建对象，某些情况下容器会调用该````static````工厂方法创建 bean 。该方法返回的对象类型可以是指定类型或者其它类型。

> *内部类名称*
>
> 如果你想为一个````static````内部类配置一个 bean 定义，就必须使用该内部类的二进制名称。
>
> 比如，如果你有一个名为````SomeThing````的类位于````com.example````包下，同时该类有一个名为````OtherThing```` 的````static````内部类，则对应的 bean 定义的````class````属性值应该是````com.example.SomeThing$OtherThing````。
>
> 注意在类型名称中使用````$````字符分隔内部类名和外部类名。

##### 使用构造器实例化

当你使用构造器方式创建 bean 时，所有正常的类都是兼容 Spring 并可以为其所用的。也就是说，你开发的类不需要实现任何特定接口或者遵循内容特定规范。简单地指定 bean 类型就足够了。然而，取决于你为特定的 bean 所使用的具体 IoC 容器类型，你可能需要一个默认（空的）构造器方法。

Spring IoC 容器可以管理任何你希望它管理的类型，它可以没有任何限制地管理真实的 JavaBeans。大多数 Spring 用户更习惯使用只有一个默认无参构造器、属性以及对应的 setters 和 getters 方法的 JavaBeans。你当然可以使用其它非 JavaBean 风格的类型。比如，你需要使用一个老式连接池类，而它完全不符合 JavaBean 规范，Spring 仍然可以毫无问题地管理它。

在基于 XML 的配置元数据中，你可以如下指定 bean 类型：

````xml
<bean id="exampleBean" class="examples.ExampleBean"/>
<bean name="anotherExample" class="examples.ExampleBeanTow"/>
````

关于向构造器提供更多参数以及在对象构造之后设置对象实例属性的机制参见 [Injecting Dependencies](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-collaborators)。

**通过静态工厂方法实例化**

当定义通过静态工厂方法创建的 bean 时，使用````class````属性指定包含该````static````工厂方法的类，使用````factory-method````属性指定工厂方法本身。你应该可以调用该方法（使用可选参数，稍后将要介绍）并返回一个活动的对象，接下来该对象会被像通过构造器创建出来的对象那样对待。这种 bean 定义的一个使用场景是调用遗留代码中的````static````工厂方法。

下面的 bean 定义制定了通过调用一个工厂方法创建 bean。该定义没有指定工厂方法返回对象的类型，只制定了包含该方法的类。该例子中````createInstance()````方法必须是````static ````的。下面例子展示了这种 bean 定义：

````xml
<bean id="clientService"
      class="examples.ClientService"
      factory-method="createInstance"/>
````

其中的类：

`````java
public class ClientService {
  private static ClientService clientService = new ClientService();
  private ClientService(){
    
  }
  public static ClientService createInstance(){
    return clientService;
  }
}
`````

更多有关为工厂方法提供可选参数以及为该方法返回的对象设置属性的机制参见 [Dependencies and Configuration in Detail](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-properties-detailed)。

**使用实例工厂方法实例化**

类似于通过静态工厂方法的实例化，这种方法通过调用容器中现存的 bean 实例的非静态方法创建新的 bean 。为了使用该机制，将````class````属性置空，同时在````factory-bean````属性中指定在当前（或者父或者祖先）容器中的包含该实例方法（调用它可以创建新的对象）的 bean 名称。将工厂方法的名称设置到````factory-method````属性中。下面是个例子：

````xml
<!-- the factory bean, which contains a method called createInstance() -->
<bean id="serviceLocator" class="examples.DefaultServiceLocator">
  <!-- inject any dependencies required by this Locator bean -->
</bean>

<!-- the bean to be created via the factory bean -->
<bean id="clientService"
      factory-bean="serviceLocator"
      factory-method="createClientServiceInstance"/>
````

相应的类：

````java
public class DefaultServiceLocator {
  private static ClientService clientService = new ClientServiceImpl();
  public ClientService createClientServiceInstance(){
    return clientService;
  }
}
````

工厂类可以拥有多个工厂方法，如下所示：

````xml
<bean id="serviceLocator" class="examples.DefaultServiceLocator">
    <!-- inject any dependencies required by this locator bean -->
</bean>

<bean id="clientService"
    factory-bean="serviceLocator"
    factory-method="createClientServiceInstance"/>

<bean id="accountService"
    factory-bean="serviceLocator"
    factory-method="createAccountServiceInstance"/>
````

相应的类：

````java
public class DefaultServiceLocator {

    private static ClientService clientService = new ClientServiceImpl();

    private static AccountService accountService = new AccountServiceImpl();

    public ClientService createClientServiceInstance() {
        return clientService;
    }

    public AccountService createAccountServiceInstance() {
        return accountService;
    }
}
````

这种方法展示了工厂 bean 本身也可以通过依赖注入被管理和配置，详情参见 [Dependencies and Configuration in Detail](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-properties-detailed)。

> 在 Spring  文档中，factory bean 指的是被配置到 Spring 容器中，通过实例或者静态工厂方法传经对象的 bean。与此不同的是````FactoryBean````（注意其中的大写字母）指的是 Spring 特定的````FactoryBean````。

### 1.4 依赖

一个典型的企业级不会仅仅只包含一个对象（在 Spring 中称为 bean）。即使是最简单的应用也包含一定数量的共同工作的对象来完成用户任务。接下来的章节解释你应该如何定义一系列的 bean 并将它们组成称为一个完整应用以完成任务目标。

#### 1.4.1 依赖注入

依赖注入（DI）是一种过程，对象通过该过程定义它们的依赖（也就是它们工作需要的其它对象），只通过构造器参数、工厂方法参数后者为构造完成之后或者由工厂方法返回的对象实例设置属性。然后容器在它创建这些 bean 的时候注入其中的依赖。此过程根本上反转了 bean 自身对它所依赖的对象的实例化或者位置的控制权，通过直接进行类构造或者服务定位模式。也就是所谓的控制反转。

遵循依赖注入的代码会更加干净，同时对象连同它们的依赖共同提供也实现了充分解耦。对象不再需要寻找它的依赖，而且也不知道依赖类型的位置。这样一来，你的类型变得更加容器测试，特别是当依赖的是接口或者抽象类时，在单元测试中你就可以使用代理桩或者 mock 实现。

依赖注入有两种变体：[Constructor-based dependency injection](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-constructor-injection) 和 [Setter-based dependency injection](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-setter-injection)。

**基于构造器的依赖注入**

构造器依赖注入通过容器携带若干参数调用构造方法实现，每个参数都表示一个依赖。通过携带特定参数对````static````工厂方法的调用来构造 bean 与此基本等价，同时此讨论中将构造方法参数和````static````工厂方法参数类似对待。下面的例子展示了通过构造器进行依赖注入的做法：

````java
public class SimpleMovieLister {
  // the SimpleMovieLister has a dependency on a MovieFinder
  private MovieFinder movieFinder;
  
  // a constructor so that the Spring container can inject a MovieFinder
  public SimpleMovieLister(MovieFinder movieFinder) {
    this.movieFinder = movieFinder;
  }
  
  // businesss logic that actually uses the injected MovieFinder is omitted...
}
````

注意，这个类并没有任何特殊的。它只是一个普通的类，没有通过类或者注解引入任何对容器特定接口的依赖。

**构造器参数解析**

构造器参数解析基于使用的参数的类型进行匹配。如果 bean 定义中没有潜在的构造器参数混淆，则在 bean 实例化过程这些参数就会按照 bean 定义中的顺序被应用到构造器方法调用中。考虑下面这个类：

````java
package x.y;

public class ThingOne {
	public ThingOne(ThingTwo thingTwo, ThingThree thingThree){
		//...
	}
}
````

假设其中的````ThingTwo````和````ThingThree````类型并没有继承关系，而且不存在潜在的混淆。则下面的配置将会工作得很好，而且你不需要通过````<constructor-arg/>````元素显式指定构造器参数下标或者类型。

````xml
<beans>
  <bean id="beanOne" class="x.y.ThingOne">
    <constructor-arg ref="beanTwo"/>
    <constructor-arg ref="beanThree"/>
  </bean>
  
  <bean id="beanTwo" class="x.y.ThingTwo"/>
  
  <bean id="beanThree" class="x.y.ThingThree"/>
</beans>
````

当其它的 bean 被引用时，类型是明确的，因此可能匹配成功。当使用一个简单类型时，比如````<value>true</value>````，则 Spring 无法确定该值的类型，也就无法基于类型进行匹配。考虑下面的类：

````java
package examples;

public class ExampleBean {
  // Number of years to calculate the Ultimate Answer
  private int years;
  
  // The Answer to Life, the Universe, and Everything
  private String ultimateAnswer;
  
  public ExampleBean(int years, String ultimateAnswer) {
    this.years = years;
    this.ultimateAnswer = ultimateAnswer;
  }
}
````

*构造器参数类型匹配*

在上述场景中，如果你使用````type````属性显式指定构造器参数类型，容器就可以为简单类型使用使用类型匹配。如下面例子所示：

````xml
<bean id="exampleBean" class="examples.ExampleBean">
  <constructor-arg type="int" value="7500000"/>
  <constructor-arg type="java.lang.String" value="42"/>
</bean>
````

*构造器参数下标*

你可以通过````index````属性显式指定构造器参数的下标，如下面例子所示：

````xml
<bean id="exampleBean" class="examples.ExampleBean">
  <constructor-arg index="0" value="7500000"/>
  <constructor-arg index="1" value="42"/>
</bean>
````

除了解决多个简单类型值的参数解析混淆问题，指定参数下标还可以解决相同类型的参数混淆问题。

> 参数下标从 0 开始。

*构造器参数名称*

你还可以使用构造器参数名称来消除值混淆，如下面例子展示的：

````xml
<bean id="exampleBean" class="examples.ExampleBean">
  <constructor-arg name="years" value="7500000"/>
  <constructor-arg name="ultimateAnswer" value="42"/>
</bean>
````

注意，为了使得此特性开箱即用，你的代码必须在调试标识打开的情况下编译，这样 Spring 才能从构造器中发现参数名称。如果你不能或者不想在打开调试标识的情况下编译代码，你就可以使用 JDK 注解 [@ConstructorProperties](https://download.oracle.com/javase/6/docs/api/java/beans/ConstructorProperties.html) 来显式指定你的构造器参数名称。如下面例子所示：

````java
package examples;

public class ExampleBean {
  // Fields omitted
  
  @ConstructorProperties({"years", "ultimateAnswer"})
  public ExampleBean(int years, String ultimateAnswer) {
    this.years = years;
    this.ultimateAnswer = ultimateAnswer;
  }
}
````

**参数设定器依赖注入**

这种依赖注入方式的实现是通过容器在调用一个无参构造器方法或者一个无参的````static````工厂方法实例化你的 bean 之后调用你的 bean 中的参数设定器方法实现。

下面的例子展示了一个只能够单纯使用参数设定器注入方式的类。就是一个普通的 Java 类。它只是一个普通的类，没有通过类或者注解引入任何对容器特定接口的依赖。

````java
public class SimpleMovieLister {
  // the SimpleMovieLister has a dependency on the MovieFinder
  private MovieFinder movieFinder;
  
  // a setter method so that the Spring container can inject a MovieFinder
  public void setMovieFinder(MovieFinder movieFinder) {
    this.movieFinder = movieFinder;
  }
  
  // business logic that actually users the injected MovieFinder is omitted...
}
````

````ApplicationContext````支持构造器和参数设定器依赖注入，适用于它所管理的所有 beans。同时还支持一些依赖已经通过构造器注入方式进行注入之后再对其它依赖使用参数设定器注入。以````BeanDefinition````形式配置依赖，与````PropertyEditor````实例联合使用来将属性从一种格式转化成另一种格式。然而，大多数 Spring 用户并不直接使用这些类（编程方式配置），而是使用 XML 形式的 bean 配置和组件注解（也就是说，标注````@Component````、````@Controller````等等注解的类），或者在基于 Java 代码的````@Configuration````类中使用````@Bean````方法。这些源码接下来会内部转化为````BeanDefinition````实例并被用于加载整个 Spring IoC 容器实例。

> **构造器注入还是参数设定器注入**
>
> 尽管你可以混合使用构造器注入和参数设定器注入，但是相对比较好的做法是为强制依赖使用构造器注入，而为可选依赖使用属性设定器诸如活着配置方法注入。注意，在参数设定器方法上使用 [@Required](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-required-annotation) 注解可以使该属性变成强制依赖。
>
> Spring 团队通常提倡使用构造器依赖注入，就像它指导你实现作为不可变对象的应用组件时确保必需依赖非空。进一步地，构造器注入的组件永远会以完全初始化之后的状态被返回给客户端代码。顺便说一句，大量的构造器参数相关代码都不怎么漂亮，导致相关的类承载了过多的责任，因而应该被重构。
>
> 设定器注入应该仅仅用于可选依赖，这些依赖可以在类内部被分配有意义的默认值。否则，所有使用此类依赖的代码都必须处处进行依赖的非空校验。设定器注入的优势是设定器方法使得该依赖对象更易重新配置或者稍后重新注入。通过 [JMX MBeans](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/integration.html#jmx) 进行的管理就是设定器注入的强制使用场景。
>
> 依赖注入的风格因类而异。有时候，使用没有源码的第三方类时，你并没有选择的余地。比如，如果第三方类没有暴露任何设定器方法，就只能使用构造器注入风格。

**依赖解析过程**

容器按照如下顺序执行依赖解析：

* ````ApplicationContext````被创建和初始化，基于描述了所有 beans 的配置元数据。配置元数据可以通过 XML 、Java 代码或者注解的形式给出。
* 对每个 bean 来说，它的依赖表现为属性、构造器参数或者静态工厂方法参数（如果你使用它来取代正常的构造方法）。当 bean 实际被创建时，这些依赖将被提供给它。
* 每个属性或者构造器参数都是一个需要设定的值的实际定义，或者是容器中其它 bean 的引用。
* 每个属性或者构造器参数，只要是一个值，都被从它们各自特定格式转化为属性或者构造器参数的实力类型。默认地，Spring 可以将字符串形式的值转化为任何内建类型，比如````int````、````long````、````String````、````boolean````等等。

Spring 容器在它自身被创建时校验每个 bean 的配置。然而，bean 属性只是到 bean 实际被创建时才会被设置。单例模式并且默认被设置为预实例化的 beans 在容器创建时被创建。模式定义在 [Bean Scopes](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-scopes) 中。否则，bean 只有在它真正被请求到的时候才会被创建。一个 bean 的创建可能会导致一系列 beans 的创建，也就是该 bean 的依赖和它的依赖的依赖等等被创建和分配。注意，这些依赖解析过程中发生的不匹配稍后就可能发生，也就是说，在第一个受影响的 bean 创建时。

> **环形依赖**
>
> 如果你主要使用的是构造器依赖注入，则很可能产生无法解析的环形依赖情形。
>
> 比如，类型 A 在构造器注入时需要类型 B 的实例，而类型 B 在构造器依赖注入时又需要类型 A 的实例。如果你配置对应于这两个类的 beans 时相互注入对方，则 Spring IoC 容器将会在运行时检测到这个环形依赖，然后抛出一个````BeanCurrentlyInCreationException````。
>
> 一种可能的解决方案是将其中一些注入代码由构造器注入修改为参数设定器注入，或者完全使用参数设定器注入形式。换句话说，尽管不推荐，你仍然可以通过参数设定器注入方式配置出环形依赖。
>
> 不同于没有环形依赖的情形，bean A 和 bean B 之间存在环形依赖时，其中一个 bean 就必须在尚未完全初始化的时候被注入另一个 bean 中去（一个典型的先有鸡还是先有蛋问题）。

你可以简单地相信 Spring 会做正确的事。它再容器加载期间检测配置问题，比如引用不存在 beans 或者环形依赖等。Spring 尽可能晚地设定属性值和解析依赖，直到 bean 实际被创建时才执行操作。这就意味着目前已经加载的 Spring 容器有可能稍后出现异常，如果你请求的对象在创建过程中自身或者依赖出现问题。比如，bean 在属性缺失或者不可用时抛出异常。这种潜在的某些配置问题的推迟出现解释了为何````ApplicationContext````是通过默认的预实例化单例模式 bean 实现。在实际使用之前预先付出一些时间和内存空间来创建这些 beans，你将可以在````ApplicationContext````被创建时发现配置问题，而不是之后。你同样可以覆盖这种默认行为，实现单例 beans 的懒加载，而不是预实例化。

如果不存在环形依赖，当一个或者多个协作 beans 被注入依赖它们的 bean 时，每个协作 bean 都是已经被完整配置好了的。也就是说，如果 bean A 依赖 bean B ，容器在调用 bean A 中的设定器方法之前会提前完成 bean B 的配置。换句话说，一个 bean 实例化之后（如果它不是预实例化单例模式的），它的依赖都已经被设定，相关的生命周期方法都被调用（比如 [configured init method](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-initializingbean) 或者 [InitializingBean callback method](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-initializingbean) ）。

**依赖注入的例子**

接下来的例子基于 XML 配置元数据进行属性设定器依赖注入。相关的 bean 定义如下：

````xml
<bean id="exampleBean" class="examples.ExampleBean">
  <!-- setter injection using the nested ref element -->
  <property name="beanOne">
    <ref bean="anotherExampleBean"/>
  </property>
  
  <!-- setter injection using the neater ref attribute -->
  <property name="beanTwo" ref="yetAnotherBean"/>
  <property name="integerProperty" value="1"/>
</bean> 

<bean id="anotherExampleBean" class="examples.AnotherBean"/>
<bean id="yetAnotherBean" class="examples.YetAnotherBean"/>
````

下面例子展示了相应的````ExampleBean````类：

````java
public class ExampleBean {
  private AnotherBean beanOne;
  private YetAnotherBean beanTwo;
  private int i;
  
  public void setBeanOne(AnotherBean beanOne) {
    this.beanOne = beanOne;
  }
  
  public void setBeanTwo(YetAnotherBean beanTwo) {
    this.beanTwo = beanTwo;
  }
  
  public void setIntegerProperty(int i) {
    this.i = i;
  }
}
````

上面的例子中，声明的属性设定器与 XML 文件中的属性相对应。

下面的例子使用了构造器依赖注入：

````xml
<bean id="exampleBean" class="examples.ExampleBean">
  <!-- constructor injection using the nested ref element -->
  <constructor-arg>
    <ref bean="anotherExampleBean"/>
  </constructor-arg>
  
  <!-- constructor injection using the neater ref attribute -->
  <constructor-arg ref="yetAnotherBean"/>
  <constructor-arg type="int" value="1"/>
</bean> 

<bean id="anotherExampleBean" class="examples.AnotherBean"/>
<bean id="yetAnotherBean" class="examples.YetAnotherBean"/>
````

下面是对应的````ExampleBean````类：

````java
public class ExampleBean {
  private AnotherBean beanOne;
  private YetAnotherBean beanTwo;
  private int i;
  
  public ExampleBean(AnotherBean anotherBean, YetAnotherBean yetAnotherBean, int i) {
    this.beanOne = anotherBean;
    this.beanTwo = yetAnotherBean;
    this.i = i;
  }
}
````

bean 定义中的构造器参数被作为````ExampleBean````的构造方法参数。

现在考虑一下这个例子的变体，告诉 Spring 通过调用一个````static````工厂方法获取对象的实例：

````xml
<bean id="exampleBean" class="examples.ExampleBean" factory-method="createInstance">
  <constructor-arg ref="anotherExampleBean"/>
  <constructor-arg ref="yetAnotherBean"/>
  <constructor-arg value="1"/>
</bean>

<bean id="anotherExampleBean" class="examples.AnotherBean"/>
<bean id="yetAnotherBean" class="examples.YetAnotherBean"/>
````

下面是相应的````ExampleBean````类：

````java
public class ExampleBean {
  
  // a private constructor
  private ExampleBean(...) {
    ...
  }
  
  // a static factory method; the arguments to this method can be considered the dependencies of 
  // the bean that is returned, regardless of how those arguments are actually used.
  public static ExampleBean createInstance(AnotherBean anotherBean, YetAnotherBean yetAnotherBean, int i) {
    ExampleBean eb = new ExampleBean (...);
    // some other operations...
    return eb;
  }
}
````

````static````工厂方法的参数通过````<constructor-arg/>````元素给出，需要与实际使用的构造方法参数完全一致。该工厂方法返回的类的类型不一定是包含该````static````工厂方法的类，虽然例子中是同一个类。一个实例工厂方法（非静态的）也可以通过类似方式使用，具体细节我们不在这里讨论。

#### 1.4.2 依赖和配置细节

如前一章节所述，你可以将代码中定义的值和指向其它容器管理的 beans (所谓的协作者) 的引用定义为 bean 属性和构造器参数。Spring 的基于 XML 的配置元数据支持子元素类型包含````<property/>````和````<constructor-arg/>````元素来实现此效果。

**直接值（原始数据类型，字符串等等）**

````<property/>````元素的````value````属性给出了一个属性或者构造器参数的人类可读的字符串表达形式。Spring 的 [conversion service](https://docs.spring.io/spring/docs/5.1.4.RELEASE/spring-framework-reference/core.html#core-convert-ConversionService-API) 被用来将这些值由````String````类型转化成为属性或者参数的实际类型。下面例子展示了各种设定值的情况：

````xml
<bean id="myDataSource" class="org.apache.commons.dbcp.BasicDataSource" destroy-method="close">
  <!-- results in a setDriverClassName(String) call -->
  <property name="driverClassName" value="com.mysql.jdbc.Driver"/>
  <property name="url" value="jdbc:mysql://localhost:3306/mydb"/>
  <property name="username" value="root"/>
  <property name="password" value="masterkaoli"/>
</bean>
````

下面的例子使用了 [p-namespace](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/core.html#beans-p-namespace) 使得该 XML 文件更加简洁：

````xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:p="http://www.springframework.org/schema/p"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
    http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="myDataSource" class="org.apache.commons.dbcp.BasicDataSource"
        destroy-method="close"
        p:driverClassName="com.mysql.jdbc.Driver"
        p:url="jdbc:mysql://localhost:3306/mydb"
        p:username="root"
        p:password="masterkaoli"/>

</beans>
````

虽然这个 XML 更加简洁，但是拼写错误却只能在运行期才能发现，除非你的 IDE 可以帮助你自动完成属性名称。我们强烈推荐此类 IDE。

你也可以配置一个````java.util.Properties````实例，如下所示：

````xml
<bean id="mappings"
    class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">

    <!-- typed as a java.util.Properties -->
    <property name="properties">
        <value>
            jdbc.driver.className=com.mysql.jdbc.Driver
            jdbc.url=jdbc:mysql://localhost:3306/mydb
        </value>
    </property>
</bean>
````

Spring 容器将位于````<value/>````元素内部的文本转化进入````java.util.Properties````实例，通过使用 JavaBeans 的````PropertiesEditor````机制。这是一种不错的快捷方式，Spring 团队喜欢用这种内部````<value/>````元素替代````value````属性形式。

**````idref````元素**

此元素是一种防错的参数传递方式，将容器中的另外一个 bean 的````id````（一个字符串值，不是引用）传递给一个````<constructor-arg/>````元素或者````<property/>````元素。下面的例子展示了如何使用：

````xml
<bean id="theTargetBean" class="..."/>

<bean id="theClientBean" class="...">
    <property name="targetName">
        <idref bean="theTargetBean"/>
    </property>
</bean>
````

上面的 bean 定义片段在运行时等价于下面这个：

````xml
<bean id="theTargetBean" class="..." />

<bean id="client" class="...">
    <property name="targetName" value="theTargetBean"/>
</bean>
````

前一种形式更好，因为使用````idref````标签使得容器可以在部署过程中校验被引用的和命名的 bean 的实际存在性。后一种变体中，被传递给````client````bean 的````targetName````属性的值不会被校验。拼写错误只有当````client````bean 实际被实例化时才会被发现，这通常是致命的。如果该````client````bean 是一个  [prototype](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/core.html#beans-factory-scopes) bean ，则其中的拼写错误及其导致的异常结果可能在容器被部署之后很长时间才会被方法。

> ````idref````元素的````local````属性在 4.0 beans XSD 中已经不再支持，因为它已经不再通过一个规则的````bean````引用提供值。当升级到 4.0 规范时请修改你已经存在的````idref local````引用为````idref bean````。

共同之处（至少在 Spring 2.0 版本之前）在于，````<idref/>````元素在````ProxyFactoryBean````定义中的 [AOP interceptors](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/core.html#aop-pfb-1) 配置中携带值。当你指定拦截器名称时使用````<idref/>````元素可以防止你将拦截器 ID 拼写错误。

**其它 Beans 的引用**

````ref````元素是````<constructor-arg/>````或者````<property/>````定义元素中不可改变的元素。这里你可以将 bean 的特性属性值设定为指向容器管理的另外一个 bean（协作者）的引用。被引用的 bean 就成为引用它的 bean 的依赖，它将会在该属性设置之前被初始化。如果该协作者是单例模式 bean，则它可能已经被容器初始化过了。所有的引用最终都是指向另外一个对象。作用域和校验取决于你通过````bean````、````local````或者````parent````属性指定的其它对象的 ID 或者名称。

通过````<ref/>````标签的````bean````属性指定目标 bean 是最常用的形式，允许创建指向同一个容器或者父容器中的任何 bean 的引用，无论它是否在同一个 XML 文件中。````bean````属性的值可以等于目标 bean 的````id````属性，或者等于目标 bean 的````name````属性中的一个值。下面的例子展示了如何使用````ref````元素：

````xml
<ref bean="someBean"/>
````

通过````parent````属性指定目标 bean 创建了一个位于当前容器的父容器中的 bean 的引用。````parent````属性可以等于目标 bean 的````id````属性，或者等于目标 bean 的````name````属性中的一个值。该目标 bean 必须位于当前容器的一个父容器中。你应该使用这种 bean 引用变体，当你拥有层级结构的容器，而你希望将一个父容器中的一个 bean 以一个代理包装起来，该代理与它的父 bean 具有相同的名字。下面两个例子展示了````parent````属性的使用：

````xml
<!-- in the parent context -->
<bean id="accountService" class="com.something.SimpleAccountService">
    <!-- insert dependencies as required as here -->
</bean>
````

````xml
<!-- in the child (descendant) context -->
<bean id="accountService" <!-- bean name is the same as the parent bean -->
	class="org.springframework.aop.framework.ProxyFactoryBean">
	<property name="target">
        <ref parent="accountService"/> <!-- notice how we refer to the parent bean -->
	</property>
	<!-- insert other configuration and dependencies as required here -->
<bean/>
````

> ````ref````元素的````local````属性在 4.0 beans XSD 中已经不再支持，因为它已经不再通过一个规则的````bean````引用提供值。当升级到 4.0 规范时请修改你已经存在的````ref local````引用为````ref bean````。

**内部 Beans**

````<constructor-arg/>````或者````<property/>````元素中的````<bean/>````元素定义了一个内部 bean。如下例子所示：

````xml
<bean id="outer" class="...">
    <!-- instead of using a reference to a target bean, simply define the target bean inline -->
    <property name="target">
        <bean class="com.example.Person"> <!-- this is the inner bean -->
            <property name="name" value="Fiona Apple"/>
            <property name="age" value="25"/>
        </bean>
    </property>
</bean>
````

内部 bean 定义并不强制定义 ID 或者名称。如果指定，容器也不会将该值作为 id 使用。容器同样会忽略创建中的````scope````标识，因为内部 bean 永远是匿名的，而且永远是和外部类一起创建。不可能独立访问内部 bean，也不可能将它们注入出了包含它们的外部 bean 之外的协作 bean 中。

特殊情况下，可能会接收到来自定制化作用域的，比如，包含在一个单例 bean 内容的请求范围作用域的内部 bean。该内部 bean 实例的创建和它包含的 bean 绑定，但是析构回调使得它分享请求作用域生命周期。这不是常见的场景。内部 beans 典型地简单分享它们包含的 bean 的作用域。

**集合**

````<list/>````,````<set/>````,````<map/>````以及````<props/>````元素设置对应的 Java ````Collection````类型````List````,````set````,````Map````以及````Properties```` 属性或者参数。下面的例子展示了使用方法：

````xml
<bean id="moreComplexObject" class="example.ComplexObject">
    <!-- results in a setAdminEmails(java.util.Properties) call -->
    <property name="adminEmails">
        <props>
            <prop key="administrator">administrator@example.org</prop>
            <prop key="support">support@example.org</prop>
            <prop key="development">development@example.org</prop>
        </props>
    </property>
    <!-- results in a setSomeList(java.util.List) call -->
    <property name="someList">
        <list>
            <value>a list element followed by a reference</value>
            <ref bean="myDataSource"/>
        </list>
    </property>
    <!-- results in a setSomeMap(java.util.Map) call -->
    <property name="somMap">
        <map>
            <entry key="an entry" value="just some string"/>
            <entry key="a ref" value-ref="myDataSource"/>
        </map>
    </property>
    <!-- results in a setSomeSet(java.util.Set) call -->
    <property name="someSet">
        <set>
            <value>just some string</value>
            <ref bean="myDataSource"/>
        </set>
    </property>
</bean>
````

其中，````map````的````key````和````value````，以及````set````中的````value````，都可以是下面的任意元素：

````
bean | ref | idref | list | set | map | props | value | null
````

**集合合并**

Spring 容器同样支持合并集合。应用开发者能够定义一个父````<list/>````，````<map/>````，````<set/>````或者````<props/>````元素同时包含子````<list/>````，````<map/>````，````<set/>````或者````<props/>````元素继承并覆盖父集合中的值。也就是说，子集合的值就是父子集合合并之后的值。

本章节讨论父子 bean 合并机制。如果对父子 bean 不熟悉的读者请先了解 [relevant section](https://docs.spring.io/spring-framework/docs/current/spring-framework-reference/core.html#beans-child-bean-definitions)。

下面的例子展现了集合合并：

````xml
<beans>
    <bean id="parent" abstract="true" class="example.ComplexObject">
        <property name="adminEmails">
            <props>
                <prop key="administrator">administrator@example.com</prop>
                <prop key="support">support@example.com</prop>
            </props>
        </property>
    </bean>
    <bean id="child" parent="parent">
        <property name="adminEmails">
            <!-- the merge is specified on the child collection definition -->
            <props merge="true">
                <prop key="sales">sales@example.com</prop>
                <prop key="support">support@example.co.uk</prop>
            </props>
        </property>
    </bean>
</beans>
````

注意，子 bean 定义中````adminEmails````属性的````<props/>````元素的````merge=true````属性的使用。当子 bean 被容器解析并初始化时，结果实例中````adminEmails````属性集合包含父子 bean 中同名属性集合合并之后的结果。如下所示：

````xml
administrator=administrator@example.com
sales=sales@example.com
support=support@example.co.uk
````

应用于````<list/>````，````<map/>````和````<set/>````集合类型的合并行为是类似的。对于这种情形下的````<list/>````元素，语义类似于````List````集合类型。如果是有序列表，则父 bean 中的列表元素排在子 bean 中列表元素之前。在````Map````，````Set````和````Properties````集合类型的情形，元素没有顺序。因此，没有顺序语义作用于容器内部使用的集合类型的实现。

**集合合并的局限性**

你不能合并不同的集合类型，比如一个````Map````和一个````List````。如果你试图这么做，就会得到一个````Exception````抛出。子 bean 定义中必须指定````merge````属性。在父 bean 中指定该属性没有任何作用。

**强类型集合**

Java 5 引入范型之后，你可以使用强类型集合。也就是说，你可以声明一个````Collection````类型，它只能包含````String````类型的元素。如果你使用 Spring 依赖注入将一个强类型````Collection````注入进入一个 bean，就可以享受到 Spring 类型转换支持的优势，这样一来强类型集合的元素就会在被加入集合之前被自动转换为适合的类型。下面的类子说明了这个特性：

````java
public class SomeClass {
    private Map<String, Float> accounts;
    
    public void setAccounts(Map<String, Float> accounts) {
        this.accounts = accounts;
    }
}
````

````xml
<beans>
    <bean id="something" class="x.y.SomeClass">
        <property name="accounts">
            <map>
                <entry key="one" value="9.99"/>
                <entry key="two" value="2.75"/>
                <entry key="six" value="3.99"/>
            </map>
        </property>
    </bean>
</beans>
````

当````something```` bean 的````accounts````属性准备好注入时，反射机制就可以获取强类型````Map<String, Float>````的范型信息。因此，Spring 的类型转换基础设施认出变量值元素应该是````Float````类型，然后字符串值````9.99````，````2.75````和````3.99````就会被转换为实际的````Float````类型。

**Null 和空字符串值**

Spring 将属性的空参数当作空````Strings````。下面的基于 XML 的配置元数据片段为````email````属性设置空````String```值。

````xml
<bean class="ExampleBean">
  <property name="email" value=""/>
</bean>
````

这个例子等价于下面的 Java 代码：

````java
exampleBean.setEmail("");
````

````<null/>````元素持有````null````值。下面的例子展示了这种情况：

````xml
<bean class="ExampleBean">
    <property name="email">
        <null/>
    </property>
</bean>
````

等价于：

````java
exampleBean.setEmail(null);
````

**使用 p-namespace 的 XML 捷径**

p-namespace 使得你可以使用````bean````元素的属性（替代内部的````<property/>````元素）来描述你的协作 beans 的属性值，或者同时使用两者。

Spring 支持基于命名空间扩展的配置格式，基于 XML 规格定义。本章中讨论的````beans````配置格式定义在 XML 规格文档中。然而，p-namespace 并没有在 XSD 文件中定义，只是存在于 Spring 核心中。

下面的例子展示了两个 XML 片段，前一个是标准格式的 XML，后一个是使用了 p-namespace 形式。两者等价：

````xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean name="classic" class="com.example.ExampleBean">
        <property name="email" value="someone@somewhere.com"/>
    </bean>
    <bean name="p-namespce" class="com.example.ExampleBean"
          p:email="someone@somewhere.com"/>
</beans>
````

该例子展示了一个 bean 定义中的在 p-namespace 中的名为````email````的属性。这告诉 Spring 来包含一个属性声明。如前所述， p-namespce 不是一个规范定义，因此你可以设置参数名称为属性名称。

下面的例子包含另外两个 bean 定义，两个定义都包含其它 bean 的引用：

````xml
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xmlns:p="http://www.springframework.org/schema/p"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd">
    <bean name="john-classic" class="com.example.Person">
        <property name="name" value="John Doe"/>
        <property name="spouse" ref="jane"/>
    </bean>
    <bean name="john-modern"
          class="com.example.Person"
          p:name="John Doe"
          p:spouse-ref="jane"/>
    <bean name="jane" class="com.example.Person">
        <property name="name" value="John Doe"/>
    </bean>
</beans>
````

这个例子不仅包含一个 p-namespace 的属性值，还使用了一种特殊格式来声明属性引用。第一个 bean 定义使用````<property name="spouse" ref="jane"/>````来创建从 bean ````john````到 bean ````jane````的引用，第二个 bean 定义使用````p:spouse-ref="jane"````作为一个属性来做到相同的事情。这种情况下，````spouse````是属性名，````-ref````部分表示这不是一个直接的数值而是一个其它 bean 的引用。

> p-namespace 并不像标准的 XML 格式那么灵活。比如，声明引用属性的格式会与名称以````Ref````结尾的属性发生冲突，但是标准的 XML 格式就没有这种问题。推荐在开发团队中约定一种方式使用。

**使用 c-namespace 的 XML 捷径**

类似于上面一节介绍的 p-namespace ，这里的 c-namespace ，由 Spring 3.1 引入，允许为构造器参数配置內联属性而不需要包含````constructor-arg````元素。

下面的例子展示了使用 c-namespace 实现基于构造器的依赖注入：

````xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:c="http://www.springframework.org/schema/c"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="beanTwo" class="x.y.ThingTwo"/>
    <bean id="beanThree" class="x.y.ThingThree"/>

    <!-- traditional declaration with optional argument names -->
    <bean id="beanOne" class="x.y.ThingOne">
        <constructor-arg name="thingTwo" ref="beanTwo"/>
        <constructor-arg name="thingThree" ref="beanThree"/>
        <constructor-arg name="email" value="something@somewhere.com"/>
    </bean>

    <!-- c-namespace declaration with argument names -->
    <bean id="beanOne" class="x.y.ThingOne" c:thingTwo-ref="beanTwo"
        c:thingThree-ref="beanThree" c:email="something@somewhere.com"/>

</beans>
````

````c:````命名空间使用与````p:````命名空间相同的约定（用````-ref````表示 bean 引用）来通过名称设定构造器参数。类似的，它需要在 XML 文件中声明，尽管它并没有在 XSD 规范中定义（它只存在于 Spring 核心中）。

比较罕见的情况下，构造器的参数名不可用（通常是字节码编译时没有附带调试信息），你可以退化使用参数索引，如下：

````xml
<!-- c-namespace index declaration -->
<bean id="beanOne" class="x.y.ThingOne" c:_0-ref="beanTwo" c:_1-ref="beanThree"
    c:_2="something@somewhere.com"/>
````

> 由于 XML 语法的要求，参数索引记号必须以下划线开头，同时 XML 属性名也不能以数字开头（即使某些 IDE 允许）。相应的下标记号同时也适用于````<constructor-arg>````元素，但是并不常用，因为字面的声明顺序通常就是足够的。

在实践中，构造器解析机制在匹配参数时是相当有效的，因此除非你真的需要，我们推荐在你的配置文件中全部使用名称记号。

**复合属性名称**

你可以使用符合或者嵌套属性名称来设置 bean 属性，只要路径上的所有组件期望最终的属性名称不是````null````。参考下面的 bean 定义：

````xml
<bean id="something" class="things.ThingOne">
    <property name="fred.bob.sammy" value="123"/>
</bean>
````

````something````bean 拥有一个````fred````属性，该属性包含一个````bob````属性，它又包含一个````sammy````属性，而最终的````sammy````属性值为设定为````123````。为了保证这个配置生效，````something````的````fred````属性，以及````fred````的````bob````属性都必须不为````null````，在 bean 被构造之后。否者，将抛出一个````NullPointException````。

#### 1.4.3 使用````depends-on````

如果一个 bean 是其它 bean 的依赖，通常意味着该 bean 被设置为其它 bean 的属性。典型的做法是在基于 XML 的配置元数据中使用````<ref/>````元素实现。然而，有时候 beans 之间的依赖关系并不直接。例如类中需要被触发的静态初始化器，诸如数据库驱动注册等。````depends-on````属性能够显式强制一个或者多个 beans 在使用它的所有 bean 被初始化之前被初始化。下面的例子展示了````depends-on````属性如何表达对单独一个 bean 的依赖：

````xml
<bean id="beanOne" class="ExampleBean" depends-on="manager"/>
<bean id="manager" class="ManagerBean"/>
````

为了表达对多个 beans 的依赖，可以为````depends-on````属性设置一个 bean 名称的列表（逗号、空格和分号都是合法的分隔符）：

````xml
<bean id="beanOne" class="ExampleBean" depends-on="manager,accountDao">
    <property name="manager" ref="manager"/>
</bean>
<bean id="manager" class="ManagerBean"/>
<bean id="accountDao" class="x.y.jdbc.JdbcAccountDao"/>
````

> ````depends-on````属性能够指定初始化阶段的依赖，以及单例 beans 的相应的析构阶段的依赖。定义与给定 bean 的````depends-on````关系的依赖 bean 会被首先销毁，先于给定 bean 的销毁。因此，````depends-on````也可以同时控制关闭顺序。

#### 1.4.4 懒初始化 Beans

默认情况下，````ApplicationContext````实现会作为初始化过程的一部分尽快创建和配置单例模式的 beans 。通常，这种预实例化是我们期待的。因为配置或者周边环境中的错误会立即被发现，而不是几个小时或者几天之后。如果不希望这种行为，你可以通过将 bean 定义标记为懒初始化的来阻止单例模式 bean 的这种预实例化。一个懒初始化的 bean 告诉 IoC 容器在它首次被请求时再创建一个 bean 实例，而不是在启动时。

在 XML 文件中，这种行为通过````<bean/>````元素上的````lazy-init````属性来控制，如下面例子所示：

````xml
<bean id="lazy" class="com.something.ExpensiveToCreateBean" lazy-init="ture"/>
<bean name="not.lazy" class="com.something.AnotherBean"/>
````

当上面的配置被````ApplicationContext````消费，其中的````lazy````  bean 不会在````ApplicationContext````启动时被预实例化，而````not.lazy```` bean 将在此时被预实例化。

不过，当一个懒初始化的 bean 是一个非懒实例化单例模式 bean 的依赖时，````ApplicationContext````就会在启动过程中创建该懒初始化 bean，因为它必须满足该单例模式 bean 的依赖需求。然后该懒初始化 bean 被注入进非懒初始化 bean 中。

你也可以在容器层面通过````<bean/>````元素上的````default-lazy-init````属性控制懒初始化，下面的例子说明了这种做法：

`````xml
<bean default-lazy-init="true">
	<!-- no beans will be pre-instantiated... -->
</bean>
`````

#### 1.4.5 自动装配协作者

Spring 容器能够自动装配相互协作的 bean 之间的关系。你可以让 Spring 为你的 bean 自动处理协作者（其它 beans），通过检查````ApplicationContext````的内容。自动装配具有以下优点：

* 自动装配能够显著减少需要指定的属性或者构造器参数。（其它机制，比如 bean 模板等同样有相同的作用）
* 自动装配能够随着你的 bean 的进化更新配置。比如，如果你需要为一个类增加一个依赖，该依赖能过够被自动满足而不需要你手动修改配置。因此，自动装配在开发阶段会非常有用，当然，当项目代码逐渐趋于稳定时也可以切换到显式装配。

当使用基于 XML 的配置元数据时，你可以通过````<bean/>````元素的````autowire````属性指定 bean 定义的自动装配模式。自动装配功能有 4 种模式。你可以为每个 bean 指定自动装配并可以选择需要装配哪些 beans 。下表展示了自动装配的 4 种模式：

| 模式          | 说明                                       |
| ----------- | ---------------------------------------- |
| no          | （默认的）不自动装配。Bean 引用必须通过````ref````元素定义。不推荐在大型项目部署中修改默认设定，因为显式指定协作者提供了更好的可控性和清晰度。某种程度上，它记录了系统的结构。 |
| byName      | 根据属性名自动装配。Spring 通过属性名查找需要被装配的 bean。比如，如果一个 bean 定义被设定为按照名称自动装配，同时它包含一个````master````属性（也就是说，它有一个````setMaster()````方法），Spring 就会查找名为````master````的 bean 定义并使用它设置该属性。 |
| byType      | 使得一个属性被自动装配，如果容器中恰好只有一个该属性类型的 bean 存在。如果存在多个该类型的 bean ，则会抛出致命异常，表示这种情况下你不能对该 bean 使用````byType````自动装配模式。如果不存在该类型的 bean ，则什么都不会发生（该属性不会被设置）。 |
| constructor | 类似于````byType````，不过是应用于构造器参数的。如果容器中不存在符合构造器参数类型的 bean，则会发生致命错误。 |

使用````byType````或者````constructor````自动装配模式时，你可以装配数组或者类型化的集合。这种情况下，容器内匹配到给定类型的所有自动装配候选者都被提供来满足依赖需求。你可以自动装配强类型````Map````实例，如果期待的键类型时````String````。被自动装配的````Map````实例的值由所有匹配期待类型的 bean 实例组成，同时，该````Map````实例的键包含相应的 bean 名称。

**自动装配的不足和局限性**

在整个项目中都一致地使用自动装配时它可以工作地很好。但是如果同时使用其它装配方式，只为一两个 bean 使用自动装配，开发者可能会很迷惑。自动装配的局限性如下：

* ````property````和````constructor-arg````中的显式依赖设定永远覆盖自动装配。你不能自动装配原始类型的简单属性，````String````和````Classes````（以及这些简单属性的数组）。这是设计上的局限性。
* 自动装配不如显式装配精确。尽管在上面的表中，Spring 会很小心地在模棱两可的情况下尽力避免猜测可能导致的预料之外的结果。你的 Spring 管理的对象之间的关系仍然会显得不那么清楚。
* 装配信息可能对那些从 Spring 容器生成文档的工具不可用。
* 容器中可能有多个 bean 定义同时匹配到由需要自动装配的````setter````方法或者构造器参数指定的类型。对数组、集合或者````Map````实例来说，这不是问题。然而，对于那些期待单个值的依赖，这种模棱两可的情况无法解决。如果可用的 bean 定义不唯一，就会抛出异常。

在上面最后一种场景下，你有下面几种选择：

* 使用显式装配阻止自动装配

* 通过设定该 bean 定义的````autowire-candidate````属性为````false````来阻止它的自动装配，在下一节中介绍。

* 指定一个 bean 定义作为首选候选者，通过设定该````<bean/>````元素的````primary````属性为````true````。

* 通过使用基于注解的配置实现更细粒度的控制，细节在 [基于注解的容器配置](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-annotation-config)中描述。


**从自动装配中排除 Bean**

在每个 bean 基础上，你可以从自动装配中排除单个的 bean。在 Spring 的 XML 格式中，设定该````<bean/>````元素的````autowire-candidate````属性为````false````。容器将把该 bean 设定为自动装配基础设施（包括注解形式的配置，比如````@Autowired````）不可用状态。

> ````autowire-candidate````属性被设计为仅仅影响基于类型的自动装配。它不影响通过名称的显式引用，即使指定的 bean 没有被标记为自动装配候选者，显式引用仍然会生效。因此，只要名称是匹配的，通过名称进行的自动装配无论如何都会执行。

你也可以使用基于 bean 名称模式匹配的方式对自动装配候选者进行限制。顶级的````<bean/>````元素在它的````default-autowire-candidates````属性中接受一个或者多个模式。比如，为了限制自动装配候选者的状态为 bean 名称以````Repository````结尾，就设定值为````*Repository````。为了提供多个模式，将它们定义在一个用逗号分隔的列表中。bean 定义的````autowire-candidate````属性的字面值````true````或者````false````永远具有优先权。对这些 beans，模式匹配规则不生效。

这些技术对那些你永远不希望被自动装配机制注入其它 beans 中的 beans 是有用的。不过这并不意味着被排除的 bean 自身不能被配置成为使用自动装配的。相反，只是说它自己不会被自动装配机制作为其它 beans 的装配候选者。

#### 1.4.6 方法注入

在大多数应用场景中，容器中的大部分 beans 都是单例模式的。当一个单例模式的 bean 需要与其它单例模式的 bean 协作，或者一个非单例模式的 bean 需要与其它非单例模式的 bean 协作时，典型的做法是将其中一个 bean 定义为其它 bean 的属性。当 bean 的生命周期不同时可能会有问题。假设单例模式的 bean A 需要使用非单例模式 bean B，可能在 A 中的每个方法的调用中都会用到。容器创建单例模式的 bean A 仅一次，因此只有一次机会设置属性。当需要时容器不可能将每个新的 bean B 实例连同 bean A 提供出来。

一种解决方案是放弃某些控制反转。你可以通过实现````ApplicationContextAware````接口来讲 bean A 标记为容器上下文敏感的，同时，通过使得每次 bean A 需要它时向容器调用````getBean("B")````获取（一个典型的新的）bean B 的实例。下面的例子展示了这种方法：

````java
// a class that uses a stateful Command-style class to perform some processing
package fiona.apple;

// Spring-API imports
import org.springframework.beans.BeansException;
import org.springframework.context.ApplicationContext;
import org.springframework.context.ApplicationContextAware;

public class CommandManager implements ApplicationContextAware {
    
    private ApplicationContext applicationContext;
    
    public Object process(Map commandState) {
        // grab a new instance of the appropriate Command
        Command command = createCommand();
        // set the state on the (hopefully brand new) Command instance
        command.setState(commandState);
        return command.execute();
    }
    
    protected Command createCommand() {
        // notice the Spring API dependency
        return this.applicationContext.getBean("command", Command.class);
    }
    
    public void setApplicationContext(
        ApplicationContext applicationContext) throws BeansException {
        this.applicationContext = applicationContext;
    }
}
````

上面这种做法其实是不可取的，因为业务代码是框架敏感、而且与框架耦合在一起。方法注入，Spring IoC 容器的一个高级特性，允许你很干净地处理这种情况。

> 你可以在[这篇博客](https://spring.io/blog/2004/08/06/method-injection/)中看到方法注入的更多动机。

**查找方法注入**

查找方法注入是容器的一种能力，可以覆盖容器管理的 beans 中的方法并返回容器中其它命名的 bean 的查找结果。这种查找通常涉及到一个原型 bean，就像在前一节中描述的场景下。Spring 框架实现此方法注入通过使用产生自 CGLIB 库的字节码，来动态产生覆盖该方法的一个子类。

> * 为了这种动态子类型能够工作，被 Spring 容器生成子类的类不能是````final````的，同时被覆盖的方法也不能是````final````的。
> * 对包含抽象方法的类进行单元测试将需要你写一个该类的子类并提供一个该抽象方法的实现“桩”。
> * 具体方法对组件扫描也是必须的，不过要求具体类被加载。
> * 更关键的限制是，查找方法不能与工厂方法共同工作，特别是配置类中的````@Bean````标注的方法。因为，这种情况下容器不负责创建实例，因而就不能在运行时凭空创建子类。

在前面的代码片段中````CommandManager````类出现的情况下，Spring 容器动态覆盖````createCommand()````方法的实现。````CommandManager````类没有任何 Spring 依赖，就像下面这个改写的例子：

````java
package fiona.apple

// no more Spring importes!

public abstract class CommandManager{
	public Object process(Object commandState){
		// grab a new instance of the appropriate Command interface
		Command command = createCommand();
		// set the state on the (hopefully brand new) Command instance
		command.setState(commandState);
		return command.execute();
	}
	
	// okay... but where is the implementation of this method?
	protected abstract Command createCommand();
}
````

在包含该需要被注入的方法的客户端类（例子中是````CommandManager````）中，需要注入的方法需要如下形式的方法签名：

````
<public | protected> [abstract] <return-type> theMethodName(no-arguments);
````

如果方法是````abstract````的，则动态生成的子类实现该方法。否则，动态生成的子类覆盖定义在初始类中的具体方法。考虑下面的例子：

````xml
<!-- a stateful bean deployed as a prototype (non-singleton) -->
<bean id="myCommand" class="fiona.apple.AsyncCommand" scope="prototype">
    <!-- inject dependencies here as required -->
</bean>

<!-- commandProcessor uses statefulCommandHelper -->
<bean id="commandManager" class="fiona.apple.CommandManager">
    <lookup-method name="createCommand" bean="myCommand"/>
</bean>
````

名为````commandManager````的 bean 调用它自己的````createCommand()````方法，每当它需要一个新的````myCommand```` bean 实例。你必须谨慎部署该````myCommand```` bean 作为一个原型，如果确实是需要的。如果它是单例模式的 bean，则每次调用该方法都会返回同一个````myCommand```` bean。

另外，在基于注解的组件模型中，你可以通过````@Lookup````注解声明查找方法，如下例子所示：

````java 
public abstract class CommandManager {

    public Object process(Object commandState) {
        Command command = createCommand();
        command.setState(commandState);
        return command.execute();
    }

    @Lookup("myCommand")
    protected abstract Command createCommand();
}
````

或者，更符合语言习惯的，你可以依赖查找方法声明的返回类型来解析目标 bean ，如下例子所示：

````java
public abstract class CommandManager {

    public Object process(Object commandState) {
        MyCommand command = createCommand();
        command.setState(commandState);
        return command.execute();
    }

    @Lookup
    protected abstract MyCommand createCommand();
}
````

注意：你应该声明这种注解的查找方法的同时提供具体的桩实现，以使得它们兼容于 Spring 容器的组件默认扫描规则，该规则默认会忽略抽象类。这个限制并不会作用于显式注册或者显式引入的 bean 类。

>另一种访问不同作用域的目标 bean 的方法是````ObjectFactory````/````Provider````注入点。参考 [Scoped Beans as Dependencies](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-other-injection).
>
>你会发现````ServiceLoatorFactoryBean````（在````org.springframework.beans.factory.config````包下）非常有用。

**任意方法替换**

相对于查找方法注入，任意方法替换是另外一种稍微弱一些的方法注入方法。这是一种可以用另外的方法实现替换容器管理的 bean 中的任意方法的能力。如果你不需要这个功能特性，就可以安全地跳过这一节。

在基于 XML 的配置元数据中，你可以使用````replaced-method````元素来替换已部署的 bean 中一个存在的方法实现。考虑下面的类，其中的````computeValue````方法是我们想要覆盖的：

````java
public class MyValueCalculator {

    public String computeValue(String input) {
        // some real code...
    }

    // some other methods...
}
````

实现了````org.springframework.beans.factory.support.MethodReplacer````接口的类提供新的方法定义，如下例所示：

````java
/**
 * meant to be used to override the existing computeValue(String)
 * implementation in MyValueCalculator
 */
public class ReplacementComputeValue implements MethodReplacer {

    public Object reimplement(Object o, Method m, Object[] args) throws Throwable {
        // get the input value, work with it, and return a computed result
        String input = (String) args[0];
        ...
        return ...;
    }
}
````

部署初始类以及指定方法覆盖的 bean 定义文件类似于下面的例子：

````xml
<bean id="myValueCalculator" class="x.y.z.MyValueCalculator">
    <!-- arbitrary method replacement -->
    <replaced-method name="computeValue" replacer="replacementComputeValue">
        <arg-type>String</arg-type>
    </replaced-method>
</bean>

<bean id="replacementComputeValue" class="a.b.c.ReplacementComputeValue"/>
````

你可以在````<replaced-method>````元素中使用若干````<arg-type>````元素来表示将被覆盖的方法的方法签名。参数的签名只有当方法被重载同时类中存在多个变体时才是必要的。方便起见，参数的类型字符串可以是对应类型全限定名的子字符串。比如，下列字符串都可以匹配到````java.lang.String````：

````
java.lang.String
String
Str
````

由于参数个数通常已经足够用来区分每个可能的方法选择，这种类型字符串的缩写可以节省大量的键入。

### 1.5 Bean 作用域

当你创建一个 bean 定义，你创建了一个创建由 bean 定义定义的类的实际实例的配方。bean 定义是一种配方，这个认识很重要，因为这就意味着基于一个类型，你可以从一个配方创建出许多对象实例。

你不仅可以控制将要被插入由特定 bean 定义创建的对象中的各种依赖和配置值，还可以控制由特定 bean 定义创建出来的对象的作用域。这种方式很强大，而且很灵活，因为你可以选择通过配置文件来控制你创建的对象的作用域，而不需要在 Java 类层面来实现这种控制。Beans 能够被定义以用于部署在不同的作用域中。Spring 框架支持 6 种作用域，其中 4 种只有当你使用 web-aware 的````ApplicationContext````时才是可用的。你也可以创建 [a custom scope.](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-custom)。

下表描述了支持的作用域：

| 作用域                                      | 描述                                       |
| ---------------------------------------- | ---------------------------------------- |
| [singleton](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-singleton) | （默认的）为每个 Spring IoC 容器，一个 bean 定义只会创建一个对象实例 |
| [prototype](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-prototype) | 一个 bean 定义可以创建任意数量的对象实例                  |
| [request](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-request) | 一个 bean 定义的作用域局限在一个 HTTP 请求范围内。也就是说，每个 HTTP 请求都用户它自己的 bean 实例，由单个的 bean 定义创建出来。仅仅在 web-aware 的 Spring ````ApplicationContext````的上下文中可用。 |
| [session](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-session) | 一个 bean 定义的作用域局限在一个 HTTP 会话范围内。仅仅在 web-aware 的 Spring ````ApplicationContext````的上下文中可用。 |
| [application](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-application) | 一个 bean 定义的作用域局限在一个````ServletContext````范围内。仅仅在 web-aware 的 Spring ````ApplicationContext````的上下文中可用。 |
| [websocket](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#websocket-stomp-websocket-scope) | 一个 bean 定义的作用域局限在一个````WebSocket````范围内。仅仅在 web-aware 的 Spring ````ApplicationContext````的上下文中可用。 |

> 在 Spring 3.0 中，线程范围的作用域是可用的，不过并没有作为默认作用域，参考[`SimpleThreadScope`](https://docs.spring.io/spring-framework/docs/5.1.5.RELEASE/javadoc-api/org/springframework/context/support/SimpleThreadScope.html)。在 Spring 4.2 中，事务范围的作用域同样可用，参考 [`SimpleTransactionScope`](https://docs.spring.io/spring-framework/docs/5.1.5.RELEASE/javadoc-api/org/springframework/transaction/support/SimpleTransactionScope.html)。关于创建以及注册这些或者其它客户化作用域的细节可参考 [Using a Custom Scope](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-custom-using)。

#### 1.5.1 单例作用域

单例 bean 只有一个共享的实例被管理，所有对该 beans 的请求，携带 ID 或者 IDs 匹配到该 bean 定义，将导致唯一的这个特定的 bean 实例被 Spring 容器返回。

换句话说，当你定义一个 bean 定义，同时它的作用域是单例的，Spring IoC 容器仅仅创建唯一的由该 bean 定义所定义的对象的实例。这个唯一的实例被存储在这个单例 bean 的缓存中，所有后续的对该 bean 的请求和引用都将返回这个缓存的对象。下面的图展示了单例作用域的原理：

![The Singleton Scope](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/spring/image-20190320155028.png)

Spring 中的单例 bean 的概念与 GoF 设计模式中定义的单例模式的概念是不同的。GoF 中的单例模式是硬编码对象的作用域，保证每个类加载器值创建唯一的一个特定类型的实例。Spring 中的单例的做好的解释是每个容器和每个 bean 。这就意味着，如果你在一个 Spring 容器中定义一个特定类型的 bean，该容器将只会创建唯一的一个该 bean 定义的类型的对象实例。单例作用域是 Spring 中默认的作用域。为了定义一个单例 bean 在 XML 中，你可以如下面的例子这样定义：

````xml
<bean id="accountService" class="com.something.DefaultAccountService"/>

<!-- the following is equivalent, though redundant (singleton scope is the default) -->
<bean id="accountService" class="com.something.DefaultAccountService" scope="singleton"/>
````

#### 1.5.2 原型作用域

bean 部署的非单例的原型作用域将会导致每次请求都会有一个新的 bean 实例被创建。也就是说，该 bean 被注入另外的 bean 或者你通过调用容器上的````getBean()````方法发起的请求。作为规则，你应该为有状态的 beans 使用原型作用域，而为无状态的 beans 使用单例作用域。

下图展示了 Spring 的原型作用域：

![The Prototype Scope](https://raw.githubusercontent.com/shenliang-2016/article/master/translate/assets/spring/image-20190320160829.png)

(数据访问对象(DAO)通常不会被配置为原型，因为一个典型的 DAO 并不持有任何会话状态。我们可以方便地重用单例图示)

下面的例子在 XML 中定义了一个原型 bean ：

````xml
<bean id="accountService" class="com.something.DefaultAccountService" scope="prototype"/>
````

相比于其它作用域，Spring 并不管理原型 bean 的完整生命周期。容器实例化、配置并且组装原型对象然后将其交与客户端，而没有任何对原型实例的进一步记录。因此，尽管初始化生命周期回调方法被在所有对象上调用，而无关乎作用域，在原型场景下，配置的析构生命周期回调不会被调用。客户端代码必须清理原型作用域的对象，并释放这些原型 bean 持有的昂贵资源。为了获取 Spring 容器以释放原型作用域 beans 持有的资源，尝试使用客户化的 [bean post-processor](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-extension-bpp), 它持有需要被清理的 beans 的引用。

从某个层面来看，对原型 beans 来说，Spring 容器的角色基本上就是作为 Java 中的````new````操作符的替身。这个时间点之后的所有生命周期管理都必须由客户端管理。（有关 Spring 容器中的 bean 的生命周期管理的更多细节参见 [Lifecycle Callbacks](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle)）

#### 1.5.3 具有原型 Bean 依赖的单例 Beans

当你使用依赖原型 beans 的单例 beans 时，注意依赖解析是发生在实例化阶段。因此，如果你将一个原型 bean 依赖注入一个单例 bean 中，一个新的原型 bean 被实例化然后被依赖注入进入该单例 bean 。该原型实例就是仅仅提供给该单例 bean 的实例。

不过，假设你希望在运行时该单例 bean 反复获取一个新的原型 bean 的实例。你就不能将一个原型 bean 依赖注入你的单例 bean ，因为该注入只会发生一次，当 Spring 容器实例化给单例 bean 并解析和注入它的依赖。如果你需要在运行时得到原型 bean 的新的实例多次，参考  [Method Injection](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-method-injection)。

#### 1.5.4 请求，会话，应用，以及 WebSocket 作用域

````request````，````session````，````application````，以及````WebSocket````作用域只是当你使用 web-aware 的 Spring ````ApplicationContext````实现（比如````XmlWebApplicationContext````）时才是可用的。如果你在标准的 Spring IoC 容器中使用这些作用域，比如````ClassPathXmlApplicationContext````，一个抱怨未知的 bean 作用域的````IllegalStateException````异常将会被抛出。

**初始 Web 配置**

为了支持 beans 的````request````，````session````，````application````，以及````WebSocket````级别的作用域（web-scoped beans），在定义你的 beans 之前少量的初始配置是必需的。（这些初始设置对标准作用域````singleton````和````prototype````不是必需的）

如何实现这种初始配置取决于你的特定 Servlet 环境。

如果你在 Spring Web MVC 环境下访问有作用域的 beans ，实际上，在一个由 Spring ````DispatcherServlet````处理的请求中，不需要任何特殊的设置。````DispatcherServlet````已经暴露了所有相关的状态。

如果你使用的是 Servlet 2.5 web 容器，请求是在 Spring ````DispatcherServlet````之外处理（比如，当使用 JSF 或者 Struts 时），你需要注册````org.springframework.web.context.request.RequestContextListener````和````ServletRequestListener````。对 Servlet 3.0+ 版本的容器，这些可以使用````WebApplicationInitializer````接口通过编程方式实现。或者，对老版本的容器，在你的应用的部署描述器文件````web.xml````中添加如下声明：

````xml
<web-app>
  ...
  <listener>
    <listener-class>
      org.springframework.web.context.request.RequestContextListner
    </listener-class>
  </listener>
  ...
</web-app>
````

或者，如果你的监听器配置有问题，考虑使用 Spring 的````RequestConextFilter````。过滤器映射取决于周边的 web 应用配置，因此你必须对它进行相应修改。下面的例子展示了该部署描述器文件的过滤器声明部分：

````xml
<web-app>
  ...
  <filter>
    <filter-name>requestContextFilter</filter-name>
    <filter-class>org.springframework.web.filter.RequestContextFilter</filter-class>
  </filter>
  <filter-mapping>
    <filter-name>requestContextFilter</filter-name>
    <url-pattern>/*</url-pattern>
  </filter-mapping>
  ...
</web-app>
````

````DispactherServlet````，````RequestContextListener````以及````RequestContextFilter````做的事情完全相同，即将 HTTP 请求对象绑定到为该请求服务的````Thread````。这就使得请求作用域和会话作用域的 beans 在调用链的下游还是可用的。

**请求作用域**

考虑下面的 XML 配置中的 bean 定义：

````xml
<bean id="loginAction" class="com.something.LoginAction" scope="request"/>
````

Spring 容器通过使用````loginAction````  bean 定义为每个 HTTP 请求创建````LoginAction```` bean 的新的实例。也就是说，````loginAction```` bean 的作用域是 HTTP 请求级别。你可以任意修改创建出来的实例的内部状态，因为由同一个 bean 定义创建出来的的其它实例并不会看到这些状态变化。它们都专属于单独的请求。当该请求处理完成，对应的请求作用域的 bean 实例就会被清理。

当使用注解驱动的组件或者 Java 配置时，````@RequestScope````注解可以被用于标注组件为````request````作用域。下面例子展示了这种用法：

````java
@RequestScope
@Component
public class LoginAction {
  // ...
}
````

**会话作用域**

考虑下面的 XML 配置中的 bean 定义：

````xml
<bean id="userPreferences" class="com.something.UserPreferences" scope="session"/>
````

Spring 容器通过使用````userPreferences````  bean 定义为每个 HTTP 会话的生命周期创建一个新的````UserPreferences````实例。换句话说，````userPreferences```` bean 的作用域就是 HTTP ````Session````级别。如同请求作用域的 beans ，你也可以任意修改这些 beans 的内部状态，而其它使用从同一个````userPreferences```` bean 定义创建的实例的 HTTP ````Session````实例无法看到这种状态变化，因为它们都特定地属于每个 HTTP ````Session````。当 HTTP ````Session```` 被彻底废弃之后，作用域是该 HTTP ````Session```` 的 bean 实例也会被废弃。

当使用注解驱动的组件或者 Java 配置时，````@SessionScope````注解可以被用于标注组件为````session````作用域。下面例子展示了这种用法：

````java
@SessionScope
@Component
public class UserPreferences {
  // ...
}
````

**应用作用域**

考虑如下 XML 配置用来定义 bean ：

````xml
<bean id="appPreferences" class="com.something.AppPreferences" scope="application"/>
````

Spring 容器通过对整个 Web 应用程序使用 ````appPreferences```` bean 定义一次来创建 ````AppPreferences```` bean的新实例。 也就是说，````appPreferences```` bean 的作用域是 ````ServletContext```` 级别，并存储为常规的 ````ServletContext```` 属性。 这有点类似于 Spring 单例 bean，但在两个重要方面有所不同：它是每个 ````ServletContext```` 的单例，而不是每个 Spring 的 'ApplicationContext'（在任何给定的 Web 应用程序中可能有几个），它实际上是暴露的，因此 作为 ````ServletContext````属性可见。

当使用注解驱动的组件或者 Java 配置类时，你可以使用 ````@ApplicationScope```` 注解来将一个组件配置为 ````application```` 作用域。下面的例子展示了如何做到：

````java
@ApplicationScope
@Component
public class AppPreferences {
  // ...
}
````

**作为依赖的 Beans 的作用域**

Spring IoC 容器不仅管理你的对象 (beans) 实例，同时还管理它们的协作者 (或者依赖) 之间的联系。如果你希望注射一个 HTTP 请求作用域 bean 进入另一个更长生存时间作用域的 bean 时，你可以选择注入一个 AOP 代理类来替代该具有作用域的 bean 。也就是说，你需要注入一个代理对象来暴露与该 bean 相同的公共接口，而同时又能够从相应的作用域（比如一个 HTTP 请求）中获取真实的目标对象，并将方法调用委托给真实目标对象。

> 你也可以在 ````singleton```` 作用域的 beans 中间使用 ````<aop:scoped-proxy/>```` ，以及 beans 引用，然后通过一个可以序列化的中间代理，因此可以在反序列化时重新获取目标单例 bean 。
>
> 当为一个作用域为 ````prototype```` 的 bean 声明 ````<aop:scoped-proxy/>```` 时，每个到达该共享代理的请求将导致一个新的目标实例的创建，然后该请求会被转发到其上。
>
> 同时，具有作用域的代理并不只有这一种生命周期安全的方式来访问具有更短作用域的 beans 。你也可以声明你的注入点 (也就是说，构造器方法或者设置器参数或者自动绑定字段) 为 ````ObjectFactory<MyTargetBean>````，允许一个 ````getObject()```` 调用来按照每次请求按需获取当前实例—而不是单独持有并存储该实例。
>
> 作为一个扩展变体，你可以声明 ````ObjectProvider<MyTargetBean>```` ，它提供了几个额外的访问变体，包括 ````getIfAvailable```` 和 ````getIfUnique````。
>
> JSR-330 变体被称为 ````Provider```` ，与一个 ````Provider<MyTargetBean>```` 声明和一个相应的为每个查询请求的 ````get()```` 调用共同使用。参考 [JSR-330](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/core.html#beans-standard-annotations)。

下面例子中的配置只有一行，不过理解它的原理和作用同样重要：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop
        https://www.springframework.org/schema/aop/spring-aop.xsd">

    <!-- an HTTP Session-scoped bean exposed as a proxy -->
    <bean id="userPreferences" class="com.something.UserPreferences" scope="session">
        <!-- instructs the container to proxy the surrounding bean -->
        <aop:scoped-proxy/> <!-- 	The line that defines the proxy. -->
    </bean>

    <!-- a singleton-scoped bean injected with a proxy to the above bean -->
    <bean id="userService" class="com.something.SimpleUserService">
        <!-- a reference to the proxied userPreferences bean -->
        <property name="userPreferences" ref="userPreferences"/>
    </bean>
</beans>
````

为了创建这样的代理，你插入一个子 ````<aop:scoped-proxy>```` 元素到一个拥有作用域的 bean 定义中（参考  [Choosing the Type of Proxy to Create](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-other-injection-proxies) 和 [XML Schema-based configuration](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/core.html#xsd-schemas)）。为什么定义作用域为 ````request````、````session```` 以及自定义作用域的 beans 需要使用 ````<aop:scoped-proxy>```` 元素？考虑下面的单例 bean 定义并将其与需要为上述作用域定义的内容作比较（注意，下面的 ````userPreferences````  bean 定义是不完整的）：

````xml
<bean id="userPreferences" class="com.something.UserPreferences" scope="session"/>

<bean id="userManager" class="com.something.UserManager">
    <property name="userPreferences" ref="userPreferences"/>
</bean>
````

在上面的例子中，该单例 bean ````userManager```` 被注入一个 HTTP ````session```` 作用域的 bean ````userPreferences```` 。这里的重点是 ````userManager```` bean 是一个单例：它每个容器只实例化一次，它的依赖项（在这种情况下只有一个，````userPreferences```` bean）也只注入一次。这意味着 ````userManager```` bean 仅在完全相同的 ````userPreferences```` 对象（即最初注入它的对象）上运行。

当将一个寿命较短的 bean 注入一个寿命较长的 bean 时，这不是你想要的行为（例如，将一个 HTTP ````Session````-scoped 协作 bean 作为依赖注入单例 bean）。相反，您需要一个 ````userManager```` 对象，并且，对于 HTTP 会话的生命周期，您需要一个特定于 HTTP 会话的 ````userPreferences```` 对象。因此，容器创建一个对象，该对象公开与 ````UserPreferences````类（理想情况下是 ````UserPreferences```` 实例的对象）完全相同的公共接口，该对象可以从作用域机制（HTTP 请求、````Session```` 等）获取真实的 ````UserPreferences```` 对象。容器将此代理对象注入 ````userManager```` bean，该bean不知道此 ````UserPreferences```` 引用是代理。在此示例中，当 ````UserManager```` 实例在依赖注入的 ````UserPreferences```` 对象上调用方法时，它实际上是在代理上调用方法。然后，代理从（在这种情况下）HTTP ````Session```` 中获取真实的 ````UserPreferences```` 对象，并将方法调用委托给检索到的真实 ````UserPreferences```` 对象。

因此，在将 ````request```` 和 ````session-scoped```` 的 bean 注入协作对象时，您需要以下（正确和完整）配置，如以下示例所示：

````xml
<bean id="userPreferences" class="com.something.UserPreferences" scope="session">
    <aop:scoped-proxy/>
</bean>

<bean id="userManager" class="com.something.UserManager">
    <property name="userPreferences" ref="userPreferences"/>
</bean>
````

**选择代理创建的类型**

默认地，当 Spring 容器为一个用 ````<aop:scoped-proxy/>```` 标记的 bean 创建一个代理时，一个基于 CGLIB 的代理类被创建。

> CGLIB 代理只会拦截 public 方法调用！不用在这个代理上调用非 public 方法。那些方法调用并不会被下放给实际的作用域内的目标对象。

另外，你可以配置 Spring 容器来为这种有作用域的 beans 创建标准的 JDK 基于接口的代理，通过指定 ````<aop:scoped-proxy/>```` 元素上的 ````proxy-target-class```` 属性的值为 ````false```` 。使用 JDK 基于接口的代理意味着你不需要在应用的类路径上放置额外的类库来影响此类代理。不过，它同时也意味着作用域内的 beans 的类型必须实现至少一个接口，同时，该 bean 被注入的所有协作者都必须通过这些接口中的一个引用它。下面的例子展示了一个基于接口的代理：

````xml
<!-- DefaultUserPreferences implements the UserPreferences interface -->
<bean id="userPreferences" class="com.stuff.DefaultUserPreferences" scope="session">
    <aop:scoped-proxy proxy-target-class="false"/>
</bean>

<bean id="userManager" class="com.stuff.UserManager">
    <property name="userPreferences" ref="userPreferences"/>
</bean>
````

有关选择基于类的代理还是基于接口的代理的更多细节可参考 [Proxying Mechanisms](https://docs.spring.io/spring/docs/5.1.6.RELEASE/spring-framework-reference/core.html#aop-proxying)。

#### 1.5.5 自定义作用域

bean 作用域机制是可扩展的。你可以定义你自己的作用域，甚至重新定义已经存在的作用域，尽管后者通常被认为不是什么好的做法，同时你也不能覆盖内建的 ````singleton```` 和 ````prototype```` 作用域。

**创建自定义作用域**

为了将你的自定义作用域集成到 Spring 容器中，你需要实现 ````org.springframework.beans.factory.config.Scope```` 接口，该接口将在本节描述。为了了解如何实现你自己的作用域，参考 Spring 框架本身自带的 ````Scope```` 实现及其文档说明，那里详细介绍了你需要实现的方法细节。

````Scope```` 接口拥有四个方法来从作用域中获取对象、从作用域中删除它们以及使它们被销毁。

以会话作用域实现为例，返回会话作用域的 bean (如果不存在，则该方法返回一个 bean 的新实例，在将其绑定到一个会话之后，为了将来的引用)。下面的方法返回潜在作用域中的对象：

````java
Object get(String name, ObjectFactory objectFactory)
````

会话作用域实现，从潜在的会话中清除会话作用域的 bean 。该对象应该被返回，不过，如果特定名称的对象没有找到，则你可以返回 ````null````  。下面的方法从潜在作用域中删除对象：

````java
Object remove(String name)
````

下面的方法注册作用域在它自身被销毁或者该作用域中特定名称的对象被销毁时应该执行的回调：

````java
void registerDestructionCallbacks(String name, Runnable destructionCallback)
````

参考  [javadoc](https://docs.spring.io/spring-framework/docs/5.1.6.RELEASE/javadoc-api/org/springframework/beans/factory/config/Scope.html#registerDestructionCallback) 获取更多有关销毁回调的细节。

下面的方法获取潜在作用域的会话标识符：

````java
String getConversationId()
````

该标识符每个作用域都不同。对会话作用域实现而言，该标识符可以是该会话的标识符。

**使用自定义作用域**

当你编写并测试一个或者多个自定义 `Scope` 实现之后，你需要让 Spring 容器注意到你的新的作用域。下面的方法是向 Spring 容器注册新的 `Scope` 的核心方法：

```java
void registerScope(String scopeName, Scope scope);
```

上面的方法声明在 `ConfigurableBeanFactory` 接口中，该接口可通过 Spring 随附的大多数具体 `ApplicationContext` 实现上的 `BeanFactory` 属性获得。

`registerScope(...)` 方法的第一个参数是与作用域关联的唯一名称。Spring 容器本身中的这些名称的实例是 `singleton` 和 `prototype`。`registerScope(...)` 方法的第二个参数是您希望注册和使用的自定义 `Scope` 实现的实例。

假设您编写自定义 `Scope` 实现，然后按照下一个示例中的说明进行注册。

> 下一个示例使用 `SimpleThreadScope` ，它包含在 Spring 中，但默认情况下未注册。对于您自己的自定义 `Scope` 实现，指令是相同的。

```java
Scope threadScope = new SimpleThreadScope();
beanFactory.registerScope("thread", threadScope);
```

然后，您可以创建符合自定义 `Scope` 规则的 `bean` 定义，如下所示：

```java
<bean id="..." class="..." scope="thread">
```

使用自定义 `Scope` 实现，您不必局限于 `Scope` 的编程式注册。您还可以使用 `CustomScopeConfigurer` 类以声明方式执行作用域注册。如以下示例所示：

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:aop="http://www.springframework.org/schema/aop"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/aop
        http://www.springframework.org/schema/aop/spring-aop.xsd">

    <bean class="org.springframework.beans.factory.config.CustomScopeConfigurer">
        <property name="scopes">
            <map>
                <entry key="thread">
                    <bean class="org.springframework.context.support.SimpleThreadScope"/>
                </entry>
            </map>
        </property>
    </bean>

    <bean id="thing2" class="x.y.Thing2" scope="thread">
        <property name="name" value="Rick"/>
        <aop:scoped-proxy/>
    </bean>

    <bean id="thing1" class="x.y.Thing1">
        <property name="thing2" ref="thing2"/>
    </bean>

</beans>
```

> 当你在 `FactoryBean` 实现中放置 `<aop:scope-proxy/>` 时，它表示有作用域的工厂 bean 自己，而不是由 `getObject()` 返回的对象。

### 1.6 定制 Bean 本质属性

Spring Framework 提供了许多可用于自定义 bean 特性的接口。本节将它们分组如下：

- [生命周期回调](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle)
- [`ApplicationContextAware` and `BeanNameAware`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-aware)
- [其它 `Aware` 接口](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#aware-list)

#### 1.6.1 生命周期回调

要与容器的 bean 生命周期管理进行交互，可以实现 Spring `InitializingBean` 和 `DisposableBean` 接口。容器为前者调用 `afterPropertiesSet()`，为后者调用 `destroy()`，在 bean 初始化和销毁时执行某些操作。

> JSR-250 `@PostConstruc` t和 `@PreDestroy` 注解通常被认为是在现代 Spring 应用程序中接收生命周期回调的最佳实践。使用这些注释意味着您的 bean 不会耦合到特定于 Spring 的接口。有关详细信息，请参阅 [使用 `@PostConstruct` 和 `@PreDestroy`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-postconstruct-and-predestroy-annotations) 。
>
> 如果您不想使用 JSR-250 注解但仍想删除耦合，请考虑 `init-method` 和 `destroy-method`  bean定义元数据。

在内部，Spring Framework 使用 `BeanPostProcessor` 实现来处理它可以找到的任何回调接口并调用适当的方法。如果您需要 Spring 默认提供的自定义功能或其他生命周期行为，您可以自己实现 `BeanPostProcessor` 。 有关更多信息，请参阅  [容器扩展点](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-extension) 。

除了初始化和销毁回调之外，Spring 管理的对象还可以实现 `Lifecycle` 接口，以便这些对象可以参与启动和关闭过程，这是由容器自身的生命周期驱动的。

本节描述了生命周期回调接口。

**初始化回调**

`org.springframework.beans.factory.InitializingBean` 接口允许 bean 在容器为其设置所有必需属性后执行初始化工作。`InitializingBean` 接口指定一个方法：

```java
void afterPropertiesSet() throws Exception;
```

我们建议您不要使用 `InitializingBean` 接口，因为它会不必要地将代码耦合到 Spring。我们建议使用 [`@PostConstruct`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-postconstruct-and-predestroy-annotations) 注解或指定 POJO 初始化方法。对于基于 XML 的配置元数据，可以使用 `init-method` 属性指定具有 `void` 无参数签名的方法的名称。使用 Java 配置，您可以使用 `@Bean的initMethod` 属性。请参阅 [接收生命周期回调](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-java-lifecycle-callbacks) 。 请考虑以下示例：

```xml
<bean id="exampleInitBean" class="examples.ExampleBean" init-method="init"/>
```

```java
public class ExampleBean {

    public void init() {
        // do some initialization work
    }
}
```

前面的示例与以下示例几乎完全相同（包含两个列表）：

```java
<bean id="exampleInitBean" class="examples.AnotherExampleBean"/>
public class AnotherExampleBean implements InitializingBean {

    public void afterPropertiesSet() {
        // do some initialization work
    }
}
```

但是，前面两个示例中的第一个没有将代码耦合到Spring。

**销毁回调**

实现 `org.springframework.beans.factory.DisposableBean` 接口允许 bean 在包含它的容器被销毁时获得回调。`DisposableBean` 接口指定一个方法：

```java
void destroy() throws Exception;
```

我们建议您不要使用 `DisposableBean` 回调接口，因为它会不必要地将代码耦合到 Spring。我们建议使用 [`@PreDestroy`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-postconstruct-and-predestroy-annotations)  注解或指定 bean 定义支持的泛型方法。使用基于 XML 的配置元数据，您可以在 `<bean />` 上使用 `destroy-method` 属性。使用Java配置，您可以使用 `@Bean` 的 `destroyMethod`属性。 请参阅 [Receiving Lifecycle Callbacks](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-java-lifecycle-callbacks) 。 考虑以下定义：

```xml
<bean id="exampleInitBean" class="examples.ExampleBean" destroy-method="cleanup"/>
```

```java
public class ExampleBean {

    public void cleanup() {
        // do some destruction work (like releasing pooled connections)
    }
}
```

前面的定义与以下定义几乎完全相同：

```xml
<bean id="exampleInitBean" class="examples.AnotherExampleBean"/>
```

```java
public class AnotherExampleBean implements DisposableBean {

    public void destroy() {
        // do some destruction work (like releasing pooled connections)
    }
}
```

但是，前面两个定义中的第一个没有将代码耦合到Spring。

> 您可以为 `<bean>` 元素的 `destroy-method` 属性分配一个特殊`(inferred)` 值，该值指示 Spring 自动检测特定 bean 类的`public`的 `close` 或 `shutdown` 方法。（因此，任何实现 `java.lang.AutoCloseable` 或 `java.io.Closeable` 的类都将匹配。）您还可以在 `<beans>` 元素的 `default-destroy-method` 属性上设置此特殊 `(inferred)` 值，以将此行为应用于 一整套 bean（参见 [默认初始化和销毁方法](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-default-init-destroy-methods)）。请注意，这是 Java 配置的默认行为。

**默认初始化和销毁方法**

当您编写初始化和销毁不使用特定于 Spring 的 `InitializingBean` 和 `DisposableBean` 回调接口的方法回调时，通常会编写名称为 `init()`，`initialize()`，`dispose()` 等的方法。理想情况下，此类生命周期回调方法的名称在项目中是标准化的，以便所有开发人员使用相同的方法名称并确保一致性。

您可以将 Spring 容器配置为“查找”命名初始化并销毁每个 bean 上的回调方法名称。这意味着，作为应用程序开发人员，您可以编写应用程序类并使用名为 `init()` 的初始化回调，而无需为每个 bean 定义配置 `init-method ="init"` 属性。Spring IoC 容器在创建 bean 时调用该方法（并且符合前面描述的标准生命周期回调约定）。此功能还强制执行初始化和销毁方法回调的一致命名约定。

假定你的初始化回调方法名为 `init()` 同时你的销毁方法名为 `destroy()` 。你的类就可以装配进入下面例子中的类：

```java
public class DefaultBlogService implements BlogService {

    private BlogDao blogDao;

    public void setBlogDao(BlogDao blogDao) {
        this.blogDao = blogDao;
    }

    // this is (unsurprisingly) the initialization callback method
    public void init() {
        if (this.blogDao == null) {
            throw new IllegalStateException("The [blogDao] property must be set.");
        }
    }
}
```

然后你就可以在下面的类组装中使用该类：

```xml
<beans default-init-method="init">

    <bean id="blogService" class="com.something.DefaultBlogService">
        <property name="blogDao" ref="blogDao" />
    </bean>

</beans>
```

顶级`<beans/>`元素属性中存在`default-init-method`属性会导致Spring IoC容器将bean类上的一个名为`init`的方法识别为初始化方法回调。当bean被创建和组装时，如果bean类具有这样的方法，则在适当的时候调用它。

您可以通过在顶级`<beans/>`元素上使用`default-destroy-method`属性来类似地配置 `destroy` 方法回调（在XML中）。

如果现有bean类已经具有与约定一致的变量命名的回调方法，则可以通过使用`<bean/>`本身的 `init-method`和`destroy-method`属性指定（在XML中）方法名称来覆盖缺省值。 

Spring容器保证在为bean提供所有依赖项后立即调用已配置的初始化回调。因此，在原始bean引用上调用初始化回调，这意味着 AOP 拦截器等尚未应用于bean。首先完全创建目标bean，然后应用带有拦截器链的 AOP 代理（例如）。如果目标bean和代理是分开定义的，那么您的代码甚至可以绕过代理与原始目标bean交互。因此，将拦截器应用于`init`方法是不一致的，因为这样做会将目标bean的生命周期耦合到其代理或拦截器，并在代码直接与原始目标bean交互时形成奇怪的语义。

