### 6.6 使用 `ProxyFactory` 以编程方式创建 AOP 代理

使用 Spring 通过编程方式可以很容易地创建 AOP 代理。这使得你可以使用 Spring AOP 而不需要依赖 Spring IoC。

目标对象实现的接口会被自动代理。下面的例子展示了一个目标对象的代理的创建，使用一个拦截器和一个增强器：

```java
ProxyFactory factory = new ProxyFactory(myBusinessInterfaceImpl);
factory.addAdvice(myMethodInterceptor);
factory.addAdvisor(myAdvisor);
MyBusinessInterface tb = (MyBusinessInterface) factory.getProxy();
```

第一步是构造一个 `org.springframework.aop.framework.ProxyFactory` 类型的对象。你可以使用一个目标对象来创建它，如前面例子所示，或者在备用构造方法中指定需要被代理的接口。

你可以添加增强（拦截器作为一类特殊的增强），增强器，或者同时添加两者，并为`ProxyFactory` 的声明周期维护它们。如果你添加一个 `IntroductionInterceptionAroundAdvisor` ，你就可以让该代理实现额外的接口。

`ProxyFactory` 上有些方便方法（继承自 `AdvisedSupported`）允许你添加其它增强类型，比如前置增强和抛出增强。`AdvisedSupport` 是`ProxyFactory`和`ProxyFactoryBean`的超类。

> 在大多数应用程序中，将AOP代理创建与IoC框架集成是最佳实践。通常，我们建议您将使用AOP的Java代码的配置外部化。

### 6.7 操作被增强的对象

但是，无论您如何创建AOP代理，都可以使用`org.springframework.aop.framework.Advised`接口来操作它们。 无论它实现哪个其他接口，任何AOP代理都可以转换为此接口。该接口包括以下方法：

```java
Advisor[] getAdvisors();

void addAdvice(Advice advice) throws AopConfigException;

void addAdvice(int pos, Advice advice) throws AopConfigException;

void addAdvisor(Advisor advisor) throws AopConfigException;

void addAdvisor(int pos, Advisor advisor) throws AopConfigException;

int indexOf(Advisor advisor);

boolean removeAdvisor(Advisor advisor) throws AopConfigException;

void removeAdvisor(int index) throws AopConfigException;

boolean replaceAdvisor(Advisor a, Advisor b) throws AopConfigException;

boolean isFrozen();
```

`getAdvisors()`方法为每个增强器，拦截器或已添加到工厂的其他增强类型返回一个`Advisor`。如果添加了`Advisor`，则此索引返回的增强器是您添加的对象。如果您添加了一个拦截器或其他增强类型，Spring 会将其包含在一个增强器中，并且该增强器关联的切入点始终返回`true`。因此，如果添加了一个`MethodInterceptor`，则为此索引返回的增强器是一个`DefaultPointcutAdvisor`，它返回`MethodInterceptor`和一个匹配所有类和方法的切入点。

`addAdvisor()`方法可用于添加任何`Advisor`。通常，持有切入点和增强的增强器是通用的`DefaultPointcutAdvisor`，您可以将其用于任何增强或切入点（但不适用于引介）。

默认情况下，即使创建了代理，也可以添加或删除增强器或拦截器。唯一的限制是不可能添加或删除引介增强器，因为来自工厂的现有代理不显示接口更改。（您可以从工厂获取新代理以避免此问题。）

以下示例显示将AOP代理转换为`Advised`接口并检查和操作其增强：

```java
Advised advised = (Advised) myObject;
Advisor[] advisors = advised.getAdvisors();
int oldAdvisorCount = advisors.length;
System.out.println(oldAdvisorCount + " advisors");

// Add an advice like an interceptor without a pointcut
// Will match all proxied methods
// Can use for interceptors, before, after returning or throws advice
advised.addAdvice(new DebugInterceptor());

// Add selective advice using a pointcut
advised.addAdvisor(new DefaultPointcutAdvisor(mySpecialPointcut, myAdvice));

assertEquals("Added two advisors", oldAdvisorCount + 2, advised.getAdvisors().length);
```

> 尽管存在合法的使用案例，但是否有必要修改生产中的业务对象的增强是值得怀疑的（没有双关语意）。但是，它在开发中非常有用（例如，在测试中）。我们有时发现能够以拦截器或其他增强的形式添加测试代码，进入我们想要测试的方法调用非常有用。（例如，在为回滚标记事务之前，增强可以进入为该方法创建的事务内部，可能运行SQL以检查数据库是否已正确更新。）

根据您创建代理的方式，通常可以设置`frozen`标志。在这种情况下，`Advised` `isFrozen()`方法返回`true`，任何通过添加或删除来修改增强的尝试都会导致`AopConfigException`。在某些情况下，冻结被增强对象状态的能力很有用（例如，防止调用代码删除安全拦截器）。

