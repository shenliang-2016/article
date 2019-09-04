# Testing

**Version 5.1.9.RELEASE**

本章节涵盖 Spring 对集成测试和单元测试最佳实践的支持。Spring 团队推崇测试驱动开发模式（TDD）。Spring 团队已经发现控制反转（IoC）的正确使用是的单元测试和集成测试变得更简单（因为类的`setter`方法和适当的构造函数的存在使它们更容易在测试中连接在一起，而无需设置服务定位器注册表和类似的结构）。

## 1. Spring Testing 介绍

测试是企业软件开发不可或缺的一部分。 本章重点介绍IoC原理对 [unit testing](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#unit-testing) 的好处以及Spring Framework对 [integration testing](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#integration-testing) 支持的好处。（对企业中的测试进行全面处理超出了本参考手册的范围。）

## 2. 单元测试

与传统的Java EE开发相比，依赖注入应该使您的代码对容器的依赖性降低。构成应用程序的POJO应该在JUnit或TestNG测试中可测试，对象使用`new`运算符实例化，不使用Spring或任何其他容器。您可以使用 [mock objects](https://docs.spring.io/spring/docs/5.1.9.RELEASE/spring-framework-reference/testing.html#mock-objects) （与其他有价值的测试技术结合使用）来单独测试代码。如果您遵循Spring的体系结构建议，那么代码库的干净分层和组件化便于单元测试。例如，您可以通过存根或模拟DAO或存储库接口来测试服务层对象，而无需在运行单元测试时访问持久数据。

真正的单元测试通常运行得非常快，因为没有要设置的运行时基础结构。强调真正的单元测试作为开发方法的一部分可以提高您的工作效率。您可能不需要本章节的这一部分来帮助您为基于IoC的应用程序编写有效的单元测试。但是，对于某些单元测试场景，Spring Framework提供了模拟对象和测试支持类，本章将对其进行介绍。

