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

### Set 接口

[`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html) 是一个不能包含重复元素的 [`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html) 。它模拟了数学集抽象。`Set`接口仅包含从`Collection`继承的方法，并添加禁止重复元素的限制。`Set`还为`equals`和`hashCode`操作的行为添加了一个更强的契约，允许`Set`实例有意义地进行比较，即使它们的实现类型不同。如果两个`Set`实例包含相同的元素，则它们是相等的。

Java平台包含三个通用的`Set`实现：`HashSet`，`TreeSet`和`LinkedHashSet`。将其元素存储在哈希表中的 [`HashSet`](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html) 是性能最佳的实现，但它不能保证迭代的顺序。[`TreeSet`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html) 将其元素存储在红黑树中，根据其值对其元素进行排序，它比`HashSet`慢得多。[`LinkedHashSet`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashSet.html) 实现为一个哈希表，其中包含一个链表，它根据它们插入集合（插入顺序）的顺序对其元素进行排序。`LinkedHashSet`将客户端从`HashSet`提供的未指定的，通常是混乱的排序中拯救出来，其成本仅略高。

这是一个简单但有用的`Set`习语。假设您有一个`Collection`，`c`，并且您想要创建另一个包含相同元素的`Collection`，但需要删除所有重复项。下面的一行代码就可以做到了。

```java
Collection<Type> noDups = new HashSet<Type>(c);
```

它的工作原理是创建一个`Set`（根据定义，它不能包含重复项），初始包含`c`中的所有元素。它使用 [The Collection Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/collection.html) 部分中描述的标准转换构造函数。

或者，如果使用JDK 8或更高版本，您可以使用聚合操作轻松收集到`Set`：

```java
c.stream()
.collect(Collectors.toSet()); // no duplicates
```

这是一个稍长的示例，它将名称集合内容聚集到`TreeSet`中：

```java
Set<String> set = people.stream()
.map(Person::getName)
.collect(Collectors.toCollection(TreeSet::new));
```

以下是第一个习语的次要变体，它在删除重复元素时保留了原始集合的顺序：

```java
Collection<Type> noDups = new LinkedHashSet<Type>(c);
```

以下是封装前面的习惯用法的泛型方法，返回与传入参数相同的泛型类型的`Set`。

```java
public static <E> Set<E> removeDups(Collection<E> c) {
    return new LinkedHashSet<E>(c);
}
```

**Set 接口基本操作**

`size`操作返回`Set`中的元素数（其*基数*）。`isEmpty`方法完全符合您的想法。`add`方法将指定的元素添加到`Set`（如果它尚不存在与集合中）并返回一个布尔值，指示是否添加了元素。类似地，`remove`方法从`Set`中删除指定的元素（如果存在）并返回一个布尔值，指示元素是否存在。 `iterator` 方法在`Set`上返回`Iterator`。

