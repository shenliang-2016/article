### 6.4 使用 `ProxyFactoryBean` 创建 AOP 代理

如果你使用的是 Spring IoC 容器（`ApplicationContext` 或者 `BeanFactory`）来管理你的业务对象（你本来就应该这样做！），你可能会希望使用 Spring AOP `FactoryBean` 实现。（记住，bean 工厂引入了一个间接层，允许它创建不同类型的对象。）

> Spring AOP 支持内部也使用了 bean 工厂。

Spring 中创建一个 AOP 代理的基本方法是使用 `org.springframework.aop.framework.ProxyFactoryBean` 。这提供了对切入点、应用的增强、以及它们的顺序的完整控制。不过，如果你不需要这些控制，还是存在一些更简单的选项。

#### 6.4.1 基础

`ProxyFactoryBean` ，类似于其它 Spring `FactoryBean` 实现，引入了一个间接层。如果你定义了一个名为 `foo` 的 `ProxyFactoryBean` ，引入 `foo` 的对象看不到该 `ProxyFactoryBean` 实例本身，只能看到 `ProxyFactoryBean` 的 `getObject()` 方法实现创建的对象。该方法创建一个包装目标对象的 AOP 代理。

使用 `ProxyFactoryBean` 或者其它 IoC 敏感的类来创建 AOP 代理的的最主要的好处就是增强和切入点也能够被 IoC 管理。这是一个强大的特性，使用其它 AOP 框架可能很难实现同样的效果。比如，一个增强本身可以引用应用对象（除了目标对象，这应该在任何 AOP 框架中都可用），受益于依赖注入提供的所有可插拔性。

#### 6.4.2 JavaBean 属性

与 Spring 提供的大多数`FactoryBean`实现一样，`ProxyFactoryBean`类本身就是一个 JavaBean。其属性用于：

 - 指定要代理的目标。
 - 指定是否使用 CGLIB（稍后描述并参见 [基于JDK和CGLIB的代理](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-pfb-proxy-types) ）。

一些关键属性是继承自 `org.springframework.aop.framework.ProxyConfig` （Spring 中所有 AOP 代理工厂的超类）。这些关键属性包括：

 -  `proxyTargetClass`：如果要代理目标类，而不是目标类的接口，则为`true`。如果此属性值设置为`true`，则会创建 CGLIB 代理（但另请参阅 [基于JDK和CGLIB的代理](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-pfb-proxy-types) ）。
 -  `optimize`：控制是否将积极优化应用于通过 CGLIB 创建的代理。除非您完全了解相关 AOP 代理如何处理优化，否则您不应轻易使用此设置。目前仅用于 CGLIB 代理。它对JDK动态代理没有影响。
 -  `frozen`：如果代理配置为`frozen`，则不再允许对配置进行更改。这既可以作为轻微的优化，也可以用于在创建代理后不希望调用者能够操作代理（通过 `Advised` 接口）的情况。此属性的默认值为`false`，因此允许更改（例如添加其他增强）。
 -  `exposeProxy`：确定当前代理是否应该在`ThreadLocal`中暴露，以便目标可以访问它。如果目标需要获取代理并且`exposeProxy`属性设置为`true`，则目标可以使用`AopContext.currentProxy()`方法。

特定于 `ProxyFactoryBean` 的其它属性包括：

 -  `proxyInterfaces`：`String`接口名称的数组。如果未提供，则使用目标类的 CGLIB 代理（但另请参阅 [基于JDK和CGLIB的代理](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-pfb-proxy-types) ）。
 -  `interceptorNames`：要应用的`Advisor`，拦截器或其他增强名称的`String`数组。顺序非常重要，最基础的是先到先服务的顺序。也就是说，列表中的第一个拦截器是第一个能够拦截调用的拦截器。
     名称是当前工厂中的 bean 名称，包括来自祖先工厂的 bean 名称。你不能在这里提到 bean 引用，因为这样做会导致`ProxyFactoryBean`忽略增强的单例设置。
     您可以使用星号（*）附加拦截器名称。这样做会导致应用中所有其名称以星号之前的部分开头的增强器 bean 被应用。您可以在 [使用“全局”增强器](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-global-advisors) 中找到使用此功能的示例。
 -  `singleton`：无论调用`getObject()`方法的频率如何，工厂是否应该返回单个对象。几个`FactoryBean`实现提供了这样的方法。默认值是`true`。如果您想使用有状态增强 - 例如，对于有状态的mixins  - 使用原型增强以及单个值`false`。

