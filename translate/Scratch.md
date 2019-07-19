### 1.16 `BeanFactory`

`BeanFactory` API 提供了 Spring IoC 功能的底层基础。它确定的契约被广泛用于与 Spring 的其它部分或者相关的第三方框架集成，同时它的`DefaultListableBeanFactory`实现是更高层次的`GenericApplicationContext`容器中的一个关键代理。

`BeanFactory`以及相关的接口（比如`BeanFactoryAware`，`InitializingBean`，`DisposableBean`）都是其它框架组件的重要的集成点。不需要任何注解甚至是反射，它们允许容器和它的组件之间非常有效的交叉。应用层面的 beans 可以使用相同的回调接口，但是通常更倾向于使用声明式依赖注，要么通过注解，要么通过编程式配置。

注意，核心`BeanFactory` API 层级和它的`DefaultListableBeanFactory`实现不会对配置格式或者注解应用到的所有组件做任何假定。所有这些风格都通过扩展（例如`XmlBeanDefinitionReader`和`AutowiredAnnotationBeanPostProcessor`）进行，并作为核心元数据表示在共享`BeanDefinition`对象上运行。这是使Spring的容器如此灵活和可扩展的本质。

#### 1.16.1. `BeanFactory` 还是 `ApplicationContext`?

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