以下 [`program`](https://docs.oracle.com/javase/tutorial/collections/interfaces/examples/FindDups.java) 打印出其参数列表中的所有不同单词。提供了该程序的两个版本。第一个使用JDK 8聚合操作。第二个使用`for-each`构造。

使用JDK 8聚合操作：

```java
import java.util.*;
import java.util.stream.*;

public class FindDups {
    public static void main(String[] args) {
        Set<String> distinctWords = Arrays.asList(args).stream()
		.collect(Collectors.toSet()); 
        System.out.println(distinctWords.size()+ 
                           " distinct words: " + 
                           distinctWords);
    }
}
```

使用 `for-each` 结构：

```java
import java.util.*;

public class FindDups {
    public static void main(String[] args) {
        Set<String> s = new HashSet<String>();
        for (String a : args)
               s.add(a);
               System.out.println(s.size() + " distinct words: " + s);
    }
}
```

运行随便一个版本：

```
java FindDups i came i saw i left
```

输出：

```
4 distinct words: [left, came, saw, i]
```

请注意，代码始终通过其接口类型（`Set`）而不是其实现类型引用`Collection`。这是一个强烈推荐的编程实践，因为它使您可以灵活地仅通过更改构造函数来更改实现。如果用于存储集合的变量或用于传递它的参数被声明为`Collection`的实现类型而不是其接口类型，则必须更改所有此类变量和参数以更改其实现类型。

此外，无法保证生成的程序能够正常运行。如果程序使用原始实现类型中存在但未在新实现类型中存在的任何非标准操作，则程序将失败。仅通过其接口引用集合可防止您使用任何非标准操作。

前面示例中`Set`的实现类型是`HashSet`，它不保证`Set`中元素的顺序。如果希望程序按字母顺序打印单词列表，只需将`Set`的实现类型从`HashSet`更改为`TreeSet`。进行这个简单的单行更改会导致前一个示例中的命令行生成以下输出。

```
java FindDups i came i saw i left

4 distinct words: [came, i, left, saw]
```

**Set 接口批量操作**

批量操作特别适合于`Set`；应用时，它们执行标准的集合代数运算。假设`s1`和`s2`是集合。以下是批量操作的作用：

- `s1.containsAll(s2)` — 如果`s2`是`s1`的子集则返回`true`。（`s1`包含`s2`的所有元素）
- `s1.addAll(s2)` — 将`s1`转化为`s1`和`s2`的并集。（两个集合的并集包含两个集合中的所有元素）
- `s1.retainAll(s2)` — 将`s1`转化为`s1`和`s2`的交集。（交集包含同时存在于两个集合中的元素）
- `s1.removeAll(s2)` — 将`s1`转化为`s1`和`s2`的（非对称）差集。（此差集包含存在于`s1`中而不存在于`s2`中的元素）

要非破坏性地计算两个集合的并集，交集或差集（不修改任何一个集合），调用者必须在调用适当的批量操作之前复制一个集合。以下是由此产生的习语。

```java
Set<Type> union = new HashSet<Type>(s1);
union.addAll(s2);

Set<Type> intersection = new HashSet<Type>(s1);
intersection.retainAll(s2);

Set<Type> difference = new HashSet<Type>(s1);
difference.removeAll(s2);
```

前面的习语中的结果集的实现类型是`HashSet`，正如已经提到的，它是Java平台中最好的全能`Set`实现。但是，任何通用的`Set`实现都可以替代。

让我们重温一下`FindDups`程序。假设您想知道参数列表中的哪些单词只出现一次，哪些出现多次，但您不希望重复打印任何重复项。这种效果可以通过生成两个集合来实现 - 一个集合包含参数列表中的每个单词，另一个集合仅包含重复项目。仅出现一次的单词是这两组的集合差异，我们知道如何计算这种差异。以下是生成的程序。

```java
import java.util.*;

public class FindDups2 {
    public static void main(String[] args) {
        Set<String> uniques = new HashSet<String>();
        Set<String> dups    = new HashSet<String>();

        for (String a : args)
            if (!uniques.add(a))
                dups.add(a);

        // Destructive set-difference
        uniques.removeAll(dups);

        System.out.println("Unique words:    " + uniques);
        System.out.println("Duplicate words: " + dups);
    }
}
```

当使用前面使用的相同参数列表运行时（`i came i saw i left`），程序产生以下输出。

```
Unique words:    [left, saw, came]
Duplicate words: [i]
```

不太常见的集合代数运算是*对称差集* - 存在于两个指定集合中某一个里，但不同时存在于两个集合中的元素集合。以下代码非破坏性地计算两组的对称差集。

```java
Set<Type> symmetricDiff = new HashSet<Type>(s1);
symmetricDiff.addAll(s2);
Set<Type> tmp = new HashSet<Type>(s1);
tmp.retainAll(s2);
symmetricDiff.removeAll(tmp);
```

**Set 接口数组操作**

除了对其他任何`Collection`执行的操作之外，数组操作不会对`Set`执行任何特殊操作。 [The Collection Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/collection.html) 部分介绍了这些操作。

### List 接口

 [`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html) 是一个有序的 [`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html) （有时称为序列）。列表可能包含重复元素。除了从`Collection`继承的操作之外，`List` 接口还包括以下操作：

- `Positional access` — 根据列表中的数字位置操纵元素。这包括`get`，`set`，`add`，`addAll`和`remove`等方法。
- `Search` — 搜索列表中的指定对象并返回其数字位置。搜索方法包括`indexOf`和`lastIndexOf`。
- `Iteration` — 扩展`Iterator`语义以利用列表的顺序性。`listIterator`方法提供此行为。
- `Range-view` —  `sublist` 方法对列表执行任意范围操作。

Java平台包含两个通用的`List`实现。[`ArrayList`](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html) ，通常是性能更好的实现，而 [`LinkedList`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html) 在某些情况下提供更好的性能。

**集合操作**

假设您已经熟悉它们，那么从`Collection`继承的操作都可以完成您期望它们做的事情。如果您不熟悉`Collection`，现在是阅读 [The Collection Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/collection.html) 部分的好时机。`remove`操作始终从列表中删除指定元素的第一个匹配项。`add`和`addAll`操作始终将新元素附加到列表的末尾。因此，以下习语将一个列表连接到另一个列表。

```java
list1.addAll(list2);
```

这是这个习语的非破坏性形式，它产生第三个`List`，其中包含附加到第一个列表的第二个列表。

```java
List<Type> list3 = new ArrayList<Type>(list1);
list3.addAll(list2);
```

请注意，成语以其非破坏性形式利用了`ArrayList`的标准转换构造函数。

这是一个将一些名称聚合到`List`中的示例（JDK 8及更高版本）：

```java
List<String> list = people.stream()
.map(Person::getName)
.collect(Collectors.toList());
```

与 [`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html) 接口一样，`List`增强了对`equals`和`hashCode`方法的要求，因此可以比较两个`List`对象的逻辑相等性，而不考虑它们的实现类。如果两个`List`对象包含相同顺序的相同元素，则它们是相等的。

**位置访问和搜索操作**

基本的位置访问操作是`get`，`set`，`add`和`remove`。（`set`和`remove`操作返回被覆盖或删除的旧值。）其他操作（`indexOf`和`lastIndexOf`）返回列表中指定元素的第一个或最后一个索引。

`addAll`操作从指定位置开始插入指定`Collection`的所有元素。元素按指定`Collection`的迭代器返回的顺序插入。此调用是`Collection`的`addAll`操作的位置访问模拟。

这是在`List`中交换两个索引位置元素的一个小方法。

```java
public static <E> void swap(List<E> a, int i, int j) {
    E tmp = a.get(i);
    a.set(i, a.get(j));
    a.set(j, tmp);
}
```

当然，这有一个很大的不同。这是一种多态算法：它在任何`List`中交换两个元素，而不管其实现类型如何。这是另一种使用前面 `swap` 方法的多态算法。

```java
public static void shuffle(List<?> list, Random rnd) {
    for (int i = list.size(); i > 1; i--)
        swap(list, i - 1, rnd.nextInt(i));
}
```

此算法包含在Java平台的 [`Collections`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html) 类中，使用指定的随机源随机置换指定的列表。这有点微妙：它从底部向上运行列表，反复地将随机选择的元素交换到当前位置。与大多数幼稚的洗牌尝试不同，这是公平的（假设一个无偏见的随机源，所有排列都有相同的可能性。）和快速的（需要 `list.size()-1` 次交换）。以下程序使用此算法以随机顺序打印其参数列表中的单词。

```java
import java.util.*;

public class Shuffle {
    public static void main(String[] args) {
        List<String> list = new ArrayList<String>();
        for (String a : args)
            list.add(a);
        Collections.shuffle(list, new Random());
        System.out.println(list);
    }
}
```

事实上，这个程序可以更短，更快。 [`Arrays`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html) 类有一个名为`asList`的静态工厂方法，它允许将数组视为`List`。此方法不会复制数组。列表中的更改会写入数组，反之亦然。生成的`List`不是通用的`List`实现，因为它没有实现（可选） `add` 和 `remove` 操作：数组不可调整大小。利用`Arrays.asList`并调用`shuffle`的库版本（使用默认的随机源），您将得到以下小程序，其行为与前一个程序相同。

```java
import java.util.*;

public class Shuffle {
    public static void main(String[] args) {
        List<String> list = Arrays.asList(args);
        Collections.shuffle(list);
        System.out.println(list);
    }
}
```

**迭代器**

正如您所期望的那样，`List`的迭代器操作返回的`iterator` 以适当的顺序返回列表的元素。`List`还提供了一个更强大的迭代器，称为`ListIterator`，它允许您在任一方向遍历列表，在迭代期间修改列表，并获取迭代器的当前位置。

`ListIterator`从`Iterator`继承的三个方法（`hasNext`，`next`和`remove`）在两个接口中完全相同。`hasPrevious`和 `previous` 的操作和`hasNext`和`next`的精确类似。前一个操作引用（隐式）游标之前的元素，而后者引用游标之后的元素。上一个操作向后移动游标，然后向下移动游标。

这是在列表中向后迭代的标准习惯用法。

```java
for (ListIterator<Type> it = list.listIterator(list.size()); it.hasPrevious(); ) {
    Type t = it.previous();
    ...
}
```

请注意前面的习语中`listIterator`的参数。`List`接口有两种形式的`listIterator`方法。没有参数的形式返回位于列表开头的`ListIterator`；带有`int`参数的形式返回一个位于指定索引处的`ListIterator`。索引引用初始调用`next`返回的元素。对`previous`的初始调用将返回索引为`index-1`的元素。在长度为`n`的列表中，索引有`n+1`个有效值，从`0`到`n`，包括`0`和`n`。

直观地说，游标总是在两个元素之间 - 一个将通过调用`previous`返回的元素和一个将通过调用`next`返回的元素。`n+1`个有效索引值对应于元素之间的`n+1`个间隙，从第一个元素之前的间隙到最后一个元素之后的间隙。下图显示了包含四个元素的列表中的五个可能的光标位置。

![Five arrows representing five cursor positions, from 0 to 4, with four elements, one between each arrow.](https://docs.oracle.com/javase/tutorial/figures/collections/colls-fivePossibleCursor.gif)

5个可能的游标位置。

对 `next` 和 `previous` 的调用可以混合，但你必须要小心。对`previous`的第一次调用返回与上一次调用`next`相同的元素。类似地，在对`previous`的一系列调用之后对`next`的第一次调用返回与最后一次`previous`调用相同的元素。

`nextIndex`方法返回后续调用`next`返回的元素的索引并不奇怪，而`previousIndex`返回后续调用`previous`返回的元素的索引。这些调用通常用于报告找到某些内容的位置或记录`ListIterator`的位置，以便可以创建具有相同位置的另一个`ListIterator`。

同样也不足为奇的是，`nextIndex`返回的数字总是大于`previousIndex`返回的数字。这意味着两种边界情况的行为：（1）当光标在初始元素返回`-1`之前调用`previousIndex`，以及（2）当光标在`final`元素之后返回`list.size()`时调用`nextIndex`。 为了使所有这些具体化，以下是`List.indexOf`的可能实现。

```java
public int indexOf(E e) {
    for (ListIterator<E> it = listIterator(); it.hasNext(); )
        if (e == null ? it.next() == null : e.equals(it.next()))
            return it.previousIndex();
    // Element not found
    return -1;
}
```

请注意，`indexOf`方法返回`it.previousIndex()`，即使它正在向前遍历列表。原因是`it.nextIndex()`将返回我们要检查的元素的索引，并且我们想要返回刚检查的元素的索引。

`Iterator`接口提供`remove`操作以从`Collection`中删除`next`返回的最后一个元素。对于`ListIterator`，此操作将删除`next`或`previous`返回的最后一个元素。`ListIterator`接口提供了两个额外的操作来修改列表 - `set` 和 `add`。`set`方法用指定的元素覆盖`next`或`previous`返回的最后一个元素。以下多态算法使用`set`将一个指定值的所有出现替换为另一个。

```java
public static <E> void replace(List<E> list, E val, E newVal) {
    for (ListIterator<E> it = list.listIterator(); it.hasNext(); )
        if (val == null ? it.next() == null : val.equals(it.next()))
            it.set(newVal);
}
```

在这个例子中唯一棘手的是`val`和`it.next`之间的相等性测试。您需要当心特殊情况下`val`值为`null`以防止`NullPointerException`。

`add`方法在当前光标位置之前立即将新元素插入到列表中。此方法在以下多态算法中说明，以使用指定列表中包含的值序列替换指定值的所有出现。

```java
public static <E> 
    void replace(List<E> list, E val, List<? extends E> newVals) {
    for (ListIterator<E> it = list.listIterator(); it.hasNext(); ){
        if (val == null ? it.next() == null : val.equals(it.next())) {
            it.remove();
            for (E e : newVals)
                it.add(e);
        }
    }
}
```

**范围视图操作**

范围视图操作`subList(int fromIndex, int toIndex)`返回此列表部分的`List`视图，其索引范围从`fromIndex`（包括）到`toIndex`（不包括）。这个半开放范围反映了典型的`for`循环。

```java
for (int i = fromIndex; i < toIndex; i++) {
    ...
}
```

正如术语*视图*所暗示的那样，返回的`List`由调用了`subList`的`List`进行备份，因此前者中的更改将反映在后者中。

此方法消除了对显式范围操作（对于数组通常存在的排序）的需要。任何期望`List`的操作都可以通过传递`subList`视图而不是整个`List`来用作范围操作。例如，以下习语从`List`中删除了一系列元素。

```java
list.subList(fromIndex, toIndex).clear();
```

可以构造类似的习语以搜索范围中的元素。

```java
int i = list.subList(fromIndex, toIndex).indexOf(o);
int j = list.subList(fromIndex, toIndex).lastIndexOf(o);
```

请注意，前面的惯用法返回`subList`中找到的元素的索引，而不是后备列表中的索引。

在`List`上操作的任何多态算法（例如`replace`和`shuffle`示例）都与`subList`返回的`List`一起使用。

这是一个多态算法，其实现使用`subList`来处理来自牌组的牌。也就是说，它返回一个新的`List`（“hand”），它包含从指定`List`（“deck”）末尾获取的指定数量的元素。手中返回的元素将从卡座中移除。

```java
public static <E> List<E> dealHand(List<E> deck, int n) {
    int deckSize = deck.size();
    List<E> handView = deck.subList(deckSize - n, deckSize);
    List<E> hand = new ArrayList<E>(handView);
    handView.clear();
    return hand;
}
```

请注意，此算法将牌从牌组末端移开。对于许多常见的`List`实现，例如`ArrayList`，从列表末尾删除元素的性能明显优于从头开始删除元素的性能。

以下是[`a program`](https://docs.oracle.com/javase/tutorial/collections/interfaces/examples/Deal.java) ，它使用`dealHand`方法与`Collections.shuffle`结合，从正常的52张牌组生成牌局。该程序采用两个命令行参数：（1）交易手数和（2）每手牌数。

```java
import java.util.*;

public class Deal {
    public static void main(String[] args) {
        if (args.length < 2) {
            System.out.println("Usage: Deal hands cards");
            return;
        }
        int numHands = Integer.parseInt(args[0]);
        int cardsPerHand = Integer.parseInt(args[1]);
    
        // Make a normal 52-card deck.
        String[] suit = new String[] {
            "spades", "hearts", 
            "diamonds", "clubs" 
        };
        String[] rank = new String[] {
            "ace", "2", "3", "4",
            "5", "6", "7", "8", "9", "10", 
            "jack", "queen", "king" 
        };

        List<String> deck = new ArrayList<String>();
        for (int i = 0; i < suit.length; i++)
            for (int j = 0; j < rank.length; j++)
                deck.add(rank[j] + " of " + suit[i]);
    
        // Shuffle the deck.
        Collections.shuffle(deck);
    
        if (numHands * cardsPerHand > deck.size()) {
            System.out.println("Not enough cards.");
            return;
        }
    
        for (int i = 0; i < numHands; i++)
            System.out.println(dealHand(deck, cardsPerHand));
    }
  
    public static <E> List<E> dealHand(List<E> deck, int n) {
        int deckSize = deck.size();
        List<E> handView = deck.subList(deckSize - n, deckSize);
        List<E> hand = new ArrayList<E>(handView);
        handView.clear();
        return hand;
    }
}
```

运行程序会产生如下输出。

```
% java Deal 4 5

[8 of hearts, jack of spades, 3 of spades, 4 of spades,
    king of diamonds]
[4 of diamonds, ace of clubs, 6 of clubs, jack of hearts,
    queen of hearts]
[7 of spades, 5 of spades, 2 of diamonds, queen of diamonds,
    9 of clubs]
[8 of spades, 6 of diamonds, ace of spades, 3 of hearts,
    ace of hearts]
```

尽管`subList`操作非常强大，但在使用它时必须小心。如果通过返回的`List`之外的任何方式将元素添加到后备`List`或从后备`List`中删除元素，则`subList`返回的`List`的语义将变为未定义。因此，强烈建议您仅仅使用`subList`返回的`List`作为临时对象 - 在后备列表上执行一个或一系列范围操作。使用`subList`实例的时间越长，通过直接修改后备`List`或通过另一个`subList`对象来破坏它的可能性就越大。请注意，修改子列表的子列表并继续使用原始子列表（尽管不是并发）是合法的。

**List 算法**

Most polymorphic algorithms in the `Collections` class apply specifically to `List`. Having all these algorithms at your disposal makes it very easy to manipulate lists. Here's a summary of these algorithms, which are described in more detail in the [Algorithms](https://docs.oracle.com/javase/tutorial/collections/algorithms/index.html) section.

- `sort` — 使用合并排序算法对`List`进行排序，该算法提供快速，稳定的排序。（稳定的排序是不重新排序相同元素的排序。）
- `shuffle` — 随机置换`List`中的元素。
- `reverse` — 反转`List`中元素的顺序。
- `rotate` — 将`List`中的所有元素旋转指定的距离。
- `swap` — 将元素交换到`List`中的指定位置。
- `replaceAll` — 将所有出现的一个指定值替换为另一个。
- `fill` — 用指定的值覆盖`List`中的每个元素。
- `copy` — 将源列表复制到目标列表中。
- `binarySearch` — 使用二进制搜索算法搜索有序列表中的元素。
- `indexOfSubList` — 返回一个`List`的第一个等于另一个子列表的子列表索引。
- `lastIndexOfSubList` — 返回一个`List`的最后一个等于另一个子列表的子列表索引。

### Queue 接口

 [`Queue`](https://docs.oracle.com/javase/8/docs/api/java/util/Queue.html) 是在处理之前保存元素的集合。除了基本的`Collection`操作外，队列还提供额外的插入，删除和检查操作。 `Queue`接口如下。

```java
public interface Queue<E> extends Collection<E> {
    E element();
    boolean offer(E e);
    E peek();
    E poll();
    E remove();
}
```

每个`Queue`方法以两种形式存在：（1）如果操作失败，则抛出异常;（2）如果操作失败，则返回特殊值（`null`或`false`，具体取决于操作）。接口的常规结构如下表所示。

| Type of Operation | Throws exception | Returns special value |
| ----------------- | ---------------- | --------------------- |
| Insert            | `add(e)`         | `offer(e)`            |
| Remove            | `remove()`       | `poll()`              |
| Examine           | `element()`      | `peek()`              |

队列通常（但不一定）以FIFO（先进先出）方式对元素进行排序。优先级队列除外，它们根据元素的值对元素进行排序 - 有关详细信息，请参阅 [Object Ordering](https://docs.oracle.com/javase/tutorial/collections/interfaces/order.html) 部分。无论使用什么排序，队列的头部都是通过调用 `remove` 或 `poll` 删除的元素。在FIFO队列中，所有新元素都插入队列的尾部。其他类型的队列可能使用不同的放置规则。每个`Queue`实现都必须指定其排序属性。

`Queue`实现可以限制它拥有的元素数量：这样的队列被称为有界队列。`java.util.concurrent`中的某些`Queue`实现是有界的，但`java.util`中的实现不是。

`Queue`从`Collection`继承的`add`方法插入一个元素，除非它违反了队列的容量限制，在这种情况下它会抛出`IllegalStateException`。`offer`方法仅用于有界队列，与`add`的不同之处仅在于它通过返回false来表示无法插入元素。

`remove`和`poll`方法都删除并返回队列的头部元素。确切地删除哪个元素是队列的排序策略的功能。仅当队列为空时，`remove`和`poll`方法的行为才有所不同。在这些情况下，`remove` 抛出`NoSuchElementException`，而`poll`返回`null`。

 `element` 和`peek`方法返回但不删除队列的头部元素。它们以与`remove`和`poll`完全相同的方式彼此不同：如果队列为空，则 `element` 抛出`NoSuchElementException`，而`peek`返回`null`。

`Queue` 实现通常不允许插入`null`元素。为实现`Queue`而进行了改进的`LinkedList`实现是一个例外。由于历史原因，它允许`null`元素，但是你应该避免利用它，因为`null`被`poll`和`peek`方法用作特殊的返回值。

队列实现通常不定义`equals`和`hashCode`方法的基于元素的版本，而是从Object继承基于`id`的版本。

Queue接口不定义阻塞队列方法，这在并发编程中很常见。这些等待元素出现或空间可用的方法在 [`java.util.concurrent.BlockingQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/BlockingQueue.html) 接口中定义，该接口扩展了`Queue`。

在以下示例程序中，队列用于实现倒数计时器。队列预先加载了从命令行上指定的数字到0的所有索引位置上的整数值，按降序排列。然后，从队列中删除值并以一秒的间隔打印。该程序是刻意而为的，因为在不使用队列的情况下执行相同的操作会更自然，但它说明了在后续处理之前使用队列来存储元素。

```java
import java.util.*;

public class Countdown {
    public static void main(String[] args) throws InterruptedException {
        int time = Integer.parseInt(args[0]);
        Queue<Integer> queue = new LinkedList<Integer>();

        for (int i = time; i >= 0; i--)
            queue.add(i);

        while (!queue.isEmpty()) {
            System.out.println(queue.remove());
            Thread.sleep(1000);
        }
    }
}
```

在以下示例中，优先级队列用于对元素集合进行排序。同样，这个程序是刻意而为的，因为没有理由使用它来支持`Collections`中提供的 `sort` 方法，但它说明了优先级队列的行为。

```java
static <E> List<E> heapSort(Collection<E> c) {
    Queue<E> queue = new PriorityQueue<E>(c);
    List<E> result = new ArrayList<E>();

    while (!queue.isEmpty())
        result.add(queue.remove());

    return result;
}
```

### Deque 接口

deque是双端队列，通常发音为deck。双端队列是元素的线性集合，支持在两个端点处插入和移除元素。`Deque`接口是比`Stack`和`Queue`更强大的抽象数据类型，因为它同时实现堆栈和队列。[`Deque`](https://docs.oracle.com/javase/8/docs/api/java/util/Deque.html) 接口定义了访问`Deque`实例两端元素的方法。提供了插入，移除和检查元素的方法。预定义的类（如[`ArrayDeque`](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayDeque.html) 和 [`LinkedList`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html) ）实现了`Deque`接口。

请注意，`Deque`接口既可以用作后进先出堆栈，也可以用作先进先出队列。`Deque`接口中给出的方法分为三个部分：

**Insert**

`addfirst`和`offerFirst`方法在`Deque`实例的开头插入元素。方法`addLast`和`offerLast`插入元素在`Deque`实例的末尾。当`Deque`实例的容量受到限制时，首选方法是`offerFirst`和`offerLast`，因为如果`Deque`实例已满，则`addFirst`可能无法插入元素而抛出异常。

**Remove**

`removeFirst`和`pollFirst`方法从`Deque`实例的开头删除元素。`removeLast`和`pollLast`方法从末尾删除元素。如果`Deque`为空，则方法`pollFirst`和`pollLast`返回`null`，而如果`Deque`实例为空，则方法`removeFirst`和`removeLast`会抛出异常。

**Retrieve**

方法`getFirst`和`peekFirst`检索`Deque`实例的第一个元素。这些方法不会从`Deque`实例中删除该值。同样，方法`getLast`和`peekLast`检索最后一个元素。如果`deque`实例为空，则方法`getFirst`和`getLast`会抛出异常，而方法`peekFirst`和`peekLast`将返回`null`。

插入，删除和检索`Deque`元素的12种方法总结在下表中：

| Type of Operation | First Element (Beginning of the `Deque` instance) | Last Element (End of the `Deque` instance) |
| ----------------- | ---------------------------------------- | ---------------------------------------- |
| **Insert**        | `addFirst(e)``offerFirst(e)`             | `addLast(e)``offerLast(e)`               |
| **Remove**        | `removeFirst()``pollFirst()`             | `removeLast()``pollLast()`               |
| **Examine**       | `getFirst()``peekFirst()`                | `getLast()``peekLast()`                  |

除了插入，删除和检查`Deque`实例的这些基本方法之外，`Deque`接口还有一些预定义的方法。其中之一是`removeFirstOccurence`，如果指定元素存在于`Deque`实例中，则此方法将删除指定元素的第一次出现。如果该元素不存在，则`Deque`实例保持不变。 另一种类似的方法是`removeLastOccurence`；此方法删除`Deque`实例中指定元素的最后一次出现。这些方法的返回类型是`boolean`，如果元素存在于`Deque`实例中，它们将返回`true`。

