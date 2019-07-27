因为 Spring AOP 限制仅仅匹配到方法执行连接点，前面对切入点指示符的讨论给出了一个相对于 AspectJ 编程向导中给出的更严格的定义。另外，AspectJ 本身也有基于类型的语义，同时，在方法执行连接点处，`this`和`target`指向同一个对象，该对象执行该方法。Spring AOP 是基于代理的系统，它区分代理对象本身（绑定到`this`）和代理背后的目标对象（绑定到`target`）。

> 由于Spring的AOP框架基于代理的特性，根据定义，目标对象内部的调用不会被截获。对于JDK代理，只能拦截代理上的公共接口方法调用。使用CGLIB，代理上的公共和受保护方法调用被截获（如果需要，甚至是包可见的方法）。但是，通过代理进行的常见交互应始终通过公共签名进行设计。
>
> 请注意，切入点定义通常与任何截获的方法匹配。如果切入点是严格意义上的仅仅用于公开方法的，即使在通过代理进行潜在非公共交互的CGLIB代理方案中，也需要相应地定义切入点。
>
> 如果您的拦截需要包括目标类中的方法调用甚至构造函数，请考虑使用Spring驱动的 [本地AspectJ编织](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#aop-aj-ltw) 而不是Spring的基于代理的AOP框架。这构成了具有不同特征的不同AOP使用模式，因此在做出决定之前一定要熟悉编织。

Spring AOP还支持另一个名为`bean`的PCD。此PCD允许您将连接点的匹配限制为特定的命名Spring bean或一组命名的Spring bean（使用通配符时）。 `bean` PCD具有以下形式：

```
bean(idOrNameOfBean)
```

`idOrNameOfBean`标记可以是任何Spring bean的名称。提供了使用`*`字符的有限通配符支持，因此，如果为Spring bean建立了一些命名约定，则可以编写一个`bean` PCD表达式来选择它们。与其他切入点指示符的情况一样，`bean`PCD也可以与`&&`（和），`||`（或）和`!`（否定）运算符一起使用。

> `bean` PCD仅在Spring AOP中受支持，而在本地AspectJ编织中不受支持。它是AspectJ定义的标准PCD的特定于Spring的扩展，因此不适用于`@Aspect`模型中声明的方面。
>
> `bean` PCD在实例级别（基于Spring bean名称概念）而不是仅在类型级别（基于编织的AOP受限）上运行。基于实例的切入点指示符是Spring基于代理的AOP框架的一种特殊功能，它与Spring bean工厂紧密集成，通过名称可以自然而直接地识别特定的bean。

