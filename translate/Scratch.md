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

