## 3. 验证，数据绑定和类型转化

将验证视为业务逻辑有利有弊，Spring 提供了针对验证（以及数据绑定）的设计，避免了这种麻烦。特别地，验证逻辑不应该与 web 层耦合，并应该便于本地化，同时应该可以插入任何可用的验证器。考虑到这些问题，Spring 提供了一个基本的`Validator`接口，它在应用的各个层次都非常有用。

数据绑定主要用来将用户输入动态绑定到应用的域模型（或者你用来处理用户输入的随便什么对象）。Spring 提供了一个合适的名字`DataBinder`来完成这项任务。`Validator`和`DataBinder`组成`validation`包，主要用于 MVC 框架中，但是并不局限于此。

`BeanWrapper`是 Spring 框架的一个基础概念，被用在很多地方。不过，可能你并不需要直接使用`BeanWrapper`。由于这是参考文档，我们觉得还是应该对它进行一些介绍比较合适。我们在这一章中解释`BeanWrapper`，因为，如果你正打算使用它，最大的可能性是你正在尝试将数据绑定到对象。

Spring 的`DataBinder`和低级`BeanWrapper`都使用了`PropertyEditorSupport`实现来转化和格式化属性值。`PropertyEditor`和`PropertyEditorSupport`类型都是 JavaBeans 规范的一部分，都在本章节中解释。Spring 3 引入了`cort.convert`包，该包提供了通用的类型转化工具，以及一个高级的格式化包用来格式化 UI 字段值。你可以使用这些包作为`PropertyEditorSupport`实现的更简单的替代品。它们也在本章中讨论。

> <center>JSR-303/JSR-349 Bean Validation</center>
>
> As of version 4.0, Spring Framework supports Bean Validation 1.0 (JSR-303) and Bean Validation 1.1 (JSR-349) for setup support and adapting them to Spring’s `Validator` interface.
>
> An application can choose to enable Bean Validation once globally, as described in [Spring Validation](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#validation-beanvalidation), and use it exclusively for all validation needs.
>
> An application can also register additional Spring `Validator` instances for each `DataBinder` instance, as described in [Configuring a `DataBinder`](https://docs.spring.io/spring/docs/5.1.8.RELEASE/spring-framework-reference/core.html#validation-binder). This may be useful for plugging in validation logic without the use of annotations.