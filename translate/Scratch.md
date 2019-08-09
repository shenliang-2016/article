#### 5.10.1 在使用 Spring 依赖注入的域对象中使用 AspectJ

Spring 容器会实例化并配置定义你在应用上下文中定义的 beans。它也可能要求 bean 工厂配置一个预先存在的对象，给定包含需要应用的配置的 bean 定义的名称。`spring-aspects.jar`包含一个注解驱动的切面，它利用此能力来允许任意对象的依赖注入。这种支持希望被用于那些在任何容器控制范围之外创建的对象。域对象通常采用此策略，因为他们经常采用编程方式使用`new`操作符创建，或者作为查询结果由 ORM 工具创建。

`@Configurable`注解将一个类标记为适合于 Spring 驱动的配置。在最简单的场景中，你可以只使用它作为标记注解，如下面例子所示：

```java
package com.xyz.myapp.domain;

import org.springframework.beans.factory.annotation.Configurable;

@Configurable
public class Account {
    // ...
}
```

当以这种方式被用作标记注解时，Spring 配置被注解修饰的类型（`Account`，在此例子中）的新实例，通过使用名为全限定类型名（`com.xyz.myapp.domain.Account`）的 bean 定义（典型地是原型作用域）。由于 bean 默认名称是它的类型的全限定名，声明该原型的便捷方法是忽略其中的`id`属性，如下面例子所示：

```xml
<bean class="com.xyz.myapp.domain.Account" scope="prototype">
    <property name="fundsTransferService" ref="fundsTransferService"/>
</bean>
```

如果你想要显示指定要使用的原型 bean 定义的名称，你可以直接在注解里这么做，如下面例子所示：

```java
package com.xyz.myapp.domain;

import org.springframework.beans.factory.annotation.Configurable;

@Configurable("account")
public class Account {
    // ...
}
```

Spring 现在会寻找名为`account`的 bean 定义并将其用于新的`Account`实例的配置。

你也可以使用自动绑定来避免必须指定 bean 定义名称。为了使用 Spring 自动绑定，使用`@Configurable`注解的`autowire`属性。你可以指定`@Configurable(autowire=Autowire.BY_TYPE)`或者`@Configurable(autowire=Autowire.BY_NAME)`，前者表示按照类型自动绑定，后者按照名称自动绑定。作为替代方案，最好在字段或方法级别通过`@Autowired`或`@Inject`为`@Configurable` bean指定显式的注解驱动依赖注入（有关更多详细信息，请参阅 [基于注解的容器配置](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#beans-annotation-config) ）。

最后，你可以开启 Spring 依赖检查，对新创建和配置的对象中的对象引用进行检查，使用`dependencyCheck`属性（比如，`@Configurable(autowire=Autowire.BY_NAME,dependencyCheck=ture`）。如果该属性设置为`true`，Spring 将在配置完成之后校验所有的属性（那些不是基本数据类型或者集合类型的属性）已经被设置。

请注意，对其本身使用的注解不会做任何事情。`Spring-aspects.jar`中的`AnnotationBeanConfigurerAspect`作用于存在的注解。本质上，该切面意味着，“从使用`@Configurable`注解修饰的类型的新对象的初始化返回后，根据注解的属性使用 Spring 配置新创建的对象”。在此上下文中，“初始化”是指新实例化的对象（例如，使用`new`操作符实例化的对象）以及正在进行反序列化的`Serializable`对象（例如，通过[readResolve()](https://docs.oracle.com/javase/8/docs/api/java/io/Serializable.html)）。

> 上面段落中的一个关键短语是“实质上”。对于大多数情况，“从新对象初始化返回后”的确切语义很好。在此上下文中，“初始化之后”意味着在构造对象之后注入依赖项。这意味着依赖项不可用于类的构造函数体。如果希望在构造函数体执行之前注入依赖项，从而可以在构造函数体中使用，则需要在`@Configurable`声明中定义它，如下所示：
>
> `````java
> @Configurable(preConstruction = true)
> `````
>
> 你可以在  [AspectJ Programming Guide](https://www.eclipse.org/aspectj/doc/next/progguide/index.html) 中找到更多有关 AspectJ 中的各种切入点类型的语言语义的信息。

