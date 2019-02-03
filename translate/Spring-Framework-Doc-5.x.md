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

