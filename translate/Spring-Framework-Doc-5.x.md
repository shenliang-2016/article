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

### 1. Spring  是什么意思

Spring 这个词在不同的语境下有不同的含义。可以用于指代 Spring 框架本身，这也是它的最初含义。随着时间推移，其它的  Spring 项目基于 Spring 框架逐步构建起来。但多数情况下，人们谈到 Spring ，指的其实是整个项目家族。本参考文档只关注基础，Spring 框架本身。

Spring 框架被分为多个模块。应用可以各取所需。处于核心地位的是所谓的核心容器，包括一个配置模型和一套依赖注入机制。在此之外，框架提供了对多种不同应用技术架构的基础支持，包括消息、数据事务和持久化以及 web 。框架还包括基于 Servlet 的 Spring MVC web 框架，以及与之平行的，Spring WebFlux 响应式 web 框架。

关于模块的说明：

Spring 框架的 jar 包可以部署到 JDK 9 的模块路径（“Jigsaw”）下。当然，框架的模块在 JDK 8 和 JDK 9 的 classpath 下都可以正常工作。

### 2. Spring 和 Spring 框架的历史

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

### 3. 设计哲学

学习一个框架，重要的不仅是了解它都做了什么，更重要的是把握它所遵循的基本原则。Spring 框架的指导思想如下：

* 提供各个层面的选择。Spring 支持你尽可能晚地做出设计决策。例如，你可以通过修改配置文件的方式切换持久化提供者，而不需要修改代码。类似的做法也适用于很多其它的基础组件和第三方 APIs 的集成。
* 不同角度的协调。Spring 提供丰富的扩展性，但是并不替你做任何决定。它从不同角度提供了很广泛的应用需求支持。
* 保持向后兼容。Spring 的进化很谨慎，尽可能少地在新版本中改变已有功能特性的修改。同时，很谨慎地选择 JDK 版本和第三方库，便于基于 Spring 的应用和库的维护。
* 谨慎的 API 设计。Spring 团队投入了大量的精力和时间进行 API 设计，尽力在所有版本中始终保持 API 的直观性。
* 重视代码质量。Spring 框架投入大量努力保持文档的清晰精确并及时更新。同时，它也是为数不多的几个敢于公开声称拥有干净的代码结构而绝对不存在包的循环依赖的项目之一。

### 4. 反馈和贡献

### 5. 新手上路

----

# 核心技术

----

这一部分涵盖了 Spring 框架必需的所有技术。

