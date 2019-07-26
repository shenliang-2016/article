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

Spring容器保证在为bean提供所有依赖项后立即调用已配置的初始化回调。因此，在原始bean引用上调用初始化回调，这意味AOP拦截器等尚未应用于bean。首先完全创建目标bean，然后应用带有拦截器链的AOP代理（例如）。如果目标bean和代理是分开定义的，那么您的代码甚至可以绕过代理与原始目标bean交互。因此，将拦截器应用于`init`方法是不一致的，因为这样做会将目标bean的生命周期耦合到其代理或拦截器，并在代码直接与原始目标bean交互时形成奇怪的语义。

**结合生命周期机制**

作为 Spring 2.5，你可以有以下三种选择来控制 bean 的生命周期行为：

-  [`InitializingBean`](https://docs.spring.io/spring/docs/5.1.7.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-initializingbean) 和 [`DisposableBean`](https://docs.spring.io/spring/docs/5.1.7.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-disposablebean) 回调接口
-  定制 `init()` 和 `destroy()` 方法
-  [`@PostConstruct` 和 `@PreDestroy` 注解](https://docs.spring.io/spring/docs/5.1.7.RELEASE/spring-framework-reference/core.html#beans-postconstruct-and-predestroy-annotations) 。你可以结合这些机制来控制给定的 bean。

> 如果为bean配置了多个生命周期机制，并且每个机制都配置了不同的方法名称，则每个配置的方法都按照此注释后列出的顺序执行。但是，如果为初始化方法配置了相同的方法名称，例如`init()` - 对于多个这些生命周期机制，该方法将执行一次，如[上一节中所述。

为同一个bean配置的多个生命周期机制具有不同的初始化方法，如下所示：

1.  `@PostConstruct` 注解修饰的方法
2.  `afterPropertiesSet()` 作为 `InitializingBean` 回调接口定义的方法
3.  定制的 `init()` 方法


销毁方法按照相同顺序被调用：

1.  `@PreDestroy` 注解修饰的方法
2.  `destroy()` 作为 `DisposableBean` 回调接口定义的方法
3.  定制的 `destroy()` 方法

**启动和关闭回调**

 `Lifecycle` 接口为所有具有生命周期管理需求的对象定义基础方法 (比如启动和停止某些后台进程)：

```java
public interface Lifecycle {

    void start();

    void stop();

    boolean isRunning();
}
```

任何Spring管理的对象都可以实现 `Lifecycle` 接口。然后，当 `ApplicationContext` 本身接收到启动和停止信号时（例如，对于运行时的停止/重启场景），它会将这些调用级联到该上下文中定义的所有生命周期实现。它通过委托 `LifecycleProcessor` 完成此操作，如下面的清单所示：

```java
public interface LifecycleProcessor extends Lifecycle {

    void onRefresh();

    void onClose();
}
```

注意 `LifecycleProcessor` 本身就扩展了 `Lifecycle` 接口。它同时还添加了其它两个方法来与被刷新或者关闭的上下文交互。

> 请注意，常规 `org.springframework.context.Lifecycle` 接口是显式启动和停止通知的简单契约，并不意味着在上下文刷新时自动启动。要对特定bean的自动启动（包括启动阶段）进行细粒度控制，请考虑实现 `org.springframework.context.SmartLifecycle` 。
>
> 此外，请注意，不能保证停止通知在销毁之前到来。在常规关闭时，所有 `Lifecycle`  bean首先会在传播常规销毁回调之前收到停止通知。但是，在上下文生命周期中的热刷新或中止刷新尝试时，仅 `destroy` 方法被调用。

启动和关闭调用的顺序非常重要。如果任何两个对象之间存在“依赖”关系，则依赖方在其依赖之后开始，并且在其依赖之前停止。但是，有时，直接依赖性是未知的。您可能只知道某种类型的对象应该在另一种类型的对象之前开始。在这些情况下，`SmartLifecycle` 接口定义了另一个选项，即在其超级接口 `Phased` 上定义的 `getPhase()` 方法。以下清单显示了 `Phased` 接口的定义：

```java
public interface Phased {

    int getPhase();
}
```

下面是 `SmartLifecycle` 接口定义：

```java
public interface SmartLifecycle extends Lifecycle, Phased {

    boolean isAutoStartup();

    void stop(Runnable callback);
}
```

启动时，具有最低 `phase` 值的对象首先开始。停止时，遵循相反的顺序。因此，实现 `SmartLifecycle` 并且其 `getPhase()` 方法返回 `Integer.MIN_VALUE` 的对象将是第一个开始和最后一个停止的对象。在频谱的另一端，`Integer.MAX_VALUE` 的 `phase` 值将指示对象应该最后启动并首先停止（可能是因为它依赖于正在运行的其他进程）。在考虑 `phase` 值时，同样重要的是要知道任何未实现 `SmartLifecycle` 的“正常” `Lifecycle`对象的默认 `phase` 值为0。因此，任何负 `phase` 值都表示对象应该在这些标准组件之前启动（并停止在他们之后）。任何正 `phase` 值都是相反的。

`SmartLifecycle` 定义的 `stop` 方法接受回调。在该实现的关闭过程完成之后，任何实现都必须调用该回调的 `run()` 方法。这样可以在必要时启用异步关闭，因为 `LifecycleProcessor` 接口的默认实现 `DefaultLifecycleProcessor` 等待每个阶段内的对象组的超时值来调用该回调。默认的每阶段超时为30秒。您可以通过在上下文中定义名为 `lifecycleProcessor` 的 bean 来覆盖缺省生命周期处理器实例。如果您只想修改超时，则定义以下内容就足够了：

```xml
<bean id="lifecycleProcessor" class="org.springframework.context.support.DefaultLifecycleProcessor">
    <!-- timeout value in milliseconds -->
    <property name="timeoutPerShutdownPhase" value="10000"/>
</bean>
```

如前所述，`LifecycleProcessor` 接口还定义了用于刷新和关闭上下文的回调方法。后者驱动关闭过程，就像显式调用了 `stop()` 一样，但是当上下文关闭时会发生。另一方面，'refresh' 回调启用了 `SmartLifecycle`  bean的另一个功能。刷新上下文时（在实例化并初始化所有对象之后），将调用该回调。此时，默认生命周期处理器检查每个 `SmartLifecycle` 对象的 `isAutoStartup()` 方法返回的布尔值。如果为 `true`，则在该点启动该对象，而不是等待显式调用上下文或其自己的 `start()` 方法（与上下文刷新不同，上下文启动不会自动发生在标准上下文实现中）。如前所述，`phase` 值和任何“依赖”关系确定启动顺序。

**在非Web应用程序中优雅地关闭Spring IoC容器**

> 本节仅适用于非Web应用程序。 Spring的基于Web的 `ApplicationContext`实现已经具有相关功能，可以在相关Web应用程序关闭时正常关闭Spring IoC容器。

如果在非Web应用程序环境中使用Spring的IoC容器（例如，在富客户端桌面环境中），请使用JVM注册关闭挂钩。这样做可确保正常关闭并在单例bean上调用相关的 `destroy` 方法，以便释放所有资源。您仍然必须正确配置和实现这些 `destroy` 回调。

要注册关闭挂钩，请调用  `ConfigurableApplicationContext` 接口上声明的 `registerShutdownHook()` 方法，如以下示例所示：

```java
import org.springframework.context.ConfigurableApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;

public final class Boot {

    public static void main(final String[] args) throws Exception {
        ConfigurableApplicationContext ctx = new ClassPathXmlApplicationContext("beans.xml");

        // add a shutdown hook for the above context...
        ctx.registerShutdownHook();

        // app runs here...

        // main method exits, hook is called prior to the app shutting down...
    }
}
```

#### 1.6.2`ApplicationContextAware` 和 `BeanNameAware`

当 `ApplicationContext` 创建实现 `org.springframework.context.ApplicationContextAware` 接口的对象实例时，将为该实例提供对该 `ApplicationContext` 的引用。以下清单显示了 `ApplicationContextAware` 接口的定义：

```java
public interface ApplicationContextAware {

    void setApplicationContext(ApplicationContext applicationContext) throws BeansException;
}
```

因此，bean可以通过 `ApplicationContext` 接口以编程方式操作创建它们的 `ApplicationContext` ，或者通过将引用转换为此接口的已知子类（例如 `ConfigurableApplicationContext`，它暴露其他功能）。一种用途是对其他bean进行编程检索。有时这种能力很有用。但是，一般情况下，您应该避免使用它，因为它将代码耦合到Spring并且不遵循 `Inversion of Control` 风格，其中协作者作为属性提供给bean。`ApplicationContext` 的其他方法提供对文件资源的访问，发布应用程序事件和访问 `MessageSource`。 这些附加功能在 [`ApplicationContext` 的附加功能](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#context-introduction) 中描述。

从Spring 2.5开始，自动装配是另一种获取 `ApplicationContext` 引用的替代方法。“传统”构造函数和 `byType` 自动装配模式（如  [Autowiring Collaborators](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-autowire) 中所述）可以分别为构造函数参数或 `setter` 方法参数提供 `ApplicationContext` 的依赖性。为了获得更大的灵活性，包括自动装配字段和多参数方法的能力，请使用基于注解的自动装配功能。如果这样做， `ApplicationContext` 将自动装入一个字段，构造函数参数或方法参数，或者上面涉及到的方法，都带有 `@Autowired` 注解，则该参数需要 `ApplicationContext`。 有关更多信息，请参阅 [使用 `@Autowired`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-autowired-annotation) 。

当 `ApplicationContext` 创建实现 `org.springframework.beans.factory.BeanNameAwareinterface` 的类时，将为该类提供对其关联对象定义中定义的名称的引用。以下清单显示了 `BeanNameAware` 接口的定义：

```java
public interface BeanNameAware {

    void setBeanName(String name) throws BeansException;
}
```

The callback is invoked after population of normal bean properties but before an initialization callback such as `InitializingBean`, `afterPropertiesSet`, or a custom init-method.

在普通bean属性的产生之后、在初始化回调之前调用的回调方法诸如 `InitializingBean`，`afterPropertiesSet` 或自定义 `init` 方法。

#### 1.6.3  其它`Aware`接口

除了 `ApplicationContextAware` 和 `BeanNameAware`（前面讨论过）之外，Spring还提供了一系列 `Aware` 接口，让bean向容器表明它们需要某种基础结构依赖性。作为一般规则，名称是依赖类型的良好指示。下表总结了最重要的 `Aware` 接口：

| 名称                               | 依赖注入                                     | 解释                                       |
| -------------------------------- | ---------------------------------------- | ---------------------------------------- |
| `ApplicationContextAware`        | 声明 `ApplicationContext` 。                | [`ApplicationContextAware` and `BeanNameAware`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-aware) |
| `ApplicationEventPublisherAware` | `ApplicationContext` 中包装的时间发布器。          | [Additional Capabilities of the `ApplicationContext`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#context-introduction) |
| `BeanClassLoaderAware`           | 类加载器用来加载 bean 类。                         | [Instantiating Beans](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-class) |
| `BeanFactoryAware`               | 声明 `BeanFactory` 。                       | [`ApplicationContextAware` and `BeanNameAware`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-aware) |
| `BeanNameAware`                  | 声明 bean 的名称。                             | [`ApplicationContextAware` and `BeanNameAware`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-aware) |
| `BootstrapContextAware`          | 资源适配器`BootstrapContext` 运行所在的容器。通常仅在JCA敏感的 `ApplicationContext` 实例中可用。 | [JCA CCI](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/integration.html#cci) |
| `LoadTimeWeaverAware`            | 定义的weaver用于在加载时处理类定义。                    | [Load-time Weaving with AspectJ in the Spring Framework](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#aop-aj-ltw) |
| `MessageSourceAware`             | 用于解析消息的已配置策略（支持参数化和国际化）。                 | [Additional Capabilities of the `ApplicationContext`](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#context-introduction) |
| `NotificationPublisherAware`     | Spring JMX 通知发布器。                        | [Notifications](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/integration.html#jmx-notifications) |
| `ResourceLoaderAware`            | 配置的加载程序，用于对资源进行低级访问。                     | [Resources](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#resources) |
| `ServletConfigAware`             | 容器运行的当前 `ServletConfig`。仅在Web敏感的Spring `ApplicationContext` 中有效。 | [Spring MVC](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc) |
| `ServletContextAware`            | 容器运行的当前 `ServletContext`。仅在Web敏感的Spring `ApplicationContext` 中有效。 | [Spring MVC](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/web.html#mvc) |

请再次注意，使用这些接口会将您的代码绑定到Spring API，而不会遵循 `Inversion of Control` 风格。因此，我们建议将它们用于需要以编程方式访问容器的基础架构bean。

### 1.7 Bean 定义继承

bean定义可以包含许多配置信息，包括构造函数参数，属性值和特定于容器的信息，例如初始化方法，静态工厂方法名称等。子bean定义从父定义继承配置数据。子定义可以覆盖某些值或根据需要添加其他值。使用父bean和子bean定义可以节省大量的输入。实际上，这是一种模板形式。

如果以编程方式使用 `ApplicationContext` 接口，则子bean定义由 `ChildBeanDefinition` 类表示。大多数用户不在此级别上使用它们。相反，它们在类（如 `ClassPathXmlApplicationContext`）中以声明方式配置bean定义。使用基于XML的配置元数据时，可以使用 `parent` 属性指定子bean定义，将父bean指定为此属性的值。以下示例显示了如何执行此操作：

```xml
<bean id="inheritedTestBean" abstract="true"
        class="org.springframework.beans.TestBean">
    <property name="name" value="parent"/>
    <property name="age" value="1"/>
</bean>

<bean id="inheritsWithDifferentClass"
        class="org.springframework.beans.DerivedTestBean"
        parent="inheritedTestBean" init-method="initialize">  
    <property name="name" value="override"/>
    <!-- the age property value of 1 will be inherited from parent -->
</bean>
```

如果没有指定，则bean定义使用父定义中的bean类，但也可以覆盖它。在后一种情况下，子bean类必须与父类兼容（即，它必须接受父类的属性值）。

子bean定义从父级继承作用域，构造函数参数值，属性值和方法覆盖，并带有添加新值的选项。 您指定的任何作用域，初始化方法，销毁方法或静态工厂方法设置都会覆盖相应的父设置。

其余设置始终取自子定义：依赖，`autowire` 模式，依赖性检查，单例和惰性初始化。

前面的示例通过使用 `abstract` 属性将父bean定义显式标记为 `abstract`。如果父定义未指定类，则需要将父bean定义显式标记为 `abstract`，如以下示例所示：

```xml
<bean id="inheritedTestBeanWithoutClass" abstract="true">
    <property name="name" value="parent"/>
    <property name="age" value="1"/>
</bean>

<bean id="inheritsWithClass" class="org.springframework.beans.DerivedTestBean"
        parent="inheritedTestBeanWithoutClass" init-method="initialize">
    <property name="name" value="override"/>
    <!-- age will inherit the value of 1 from the parent bean definition-->
</bean>
```

父bean不能单独实例化，因为它不完整，并且也明确标记为 `abstract` 的。当定义是 `abstract` 的时，它仅可用作纯模板bean定义，用作子定义的父定义。尝试使用这样一个 `abstract` 的父bean，通过将它作为另一个bean的 `ref` 属性引用或者使用父bean ID进行显式 `getBean()` 调用会返回错误。类似地，容器的内部 `preInstantiateSingletons()` 方法忽略定义为 `abstract` 的bean定义。

> `ApplicationContext` 默认情况下预先实例化所有单例。因此，重要的是（至少对于单例bean），如果你有一个（父）bean定义，而你只打算将其用作模板，并且这个定义指定了一个类，你必须确保将 `abstract` 属性设置为 `true` 。 否则应用程序上下文将实际（尝试）预先实例化该抽象bean。

### 1.8 容器扩展点

通常，应用程序开发人员不需要继承 `ApplicationContext` 实现类。相反，可以通过插入特殊集成接口的实现来扩展Spring IoC容器。接下来的几节将介绍这些集成接口。

#### 1.8.1 使用 `BeanPostProcessor` 自定义Bean

`BeanPostProcessor` 接口定义了可以实现的回调方法，以提供您自己的（或覆盖容器的默认）实例化逻辑，依赖关系解析逻辑等。如果要在Spring容器完成实例化，配置和初始化bean之后实现某些自定义逻辑，则可以插入一个或多个自定义 `BeanPostProcessor` 实现。

您可以配置多个 `BeanPostProcessor` 实例，并且可以通过设置 `order` 属性来控制这些 `BeanPostProcessor` 实例的执行顺序。仅当 `BeanPostProcessor` 实现 `Ordered` 接口时，才能设置此属性。如果编写自己的 `BeanPostProcessor`，则应考虑实现 `Ordered` 接口。有关更多详细信息，请参阅 [`BeanPostProcessor`](https://docs.spring.io/spring-framework/docs/5.1.5.RELEASE/javadoc-api/org/springframework/beans/factory/config/BeanPostProcessor.html) 和 [`Ordered`](https://docs.spring.io/spring-framework/docs/5.1.5.RELEASE/javadoc-api/org/springframework/core/Ordered.html) 接口文档。另请参阅 [编程方式注册`BeanPostProcessor` 实例](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-programmatically-registering-beanpostprocessors) 。

> `BeanPostProcessor` 实例操作bean（或对象）实例。也就是说，Spring IoC容器实例化一个bean实例，然后 `BeanPostProcessor` 实例完成它们的工作。
>
> `BeanPostProcessor` 实例的作用域是容器范围。仅当您使用容器层次结构时，这才是相关的。如果在一个容器中定义 `BeanPostProcessor`，它只对该容器中的bean进行后处理。换句话说，在一个容器中定义的bean不会被另一个容器中定义的 `BeanPostProcessor` 进行后处理，即使两个容器都是同一层次结构的一部分。
>
> 要更改实际的bean定义（即定义bean的蓝图），您需要使用 `BeanFactoryPostProcessor`，如 [Customizing Configuration Metadata with a 通过 `BeanFactoryPostProcessor` 定制配置元数据](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/core.html#beans-factory-extension-factory-postprocessors) 中所述。

`org.springframework.beans.factory.config.BeanPostProcessor` 接口由两个回调方法组成。当这样的类被注册为容器的后处理器时，对于容器创建的每个bean实例，后处理器在容器初始化方法之前从容器中获取回调（例如 `InitializingBean.afterPropertiesSet()` 或在任何bean初始化回调之后调用任何声明的 `init` 方法）。后处理器可以对bean实例执行任何操作，包括完全忽略回调。bean后处理器通常检查回调接口，或者它可以用代理包装bean。一些Spring AOP基础结构类实现为bean后处理器，以便提供代理包装逻辑。

`ApplicationContext` 自动检测在实现 `BeanPostProcessor` 接口的配置元数据中定义的任何bean。`ApplicationContext` 将这些bean注册为后处理器，以便在创建bean时可以稍后调用它们。Bean后处理器可以以与任何其他bean相同的方式部署在容器中。

注意，在配置类上使用 `@Bean` 工厂方法声明 `BeanPostProcessor` 时，工厂方法的返回类型应该是实现类本身，或者至少是 `org.springframework.beans.factory.config.BeanPostProcessor` 接口，指示该bean的后处理器性质。否则， `ApplicationContext` 无法在完全创建之前按类型自动检测它。由于 `BeanPostProcessor` 需要尽早实例化以便应用于上下文中其他bean的初始化，因此这种早期类型检测至关重要。

> 以编程方式注册 `BeanPostProcessor` 实例
> 虽然 `BeanPostProcessor` 注册的推荐方法是通过 `ApplicationContext` 自动检测（如前所述），但您可以使用`addBeanPostProcessor` 方法以编程方式对 `ConfigurableBeanFactory` 注册它们。当您需要在注册前评估条件逻辑或甚至跨层次结构中的上下文复制 Bean 后处理器时，这非常有用。但请注意，以编程方式添加的 `BeanPostProcessor` 实例不遵循 `Ordered` 接口。这里，注册的顺序决定了执行的顺序。另请注意，以编程方式注册的 `BeanPostProcessor` 实例始终在通过自动检测注册的实例之前处理，而不管任何显式排序。

> `BeanPostProcessor` 实例和 `AOP` 自动代理
> 实现 `BeanPostProcessor` 接口的类是特殊的，容器会对它们进行不同的处理。作为 `ApplicationContext` 的特殊启动阶段的一部分，它们直接引用的所有 `BeanPostProcessor` 实例和 bean 都在启动时实例化。接下来，所有 `BeanPostProcessor` 实例都以排序方式注册，并应用于容器中的所有其他 bean。因为 `AOP` 自动代理是作为 `BeanPostProcessor` 本身实现的，所以 `BeanPostProcessor` 实例和它们直接引用的 bean 都不符合自动代理的条件，因此没有编入方法。
>
> 对于任何此类 bean，您应该看到一条信息性日志消息：Bean `someBean` 不适合所有 `BeanPostProcessor` 接口处理（例如：不符合自动代理条件）。
>
> 如果您通过使用自动装配或 `@Resource`（可能回退到自动装配）将 Bean 连接到 `BeanPostProcessor`，则Spring可能会在搜索类型匹配依赖项候选项时访问意外的 bean，因此使它们不符合自动代理或其他类型的条件 Bean 后处理。例如，如果您有一个使用 `@Resource` 注解的依赖项，其中字段或 `setter` 名称不直接对应于 bean 的声明名称而且没有使用 `name` 属性，则Spring会访问其他 bean 以按类型匹配它们。

以下示例显示如何在 `ApplicationContext` 中编写、注册和使用 `BeanPostProcessor` 实例。

**示例：Hello World，`BeanPostProcessor` 样式**

 第一个例子说明了基本用法。该示例显示了一个自定义 `BeanPostProcessor` 实现，该实现在容器创建时调用每个bean的 `toString()` 方法，并将生成的字符串输出到系统控制台。

以下清单显示了自定义 `BeanPostProcessor` 实现类定义：

```java
package scripting;

import org.springframework.beans.factory.config.BeanPostProcessor;

public class InstantiationTracingBeanPostProcessor implements BeanPostProcessor {

    // simply return the instantiated bean as-is
    public Object postProcessBeforeInitialization(Object bean, String beanName) {
        return bean; // we could potentially return any object reference here...
    }

    public Object postProcessAfterInitialization(Object bean, String beanName) {
        System.out.println("Bean '" + beanName + "' created : " + bean.toString());
        return bean;
    }
}
```

下面的 `beans` 元素使用了 `InstantiationTracingBeanPostProcessor`：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:lang="http://www.springframework.org/schema/lang"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/lang
        http://www.springframework.org/schema/lang/spring-lang.xsd">

    <lang:groovy id="messenger"
            script-source="classpath:org/springframework/scripting/groovy/Messenger.groovy">
        <lang:property name="message" value="Fiona Apple Is Just So Dreamy."/>
    </lang:groovy>

    <!--
    when the above bean (messenger) is instantiated, this custom
    BeanPostProcessor implementation will output the fact to the system console
    -->
    <bean class="scripting.InstantiationTracingBeanPostProcessor"/>

</beans>
```

注意如何定义`InstantiationTracingBeanPostProcessor`。 它甚至没有名称，并且，因为它是一个bean，它可以像任何其他bean一样依赖注入。（前面的配置还定义了一个由 Groovy 脚本支持的bean。在 [Dynamic Language Support](https://docs.spring.io/spring/docs/5.1.5.RELEASE/spring-framework-reference/languages.html#dynamic-language) 一章中详细介绍了Spring动态语言支持。

以下Java应用程序运行上述代码和配置：

```java
import org.springframework.context.ApplicationContext;
import org.springframework.context.support.ClassPathXmlApplicationContext;
import org.springframework.scripting.Messenger;

public final class Boot {

    public static void main(final String[] args) throws Exception {
        ApplicationContext ctx = new ClassPathXmlApplicationContext("scripting/beans.xml");
        Messenger messenger = (Messenger) ctx.getBean("messenger");
        System.out.println(messenger);
    }

}
```

上述应用程序的输出类似于以下内容：

```shell
Bean 'messenger' created : org.springframework.scripting.groovy.GroovyMessenger@272961
org.springframework.scripting.groovy.GroovyMessenger@272961
```

**例子： `RequiredAnnotationBeanPostProcessor`**

将回调接口或注解与自定义`BeanPostProcessor`实现结合使用是扩展Spring IoC容器的常用方法。一个例子是Spring的`RequiredAnnotationBeanPostProcessor`  - 一个随Spring发行版一起提供的`BeanPostProcessor`实现，它确保用（任意）注解标记的bean上的 Java Bean 属性确实（配置为）依赖注入一个值。

#### 1.8.2 使用`BeanFactoryPostProcessor`自定义配置元数据

我们寻找的下一个扩展点是`org.springframework.beans.factory.config.BeanFactoryPostProcessor`。这个接口的语义类似于`BeanPostProcessor`。不过有个主要的不同：`BeanFactoryPostProcessor`操作 bean 配置元数据。也就是说，Spring IoC 容器允许`BeanFactoryPostProcessor`读取配置元数据并能够在容器实例化除`BeanFactoryPostProcessor`实例之外任何实例之前修改配置元数据。

你可以配置多个`BeanFactoryPostProcessor`实例，并且还可以通过设定`order`属性来控制这些`BeanFactoryPostProcessor`实例的运行顺序。不过，只有`BeanFactoryPostProcessor`实现了`Ordered`接口时你才能这么做。如果你编写自己的`BeanFactoryPostProcessor`，你也应该考虑实现`Ordered`接口。参考文档 [`BeanFactoryPostProcessor`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/beans/factory/config/BeanFactoryPostProcessor.html) 和 [`Ordered`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/core/Ordered.html) 获取更多信息。

> 如果你想要改变实际的 bean 实例（根据配置元数据创建而来的对象），你就需要借助 `BeanPostProcessor`（前文 [Customizing Beans by Using a `BeanPostProcessor`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-extension-bpp) 中描述过 ）。尽管在 `BeanFactoryPostProcessor` 中操作 bean 实例在技术上是可能的（比如，通过使用 `BeanFactory.getBean()`），这么做会导致过早的 bean 实例化，因而违反了标准的容器生命周期管理规则。这可能会导致负面影响，比如可能会跳过 bean 后处理过程。
>
> 同时，`BeanFactoryPostProcessor` 实例的作用域是容器范围。仅当您使用容器层次结构时，这才有意义。如果在一个容器中定义`BeanFactoryPostProcessor`，它只应用于该容器中的bean定义。一个容器中的Bean定义不会被另一个容器中的`BeanFactoryPostProcessor`实例进行后处理，即使两个容器都是同一层次结构的一部分。

当它在 `ApplicationContext` 内部被声明时，bean 工厂后处理器自动执行，以便将修改应用到定义容器的配置元数据。Spring 包含大量的预定义 bean 工厂后处理器，比如 `PropertyOverrideConfigurer` and `PropertyPlaceholderConfigurer` 。你也可以使用自定义的 `BeanFactoryPostProcessor` - 比如，注册自定义属性编辑器。

`ApplicationContext`自动检测部署到其中的任何实现`BeanFactoryPostProcessor`接口的bean。它在适当的时候使用这些bean作为bean工厂后处理器。您可以像处理任何其他bean一样部署这些后处理器bean。

> 与`BeanPostProcessors`一样，您通常不希望为延迟初始化配置`BeanFactoryPostProcessors`。如果没有其他bean引用 `Bean(Factory)PostProcessor`，则该后处理器根本不会被实例化。因此，将忽略将其标记为延迟初始化，即使在`<beans/>`元素的声明中将`default-lazy-init`属性设置为`true`，也会急切地实例化`Bean(Factory)PostProcessor` 。

**示例：类名替换`PropertyPlaceholderConfigurer`**
您可以使用`PropertyPlaceholderConfigurer`通过使用标准Java Properties格式从单独文件中的bean定义外部化属性值。这样做可以使部署应用程序的人员自定义特定于环境的属性，例如数据库URL和密码，而不会出现修改主XML定义文件或容器文件的复杂性或风险。

请考虑以下基于XML的配置元数据片段，其中定义了具有占位符值的`DataSource`：

````xml
<bean class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
    <property name="locations" value="classpath:com/something/jdbc.properties"/>
</bean>

<bean id="dataSource" destroy-method="close"
        class="org.apache.commons.dbcp.BasicDataSource">
    <property name="driverClassName" value="${jdbc.driverClassName}"/>
    <property name="url" value="${jdbc.url}"/>
    <property name="username" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>
````

该示例显示了从外部 `Properties` 文件配置的属性。在运行时，`PropertyPlaceholderConfigurer`应用于替换`DataSource`的某些属性的元数据。要替换的值被指定为 `${property-name}`形式的占位符，它遵循 Ant 和 log4j 以及 JSP EL 样式。

实际值来自标准Java `Properties` 格式的另一个文件：

````xml
jdbc.driverClassName=org.hsqldb.jdbcDriver
jdbc.url=jdbc:hsqldb:hsql://production:9002
jdbc.username=sa
jdbc.password=root
````

因此， `${jdbc.username}` 字符串在运行时将替换为值'sa'，并且同样适用于与属性文件中的键匹配的其他占位符值。`PropertyPlaceholderConfigurer`检查bean定义的大多数属性和属性中的占位符。此外，您可以自定义占位符前缀和后缀。

使用Spring 2.5中引入的 `context` 命名空间，您可以使用专用配置元素配置属性占位符。您可以在 `location` 属性中以逗号分隔列表的形式提供一个或多个位置，如以下示例所示：

````xml
<context:property-placeholder location="classpath:com/something/jdbc.properties"/>
````

`PropertyPlaceholderConfigurer`不仅在您指定的 `Properties` 文件中查找属性。默认情况下，如果它在指定的属性文件中找不到属性，它还会检查Java `System`属性。您可以通过使用以下三个受支持的整数值之一设置configurer的`systemPropertiesMode`属性来自定义此行为：

* `never (0)`：从不检查系统属性。

* `fallback (1)`：如果在指定的属性文件中无法解析，则检查系统属性。这是默认值。

* `override (2)`：在尝试指定的属性文件之前，首先检查系统属性。这使系统属性可以覆盖任何其他属性源。

有关更多信息，请参见 [`PropertyPlaceholderConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/beans/factory/config/PropertyPlaceholderConfigurer.html) 文档。

> 您可以使用`PropertyPlaceholderConfigurer`来替换类名，当您必须在运行时选择特定的实现类时，这有时很有用。以下示例显示了如何执行此操作：
>
> ````xml
> <bean class="org.springframework.beans.factory.config.PropertyPlaceholderConfigurer">
>     <property name="locations">
>         <value>classpath:com/something/strategy.properties</value>
>     </property>
>     <property name="properties">
>         <value>custom.strategy.class=com.something.DefaultStrategy</value>
>     </property>
> </bean>
>
> <bean id="serviceStrategy" class="${custom.strategy.class}"/>
> ````
>
> 如果在运行时无法将类解析为有效的类，则在即将创建bean时，bean的解析将失败，这是在`ApplicationContext`为非延迟初始化 bean的`preInstantiateSingletons()`阶段期间。

**示例：`PropertyOverrideConfigurer`**

另一个bean工厂后处理器`PropertyOverrideConfigurer`类似于`PropertyPlaceholderConfigurer`，但与后者不同，原始定义可以具有默认值，或者根本没有值用于bean属性。如果覆盖的`Properties`文件没有某个bean属性的条目，则使用默认的上下文定义。

请注意，bean定义并不知道属性被覆盖，因此从XML定义文件中无法立即看出正在使用覆盖配置器。如果多个`PropertyOverrideConfigurer`实例为同一个bean属性定义不同的值，则由于覆盖机制，最后一个实例将生效。

属性文件配置行采用以下格式：

```
beanName.property=value
```

以下清单显示了格式的示例：

```
dataSource.driverClassName=com.mysql.jdbc.Driver
dataSource.url=jdbc:mysql:mydb
```

此示例文件可以与包含名为`dataSource`的bean的容器定义一起使用，该bean具有`driver`和`url`属性。

同时也支持复合属性名称，只要路径的每个组件（重写的最终属性除外）都已经非空（可能由构造函数初始化）。在下面的例子中，`tom` bean的`fred`属性的`bob`属性的`sammy`属性被设置为标量值`123`：

```
tom.fred.bob.sammy=123
```

> 指定的覆盖值始终是字面值。它们不会被翻译成bean引用。当XML bean定义中的原始值指定bean引用时，此约定也适用。

使用Spring 2.5中引入的`context`命名空间，可以使用专用配置元素配置属性覆盖，如以下示例所示：

```
<context:property-override location="classpath:override.properties"/>
```

#### 1.8.3 使用`FactoryBean`自定义实例化逻辑

您可以为本身为工厂的对象实现`org.springframework.beans.factory.FactoryBean`接口。

`FactoryBean`接口是Spring IoC容器实例化逻辑的可插拔点。如果您有更复杂的初始化代码，这些代码在Java中表达得更好，而不是（可能）冗长的XML，您可以创建自己的`FactoryBean`，在该类中编写复杂的初始化，然后将自定义的`FactoryBean`插入容器。

`FactoryBean` 接口体用了三个方法：

- `Object getObject()`: 返回此工厂创建的对象的实例。可以共享实例，具体取决于此工厂是返回单例还是原型。
- `boolean isSingleton()`: 如果`FactoryBean`返回单例，则返回`true`，否则返回`false`。
- `Class getObjectType()`: 如果事先不知道类型，则返回`getObject()`方法返回的对象类型或`null`。

`FactoryBean`概念和接口在Spring Framework中的许多地方使用。`FactoryBean`接口的50多个实现随Spring一起提供。

当你需要向容器请求一个实际的`FactoryBean`实例本身而不是它生成的bean时，在调用`ApplicationContext`的`getBean()`方法时，用`＆`符号作为bean的`id`的前缀。因此，对于具有`id`为`myBean`的给定`FactoryBean`，在容器上调用`getBean("myBean")`返回`FactoryBean`的产品，而调用`getBean("&myBean")`返回 `FactoryBean`实例本身。

### 1.9 基于注解的容器配置

> 配置 Spring ，注解还是 XML 更好？
>
> 基于注解的配置的引入引发了这种方法是否比XML“更好”的问题。简短的回答是“看情况。”完整的答案是每种方法都有其优点和缺点，通常，由开发人员决定哪种策略更适合他们。由于它们的定义方式，注解在其声明中提供了大量上下文，从而导致更短更简洁的配置。但是，XML擅长在不触及源代码或重新编译它们的情况下连接组件。一些开发人员更喜欢将布线靠近源，而另一些开发人员则认为注解类不再是POJO，而且配置变得分散且难以控制。
>
> 无论选择如何，Spring都可以兼顾两种风格，甚至可以将它们混合在一起。值得指出的是，通过其 [JavaConfig](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java) 选项，Spring允许以非侵入方式使用注解，而无需触及目标组件源代码，并且在工具方面， [Spring Tool Suite](https://spring.io/tools/sts) 支持所有配置样式。

基于注解的配置提供了XML设置的替代方案，该配置依赖于字节码元数据来连接组件而不是角括号声明。开发人员不是使用XML来描述bean连接，而是通过在相关的类，方法或字段声明上使用注解将配置移动到组件类本身。如示例中所述： [Example: The `RequiredAnnotationBeanPostProcessor`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-extension-bpp-examples-rabpp)，将`BeanPostProcessor`与注解结合使用是扩展Spring IoC容器的常用方法。例如，Spring 2.0引入了使用 [`@Required`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-required-annotation) 注解强制执行所需属性的可能性。Spring 2.5使得有可能采用相同的通用方法来驱动Spring的依赖注入。从本质上讲，`@Autowired`注释提供的功能与 [自动装配协作者](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-autowire) 中描述的相同，但具有更细粒度的控制和更广泛的适用性。Spring 2.5还增加了对JSR-250注解的支持，例如`@PostConstruct`和`@PreDestroy`。Spring 3.0增加了对`javax.inject`包中包含的JSR-330（Java的依赖注入）注解的支持，例如`@Inject`和`@Named`。有关这些注解的详细信息，请参阅 [相关章节](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-standard-annotations) 。

> 注解注入在XML注入之前执行。因此，XML配置会覆盖通过这两种方法连接的属性的注解。

与往常一样，您可以将它们注册为单独的bean定义，但也可以通过在基于XML的Spring配置中包含以下标记来隐式注册它们（请注意包含上下文命名空间）：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

</beans>
````



（ 隐式注册的后处理器包括 [`AutowiredAnnotationBeanPostProcessor`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/beans/factory/annotation/AutowiredAnnotationBeanPostProcessor.html),[`CommonAnnotationBeanPostProcessor`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/context/annotation/CommonAnnotationBeanPostProcessor.html), [`PersistenceAnnotationBeanPostProcessor`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/orm/jpa/support/PersistenceAnnotationBeanPostProcessor.html), 以及前面提到的 [`RequiredAnnotationBeanPostProcessor`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/beans/factory/annotation/RequiredAnnotationBeanPostProcessor.html) ）

> `<context:annotation-config/>` 仅仅查找它被定义于其中的应用上下文中的beans上的注解。这就意味着，如果你将 `<context:annotation-config/>` 放进`DispatcherServlet`的 `WebApplicationContext` 中，它将仅仅检查你的控制器中的的 `@Autowired` beans，而不管你的服务类。参考 [The DispatcherServlet](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/web.html#mvc-servlet) 获取更多信息。

#### 1.9.1 `@Required`

`@Required` 注解应用于bean属性设定器方法，如下面例子所示：

```java
public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Required
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    // ...
}
```

此注解指示必须在配置时通过bean定义中的显式属性值或通过自动装配填充受影响的bean属性。如果尚未填充受影响的bean属性，则容器将引发异常。这允许急切和显式的失败，避免以后出现`NullPointerException`实例等。我们仍然建议您将断言放入bean类本身（例如，放进`init`方法）。即使您在容器外部使用类，这样做也会强制保证那些必需的引用和值。

> `@Required`注解从Spring Framework 5.1开始正式弃用，转而支持使用构造函数注入所需的设置（或者自定义实现`InitializingBean.afterPropertiesSet()`以及bean属性setter方法）。

#### 1.9.2 使用 `@Autowired`

> 在本节所包含的示例中，可以使用JSR 330的`@Inject`注解代替Spring的`@Autowired`注解。有关详细信息，请参见 [此处](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-standard-annotations) 。

你可以将`@Autowired` 注解用在构造器上面，如下面例子所示：

```java
public class MovieRecommender {

    private final CustomerPreferenceDao customerPreferenceDao;

    @Autowired
    public MovieRecommender(CustomerPreferenceDao customerPreferenceDao) {
        this.customerPreferenceDao = customerPreferenceDao;
    }

    // ...
}
```

> 从Spring Framework 4.3开始，如果目标bean只在开头定义了一个构造函数，则不再需要在这样的构造函数上使用`@Autowired`注解。但是，如果有几个构造器可用，则必须注解至少一个构造器以告知容器使用哪一个。

你也可以将 `@Autowired` 注解应用于“传统的”设定器方法，如下面例子所示：

```java
public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Autowired
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    // ...
}
```

您还可以将注释应用于具有任意名称和多个参数的方法，如以下示例所示：

```java
public class MovieRecommender {

    private MovieCatalog movieCatalog;

    private CustomerPreferenceDao customerPreferenceDao;

    @Autowired
    public void prepare(MovieCatalog movieCatalog,
            CustomerPreferenceDao customerPreferenceDao) {
        this.movieCatalog = movieCatalog;
        this.customerPreferenceDao = customerPreferenceDao;
    }

    // ...
}
```

您也可以将`@Autowired`应用于字段，甚至可以将其与构造函数混合使用，如下例所示：

```java
public class MovieRecommender {

    private final CustomerPreferenceDao customerPreferenceDao;

    @Autowired
    private MovieCatalog movieCatalog;

    @Autowired
    public MovieRecommender(CustomerPreferenceDao customerPreferenceDao) {
        this.customerPreferenceDao = customerPreferenceDao;
    }

    // ...
}
```

> 确保您的目标组件（例如，`MovieCatalog`或`CustomerPreferenceDao`）始终按照用于`@Autowired`注解标识的注入点的类型声明。否则，由于在运行时未找到类型匹配，注入可能会失败。
>
> 对于通过类路径扫描找到的XML定义的bean或组件类，容器通常预先知道具体类型。但是，对于`@Bean`工厂方法，您需要确保声明的返回类型具有足够的表现力。对于实现多个接口的组件或可能由其实现类型引用的组件，请考虑在工厂方法上声明最具体的返回类型（至少与引用bean的注入点所需的特定类型一致）。

您还可以通过将注解添加到需要该类型数组的字段或方法，从`ApplicationContext`提供特定类型的所有bean，如以下示例所示：

```java
public class MovieRecommender {

    @Autowired
    private MovieCatalog[] movieCatalogs;

    // ...
}
```

这同样适用于类型化集合，如以下示例所示：

```java
public class MovieRecommender {

    private Set<MovieCatalog> movieCatalogs;

    @Autowired
    public void setMovieCatalogs(Set<MovieCatalog> movieCatalogs) {
        this.movieCatalogs = movieCatalogs;
    }

    // ...
}
```

> 你的目标 beans 可以实现 `org.springframework.core.Ordered` 接口，或者使用 `@Order` 或者标准的 `@Priority` 注解，如果你希望数组或者列表中的元素按照特定顺序排序。否则，它们的顺序遵循容器中相应目标 bean 定义的注册顺序。
>
> 您可以在目标类级别和`@Bean`方法上声明`@Order`注释，可能是通过单个bean定义（在多个定义使用相同bean类的情况下）。`@Order`值可能影响注入点的优先级，但要注意它们不会影响单例启动顺序，这是由依赖关系和`@DependsOn`声明确定的正交关注点。
>
> 请注意，标准的`javax.annotation.Priority`注释在`@Bean`级别不可用，因为它无法在方法上声明。它的语义可以通过`@Order`值与`@Primary`在每个类型的单个bean上进行建模。

只要预期的键类型是`String`，即使是类型化的`Map`实例也可以自动装配。`Map`值包含所有期望类型的bean，并且键包含相应的bean名称，如以下示例所示：

```java
public class MovieRecommender {

    private Map<String, MovieCatalog> movieCatalogs;

    @Autowired
    public void setMovieCatalogs(Map<String, MovieCatalog> movieCatalogs) {
        this.movieCatalogs = movieCatalogs;
    }

    // ...
}
```

默认情况下，当给定注入点没有匹配的候选bean时，自动装配失败。对于声明的数组，集合或映射，至少需要一个匹配元素。

默认行为是将带注解的方法和字段视为指示所需的依赖项。您可以更改此行为，如以下示例所示，通过将其标记为非必需，使框架能够来跳过不可满足的注入点：

```java
public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Autowired(required = false)
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    // ...
}
```

如果它的依赖项（或多个参数情况下的依赖项之一）不可用，则根本不会调用该非必需的方法。在这种情况下，根本不会填充非必填字段，保留其默认值。

注入构造函数和工厂方法参数是一种特殊情况，因为·@Autowired·上的'required'标志具有一些不同的含义，因为Spring的构造函数解析算法可能涉及多个构造函数。默认情况下确实需要构造函数和工厂方法参数，但在单构造函数场景中有一些特殊规则，例如，如果没有匹配的bean可用，则多元素注入点（数组，集合，映射）解析为空实例。这允许一种通用的实现模式，其中所有依赖关系都可以在唯一的多参数构造函数中声明，例如， 声明为没有`@Autowired`注解的单个公共构造函数。

> 每个类中只有一个注解修饰的构造器可以被标记为必需的，但是多个非必需的构造器都可以被注解修饰。这种情况下，每个构造器都作为候选，Spring 会使用其中依赖被满足的最贪婪的那个 - 也就是说，那个参数最多的构造器。构造器解析算法与包含重载构造器的非注解类相同，只是将候选构造器范围限制为被注解修饰的构造器。
>
> 在 setter 方法上推荐使用`@Autowired`注解的`required`属性而不是`@Required`注解。`required`属性表示该属性对自动绑定是非必需的。如果不能被自动绑定，则该属性就会被忽略。而`@Required`则强制该属性必须在容器支持的意义上被设置。如果值没有定义，就会产生相应的异常。

或者，您可以通过Java 8的`java.util.Optional`表达特定依赖项的非必需特性，如以下示例所示：

```java
public class SimpleMovieLister {

    @Autowired
    public void setMovieFinder(Optional<MovieFinder> movieFinder) {
        ...
    }
}
```

从Spring Framework 5.0开始，您还可以使用`@Nullable`注解（任何包中的任何类型 - 例如，来自JSR-305的`javax.annotation.Nullable`）：

```java
public class SimpleMovieLister {

    @Autowired
    public void setMovieFinder(@Nullable MovieFinder movieFinder) {
        ...
    }
}
```

您还可以将`@Autowired`用于众所周知的可解析依赖项的接口：`BeanFactory`，`ApplicationContext`，`Environment`，`ResourceLoader`，`ApplicationEventPublisher`和`MessageSource`。这些接口及其扩展接口（如`ConfigurableApplicationContext`或`ResourcePatternResolver`）将自动解析，无需特殊设置。以下示例自动装配`ApplicationContext`对象：

```java
public class MovieRecommender {

    @Autowired
    private ApplicationContext context;

    public MovieRecommender() {
    }

    // ...
}
```

> `@Autowired`，`@Inject`，`@Value`和`@Resource`注解由Spring `BeanPostProcessor`实现处理。这意味着您无法在自己的`BeanPostProcessor`或`BeanFactoryPostProcessor`类型（如果有）中应用这些注解。必须使用XML或Spring `@Bean`方法显式地“连接”这些类型。

#### 1.9.3 使用`@Primary`微调基于注释的自动装配

由于按类型自动装配可能会导致多个候选者，因此通常需要对选择过程进行更多控制。实现这一目标的一种方法是使用Spring的`@Primary`注解。`@Primary`指示当多个bean可以自动装配到单值依赖项时，应该优先选择特定的bean。如果候选者中只存在一个主bean，则它将成为自动装配的值。

请考虑以下配置，将`firstMovieCatalog`定义为主要`MovieCatalog`：

```java
@Configuration
public class MovieConfiguration {

    @Bean
    @Primary
    public MovieCatalog firstMovieCatalog() { ... }

    @Bean
    public MovieCatalog secondMovieCatalog() { ... }

    // ...
}
```

使用上述配置，以下`MovieRecommender`将与`firstMovieCatalog`一起自动装配：

```java
public class MovieRecommender {

    @Autowired
    private MovieCatalog movieCatalog;

    // ...
}
```

相应的bean定义如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

    <bean class="example.SimpleMovieCatalog" primary="true">
        <!-- inject any dependencies required by this bean -->
    </bean>

    <bean class="example.SimpleMovieCatalog">
        <!-- inject any dependencies required by this bean -->
    </bean>

    <bean id="movieRecommender" class="example.MovieRecommender"/>

</beans>
```

#### 1.9.4 使用限定符微调基于注解的自动装配

@Primary是一种有效的方法，可以在按类型使用自动装配的情况下确定一个主要候选者。当您需要更多控制选择过程时，可以使用Spring的`@Qualifier`注解。您可以将限定符值与特定参数相关联，缩小类型匹配集，以便为每个参数选择特定的bean。在最简单的情况下，这可以是一个简单的描述性值，如以下示例所示：

```java
public class MovieRecommender {

    @Autowired
    @Qualifier("main")
    private MovieCatalog movieCatalog;

    // ...
}
```

您还可以在各个构造函数参数或方法参数上指定`@Qualifier`注释，如以下示例所示：

```java
public class MovieRecommender {

    private MovieCatalog movieCatalog;

    private CustomerPreferenceDao customerPreferenceDao;

    @Autowired
    public void prepare(@Qualifier("main") MovieCatalog movieCatalog,
            CustomerPreferenceDao customerPreferenceDao) {
        this.movieCatalog = movieCatalog;
        this.customerPreferenceDao = customerPreferenceDao;
    }

    // ...
}
```

下面的例子展示了相应的 bean 定义：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

    <bean class="example.SimpleMovieCatalog">
        <qualifier value="main"/> <!-- The bean with the main qualifier value is wired with the constructor argument that is qualified with the same value. -->

        <!-- inject any dependencies required by this bean -->
    </bean>

    <bean class="example.SimpleMovieCatalog">
        <qualifier value="action"/> <!-- The bean with the action qualifier value is wired with the constructor argument that is qualified with the same value. -->

        <!-- inject any dependencies required by this bean -->
    </bean>

    <bean id="movieRecommender" class="example.MovieRecommender"/>

</beans>
```

对于回退匹配，bean名称被视为默认限定符值。因此，您可以使用id而不是嵌套限定符元素定义bean，从而得到相同的匹配结果。但是，虽然您可以使用此约定来按名称引用特定bean，但`@Autowired`基本上是关于具有可选语义限定符的类型驱动注入。这意味着即使使用bean名称回退，限定符值在类型匹配集中也总是具有缩窄范围的语义。它们在语义上不表示对唯一bean `id`的引用。良好的限定符值是`main`或`EMEA`或`persistent`，表示独立于bean `id`的特定组件的特征，可以在匿名bean定义（例如前面示例中的定义）的情况下自动生成。

限定符也适用于类型化集合，如前所述 - 例如， `Set<MovieCatalog>`。在这种情况下，根据声明的限定符，所有匹配的bean都作为集合注入。这意味着限定符不必是唯一的。相反，它们构成了过滤标准。例如，您可以使用相同的限定符值“action”定义多个`MovieCatalog` bean，所有这些bean都注入到使用`@Qualifier("action")`注解修饰的 `Set<MovieCatalog>` 中。

> 在类型匹配候选项中，根据目标bean名称选择限定符值，在注入点不需要`@Qualifier`注解。 如果没有其他解析指示符（例如限定符或主要标记），则对于非唯一依赖性情况，Spring会将注入点名称（即字段名称或参数名称）与目标bean名称进行匹配，然后选择同名的候选人，如果有的话。
>
> 也就是说，如果您打算用名称表达注解驱动的注入，请不要主要使用`@Autowired`，即使它能够在类型匹配候选项中通过bean名称进行选择。相反，使用JSR-250 `@Resource`注解，它在语义上定义为通过其唯一名称标识特定目标组件，声明的类型与匹配过程无关。`@Autowired`具有相当不同的语义：在按类型选择候选bean之后，仅在那些类型选择的候选项中考虑指定的 `String` 限定符值（例如，将 `account` 限定符与标记有相同限定符标签的bean匹配）。
>
> 对于自身定义为集合，`Map`或数组类型的bean，`@ Resource`是一个很好的解决方案，通过唯一名称引用特定的集合或数组bean。也就是说，从4.3版本开始，只要元素类型信息保存在`@Bean`返回类型签名或集合继承层次结构中，您就可以通过Spring的`@Autowired`类型匹配算法匹配`Map`和数组类型。在这种情况下，您可以使用限定符值在相同类型的集合中进行选择，如上一段所述。
>
> 从4.3开始，`@Autowired`还会考虑自引用注入（即，引用回头指向到当前注入的bean）。请注意，自我注入是一种后备。对其他组件的常规依赖性始终具有优先权。从这个意义上说，自我引用并不参与常规的候选人选择，因此特殊情况永远不会是主要的。相反，它们总是最低优先级。在实践中，您应该仅使用自引用作为最后的手段（例如，通过bean的事务代理调用同一实例上的其他方法）。考虑在这种情况下将受影响的方法分解为单独的委托bean。或者，您可以使用`@Resource`，它可以通过其唯一名称获取当前bean的代理。
>
> `@Autowired`适用于字段，构造函数和多参数方法，允许在参数级别缩小限定符注解选择范围。相比之下，`@Resource`仅支持字段和具有单个参数的bean属性setter方法。因此，如果注射目标是构造函数或多参数方法，则应该使用限定符。

你可以创建自定义限定器注解。想要这样做，定义一个注解并在其中提供`@Qualifier`注解，如下面例子所示：

````java
@Target({ElementType.FIELD, ElementType.PARAMETER})
@Retention(RetentionPolicy.RUNTIME)
@Qualifier
public @interface Genre {

    String value();
}
````

然后你可以在自动装配的字段和参数上使用这个限定器，如下面例子所示：

````java
public class MovieRecommender {
  
  @Autowired
  @Genre("Action")
  private MovieCatalog actionCatalog;
  
  private MovieCatalog comedyCatalog;
  
  @Autowired
  public void setComedyCatalog(@Genre("Comedy") MovieCatalog comedyCatalog) {
    this.comedyCatalog = comedyCatalog;
  }
  
  //...
}
````

接下来，你可以提供有关候选者 bean 定义的信息。你可以添加`<qualifier/>`标签作为`<bean/>`标签的子元素来指定`type`和`value`来匹配你自定义的限定器注解。该类型匹配到注解的全限定类型名。另外，如果不存在名称冲突的风险，你也可以使用简单类名。下面的例子展示了这两种方式：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

    <bean class="example.SimpleMovieCatalog">
        <qualifier type="Genre" value="Action"/>
        <!-- inject any dependencies required by this bean -->
    </bean>

    <bean class="example.SimpleMovieCatalog">
        <qualifier type="example.Genre" value="Comedy"/>
        <!-- inject any dependencies required by this bean -->
    </bean>

    <bean id="movieRecommender" class="example.MovieRecommender"/>

</beans>
````



在 [Classpath Scanning and Managed Components](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-classpath-scanning) 中，你可以看到通过基于注解额配置提供上面XML中的限定器元数据的方法。具体来说，请参考 [Providing Qualifier Metadata with Annotations](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-scanning-qualifiers) 。

某些情况下，使用不指定值的注解就足够了。这在注解支持更通用的场景且注解可以用于多种不同类型的依赖时很有用。比如，你可以提供一个离线目录可以在网络连接不可用情况下使用。首先，定义一个简答的注解如下：

````java
@Target({ElementType.FIELD, ElementType.PARAMETER})
@Retention(RetentionPolicy.RUNTIME)
@Qualifier
public @interface Offline {

}
````

然后将此注解添加到自动装配的字段或者属性上，如下例子所示：

````java
public class MovieRecommender {
  
  @Autowired
  @Offline
  private MovieCatalog offlineCatalog;
  
  //...
}
````

现在，该 bean 定义只需要一个限定器`type`，如下面例子所示：

````xml
<bean class="example.SimpleMovieCatalog">
    <qualifier type="Offline"/> 
    <!-- inject any dependencies required by this bean -->
</bean>
````

你也可以自定义接受命名属性的自定义限定器注解，而不仅仅接受`value`属性。如果多个属性值被指定到一个自动装配的字段或者参数上，bean定义必须匹配所有这些属性值才能为认为是自动装配的候选者。作为示例，考虑下面的注解定义：

```java
@Target({ElementType.FIELD, ElementType.PARAMETER})
@Retention(RetentionPolicy.RUNTIME)
@Qualifier
public @interface MovieQualifier {

    String genre();

    Format format();
}
```

`Format` 是一个枚举，定义如下：

```java
public enum Format {
    VHS, DVD, BLURAY
}
```

要自动装配的字段使用自定义限定符进行注解，并包含两个属性的值：`genre`和`format`，如以下示例所示：

```java
public class MovieRecommender {

    @Autowired
    @MovieQualifier(format=Format.VHS, genre="Action")
    private MovieCatalog actionVhsCatalog;

    @Autowired
    @MovieQualifier(format=Format.VHS, genre="Comedy")
    private MovieCatalog comedyVhsCatalog;

    @Autowired
    @MovieQualifier(format=Format.DVD, genre="Action")
    private MovieCatalog actionDvdCatalog;

    @Autowired
    @MovieQualifier(format=Format.BLURAY, genre="Comedy")
    private MovieCatalog comedyBluRayCatalog;

    // ...
}
```

最后，bean定义应包含匹配的限定符值。此示例还演示了您可以使用bean元属性而不是`<qualifier/>`元素。如果可用，`<qualifier/>`元素及其属性优先，但是如果不存在这样的限定符，则自动装配机制将回退到`<meta/>`标签内提供的值，如以下示例中的最后两个bean定义：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:annotation-config/>

    <bean class="example.SimpleMovieCatalog">
        <qualifier type="MovieQualifier">
            <attribute key="format" value="VHS"/>
            <attribute key="genre" value="Action"/>
        </qualifier>
        <!-- inject any dependencies required by this bean -->
    </bean>

    <bean class="example.SimpleMovieCatalog">
        <qualifier type="MovieQualifier">
            <attribute key="format" value="VHS"/>
            <attribute key="genre" value="Comedy"/>
        </qualifier>
        <!-- inject any dependencies required by this bean -->
    </bean>

    <bean class="example.SimpleMovieCatalog">
        <meta key="format" value="DVD"/>
        <meta key="genre" value="Action"/>
        <!-- inject any dependencies required by this bean -->
    </bean>

    <bean class="example.SimpleMovieCatalog">
        <meta key="format" value="BLURAY"/>
        <meta key="genre" value="Comedy"/>
        <!-- inject any dependencies required by this bean -->
    </bean>

</beans>
```

#### 1.9.5 使用泛型作为自动装配限定符

除了`@Qualifier`注解之外，您还可以使用Java泛型类型作为隐式的限定形式。例如，假设您具有以下配置：

```java
@Configuration
public class MyConfiguration {

    @Bean
    public StringStore stringStore() {
        return new StringStore();
    }

    @Bean
    public IntegerStore integerStore() {
        return new IntegerStore();
    }
}
```

假设上面的bean实现了一个通用接口（即`Store<String>`和`Store<Integer>`），您可以`@Autowired`该`Store`接口，并将泛型用作限定符，如下例所示：

```java
@Autowired
private Store<String> s1; // <String> qualifier, injects the stringStore bean

@Autowired
private Store<Integer> s2; // <Integer> qualifier, injects the integerStore bean
```

通用限定符也适用于自动装配列表，`Map`实例和数组。以下示例自动装配泛型`List`：

```java
// Inject all Store beans as long as they have an <Integer> generic
// Store<String> beans will not appear in this list
@Autowired
private List<Store<Integer>> s;
```

#### 1.9.6 使用 `CustomAutowireConfigurer`

[`CustomAutowireConfigurer`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/beans/factory/annotation/CustomAutowireConfigurer.html) 是一个 `BeanFactoryPostProcessor` ，允许你注册你自己定义的限定器注解类型，即使它们没有用 Spring 的 `@Qualifier` 注解修饰。下面的例子展示了如何使用 `CustomAutowireConfigurer`：

```xml
<bean id="customAutowireConfigurer"
        class="org.springframework.beans.factory.annotation.CustomAutowireConfigurer">
    <property name="customQualifierTypes">
        <set>
            <value>example.CustomQualifier</value>
        </set>
    </property>
</bean>
```

`AutowireCandidateResolver` 确定自动装配候选者，通过：

- 每个 bean 定义的 `autowire-candidate` 值
- `<beans/>` 元素上所有可用的 `default-autowire-candidates` 模式
- 存在`@Qualifier`注解以及使用`CustomAutowireConfigurer`注册的任何自定义注解

当多个bean有资格作为autowire候选者时，“primary”的确定如下：如果候选者中只有一个bean定义的`primary`属性设置为`true`，则选择它。

#### 1.9.7 使用 `@Resource` 注入

Spring还通过对字段或bean属性setter方法使用JSR-250 `@Resource`注解（`javax.annotation.Resource`）来支持注入。这是Java EE中的常见模式：例如，在JSF管理的bean和JAX-WS端点中。Spring也支持Spring管理对象的这种模式。

`@Resource`采用name属性。默认情况下，Spring将该值解释为要注入的bean名称。换句话说，它遵循按名称语义，如以下示例所示：

```java
public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Resource(name="myMovieFinder") 
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }
}
```

如果未明确指定名称，则默认名称是从字段名称或setter方法派生的。如果是字段，则采用字段名称。在setter方法的情况下，它采用bean属性名称。下面的例子将把名为`movieFinder`的bean注入其setter方法：

```java
public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Resource
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }
}
```

> 随注解提供的名称由`ApplicationContext`解析为bean名称，`CommonAnnotationBeanPostProcessor`知道该名称。如果您显式配置Spring的 [`SimpleJndiBeanFactory`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/jndi/support/SimpleJndiBeanFactory.html) ，则可以通过JNDI解析名称。但是，我们建议您依赖于默认行为并使用Spring的JNDI查找功能来保留间接级别。

在没有指定显式名称的`@Resource`用法的独有情况下，类似于`@Autowired`，`@Resource`找到主要类型匹配而不是特定的命名bean，并解析众所周知的可解析依赖项：`BeanFactory`，`ApplicationContext`，`ResourceLoader`，`ApplicationEventPublisher`和 `MessageSource`接口。

因此，在以下示例中，`customerPreferenceDao`字段首先查找名为“customerPreferenceDao”的bean，然后返回到`CustomerPreferenceDao`类型的主类型匹配：

```java
public class MovieRecommender {

    @Resource
    private CustomerPreferenceDao customerPreferenceDao;

    @Resource
    private ApplicationContext context; //	The context field is injected based on the known resolvable dependency type: ApplicationContext.


    public MovieRecommender() {
    }

    // ...
}
```

#### 1.9.8 使用 `@PostConstruct` 和 `@PreDestroy`

`CommonAnnotationBeanPostProcessor`不仅识别`@Resource`注解，还识别JSR-250生命周期注解：`javax.annotation.PostConstruct`和`javax.annotation.PreDestroy`。在Spring 2.5中引入，对这些注解的支持提供了 [initialization callbacks](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-initializingbean) 和 [destruction callbacks](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-disposablebean) 中描述的生命周期回调机制的替代方法。如果`CommonAnnotationBeanPostProcessor`在Spring `ApplicationContext`中注册，则在生命周期的同一点调用承载这些注释之一的方法，将作为相应的Spring生命周期接口方法或显式声明的回调方法。在以下示例中，缓存在初始化时预填充并在销毁时清除：

```java
public class CachingMovieLister {

    @PostConstruct
    public void populateMovieCache() {
        // populates the movie cache upon initialization...
    }

    @PreDestroy
    public void clearMovieCache() {
        // clears the movie cache upon destruction...
    }
}
```

有关组合各种生命周期机制的效果的详细信息，请参阅 [Combining Lifecycle Mechanisms](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-combined-effects) 。

> 与`@Resource`一样，`@PostConstruct`和`@PreDestroy`注解类型是JDK 6到8的标准Java库的一部分。但是，整个`javax.annotation`包与JDK 9中的核心Java模块分离，最终在JDK 11中删除。如果需要，现在需要通过Maven Central获取`javax.annotation-api`组件，只需像任何其他库一样添加到应用程序的类路径中。

### 1.10 类路径扫描和受管理的组件

本章中的大多数示例都使用XML来指定在Spring容器中生成每个`BeanDefinition`的配置元数据。上一节（ [基于注解的容器配置](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-annotation-config) ）演示了如何通过源码层面的注解提供大量配置元数据。但是，即使在这些示例中，“基本”bean定义也在XML文件中显式定义，而注解仅驱动依赖项注入。本节介绍通过扫描类路径隐式检测候选组件的选项。候选组件是与筛选条件匹配的类，并且具有向容器注册的相应bean定义。这消除了使用XML执行bean注册的需要。相反，您可以使用注解（例如，`@Component`），AspectJ类型表达式或您自己的自定义筛选条件来选择哪些类具有向容器注册的bean定义。

> 从Spring 3.0开始，Spring JavaConfig项目提供的许多功能都是核心Spring Framework的一部分。这允许您使用Java类而不是使用传统的XML文件来定义bean。有关如何使用这些新功能的示例，请查看`@Configuration`，`@Both`，`@Import`和`@DependsOn`注解。

#### 1.10.1 `@Component` 和其它构造型注解

`@Repository` 注解是任何满足存储仓库（也被称为数据访问对象，DAO）的角色或者构造的所有类的标记。这个标记的一种使用场景就是自动异常转换，在 [Exception Translation](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/data-access.html#orm-exception-translation) 中描述。

Spring提供了进一步的构造型注解：`@Component`，`@Service`和`@Controller`。`@Component`是任何Spring管理组件的通用构造型注解。`@Repository`，`@Service`和`@Controller`是`@Component`的特殊化，用于更具体的情况（分别用在持久性，服务和表示层中）。因此，您可以使用`@Component`注解组件类，但是，通过使用`@Repository`，`@Service`或`@Controller`注解它们，您的类将更适合通过工具处理或与切面关联。例如，这些构造型注解成为切入点的理想目标。`@Repository`，`@Service`和`@Controller`还可以在Spring Framework的未来版本中携带其他语义。因此，如果您选择在服务层使用`@Component`或`@Service`，`@Service`显然是更好的选择。同样，如前所述，已经支持`@Repository`作为持久层中自动异常转换的标记。

#### 1.10.2 使用元注解和组合注解

Spring提供的许多注解都可以在您自己的代码中用作元注解。元注解是可以应用于另一个注解的注解。例如，前面提到的`@Service`注解是使用`@Component`进行元注解的，如下例所示：

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Component //The Component causes @Service to be treated in the same way as @Component.
public @interface Service {

    // ....
}
```

您还可以组合元注解来创建“组合注解”。例如，Spring MVC的`@RestController`注解由`@Controller`和`@ResponseBody`组成。

此外，组合注解可以选择从元注解重新声明属性以允许自定义。当您只想公开元注解属性的子集时，这可能特别有用。例如，Spring的`@SessionScope`注解将作用域名称硬编码为 `session` ，但仍允许自定义`proxyMode`。以下清单显示了`SessionScope`注解的定义：

```java
@Target({ElementType.TYPE, ElementType.METHOD})
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Scope(WebApplicationContext.SCOPE_SESSION)
public @interface SessionScope {

    /**
     * Alias for {@link Scope#proxyMode}.
     * <p>Defaults to {@link ScopedProxyMode#TARGET_CLASS}.
     */
    @AliasFor(annotation = Scope.class)
    ScopedProxyMode proxyMode() default ScopedProxyMode.TARGET_CLASS;

}
```

然后，您可以使用`@SessionScope`而不声明`proxyMode`，如下所示：

```java
@Service
@SessionScope
public class SessionScopedService {
    // ...
}
```

您还可以覆盖`proxyMode`的值，如以下示例所示：

```java
@Service
@SessionScope(proxyMode = ScopedProxyMode.INTERFACES)
public class SessionScopedUserService implements UserService {
    // ...
}
```

有关更多详细信息，请参阅 [Spring Annotation Programming Model](https://github.com/spring-projects/spring-framework/wiki/Spring-Annotation-Programming-Model) wiki页面。

#### 1.10.3 自动探测类并注册 Bean 定义

Spring可以自动检测构造型类，并使用`ApplicationContext`注册相应的`BeanDefinition`实例。例如，以下两个类符合此类自动检测的条件：

```java
@Service
public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Autowired
    public SimpleMovieLister(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }
}
```

```java
@Repository
public class JpaMovieFinder implements MovieFinder {
    // implementation elided for clarity
}
```

要自动检测这些类并注册相应的bean，需要将`@ComponentScan`添加到`@Configurationclass`，其中`basePackages`属性值是两个类的公共父包。（或者，您可以指定包含每个类的父包的逗号或分号或空格分隔列表。）

```java
@Configuration
@ComponentScan(basePackages = "org.example")
public class AppConfig  {
    ...
}
```

> 简介起见，上面的例子可以使用注解的`value`属性，也就是说，`@ComponentScan("org.example")` 。

下面是使用 XML 的形式：

````xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        https://www.springframework.org/schema/context/spring-context.xsd">

    <context:component-scan base-package="org.example"/>

</beans>
````

> 使用`<context:component-scan>`隐式启用`<context:annotation-config>`功能。通常在使用`<context:component-scan>`时不需要包含`<context:annotation-config>`元素。

> 类路径包扫描需要相应的目录实体存在于类路径上。当你使用 Ant 构建 JARs 文件时，请确保你没有开启 JAR 任务的“仅文件”开关。同时，在某些环境下，基于安全策略考虑，类路径的目录可以不向外暴露，比如，JDK 1.7.0_45 或者更高版本（需要清单中的“Trusted-Library”设置，参考 <https://stackoverflow.com/questions/19394570/java-jre-7u45-breaks-classloader-getresources> ）之上的独立应用。
>
> 在 JDK 9 的模块路径（Jigsaw）上，Spring 的类路径扫描通常可以正常工作。不过，请确保你的组件类都输出在了`module-info`描述器中。如果你希望 Spring 调用你的类中的非公共成员，请确保它们是“开放的”（也就是说，在你的`module-info`描述器中，它们使用`opens`声明而不是`exports`声明。）

此外，使用`component-scan`元素时，将隐式包含`AutowiredAnnotationBeanPostProcessor`和`CommonAnnotationBeanPostProcessor`。这意味着这两个组件是自动检测并连接在一起的 - 所有这些都没有在XML中提供任何bean配置元数据。

> 您可以通过包含值为`false`的`annotation-config`属性来禁用`AutowiredAnnotationBeanPostProcessor`和`CommonAnnotationBeanPostProcessor`的注册。

#### 1.10.4 使用过滤器定制组件扫描

默认情况下，被注解`@Component`，`@Repository`，`@Service`，`@Controller` 或者你自定义的注解（本身被`@Component`修饰）修饰的类就是自动扫描探测的候选组件。不过，你可以修改和扩展这种行为，通过应用自定义过滤器。将它们添加为`@ComponentScan`注解的`include-filters`或者`excludeFilters`参数（或者作为`component-scan`元素的`include-filter`或者`exclude-filter`子元素）。每个过滤器元素都需要`type`和`expression`属性。下表描述了过滤器选项：

| Filter Type          | Example Expression           | Description                              |
| -------------------- | ---------------------------- | ---------------------------------------- |
| annotation (default) | `org.example.SomeAnnotation` | 要在目标组件中的类型级别出现的注解。                       |
| assignable           | `org.example.SomeClass`      | 目标组件可分配给（扩展或实现）的类（或接口）。                  |
| aspectj              | `org.example..*Service+`     | 要由目标组件匹配的AspectJ类型表达式。                   |
| regex                | `org\.example\.Default.*`    | 要由目标组件类名匹配的正则表达式。                        |
| custom               | `org.example.MyTypeFilter`   | `org.springframework.core.type.TypeFilter`接口的自定义实现。 |

以下示例显示忽略所有`@Repository`注释并使用“存根”存储库的配置：

```java
@Configuration
@ComponentScan(basePackages = "org.example",
        includeFilters = @Filter(type = FilterType.REGEX, pattern = ".*Stub.*Repository"),
        excludeFilters = @Filter(Repository.class))
public class AppConfig {
    ...
}
```

以下清单显示了等效的XML：

```java
<beans>
    <context:component-scan base-package="org.example">
        <context:include-filter type="regex"
                expression=".*Stub.*Repository"/>
        <context:exclude-filter type="annotation"
                expression="org.springframework.stereotype.Repository"/>
    </context:component-scan>
</beans>
```

> 您还可以通过在注解上设置`useDefaultFilters=false`或通过提供`use-default-filters=“false”`作为`<component-scan />`元素的属性来禁用默认过滤器。实际上，这会禁用自动检测使用`@Component`，`@Repository`，`@Service`，`@Controller`或`@Configuration`注解修饰的类。

#### 1.10.5 在组件中定义 Bean 元数据

Spring组件还可以向容器提供bean定义元数据。您可以在`@Configuration`注解修饰的类中使用用于定义bean元数据的相同`@Bean`注解来执行此操作。以下示例显示了如何执行此操作：

```java
@Component
public class FactoryMethodComponent {

    @Bean
    @Qualifier("public")
    public TestBean publicInstance() {
        return new TestBean("publicInstance");
    }

    public void doWork() {
        // Component method implementation omitted
    }
}
```

上面的类是一个Spring组件，在其 `doWork()` 方法中具有特定于应用程序的代码。但是，它还提供了一个bean定义，它具有引用 `publicInstance()`方法的工厂方法。`@Bean`注解标识工厂方法和其他bean定义属性，例如通过`@Qualifier`注解指定的限定符值。可以指定的其他方法级注解是`@Scope`，`@Lazy`和自定义限定符注解。

> 除了它的组件初始化角色之外，您还可以将`@Lazy`注解放在标有`@Autowired`或`@Inject`的注入点上。在这种情况下，它会导致惰性解析代理注入。

如前所述，支持自动装配的字段和方法，以及对`@Bean`方法的自动装配的额外支持。以下示例显示了如何执行此操作：

```java
@Component
public class FactoryMethodComponent {

    private static int i;

    @Bean
    @Qualifier("public")
    public TestBean publicInstance() {
        return new TestBean("publicInstance");
    }

    // use of a custom qualifier and autowiring of method parameters
    @Bean
    protected TestBean protectedInstance(
            @Qualifier("public") TestBean spouse,
            @Value("#{privateInstance.age}") String country) {
        TestBean tb = new TestBean("protectedInstance", 1);
        tb.setSpouse(spouse);
        tb.setCountry(country);
        return tb;
    }

    @Bean
    private TestBean privateInstance() {
        return new TestBean("privateInstance", i++);
    }

    @Bean
    @RequestScope
    public TestBean requestScopedInstance() {
        return new TestBean("requestScopedInstance", 3);
    }
}
```

该示例将`String`方法参数`country`自动装配到另一个名为`privateInstance`的bean上的`age`属性值。Spring Expression Language元素通过符号`#{<expression>}`定义属性的值。对于`@Value`注释，表达式解析器预先配置为在解析表达式文本时查找bean名称。

从Spring Framework 4.3开始，您还可以声明一个类型为`InjectionPoint`的工厂方法参数（或其更具体的子类：`DependencyDescriptor`）来访问触发创建当前bean的请求注入点。请注意，这仅适用于创建bean实例，而不适用于注入现有实例。因此，此功能对原型作用域的bean最有意义。对于其他作用域，工厂方法只能看到触发在给定作用域中创建新bean实例的注入点（例如，触发创建惰性单例bean的依赖项）。在这种情况下，您可以使用提供的注入点元数据和相关语义。以下示例显示了如何使用`InjectionPoint`：

```java
@Component
public class FactoryMethodComponent {

    @Bean @Scope("prototype")
    public TestBean prototypeInstance(InjectionPoint injectionPoint) {
        return new TestBean("prototypeInstance for " + injectionPoint.getMember());
    }
}
```

常规Spring组件中的`@Bean`方法的处理方式与Spring `@Configuration`类中的处理方式不同。不同之处在于，使用CGLIB不会增强`@Component`类来拦截方法和字段的调用。CGLIB代理是调用`@Configuration`类中的`@Bean`方法中的方法或字段创建对协作对象的bean元数据引用的方法。这些方法不是用普通的Java语义调用的，而是通过容器来提供通常的生命周期管理和Spring bean的代理，即使在通过对`@Bean`方法的编程调用引用其他bean时也是如此。相反，在普通的`@Component`类中调用`@Bean`方法中的方法或字段具有标准的Java语义，没有应用特殊的CGLIB处理或其他约束。

> 您可以将`@Bean`方法声明为`static`，允许在不创建包含配置类实例的情况下调用它们。这在定义后处理器bean（例如，`BeanFactoryPostProcessor`或`BeanPostProcessor`类型）时特别有意义，因为这样的bean在容器生命周期的早期就会初始化，并且应该避免在那时触发配置的其他部分。
>
> 由于技术限制，对静态`@Bean`方法的调用永远不会被容器拦截，甚至在`@Configuration`类中也没有（如本节前面所述）：CGLIB子类化只能覆盖非静态方法。因此，直接调用另一个`@Bean`方法具有标准的Java语义，从而导致直接从工厂方法本身返回一个独立的实例。
>
> `@Bean`方法的Java语言可见性对Spring容器中生成的bean定义没有立即影响。您可以根据需要在非`@Configuration`类中自由声明工厂方法，也可以在任何地方自由声明静态方法。但是，`@Conffiguration`类中的常规`@Bean`方法需要可以覆盖 - 也就是说，它们不能声明为`private`或`final`。
>
> `@Bean`方法也可以在给定组件或配置类的基类上出现，也可以在组件或配置类实现的接口中声明的Java 8默认方法上出现。这使得在编写复杂的配置时具有很大的灵活性，从Spring 4.2开始，甚至可以通过Java 8默认方法实现多重继承。
>
> 最后，单个类可以为同一个bean保存多个`@Bean`方法，作为根据运行时可用依赖项使用的多个工厂方法的安排。这与在其他配置方案中选择“最贪婪”构造函数或工厂方法的算法相同：在构造时选择具有最多可满足依赖项的变体，类似于容器在多个`@Autowired`构造函数之间进行选择的方式。

#### 1.10.6 命名被自动探测的组件

当一个组件被自动探测为扫描过程的一部分时，它的 bean 名称由扫描器所知的`BeanNameGenerator`策略产生。默认地，包含一个名称`value`的任何 Spring 构造型注解（`@Component`, `@Repository`, `@Service`, 和 `@Controller`）则会将该名称提供给相应的 bean 定义。

如果这样的注解不包含名称`value` ，或者是通过其它方式被探测到的组件，比如被自定义过滤器发现的那些组件，默认的 bean 名称产生器将返回首字母小写的非限定类名。比如，如果下面的组件类被探测到，则其 bean 名称将分别是 `myMovieLister` 和 `movieFinderImpl` ：

```java
@Service("myMovieLister")
public class SimpleMovieLister {
    // ...
}
@Repository
public class MovieFinderImpl implements MovieFinder {
    // ...
}
```

> 如果您不想依赖默认的bean命名策略，则可以提供自定义bean命名策略。首先，实现`BeanNameGenerator`接口，并确保包含默认的无参数构造函数。然后，在配置扫描程序时提供完全限定的类名，如以下示例注解和bean定义所示：

```java
@Configuration
@ComponentScan(basePackages = "org.example", nameGenerator = MyNameGenerator.class)
public class AppConfig {
    ...
}
<beans>
    <context:component-scan base-package="org.example"
        name-generator="org.example.MyNameGenerator" />
</beans>
```

作为一般规则，考虑在其他组件可能对其进行显式引用时使用注解指定名称。另一方面，只要容器负责装配，自动生成的名称就足够了。

#### 1.10.7 为被探测到的组件提供作用域

与Spring管理的组件一样，自动检测组件的默认和最常见的作用域是单例。但是，有时您需要一个可由`@Scope`注解指定的不同作用域。您可以在注解中提供作用域的名称，如以下示例所示：

```java
@Scope("prototype")
@Repository
public class MovieFinderImpl implements MovieFinder {
    // ...
}
```

> `@Scope`注解仅在具体bean类（对于带注解的组件）或工厂方法（对于`@Bean`方法）上进行了内省。与XML bean定义相比，没有bean定义继承的概念，类级别的继承层次结构与元数据目的无关。

有关特定于Web应用的作用域范围（如Spring上下文中的“request”或“session”）的详细信息，请参阅请 [Request, Session, Application, and WebSocket Scopes](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-other) 。与这些作用域范围的预构建注解一样，您也可以使用Spring的元注解方法编写自己的作用域范围注解：例如，使用`@Scope("prototype")`进行元注解的自定义注解，可能还会声明自定义作用域代理模式。

> 要为作用域范围解析提供自定义策略而不是依赖基于注解的方法，可以实现`ScopeMetadataResolver`接口。请确保包含默认的无参数构造函数。然后，您可以在配置扫描程序时提供完全限定的类名，如以下注解和bean定义示例显示：

```java
@Configuration
@ComponentScan(basePackages = "org.example", scopeResolver = MyScopeResolver.class)
public class AppConfig {
    ...
}
```

```xml
<beans>
    <context:component-scan base-package="org.example" scope-resolver="org.example.MyScopeResolver"/>
</beans>
```

使用某些非单例作用域时，可能需要为作用域对象生成代理。这种推理在 [Scoped Beans as Dependencies](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-other-injection) 中描述。为此，component-scan元素上提供了scoped-proxy属性。三个可能的值是：`no`，`interfaces`和`targetClass`。例如，以下配置导致标准JDK动态代理：

```java
@Configuration
@ComponentScan(basePackages = "org.example", scopedProxy = ScopedProxyMode.INTERFACES)
public class AppConfig {
    ...
}
<beans>
    <context:component-scan base-package="org.example" scoped-proxy="interfaces"/>
</beans>
```

#### 1.10.8 使用注解提供限定符元数据

在 [使用限定符微调基于注解的自动装配](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-autowired-annotation-qualifiers) 中讨论了`@Qualifier`注解。该部分中的示例演示了在解析自动线候选时使用`@Qualifier`注解和自定义限定符注解来提供细粒度控制。因为这些示例基于XML bean定义，所以通过使用XML中`bean`元素的 `qualifier` 或 `meta` 子元素，在候选bean定义上提供限定符元数据。当依靠类路径扫描来自动检测组件时，可以在候选类上使用类型级注解限定符元数据。以下三个示例演示了此技术：

```java
@Component
@Qualifier("Action")
public class ActionMovieCatalog implements MovieCatalog {
    // ...
}
@Component
@Genre("Action")
public class ActionMovieCatalog implements MovieCatalog {
    // ...
}
@Component
@Offline
public class CachingMovieCatalog implements MovieCatalog {
    // ...
}
```

> 与大多数基于注解的备选方案一样，请记住注解元数据绑定到类定义本身，而XML的使用允许多个相同类型的bean在其限定符元数据中提供变体，因为元数据都是为每个实例提供而不是为每个类提供。

#### 1.10.9 生成候选组件索引

虽然类路径扫描速度非常快，但可以通过在编译时创建候选的静态列表来提高大型应用程序的启动性能。在此模式下，所有作为组件扫描目标的模块都必须使用此机制。

> 您现有的`@ComponentScan`或`<context:component-scan>`指令必须保持原样，以请求上下文扫描某些包中的候选组件。当`ApplicationContext`检测到这样的索引时，它会自动使用它而不是扫描类路径。

要生成索引，请为包含组件扫描指令目标的组件的每个模块添加附加依赖项。以下示例显示了如何使用Maven执行此操作：

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context-indexer</artifactId>
        <version>5.1.8.RELEASE</version>
        <optional>true</optional>
    </dependency>
</dependencies>
```

使用Gradle 4.5及更早版本时，应在`compileOnly`配置中声明依赖项，如以下示例所示：

```xml
dependencies {
    compileOnly "org.springframework:spring-context-indexer:5.1.8.RELEASE"
}
```

使用Gradle 4.6及更高版本时，应在`annotationProcessor`配置中声明依赖项，如以下示例所示：

```xml
dependencies {
    annotationProcessor "org.springframework:spring-context-indexer:5.1.8.RELEASE"
}
```

该过程生成包含在jar文件中的 `META-INF/spring.components` 文件。

> 在IDE中使用此模式时，必须将`spring-context-indexer`注册为注解处理器，以确保在更新候选组件时索引是最新的。

> 在类路径上找到 `META-INF/spring.components` 时，将自动启用索引。如果索引部分可用于某些库（或用例）但不能为整个应用程序构建，则可以通过将`spring.index.ignore`设置为`true`而回退到常规类路径扫描配置（就好像根本没有索引），无论是作为系统属性还是在类路径根目录下的`spring.properties`文件中。

### 1.11 使用 JSR 330 标准注解

从 Spring 3.0 开始，Spring 提供了对 JSR-330 标准注解（依赖注入）的支持。那些注解像 Spring 注解一样被扫描。为了使用它们，你需要将相关的 jars 放在你的类路径下。

> 如果你使用Maven，则 `javax.inject` 坐标在 Maven 标准中央仓库 (<https://repo1.maven.org/maven2/javax/inject/javax.inject/1/>) 中是可用的。你可以添加下列依赖到你的 `pom.xml` 文件中：
>
> ```xml
> <dependency>
>     <groupId>javax.inject</groupId>
>     <artifactId>javax.inject</artifactId>
>     <version>1</version>
> </dependency>
> ```

#### 1.11.1 使用`@Inject`和`@Named`进行依赖注入

代替 `@Autowired`，你可以如下使用 `@javax.inject.Inject` ：

```java
import javax.inject.Inject;

public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Inject
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    public void listMovies() {
        this.movieFinder.findMovies(...);
        ...
    }
}
```

与`@Autowired`一样，您可以在字段级别，方法级别和构造函数 - 参数级别使用`@Inject`。此外，您可以将注入点声明为 `Provider`，允许按需访问较短作用域范围的bean或通过 `Provider.get()` 调用对其他bean的延迟访问。以下示例提供了上述示例的变体：

```java
import javax.inject.Inject;
import javax.inject.Provider;

public class SimpleMovieLister {

    private Provider<MovieFinder> movieFinder;

    @Inject
    public void setMovieFinder(Provider<MovieFinder> movieFinder) {
        this.movieFinder = movieFinder;
    }

    public void listMovies() {
        this.movieFinder.get().findMovies(...);
        ...
    }
}
```

如果要为应注入的依赖项使用限定名称，则应使用`@Named`注解，如以下示例所示：

```java
import javax.inject.Inject;
import javax.inject.Named;

public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Inject
    public void setMovieFinder(@Named("main") MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    // ...
}
```

与`@Autowired`一样，`@Inject`也可以与`java.util.Optional`或`@Nullable`一起使用。这在这里更适用，因为`@Inject`没有必需的属性。以下一对示例显示了如何使用`@Inject`和`@Nullable`：

```java
public class SimpleMovieLister {

    @Inject
    public void setMovieFinder(Optional<MovieFinder> movieFinder) {
        ...
    }
}
public class SimpleMovieLister {

    @Inject
    public void setMovieFinder(@Nullable MovieFinder movieFinder) {
        ...
    }
}
```

#### 1.11.2 `@Named`和`@ManagedBean`：`@Component`注解的标准等价物

代替 `@Component`，你可以使用 `@javax.inject.Named` 或者 `javax.annotation.ManagedBean`，如下面例子所示：

```java
import javax.inject.Inject;
import javax.inject.Named;

@Named("movieListener")  // @ManagedBean("movieListener") could be used as well
public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Inject
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    // ...
}
```

在不指定组件名称的情况下使用`@Component`是很常见的。`@Named`可以以类似的方式使用，如下例所示：

```java
import javax.inject.Inject;
import javax.inject.Named;

@Named
public class SimpleMovieLister {

    private MovieFinder movieFinder;

    @Inject
    public void setMovieFinder(MovieFinder movieFinder) {
        this.movieFinder = movieFinder;
    }

    // ...
}
```

使用`@Named`或`@ManagedBean`时，可以使用与使用Spring注解时完全相同的方式使用组件扫描，如以下示例所示：

```java
@Configuration
@ComponentScan(basePackages = "org.example")
public class AppConfig  {
    ...
}
```

> 与`@Component`相比，JSR-330 `@Named`和JSR-250 `@ManagedBean`注解不可组合。您应该使用Spring的构造型模型来构建自定义组件注解。

#### 1.11.3 JSR-330 标准注解的局限性

当你使用标准注解时，你应该了解其一些重要的不可用的特性，如下表所述：

| Spring              | javax.inject.*        | javax.inject restrictions / comments     |
| ------------------- | --------------------- | ---------------------------------------- |
| @Autowired          | @Inject               | `@Inject` 没有 'required' 属性。可以以 Java 8 中的 `Optional`替代。 |
| @Component          | @Named / @ManagedBean | JSR-330不提供可组合模型，只是一种识别命名组件的方法。           |
| @Scope("singleton") | @Singleton            | JSR-330的默认作用域范围就像Spring的原型。但是，为了使其与Spring的一般默认值保持一致，默认情况下，Spring容器中声明的JSR-330 bean是一个单例。为了使用除单例之外的作用域范围，您应该使用Spring的`@Scope`注解。`javax.inject`也提供了`@Scope`注解。然而，这个仅用于创建你自己的注解。 |
| @Qualifier          | @Qualifier / @Named   | `javax.inject.Qualifier`只是构建自定义限定符的元注解。具体`String`限定符（如Spring的带有值的`@Qualifier`）可以通过`javax.inject.Named`关联。 |
| @Value              | -                     | 没有等价物                                    |
| @Required           | -                     | 没有等价物                                    |
| @Lazy               | -                     | 没有等价物                                    |
| ObjectFactory       | Provider              | `javax.inject.Provider`是Spring的`ObjectFactory`的直接替代品，只有更短的`get()`方法名称。它也可以与Spring的`@Autowired`或者没有注解修饰的构造函数和setter方法结合使用。 |

### 1.12 基于 Java 类的容器配置

本章节介绍如何在你的 Java 代码中使用注解来配置 Spring 容器。包含以下主题：

- [基本概念: `@Bean` 和 `@Configuration`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java-basic-concepts)
- [使用 `AnnotationConfigApplicationContext`实例化 Spring 容器](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java-instantiating-container)
- [使用 `@Bean` 注解](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java-bean-annotation)
- [使用 `@Configuration` 注解](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java-configuration-annotation)
- [构造基于 Java 类的配置](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java-composing-configuration-classes)
- [Bean 定义配置](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-definition-profiles)
- [`PropertySource` 抽象](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-property-source-abstraction)
- [使用 `@PropertySource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-using-propertysource)
- [语句中的占位符解析](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-placeholder-resolution-in-statements)

#### 1.12.1 基本概念：`@Bean` 和 `@Configuration`

Spring 的新 Java 配置支持机制的核心是`@Configuration`注解修饰的类和`@Bean`注解修饰的方法。

`@Bean`注解用于指示一个方法实例化，配置和初始化由Spring IoC容器管理的新对象。对于那些熟悉Spring的`<beans/>` XML配置的人来说，`@Bean`注解扮演的角色与`<bean/>`元素相同。您可以将`@Bean`注解修饰的方法与任何Spring `@Component`一起使用。但是，它们最常用于`@Configuration`bean 中。

使用`@Configuration`注释类表示其主要目的是作为bean定义的源。此外，`@Configuration`类允许通过调用同一个类中的其他`@Bean`方法来定义bean间依赖关系。最简单的`@Configuration`类如下所示：

```java
@Configuration
public class AppConfig {

    @Bean
    public MyService myService() {
        return new MyServiceImpl();
    }
}
```

前面的`AppConfig`类等效于以下Spring `<beans/>` XML：

```xml
<beans>
    <bean id="myService" class="com.acme.services.MyServiceImpl"/>
</beans>
```

> 完整的`@Configuration` VS “精简的” `@Bean`模式？
>
> 当`@Bean`方法在未使用`@Configuration`注解修饰的类中声明时，它们被称为以“精简”模式处理。在`@Component`或甚至普通旧类中声明的Bean方法被认为是“精简的”，包含类的主要目的不同，而`@Bean`方法在那里更像是是一种奖励。例如，服务组件可以通过每个适用的组件类上的附加`@Bean`方法将管理视图公开给容器。在这种情况下，`@Bean`方法是一种通用的工厂方法机制。
>
> 与完整的`@Configuration`不同，精简的`@Bean`方法不能声明bean间依赖关系。相反，它们对其包含组件的内部状态进行操作，并且可选地，对它们可以声明的参数进行操作。因此，这样的`@Bean`方法不应该调用其他`@Bean`方法。每个这样的方法实际上只是特定bean引用的工厂方法，没有任何特殊的运行时语义。这里所谓的积极副作用是不必在运行时应用CGLIB子类，因此在类设计方面没有限制（即，包含类可能是`final`的，等等）。
>
> 在常见的场景中，`@Bean`方法将在`@Configuration`类中声明，确保始终使用“完整”模式，并因此将交叉方法引用重定向到容器的生命周期管理。这可以防止通过常规Java调用意外地调用相同的`@Bean`方法，这有助于减少在“精简”模式下操作时难以跟踪的细微错误。

The `@Bean` and `@Configuration` annotations are discussed in depth in the following sections. First, however, we cover the various ways of creating a spring container using by Java-based configuration.

`@Bean`和`@Configuration`注解将在以下部分中进行深入讨论。首先，我们将介绍使用基于Java的配置创建 Spring 容器的各种方法。

#### 1.12.2 使用 `AnnotationConfigApplicationContext` 实例化 Spring 容器

接下来的章节介绍了 Spring 的`AnnotationConfigApplicationContext`，它在 Spring 3.0 中引入。这个多功能的`ApplicationContext`实现不仅能够接受`@Configuration`类作为输入，还能接受`@Component`注解修饰的普通类，以及由 JSR-330 元数据注解的类。

当`@Configuration`类被作为输入时，该`@Configuration`类本身作为bean定义被注册，同时该类中声明的所有`@Bean`方法也被作为bean定义注册。

当`@Component`类和 JSR-330 类被作为输入时，它们也被作为bean定义注册，同时假定诸如`@Autovired`或者`@Inject`之类的依赖注入元数据被用在这些类中必要的位置。

**简单构造**

以在实例化`ClassPathXmlApplicationContext`时提供 Spring XML 文件作为输入完全相同的方式，你可以在实例化`AnnotationConfigApplicationContext`时使用`@Configuration`类作为输入。这就允许无 XML 的 Spring 容器，入下面例子所示：

```java
public static void main(String[] args) {
  ApplicationContext ctx = new AnnotationConfigApplicationContext(AppConfig.class);
  MyService myService = ctx.getBean(MyService.class);
  myService.doStuff();
}
```

如前文所述，`AnnotationConfigApplicationContext`并不仅限于配合`@Configuration`类使用。任何`@Component`或者JSR-330 注解修饰的类都可以作为构造器的输入，如下面例子所示：

```java
public static void main(String[] args) {
  ApplicationContext ctx = new AnnotationConfigApplicationContext(MyServiceImpl.class, Dependency1.class, Dependency2.class);
  MyService myService = ctx.getBean(MyService.class);
  myService.doStuff();
}
```

上面的例子假定`MyServiceImpl`，`Dependency1`，`Dependency2`都使用了 Spring 的依赖注入注解，比如`@Autowired` 。

**使用`register(Class<?>...)`以编程方式创建容器**

你可以使用一个无参构造器来实例化`AnnotationConfigApplicationContext`，然后使用`register()`方法来配置它。这种方法在以编程方式构造`AnnotataionConfigApplicationContext`时非常有用。下面的例子展示了这种方法：

```java
public static void main(String[] args) {
  AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext();
  ctx.register(AppConfig.class, OtherConfig.class);
  ctx.register(AdditionalConfig.class);
  ctx.refresh();
  MyService myService = ctx.getBean(MyService.class);
  myService.doStuff();
}
```

**使用`scan(String...)`开启组件扫描**

为了开启组件扫描，你可以如下修饰你的`@Configuration`类：

```java
@Configuration
@ComponentScan(basePackages = "com.acme")	//	This annotation enables component scanning.
public class AppConfig {
  //...
}
```

> 有经验的 Spring 用户会发现这中写法类似于 XML 中声明的 `context:namespace` 。如下面例子所示：
>
> ```xml
> <beans>
>     <context:component-scan base-package="com.acme"/>
> </beans>
> ```

在前面的例子中，`com.acme`包被扫描来寻找任何`@Component`注解修饰的类，同时这些类作为 Spring bean 定义被注册进入容器中。`AnnotationConfigApplicationContext`暴露`scan(String...)`方法以允许相同的组件扫描功能性。如下面例子所示：

```java
public static void main(String[] args) {
  AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext();
  ctx.scan("com.acme");
  ctx.refresh();
  MyService myService = ctx.getBean(MyService.class);
}
```

> 请记住`@Configuration`类是使用`@Component`进行 [元注解](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-meta-annotations) 的，因此它们是组件扫描的候选者。在前面的示例中，假设`AppConfig`在`com.acmepackage`（或下面的任何包）中声明，它将在`scan()`调用期间被拾取。在`refresh()`之后，它的所有`@Bean`方法都被处理并在容器中注册为bean定义。

**使用`AnnotationConfigWebApplicationContext`支持Web应用程序**

`AnnotationConfigApplicationContext`的`WebApplicationContext`变体与`AnnotationConfigWebApplicationContext`一起提供。配置Spring `ContextLoaderListener` servlet 侦听器，Spring MVC `DispatcherServlet`等时，可以使用此实现。以下`web.xml`代码段配置典型的Spring MVC Web应用程序（请注意`contextClass` context-param和init-param的使用）：

```xml
<web-app>
    <!-- Configure ContextLoaderListener to use AnnotationConfigWebApplicationContext
        instead of the default XmlWebApplicationContext -->
    <context-param>
        <param-name>contextClass</param-name>
        <param-value>
            org.springframework.web.context.support.AnnotationConfigWebApplicationContext
        </param-value>
    </context-param>

    <!-- Configuration locations must consist of one or more comma- or space-delimited
        fully-qualified @Configuration classes. Fully-qualified packages may also be
        specified for component-scanning -->
    <context-param>
        <param-name>contextConfigLocation</param-name>
        <param-value>com.acme.AppConfig</param-value>
    </context-param>

    <!-- Bootstrap the root application context as usual using ContextLoaderListener -->
    <listener>
        <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
    </listener>

    <!-- Declare a Spring MVC DispatcherServlet as usual -->
    <servlet>
        <servlet-name>dispatcher</servlet-name>
        <servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
        <!-- Configure DispatcherServlet to use AnnotationConfigWebApplicationContext
            instead of the default XmlWebApplicationContext -->
        <init-param>
            <param-name>contextClass</param-name>
            <param-value>
                org.springframework.web.context.support.AnnotationConfigWebApplicationContext
            </param-value>
        </init-param>
        <!-- Again, config locations must consist of one or more comma- or space-delimited
            and fully-qualified @Configuration classes -->
        <init-param>
            <param-name>contextConfigLocation</param-name>
            <param-value>com.acme.web.MvcConfig</param-value>
        </init-param>
    </servlet>

    <!-- map all requests for /app/* to the dispatcher servlet -->
    <servlet-mapping>
        <servlet-name>dispatcher</servlet-name>
        <url-pattern>/app/*</url-pattern>
    </servlet-mapping>
</web-app>
```

#### 1.12.3 使用 `@Bean` 注解

`@Bean`是方法级别的注解，是 XML 配置文件中的`<bean/>`元素的直接等价物。该注解支持`<bean/>`提供的一些属性，比如：[init-method](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-initializingbean) 、 [destroy-method](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-lifecycle-disposablebean) 、 [autowiring](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-autowire) 、以及 `name` 等。

你可以在`@Configuration`或者`@Component`注解修饰的类中使用`@Bean`注解。

**声明一个 Bean**

为了声明一个 bean，你可以用`@Bean`注解修饰一个方法。你使用这个方法来在`ApplicationContext`中注册一个 bean 定义，该 bean 定义的类型由该方法返回值的类型指定。默认地，bean 名称就是该方法名。下面的例子展示了`@Bean`方法声明：

```java
@Configuration
public class AppConfig {
  @Bean
  public TransferServiceImpl transferService() {
    return new TransferServiceImpl();
  }
}
```

完全等价于下面的 Spring XML 片段：

```xml
<beans>
  <bean id="transferService" class="com.acme.TransferServiceImpl"/>
</beans>
```

上面两种声明都使得`ApplicationContext`中名为`transferService`的 bean 成为可用，绑定到一个类型为`TransferServiceImpl`的一个对象实例，如下面文字图所示：

```
transferService -> com.acme.TransferServiceImpl
```

你也可以声明你的`@Bean`方法，其返回值类型为接口或者基类。如下面例子所示：

```java
@Configuration
public class AppConfig {
  @Bean
  public TransferService transferService() {
    return new TransferServiceImpl();
  }
}
```

但是，这会将高级类型预测的可见性限制为指定的接口类型（`TransferService`）。然后，只要容器了解完整类型（`TransferServiceImpl`）一次，受影响的单例 bean 就已经被实例化。非懒加载的单例 bean 按照它们被声明的顺序实例化，因而你可能会看到不同的类型匹配结果，具体取决于另一个组件何时尝试通过非声明类型进行匹配（比如`@Autowired TransferServiceImp`，只会在`transferService` bean 已经被实例化时被解析一次）。

> 如果您始终通过声明的服务接口引用您的类型，则`@Bean`返回类型可以安全地加入该设计决策。但是，对于实现多个接口的组件或可能由其实现类型引用的组件，更安全的做法是声明可能的最具体的返回类型（至少与引用您的bean的注入点所需的具体类型相同）。

**Bean 依赖**

`@Bean`注解的方法能够携带任意数量的参数来描述构造该 bean 所必需的依赖。比如，如果我们的`TransferService`需要一个`AccountRepository`，我们可以使用方法参数来实现该依赖关系。如下面例子所示：

```java
@Configuration
public class AppConfig {

    @Bean
    public TransferService transferService(AccountRepository accountRepository) {
        return new TransferServiceImpl(accountRepository);
    }
}
```

解析机制与基于构造器的依赖注入完全一样。参考 [the relevant section](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-constructor-injection) 获取更多细节。

**接收生命周期回调**

使用`@Bean`注解定义的任何类都支持常规生命周期回调，并且可以使用JSR-250中的`@PostConstruct`和`@PreDestroy`注解。有关更多详细信息，请参阅 [JSR-250注解](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-postconstruct-and-predestroy-annotations)  。

同样，常规的 Spring [声明周期](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-nature) 回调也是完全支持的。如果一个 bean 实现了`InitializingBean`，`DisposableBean`，或者`Lifecycle` ，它们各自的方法都由容器调用。

标准的`*Aware`接口集合，诸如 [BeanFactoryAware](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-beanfactory), [BeanNameAware](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-aware), [MessageSourceAware](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#context-functionality-messagesource),[ApplicationContextAware](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-aware), 等等，也是完整支持的。

`@Bean`注解支持指定任意初始化和销毁回调方法，就像Spring XML中`bean`元素上的`init-method`和`destroy-method`属性一样，如下例所示：

```java
public class BeanOne {

    public void init() {
        // initialization logic
    }
}

public class BeanTwo {

    public void cleanup() {
        // destruction logic
    }
}

@Configuration
public class AppConfig {

    @Bean(initMethod = "init")
    public BeanOne beanOne() {
        return new BeanOne();
    }

    @Bean(destroyMethod = "cleanup")
    public BeanTwo beanTwo() {
        return new BeanTwo();
    }
}
```

> 默认情况下，使用Java配置定义的具有公共`close`或`shutdown`方法的bean会自动使用销毁回调登记。如果您有一个公共`close`或`shutdown`方法，并且您不希望在容器关闭时调用它，则可以将`@Bean(destroyMethod=“”)`添加到bean定义中以禁用默认 `(inferred)` 模式。
>
> 对于使用JNDI获取的资源，您可能希望默认执行此操作，因为其生命周期在应用程序之外进行管理。特别是，请确保始终为`DataSource`执行此操作，因为已知它在Java EE应用程序服务器上存在问题。
>
> 以下示例说明如何防止`DataSource`的自动销毁回调：
>
> ```java
> @Bean(destroyMethod="")
> public DataSource dataSource() throws NamingException {
>     return (DataSource) jndiTemplate.lookup("MyDS");
> }
> ```
>
> 同时，使用`@Bean`方法，您通常使用编程式JNDI查找，或者使用Spring的`JndiTemplateor` 或者  `JndiLocatorDelegate`帮助程序或直接JNDI `InitialContext`用法，但不使用`JndiObjectFactoryBean` 变体（这会强制您将返回类型声明为`FactoryBean`类型而不是实际目标类型 ，使得在其他打算引用此方法提供的资源的`@Bean`方法中更难进行交叉引用调用）。

In the case of `BeanOne` from the example above the preceding note, it would be equally valid to call the `init()` method directly during construction, as the following example shows:

对于上面提示示例中的`BeanOne`的情况，在构造期间直接调用`init()`方法同样有效，如下例所示：

```java
@Configuration
public class AppConfig {

    @Bean
    public BeanOne beanOne() {
        BeanOne beanOne = new BeanOne();
        beanOne.init();
        return beanOne;
    }

    // ...
}
```

> 当你直接使用 Java 工作，你就可以随意使用你的对象而不需要始终依赖容器的生命周期管理。

**指定 Bean 作用域**

Spring 包含`@Scope`注解因而你可以指定 bean 的作用域。

**使用`@Scope`注解**

你可以指定使用`@Bean`注解定义的 beans 应该具有的特定作用域。你可以使用任何在 [Bean 作用域](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-scopes)  章节中描述的所有标准作用域。

默认的作用域是`singleton`，不过你可以用`@Scope`注解覆盖它。如下面例子所示：

```java
@Configuration
public class MyConfiguration {

    @Bean
    @Scope("prototype")
    public Encryptor encryptor() {
        // ...
    }
}
```

**`Scope` 和 `scoped-proxy` **

Spring提供了一种通过 [作用域代理](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-other-injection) 处理作用域依赖项的便捷方法。使用XML配置时创建此类代理的最简单方法是`<aop：scoped-proxy/>`元素。使用`@Scope`注解在Java中配置bean提供了与`proxyMode`属性的等效支持。默认值为无代理（`ScopedProxyMode.NO`），但您可以指定`ScopedProxyMode.TARGET_CLASS`或`ScopedProxyMode.INTERFACES` 。

如果使用Java将XML参考文档（请参阅 [作用域代理](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-scopes-other-injection) ）的作用域代理示例移植到我们的@Bean，它类似于以下内容：

```java
// an HTTP Session-scoped bean exposed as a proxy
@Bean
@SessionScope
public UserPreferences userPreferences() {
    return new UserPreferences();
}

@Bean
public Service userService() {
    UserService service = new SimpleUserService();
    // a reference to the proxied userPreferences bean
    service.setUserPreferences(userPreferences());
    return service;
}
```

**自定义 Bean 名称**

默认情况下，配置类使用`@Bean`方法的名称作为结果bean的名称。但是，可以使用`name`属性覆盖此功能，如以下示例所示：

```java
@Configuration
public class AppConfig {

    @Bean(name = "myThing")
    public Thing thing() {
        return new Thing();
    }
}
```

**Bean 别名**

正如 [Naming Beans](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-beanname) 中所讨论的，有时需要为单个bean提供多个名称，也称为bean别名。`@Bean`注解的`name`属性为此接受String数组。以下示例显示如何为bean设置多个别名：

```java
@Configuration
public class AppConfig {

    @Bean({"dataSource", "subsystemA-dataSource", "subsystemB-dataSource"})
    public DataSource dataSource() {
        // instantiate, configure and return DataSource bean...
    }
}
```

**Bean 描述**

有时，提供更详细的bean文本描述会很有帮助。当bean 被暴露出来（可能通过JMX）用于监视目的时，这可能特别有用。

要向`@Bean`添加描述，可以使用 [`@Description`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/context/annotation/Description.html) 注解，如以下示例所示：

```java
@Configuration
public class AppConfig {

    @Bean
    @Description("Provides a basic example of a bean")
    public Thing thing() {
        return new Thing();
    }
}
```

#### 1.12.4 使用`@Configuration`注解

`@Configuration`是一个类级别注释，指示该对象是bean定义的来源。`@Configuration`类通过公共`@Bean`注解方法声明bean。在`@Configuration`类上调用`@Bean`方法也可用于定义bean间依赖关系。有关一般介绍，请参阅 [基本概念：`@Bean`和`@Configuration`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-java-basic-concepts) 。

##### 注入 bean 间依赖关系

当 beans 拥有对其它 bean 的依赖，表达这种依赖关系就如同让一个 bean 方法调用另一个一样简单。如下面例子所示：

```java
@Configuration
public class AppConfig {

    @Bean
    public BeanOne beanOne() {
        return new BeanOne(beanTwo());
    }

    @Bean
    public BeanTwo beanTwo() {
        return new BeanTwo();
    }
}
```

上面的例子中，`beanOne`通过构造器注入接收对`beanTwo`的引用。

> 声明 bean 间依赖的方法只有当`@Bean`方法在`@Configuration`类中声明时才会生效。你无法通过普通的`@Component`类来声明 bean间依赖。

##### 查找方法注入

前面提到过，[查找方法注入](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-method-injection) 是一个你应该很少用到的高级特性。只有在一个单例作用域的 bean 拥有对一个原型作用域的 bean 的依赖的场景下，该特性才是有用的。为这种配置类型使用 Java 提供了实现这种模式的一种自然含义。下面的例子展示了如何使用方法注入查找：

```java
public abstract class CommandManager {
    public Object process(Object commandState) {
        // grab a new instance of the appropriate Command interface
        Command command = createCommand();
        // set the state on the (hopefully brand new) Command instance
        command.setState(commandState);
        return command.execute();
    }

    // okay... but where is the implementation of this method?
    protected abstract Command createCommand();
}
```

通过使用 Java 配置，你可以创建`CommandManager`的子类，在那里抽象`createCommand()`方法被覆盖，以便它可以查找一个新的（原型）命令对象。下面的例子展示了具体做法：

```java
@Bean
@Scope("prototype")
public AsyncCommand asyncCommand() {
    AsyncCommand command = new AsyncCommand();
    // inject dependencies here as required
    return command;
}

@Bean
public CommandManager commandManager() {
    // return new anonymous implementation of CommandManager with createCommand()
    // overridden to return a new prototype Command object
    return new CommandManager() {
        protected Command createCommand() {
            return asyncCommand();
        }
    }
}
```

##### 有关基于Java的配置如何在内部工作的更多信息

考虑下面的例子，展示了`@Bean`注解方法被调用两次：

```java
@Configuration
public class AppConfig {

    @Bean
    public ClientService clientService1() {
        ClientServiceImpl clientService = new ClientServiceImpl();
        clientService.setClientDao(clientDao());
        return clientService;
    }

    @Bean
    public ClientService clientService2() {
        ClientServiceImpl clientService = new ClientServiceImpl();
        clientService.setClientDao(clientDao());
        return clientService;
    }

    @Bean
    public ClientDao clientDao() {
        return new ClientDaoImpl();
    }
}
```

`clientDao()` 在 `clientService1()` 中调用一次，在 `clientService2()` 中调用一次。由于此方法创建 `ClientDaoImpl` 的新实例并将其返回，因此通常希望有两个实例（每个服务一个）。这肯定会有问题：在Spring中，实例化的bean默认具有 `singleton` 作用域范围。这就是魔法的来源：所有`@Configuration`类在启动时都使用`CGLIB`进行子类化。在子类中，子方法在调用父方法并创建新实例之前，首先检查容器是否有任何缓存（作用域）bean。

> 根据你的 bean 的作用域不同，行为也有所不同。我们这里讨论的是单例作用域。

> 从Spring 3.2开始，不再需要将CGLIB添加到类路径中，因为CGLIB类已经在`org.springframework.cglib`下重新打包并直接包含在spring-core JAR中。

> 由于CGLIB在启动时动态添加功能特性，因此存在一些限制。特别是，配置类不能是`final`的。但是，从4.3开始，配置类允许使用任何构造函数，包括使用`@Autowired`或单个非默认构造函数声明进行默认注入。如果您希望避免任何CGLIB强加的限制，请考虑在非`@Configuration`类中声明您的`@Bean`方法（例如，在普通的`@Component`类上）。此时就不再会拦截`@Bean`方法之间的跨方法调用，因此您必须在构造函数或方法级别专门依赖依赖项注入。

#### 1.12.5 构造基于 Java 的配置

Spring 基于 Java 的配置特性使得你可以组合注解，那样做可以降低你的配置的复杂度。

##### 使用 `@Import` 注解

就像在Spring XML文件中使用 `<import/>` 元素来帮助模块化配置一样，`@Import`注解允许从另一个配置类加载`@Bean`定义，如下例所示：

```java
@Configuration
public class ConfigA {

    @Bean
    public A a() {
        return new A();
    }
}

@Configuration
@Import(ConfigA.class)
public class ConfigB {

    @Bean
    public B b() {
        return new B();
    }
}
```

现在，在实例化上下文时，不需要同时指定`ConfigA.class`和`ConfigB.class`，只需显式提供`ConfigBneeds`，如下例所示：

```java
public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(ConfigB.class);

    // now both beans A and B will be available...
    A a = ctx.getBean(A.class);
    B b = ctx.getBean(B.class);
}
```

这种方法简化了容器实例化，只需要使用一个类，而不需要你在构造过程中记忆可能存在的大量`@Configuration`类。

> 从Spring Framework 4.2开始，`@Import`还支持引用常规组件类，类似于`AnnotationConfigApplicationContext.register`方法。如果要避免组件扫描，这一点特别有用，可以使用一些配置类作为明确定义所有组件的入口点。

###### Injecting Dependencies on Imported `@Bean` Definitions

前面简化的例子可以工作。在大多数实际场景中，beans 会依赖其它跨配置类的 bean。在使用 XML 配置文件时，这不是问题，因为这不涉及编译器，同时你可以声明`ref="someBean"`并相信 Spring 在容器初始化过程中解析它。当使用`@Configuration`类时，编译器会在配置模型上施加约束，此时对其它 beans 的引用必须是合法的 Java 语法。

幸运的是，解决这个问题其实很简单。如我们已经讨论过的，`@Bean` 方法可以拥有任意多个参数来描述 bean 依赖。考虑下面这个更接近现实的场景，其中包含多个`@Configuration`类，它们相互依赖对方声明的 beans ：

```java
@Configuration
public class ServiceConfig {

    @Bean
    public TransferService transferService(AccountRepository accountRepository) {
        return new TransferServiceImpl(accountRepository);
    }
}

@Configuration
public class RepositoryConfig {

    @Bean
    public AccountRepository accountRepository(DataSource dataSource) {
        return new JdbcAccountRepository(dataSource);
    }
}

@Configuration
@Import({ServiceConfig.class, RepositoryConfig.class})
public class SystemTestConfig {

    @Bean
    public DataSource dataSource() {
        // return new DataSource
    }
}

public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(SystemTestConfig.class);
    // everything wires up across configuration classes...
    TransferService transferService = ctx.getBean(TransferService.class);
    transferService.transfer(100.00, "A123", "C456");
}
```

还有另外一种方法可以得到同样的效果。其实`@Configuration`类说到底也只是容器中的另一种 bean，这就意味着它们也可以像任何其它 bean 一样享受`@Autowired`和`@Value`注入和其它特性的好处。

> 确保以这种方式注入的依赖项只是最简单的类型。`@Configuration`类在上下文初始化期间很早就被处理，并且强制以这种方式注入依赖项可能导致意外的早期初始化。尽可能采用基于参数的注入，如前面的示例所示。
>
> 另外，需要特别注意通过`@Bean`对`BeanPostProcessor`和`BeanFactoryPostProcessor`的定义。这些通常应该声明为静态`@Bean`方法，而不是触发包含它们的配置类的实例化。否则，`@Autowired`和`@Value`不能在配置类本身上工作，因为它过早地被创建为bean实例。

以下示例显示了如何将一个bean自动装配到另一个bean：

```java
@Configuration
public class ServiceConfig {

    @Autowired
    private AccountRepository accountRepository;

    @Bean
    public TransferService transferService() {
        return new TransferServiceImpl(accountRepository);
    }
}

@Configuration
public class RepositoryConfig {

    private final DataSource dataSource;

    @Autowired
    public RepositoryConfig(DataSource dataSource) {
        this.dataSource = dataSource;
    }

    @Bean
    public AccountRepository accountRepository() {
        return new JdbcAccountRepository(dataSource);
    }
}

@Configuration
@Import({ServiceConfig.class, RepositoryConfig.class})
public class SystemTestConfig {

    @Bean
    public DataSource dataSource() {
        // return new DataSource
    }
}

public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(SystemTestConfig.class);
    // everything wires up across configuration classes...
    TransferService transferService = ctx.getBean(TransferService.class);
    transferService.transfer(100.00, "A123", "C456");
}
```

> 仅在Spring Framework 4.3中支持`@Configuration`类中的构造函数注入。另请注意，如果目标bean仅定义了一个构造函数，则无需指定`@Autowired`。在前面的示例中，`RepositoryConfig`构造函数中不需要`@Autowired`。

**完全限定导入 beans 以便于导航**

在前面的场景中，使用`@Autowired`可以很好地工作并提供所需的模块化，但确定声明自动装配的bean定义的确切位置仍然有些模棱两可。例如，作为一名查看`ServiceConfig`的开发人员，您如何确切地知道`@Autowired`的 `AccountRepository ` bean的声明位置？ 它在代码中并不明确，不过可能还好。请记住， [Spring Tool Suite](https://spring.io/tools/sts) 提供的工具可以呈现图形，显示所有内容的连线方式，这可能就是您所需要的。此外，您的Java IDE可以轻松找到`AccountRepository`类型的所有声明和用法，并快速显示返回该类型的`@Bean`方法的位置。

如果这种歧义不可接受并且您希望在IDE中从一个`@Configuration`类直接导航到另一个`@Configuration`类，请考虑自行装配配置类本身。以下示例显示了如何执行此操作：

```java
@Configuration
public class ServiceConfig {

    @Autowired
    private RepositoryConfig repositoryConfig;

    @Bean
    public TransferService transferService() {
        // navigate 'through' the config class to the @Bean method!
        return new TransferServiceImpl(repositoryConfig.accountRepository());
    }
}
```

在前面的情况中，定义`AccountRepository`是完全明确的。但是，`ServiceConfig`现在与`RepositoryConfig`紧密耦合。这是一种权衡的结果。通过使用基于接口的或基于类的抽象`@Configuration`类，可以在某种程度上减轻这种紧密耦合。请考虑以下示例：

```java
@Configuration
public class ServiceConfig {

    @Autowired
    private RepositoryConfig repositoryConfig;

    @Bean
    public TransferService transferService() {
        return new TransferServiceImpl(repositoryConfig.accountRepository());
    }
}

@Configuration
public interface RepositoryConfig {

    @Bean
    AccountRepository accountRepository();
}

@Configuration
public class DefaultRepositoryConfig implements RepositoryConfig {

    @Bean
    public AccountRepository accountRepository() {
        return new JdbcAccountRepository(...);
    }
}

@Configuration
@Import({ServiceConfig.class, DefaultRepositoryConfig.class})  // import the concrete config!
public class SystemTestConfig {

    @Bean
    public DataSource dataSource() {
        // return DataSource
    }

}

public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(SystemTestConfig.class);
    TransferService transferService = ctx.getBean(TransferService.class);
    transferService.transfer(100.00, "A123", "C456");
}
```

现在，`ServiceConfig`与具体的`DefaultRepositoryConfig`松散耦合，内置的IDE工具仍然很有用：您可以轻松获得`RepositoryConfig`实现的类型层次结构。通过这种方式，导航`@Configurationclasses`及其依赖项与导航基于接口的代码的常规过程没有什么不同。

> 如果要影响某些bean的启动创建顺序，请考虑将其中一些声明为`@Lazy`（用于在首次访问时创建而不是在启动时）或`@DependsOn`某些其他bean（确保在创建当前的bean之前创建特定的其他bean，超出两者的直接依赖性所暗示的）。

##### 有条件地包含`@Configuration`类或`@Bean`方法

基于某些任意系统状态，有条件地启用或禁用整个的`@Configuration`类甚至单个`@Bean`方法通常很有用。一个常见的例子是，只有在Spring `Environment` 中启用了特定的配置文件时才使用`@Profile`注解来激活bean（有关详细信息，请参阅[Bean定义配置文件](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-definition-profiles) ）。

`@Profile`注解实际上是通过使用更灵活的注解 [`@Conditional`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/context/annotation/Conditional.html) 实现的。`@Conditional`注解表示在注册`@Bean`之前应该参考的特定`org.springframework.context.annotation.Condition`实现。

`Condition`接口的实现提供了一个返回`true`或`false`的`matches(...)`方法。例如，以下列表显示了用于`@Profile`的实际`Condition`实现：

```java
@Override
public boolean matches(ConditionContext context, AnnotatedTypeMetadata metadata) {
    if (context.getEnvironment() != null) {
        // Read the @Profile annotation attributes
        MultiValueMap<String, Object> attrs = metadata.getAllAnnotationAttributes(Profile.class.getName());
        if (attrs != null) {
            for (Object value : attrs.get("value")) {
                if (context.getEnvironment().acceptsProfiles(((String[]) value))) {
                    return true;
                }
            }
            return false;
        }
    }
    return true;
}
```

参考 [`@Conditional`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/context/annotation/Conditional.html) 文档获取更多细节。

##### 结合 Java 和 XML 配置

Spring的`@Configuration`类支持并非旨在成为Spring XML的100％完全替代品。某些工具，如Spring XML命名空间，仍然是配置容器的理想方法。在XML方便或必要的情况下，您可以选择：使用例如`ClassPathXmlApplicationContext`以“以XML为中心”的方式实例化容器，或者使用`AnnotationConfigApplicationContext`，并使用`@ImportResource`注解，根据需要导入XML，以“以Java为中心”的方式实例化它。

###### 以XML为中心使用`@Configuration`类

最好从XML引导Spring容器，并以ad-hoc方式包含`@Configuration`类。例如，在使用Spring XML的大型现有代码库中，可以根据需要更轻松地创建`@Configuration`类，并将其包含在现有XML文件中。在本节的后面部分，我们将介绍在这种“以XML为中心”的情况下使用`@Configuration`类的选项。

将`@Configuration`类声明为普通的Spring `<bean/>`元素

请记住，`@Configuration`类是容器中最终的bean定义。在本系列示例中，我们创建一个名为`AppConfig`的`@Configuration`类，并将其作为`<bean/>`定义包含在`system-test-config.xml`中。由于`<context:annotation-config/>`已打开，容器会识别`@Configuration`注解并正确处理`AppConfig`中声明的`@Bean`方法。

以下示例显示了Java中的普通配置类：

```java
@Configuration
public class AppConfig {

    @Autowired
    private DataSource dataSource;

    @Bean
    public AccountRepository accountRepository() {
        return new JdbcAccountRepository(dataSource);
    }

    @Bean
    public TransferService transferService() {
        return new TransferService(accountRepository());
    }
}
```

以下示例显示了示例`system-test-config.xml`文件的一部分：

```xml
<beans>
    <!-- enable processing of annotations such as @Autowired and @Configuration -->
    <context:annotation-config/>
    <context:property-placeholder location="classpath:/com/acme/jdbc.properties"/>

    <bean class="com.acme.AppConfig"/>

    <bean class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>
</beans>
```

以下示例显示了可能的`jdbc.properties`文件：

```
jdbc.url=jdbc:hsqldb:hsql://localhost/xdb
jdbc.username=sa
jdbc.password=
```

```java
public static void main(String[] args) {
    ApplicationContext ctx = new ClassPathXmlApplicationContext("classpath:/com/acme/system-test-config.xml");
    TransferService transferService = ctx.getBean(TransferService.class);
    // ...
}
```

> 在`system-test-config.xml`文件中，`AppConfig` `<bean/>`不声明id元素。虽然这样做是可以接受的，但是没有必要，因为没有其他bean引用它，并且不太可能通过名称从容器中明确地获取它。类似地，`DataSource` bean只是按类型自动装配，因此不严格要求显式的bean id。

使用 <context:component-scan/> 获取 `@Configuration` 类

因为`@Configuration`是使用`@Component`进行元注解的，所以`@Configuration`注解类自动成为组件扫描的候选者。使用与前一个示例中描述的相同的方案，我们可以重新定义`system-test-config.xml`以利用组件扫描。请注意，在这种情况下，我们不需要显式声明`<context:annotation-config/>`，因为`<context:annotation-config/>`启用相同的功能。

以下示例显示了已修改的`system-test-config.xml`文件：

```xml
<beans>
    <!-- picks up and registers AppConfig as a bean definition -->
    <context:component-scan base-package="com.acme"/>
    <context:property-placeholder location="classpath:/com/acme/jdbc.properties"/>

    <bean class="org.springframework.jdbc.datasource.DriverManagerDataSource">
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>
</beans>
```

###### `@Configuration` 类为中心使用 XML 和 `@ImportResource`

在`@Configuration`类是配置容器的主要机制的应用程序中，仍然可能需要使用一些XML。在这些场景中，您可以使用`@ImportResource`并根据需要定义尽可能多的XML。这样做可以实现“以Java为中心”的方法来配置容器并将XML保持在最低限度。以下示例（包括配置类，定义bean的XML文件，属性文件和`main`类）显示了如何使用`@ImportResource`注解来实现根据需要使用XML的“以Java为中心”的配置：

```java
@Configuration
@ImportResource("classpath:/com/acme/properties-config.xml")
public class AppConfig {

    @Value("${jdbc.url}")
    private String url;

    @Value("${jdbc.username}")
    private String username;

    @Value("${jdbc.password}")
    private String password;

    @Bean
    public DataSource dataSource() {
        return new DriverManagerDataSource(url, username, password);
    }
}
```

```xml
properties-config.xml
<beans>
    <context:property-placeholder location="classpath:/com/acme/jdbc.properties"/>
</beans>
```

```
jdbc.properties
jdbc.url=jdbc:hsqldb:hsql://localhost/xdb
jdbc.username=sa
jdbc.password=
```

```java
public static void main(String[] args) {
    ApplicationContext ctx = new AnnotationConfigApplicationContext(AppConfig.class);
    TransferService transferService = ctx.getBean(TransferService.class);
    // ...
}
```

### 1.13 环境抽象

[`Environment`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/core/env/Environment.html) 接口是集成在容器内部的一个抽象，对应用环境的两个关键方面进行了建模： [profiles](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-definition-profiles) 和 [properties](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-property-source-abstraction).

配置文件是仅在给定配置文件处于活动状态时才向容器注册的bean定义的命名的逻辑组。可以将Bean分配给配置文件，无论该配置文件是以XML还是使用注解定义。与配置文件相关的`Environment`对象的作用是确定哪些配置文件（如果有）当前处于活动状态，以及默认情况下哪些配置文件（如果有）应该处于活动状态。

属性在几乎所有应用程序中都发挥着重要作用，可能源自各种来源：属性文件，JVM系统属性，系统环境变量，JNDI，servlet上下文参数，ad-hoc `Properties` 对象，`Map`对象等等。与属性相关的 `Environment` 对象的作用是为用户提供方便的服务界面，用于配置属性源和从中解析属性。

#### 1.13.1 Bean 定义配置

Bean定义配置文件在核心容器中提供了一种机制，允许在不同环境中注册不同的bean。“环境”这个词对不同的用户来说意味着不同的东西，这个功能在很多场景下都很有帮助，包括：

- 在开发过程中使用内存中的数据源，而在QA或生产环境中通过JNDI查找相同的数据源。
- 仅在将应用程序部署到性能环境时注册监控基础设施。
- 为客户A和客户B部署注册各自的bean的自定义实施。

考虑一个场景，实际应用程序中需要一个`DataSource`。在测试环境中，配置可能类似于以下内容：

```java
@Bean
public DataSource dataSource() {
    return new EmbeddedDatabaseBuilder()
        .setType(EmbeddedDatabaseType.HSQL)
        .addScript("my-schema.sql")
        .addScript("my-test-data.sql")
        .build();
}
```

现在考虑如何将此应用程序部署到QA或生产环境中，假设应用程序的数据源已在生产应用程序服务器的JNDI目录中注册。我们的`dataSource` bean现在看起来如下：

```java
@Bean(destroyMethod="")
public DataSource dataSource() throws Exception {
    Context ctx = new InitialContext();
    return (DataSource) ctx.lookup("java:comp/env/jdbc/datasource");
}
```

问题是如何根据当前环境在使用这两种变体之间切换。随着时间的推移，Spring用户已经设计了许多方法来完成这项工作，通常依赖于系统环境变量和XML`<import/>`语句的组合，这些语句包含根据环境变量的值可以解析为正确配置文件路径的`${placeholder}`占位符。Bean定义配置文件是核心容器功能，可为此问题提供解决方案。

如果我们概括了前面的特定于环境的bean定义示例中展示的用例，我们最终需要在某些上下文中注册某些bean定义，而在其他上下文中则不需要。您可以说您希望在情境A中注册特定的bean定义配置文件，在情况B中注册不同的配置文件。我们首先更新配置以反映此需求。

##### 使用 `@Profile`

[`@Profile`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/context/annotation/Profile.html) 注解允许你将一个组件标记为具有注册资格的，当一个或者多个特定的配置文件处于激活状态。使用我们前面的例子，我们可以重写其中的 `dataSource` 配置如下：

```java
@Configuration
@Profile("development")
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
@Configuration
@Profile("production")
public class JndiDataConfig {

    @Bean(destroyMethod="")
    public DataSource dataSource() throws Exception {
        Context ctx = new InitialContext();
        return (DataSource) ctx.lookup("java:comp/env/jdbc/datasource");
    }
}
```

> 正如我们前面提到的，使用`@Bean`方法，你选择了使用编程方式的 JNDI 查找，通过使用 Spring 的 `JndiTemplate`/`JndiLocatorDelegate` 帮助类或者直接使用前面展示的 `InitialContext` ，而不是使用 `JndiObjectFactoryBean` 变体，这将强制你声明返回类型为`FactoryBean` 。

配置字符串可以包含一个简单的配置名（比如，`production`）或者一个配置表达式。一个配置表达式可以表达更复杂的配置逻辑（比如，`production & us-east`）。配置表达式中支持使用以下操作符：

- `!`: 逻辑 “否”
- `&`: 逻辑 “与”
- `|`: 逻辑 “或”

> 你不能在不适用括号的情况下混用`&`和`|`。比如，`production & us-east | eu-central`是一个无效表达式。它必须被写成 `production & (us-east | eu-central)`。

你可以将`@Profile`用作一个 [meta-annotation](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-meta-annotations) 以创建一个自定义组合注解。下面的例子定义了`Production`注解，你可以将它用作`@Profile("production")` 的替代品：

```java
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Profile("production")
public @interface Production {
}
```

> 如果`@Configuration`类标有`@Frofile`，则除非一个或多个指定的配置文件处于活动状态，否则将绕过与该类关联的所有`@Bean`方法和`@Import`注解。如果`@Component`或`@Configuration`类标有`@Profile({"p1", "p2"})`，除非已激活配置文件'p1'或'p2'，否则不会注册或处理该类。如果给定的配置文件以NOT运算符（`!`）作为前缀，则仅在配置文件未激活时才注册带注解的元素。例如，给定`@Profile({"p1", "!p2"})`，如果配置文件'p1'处于活动状态或配置文件'p2'未激活，则会发生注册。

`@Profile`也可以在方法级别声明，只包含一个配置类的特定bean（例如，对于特定bean的替代变体），如下例所示：

```java
@Configuration
public class AppConfig {

    @Bean("dataSource")
    @Profile("development") 	//The standaloneDataSource method is available only in the development profile.
    public DataSource standaloneDataSource() {
        return new EmbeddedDatabaseBuilder()
            .setType(EmbeddedDatabaseType.HSQL)
            .addScript("classpath:com/bank/config/sql/schema.sql")
            .addScript("classpath:com/bank/config/sql/test-data.sql")
            .build();
    }

    @Bean("dataSource")
    @Profile("production") 	//The jndiDataSource method is available only in the production profile.
    public DataSource jndiDataSource() throws Exception {
        Context ctx = new InitialContext();
        return (DataSource) ctx.lookup("java:comp/env/jdbc/datasource");
    }
}
```

> 对于`@Bean`方法上的`@Profile`，可能适用于一个特殊的场景：对于相同Java方法名称重载`@Bean`方法（类似于构造函数重载），需要在所有重载方法上一致地声明`@Profile`条件。如果条件不一致，则只有重载方法中第一个声明的条件才会生效。因此，`@Profile`不能用于选择具有特定参数签名的重载方法。在创建时，同一bean的所有工厂方法之间的解析遵循Spring的构造函数解析算法。
>
> 如果要定义具有不同配置文件条件的备用Bean，请使用不同的Java方法名称，使用`@Bean` name属性指向相同的bean名称，如上例所示。如果参数签名都是相同的（例如，所有变体都具有无参工厂方法），这是在有效的Java类中首先表示这种配置的唯一方法（因为可以只有一个特定名称和参数签名的方法）。

##### XML Bean 定义配置

XML中的对应物是`<beans>`元素的`profile`属性。我们之前的示例配置可以在两个XML文件中重写，如下所示：

```xml
<beans profile="development"
    xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:jdbc="http://www.springframework.org/schema/jdbc"
    xsi:schemaLocation="...">

    <jdbc:embedded-database id="dataSource">
        <jdbc:script location="classpath:com/bank/config/sql/schema.sql"/>
        <jdbc:script location="classpath:com/bank/config/sql/test-data.sql"/>
    </jdbc:embedded-database>
</beans>
<beans profile="production"
    xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:jee="http://www.springframework.org/schema/jee"
    xsi:schemaLocation="...">

    <jee:jndi-lookup id="dataSource" jndi-name="java:comp/env/jdbc/datasource"/>
</beans>
```

也可以避免在同一文件中拆分和嵌套`<beans/>`元素，如下例所示：

```xml
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:jdbc="http://www.springframework.org/schema/jdbc"
    xmlns:jee="http://www.springframework.org/schema/jee"
    xsi:schemaLocation="...">

    <!-- other bean definitions -->

    <beans profile="development">
        <jdbc:embedded-database id="dataSource">
            <jdbc:script location="classpath:com/bank/config/sql/schema.sql"/>
            <jdbc:script location="classpath:com/bank/config/sql/test-data.sql"/>
        </jdbc:embedded-database>
    </beans>

    <beans profile="production">
        <jee:jndi-lookup id="dataSource" jndi-name="java:comp/env/jdbc/datasource"/>
    </beans>
</beans>
```

`spring-bean.xsd`已被约束为仅允许这些元素作为文件中的最后一个元素。这应该有助于提供灵活性，而不会在XML文件中引起混乱。

> XML副本不支持前面描述的配置文件表达式。但是，可以通过使用`!`运算符来否定配置文件。也可以通过嵌套配置文件来应用逻辑“与”，如以下示例所示：
>
> ```xml
> <beans xmlns="http://www.springframework.org/schema/beans"
>     xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>     xmlns:jdbc="http://www.springframework.org/schema/jdbc"
>     xmlns:jee="http://www.springframework.org/schema/jee"
>     xsi:schemaLocation="...">
>
>     <!-- other bean definitions -->
>
>     <beans profile="production">
>         <beans profile="us-east">
>             <jee:jndi-lookup id="dataSource" jndi-name="java:comp/env/jdbc/datasource"/>
>         </beans>
>     </beans>
> </beans>
> ```
>
> 在前面的示例中，如果`production`和`us-east`配置文件都处于活动状态，则会暴露`dataSource` bean。

##### 激活一个配置

现在我们已经更新了配置，我们仍然需要指示Spring哪个配置文件处于活动状态。如果我们现在开始我们的示例应用程序，我们会看到抛出一个`NoSuchBeanDefinitionException`，因为容器找不到名为`dataSource`的Spring bean。

激活配置文件可以通过多种方式完成，但最直接的方法是以编程方式对可通过`ApplicationContext`提供的`Environment` API进行操作。以下示例显示了如何执行此操作：

```java
AnnotationConfigApplicationContext ctx = new AnnotationConfigApplicationContext();
ctx.getEnvironment().setActiveProfiles("development");
ctx.register(SomeConfig.class, StandaloneDataConfig.class, JndiDataConfig.class);
ctx.refresh();
```

此外，您还可以通过`spring.profiles.active`属性声明性地激活配置文件，该属性可以通过系统环境变量，JVM系统属性，`web.xml`中的servlet上下文参数指定，甚至可以作为JNDI中的条目指定（参见 [`PropertySource` Abstraction](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-property-source-abstraction) ）。在集成测试中，可以使用`spring-test`模块中的`@ActiveProfiles`注释声明活动配置文件（请参阅 [context configuration with environment profiles](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/testing.html#testcontext-ctx-management-env-profiles) ）。

请注意，配置文件不是“要么 - 要么”命题。您可以一次激活多个配置文件。在编程方式中，您可以为`setActiveProfiles()`方法提供多个配置文件名称，该方法接受`String...`可变参数。以下示例激活多个配置文件：

```java
ctx.getEnvironment().setActiveProfiles("profile1", "profile2");
```

声明性地，`spring.profiles.active`可以接受以逗号分隔的配置文件名列表，如以下示例所示：

```
-Dspring.profiles.active="profile1,profile2"
```

##### 默认配置

默认配置文件表示默认启用的配置文件。 请考虑以下示例：

```java
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
```

如果没有激活配置文件，则创建`dataSource`。您可以将此视为一种为一个或多个bean提供默认定义的方法。如果启用了任何配置文件，则默认配置文件不适用。

您可以使用`Environment`上的`setDefaultProfiles()`或者声明性地使用`spring.profiles.default`属性来更改默认配置文件的名称。

#### 1.13.2 `PropertySource` 抽象

Spring 的`Environment`抽象提供了属性源的层级结构上的搜索操作。考虑下面的列表：

```java
ApplicationContext ctx = new GenericApplicationContext();
Environment env = ctx.getEnvironment();
boolean containsMyProperty = env.containsProperty("my-property");
System.out.println("Does my environment contain the 'my-property' property? " + containsMyProperty);
```

在上面的代码片段中，我们看到一种高层次的方法，询问 Spring 是否`my-property`属性已经为当前环境定义。为了回答这个问题，`Environment`对象执行一个 [`PropertySource`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/core/env/PropertySource.html) 对象集合上的搜索操作。一个`PropertySource`是对任何键值对形式的属性源的一个简单的抽象，Spring 的 [`StandardEnvironment`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/core/env/StandardEnvironment.html) 通过两个`PropertySource`对象配置，一个表达JVM系统属性集合（`System.getProperties()`），另一个表示系统环境变量集合（`System.getenv()`）。

> 这些默认的属性源存在于`StandardEnvironment`中，存在于独立安装的应用中。[`StandardServletEnvironment`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/web/context/support/StandardServletEnvironment.html) 添加了额外的默认属性源，包括 servlet 配置和 servlet 上下文参数。它可以有选择地启用 [`JndiPropertySource`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/jndi/JndiPropertySource.html) 。参考相关文档或获取更多细节。

具体来说，当你使用`StandardEnvironment`，调用`env.containsProperty("my-property")`返回`true`，如果一个`my-property`系统属性或者`my-property`环境变量存在于运行时中。

> 该搜索是层级化执行的。默认地，系统属性优先级高于环境变量。因此，如果`my-property`属性当调用`env.getProperty("my-property")`调用时被同时设置在两个地方，则系统属性值胜出并被返回。注意，同名属性的值不是合并，而是直接由更高优先级的属性值覆盖。
>
> 对普通的`StandardServletEnvironment`，完整的层级如下，顶层的属性源具有最高的优先级：
>
> 1. ServletConfig 参数 (如果适用 — 比如，在 `DispatcherServlet` 上下文中)
> 2. ServletContext 参数 (web.xml 上下文参数实体)
> 3. JNDI 环境变量 (`java:comp/env/` 实体)
> 4. JVM 系统属性 (`-D` 命令行参数)
> 5. JVM 系统环境 (操作系统环境变量)

最重要的是，整个机制是可配置的。您可能希望将自定义的属性源集成到此搜索中。为此，实现并实例化您自己的`PropertySource`并将其添加到当前`Environment`的`PropertySources`集合中。以下示例显示了如何执行此操作：

```java
ConfigurableApplicationContext ctx = new GenericApplicationContext();
MutablePropertySources sources = ctx.getEnvironment().getPropertySources();
sources.addFirst(new MyPropertySource());
```

在上面的代码中，添加了`MyPropertySource`，在搜索中具有最高优先级。如果它包含`my-property`属性，则检测并返回该属性，优先于任何其他`PropertySource`中的任何`my-property`属性。[`MutablePropertySources`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/core/env/MutablePropertySources.html) API暴露了一些允许精确操作属性源集的方法。

#### 1.13.3 使用`@PropertySource`

[`@PropertySource`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/context/annotation/PropertySource.html) 注解提供了一种方便而且声明式的机制来向 Spring `Environment`中添加`PropertySource`。

给定名为`app.properties`的文件包含键值对`testbean.name=myTestBean`，下面的`@Configuration`类使用`@PropertySource`，这种方式调用`testBean.getName()`返回`myTestBean`：

```java
@Configuration
@PropertySource("classpath:/com/myco/app.properties")
public class AppConfig {

    @Autowired
    Environment env;

    @Bean
    public TestBean testBean() {
        TestBean testBean = new TestBean();
        testBean.setName(env.getProperty("testbean.name"));
        return testBean;
    }
}
```

出现在 `@PropertySource` 资源位置中任何 `${…}` 占位符基于已经注册到当前环境中的属性源集合被解析，如下面例子所示：

```java
@Configuration
@PropertySource("classpath:/com/${my.placeholder:default/path}/app.properties")
public class AppConfig {

    @Autowired
    Environment env;

    @Bean
    public TestBean testBean() {
        TestBean testBean = new TestBean();
        testBean.setName(env.getProperty("testbean.name"));
        return testBean;
    }
}
```

假设`my.placeholder`存在于已注册的其中一个属性源中（例如，系统属性或环境变量），则占位符将解析为相应的值。如果没有，那么`default/path`用作默认值。如果未指定缺省值且无法解析属性，则抛出`IllegalArgumentException`。

> 根据Java 8惯例，`@PropertySource`注解是可重复的。但是，所有这些`@PropertySource`注解都需要在同一级别声明，可以直接在配置类上声明，也可以在同一个自定义注解中作为元注解声明。不建议混合直接注解和元注解，因为直接注解有效地覆盖了元注解。

#### 1.13.4 语句中的占位符解析

从历史上看，元素中占位符的值只能基于JVM系统属性或环境变量进行解析。不过如今已不再是这种情况。因为`Environment`抽象集成在整个容器中，所以很容易通过它来解决占位符的解析。 这意味着您可以以任何您喜欢的方式配置解析过程。您可以更改搜索系统属性和环境变量的优先级，或完全删除它们。您也可以根据需要将自己的属性源添加到混合中。

具体而言，无论`customer`属性在哪里定义，只要在`Environment`中可以使用它，以下语句就可以工作：

```xml
<beans>
    <import resource="com/bank/service/${customer}-config.xml"/>
</beans>
```

### 1.14 注册 `LoadTimeWeaver`

Spring使用`LoadTimeWeaver`在类加载到Java虚拟机（JVM）时动态转换类。

要启用加载时编织，可以将`@EnableLoadTimeWeaving`添加到一个`@Configuration`类中，如以下示例所示：

```java
@Configuration
@EnableLoadTimeWeaving
public class AppConfig {
}
```

或者，对于XML配置，您可以使用`context:load-time-weaver`元素：

```xml
<beans>
    <context:load-time-weaver/>
</beans>
```

一旦为`ApplicationContext`配置，那个`ApplicationContext`中的任何bean都可以实现`LoadTimeWeaverAware`，从而接收对加载时编织器实例的引用。这与 [Spring的JPA支持](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/data-access.html#orm-jpa) 结合使用时特别有用。加载时编织可能是JPA类转换所必需的。有关更多详细信息，请参阅[`LocalContainerEntityManagerFactoryBean`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/orm/jpa/LocalContainerEntityManagerFactoryBean.html) 文档。有关AspectJ加载时编织的更多信息，请参阅[Spring Framework中使用AspectJ进行加载时编织](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-aj-ltw) 。

### 1.15 `ApplicationContext`的附加功能

如在 [章节介绍](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans) 中所述， `org.springframework.beans.factory` 包提供了基本的管理和操作 beans 的功能，包括编程方式。`org.springframework.context` 包添加了[`ApplicationContext`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/context/ApplicationContext.html) 接口，扩展了`BeanFactory`接口，同时继承了其它接口来通过面向应用框架的方式提供额外的功能性。很多人采用完全的声明式形式使用`ApplicationContext`，而不是通过编程方式创建它，而是依赖于`ContextLoader`等支持类来自动实例化`ApplicationContext`，作为Java EE Web应用程序正常启动过程的一部分。

要以更加面向框架的方式增强`BeanFactory`的功能性，`org.springframework.context`包也提供了下面的功能：

- 通过`MessageSource`接口访问i18n风格的消息。
- 通过`ResourceLoader`接口访问URL和文件等资源。
- 事件发布，即通过使用`ApplicationEventPublisher`接口实现`ApplicationListener`接口的bean。
- 加载多个（分层）上下文，让每个上下文通过`HierarchicalBeanFactory`接口聚焦于一个特定层，例如应用程序的Web层。


#### 1.15.1 使用`MessageSource`进行国际化

`ApplicationContext`接口还继承了名为`MessageSource`的接口，因而，提供了国际化（i18n）功能。Spring 还提供了`HierarchicalMessageSource`接口，该接口可以杰斯消息层级结构。综上所述，这些接口提供了 Spring 有效消息解析所需要的基础功能。这些接口定义的方法包括：

- `String getMessage(String code, Object[] args, String default, Locale loc)`: 从`MessageSource`获取消息的基本方法。如果特定语言的消息没有找到，则使用默认消息。传入的任何参数都会编程替换值，使用标准类库提供的`MessageFormat`功能。
- `String getMessage(String code, Object[] args, Locale loc)`: 与上面的方法基本相同，但有一点不同：无法指定默认消息。如果找不到默认消息，则抛出`NoSuchMessageException`。
- `String getMessage(MessageSourceResolvable resolvable, Locale locale)`: 上述方法中使用的所有属性也包装在名为`MessageSourceResolvable`的类中，您可以将该类与此方法一起使用。

加载`ApplicationContext`时，它会自动搜索在上下文中定义的`MessageSource` bean。该bean必须具有名称`messageSource`。如果找到这样的bean，则对前面方法的所有调用都被委托给消息源。如果未找到任何消息源，`ApplicationContext`将尝试查找包含具有相同名称的bean的父类。如果是，则将该bean用作`MessageSource`。如果`ApplicationContext`仍然找不到任何消息源，则会实例化一个空的`DelegatingMessageSource`，以便能够接受对上面定义的方法的调用。

Spring 提供了两种`MessageSource`实现，`ResourceBundleMessageSource`和`StaticMessageSource`，两者都实现了`HierarchicalMessageSource`以便嵌套消息源。`StaticMessageSource`很少使用，不过它提供了编程方式向消息源添加消息的方法。下面的例子展示了`ResourceBundleMessageSource`：

```xml
<beans>
    <bean id="messageSource"
            class="org.springframework.context.support.ResourceBundleMessageSource">
        <property name="basenames">
            <list>
                <value>format</value>
                <value>exceptions</value>
                <value>windows</value>
            </list>
        </property>
    </bean>
</beans>
```

这个例子假定你在类路径下定义了三个资源包，名为`format`、`exception`和`windows`。任何涉及到消息的请求都会以 JDK 标准方式被处理，通过`ResourceBundle`对象来解析消息。为了举例子，假定两个资源包文件内容如下：

```
# in format.properties
message=Alligators rock!
```

```
# in exceptions.properties
argument.required=The {0} argument is required.
```

下面的例子展示了一个执行`MessageSource`功能的程序。记住所有的`ApplicationContext`实现同时也是`MessageSource`实现，因此可以被转化为`MessageSource`接口：

```java
public static void main(String[] args) {
    MessageSource resources = new ClassPathXmlApplicationContext("beans.xml");
    String message = resources.getMessage("message", null, "Default", null);
    System.out.println(message);
}
```

上面的程序输入如下：

```
Alligators rock!
```

总而言之，`MessageSource`在名为`beans.xml`的文件中定义，该文件存在于类路径的根目录中。`messageSource` bean定义通过其`basenames`属性引用许多资源包。以列表形式传递给`basenames`属性的三个文件名作为类路径根目录下的文件存在，分别称为`format.properties`，`exceptions.properties`和`windows.properties`。

下面的例子展示了传递给消息查找的参数。这些参数被转化为`String`对象并插入查找消息中的占位符中：

```xml
<beans>

    <!-- this MessageSource is being used in a web application -->
    <bean id="messageSource" class="org.springframework.context.support.ResourceBundleMessageSource">
        <property name="basename" value="exceptions"/>
    </bean>

    <!-- lets inject the above MessageSource into this POJO -->
    <bean id="example" class="com.something.Example">
        <property name="messages" ref="messageSource"/>
    </bean>

</beans>
```

```java
public class Example {

    private MessageSource messages;

    public void setMessages(MessageSource messages) {
        this.messages = messages;
    }

    public void execute() {
        String message = this.messages.getMessage("argument.required",
            new Object [] {"userDao"}, "Required", null);
        System.out.println(message);
    }
}
```

`execute()` 方法调用输出：

```
The userDao argument is required.
```

关于国际化（“i18n”），Spring的各种`MessageSource`实现遵循与标准JDK `ResourceBundle`相同的区域设置解析和回退规则。简而言之，继续前面定义的示例`messageSource`，如果要根据British（`en-GB`）语言环境解析消息，则应分别创建名为`format_en_GB.properties`，`exceptions_en_GB.properties`和`windows_en_GB.properties`的文件。

通常，区域设置解析由应用程序的周围环境管理。在以下示例中，手动指定解析（英国）消息的区域设置：

```
# in exceptions_en_GB.properties
argument.required=Ebagum lad, the {0} argument is required, I say, required.
```

```java
public static void main(final String[] args) {
    MessageSource resources = new ClassPathXmlApplicationContext("beans.xml");
    String message = resources.getMessage("argument.required",
        new Object [] {"userDao"}, "Required", Locale.UK);
    System.out.println(message);
}
```

上面程序的输出：

```
Ebagum lad, the 'userDao' argument is required, I say, required.
```

您还可以使用`MessageSourceAware`接口获取对已定义的任何`MessageSource`的引用。在创建和配置bean时，应用程序上下文的`MessageSource`会注入实现`MessageSourceAware`接口的`ApplicationContext`中定义的任何bean。

> 作为`ResourceBundleMessageSource`的替代，Spring提供了一个`ReloadableResourceBundleMessageSource`类。此变体支持相同的包文件格式，但比基于标准JDK的`ResourceBundleMessageSource`实现更灵活。特别是，它允许从任何Spring资源位置（不仅从类路径）读取文件，并支持属性文件的热重新加载（同时有效地缓存它们）。有关详细信息，请参阅`ReloadableResourceBundleMessageSource`文档。

#### 1.15.2 标准事件和自定义事件

`ApplicationContext`中的事件处理通过`ApplicationEvent`类和`ApplicationListener`接口提供。如果一个实现了`ApplicationListener`接口的 bean 部署到上下文中，每当有`ApplicationEvent`被发布到`ApplicationContext`中时，该 bean 就会被通知到。本质上，这就是一个标准的观察者设计模式。

> 在 Spring 4.2 中，事件基础设施已经被显著改进，提供了一个 [annotation-based model](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#context-functionality-events-annotation) 和发布任意事件的能力 (也就是说，事件对象甚至都不需要扩展自 `ApplicationEvent`)。当这种对象被发布，Spring 会将它包装成一个事件。

下表描述了 Spring 提供的标准事件：

| Event                   | Explanation                              |
| ----------------------- | ---------------------------------------- |
| `ContextRefreshedEvent` | 初始化或刷新`ApplicationContext`时发布（例如，通过使用`ConfigurableApplicationContext`接口上的`refresh()`方法）。这里，“已初始化”意味着加载所有bean，检测并激活后处理器bean，预先实例化单例，并且`ApplicationContext`对象已准备好使用。只要上下文尚未关闭，而所选的`ApplicationContext`实际支持这种“热”刷新，就可以多次触发刷新。例如，`XmlWebApplicationContext`支持热刷新，但`GenericApplicationContext`不支持。 |
| `ContextStartedEvent`   | 通过使用`ConfigurableApplicationContext`接口上的`start()`方法启动`ApplicationContext`时发布。这里，“已启动”表示所有`Lifecycle`bean都会收到明确的启动信号。通常，此信号用于在显式停止后重新启动Bean，但它也可用于启动尚未为自动启动配置的组件（例如，尚未在初始化时启动的组件）。 |
| `ContextStoppedEvent`   | 通过使用`ConfigurableApplicationContext`接口上的`stop()`方法停止`ApplicationContext`时发布。这里，“已停止”表示所有`Lifecycle`bean都会收到明确的停止信号。可以通过`start()`调用重新启动已停止的上下文。 |
| `ContextClosedEvent`    | 通过使用`ConfigurableApplicationContext`接口上的`close()`方法关闭`ApplicationContext`时发布。这里，“关闭”意味着所有单例bean都被销毁。封闭的环境达到了生命的终点。它无法刷新或重新启动。 |
| `RequestHandledEvent`   | 一个特定于Web的事件，告诉所有bean已经为HTTP请求提供服务。请求完成后发布此事件。此事件仅适用于使用Spring的`DispatcherServlet`的Web应用程序。 |

你还可以创建并发布自定义事件，下面的例子展示了一个简单的类，它扩展了 Spring 的`ApplicationEvent`基类：

```java
public class BlackListEvent extends ApplicationEvent {

    private final String address;
    private final String content;

    public BlackListEvent(Object source, String address, String content) {
        super(source);
        this.address = address;
        this.content = content;
    }

    // accessor and other methods...
}
```

为了发布一个自定义`ApplicationEvent`，请调用`ApplicationEventPublisher`上的`publishEvent`方法。典型地，这通过创建一个实现`ApplicationEventPublisherAware`接口并将其注册为 Spring 的 bean 的方式来实现。下面的例子展示了这样一个类：

```java
public class EmailService implements ApplicationEventPublisherAware {

    private List<String> blackList;
    private ApplicationEventPublisher publisher;

    public void setBlackList(List<String> blackList) {
        this.blackList = blackList;
    }

    public void setApplicationEventPublisher(ApplicationEventPublisher publisher) {
        this.publisher = publisher;
    }

    public void sendEmail(String address, String content) {
        if (blackList.contains(address)) {
            publisher.publishEvent(new BlackListEvent(this, address, content));
            return;
        }
        // send email...
    }
}
```

在配置时，Spring容器检测到`EmailService`实现`ApplicationEventPublisherAware`并自动调用`setApplicationEventPublisher()`。实际上，传入的参数是Spring容器本身。您正在通过其`ApplicationEventPublisher`接口与应用程序上下文进行交互。

要接收自定义`ApplicationEvent`，您可以创建一个实现`ApplicationListener`的类并将其注册为Spring bean。 以下示例显示了这样一个类：

```java
public class BlackListNotifier implements ApplicationListener<BlackListEvent> {

    private String notificationAddress;

    public void setNotificationAddress(String notificationAddress) {
        this.notificationAddress = notificationAddress;
    }

    public void onApplicationEvent(BlackListEvent event) {
        // notify appropriate parties via notificationAddress...
    }
}
```

请注意，`ApplicationListener`通常使用自定义事件的类型进行参数化（前面示例中为`BlackListEvent`）。这意味着`onApplicationEvent()`方法可以保持类型安全，从而避免任何向下转换的需要。您可以根据需要注册任意数量的事件侦听器，但请注意，默认情况下，事件侦听器会同步接收事件。这意味着`publishEvent()`方法将阻塞，直到所有侦听器都已完成对事件的处理。这种同步和单线程方法的一个优点是，当侦听器接收到事件时，如果事务上下文可用，它将在发布者的事务上下文内运行。如果需要另一个事件发布策略，请参阅Spring的 [`ApplicationEventMulticaster`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/context/event/ApplicationEventMulticaster.html) 接口的javadoc。

以下示例显示了用于注册和配置上述每个类的bean定义：

```xml
<bean id="emailService" class="example.EmailService">
    <property name="blackList">
        <list>
            <value>known.spammer@example.org</value>
            <value>known.hacker@example.org</value>
            <value>john.doe@example.org</value>
        </list>
    </property>
</bean>

<bean id="blackListNotifier" class="example.BlackListNotifier">
    <property name="notificationAddress" value="blacklist@example.org"/>
</bean>
```

总而言之，当调用`emailService` bean的`sendEmail()`方法时，如果有任何应列入黑名单的电子邮件消息，则会发布`BlackListEvent`类型的自定义事件。`blackListNotifier` bean注册为`ApplicationListener`，并接收`BlackListEvent`，此时它可以通知相关方。

> Spring的事件机制是为在同一应用程序上下文中的Spring bean之间的简单通信而设计的。但是，对于更复杂的企业集成需求，单独维护的 [Spring Integration](https://projects.spring.io/spring-integration/) 项目为构建基于众所周知的Spring编程模型的轻量级，[pattern-oriented](https://www.enterpriseintegrationpatterns.com/)，事件驱动的体系结构提供了完整的支持。

##### 基于注解的事件监听器

从Spring 4.2开始，您可以使用`EventListener`注解在托管bean的任何公共方法上注册事件侦听器。`BlackListNotifier`可以重写如下：

```java
public class BlackListNotifier {

    private String notificationAddress;

    public void setNotificationAddress(String notificationAddress) {
        this.notificationAddress = notificationAddress;
    }

    @EventListener
    public void processBlackListEvent(BlackListEvent event) {
        // notify appropriate parties via notificationAddress...
    }
}
```

方法签名再次声明它侦听的事件类型，但这次使用灵活的名称并且没有实现特定的侦听器接口。只要实际事件类型在其实现层次结构中解析通用参数，也可以通过泛型缩小事件类型范围。

如果您的方法应该监听多个事件，或者您不想根据参数进行定义，那么也可以在注解本身上指定事件类型。以下示例显示了如何执行此操作：

```java
@EventListener({ContextStartedEvent.class, ContextRefreshedEvent.class})
public void handleContextStart() {
    ...
}
```

还可以通过使用定义 [`SpEL`expression](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#expressions) 的注解的`condition`属性来添加额外的运行时过滤，该属性应匹配以实际调用特定事件的方法。

以下示例显示了仅当事件的`content`属性等于`my-event`时，才能重写我们的通知程序以进行调用：

```java
@EventListener(condition = "#blEvent.content == 'my-event'")
public void processBlackListEvent(BlackListEvent blEvent) {
    // notify appropriate parties via notificationAddress...
}
```

每个`SpEL`表达式都针对专用上下文进行评估。下表列出了可用于上下文的项目，以便您可以将它们用于条件事件处理：

| Name            | Location           | Description                              | Example                                  |
| --------------- | ------------------ | ---------------------------------------- | ---------------------------------------- |
| Event           | root object        | 实际的 `ApplicationEvent` 。                 | `#root.event`                            |
| Arguments array | root object        | 用来调用目标的参数（作为数组）。                         | `#root.args[0]`                          |
| *Argument name* | evaluation context | 所有方法参数的名称。如果，由于某种原因，该名称不可用（比如，不存在调试信息），该参数名称也可以在`#a<#arg>`下面找到，其中`#arg`代表参数下标（从0开始）。 | `#blEvent` 或者 `#a0` (你也可以使用 `#p0` 或者 `#p<#arg>`记号作为别名) |

请注意，即使您的方法签名实际引用已发布的任意对象， `#root.event` 也允许您访问基础事件。

如果您需要发布作为处理其他事件的结果的事件，则可以更改方法签名以返回应发布的事件，如以下示例所示：

```java
@EventListener
public ListUpdateEvent handleBlackListEvent(BlackListEvent event) {
    // notify appropriate parties via notificationAddress and
    // then publish a ListUpdateEvent...
}
```

> [异步监听器](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#context-functionality-events-async) 不支持此功能。

这个新方法为上面方法处理的每个`BlackListEvent`发布一个新的`ListUpdateEvent`。如果需要发布多个事件，则可以返回事件集合。

##### 异步监听器

如果你希望特定监听器异步处理事件，可以复用 [regular `@Async` support](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/integration.html#scheduling-annotation-support-async) 。下面是例子：

```java
@EventListener
@Async
public void processBlackListEvent(BlackListEvent event) {
    // BlackListEvent is processed in a separate thread
}
```

使用异步监听器时注意以下限制：

- 如果事件监听器抛出 `Exception`，它并不会传播给调用者。参考 `AsyncUncaughtExceptionHandler` 获取更多细节。
- 这种事件监听器不能发送回复。如果你需要发送另外一个事件作为某个事件处理的结果，注入[`ApplicationEventPublisher`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/aop/interceptor/AsyncUncaughtExceptionHandler.html) 来手动发送它。

##### 监听器排序

如果需要在另一个侦听器之前调用一个侦听器，则可以将`@Order`注解添加到方法声明中，如以下示例所示：

```java
@EventListener
@Order(42)
public void processBlackListEvent(BlackListEvent event) {
    // notify appropriate parties via notificationAddress...
}
```

##### 泛型事件

您还可以使用泛型来进一步定义事件的结构。考虑使用`EntityCreatedEvent <T>`，其中`T`是创建的实际实体的类型。例如，您可以创建以下侦听器定义以仅接收`Person`的`EntityCreatedEvent`：

```java
@EventListener
public void onPersonCreated(EntityCreatedEvent<Person> event) {
    ...
}
```

由于类型擦除，仅当被触发的事件解析了事件侦听器过滤器的泛型参数时（即类`PersonCreatedEvent`类扩展了`EntityCreatedEvent <Person> {...}`），这才起作用。

在某些情况下，如果所有事件都遵循相同的结构，这可能会变得相当繁琐（前面示例中的事件应该如此）。在这种情况下，您可以实现`ResolvableTypeProvider`来在超出运行时环境提供的范围时指导框架。以下事件显示了如何执行此操作：

```java
public class EntityCreatedEvent<T> extends ApplicationEvent implements ResolvableTypeProvider {

    public EntityCreatedEvent(T entity) {
        super(entity);
    }

    @Override
    public ResolvableType getResolvableType() {
        return ResolvableType.forClassWithGenerics(getClass(), ResolvableType.forInstance(getSource()));
    }
}
```

> 这不仅可以用于 `ApplicationEvent` ，还可以用于任何你作为事件发送的对象。

#### 1.15.3 低级资源的方便访问

为了优化对应用上下文的理解和使用，你应该熟悉 Spring 的`Resource`抽象，如 [Resources](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources) 中所描述。

一个应用上下文是一个`ResourceLoader`，它可以被用来加载`Resource`对象。`Resource`对象本质上是功能丰富版本的 JDK `java.net.URL`类。事实上，`Resource`的实现适当地包装了一个`java.net.URL`实例。`Resource`对象能够从几乎任何地方透明地获取低级资源，包括从类路径、文件系统位置、任何以标准 URL 或者其它变体描述的位置。如果资源位置字符串是一个简单路径，没有任何特殊前缀，那么这些资源的来源就是特定的，而且适合于实际应用的上下文类型。

你可以配置一个部署到应用上下文中的 bean 来实现特殊的回调接口，`ResourceLoaderAware`，会在初始化时刻被自动回调，此时应用上下文本身被作为`ResourceLoader`被传入。你也可以暴露`Resource`类型的属性，以便访问静态资源。它们像其它所有属性一样被注入。您可以为这些`Resource`属性指定简单的`String`路径，并在部署Bean时依赖从这些文本字符串到实际`Resource`对象的自动转换。

提供给`ApplicationContext`构造器的位置路径是实际的资源字符串，或者是其简单形式，根据特定的上下文实现，各种形式都会被恰当地处理。比如，`ClassPathXmlApplicationContext`将简单位置路径作为类路径位置。你也可以在位置路径（资源字符串）上使用特定的前缀来强制定义从类路径或者 URL 加载，而不管实际的上下文类型。

#### 1.15.4 Web 应用的 ApplicationContext 方便实例化

您可以使用例如`ContextLoader`以声明方式创建`ApplicationContext`实例。当然，您也可以使用其中一个`ApplicationContext`实现以编程方式创建`ApplicationContext`实例。

您可以使用`ContextLoaderListener`注册`ApplicationContext`，如以下示例所示：

```xml
<context-param>
    <param-name>contextConfigLocation</param-name>
    <param-value>/WEB-INF/daoContext.xml /WEB-INF/applicationContext.xml</param-value>
</context-param>

<listener>
    <listener-class>org.springframework.web.context.ContextLoaderListener</listener-class>
</listener>
```

侦听器检查`contextConfigLocation`参数。如果参数不存在，则侦听器将`/WEB-INF/applicationContext.xml`用作默认值。当参数确实存在时，侦听器使用预定义的分隔符（逗号，分号和空格）分隔`String`，并将值用作搜索应用程序上下文的位置。同时还支持Ant样式的路径模式。示例是`/WEB-INF/*Context.xml`（对于名称以`Context.xml`结尾且位于`WEB-INF`目录中的所有文件）和`/WEB-INF/**/*Context.xml`（对于所有 `WEB-INF`的任何子目录中的此类文件）。

#### 1.15.5 以 Java EE RAR 文件形式部署 Spring `ApplicationContext`

可以将Spring `ApplicationContext`部署为RAR文件，将上下文及其所有必需的bean类和库JAR封装在Java EE RAR部署单元中。这相当于引导能够访问Java EE服务器设施的独立`ApplicationContext`（仅托管在Java EE环境中）。RAR部署是部署无头WAR文件的一种更自然的替代方案 - 实际上是一个没有任何HTTP入口点的WAR文件，仅用于在Java EE环境中引导Spring `ApplicationContext`。

RAR部署非常适用于不需要HTTP入口点但仅包含消息端点和预定作业的应用程序上下文。在这样的上下文中，Bean可以使用应用程序服务器资源，例如JTA事务管理器和JNDI绑定的JDBC `DataSource`实例以及JMS `ConnectionFactory`实例，并且还可以通过Spring的标准事务管理以及JNDI和JMX支持工具向平台的JMX服务器注册。应用程序组件还可以通过Spring的`TaskExecutor`抽象与应用程序服务器的JCA `WorkManager`进行交互。

有关RAR部署中涉及的配置详细信息，请参阅 [`SpringContextResourceAdapter`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/jca/context/SpringContextResourceAdapter.html) 类的javadoc。

对于将Spring `ApplicationContext`简单部署为Java EE RAR文件：

1. 将所有应用程序类打包到一个RAR文件（这是一个具有不同文件扩展名的标准JAR文件）。将所有必需的库JAR添加到RAR存档的根目录中。添加`META-INF/ra.xml`部署描述符（如 [javadoc for `SpringContextResourceAdapter`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/jca/context/SpringContextResourceAdapter.html) 所示）和相应的Spring XML bean定义文件（通常是`META-INF/applicationContext.xml`）。
2. 将生成的RAR文件放入应用程序服务器的部署目录中。

> 这种RAR部署单元通常是独立的。它们不会将组件暴露给外部世界，甚至不会暴露给同一应用程序的其他模块。与基于RAR的`ApplicationContext`的交互通常通过与其他模块共享的JMS目标进行。例如，基于RAR的`ApplicationContext`还可以调度一些作业或对文件系统（或类似物）中的新文件作出反应。如果它需要允许来自外部的同步访问，它可以（例如）导出RMI端点，这可以由同一台机器上的其他应用程序模块使用。

### 1.16 `BeanFactory`

`BeanFactory` API 提供了 Spring IoC 功能的底层基础。它确定的契约被广泛用于与 Spring 的其它部分或者相关的第三方框架集成，同时它的`DefaultListableBeanFactory`实现是更高层次的`GenericApplicationContext`容器中的一个关键代理。

`BeanFactory`以及相关的接口（比如`BeanFactoryAware`，`InitializingBean`，`DisposableBean`）都是其它框架组件的重要的集成点。不需要任何注解甚至是反射，它们允许容器和它的组件之间非常有效的交叉。应用层面的 beans 可以使用相同的回调接口，但是通常更倾向于使用声明式依赖注，要么通过注解，要么通过编程式配置。

注意，核心`BeanFactory` API 层级和它的`DefaultListableBeanFactory`实现不会对配置格式或者注解应用到的所有组件做任何假定。所有这些风格都通过扩展（例如`XmlBeanDefinitionReader`和`AutowiredAnnotationBeanPostProcessor`）进行，并作为核心元数据表示在共享`BeanDefinition`对象上运行。这是使Spring的容器如此灵活和可扩展的本质。

#### 1.16.1 `BeanFactory` 还是 `ApplicationContext`?

本节介绍`BeanFactory`和`ApplicationContext`容器级别之间的差异以及对引导的影响。

您应该使用`ApplicationContext`，除非您有充分的理由不这样做，使用`GenericApplicationContext`及其子类`AnnotationConfigApplicationContext`作为自定义引导的常见实现。这些是Spring用于所有常见目的的核心容器的主要入口点：加载配置文件，触发类路径扫描，以编程方式注册bean定义和带注解的类，以及（从5.0开始）注册功能bean定义。

因为`ApplicationContext`包含`BeanFactory`的所有功能，所以通常建议使用`BeanFactory`，除了需要完全控制bean处理的场景之外。在`ApplicationContext`（例如`GenericApplicationContext`实现）中，按惯例检测到几种bean（即，通过bean名称或bean类型 - 特别是后处理器），而普通的`DefaultListableBeanFactory`对任何特殊bean都是不可知的。

对于许多扩展容器功能，例如注解处理和AOP代理， [`BeanPostProcessor` extension point](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-extension-bpp) 是必不可少的。如果仅使用普通的`DefaultListableBeanFactory`，则默认情况下不会检测到并激活此类后处理器。这种情况可能令人困惑，因为您的bean配置实际上没有任何问题。相反，在这种情况下，容器需要通过额外的设置完全自举。

下表列出了`BeanFactory`和`ApplicationContext`接口和实现提供的特性：

| Feature                                  | `BeanFactory` | `ApplicationContext` |
| ---------------------------------------- | ------------- | -------------------- |
| Bean instantiation/wiring                | Yes           | Yes                  |
| Integrated lifecycle management          | No            | Yes                  |
| Automatic `BeanPostProcessor` registration | No            | Yes                  |
| Automatic `BeanFactoryPostProcessor` registration | No            | Yes                  |
| Convenient `MessageSource` access (for internalization) | No            | Yes                  |
| Built-in `ApplicationEvent` publication mechanism | No            | Yes                  |

要使用`DefaultListableBeanFactory`显式注册bean后处理器，您需要以编程方式调用`addBeanPostProcessor`，如以下示例所示：

```java
DefaultListableBeanFactory factory = new DefaultListableBeanFactory();
// populate the factory with bean definitions

// now register any needed BeanPostProcessor instances
factory.addBeanPostProcessor(new AutowiredAnnotationBeanPostProcessor());
factory.addBeanPostProcessor(new MyBeanPostProcessor());

// now start using the factory
```

要将`BeanFactoryPostProcessor`应用于普通的`DefaultListableBeanFactory`，需要调用其`postProcessBeanFactory`方法，如以下示例所示：

```java
DefaultListableBeanFactory factory = new DefaultListableBeanFactory();
XmlBeanDefinitionReader reader = new XmlBeanDefinitionReader(factory);
reader.loadBeanDefinitions(new FileSystemResource("beans.xml"));

// bring in some property values from a Properties file
PropertyPlaceholderConfigurer cfg = new PropertyPlaceholderConfigurer();
cfg.setLocation(new FileSystemResource("jdbc.properties"));

// now actually do the replacement
cfg.postProcessBeanFactory(factory);
```

在这两种情况下，显式注册步骤都不方便，这就是为什么各种`ApplicationContext`变体优先于Spring支持的应用程序中的普通`DefaultListableBeanFactory`，尤其是在典型企业设置中依赖`BeanFactoryPostProcessor`和`BeanPostProcessor`实例来扩展容器功能时。

> `AnnotationConfigApplicationContext`具有注册的所有通用注释后处理器，并且可以通过配置注解（例如`@EnableTransactionManagement`）引入其他处理器。在Spring的基于注解的配置模型的抽象级别，bean后处理器的概念变成仅仅是内部容器细节。

## 2. 资源

本章节介绍 Spring 如何处理资源以及如何在 Spring 中使用资源。包含下列主题：

- [介绍](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-introduction)
- [Resource 接口](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-resource)
- [内建 Resource 实现](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations)
- [`ResourceLoader`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-resourceloader)
- [`ResourceLoaderAware` 接口](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-resourceloaderaware)
- [Resources 作为依赖](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-as-dependencies)
- [应用上下文和资源路径](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-app-ctx)

### 2.1  介绍

Java 的标准`java.net.URL`类和用来处理各种 URL 前缀的标准处理器，很不幸，并不非常能够胜任对所有低层次资源的访问。例如，没有标准化的 URL 实现可用于访问需要从类路径或相对于`ServletContext`获取的资源。虽然可以为专用的 URL 前缀注册新的处理程序（类似于`http:`这样的前缀的现有处理程序），但这通常非常复杂，并且 URL 接口仍然缺少一些理想的功能，例如检查被指向的资源存在的方法。

### 2.2  Resource 接口

Spring的`Resource`接口旨在成为一个更有能力的接口，用于抽象对低级资源的访问。以下清单显示了`Resource`接口定义：

```java
public interface Resource extends InputStreamSource {

    boolean exists();

    boolean isOpen();

    URL getURL() throws IOException;

    File getFile() throws IOException;

    Resource createRelative(String relativePath) throws IOException;

    String getFilename();

    String getDescription();

}
```

正如`Resource`接口的定义所示，它扩展了`InputStreamSource`接口。以下清单显示了`InputStreamSource`接口的定义：

```java
public interface InputStreamSource {

    InputStream getInputStream() throws IOException;

}
```

`Resource` 接口的最重要的方法包括：

- `getInputStream()`: 定位并打开资源，返回读取资源的`InputStream`。每次调用都会返回一个新的`InputStream`。关闭这些流是方法调用者的责任。
- `exists()`: 返回一个 `boolean` 值表示该资源的物理形式是否确实存在。
- `isOpen()`: 返回一个 `boolean` 值表示该资源是否使用一个打开的流处理。如果返回`true`，则该`InputStream`就不能被多次读取，只能读取一次之后就关闭以防止资源泄漏。对所有常规资源实现，返回`false`，但是`InputStreamResource`除外。
- `getDescription()`: 返回此资源的描述，用于处理资源时的错误输出。这通常是完全限定的文件名或资源的实际URL。

其它方法允许你获取表示资源的实际的`URL`或者`File`对象（如果底层实现兼容并支持该功能）。

当需要资源时，Spring 自身广泛使用了`Resource`抽象，作为很多方法签名的参数类型。一些 Spring APIs 中的其它方法（比如各种`ApplicationContext`实现的构造器）使用一个`String`以简单形式来创建适用于上下文实现的`Resource`，或者通过`String`路径上的特殊前缀，让调用者指定必须创建和使用的特定`Resource`。

虽然Spring中大量使用了`Resource`接口，但在自己的代码中使用它作为通用实用程序类非常有用，用于访问资源，即使你的代码不知道或不关心任何其他 Spring 组件。虽然这会将您的代码耦合到 Spring，但它实际上只将它耦合到这一小组实用程序类中，这些实用程序类可以作为`URL`的更有能力的替代品，并且可以被认为等同于您将用于此目的的任何其他库。

> `Resource`抽象不会替代功能，它会尽可能包装功能。比如，`UrlResource`包装 URL 并使用包装后的`URL`来完成它的工作。

### 2.3 内建 Resource 实现

Spring 包含下列 `Resource` 实现：

- [`UrlResource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations-urlresource)
- [`ClassPathResource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations-classpathresource)
- [`FileSystemResource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations-filesystemresource)
- [`ServletContextResource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations-servletcontextresource)
- [`InputStreamResource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations-inputstreamresource)
- [`ByteArrayResource`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-implementations-bytearrayresource)

#### 2.3.1 `UrlResource`

`UrlResource`包装`java.net.URL`，可用于访问通常可通过 URL 访问的任何对象，例如文件，HTTP目标，FTP目标等。所有 URL 都具有标准化的字符串表示，以便使用适当的标准化前缀来指示另一个URL类型。这包括 `file:` 用于访问文件系统路径，`http:` 用于通过HTTP协议访问资源，`ftp:`用于通过FTP访问资源，以及其他。

`UrlResource`由Java代码通过显式使用`UrlResource`构造函数创建，但通常在调用采用`String`参数表示路径的API方法时隐式创建。对于后一种情况，JavaBeans `PropertyEditor`最终决定要创建哪种类型的`Resource`。如果路径字符串包含众所周知的（对于它）前缀（例如 `classpath:`)，则会为该前缀创建适当的专用 `Resource` 。但是，如果它无法识别前缀，则假定该字符串是标准URL字符串并创建`UrlResource`。

#### 2.3.2 `ClassPathResource`

此类表示一个应该从类路径获取的资源。它要么使用线程上下文类加载器，一个给定的类加载器，或者一个给定的用于资源加载的类。

如果类路径资源留驻在文件系统中，`Resource`实现支持解析为`java.io.File`。但是当类路径资源位于 jar 包中而尚未解压（被 servlet 引擎或者其他容器或环境）到文件系统中，不支持这种解析。为了解决这个问题，各种`Resource`实现都支持解析为`java.net.URL`。

`ClassPathResource`是由Java代码通过显式使用`ClassPathResource`构造函数创建的，但是当你调用一个带有表示路径的`String`参数的API方法时，通常会隐式创建它。对于后一种情况，JavaBeans`PropertyEditor`在字符串路径上识别特殊前缀`classpath:`，并在这种情况下创建`ClassPathResource`。

#### 2.3.3 `FileSystemResource`

这是一个用于`java.io.File`和`java.nio.file.Path`处理的`Resource`实现。它支持解析为`File`和`URL`。

#### 2.3.4 `ServletContextResource`

这是`ServletContext`资源的`Resource`实现，它解释相关Web应用程序根目录中的相对路径。

它始终支持流访问和 URL 访问，但只有在Web应用程序存档被解压之后且资源实际位于文件系统上时才允许`java.io.File`访问。无论它是解压到在文件系统上还是直接从JAR或其他地方（如数据库）访问，实际上都依赖于Servlet容器。

#### 2.3.5 `InputStreamResource`

`InputStreamResource`是给定`InputStream`的`Resource`实现。只有在没有适用的特定`Resource`实现时才应该使用它。特别是，在可能的情况下，应该优先考虑使用`ByteArrayResource`或任何基于文件的`Resource`实现。

与其他`Resource`实现相比，这是已经打开的资源的描述符。因此，它从`isOpen()`返回`true`。如果需要将资源描述符保留在某处或者需要多次读取流，请不要使用它。

#### 2.3.6 `ByteArrayResource`

这是给定字节数组的`Resource`实现。它为给定的字节数组创建一个`ByteArrayInputStream`。

它对于从任何给定的字节数组加载内容非常有用，而无需使用一次性的`InputStreamResource`。

### 2.4 `ResourceLoader`

`ResourceLoader`接口意味着由可以返回（即加载）`Resource`实例的对象实现。以下清单显示了`ResourceLoader`接口定义：

```java
public interface ResourceLoader {

    Resource getResource(String location);

}
```

所有应用程序上下文都实现了`ResourceLoader`接口。因此，所有应用程序上下文都可用于获取`Resource`实例。

当你在特定的应用程序上下文中调用`getResource()`，并且指定的位置路径没有特定的前缀时，你会得到一个适合于该特定应用程序上下文的`Resource`类型。例如，假设针对`ClassPathXmlApplicationContext`实例执行了以下代码片段：

```java
Resource template = ctx.getResource("some/resource/path/myTemplate.txt");
```

对于`ClassPathXmlApplicationContext`，该代码返回一个`ClassPathResource`。如果针对`FileSystemXmlApplicationContext`实例执行相同的方法，它将返回`FileSystemResource`。对于`WebApplicationContext`，它将返回一个`ServletContextResource`。它同样会为每个上下文返回适当的对象。

因此，您可以以适合特定应用程序上下文的方式加载资源。

另一方面，您可以通过指定特殊的`classpath:`前缀来强制使用`ClassPathResource`，而不管应用程序上下文类型如何，如下例所示：

```java
Resource template = ctx.getResource("classpath:some/resource/path/myTemplate.txt");
```

类似地，您可以通过指定任何标准的`java.net.URL`前缀来强制使用`UrlResource`。以下一对示例使用`file`和`http`前缀：

```java
Resource template = ctx.getResource("file:///some/resource/path/myTemplate.txt");
Resource template = ctx.getResource("https://myhost.com/resource/path/myTemplate.txt");
```

下表总结了将`String`对象转换为`Resource`对象的策略：

| Prefix     | Example                          | Explanation                              |
| :--------- | :------------------------------- | :--------------------------------------- |
| classpath: | `classpath:com/myapp/config.xml` | 从类路径加载。                                  |
| file:      | `file:///data/config.xml`        | 作为 `URL` 从文件系统加载。参考 [`FileSystemResource` Caveats](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#resources-filesystemresource-caveats) 。 |
| http:      | `https://myserver/logo.png`      | 作为 `URL` 加载。                             |
| (none)     | `/data/config.xml`               | 依赖底层的 `ApplicationContext`。              |

### 2.5 `ResourceLoaderAware` 接口

`ResourceLoaderAware`接口是一个特殊的回调接口，它标识希望提供`ResourceLoader`引用的组件。以下清单显示了`ResourceLoaderAware`接口的定义：

```java
public interface ResourceLoaderAware {

    void setResourceLoader(ResourceLoader resourceLoader);
}
```

当一个类实现`ResourceLoaderAware`并被部署到应用程序上下文（作为Spring管理的bean）时，它被应用程序上下文识别为`ResourceLoaderAware`。然后，应用程序上下文调用`setResourceLoader(ResourceLoader)`，将自身作为参数提供（请记住，Spring中的所有应用程序上下文都实现了`ResourceLoader`接口）。

由于`ApplicationContext`是`ResourceLoader`，bean也可以实现`ApplicationContextAware`接口并直接使用提供的应用程序上下文来加载资源。但是，一般来说，最好使用专门的`ResourceLoader`接口，如果这就是你所需要的。代码只能耦合到资源加载接口（可以认为是实用程序接口），而不是整个Spring`ApplicationContext`接口。

在应用程序组件中，您还可以依赖自动装配`ResourceLoader`作为实现`ResourceLoaderAware`接口的替代方法。“传统的”构造函数和`byType`自动装配模式（如 [自动装配协作者](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-factory-autowire) 中所述）能够分别为构造函数参数或 setter 方法参数提供`ResourceLoader`。为了获得更大的灵活性（包括自动装配字段和多参数方法的能力），请考虑使用基于注解的自动装配功能。在这种情况下，只要字段，构造函数或方法带有`@Autowired`注解，`ResourceLoader`就自动注入一个字段，构造函数参数或方法参数，它们需要`ResourceLoader`类型。有关更多信息，请参阅 [使用`@Autowired`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-autowired-annotation) 。

### 2.6  Resources as Dependencies

如果 bean 本身将通过某种动态过程确定并提供资源路径，那么 bean 使用`ResourceLoader`接口加载资源可能是有意义的。例如，考虑加载某种模板，其中所需的特定资源取决于用户的角色。如果资源是静态的，那么完全消除`ResourceLoader`接口的使用是有意义的，让 bean 暴露它需要的`Resource`属性，并期望它们被注入其中。

使得注入这些属性变得微不足道的是，所有应用程序上下文都注册并使用特殊的JavaBeans`PropertyEditor`，它可以将`String`路径转换为`Resource`对象。因此，如果`myBean`具有类型为`Resource`的模板属性，则可以使用该资源的简单字符串进行配置，如以下示例所示：

```xml
<bean id="myBean" class="...">
    <property name="template" value="some/resource/path/myTemplate.txt"/>
</bean>
```

请注意，资源路径没有前缀。因此，由于应用程序上下文本身将被用作`ResourceLoader`，所以资源本身通过`ClassPathResource`，`FileSystemResource`或`ServletContextResource`加载，具体取决于上下文的确切类型。

如果需要强制使用特定的`Resource`类型，则可以使用前缀。以下两个示例显示了如何强制使用`ClassPathResource`和`UrlResource`（后者用于访问文件系统文件）：

```xml
<property name="template" value="classpath:some/resource/path/myTemplate.txt">
<property name="template" value="file:///some/resource/path/myTemplate.txt"/>
```

### 2.7 应用上下文和资源路劲

本节介绍如何使用资源创建应用程序上下文，包括使用XML的快捷方式，如何使用通配符以及其他详细信息。

#### 2.7.1 构建应用上下文

应用程序上下文构造函数（对于特定的应用程序上下文类型）通常将字符串或字符串数组作为资源的位置路径，例如构成上下文定义的XML文件。

当这样的位置路径没有前缀时，从该路径构建并用于加载 bean 定义的特定`Resource`类型取决于并且适合于特定的应用程序上下文。例如，考虑以下示例，它创建一个`ClassPathXmlApplicationContext`：

```java
ApplicationContext ctx = new ClassPathXmlApplicationContext("conf/appContext.xml");
```

bean 定义是从类路径加载的，因为使用了`ClassPathResource`。但是，请考虑以下示例，它创建一个`FileSystemXmlApplicationContext`：

```java
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("conf/appContext.xml");
```

现在，bean 定义是从文件系统位置加载的（在这种情况下，相对于当前工作目录）。

请注意，在位置路径上使用特殊类路径前缀或标准 URL 前缀会覆盖为加载定义而创建的默认类型`Resource`。请考虑以下示例：

```java
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("classpath:conf/appContext.xml");
```

使用`FileSystemXmlApplicationContext`从类路径加载 bean 定义。但是，它仍然是一个`FileSystemXmlApplicationContext`。如果它随后被用作`ResourceLoader`，任何未加前缀的路径仍被视为文件系统路径。

##### 构建 `ClassPathXmlApplicationContext` 实例 — 快捷方式

`ClassPathXmlApplicationContext`公开了许多构造函数，以便于实例化。基本思想是你只能提供一个字符串数组，它只包含XML文件本身的文件名（没有前导路径信息），还提供了一个`Class`。然后，`ClassPathXmlApplicationContext`从提供的类派生路径信息。

请考虑以下目录布局：

```
com/
  foo/
    services.xml
    daos.xml
    MessengerService.class
```

下面的示例演示如何实例化一个`ClassPathXmlApplicationContext`实例，该实例由名为`services.xml`和`daos.xml`的文件中定义的 bean 组成（在类路径上）。

```java
ApplicationContext ctx = new ClassPathXmlApplicationContext(
    new String[] {"services.xml", "daos.xml"}, MessengerService.class);
```

参考 [`ClassPathXmlApplicationContext`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/jca/context/SpringContextResourceAdapter.html) 文档获取有关各种构造器细节。

#### 2.7.2 应用上下文构造器资源路径中的通配符

应用程序上下文构造函数值中的资源路径可以是简单路径（如前所示），每个路径都与目标`Resource`进行一对一映射，或者可以包含特殊的`classpath*:`前缀或内部 Ant 风格的正则表达式（使用Spring的`PathMatcher`实用程序进行匹配）。 后两者都是有效的通配符。

此机制的一个用途是当您需要进行基于组件风格的应用程序组装时。所有组件都可以将上下文定义片段“发布”到一个众所周知的位置路径，并且当使用前缀为`classpath*:`的相同路径创建最终应用程序上下文时，将自动拾取所有组件片段。

请注意，此通配符特定于在应用程序上下文构造函数中使用资源路径（或当直接使用`PathMatcher`实用程序类层次结构时），并在构造时解析。它与`Resource`类型本身无关。您不能使用`classpath*:`前缀来构造实际的`Resource`，因为一个资源对象一次只指向一个资源。

##### Ant-风格模式

路径位置可以包含 Ant-风格模式，如下面例子所示：

```
/WEB-INF/*-context.xml
com/mycompany/**/applicationContext.xml
file:C:/some/path/*-context.xml
classpath:com/mycompany/**/applicationContext.xml
```

当路径位置包含 Ant 样式模式时，解析程序遵循更复杂的过程来尝试解析通配符。它为直到最后一个非通配符段的路径生成一个`Resource`，并从中获取一个 URL 。如果此 URL 不是`jar：`URL 或特定于容器的变体（例如 WebLogic 中的`zip:`，WebSphere 中的`wsjar`等），则从中获取`java.io.File`并且用于通过遍历文件系统来解析通配符。对于jar URL，解析器从它获取`java.net.JarURLConnection`或手动解析jar URL，然后遍历jar文件的内容以解析通配符。

###### 对可移植性的影响

如果指定的路径已经是文件URL（隐式，因为基本的`ResourceLoader`是一个文件系统或明确的文件系统），保证通配符以完全可移植的方式工作。

如果指定的路径是类路径位置，则解析器必须通过进行`Classloader.getResource()`调用来获取最后一个非通配符路径段URL。由于这只是路径的一个节点（不是最后的文件），实际上它是未定义的（如`ClassLoader`文档所述）在这种情况下确切地返回了什么类型的URL。在实践中，它始终是一个`java.io.File`，表示目录（类路径资源解析为文件系统位置）或某种类型的jar URL（类路径资源解析为jar位置）。尽管如此，这种操作仍存在可移植性问题。

如果获取最后一个非通配符段的jar URL，解析器必须能够从中获取`java.net.JarURLConnection`或手动解析jar URL，以便能够遍历jar的内容并解析通配符。这在大多数环境中都有效，但在其他环境中无效，我们强烈建议您在依赖它之前，在特定环境中对来自jar的资源的通配符解析进行全面测试。

#####  `classpath*:` 前缀

构造基于XML的应用程序上下文时，位置字符串可以使用特殊的`classpath*:`前缀，如以下示例所示：

```java
ApplicationContext ctx =
    new ClassPathXmlApplicationContext("classpath*:conf/appContext.xml");
```

这个特殊的前缀指定必须获取与给定名称匹配的所有类路径资源（在内部，这主要通过调用 `ClassLoader.getResources(…)`）然后合并以形成最终的应用程序上下文定义。

> 通配符类路径依赖于底层类加载器的 `getResources()` 方法。由于现在大多数应用程序服务器都提供了自己的类加载器实现，因此行为可能会有所不同，尤其是在处理jar文件时。 检查 `classpath*` 是否有效的简单测试是使用类加载器从类路径中的jar中加载文件： `getClass().getClassLoader().getResources("<someFileInsideTheJar>")`。尝试使用具有相同名称但放在两个不同位置的文件进行此测试。 如果返回了不适当的结果，请检查应用程序服务器文档以获取可能影响类加载器行为的设置。

您还可以在位置路径的其余部分中将 `classpath*:` 前缀与`PathMatcher`模式组合在一起（例如，`classpath*:META-INF/*-beans.xml`）。在这种情况下，解析策略非常简单：在最后一个非通配符路径段上使用`ClassLoader.getResources()`调用来获取类加载器层次结构中的所有匹配资源，然后从每个资源中获取相同的资源。前面描述的`PathMatcher`解析策略用于通配符子路径。

##### 有关通配符的其它问题

请注意， `classpath*:`与Ant样式模式结合使用时，只能在模式启动前与至少一个根目录一起可靠地工作，除非实际目标文件驻留在文件系统中。这意味着诸如`classpath*:*.xml`之类的模式可能无法从jar文件的根目录中检索文件，而只能从扩展目录的根目录中检索文件。

Spring检索类路径条目的能力来自JDK的`ClassLoader.getResources()`方法，该方法只返回空字符串的文件系统位置（指示搜索的潜在根）。Spring也会在jar文件中评估`URLClassLoader`运行时配置和`java.class.path`清单，但这不能保证导致可移植行为。

> 扫描类路径包需要在类路径中存在相应的目录条目。使用Ant构建JAR时，请不要激活JAR任务的仅文件开关。此外，在某些环境中，基于安全策略，类路径目录可能不会公开 - 例如，JDK 1.7.0_45及更高版本上的独立应用程序（需要在清单中设置“Trusted-Library”。请参阅  https://stackoverflow.com/questions/19394570/java-jre-7u45-breaks-classloader-getresources）。
>
> 在JDK 9的模块路径（Jigsaw）上，Spring的类路径扫描通常按预期工作。此处强烈建议将资源放入专用目录，避免上述搜索jar文件根级别的可移植性问题。

如果要搜索的根包在多个类路径位置中可用，则不能保证使用带有`classpath：`资源的Ant样式模式查找匹配的资源。请考虑以下资源位置示例：

```
com/mycompany/package1/service-context.xml
```

现在考虑可能用来尝试查找该文件的Ant风格路径：

```
classpath:com/mycompany/**/service-context.xml
```

这样的资源可能只在一个位置，但是当使用前面例子之类的路径来尝试解析它时，解析器会处理由 `getResource("com/mycompany");`返回的（第一个）URL。如果此基本包节点存在于多个类加载器位置中，则实际的最终资源可能不存在。因此，在这种情况下，您应该更喜欢使用具有相同Ant样式模式的 `classpath*:`，它搜索包含根包的所有类路径位置。

#### 2.7.3 `FileSystemResource` 注意事项

没有附加到`FileSystemApplicationContext`的`FileSystemResource`（也就是说，当`FileSystemApplicationContext`不是实际的`ResourceLoader`时）就像你期望的那样处理绝对路径和相对路径。相对路径相对于当前工作目录，而绝对路径相对于文件系统的根目录。

但是，为了向后兼容（历史）原因，当`FileSystemApplicationContext`是`ResourceLoader`时，这会发生变化。`FileSystemApplicationContext`强制所有附加的`FileSystemResource`实例将所有位置路径视为相对路径，无论它们是否以前导斜杠开头。实际上，这意味着以下示例是等效的：

```java
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("conf/context.xml");
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("/conf/context.xml");
```

以下示例也是等效的（即使它们有所不同，因为一个案例是相对的而另一个案例是绝对的）：

```java
FileSystemXmlApplicationContext ctx = ...;
ctx.getResource("some/resource/path/myTemplate.txt");
FileSystemXmlApplicationContext ctx = ...;
ctx.getResource("/some/resource/path/myTemplate.txt");
```

实际上，如果你需要真正的绝对文件系统路径，你应该避免使用带有`FileSystemResource`或`FileSystemXmlApplicationContext`的绝对路径，并使用`file：`URL前缀强制使用`UrlResource`。以下示例显示了如何执行此操作：

```java
// actual context type doesn't matter, the Resource will always be UrlResource
ctx.getResource("file:///some/resource/path/myTemplate.txt");
// force this FileSystemXmlApplicationContext to load its definition via a UrlResource
ApplicationContext ctx =
    new FileSystemXmlApplicationContext("file:///conf/context.xml");
```

## 3. 验证，数据绑定和类型转化

将验证视为业务逻辑有利有弊，Spring 提供了针对验证（以及数据绑定）的设计，避免了这种麻烦。特别地，验证逻辑不应该与 web 层耦合，并应该便于本地化，同时应该可以插入任何可用的验证器。考虑到这些问题，Spring 提供了一个基本的`Validator`接口，它在应用的各个层次都非常有用。

数据绑定主要用来将用户输入动态绑定到应用的域模型（或者你用来处理用户输入的随便什么对象）。Spring 提供了一个合适的名字`DataBinder`来完成这项任务。`Validator`和`DataBinder`组成`validation`包，主要用于 MVC 框架中，但是并不局限于此。

`BeanWrapper`是 Spring 框架的一个基础概念，被用在很多地方。不过，可能你并不需要直接使用`BeanWrapper`。由于这是参考文档，我们觉得还是应该对它进行一些介绍比较合适。我们在这一章中解释`BeanWrapper`，因为，如果你正打算使用它，最大的可能性是你正在尝试将数据绑定到对象。

Spring 的`DataBinder`和低级`BeanWrapper`都使用了`PropertyEditorSupport`实现来转化和格式化属性值。`PropertyEditor`和`PropertyEditorSupport`类型都是 JavaBeans 规范的一部分，都在本章节中解释。Spring 3 引入了`cort.convert`包，该包提供了通用的类型转化工具，以及一个高级的格式化包用来格式化 UI 字段值。你可以使用这些包作为`PropertyEditorSupport`实现的更简单的替代品。它们也在本章中讨论。

> JSR-303/JSR-349 Bean Validation
>
> 在版本 4.0 中，Spring 框架支持 Bean 验证 1.0（JSR-303）和 Bean 验证 1.1（JSR-349）用于设置支持并将它们与 Spring 的`Validator`接口进行了适配。
>
> 应用可以选择全局一次性启用 Bean 验证，如 [Spring Validation](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#validation-beanvalidation) 所描述，然后在所有需要验证的地方使用。
>
> 应用程序也可以为每个`DataBinder`实例注册额外的 Spring `Validator`实例，如 [Configuring a `DataBinder`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#validation-binder) 中所述。通过这种方式，可以在不使用注解的情况下插入验证逻辑。

### 3.1 使用 Spring 的`Validator`接口进行验证

Spring 的特性`Validator`接口让你用来验证对象。`Validator`接口通过使用`Errors`对象来做到这一点，在验证过程中，验证器可以通过`Errors`对象报告验证失败。

考虑下面的例子：

```java
public class Person {

    private String name;
    private int age;

    // the usual getters and setters...
}
```

下面的例子为`Person`类提供验证行为，通过实现`org.springframework.validation.Validator`接口的下面的两个方法：

- `supports(Class)`: 这个 `Validator` 是否能够验证给定的 `Class`实例？
- `validate(Object, org.springframework.validation.Errors)`: 验证给定的对象，如果验证失败，通过给定的`Errors`对象报告失败信息。

实现一个`Validator`是非常直接的想法，特别是当你知道 Spring 也提供了`ValidationUtils`帮助类。下面例子为`Person`实例提供了`Validator`实现：

```java
public class PersonValidator implements Validator {

    /**
     * This Validator validates *only* Person instances
     */
    public boolean supports(Class clazz) {
        return Person.class.equals(clazz);
    }

    public void validate(Object obj, Errors e) {
        ValidationUtils.rejectIfEmpty(e, "name", "name.empty");
        Person p = (Person) obj;
        if (p.getAge() < 0) {
            e.rejectValue("age", "negativevalue");
        } else if (p.getAge() > 110) {
            e.rejectValue("age", "too.darn.old");
        }
    }
}
```

`ValidationUtils`类上的`static rejectIfEmpty(...)`方法用来拒绝`name`属性，如果它是`null`或者空字符串。更多细节参考 [`ValidationUtils`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/validation/ValidationUtils.html) 文档。

虽然可以实现一个`Validator`类来验证"富"对象中的每个嵌套对象，但最好将每个嵌套对象类的验证逻辑封装在自己的`Validator`实现中。“富”对象的一个简单示例是`Customer`，它由两个`String`属性（第一个和第二个名称）和一个复杂的`Address`对象组成。`Address`对象可以独立于`Customer`对象使用，因此实现了不同的`AddressValidator`。如果您希望`CustomerValidator`重用`AddressValidator`类中包含的逻辑，则可以在`CustomerValidator`中依赖注入或实例化`AddressValidator`，如以下示例所示：

```java
public class CustomerValidator implements Validator {

    private final Validator addressValidator;

    public CustomerValidator(Validator addressValidator) {
        if (addressValidator == null) {
            throw new IllegalArgumentException("The supplied [Validator] is " +
                "required and must not be null.");
        }
        if (!addressValidator.supports(Address.class)) {
            throw new IllegalArgumentException("The supplied [Validator] must " +
                "support the validation of [Address] instances.");
        }
        this.addressValidator = addressValidator;
    }

    /**
     * This Validator validates Customer instances, and any subclasses of Customer too
     */
    public boolean supports(Class clazz) {
        return Customer.class.isAssignableFrom(clazz);
    }

    public void validate(Object target, Errors errors) {
        ValidationUtils.rejectIfEmptyOrWhitespace(errors, "firstName", "field.required");
        ValidationUtils.rejectIfEmptyOrWhitespace(errors, "surname", "field.required");
        Customer customer = (Customer) target;
        try {
            errors.pushNestedPath("address");
            ValidationUtils.invokeValidator(this.addressValidator, customer.getAddress(), errors);
        } finally {
            errors.popNestedPath();
        }
    }
}
```

验证错误将报告给传递给验证程序的`Errors`对象。对于Spring Web MVC，您可以使用`<spring:bind />`标记来检查错误消息，但您也可以自己检查`Errors`对象。有关它提供的方法的更多信息可以在 [javadoc](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframeworkvalidation/Errors.html) 中找到。

### 3.2 解析错误码为错误信息

上面介绍了数据绑定和验证。本章节涵盖对应于验证失败的输出信息。在上一章节中的例子中，我们拒绝了`name`和`age`字段。如果我们希望使用`MessageSource`来输出错误消息，则可以在拒绝字段（例子中是`name`和`age`）时使用错误编码。当我们调用（直接或者间接调用，比如使用`ValidationUtils`类）`rejectValue`或者`Errors`接口中的任何一个其它的`reject`方法。底层实现不仅注册你传入的错误编码，同时还注册了大量额外的错误编码。`MessgeCodesResolver`确定`Errors`接口注册的错误编码。默认地，使用`DefaultMessageCodesResolver`，它不仅注册你给出的错误编码和相应的错误消息，同时还注册包含你传入该`reject`方法的字段名称的消息。因此，如果你通过使用`rejectValue("age", "too.darn.old")`来拒绝字段，除了`too.darn.old`编码，Spring 同时注册了`too.darn.old.age`和`too.darn.old.age.int`（前者包含字段名称而后者包含字段类型）。这样做是为了方便在定位错误消息时帮助开发人员。

有关`MessageCodesResolver`和默认策略的更多细节参见 [`MessageCodesResolver`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/validation/MessageCodesResolver.html) 和 [`DefaultMessageCodesResolver`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/validation/DefaultMessageCodesResolver.html) 文档。

### 3.3 Bean 操纵和 `BeanWrapper`

`org.springframework.beans`包遵循 JavaBeans 标准。所谓的 JavaBean 是这样的类：拥有默认的无参构造器，遵行如下字段命名约定，名为`bingoMadness`的字段有相应的 setter 方法`setBingoMadness(...)`和 getter 方法`getBingoMadness()`。更多信息参考 [javabeans](https://docs.oracle.com/javase/8/docs/api/java/beans/package-summary.html) 。

beans 包中一个相当重要的类是`BeanWrapper`接口和它相应的实现`BeanWrapperImpl` 。从官方文档可知，`BeanWrapper`提供了设置和获取属性值（单个或者批量）、获取属性描述符、查询属性以确定它们是否可读或者可写等功能。同时，`BeanWrapper`提供了嵌套属性支持，开启了任意深度的子属性设置功能。`BeanWrapper`还支持添加标准 JavaBeans `PropertyChangeListeners`和`VetoableChangeListeners`的能力，而且不需要目标类中提供支持代码。最后，`BeanWrapper`提供了设定索引属性的支持。`BeanWrapper`通常不会直接由应用代码使用，而是通常由`DataBinder`和`BeanFactory`使用。

`BeanWrapper`的工作方式部分如其名称表示：它包装 bean 以对该 bean 执行操作，例如设置和检索属性。

#### 3.3.1 设定和获取基本属性和嵌套属性

设置和获取属性是通过使用`setPropertyValue`，`setPropertyValues`，`getPropertyValue`和`getPropertyValues`方法完成的，这些方法带有几个重载变体。Springs javadoc更详细地描述了它们。JavaBeans规范具有指示对象属性的约定。下表显示了这些约定的一些示例：

| 表达式                    | 解释                                       |
| ---------------------- | ---------------------------------------- |
| `name`                 | 指示对应于 `getName()` 或者 `isName()` 和 `setName(..)` 方法的属性 `name` 。 |
| `account.name`         | 指示属性 `account`上的对应于 `getAccount().setName()` 或者 `getAccount().getName()`方法的嵌套属性 `name` 。 |
| `account[2]`           | 只是索引属性 `account` 的第三个元素。索引属性可以是类型 `array`, `list`, 或者其它自然有序集合。 |
| `account[COMPANYNAME]` | 指示由`account` Map属性的`COMPANYNAME`键索引的映射条目的值。 |

（如果您不打算直接使用`BeanWrapper`，那么下一部分对您来说并不重要。如果您只使用`DataBinder`和`BeanFactory`及其默认实现，那么您应该跳到 [PropertyEditors](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-beans-conversion) 部分。）

以下两个示例类使用`BeanWrapper`来获取和设置属性：

```java
public class Company {

    private String name;
    private Employee managingDirector;

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public Employee getManagingDirector() {
        return this.managingDirector;
    }

    public void setManagingDirector(Employee managingDirector) {
        this.managingDirector = managingDirector;
    }
}
```

```java
public class Employee {

    private String name;

    private float salary;

    public String getName() {
        return this.name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public float getSalary() {
        return salary;
    }

    public void setSalary(float salary) {
        this.salary = salary;
    }
}
```

以下代码片段显示了如何检索和操作实例化的 `Companies` 和 `Employees`的某些属性的一些示例：

```java
BeanWrapper company = new BeanWrapperImpl(new Company());
// setting the company name..
company.setPropertyValue("name", "Some Company Inc.");
// ... can also be done like this:
PropertyValue value = new PropertyValue("name", "Some Company Inc.");
company.setPropertyValue(value);

// ok, let's create the director and tie it to the company:
BeanWrapper jim = new BeanWrapperImpl(new Employee());
jim.setPropertyValue("name", "Jim Stravinsky");
company.setPropertyValue("managingDirector", jim.getWrappedInstance());

// retrieving the salary of the managingDirector through the company
Float salary = (Float) company.getPropertyValue("managingDirector.salary");
```

#### 3.3.2 内建的 `PropertyEditor` 实现

Spring 使用`PropertyEditor`的概念来实现`Object`和`String`之间的转换。以与对象本身不同的方式表示属性可能很方便。例如，`Date`可以用人类可读的方式表示（如`String`：`'2007-14-09'`），而我们仍然可以将人类可读的形式转换回原始日期（或者更好的是，转换任何以人类可读的形式输入的日期为`Date`对象）。可以通过注册`java.beans.PropertyEditor`类型的自定义编辑器来实现此行为。在`BeanWrapper`上注册自定义编辑器，或者在特定的IoC容器中注册自定义编辑器（如前一章所述），使其了解如何将属性转换为所需类型。有关`PropertyEditor`的更多信息，请参阅 [Oracle的java.beans包的javadoc](https://docs.oracle.com/javase/8/docs/api/java/beans/package-summary.html) 。

在 Spring 中使用属性编辑的几个例子：

- 通过使用`PropertyEditor`实现来完成 beans 属性的设置。当你使用`String`作为你在 XML 中声明的一些 bean 的属性的值时，Spring（如果该属性的 setter 拥有一个`Class`参数）使用`ClassEditor`尝试解析该参数为一个`Class`对象。
- 在Spring的MVC框架中解析HTTP请求参数是通过使用可以在`CommandController`的所有子类中手动绑定的各种`PropertyEditor`实现来完成的。

Spring 拥有若干内建的`PropertyEditor`实现以方便使用。它们都放在`org.springframework.beans.propertyeditors`包中。大多数（不是所有，如下表中所示）都是，默认地，由`BeanWrapperImpl`注册。属性编辑器也以同样方式配置。你仍然可以注册你自己的变体来覆盖默认的。下表描述了 Spring 提供的各种`PropertyEditor`实现：

| 类                         | 解释                                       |
| ------------------------- | ---------------------------------------- |
| `ByteArrayPropertyEditor` | 字节数组编辑器。将字符串转化为相应的字节表示。默认通过`BeanWrapperImpl`注册。 |
| `ClassEditor`             | 将表示类的字符串解析为实际的类，或者执行逆向转换。当一个类没有找到，抛出`IllegalArgumentException`。默认地由`BeanWrapperImpl`注册。 |
| `CustomBooleanEditor`     | `Boolean`属性的可自定义属性编辑器。默认情况下，由`BeanWrapperImpl`注册。但可以通过将其自定义实例注册为自定义编辑器来覆盖。 |
| `CustomCollectionEditor`  | 集合的属性编辑器，将任何源`Collection`转换为给定的目标`Collection`类型。 |
| `CustomDateEditor`        | `java.util.Date`的可自定义属性编辑器，支持自定义`DateFormat`。没有默认注册。必须根据需要使用适当的格式进行注册。 |
| `CustomNumberEditor`      | 任何`Number`子类的可自定义属性编辑器，例如`Intege`r，`Long`，`Float`或`Double`。默认情况下，由`BeanWrapperImpl`注册，但可以通过将其自定义实例注册为自定义编辑器来覆盖。 |
| `FileEditor`              | 将字符串解析为 `java.io.File` 对象。默认情况下，由`BeanWrapperImpl`注册。 |
| `InputStreamEditor`       | 单向属性编辑器，可以获取字符串并生成（通过中间`ResourceEditor`和`Resource`）`InputStream`，以便`InputStream`属性可以直接以字符串形式设置。请注意，默认用法不会为您关闭`InputStream`。默认情况下，由`BeanWrapperImpl`注册。 |
| `LocaleEditor`            | 可以将字符串解析为`Locale`对象，反之亦然（字符串格式为`*[country]*[variant]`，与`Locale`的`toString()`方法相同）。默认情况下，由`BeanWrapperImpl`注册。 |
| `PatternEditor`           | 可以将字符串解析为`java.util.regex.Pattern`对象，反之亦然。 |
| `PropertiesEditor`        | 可以将字符串（使用`java.util.Properties`类的javadoc中定义的格式进行格式化）转换为`Properties`对象。默认情况下，由`BeanWrapperImpl`注册。 |
| `StringTrimmerEditor`     | 修剪字符串的属性编辑器。允许有选择性地将空字符串转换为`null`。默认情况下未注册 - 必须是用户注册的。 |
| `URLEditor`               | 可以将URL的字符串表示形式解析为实际的`URL`对象。 默认情况下，由`BeanWrapperImpl`注册。 |

Spring使用`java.beans.PropertyEditorManager`来设置可能需要的属性编辑器的搜索路径。搜索路径还包括`sun.bean.editors`，其中包括`Font`，`Color`和大多数基本类型等类型的`PropertyEditor`实现。另请注意，标准JavaBeans基础结构会自动发现`PropertyEditorclasses`（无需显式注册），如果它们与它们处理的类位于同一个包中，并且与该类具有相同的名称，并附加了`Editor`。例如，可以使用以下类和包结构，这足以使`SomethingEditor`类被识别并用作`Something-typed`属性的`PropertyEditor`。

```
com
  chank
    pop
      Something
      SomethingEditor // the PropertyEditor for the Something class
```

请注意，您也可以在此处使用标准`BeanInfo` JavaBeans机制（描述在 [这里](https://docs.oracle.com/javase/tutorial/javabeans/advanced/customization.html) ）。以下示例使用`BeanInfo`机制显式注册一个或多个`PropertyEditor`：

```
com
  chank
    pop
      Something
      SomethingBeanInfo // the BeanInfo for the Something class
```

以下引用的`SomethingBeanInfo`类的Java源代码将`CustomNumberEditor`与`Something`类的`age`属性相关联：

```java
public class SomethingBeanInfo extends SimpleBeanInfo {

    public PropertyDescriptor[] getPropertyDescriptors() {
        try {
            final PropertyEditor numberPE = new CustomNumberEditor(Integer.class, true);
            PropertyDescriptor ageDescriptor = new PropertyDescriptor("age", Something.class) {
                public PropertyEditor createPropertyEditor(Object bean) {
                    return numberPE;
                };
            };
            return new PropertyDescriptor[] { ageDescriptor };
        }
        catch (IntrospectionException ex) {
            throw new Error(ex.toString());
        }
    }
}
```

##### 注册额外的自定义 `PropertyEditor` 实现

当使用字符串值设置 bean 属性时，Spring IoC 容器最终使用标准的 JavaBeans`PropertyEditor`实现将这些字符串转化为属性的复杂类型。Spring 预注册了一系列的自定义`PropertyEditor`实现（比如，转化表示类名的字符串为`Class`对象）。更进一步，Java 的标准 JavaBeans`PropertyEditor`查找机制要求一个类的`PropertyEditor`应该被合适地命名，并放在它所支持的类同一个包中，从而保证它可以被自动发现。

如果需要注册其它自定义`PropertyEditor`，存在几种机制可以使用。手动程度最高的方法，通常不方便也不推荐，是使用`ConfigurableBeanFactory`接口的`registerCustomEditor()`方法，假定你拥有一个`BeanFactory`引用。另一种机制（稍微方便一点）使用一种特殊的 bean 工厂后处理器，名为`CustomEditorConfigurer`。尽管你可以与`BeanFactory`实现一起使用 bean 工厂后处理器，`CustomEditorConfigurer`拥有一个嵌套属性设置，因而我们强烈推荐你将其和`ApplicationContext`一起使用，此时你可以与所有其它 bean 一样部署它，它同样可以被自动侦测并应用。

注意，所有 bean 工厂和应用上下文都会自动使用一系列内建的属性编辑器，通过它们使用`BeanWrapper`处理属性转化。上一章节中列出了`BeanWrapper`注册的标准属性编辑器。另外，`ApplicationContext`也覆盖或者添加了额外的编辑器来处理资源，这些资源按照特定与应用上下文类型的方式查找。

标准 JavaBeans`PropertyEditor`实例被用来将表示为字符串的属性值转化为实际的属性复杂类型。你可以使用`CustomEditorConfigurer`，这是一个 bean 工厂后处理器，来方便地向`ApplicationContext`添加额外的`PropertyEditor`支持。

考虑下面的例子，定义了一个名为`ExoticType`的用户类以及另外一个类`DependsOnExoticType`，它需要`ExoticType`实例设定为属性：

```java
package example;

public class ExoticType {

    private String name;

    public ExoticType(String name) {
        this.name = name;
    }
}

public class DependsOnExoticType {

    private ExoticType type;

    public void setType(ExoticType type) {
        this.type = type;
    }
}
```

正确设置后，我们希望能够将`type`属性指定为字符串，`PropertyEditor`将其转换为实际的`ExoticType`实例。以下bean定义显示了如何设置此关系：

```xml
<bean id="sample" class="example.DependsOnExoticType">
    <property name="type" value="aNameForExoticType"/>
</bean>
```

`PropertyEditor`实现大概是下面这个样子：

```java
// converts string representation to ExoticType object
package example;

public class ExoticTypeEditor extends PropertyEditorSupport {

    public void setAsText(String text) {
        setValue(new ExoticType(text.toUpperCase()));
    }
}
```

最后，下面的示例演示如何使用`CustomEditorConfigurer`向`ApplicationIntext`注册新的`PropertyEditor`，然后可以根据需要使用它：

```xml
<bean class="org.springframework.beans.factory.config.CustomEditorConfigurer">
    <property name="customEditors">
        <map>
            <entry key="example.ExoticType" value="example.ExoticTypeEditor"/>
        </map>
    </property>
</bean>
```

###### 使用 `PropertyEditorRegistrar`

使用 Spring 容器注册属性编辑器的另一种机制是创建和使用`PropertyEditorRegistrar`。当您需要在几种不同情况下使用同一组属性编辑器时，此接口特别有用。您可以编写相应的注册器，并在每种情况下重复使用它。`PropertyEditorRegistrar`实例与名为`PropertyEditorRegistry`的接口一起工作，该接口由 Spring `BeanWrapper`（和`DataBinder`）实现。`PropertyEditorRegistrar`实例在与`CustomEditorConfigurer`（[此处](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-beans-conversion-customeditor-registration) 描述）结合使用时特别方便，它公开了一个名为`setPropertyEditorRegistrars(..)`的方法。以这种方式添加到`CustomEditorConfigurer`的`PropertyEditorRegistrar`实例可以很容易地与`DataBinder`和 Spring MVC 控制器共享。此外，它避免了在自定义编辑器上进行同步的需要：`PropertyEditorRegistrar`需要为每个 bean 创建尝试创建新的`PropertyEditor`实例。

下面的例子展示了如何创建你自己的`PropertyEditorRegistrar`实现：

```java
package com.foo.editors.spring;

public final class CustomPropertyEditorRegistrar implements PropertyEditorRegistrar {

    public void registerCustomEditors(PropertyEditorRegistry registry) {

        // it is expected that new PropertyEditor instances are created
        registry.registerCustomEditor(ExoticType.class, new ExoticTypeEditor());

        // you could register as many custom property editors as are required here...
    }
}
```

另请参阅`org.springframework.beans.support.ResourceEditorRegistrar`以获取`PropertyEditorRegistrar`实现示例。请注意，在实现 `registerCustomEditors(..)` 方法时，它会创建每个属性编辑器的新实例。

下一个示例显示如何配置`CustomEditorConfigurer`并将我们的`CustomPropertyEditorRegistrar`实例注入其中：

```xml
<bean class="org.springframework.beans.factory.config.CustomEditorConfigurer">
    <property name="propertyEditorRegistrars">
        <list>
            <ref bean="customPropertyEditorRegistrar"/>
        </list>
    </property>
</bean>

<bean id="customPropertyEditorRegistrar"
    class="com.foo.editors.spring.CustomPropertyEditorRegistrar"/>
```

最后（与本章的重点有所不同，对于那些使用 [Spring的MVC Web框架](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/web.html#mvc) 的人来说），使用`PropertyEditorRegistrars`和数据绑定 `Controllers`（如`SimpleFormController`）会非常方便。以下示例在`initBinder(..)`方法的实现中使用`PropertyEditorRegistrar`：

```java
public final class RegisterUserController extends SimpleFormController {

    private final PropertyEditorRegistrar customPropertyEditorRegistrar;

    public RegisterUserController(PropertyEditorRegistrar propertyEditorRegistrar) {
        this.customPropertyEditorRegistrar = propertyEditorRegistrar;
    }

    protected void initBinder(HttpServletRequest request,
            ServletRequestDataBinder binder) throws Exception {
        this.customPropertyEditorRegistrar.registerCustomEditors(binder);
    }

    // other methods to do with registering a User
}
```

这种`PropertyEditor`注册方式会导致简洁的代码（`initBinder(..)`的实现只有一行），并允许将公共`PropertyEditor`注册代码封装在一个类中，然后在所需的 `Controllers`之间共享。

### 3.4 Spring 类型转化

Spring 3 引入了`core.convert`包来提供通用的类型转化系统。该系统定义一个 SPI 来实现类型转化逻辑，并提供一个在运行时执行类型转化的 API。在 Spring 容器中，你可以使用这个系统作为`PropertyEditor`实现的替代品来将外部 bean 属性值字符串转化为需要的属性类型。你也可以在你的应用程序中任何需要类型转化的地方使用该公开 API 。

#### 3.4.1. 转化器 SPI

实现类型转化逻辑的 SPI 是简洁的，它是强类型的。如下面接口定义所示：

```java
package org.springframework.core.convert.converter;

public interface Converter<S, T> {

    T convert(S source);
}
```

要实现你自己的转化器，实现`Converter`接口，其中的参数`S`是你想要转化的类型，`T`是你想要转化为的类型。如果一个`S`集合或者数组需要转化为`T`集合或者数组，你也可以透明地应用该转化器，前提是已经注册了委托数组或者集合转化器（默认情况下`DefaultConversionService`就是这么做）。

每次`convert(S)`调用，源参数保证不为`null`。如果转化失败，你的`Converter`可以抛出任何未检查的异常。特别地，它应该抛出`IllegalArgumentException`来报告非法的源值。请确保你的`Converter`实现是线程安全的。

方便起见，`core.convert.support`包中提供了一些转化器实现。包括将字符串转化未数字或者其它常用类型的转化器。下面是`StringToInteger`类，一个典型的`Converter`实现：

```java
package org.springframework.core.convert.support;

final class StringToInteger implements Converter<String, Integer> {

    public Integer convert(String source) {
        return Integer.valueOf(source);
    }
}
```

#### 3.4.2. 使用 `ConverterFactory`

当您需要集中整个类层次结构的转换逻辑时（例如，从`String`转换为`Enum`对象时），您可以实现`ConverterFactory`，如以下示例所示：

```java
package org.springframework.core.convert.converter;

public interface ConverterFactory<S, R> {

    <T extends R> Converter<S, T> getConverter(Class<T> targetType);
}
```

参数化`S`为要转换的类型，`R`为定义转化目标类的范围的基本类型。然后实现`getConverter(Class<T>)`，其中`T`是`R`的子类。

以`StringToEnumConverterFactory`为例：

```java
package org.springframework.core.convert.support;

final class StringToEnumConverterFactory implements ConverterFactory<String, Enum> {

    public <T extends Enum> Converter<String, T> getConverter(Class<T> targetType) {
        return new StringToEnumConverter(targetType);
    }

    private final class StringToEnumConverter<T extends Enum> implements Converter<String, T> {

        private Class<T> enumType;

        public StringToEnumConverter(Class<T> enumType) {
            this.enumType = enumType;
        }

        public T convert(String source) {
            return (T) Enum.valueOf(this.enumType, source.trim());
        }
    }
}
```

#### 3.4.3. 使用 `GenericConverter`

当你需要比较复杂的`Converter`实现时，考虑使用`GenericConverter`接口。`GenericConverter`具有比`Converter`更灵活但不太强类型的签名，支持在多种源和目标类型之间进行转换。此外，`GenericConverter`提供了在实现转换逻辑时可以使用的源和目标字段上下文。这样的上下文允许类型转换由字段注解或在字段签名上声明的通用信息驱动。以下清单显示了`GenericConverter`的接口定义：

```java
package org.springframework.core.convert.converter;

public interface GenericConverter {

    public Set<ConvertiblePair> getConvertibleTypes();

    Object convert(Object source, TypeDescriptor sourceType, TypeDescriptor targetType);
}
```

要实现`GenericConverter`，请让 `getConvertibleTypes()` 返回支持的源→目标类型对。然后实现 `convert(Object, TypeDescriptor, TypeDescriptor)` 以包含转换逻辑。源`TypeDescriptor`提供对包含要转换的值的源字段的访问。目标`TypeDescriptor`提供对要设置转换值的目标字段的访问。

`GenericConverter`的一个很好的例子是在Java数组和集合之间进行转换的转换器。这样的`ArrayToCollectionConverter`会内省声明目标集合类型的字段以解析集合的元素类型。这样，在目标字段上设置集合之前，可以将源数组中的每个元素转换为目标集合元素类型。

> 由于`GenericConverter`是更复杂的 SPI 接口，你应该仅仅在确实需要时使用。通常的类型转化请优先使用`Converter`或者`ConverterFactory`。

##### 使用 `ConditionalGenericConverter`

有时，只有在特定条件成立时才希望`Converter`运行。例如，如果目标字段上存在特定注解，才需要运行`Converter`，或者如果在目标类上定义了特定方法（例如静态`valueOf`方法），才运行`Converter`。`ConditionalGenericConverter`是`GenericConverter`和`ConditionalConverter`接口的联合，允许您定义此类自定义匹配条件：

```java
public interface ConditionalConverter {

    boolean matches(TypeDescriptor sourceType, TypeDescriptor targetType);
}

public interface ConditionalGenericConverter extends GenericConverter, ConditionalConverter {
}
```

`ConditionalGenericConverter`的一个很好的例子是`EntityConverter`，它在持久化实体标识符和实体引用之间进行转换。仅当目标实体类型声明静态查找方法（例如，`findAccount(Long)`）时，此类`EntityConverter`才可能匹配。您可以在匹配的实现`matches(TypeDescriptor, TypeDescriptor)`中执行这样的查找方法检查。

#### 3.4.4 `ConversionService` API

`ConversionService`定义了一个通用接口用于在运行时执行类型转化逻辑。转换器通常运行在下面这种门面接口背后。

```java
package org.springframework.core.convert;

public interface ConversionService {
  boolean canConvert(Class<?> sourceType, Class<?> targetType);
  
  <T> T convert(Object source, Class<T> targetType);
  
  boolean canConvert(TypeDescriptor sourceType, TypeDescriptor targetType);

  Object convert(Object source, TypeDescriptor sourceType, TypeDescriptor targetType);
}
```

大部分`ConversionService`实现同样实现了`ConverterRegistry`，该接口提供了注册转换器的 SPI。站在内部来说，`ConversionService`实现代理了它注册的转换器来执行类型转换逻辑。

在`core.convert.support`包中有一个健壮的`ConversionService`实现。`GenericConversionService`是通用实现，适用于大部分场景。`ConversionServiceFactory`提供了一个方便的工厂来创建普通的`ConversionService`配置。

#### 3.4.5 配置`ConversionService`

`ConversionService`是一个无状态的对下个，它被设计为在应用启动时实例化，然后在多个进程之间共享。在一个 Spring 应用中，你通常应该为每个 Spring 容器（或者`ApplicationContext`）配置一个`ConversionService`实例。Spring 获取该`ConversionService`实例并在任何需要框架执行类型转换的地方使用。你也可以将该实例注入你的 beans 并直接调用它。

> 如果没有为 Spring 配置`ConversionService`，则使用原始的基于`PropertyEditor`的系统。

为 Spring 注册默认的`ConversionService`，添加下面的 bean 定义：

```xml
<bean id="conversionService"
    class="org.springframework.context.support.ConversionServiceFactoryBean"/>
```

默认的`ConversionService`可以在字符串、数字、枚举、集合、映射以及其它普通类型之间执行转换。为了用你自己的自定义转化器替换或者覆盖默认的转化器，设置`converters`属性。该属性值实现任意`Converter`，`ConverterFactory`或者`GenericConverter`接口。

```xml
<bean id="conversionService"
        class="org.springframework.context.support.ConversionServiceFactoryBean">
    <property name="converters">
        <set>
            <bean class="example.MyCustomConverter"/>
        </set>
    </property>
</bean>
```

在 Spring MVC 应用中也广泛应用了`ConversionService`。参考 Spring MVC 章节中的 [Conversion and Formatting](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/web.html#mvc-config-conversion) 。

某些情况下，你可能希望在类型转换过程中进行格式化。参考 [The `FormatterRegistry` SPI](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#format-FormatterRegistry-SPI) 中有关`FormattingConversionServiceFactoryBean`的使用细节。

#### 3.4.6 编程方式使用`ConversionService`

为了以编程方式使用`ConversionService`实例，你可以将其引用注入任何其它 bean 中。下面的例子展示了如何做。

```java
@Service
public class MyService {
  
  @Autowired
  public MyService(ConversionService conversionService) {
    this.conversionService = conversionService;
  }
  
  public void doIt() {
    this.conversionService.convert(...);
  }
}
```

大多数情况下，你可以使用指定`targetType`的`convert`方法，但是它不适用于更复杂的类型，比如参数化元素的集合。比如，如果你想要以编程方式将一个`Integer`的`List`转换为`String`的`List`，你需要提供源类型和目标类型的正式定义。

幸运的是，`TypeDescriptor`提供各种选项来保证无论如何都可以这样做。如下面例子所示：

```java
DefaultConversionService cs = new DefaultConversionService();

List<Integer> input = ....
cs.convert(input,
          TypeDescriptor.forObject(input), // List<Integer> type descriptor)
          TypeDescriptor.collection(List.class, TypeDescriptor.valueOf(String.class)));
```

注意，`DefaultConversionService`自动注册转换器，这些转换器适用于大部分环境。包含集合转换器、纯量（scalar）转换器，以及基本的`Object`到`String`的转换器。你可以使用`DefaultConversionService`类上的`addDefaultConverters`静态方法来注册相同的转换器以及任何`ConverterRegistry`。

值类型转换器被数组和集合复用，因此没有必要为从`S`的`Collection`向`T`的`Collection`的转换创建特定的转换器，假定标准集合处理是合适的。

### 3.5 Spring 字段格式化

如上一章节中所述， [`core.convert`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#core-convert) 是一个通用类型转换系统。它提供了一个通用的`ConversionService` API 以及一个强类型的`Converter` SPI 来实现类型转换逻辑。Spring 容器使用这个系统来绑定 bean 属性值。另外，Spring 表达式语言（SpEL）和`DataBinder`都使用该系统绑定字段值。比如，当 SpEL 需要将`Short`强制转换为`Long`以完成`expression.setValue(Object bean, Object value)`尝试，`core.convert`系统将执行此强制转换。

考虑典型的客户端环境下，比如 web 或者桌面应用，的类型转换需求。在这种环境下，你通常会从`String`转换以支持客户端回传过程，同时转换为`String`以支持视图渲染过程。另外，你通常会需要本地化`String` 值。通用的`core.convert` `Converter` SPI 不直接支持这种格式化需求。为了直接支持它们，Spring 3 引入了一个方便的`Formatter`提供一个简单而健壮的客户端环境下的`PropertyEditor`实现替代品。

通常，你可以使用`Converter` SPI 当你需要实现通用类型转换逻辑 - 比如，为了转换`java.util.Date`和`Long`。你可以使用该`Formatter` SPI 当你在客户端环境中（比如 web 应用）工作而又需要转换并打印本地化的字段值时。`ConversionService`同时为两个 SPIs 提供了通用类型转换 API 。

#### 3.5.1 `Formatter` SPI

`Formatter` SPI 提供实现字段格式化逻辑是简单而强类型的。下面列出了`Formatter`接口定义：

```java
package org.springframework.format

public interface Formatter<T> extends Printer<T>, Parser<T> {

}
```

`Formatter`继承自`Printer`和`Parser`两个构建块（building-block）接口。下面里除了这两个接口的定义：

```java
public interface Printer<T> {
  String print(T fieldValue, Locale locale);
}
```

```java
import java.text.ParseException;

public interface Parser<T> {
  T parse(String clientValue, Locale locale) throws ParseException;
}
```

为了创建你自己的`Formatter`，实现前面说到的`Formatter`接口。参数化的`T`是你希望格式化的对象的类型 - 比如，`java.util.Date`。实现`print()`方法来将`T`的实例打印显示到本地化客户端上。实现`parse()`方法来将从本地化客户端返回的格式化表示转换为`T`实例。你的`Formatter`应该抛出`ParseException`或者`IllegalArgumentException`，如果转换尝试失败。注意确保你的`Formatter`实现是线程安全的。

方便起见，`format`子包提供了若干`Formatter`实现。`number`包提供了`NumberStyleFormatter`，`CurrencyStyleFormatter`，以及`PercentStyleFormatter`来使用`java.text.NumberFormat`格式化`Number`对象。`datetime`包提供了`DateFormatter`来使用`java.text.DateFormat`格式化`java.util.Date`对象。`datetime.joda`包基于 [Joda-Time library](http://joda-time.sourceforge.net/) 提供了完善的日期时间格式化支持。

下面的`DateFormatter`是一个`Formatter`实现的例子：

```java
package org.springframework.format.datetime

public final class DateFormatter implements Formatter<Date> {

    private String pattern;

    public DateFormatter(String pattern) {
        this.pattern = pattern;
    }

    public String print(Date date, Locale locale) {
        if (date == null) {
            return "";
        }
        return getDateFormat(locale).format(date);
    }

    public Date parse(String formatted, Locale locale) throws ParseException {
        if (formatted.length() == 0) {
            return null;
        }
        return getDateFormat(locale).parse(formatted);
    }

    protected DateFormat getDateFormat(Locale locale) {
        DateFormat dateFormat = new SimpleDateFormat(this.pattern, locale);
        dateFormat.setLenient(false);
        return dateFormat;
    }
}
```

Spring 团队欢迎社区驱动的`Formatter`贡献。参考 [GitHub Issues](https://github.com/spring-projects/spring-framework/issues) 来贡献。

#### 3.5.2 注解驱动的格式化

字符串格式化能够被通过字段类型或者注解配置。为了绑定注解到`Formatter`，实现`AnnotationFormatterFactory`。下面的例子展示了`AnnotationFormatterFactory`接口：

```java
package org.springframework.format;

public interface AnnotationFormatterFactory<A extends Annotation> {

    Set<Class<?>> getFieldTypes();

    Printer<?> getPrinter(A annotation, Class<?> fieldType);

    Parser<?> getParser(A annotation, Class<?> fieldType);
}
```

为了创建一个实现，参数`A`应该是你希望关联到格式化逻辑的字段`annotationType`，比如`org.springframework.format.annotation.DateTimeFormat`。同时拥有`getFieldTypes()`返回该注解能够修饰的字段的类型。拥有`getPrinter()`返回一个`Printer`对象来打印注解修饰的字段值。拥有`getParser()`返回一个`Parser`为注解修饰的字段转换一个`clientValue`。

下面的例子`AnnotationFormatterFactory`实现绑定`@NumberFormat`注解到一个格式化器上以指定一个数字格式或者模式：

```java
public final class NumberFormatAnnotationFormatterFactory
        implements AnnotationFormatterFactory<NumberFormat> {

    public Set<Class<?>> getFieldTypes() {
        return new HashSet<Class<?>>(asList(new Class<?>[] {
            Short.class, Integer.class, Long.class, Float.class,
            Double.class, BigDecimal.class, BigInteger.class }));
    }

    public Printer<Number> getPrinter(NumberFormat annotation, Class<?> fieldType) {
        return configureFormatterFrom(annotation, fieldType);
    }

    public Parser<Number> getParser(NumberFormat annotation, Class<?> fieldType) {
        return configureFormatterFrom(annotation, fieldType);
    }

    private Formatter<Number> configureFormatterFrom(NumberFormat annotation, Class<?> fieldType) {
        if (!annotation.pattern().isEmpty()) {
            return new NumberStyleFormatter(annotation.pattern());
        } else {
            Style style = annotation.style();
            if (style == Style.PERCENT) {
                return new PercentStyleFormatter();
            } else if (style == Style.CURRENCY) {
                return new CurrencyStyleFormatter();
            } else {
                return new NumberStyleFormatter();
            }
        }
    }
}
```

为了触发格式化，你可以用`@NumberFormat`注解修饰字段，如下面例子所示：

```java
public class MyModel {

    @NumberFormat(style=Style.CURRENCY)
    private BigDecimal decimal;
}
```

##### 格式化注解 API

可移植格式注解 API 存在于`org.springframework.format.annotation`包中。您可以使用`@NumberFormat`来格式化`Number`字段，例如`Double`和`Long`，以及`@DateTimeFormat`来格式化`java.util.Date`，`java.util.Calendar`，`Long`（ 对于毫秒时间戳）以及 JSR-310`java.time`和 Joda-Time 值类型。

以下示例使用`@DateTimeFormat`将`java.util.Date`格式化为 ISO Date（yyyy-MM-dd）：

```java
public class MyModel {

    @DateTimeFormat(iso=ISO.DATE)
    private Date date;
}
```

#### 3.5.3 `FormatterRegistry` SPI

`FormatterRegistry`是用于注册格式化器和转换器的 SPI。`FormattingConversionService`是适用于大多数环境的`FormatterRegistry`的实现。您可以以编程方式或声明性地将此变体配置为Spring bean，例如，通过使用`FormattingConversionServiceFactoryBean`。因为此实现还实现了`ConversionService`，所以您可以直接将其配置为与 Spring 的`DataBinder`和 Spring Expression Language（SpEL）一起使用。

以下清单显示了`FormatterRegistry` SPI：

```java
package org.springframework.format;

public interface FormatterRegistry extends ConverterRegistry {

    void addFormatterForFieldType(Class<?> fieldType, Printer<?> printer, Parser<?> parser);

    void addFormatterForFieldType(Class<?> fieldType, Formatter<?> formatter);

    void addFormatterForFieldType(Formatter<?> formatter);

    void addFormatterForAnnotation(AnnotationFormatterFactory<?, ?> factory);
}
```

如上面的清单所示，您可以按字段类型或注解注册格式化程序。

`FormatterRegistry` SPI 允许您集中配置格式规则，而不是在控制器之间复制此类配置。例如，您可能希望强制所有日期字段以某种方式格式化，或者具有特定注解的字段以某种方式格式化。使用共享的`FormatterRegistry`，您可以定义一次这些规则，并在需要格式化时应用它们。

#### 3.5.4 `FormatterRegistrar` SPI

`FormatterRegistrar`是一个 SPI，用于通过`FormatterRegistry`注册格式化程序和转换器。以下清单显示了其接口定义：

```java
package org.springframework.format;

public interface FormatterRegistrar {

    void registerFormatters(FormatterRegistry registry);
}
```

在为给定格式类别注册多个相关转换器和格式化程序时，`FormatterRegistrar`非常有用，例如日期格式。它在声明性注册不足的情况下也很有用 - 例如，当格式化程序需要在与其自己的`<T>`不同的特定字段类型下编入索引时，或者在注册`Printer` /`Parser`对时。下一节提供有关转换器和格式化程序注册的更多信息。

#### 3.5.5 在 Spring MVC 中配置格式化

参考 Spring MVC 中的 [Conversion and Formatting](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/web.html#mvc-config-conversion) 。

### 3.6 配置全局日期和时间格式

默认情况下，没有`@DateTimeFormat`注解修饰的日期和时间字段使用`DateFormate.SHORT`风格从`String`转换而来。如果你愿意，你可以通过定义你自己的全局格式来改变这种行为。

要这样做，你需要确保 Spring 没有注册默认格式化器。你应该手动注册所有的格式化器。使用`org.springframework.format.datetime.joda.JodaTimeFormatterRegistrar`或者`org.springframework.format.datetime.DateFormatterRegistrar`类，取决于你是否使用 Joda-Time 类库。

比如，下面的 Java 配置注册一个全局的`yyyyMMdd`格式（例子没有依赖 Joda-Time 类库）：

```java
@Configuration
public class AppConfig {

    @Bean
    public FormattingConversionService conversionService() {

        // Use the DefaultFormattingConversionService but do not register defaults
        DefaultFormattingConversionService conversionService = new DefaultFormattingConversionService(false);

        // Ensure @NumberFormat is still supported
        conversionService.addFormatterForFieldAnnotation(new NumberFormatAnnotationFormatterFactory());

        // Register date conversion with a specific global format
        DateFormatterRegistrar registrar = new DateFormatterRegistrar();
        registrar.setFormatter(new DateFormatter("yyyyMMdd"));
        registrar.registerFormatters(conversionService);

        return conversionService;
    }
}
```

如果你更习惯使用基于 XML 的配置，你可以使用`FormattingConversionServiceFactoryBean`，下面的例子展示了如何做（这里的时间使用了 Joda Time）：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        https://www.springframework.org/schema/beans/spring-beans.xsd>

    <bean id="conversionService" class="org.springframework.format.support.FormattingConversionServiceFactoryBean">
        <property name="registerDefaultFormatters" value="false" />
        <property name="formatters">
            <set>
                <bean class="org.springframework.format.number.NumberFormatAnnotationFormatterFactory" />
            </set>
        </property>
        <property name="formatterRegistrars">
            <set>
                <bean class="org.springframework.format.datetime.joda.JodaTimeFormatterRegistrar">
                    <property name="dateFormatter">
                        <bean class="org.springframework.format.datetime.joda.DateTimeFormatterFactoryBean">
                            <property name="pattern" value="yyyyMMdd"/>
                        </bean>
                    </property>
                </bean>
            </set>
        </property>
    </bean>
</beans>
```

> Joda-Time 提供了单独的特别类型来表示`date`，`time` 以及 `date-time` 值。`JodaTimeFormatterRegistrar`的`dateFormatter`，`timeFormatter`以及`dateTimeFormatter`属性应该被用于为每种类型配置不同的格式。`DateTimeFormatterFactoryBean`提供了创建格式化器的方便方法。
>
> 如果你使用 Spring MVC，记得显式配置使用的类型转换服务。对基于 Java 的`@Configuration`，这意味着扩展`WebMvcConfigurationSupport`类并重载`mvcConversionService()`方法。对 XML ，你应该使用`mvc:annotation-driven`元素的`conversion-service`属性。参考 [Conversion and Formatting](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/web.html#mvc-config-conversion) 了解更多细节。

### 3.7 Spring 校验

Spring 3 引入了若干对它的校验支持的增强机制。首先，JSR-303 Bean 校验 API 被完整支持。其次，当使用编程方式时，Spring 的`DateBinder`能够校验对象并绑定它们。第三，Spring MVC 已经支持声明式`@Controller`输入校验。

#### 3.7.1 JSR-303 Bean Validation API 概览

JSR-303 标准化了 Java 平台的验证约束声明和元数据。通过使用此API，您可以使用声明性验证约束来注解域模型属性，并且运行时会强制执行它们。您可以使用许多内置约束，还可以定义自己的自定义约束。

请考虑以下示例，该示例显示了一个具有两个属性的简单`PersonForm`模型：

```java
public class PersonForm {
    private String name;
    private int age;
}
```

JSR-303允许您为这些属性定义声明性验证约束，如以下示例所示：

```java
public class PersonForm {

    @NotNull
    @Size(max=64)
    private String name;

    @Min(0)
    private int age;
}
```

当JSR-303 Validator验证此类的实例时，将强制执行这些约束。

有关JSR-303和JSR-349的一般信息，请参阅  [Bean Validation website](https://beanvalidation.org/) 网站。有关默认参考实现的特定功能的信息，请参阅 [Hibernate Validator](https://www.hibernate.org/412.html) 文档。要学习如何将bean验证提供程序设置为Spring bean，请继续阅读。

#### 3.7.2 配置 Bean Validation Provider

Spring提供对Bean Validation API的完全支持。这包括方便地支持将JSR-303或JSR-349 Bean Validation提供程序作为Spring bean引导。这允许您在应用程序中需要验证的任何地方注入`javax.validation.ValidatorFactory`或`javax.validation.Validator`。

您可以使用`LocalValidatorFactoryBean`将默认Validator配置为Spring bean，如以下示例所示：

```xml
<bean id="validator"
    class="org.springframework.validation.beanvalidation.LocalValidatorFactoryBean"/>
```

前面示例中的基本配置通过使用其默认引导机制触发bean验证以进行初始化。JSR-303或JSR-349提供程序（例如Hibernate Validator）应该存在于类路径中并自动检测。

##### 注入校验器

`LocalValidatorFactoryBean`实现了`javax.validation.ValidatorFactory`和`javax.validation.Validator`，以及Spring的`org.springframework.validation.Validator`。您可以将这些接口中的任何一个引用注入到需要调用验证逻辑的bean中。

如果您希望直接使用Bean Validation API，则可以注入对`javax.validation.Validator`的引用，如以下示例所示：

```java
import javax.validation.Validator;

@Service
public class MyService {

    @Autowired
    private Validator validator;
```

你可以注入 `org.springframework.validation.Validator` 引用，如果你的 bean需要 Spring 校验 API，如下面例子所示：

```java
import org.springframework.validation.Validator;

@Service
public class MyService {

    @Autowired
    private Validator validator;
}
```

##### 配置自定义约束

每个bean验证约束由两部分组成：

- 声明约束及其可配置属性的`@Constraint`注解。
- 实现约束行为的`javax.validation.ConstraintValidator`接口的实现。

要将声明与实现相关联，每个`@Constraint`注解都引用相应的`ConstraintValidator`实现类。在运行时，`ConstraintValidatorFactory`在域模型中遇到约束注解时实例化引用的实现。

默认情况下，`LocalValidatorFactoryBean`配置一个`SpringConstraintValidatorFactory`，它使用Spring创建`ConstraintValidator`实例。这使得自定义`ConstraintValidators`可以像任何其他Spring bean一样受益于依赖注入。

以下示例显示了一个自定义的`@Constraint`声明，后跟一个使用Spring进行依赖项注入的关联`ConstraintValidator`实现：

```java
@Target({ElementType.METHOD, ElementType.FIELD})
@Retention(RetentionPolicy.RUNTIME)
@Constraint(validatedBy=MyConstraintValidator.class)
public @interface MyConstraint {
}
```

```java
import javax.validation.ConstraintValidator;

public class MyConstraintValidator implements ConstraintValidator {

    @Autowired;
    private Foo aDependency;

    ...
}
```

如上面例子所示，`ConstraintValidator`实现可以像其它 Spring bean 那样通过`@Autowired`注解进行依赖注入。

##### Spring 驱动的方法校验

您可以通过`MethodValidationPostProcessor` bean定义将Bean Validation 1.1支持（以及作为自定义扩展，通过Hibernate Validator 4.3 支持）的方法验证功能集成到Spring上下文中，如下所示：

```xml
<bean class="org.springframework.validation.beanvalidation.MethodValidationPostProcessor"/>
```

要获得Spring驱动的方法验证资格，所有目标类都需要使用Spring的`@Validated`注解进行修饰。（或者，您也可以声明要使用的验证组。）请参阅 [`MethodValidationPostProcessor`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/validation/beanvalidation/MethodValidationPostProcessor.html) 文档以获取有关Hibernate Validator和Bean Validation 1.1提供程序的设置详细信息。

##### 附加配置选项

对于大多数情况，默认的`LocalValidatorFactoryBean`配置就足够了。从消息插补到遍历解析，各种Bean Validation构造有许多配置选项。有关这些选项的更多信息，请参见 [`LocalValidatorFactoryBean`](https://docs.spring.io/spring-framework/docs/5.1.8.RELEASE/javadoc-api/org/springframework/validation/beanvalidation/LocalValidatorFactoryBean.html) 的文档。

#### 3.7.3 配置 `DataBinder`

从Spring 3开始，您可以使用`Validator`配置`DataBinder`实例。配置完成后，您可以通过调用`binder.validate()`来调用`Validator`。任何验证`Errors`都会自动添加到绑定器的`BindingResult`中。

以下示例说明如何在绑定到目标对象后以编程方式使用`DataBinder`来调用验证逻辑：

```java
Foo target = new Foo();
DataBinder binder = new DataBinder(target);
binder.setValidator(new FooValidator());

// bind to the target object
binder.bind(propertyValues);

// validate the target object
binder.validate();

// get BindingResult that includes any validation errors
BindingResult results = binder.getBindingResult();
```

您还可以通过`dataBinder.addValidators`和`dataBinder.replaceValidators`配置具有多个`Validator`实例的`DataBinder`。当将全局配置的bean验证与在`DataBinder`实例上本地配置的Spring Validator组合时，这非常有用。 请参阅 [[validation-mvc-configuring\]](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#validation-mvc-configuring) 。

#### 3.7.4. Spring MVC 3 校验

参考 Spring MVC 章节中的 [Validation](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/web.html#mvc-config-validation) 。

## 4. Spring 表达式语言 SpEL

略

## 5. Spring 的面向切面编程

面向切面编程（AOP）通过提供另外一种设计程序结构的思路而称为了面向对象编程（OOP）的有效补充。OOP 中程序模块化的关键单元是类，而在 AOP 中模块化的单元变成了切面。切面实现了跨越多种类型和对象的“关注点”（例如事务管理）的模块化。（这些关注点在 AOP 文献中通常被称为“横切”问题。）

AOP 框架是 Spring 的一个关键组成部分。尽管 Spring IoC 容器并不依赖 AOP（意思是如果你不想用 AOP 就可以不用），AOP 还是通过提供相当强力的中间件功能解决方案而称为 Spring IoC 容器的有效补充。

> 使用 AspectJ 切入点的 Spring AOP
>
> Spring 提供简单而强大的方法来写入自定义切面，通过使用  [schema-based approach](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-schema) 或者 [@AspectJ annotation style](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-ataspectj) 。这两种风格都提供了充足的类型建议并使用 AspectJ 切入点语言，同时仍然使用 Spring AOP 来织入。
>
> 本章节讨论基于`schema`和`@AspectJ`的 AOP 支持。低级的 AOP 支持在 [下一章](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-api) 中讨论。

AOP 在 Spring Framework 框架中用来：

- 提供声明式企业服务。此类服务中最重要的就是 [声明式事务管理](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/data-access.html#transaction-declarative) 。
- 允许用户实现自己的切面，让大家可以使用 AOP 补充 OOP。

> 如果您只对通用声明性服务或其他预先打包的声明性中间件服务（如池化服务）感兴趣，则无需直接使用 Spring AOP，并且可以跳过本章的大部分内容。

### 5.1 AOP 概念

让我们首先来定义一些核心的 AOP 概念和术语。这些术语不是特定于 Spring 的。不幸的是，AOP 术语并不都是那么直观。而且，当同时存在 Spring 自己的术语时，情况将会变得更加令人迷惑。

- 切面：横切多个类的关注点的模块化。事务管理是企业级 Java 应用中横切关注点的一个很好的例子。在 Spring AOP 中，切面使用普通的类实现（[schema-based approach](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-schema)）或者由`@Aspect`注解修饰的普通类（[@AspectJ style](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-ataspectj)）。
- 连接点：程序执行过程中的一个点，比如一个方法的执行或者一个异常的处理。在 Spring AOP 中，连接点永远表示一个方法的执行。
- 增强：被特地连接点的切面携带。增强的类型包括`around`，`before`和`after`三种，稍后我们会讨论这些类型。许多 AOP 框架，包括 Spring，将增强建模为一个拦截器，并在连接点周围维护一个拦截器链。
- 切入点：匹配连接点的谓词。增强与切入点表达式相关联，并在切入点匹配的任何连接点处运行（例如，执行具有特定名称的方法）。由切入点表达式匹配的连接点的概念是 AOP 的核心，Spring 默认使用 AspectJ 切入点表达式语言。
- 引介：声明附加方法或者代表类型的字段。Spring AOP 允许您向任何增强的对象引入新接口（以及相应的实现）。例如，您可以使用引介使bean实现`IsModified`接口，以简化缓存。（引介在 AspectJ 社区中被称为类型间声明。）
- 目标对象：被一个或者多个切面增强的对象。也被称为“被增强的对象”。因为 Spring AOP 是通过使用运行时代理实现，目标对象永远都是被代理的对象。
- AOP 代理：由 AOP 框架创建用来实现切面契约（增强方法执行等等）的对象。在 Spring 框架中，一个 AOP 代理是一个 JDK 动态代理或者一个 CGLIB 代理。
- 织入：将切面与其它应用类型或者对象连接起来以创建增强的对象。此过程可以在编译期（比如，使用 AspectJ 编译器），加载期，或者运行时完成。Spring AOP，如其它纯 Java AOP 框架一样，在运行时执行织入。

Spring AOP 包含下列增强类型：

- Before advice: 在连接点之前运行但无法阻止执行流程进入连接点（除非该增强自身抛出异常）。
- After returning advice: 在连接点正常执行完成之后运行（比如，方法正常返回并没有抛出异常）。
- After throwing advice: 当方法因为抛出异常而退出时执行。
- After (finally) advice: 无论连接点如何退出（正常退出或者抛出异常）此增强都会执行。
- Around advice: 围绕连接点，例如方法调用，的增强。这是最有力的增强。这种增强可以在方法调用之前和之后执行自定义行为。它还负责选择是继续执行连接点，还是通过返回增强自己的返回值或抛出异常来短路被增强的方法执行。

围绕增强是最通用的增强。由于Spring AOP，类似于 AspectJ，提供了全方位的增强类型，因此我们建议您使用可以实现所需行为的最弱的增强类型。例如，如果您只需要使用方法的返回值更新缓存，那么最好实现返回后的增强而不是围绕的增强，尽管围绕的增强可以完成同样的事情。使用最具体的增强类型可以提供更简单的编程模型，减少错误的可能性。例如，您不需要在用于`around`增强的`JoinPoint`上调用`proceed()`方法，这样一来，就不可能出现调用失败的情况。

所有增强参数都是静态类型的，因此您可以使用适当类型的增强参数（例如，方法执行的返回值的类型）而不是`Object`数组。

由切入点匹配的连接点的概念是 AOP 的关键，它将 AOP 与仅提供拦截的旧技术区分开来。切入点使得增强可以独立于面向对象的层次结构进行目标确定。例如，您可以将一个提供声明性事务管理的增强应用于跨多个对象的一组方法（例如服务层中的所有业务操作）。

### 5.2 Spring AOP 能力和目标

Spring AOP 由纯 Java 语言实现。不需要特殊的汇编过程。Spring AOP 不需要控制类加载器层级结构，因而适用于 servlet 容器或者应用服务器。

Spring AOP 目前仅仅支持方法执行连接点（增强 Spring beans 上的方法执行）。字段拦截没有实现，尽管对字段拦截的支持可以在不妨碍核心 Spring AOP APIs 前提下添加。如果你需要增强字段访问以及更新连接点，考虑类似于 AspectJ 的语言。

Spring AOP 的 AOP 方式不同于大K部分其他 AOP 框架。它的目标不是要提供最完整的 AOP 实现（尽管 Spring AOP 已经相当强大），它的目标是提供 AOP 实现和 Spring IoC 之间的紧密集成，以帮助解决企业级应用中的常见问题。

因此，比如，Spring 框架的 AOP 功能通常用在 Spring IoC 容器中。切面通过使用正常 bean 定义语法配置（尽管这允许强大的“自动代理”能力）。这是 Spring AOP 与其他 AOP 实现的关键差异。有些事情你使用 Spring AOP 不会很容易和高效，比如增强细粒度的对象（典型的，域对象）。AspectJ 在这种情况下是最佳选择。不过，我们的经验是 Spring AOP 为适合 AOP 的企业级 Java 应用中的大部分问题提供了出色的解决方案。

Spring AOP 从未试图与 AspectJ 竞争，以提供全面的 AOP 解决方案。我们相信，基于代理的框架（如Spring AOP）和完整的框架（如AspectJ）都很有价值，而且它们是互补的，而不是竞争。Spring 将 Spring AOP 和 IoC 与 AspectJ 无缝集成，以在一致的基于 Spring 的应用程序架构中实现 AOP 的所有使用。此集成不会影响 Spring AOP API 或 AOP 同盟 API。Spring AOP仍然向后兼容。有关 Spring AOP API 的讨论，请参见 [下一章节](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-api) 。

> Spring框架的核心原则之一是非侵入性。这个想法是，您不应该被迫在您的业务或域模型中引入特定于框架的类和接口。但是，在某些地方，Spring Framework确实为您提供了将Spring Framework特定的依赖项引入代码库的选项。为您提供此类选项的基本原理是，在某些情况下，以这种方式阅读或编写某些特定功能可能更容易。但是，Spring Framework（几乎）总是为您提供选择：您可以自由决定哪种选项最适合您的特定用例或场景。
>
> 与本章相关的一个选择是选择哪种AOP框架（以及哪种AOP样式）。您可以选择AspectJ，Spring AOP或两者。您还可以选择@AspectJ注解样式方法或Spring XML配置样式方法。本章选择首先介绍@ AspectJ风格的方法，这一事实不应被视为Spring团队倾向于采用Spring XML配置风格的@AspectJ注释风格方法。
>
> 请参阅 [选择使用哪种AOP声明样式](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-choosing) 以获得更完整的讨论每种风格的“为什么和如何做”。

### 5.3 AOP 代理

Spring AOP 默认使用标准 JDK 动态代理来实现 AOP 代理。这就使得任何接口（或者接口集合）都能够被代理。

Spring AOP 也可以使用 CGLIB 代理。为了代理接口之外的类时，这就是必要的。默认情况下，CGLIB 在业务对象没有实现一个接口时使用。基于接口编程而不是基于实现编程是一种好的实践，业务类通常都会实现一个或者多个业务接口。 [强制使用 CGLIB](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-proxying) 是可能的，我们希望这种情况很少出现，当你需要增强没有在接口中声明的方法时，或者你需要将一个被代理的对象作为一个具体类型传递给一个方法时。

掌握Spring AOP是基于代理的这一事实非常重要。请参阅 [了解AOP代理](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-understanding-aop-proxies) 以全面了解这个实现细节究竟意味着什么。

### 5.4 @AspectJ 支持

@AspectJ 指的是将切面声明为使用注解修饰的常规Java类的样式。作为AspectJ 5版本的一部分，[AspectJ项目](https://www.eclipse.org/aspectj) 引入了@AspectJ样式。Spring使用AspectJ提供的库解释与AspectJ 5相同的注解，用于切入点解析和匹配。但是，AOP运行时仍然是纯Spring AOP，并且不依赖于AspectJ编译器或者编织器。

> 使用AspectJ编译器和编织器可以使用完整的AspectJ语言，并在 [在 Spring 应用中使用AspectJ](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-using-aspectj) 中讨论。

