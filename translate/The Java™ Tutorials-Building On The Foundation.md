# Java™教程

[主页](https://docs.oracle.com/javase/tutorial/index.html)

## Java教程学习路径

> Java教程是为JDK 8编写的。本页描述的示例和实践没有利用后续版本中引入的改进。

## 入门

- [入门](https://docs.oracle.com/javase/tutorial/getStarted/index.html) - 介绍Java技术和安装Java开发软件并使用它来创建简单程序的课程。
- [学习Java语言](https://docs.oracle.com/javase/tutorial/java/index.html) - 描述基本概念（如类，对象，继承，数据类型，泛型和包）的课程。
- [基本Java类](https://docs.oracle.com/javase/tutorial/essential/index.html) - 有关异常，基本输入/输出，并发，正则表达式和平台环境的课程。

## 基础

- [集合](https://docs.oracle.com/javase/tutorial/collections/index.html) - 使用和扩展Java集合框架的经验教训。
- [Lambda表达式](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html)：了解如何以及为何在应用程序中使用Lambda表达式。
- [聚合操作](https://docs.oracle.com/javase/tutorial/collections/streams/index.html)：探索聚合操作，流和Lambda表达式如何协同工作以提供强大的过滤功能。
- [JAR文件中的打包程序](https://docs.oracle.com/javase/tutorial/deployment/jar/index.html) - 有关创建和签署JAR文件的课程。
- [国际化](https://docs.oracle.com/javase/tutorial/i18n/index.html) - 设计软件的介绍，以便可以轻松地适应（本地化）各种语言和区域。
- [反射](https://docs.oracle.com/javase/tutorial/reflect/index.html) - 表示（“反映”）当前Java虚拟机中的类，接口和对象的API。
- [安全性](https://docs.oracle.com/javase/tutorial/security/index.html) - Java平台功能，有助于保护应用程序免受恶意软
- [JavaBeans](https://docs.oracle.com/javase/tutorial/javabeans/index.html) - Java平台的组件技术。
- [扩展机制](https://docs.oracle.com/javase/tutorial/ext/index.html) - 如何使Java平台上运行的所有应用程序都可以使用自定义API。
- [泛型](https://docs.oracle.com/javase/tutorial/extra/generics/index.html) - 对类型系统的增强，支持对各种类型的对象的操作，同时提供编译时类型安全性。

## 客户端开发

- [JavaFX入门](http://www.oracle.com/pls/topic/lookup?ctx=javase80&id=JFXST804) - 一组示例应用程序，旨在帮助您开始使用常见的JavaFX任务
- [Scene Builder入门](http://www.oracle.com/pls/topic/lookup?ctx=javase80&id=JSBGS101) - 逐步向您展示如何使用JavaFX Scene Builder工具创建简单的问题跟踪应用程序。
- [使用Swing创建GUI](https://docs.oracle.com/javase/tutorial/uiswing/index.html) - 全面介绍Java平台上的GUI创建。
- [部署](https://docs.oracle.com/javase/tutorial/deployment/index.html) - 如何使用JAR文件打包应用程序和applet，并使用Java Web Start和Java Plug-in进行部署。
- [2D图形](https://docs.oracle.com/javase/tutorial/2d/index.html) - 如何在应用程序中显示和打印2D图形。
- [全屏独占模式API](https://docs.oracle.com/javase/tutorial/extra/fullscreen/index.html) - 如何编写更充分利用用户图形硬件的应用程序。

## 服务端开发

- [JDBC数据库访问](https://docs.oracle.com/javase/tutorial/jdbc/index.html) - 介绍用于Java应用程序与各种数据库和数据源之间的连接的API。
- [JMX](https://docs.oracle.com/javase/tutorial/jmx/index.html) - Java Management Extensions提供了一种管理应用程序，设备和服务等资源的标准方法。
- [JNDI](https://docs.oracle.com/javase/tutorial/jndi/index.html) - Java命名和目录接口支持访问DNS和LDAP等命名和目录服务。
- [JAXP](https://docs.oracle.com/javase/tutorial/jaxp/index.html) - 介绍用于XML处理的Java API（JAXP）1.4技术。
- [RMI](https://docs.oracle.com/javase/tutorial/rmi/index.html) - 远程方法调用API允许对象调用在另一个Java虚拟机上运行的对象的方法。
- [并发](https://docs.oracle.com/javase/tutorial/essential/concurrency/index.html) - Java平台具有API，可帮助您开发多线程程序。


# 集合

本节介绍Java Collections Framework。在这里，您将了解集合是什么以及如何使您的工作更轻松，程序更好。您将了解构成Java Collections Framework的核心元素 - 接口，实现，聚合操作和算法。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**介绍**](https://docs.oracle.com/javase/tutorial/collections/intro/index.html) 告诉您什么是集合，以及它们如何使您的工作更轻松，您的程序更好。您将了解构成集合框架的核心元素：接口，实现和算法。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**接口**](https://docs.oracle.com/javase/tutorial/collections/interfaces/index.html) 描述了核心集合接口，它是Java Collections Framework的核心和灵魂。您将学习有效使用这些接口的一般准则，包括何时使用哪个接口。您还将学习每个接口的习惯用法，以帮助您充分利用接口。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**聚合操作**](https://docs.oracle.com/javase/tutorial/collections/streams/index.html) 迭代集合，这使您能够编写更简洁有效的代码来处理存储在集合中的元素。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**实现**](https://docs.oracle.com/javase/tutorial/collections/implementations/index.html) 描述了JDK的通用集合实现，并告诉您何时使用哪个实现。您还将了解包装器实现，它为通用实现添加功能。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**算法**](https://docs.oracle.com/javase/tutorial/collections/algorithms/index.html) 描述了JDK提供的用于对集合进行操作的多态算法。运气好的话，你再也不用写自己的排序程序了！

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**自定义实现**](https://docs.oracle.com/javase/tutorial/collections/custom-implementations/index.html) 告诉你为什么你可能想要编写自己的集合实现（而不是使用JDK提供的一个通用实现），以及你如何去做。使用JDK的抽象集合实现很容易！

[![trail icon](https://docs.oracle.com/javase/tutorial/images/coreIcon.gif)**互操作性**](https://docs.oracle.com/javase/tutorial/collections/interoperability/index.html) 告诉您集合框架如何与早于将集合添加到Java之前的API进行互操作。此外，它还告诉您如何设计新的API，以便它们可以与其他新API无缝地互操作。

## 介绍

集合（有时称为容器）只是一个将多个元素组合到一个单元中的对象。集合用于存储，检索，操作和传递聚合数据。通常，它们表示形成自然组的数据项，例如扑克牌（卡片集合），邮件文件夹（字母集合）或电话目录（名称到电话号码的映射）。如果您使用过Java编程语言 - 或者只使用其他任何编程语言 - 那么您已经熟悉了集合。

**什么是集合框架？**

集合框架是用于表示和操作集合的统一体系结构。所有集合框架都包含以下内容：

 - 接口：这些是表示集合的抽象数据类型。接口允许独立于其表示的细节来操纵集合。在面向对象语言中，接口通常形成层次结构。
 - 实现：这些是集合接口的具体实现。实质上，它们是可重用的数据结构。
 - 算法：这些是对实现集合接口的对象执行有用计算（如搜索和排序）的方法。算法被认为是多态的：也就是说，相同的方法可以用于适当的集合接口的许多不同实现。实质上，算法是可重用的功能。

除了Java Collections Framework之外，最着名的集合框架示例是C++标准模板库（STL）和Smalltalk的集合层次结构。从历史上看，集合框架相当复杂，这使得它们具有陡峭的学习曲线的声誉。我们相信Java Collections Framework打破了这一传统，因为您将在本章中自学。

**Java Collections Framework 的好处**

Java Collections Framework提供以下好处：

- **减少编程工作：** 通过提供有用的数据结构和算法，Collections Framework可以让您专注于程序的重要部分，而不是使其工作所需的低级“管道”。通过促进不相关API之间的互操作性，Java Collections Framework使您无需编写适配器对象或转换代码来连接API。
- **提高程序速度和质量：** 集合框架提供有用数据结构和算法的高性能，高质量实现。每个接口的各种实现是可互换的，因此可以通过切换集合实现来轻松调整程序。因为您没有编写自己的数据结构的苦差事，所以您将有更多的时间投入到改进程序的质量和性能上。
- **允许不相关的API之间的互操作性：** 集合接口是通过其API来回传递集合的本地语言。如果我的网络管理API提供了一组节点名称，并且您的GUI工具包需要一组列标题，那么我们的API将无缝地互操作，即使它们是独立编写的。
- **减少学习和使用新API的工作量：** 许多API自然地在输入上收集集合并将它们作为输出提供。过去，每个这样的API都有一个专门用于操作其集合的小型子API。这些专用集合子API之间几乎没有一致性，因此您必须从头开始学习每一个，并且在使用它们时很容易出错。随着标准集合接口的出现，问题就消失了。
- **减少设计新API的工作量：** 这是之前优势的另一面。设计人员和实施人员每次创建依赖于集合的API时都不必重新发明轮子；相反，他们可以使用标准的集合接口。
- **促进软件重用：** 符合标准集合接口的新数据结构本质上是可重用的。对于实现这些接口的对象进行操作的新算法也是如此。

## 接口

核心集合接口封装了不同类型的集合，如下图所示。这些接口允许独立于其表示的细节来操纵集合。核心集合接口是Java集合框架的基础。如下图所示，核心集合接口形成层次结构。

![Two interface trees, one starting with Collection and including Set, SortedSet, List, and Queue, and the other starting with Map and including SortedMap.](https://docs.oracle.com/javase/tutorial/figures/collections/colls-coreInterfaces.gif)

核心集合接口。

`Set`是一种特殊的`Collection`，`SortedSet`是一种特殊的`Set`，依此类推。另请注意，层次结构由两个不同的树组成 -  `Map`不是真正的`Collection`。

请注意，所有核心集合接口都是泛型化的。例如，这是`Collection`接口的声明。

```java
public interface Collection<E>...
```

`<E>`语法告诉您该接口是泛型化的。声明`Collection`实例时，您可以并且应该指定集合中包含的对象类型。指定类型允许编译器验证（在编译时）您放入集合的对象类型是否正确，从而减少运行时的错误。有关泛型类型的信息，请参阅 [Generics (Updated)](https://docs.oracle.com/javase/tutorial/java/generics/index.html) 课程。

当您了解如何使用这些接口时，您将了解有关Java Collections Framework的大部分知识。本章讨论有效使用接口的一般准则，包括何时使用哪个接口。您还将学习每个接口的编程习惯用语，以帮助您充分利用它。

为了保持核心集合接口的数量可管理，Java平台不为每个集合类型的每个变体提供单独的接口。（这些变体可能包括不可变，固定大小和仅可附加。）相反，每个接口中的修改操作都被指定为可选 - 给定的实现可以选择不支持所有操作。如果调用了不受支持的操作，则集合将抛出 [`UnsupportedOperationException`](https://docs.oracle.com/javase/8/docs/api/java/lang/UnsupportedOperationException.html) 。实现负责记录它们支持哪些可选操作。所有Java平台的通用实现都支持所有可选操作。

以下列表描述了核心集合接口：

- `Collection` — 集合层次结构的根。集合表示一组称为其元素的对象。`Collection`接口是所有集合实现的最小公分母，用于传递集合并在需要最大通用性时对其进行操作。某些类型的集合允许重复元素，而其他集合则不允许。有些是有序的，有些则是无序的。Java平台不提供此接口的任何直接实现，但提供了更具体的子接口的实现，例如`Set`和`List`。另请参阅 [The Collection Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/collection.html) 部分。

- `Set` — 一个不能包含重复元素的集合。该接口对数学集合抽象进行建模，并用于表示集合，例如包含扑克手牌的卡片，构成学生日程表的课程或在机器上运行的进程。另请参见 [The Set Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/set.html) 部分。

- `List` — 有序集合（有时称为序列）。列表可以包含重复元素。`List`的用户通常可以精确控制列表中每个元素的插入位置，并可以通过整数索引（位置）访问元素。如果您使用过`Vector`，那么您就熟悉`List`的一般风格。另请参阅 [The List Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/list.html) 部分。

- `Queue` — 用于在处理之前保存多个元素的集合。除了基本的`Collection`操作外，`Queue`还提供额外的插入，提取和检查操作。

  队列通常（但不一定）以FIFO（先进先出）方式对元素进行排序，除了优先级队列之外，优先级队列根据提供的比较器或元素的自然顺序对元素进行排序。无论使用什么顺序，队列的头部是通过调用删除或轮询删除的元素。在FIFO队列中，所有新元素都插入队列的尾部。其他类型的队列可能使用不同的放置规则。每个`Queue`实现都必须指定其排序属性。另请参阅 [The Queue Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/queue.html) 部分。

- `Deque` — 用于在处理之前保存多个元素的集合。除了基本的 `Collection` 操作外，Deque还提供额外的插入，提取和检查操作。

  `Deques`可以用作FIFO（先进先出）和LIFO（后进先出）队列。在双端队列中，可以在两端插入，检索和删除所有新元素。另请参阅 [The Deque Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/deque.html) 接口部分。

- `Map` — 将键映射到值的对象。`Map` 不能包含重复的键，每个键最多可以映射一个值。如果您使用过`Hashtable`，那么您已经熟悉了`Map`的基础知识。另请参阅 [The Map Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/map.html) 部分。

最后两个核心集合接口只是`Set`和`Map`的排序版本：

- `SortedSet` — 一个按升序维护其元素的集合。提供了几个额外的操作用来排序。排序集用于自然排序的集合，例如单词列表和成员资格卷。另请参阅 [The SortedSet Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/sorted-set.html) 部分。
- `SortedMap` — 按键升序顺序维护映射的 `Map` 。这是`SortedSet`的`Map`模拟。排序映射用于自然排序的键/值对集合，例如字典和电话目录。另请参阅 [The SortedMap Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/sorted-map.html) 部分。

要了解排序接口如何维护其元素的顺序，请参阅 [Object Ordering](https://docs.oracle.com/javase/tutorial/collections/interfaces/order.html) 部分。

### Collection 接口

`Collection`表示一组称为其元素的对象。`Collection`接口用于传递需要最大通用性的对象集合。例如，按照惯例，所有通用集合实现都有一个带有`Collection`参数的构造函数。此构造函数（称为*转换构造函数*）初始化新集合以包含指定集合中的所有元素，无论给定集合的子接口或实现类型如何。换句话说，它允许您转换集合的类型。

例如，假设您有一个`Collection<String> c`，它可以是`List`，`Set`或其他类型的`Collection`。这个习惯用法创建一个新的`ArrayList`（`List`接口的一个实现），初始包含`c`中的所有元素。

```java
List<String> list = new ArrayList<String>(c);
```

或者 - 如果您使用的是JDK 7或更高版本 - 您可以使用菱形运算符：

```java
List<String> list = new ArrayList<>(c);
```

`Collection`接口包含执行基本操作的方法，例如`int size()`，`boolean isEmpty()`，`boolean contains(Object element)`，`boolean add(E element)`，`boolean remove(Object element)`和`Iterator <E> iterator()`。

它还包含对整个集合进行操作的方法，例如`boolean containsAll(Collection <?> c)`，`boolean addAll(Collection <? extends E> c)`，`boolean removeAll(Collection <?> c)`，`boolean retainAll(Collection <?> c)`，和`void clear()`。

还存在用于数组操作的附加方法（诸如`Object [] toArray()`和`<T> T [] toArray(T [] a)`。

在JDK 8及更高版本中，`Collection`接口还公开方法`Stream <E> stream()`和`Stream <E> parallelStream()`，以从底层集合中获取顺序或并行流。（有关使用流的更多信息，请参阅标题为 [聚合操作](https://docs.oracle.com/javase/tutorial/collections/streams/index.html) 的课程。）

如果给定`Collection`表示一组对象，`Collection`接口会执行您期望的操作。它有方法告诉你集合中有多少元素（`size`，`isEmpty`），检查给定对象是否在集合中的方法（`contains`），从集合中添加和删除元素的方法（`add`, `remove`）， 和在集合（`iterator`）上提供迭代器的方法。

`add`方法通常定义得足够通用，因此对于允许重复的集合以及不重复的集合都有意义。它保证`Collection`在调用完成后将包含指定的元素，并且如果`Collection`因调用而更改，则返回`true`。类似地，`remove`方法旨在从`Collection`中删除指定元素的单个实例，假设它包含给定的元素，并且如果`Collection`被修改则返回`true`。

**遍历集合**

有三种遍历集合的方法：（1）使用聚合操作；（2）和for-each构造；（3）使用迭代器。

**聚合操作**

在JDK 8及更高版本中，迭代集合的首选方法是获取流并对其执行聚合操作。聚合操作通常与lambda表达式结合使用，以使用较少的代码行使编程更具表现力。以下代码按顺序遍历一组形状并打印出红色对象：

```java
myShapesCollection.stream()
.filter(e -> e.getColor() == Color.RED)
.forEach(e -> System.out.println(e.getName()));
```

同样，您可以轻松地请求并行流，如果集合足够大并且您的计算机具有足够的核心，这可能是有意义的：

```java
myShapesCollection.parallelStream()
.filter(e -> e.getColor() == Color.RED)
.forEach(e -> System.out.println(e.getName()));
```

使用此API收集数据的方法有很多种。例如，您可能希望将`Collection`的元素转换为`String`对象，然后将它们连接起来，用逗号分隔：

```java
    String joined = elements.stream()
    .map(Object::toString)
    .collect(Collectors.joining(", "));
```

或者总计一下所有员工的工资：

```java
int total = employees.stream()
.collect(Collectors.summingInt(Employee::getSalary)));
```

这些只是您可以使用流和聚合操作执行的一些示例。有关更多信息和示例，请参阅标题为 [Aggregate Operations](https://docs.oracle.com/javase/tutorial/collections/streams/index.html) 的课程。

`Collections`框架一直提供许多所谓的“批量操作”作为其API的一部分。这些方法包括对整个集合进行操作的方法，例如`containsAll`，`addAll`，`removeAll`等。不要将这些方法与JDK 8中引入的聚合操作混淆。新聚合操作与现有批量操作之间的主要区别（`containsAll`，`addAll`等）是旧版本都是*mutative*的，这意味着它们都修改了底层集合。相反，新的聚合操作不会修改基础集合。使用新的聚合操作和lambda表达式时，必须注意避免修改集合，以免将来引入问题，如果您的代码稍后从并行流运行。

**for-each 结构**

`for-each`构造允许您使用`for`循环简明地遍历集合或数组 - 请参阅 [The for Statement](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/for.html) 。 以下代码使用`for-each`构造在单独的行上打印出集合的每个元素。

```java
for (Object o : collection)
    System.out.println(o);
```

**迭代器**

如果需要，`Iterator`是一个对象，使您可以遍历集合并有选择地从集合中删除元素。通过调用`iterator`方法获得集合的`Iterator`。以下是`Iterator`接口。

```java
public interface Iterator<E> {
    boolean hasNext();
    E next();
    void remove(); //optional
}
```

如果迭代具有更多元素，则`hasNext`方法返回`true`，并且 `next` 方法返回迭代中的下一个元素。`remove`方法从基础`Collection`中删除`next`返回的最后一个元素。每次调用next时，只能调用一次`remove`方法，如果违反此规则，则抛出异常。

请注意，`Iterator.remove`是在迭代期间修改集合的唯一安全方法；如果在迭代进行过程中以任何其他方式修改基础集合，则程序行为结果未指定。

当需要进行如下操作时，使用`Iterator`而不是`for-each`构造：

- 删除当前元素。`for-each`构造隐藏了迭代器，因此您无法调用`remove`。因此，`for-each`构造不可用于过滤。
- 并行迭代多个集合。

以下方法说明如何使用`Iterator`过滤任意`Collection`  - 即遍历删除特定元素的集合。

```java
static void filter(Collection<?> c) {
    for (Iterator<?> it = c.iterator(); it.hasNext(); )
        if (!cond(it.next()))
            it.remove();
}
```

这段简单的代码是多态的，这意味着它适用于任何`Collection`，无论何种集合具体实现。此示例演示了使用Java Collections Framework编写多态算法是多么容易。

**集合接口批量操作**

批量操作对整个集合执行操作。您可以使用基本操作实现这些批量操作，但在大多数情况下，此类实现效率较低。以下是批量操作：

 -  `containsAll` - 如果目标`Collection`包含指定`Collection`中的所有元素，则返回`true`。
 -  `addAll` - 将指定`Collection`中的所有元素添加到目标`Collection`中。
 -  `removeAll` - 从目标`Collection`中删除也包含在指定`Collection`中的所有元素。
 -  `retainAll` - 从目标`Collection`中删除所有未包含在指定`Collection`中的元素。也就是说，它仅保留目标`Collection`中也包含在指定`Collection`中的那些元素。
 -  `clear` - 从`Collection`中删除所有元素。

如果在执行操作的过程中修改了目标`Collection`，则`addAll`，`removeAll`和`retainAll`方法都返回`true`。

作为批量操作功能的一个简单示例，请考虑以下习惯用法，下面例子从`Collection` `c`中删除指定元素的所有实例`e`。

```java
c.removeAll(Collections.singleton(e));
```

更具体地说，假设您要从`Collection`中删除所有`null`元素。

```java
c.removeAll(Collections.singleton(null));
```

这个习惯用法使用`Collections.singleton`，这是一个静态工厂方法，它返回一个只包含指定元素的不可变`Set`。

**集合接口数组操作**

`toArray`方法是作为集合和旧API之间的桥梁提供的，这些API期望输入是数组。数组操作允许将`Collection`的内容转换为数组。没有参数的简单形式创建一个新的`Object`数组。更复杂的形式允许调用者提供数组或选择输出数组的运行时类型。

例如，假设`c`是`Collection`。以下代码段将`c`的内容转储到新分配的`Object`数组中，该数组的长度与`c`中的元素数相同。

```java
Object[] a = c.toArray();
```

假设已知`c`只包含字符串（可能因为`c`的类型为`Collection<String>`）。以下代码段将`c`的内容转储到新分配的`String`数组中，该数组的长度与`c`中的元素数相同。

```java
String[] a = c.toArray(new String[0]);
```

