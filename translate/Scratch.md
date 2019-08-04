### 5.6 选择何种 AOP 声明风格

一旦你决定了切面是实现给定需求的最佳方案，接下来你将如何决定使用 Spring AOP 或者 AspectJ ？使用 AspectJ 语言（代码）风格，@AspectJ 注解风格还是 Spring XML 风格？这些决定受到很多因素影响，包括应用需求，开发工具以及团队对 AOP 的熟悉程度。

#### 5.6.1 Spring AOP 还是完全使用 AspectJ?

使用满足需求的最简单的方案。Spring AOP 要比完全使用 AspectJ 要简单，因为不需要将 AspectJ 编译器和编织器引入你的开发和构建过程。如果你只需要增强 Spring beans 上的方法执行，Spring AOP 就是正确的选择。如果你需要增强不受 Spring 容器管理的对象（典型的，比如域对象），你就需要使用 AspectJ。当你希望增强简单方法之外的连接点（比如，字段的`get`或者`set`连接点等等）时，你也需要使用 AspectJ 。

使用 AspectJ 时，您可以选择 AspectJ 语言语法（也称为“代码样式”）或 @AspectJ 注释样式。显然，如果您不使用Java 5+，则可以选择：使用代码样式。如果切面在您的设计中发挥重要作用，并且您能够使用 Eclipse 的 [AspectJ开发工具（AJDT）](https://www.eclipse.org/ajdt/) 插件，则 AspectJ 语言语法是首选选项。它更清晰，更简单，因为该语言是专门为编写切面而设计的。如果您不使用 Eclipse 或只有几个切面在您的应用程序中不起主要作用，您可能需要考虑使用 @AspectJ 样式，在 IDE 中坚持使用常规 Java 编译，并添加一个切面编织阶段到你的构建脚本。

#### 5.6.2 通过 @AspectJ 还是 XML 来使用 Spring AOP?

如果您选择使用 Spring AOP，则可以选择 @AspectJ 或 XML 风格。需要考虑各种权衡。

XML 风格可能是现有 Spring 用户最熟悉的，并且由真正的 POJO 支持。当使用 AOP 作为配置企业服务的工具时，XML 可能是一个不错的选择（一个好的测试是你是否认为切入点表达式是你可能想要独立改变的配置的一部分）。使用 XML 风格，从您的配置可以更清楚地了解系统中存在哪些切面。

XML 风格有两个缺点。首先，它没有将解决的需求的实现完全封装在一个地方。DRY 原则规定，系统中的任何知识都应该有单一，明确，权威的表示。使用 XML 风格时，有关如何实现需求的知识将分散到支持 bean 类的声明和配置文件中的 XML。使用 @AspectJ 风格时，此信息封装在单个模块中：切面。其次，XML 风格在它可以表达的内容方面比 @AspectJ 样式稍微受限：仅支持“单例”切面实例化模型，并且不可能组合在 XML 中声明的命名切入点。例如，在 @AspectJ 风格中，您可以编写如下内容：

```java
@Pointcut("execution(* get*())")
public void propertyAccess() {}

@Pointcut("execution(org.xyz.Account+ *(..))")
public void operationReturningAnAccount() {}

@Pointcut("propertyAccess() && operationReturningAnAccount()")
public void accountPropertyAccess() {}
```

在 XML 风格中，您可以声明前两个切入点：

```xml
<aop:pointcut id="propertyAccess"
        expression="execution(* get*())"/>

<aop:pointcut id="operationReturningAnAccount"
        expression="execution(org.xyz.Account+ *(..))"/>
```

XML 方法的缺点是您无法通过组合这些定义来定义`accountPropertyAccess`切入点。

@AspectJ 风格支持额外的实例化模型和更丰富的切入点组合。它具有将切面保持为模块化单元的优点。它还具有以下优点：Spring AOP 和 AspectJ 都可以理解（并因此消耗）@AspectJ 切面。因此，如果您以后决定需要 AspectJ 的功能来实现其他要求，则可以轻松迁移到经典的 AspectJ 设置。总的来说，除了简单的企业服务配置之外，Spring 团队更喜欢 @AspectJ 风格的自定义切面。

### 5.7 混合切面类型

通过使用自动代理支持，模式定义的`<aop:aspect>`切面，`<aop:advisor>`声明的增强器，甚至是同一配置中其他风格的代理和拦截器，完全可以混合 @AspectJ 风格切面。所有这些都是通过使用相同的底层支持机制实现的，并且可以毫无困难地共存。

