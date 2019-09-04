### Naming 包

[`javax.naming`](https://docs.oracle.com/javase/8/docs/api/javax/naming/package-summary.html) 包包含访问命名服务的类和接口。

**上下文**

`javax.naming` 包定义一个 [`Context`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Context.html) 接口，它是查找，绑定/解绑，重命名对象，创建和销毁子上下文等功能的核心接口。

- Lookup

  最常用的操作就是 [`lookup()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Context.html#lookup-javax.naming.Name-) 。你将查找的对象的名称传递给 `lookup()` 方法，它将返回绑定到该名称的对象。

- Bindings

  [`listBindings()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Context.html#listBindings-javax.naming.Name-) 返回一个名称—对象映射的枚举。一个绑定时一个三元组，包含对象名称，对象类名，以及对象自身。

- List

  [`list()`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Context.html#list-javax.naming.Name-) 类似于 `listBindings()` ，除了它返回一个包含对象名称和对象类名的枚举。`list()` 对应用非常有用，例如浏览器希望获取上下文中绑定的对象信息，但是又不需要实际的对象本身。尽管 `listBindings()` 提供了全部的相同信息，但是它是一个潜在的更加昂贵的操作。

- Name

  `Name` 是一个表示通用名称—零个或者多个组件的有序序列的接口。命名系统使用此接口来定义遵循它的命名约定的名称。命名约定在后续的 [Naming and Directory Concepts](https://docs.oracle.com/javase/tutorial/jndi/concepts/index.html) 中描述。

- References

  对象以不同方式存储在命名和目录服务中。引用可能是对象的非常紧凑的表示。JNDI定义 [`Reference`](https://docs.oracle.com/javase/8/docs/api/javax/naming/Reference.html) 类来表示引用。引用包含有关如何构造对象副本的信息。JNDI将尝试将从目录中查找的引用转换为它们所代表的Java对象，以便JNDI客户端可以安全地认为目录中存储的内容是Java对象。

**初始上下文**

在JNDI中，所有命名和目录操作都是相对于上下文执行的。没有绝对的根。因此，JNDI定义了一个`InitialContext`，它为命名和目录操作提供了一个起点。获得初始上下文后，可以使用它来查找其他上下文和对象。

**异常**

JNDI定义了在执行命名和目录操作过程中可以抛出的异常的类层次结构。此类层次结构的根是`NamingException`。对处理特定异常感兴趣的程序可以捕获异常的相应子类。否则，应该捕获`NamingException`。

