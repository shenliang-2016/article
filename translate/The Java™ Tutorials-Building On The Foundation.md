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

### Map 接口

`Map`是将键映射到值的对象。map不能包含重复键：每个键最多可映射一个值。它模拟数学*函数*抽象。`Map`接口包括基本操作的方法（如`put`，`get`，`remove`，`containsKey`，`containsValue`，`size`和`empty`），批量操作（如`putAll`和`clear`）和集合视图（如`keySet`，`entrySet`和`values`）。

Java平台包含三个通用的`Map`实现： [`HashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html), [`TreeMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html), 和 [`LinkedHashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashMap.html)。它们的行为和性能完全类似于`HashSet`，`TreeSet`和`LinkedHashSet`，如 [The Set Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/set.html) 部分所述。

本页的其余部分详细讨论了`Map`接口。但首先，这里有一些使用JDK 8聚合操作收集数据到`Map`的示例。对现实世界对象进行建模是面向对象编程中的常见任务，因此可以合理地认为某些程序可能会按部门对员工进行分组：

```java
// Group employees by department
Map<Department, List<Employee>> byDept = employees.stream()
.collect(Collectors.groupingBy(Employee::getDepartment));
```

或者计算部门员工的薪资总额：

```java
// Compute sum of salaries by department
Map<Department, Integer> totalByDept = employees.stream()
.collect(Collectors.groupingBy(Employee::getDepartment,
Collectors.summingInt(Employee::getSalary)));
```

或者根据是否及格对学生进行分组：

```java
// Partition students into passing and failing
Map<Boolean, List<Student>> passingFailing = students.stream()
.collect(Collectors.partitioningBy(s -> s.getGrade()>= PASS_THRESHOLD)); 
```

你也可以按照城市对人进行分组：

```java
// Classify Person objects by city
Map<String, List<Person>> peopleByCity
         = personStream.collect(Collectors.groupingBy(Person::getCity));
```

或者甚至级联两个收集器按州和城市对人进行分类：

```java
// Cascade Collectors 
Map<String, Map<String, List<Person>>> peopleByStateAndCity
  = personStream.collect(Collectors.groupingBy(Person::getState,
  Collectors.groupingBy(Person::getCity)))
```

同样，这些只是如何使用新JDK 8 API的几个示例。有关lambda表达式和聚合操作的深入介绍，请参阅标题为 [Aggregate Operations](https://docs.oracle.com/javase/tutorial/collections/streams/index.html) 的课程。

**Map 接口基本操作**

`Map`的基本操作（`put`，`get`，`containsKey`，`containsValue`，`size`和`isEmpty`）与`Hashtable`中的对应操作完全相同。以下程序生成其参数列表中找到的单词的频率表。频率表将每个单词映射到它在参数列表中出现的次数。

```java
import java.util.*;

public class Freq {
    public static void main(String[] args) {
        Map<String, Integer> m = new HashMap<String, Integer>();

        // Initialize frequency table from command line
        for (String a : args) {
            Integer freq = m.get(a);
            m.put(a, (freq == null) ? 1 : freq + 1);
        }

        System.out.println(m.size() + " distinct words:");
        System.out.println(m);
    }
}
```

关于这个程序唯一棘手的问题是`put`语句的第二个参数。该参数是一个条件表达式，如果该单词之前从未见过，则将频率设置为1，如果已经找到过该单词，则将其设置为当前值+1。尝试使用以下命令运行此程序：

```
java Freq if it is to be it is up to me to delegate
```

输出：

```
8 distinct words:
{to=3, delegate=1, be=1, it=2, up=1, if=1, me=1, is=2}
```

假设您希望按字母顺序查看频率表，您所要做的就是将`Map`的实现类型从`HashMap`更改为`TreeMap`。进行这种四字符更改会导致程序从同一命令行生成以下输出。

```
8 distinct words:
{be=1, delegate=1, if=1, is=2, it=2, me=1, to=3, up=1}
```

类似地，您可以通过将`Map`的实现类型更改为`LinkedHashMap`，使程序按照单词首次出现在命令行上的顺序打印频率表。这样做会产生以下输出。

```
8 distinct words:
{if=1, it=2, is=2, to=3, be=1, up=1, me=1, delegate=1}
```

这种灵活性提供了基于接口的框架功能的有力说明。

与 [`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html)and [`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html) 接口一样，`Map`强化了对`equals`和`hashCode`方法的要求，因此可以比较两个`Map`对象的逻辑相等性，而不考虑它们的实现类型。如果两个`Map`实例表示相同的键值映射，则它们是相等的。

按照惯例，所有通用`Map`实现都提供构造函数，这些构造函数接受`Map`对象并初始化新`Map`以包含指定`Map`中的所有键值映射。这个标准的`Map`转换构造函数完全类似于标准的`Collection`构造函数：它允许调用者创建一个所需实现类型的`Map`，该`Map`最初包含另一个`Map`中的所有映射，而不管其他`Map`的实现类型。例如，假设您有一个名为`m`的`Map`。以下单行代码创建一个新的`HashMap`，最初包含与`m`相同的所有键值映射。

```java
Map<K, V> copy = new HashMap<K, V>(m);
```

**Map 接口批量操作**

 `clear` 操作完全按照您的想法执行：它从`Map`中删除所有映射。`putAll`操作是`Collection`接口的`addAll`操作的`Map`模拟。除了明显使用将一个`Map`转储到另一个`Map`之外，它还有第二个更微妙的用途。假设`Map`用于表示属性 - 值对的集合；`putAll`操作与`Map`转换构造函数结合使用，提供了一种使用默认值实现属性映射创建的简洁方法。以下是演示此技术的静态工厂方法。

```java
static <K, V> Map<K, V> newAttributeMap(Map<K, V>defaults, Map<K, V> overrides) {
    Map<K, V> result = new HashMap<K, V>(defaults);
    result.putAll(overrides);
    return result;
}
```

**集合视图**

`Collection`视图方法允许以这三种方式将`Map`视为`Collection`：

- `keySet` — `Map`中包含的键的`Set`。
- `values` — `Map`中包含的值`Collection`。此`Collection`不是`Set`，因为多个键可以映射到相同的值。
- `entrySet` — `Map`中包含的键值对`Set`。`Map`接口提供了一个名为`Map.Entry`的小型嵌套接口，该接口是此`Set`中元素的类型。

`Collection`视图提供迭代`Map`的唯一方法。此示例说明了使用`for-each`构造迭代`Map`中的键的标准习惯用法：

```java
for (KeyType key : m.keySet())
    System.out.println(key);
```

使用 `iterator`：

```java
// Filter a map based on some 
// property of its keys.
for (Iterator<Type> it = m.keySet().iterator(); it.hasNext(); )
    if (it.next().isBogus())
        it.remove();
```

迭代值的习语是类似的。以下是迭代键值对的习语。

```java
for (Map.Entry<KeyType, ValType> e : m.entrySet())
    System.out.println(e.getKey() + ": " + e.getValue());
```

起初，许多人担心这些习惯用法可能会很慢，因为每次调用`Collection`视图操作时`Map`都必须创建一个新的`Collection`实例。轻松休息：每次需要给定的`Collection`视图时，`Map`都没有理由不能总是返回相同的对象。这正是`java.util`中所有`Map`实现的功能。

使用所有三个`Collection`视图，调用`Iterator`的`remove`操作将从基础`Map`中删除关联的条目，假设基础`Map`支持从头删除删除。这由前面的过滤习语说明。

使用`entrySet`视图，还可以通过在迭代期间调用`Map.Entry`的`setValue`方法来更改与键关联的值（同样，假设`Map`支持从头修改元素）。请注意，这些是在迭代期间修改`Map`的唯一安全方法；如果在迭代进行过程中以任何其他方式修改基础`Map`，则行为未指定。

`Collection`视图支持以多种形式删除元素 -  `remove`，`removeAll`，`retainAll`和`clear`操作，以及`Iterator.remove`操作。（再次，假设基础`Map`支持元素删除。）

`Collection`视图在任何情况下都不支持元素添加。对于`keySet`和`values`视图没有任何意义，并且对于`entrySet`视图没有必要，因为基础`Map`的`put`和`putAll`方法提供相同的功能。

**集合视图相关棘手问题：Map 代数**

应用于 `Collection` 视图时，批量操作（`containsAll`，`removeAll`和`retainAll`）是令人惊讶的强大工具。对于初学者，假设您想知道一个`Map`是否是另一个`Map`的子`Map` - 也就是说，后者`Map`是否包含前者`Map`中的所有键值映射。以下习语可以解决这个问题。

```java
if (m1.entrySet().containsAll(m2.entrySet())) {
    ...
}
```

沿着类似的路线，假设您想知道两个`Map`对象是否包含的所有键的映射都相同。

```java
if (m1.keySet().equals(m2.keySet())) {
    ...
}
```

假设您有一个表示属性 - 值对集合的`Map`，以及两个表示必需属性和允许属性的 `Set`。（允许的属性包括必需的属性。）以下代码段确定属性映射是否符合这些约束，如果不符合则打印详细的错误消息。

```java
static <K, V> boolean validate(Map<K, V> attrMap, Set<K> requiredAttrs, Set<K>permittedAttrs) {
    boolean valid = true;
    Set<K> attrs = attrMap.keySet();

    if (! attrs.containsAll(requiredAttrs)) {
        Set<K> missing = new HashSet<K>(requiredAttrs);
        missing.removeAll(attrs);
        System.out.println("Missing attributes: " + missing);
        valid = false;
    }
    if (! permittedAttrs.containsAll(attrs)) {
        Set<K> illegal = new HashSet<K>(attrs);
        illegal.removeAll(permittedAttrs);
        System.out.println("Illegal attributes: " + illegal);
        valid = false;
    }
    return valid;
}
```

假设您想知道两个`Map`对象共有的所有键。

```java
Set<KeyType>commonKeys = new HashSet<KeyType>(m1.keySet());
commonKeys.retainAll(m2.keySet());
```

类似的习语可以为你提供两个`Map`的公共值。

到目前为止提出的所有习语都是非破坏性的; 也就是说，它们不会修改基础`Map`。假设您要删除一个`Map`与另一个`Map`共有的所有键值对。

```java
m1.entrySet().removeAll(m2.entrySet());
```

假设您要从一个`Map`中删除在另一个`Map`中具有映射的所有键。

```java
m1.keySet().removeAll(m2.keySet());
```

在同一批量操作中开始混合键和值时会发生什么？假设您有一个`Map`，`managers`，将公司中的每个员工映射到相应的经理。我们会故意模糊键和值对象的类型。没关系，因为它们是相同的。现在假设您想知道所有“个人贡献者”（或非管理者）是谁。以下代码段将准确告诉您您想要了解的内容。

```java
Set<Employee> individualContributors = new HashSet<Employee>(managers.keySet());
individualContributors.removeAll(managers.values());
```

假设您要解雇所有直接向某位经理Simon报告的员工。

```java
Employee simon = ... ;
managers.values().removeAll(Collections.singleton(simon));
```

请注意，这个习惯用法是使用`Collections.singleton`，这是一个静态工厂方法，它返回一个带有指定元素的不可变`Set`。

一旦你完成了这项工作，你可能会有一大堆员工，他们的经理不再为公司工作（如果任何西蒙的直接报告人就是经理本身）。以下代码将告诉您哪些员工拥有不再为公司工作的经理。

```java
Map<Employee, Employee> m = new HashMap<Employee, Employee>(managers);
m.values().removeAll(managers.keySet());
Set<Employee> slackers = m.keySet();
```

这个例子有点棘手。首先，它创建`Map`的临时副本，并从临时副本中删除其（manager）值是原始`Map`中的键的所有条目。请记住，原始`Map`为每个员工都有一个条目。因此，临时`Map`中的其余条目包括来自原始`Map`的所有条目，其（manager）值不再是雇员。因此，临时副本中的键恰好代表了我们正在寻找的员工。

还有很多习语，比如本节中包含的习语，但列出它们都是不切实际和乏味的。一旦掌握了它，在你需要的时候找出合适的方法并不困难。

**多值映射**

*multimap*就像`Map`，但它可以将每个键映射到多个值。Java Collections Framework不包含多重映射的接口，因为它们并应用并不是那么广泛。使用值为`List`实例的`Map`作为*multimap*是一件相当简单的事情。在下一个代码示例中演示了此技术，该示例读取每行包含一个单词（全部小写）的单词列表，并打印出符合大小标准的所有变位词组。变位词组是一堆单词，所有单词都包含完全相同的字母，但顺序不同。该程序在命令行上有两个参数：（1）字典文件的名称和（2）要打印的变位词组的最小大小。不打印包含少于指定最小值的单词组的变位词组。

找到变位词组有一个标准技巧：对于字典中的每个单词，按字母顺序排列单词中的字母（即将单词的字母重新排序为字母顺序）并将条目放入*multimap*，然后将字母顺序排列的单词映射到原始单词。例如，单词`bad`导致将`abd`条目映射为`bad`以将其放入multimap中。马上就能看出任何给定键映射形成变位词组的所有单词。迭代multimap中的键，打印出满足大小约束的每个变位词组是一件简单的事情。

下面得例子直接实现了这种技术：

```java
import java.util.*;
import java.io.*;

public class Anagrams {
    public static void main(String[] args) {
        int minGroupSize = Integer.parseInt(args[1]);

        // Read words from file and put into a simulated multimap
        Map<String, List<String>> m = new HashMap<String, List<String>>();

        try {
            Scanner s = new Scanner(new File(args[0]));
            while (s.hasNext()) {
                String word = s.next();
                String alpha = alphabetize(word);
                List<String> l = m.get(alpha);
                if (l == null)
                    m.put(alpha, l=new ArrayList<String>());
                l.add(word);
            }
        } catch (IOException e) {
            System.err.println(e);
            System.exit(1);
        }

        // Print all permutation groups above size threshold
        for (List<String> l : m.values())
            if (l.size() >= minGroupSize)
                System.out.println(l.size() + ": " + l);
    }

    private static String alphabetize(String s) {
        char[] a = s.toCharArray();
        Arrays.sort(a);
        return new String(a);
    }
}
```

在173,000字的字典文件上运行此程序，最小变位词组大小为8，会产生以下输出。

```
9: [estrin, inerts, insert, inters, niters, nitres, sinter,
     triens, trines]
8: [lapse, leaps, pales, peals, pleas, salep, sepal, spale]
8: [aspers, parses, passer, prases, repass, spares, sparse,
     spears]
10: [least, setal, slate, stale, steal, stela, taels, tales,
      teals, tesla]
8: [enters, nester, renest, rentes, resent, tenser, ternes,
     treens]
8: [arles, earls, lares, laser, lears, rales, reals, seral]
8: [earings, erasing, gainers, reagins, regains, reginas,
     searing, seringa]
8: [peris, piers, pries, prise, ripes, speir, spier, spire]
12: [apers, apres, asper, pares, parse, pears, prase, presa,
      rapes, reaps, spare, spear]
11: [alerts, alters, artels, estral, laster, ratels, salter,
      slater, staler, stelar, talers]
9: [capers, crapes, escarp, pacers, parsec, recaps, scrape,
     secpar, spacer]
9: [palest, palets, pastel, petals, plates, pleats, septal,
     staple, tepals]
9: [anestri, antsier, nastier, ratines, retains, retinas,
     retsina, stainer, stearin]
8: [ates, east, eats, etas, sate, seat, seta, teas]
8: [carets, cartes, caster, caters, crates, reacts, recast,
     traces]
```

许多这些词似乎有点假，但这不是程序的错；他们就在字典文件中。[`dictionary file`](https://docs.oracle.com/javase/tutorial/collections/interfaces/examples/dictionary.txt) 是我们使用的字典文件。它源自Public Domain ENABLE 基准参考词列表。

### 对象排序

`List` `l` 可以如下排序：

```
Collections.sort(l);
```

如果`List`包含`String`元素，它将按字母顺序排序。如果它由`Date`元素组成，它将按时间顺序排序。这是怎么发生的?`String`和`Date`都实现了`Comparable`接口。可比较的实现为类提供了自然的顺序，允许该类的对象自动排序。下表总结了一些实现`Comparable`的更重要的Java平台类。

| Class          | Natural Ordering                         |
| -------------- | ---------------------------------------- |
| `Byte`         | Signed numerical                         |
| `Character`    | Unsigned numerical                       |
| `Long`         | Signed numerical                         |
| `Integer`      | Signed numerical                         |
| `Short`        | Signed numerical                         |
| `Double`       | Signed numerical                         |
| `Float`        | Signed numerical                         |
| `BigInteger`   | Signed numerical                         |
| `BigDecimal`   | Signed numerical                         |
| `Boolean`      | `Boolean.FALSE < Boolean.TRUE`           |
| `File`         | System-dependent lexicographic on path name |
| `String`       | Lexicographic                            |
| `Date`         | Chronological                            |
| `CollationKey` | Locale-specific lexicographic            |

如果您尝试对列表进行排序，其中的元素未实现`Comparable`，`Collections.sort(list)`将抛出 [`ClassCastException`](https://docs.oracle.com/javase/8/docs/api/java/lang/ClassCastException.html) 。类似地，如果您尝试使用 `comparator`对其元素无法相互比较的列表进行排序，则`Collections.sort(list, comparator)`将抛出 `ClassCastException` 。可以相互比较的元素称为*mutually comparable*。虽然不同类型的元素可以相互比较，但这里列出的类别都不允许进行类间比较。

如果您只想对可比元素的列表进行排序或创建它们的已排序集合，那么您就真正需要了解`Comparable`接口。如果要实现自己的`Comparable`类型，下一部分将是您感兴趣的。

**编写你自己的可比较类型**

`Comparable` 接口包含下面的方法：

```java
public interface Comparable<T> {
    public int compareTo(T o);
}
```

`compareTo`方法将接收到的对象与指定对象进行比较，并返回负整数、0或正整数，具体取决于接收对象是否小于，等于或大于指定对象。如果无法将指定的对象与接收对象进行比较，则该方法将抛出`ClassCastException`。

下面的类实现了`Comparable`。

```java
import java.util.*;

public class Name implements Comparable<Name> {
    private final String firstName, lastName;

    public Name(String firstName, String lastName) {
        if (firstName == null || lastName == null)
            throw new NullPointerException();
        this.firstName = firstName;
        this.lastName = lastName;
    }

    public String firstName() { return firstName; }
    public String lastName()  { return lastName;  }

    public boolean equals(Object o) {
        if (!(o instanceof Name))
            return false;
        Name n = (Name) o;
        return n.firstName.equals(firstName) && n.lastName.equals(lastName);
    }

    public int hashCode() {
        return 31*firstName.hashCode() + lastName.hashCode();
    }

    public String toString() {
	return firstName + " " + lastName;
    }

    public int compareTo(Name n) {
        int lastCmp = lastName.compareTo(n.lastName);
        return (lastCmp != 0 ? lastCmp : firstName.compareTo(n.firstName));
    }
}
```

为了保持例子简短，这个类有点额外的局限性：它不支持中间名，它既需要名字也需要姓，并且不以任何方式国际化。尽管如此，它还是说明了以下要点：

 - `Name` 对象是*不可变的*。在所有其他条件相同的情况下，不可变类型是可行的方法，特别是对于将在`Set`中用作元素或在`Map`中用作键的对象。如果您在集合中修改元素或键，这些集合将会中断。
 - 构造函数检查其参数是否为`null`。这可以确保所有`Name`对象都格式正确，这样其他任何方法都不会抛出`NullPointerException`。
 - 重新定义了`hashCode`方法。这对于重新定义`equals`方法的任何类都是必不可少的。（相等对象必须具有相同的哈希码。）
 - 如果指定的对象为`null`或类型不合适，则`equals`方法返回`false`。`compareTo`方法在这些情况下抛出运行时异常。这些行为都是各方法的通用契约所要求的。
 - 重新定义了toString方法，因此它以人类可读的形式打印`Name`。这总是一个好主意，特别是对于要放入集合的对象。各种集合类型的`toString`方法依赖于其元素，键和值的`toString`方法。

由于本节是关于元素排序的，让我们再谈谈`Name`的`compareTo`方法。它实现了标准的名称排序算法，其中姓氏优先于名字，这正是您想要的自然顺序。如果自然顺序不自然，那将会非常令人困惑啊！

看看`compareTo`是如何实现的，因为它非常典型。首先，比较对象的最重要部分（在本例中为姓氏）。通常，您可以使用该部分类型的自然顺序。在这种情况下，该部分是一个 `String` ，自然（词典）排序正是所要求的。如果比较结果为零，表示相等，那么您就完成了：您只需返回结果。如果最重要的部分相同，则继续比较下一个最重要的部分。在这种情况下，只有两个部分 - 名字和姓氏。如果有更多的部分，你会以更明显的方式进行，比较部分，直到你发现两个不相等或你正在比较最不重要的部分，此时你将返回比较的结果。

下面这个例子只是为了表明一切都能如期工作，它建立一个名单列表并对它们进行排序。

```java
import java.util.*;

public class NameSort {
    public static void main(String[] args) {
        Name nameArray[] = {
            new Name("John", "Smith"),
            new Name("Karl", "Ng"),
            new Name("Jeff", "Smith"),
            new Name("Tom", "Rich")
        };

        List<Name> names = Arrays.asList(nameArray);
        Collections.sort(names);
        System.out.println(names);
    }
}
```

程序输出：

```
[Karl Ng, Tom Rich, Jeff Smith, John Smith]
```

`compareTo`方法的行为有四个限制，我们现在不会讨论它们，因为它们技术性很差，很无聊，最好留在API文档中。实现`Comparable`的所有类都遵守这些限制非常重要，因此如果您正在编写实现它的类，请阅读`Comparable`的文档。尝试对违反限制的对象列表进行排序是未定义的行为。从技术上讲，这些限制确保了自然顺序是实现它的类的对象的总顺序；这对于确保明确定义排序是必要的。

**Comparators**

如果您想按照自然顺序以外的顺序排序某些对象，该怎么办？或者，如果要对某些未实现`Comparable`的对象进行排序，该怎么办？要执行上述任一操作，您需要提供[`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html)  - 一个封装排序的对象。与`Comparable`接口一样，`Comparator`接口由单个方法组成。

```java
public interface Comparator<T> {
    int compare(T o1, T o2);
}
```

`compare`方法比较其两个参数，返回负整数，0或正整数，具体取决于第一个参数是小于，等于还是大于第二个参数。如果其中一个参数不是`Comparator`类型，则`compare`方法将抛出`ClassCastException`。

关于`Comparable`的大部分内容也适用于 `Comparator` 。编写`compare`方法与编写`compareTo`方法几乎完全相同，只是前者将两个对象作为参数传入。由于同样的原因， `compare` 方法必须遵守与`Comparable`的`compareTo`方法相同的四个技术限制 - `Comparator` 必须为它所比较的对象产生总顺序。

假设您有一个名为`Employee`的类，如下所示。

```java
public class Employee implements Comparable<Employee> {
    public Name name()     { ... }
    public int number()    { ... }
    public Date hireDate() { ... }
       ...
}
```

让我们假设`Employee`实例的自然顺序是员工姓名上的名称排序（如前面的例子中所定义）。不幸的是，老板要求按照资历顺序列出员工名单。这意味着我们必须做一些工作，但并不多。以下程序将生成所需的列表。

```java
import java.util.*;
public class EmpSort {
    static final Comparator<Employee> SENIORITY_ORDER = 
                                        new Comparator<Employee>() {
            public int compare(Employee e1, Employee e2) {
                return e2.hireDate().compareTo(e1.hireDate());
            }
    };

    // Employee database
    static final Collection<Employee> employees = ... ;

    public static void main(String[] args) {
        List<Employee> e = new ArrayList<Employee>(employees);
        Collections.sort(e, SENIORITY_ORDER);
        System.out.println(e);
    }
}
```

该程序中的 `Comparator` 相当简单。它依赖于应用于`hireDate`访问器方法返回的值的`Date`的自然顺序。请注意， `Comparator` 将其第二个参数雇用日期传递给第一个参数，而不是相反。原因是最近雇用的员工是最不高级的；按雇用日期顺序排序会使列表按反向资历顺序排列。人们有时用来实现这种效果的另一种技术是维持参数顺序但是将比较的结果取反。

```java
// Don't do this!!
return -r1.hireDate().compareTo(r2.hireDate());
```

你应该总是使用前一种技术来支持后者，因为后者不能保证始终工作。原因是`compareTo`方法如果其参数小于调用它的对象，则可返回任何负整数。有一个负整数在取反时仍然是负的，看起来很奇怪。

```
-Integer.MIN_VALUE == Integer.MIN_VALUE
```

前面程序中的`Comparator`适用于对`List`进行排序，但它确实有一个缺陷：它不能用于排序已排序的集合，例如`TreeSet`，因为它生成的顺序与`equals`不兼容。这意味着此`Comparator`会将`equals`方法判定为不相等的对象判定为相等。特别是，在同一天雇佣的任何两名员工将相同。当你对`List`进行排序时，这并不重要。但是当你使用 `Comparator` 来排序一个已排序的集合时，它是致命的。如果您使用此 `Comparator` 将在同一日期雇用的多名员工插入到`TreeSet`中，则只会将第一个员工添加到该集合中；第二个将被视为重复元素，将被忽略。

要解决此问题，只需调整`Comparator`，以便生成与`equals`兼容的排序。换句话说，调整它以便在使用`compare`时看到相同的元素是那些在使用`equals`进行比较时也被视为相等的元素。执行此操作的方法是执行两部分比较（对于 `Name`），其中第一部分是我们感兴趣的部分 - 在这种情况下，是雇用日期 - 第二部分是唯一标识对象的属性，显然是员工编号。这是 `Comparator` 的结果。

```java
static final Comparator<Employee> SENIORITY_ORDER = 
                                        new Comparator<Employee>() {
    public int compare(Employee e1, Employee e2) {
        int dateCmp = e2.hireDate().compareTo(e1.hireDate());
        if (dateCmp != 0)
            return dateCmp;

        return (e1.number() < e2.number() ? -1 :
               (e1.number() == e2.number() ? 0 : 1));
    }
};
```

最后一点说明：您可能想要用更简单的方法替换`Comparator`中的最终`return`语句：

```java
return e1.number() - e2.number();
```

除非你绝对确定没有人会有负数的员工编号，否则不要这样做！这个技巧一般不起作用，因为有符号整数类型不足以表示两个任意有符号整数的差异。如果`i`是一个大的正整数且`j`是一个大的负整数，`i-j`将溢出并返回一个负整数。由此产生的 `comparator` 违反了我们一直在讨论的四个技术限制之一（传递性）并产生可怕的，微妙的错误。这不是纯粹的理论问题，人们被它坑了。

### SortedSet 接口

 [`SortedSet`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html) 是一个 [`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html) ，它按升序维护其元素，根据元素的自然顺序或根据`SortedSet`创建时间提供的`Comparator`进行排序。除了常规的`Set`操作外，`SortedSet`接口还提供以下操作：

- `Range view` — 允许排序集合上的任意范围操作
- `Endpoints` — 返回排序集合的头部或者尾部元素
- `Comparator access` — 返回用于集合排序的 `Comparator`，如果存在的话

下面是 `SortedSet` 接口代码：

```java
public interface SortedSet<E> extends Set<E> {
    // Range-view
    SortedSet<E> subSet(E fromElement, E toElement);
    SortedSet<E> headSet(E toElement);
    SortedSet<E> tailSet(E fromElement);

    // Endpoints
    E first();
    E last();

    // Comparator access
    Comparator<? super E> comparator();
}
```

**集合操作**

 `SortedSet` 从`Set`继承而来的方法在有序集合上的行为与普通集合相同。除了两个例外：

- `iterator` 操作返回的 `Iterator` 按顺序遍历有序集。
- `toArray`返回的数组按顺序包含有序集合的元素。

虽然接口不保证它，但Java平台的`SortedSet`实现的`toString`方法按顺序返回包含有序集的所有元素的字符串。

**标准构造器**

按照惯例，所有通用`Collection`实现都提供了一个接受`Collection`类型参数的标准转换构造函数；`SortedSet`实现也不例外。在`TreeSet`中，此构造函数创建一个实例，根据其自然顺序对其元素进行排序。这可能是一个错误。最好动态检查以查看指定的集合是否是`SortedSet`实例，如果是，则根据相同的标准（比较器或自然排序）对新的`TreeSet`进行排序。因为`TreeSet`采用了它所采用的方法，所以它还提供了一个构造函数，它接受一个`SortedSet`并返回一个新的`TreeSet`，它包含根据相同标准排序的相同元素。请注意，它是参数的编译时类型，而不是其运行时类型，它确定调用这两个构造函数中的哪一个（以及是否保留排序条件）。

按照惯例，`SortedSet`实现还提供了一个构造函数，它接受`Comparator`并返回根据指定的`Comparator`排序的空集。如果将`null`传递给此构造函数，则返回一个集合，该集合根据其自然顺序对其元素进行排序。

**范围视图操作**

`range-view` 操作有点类似于`List`接口提供的操作，但有一个很大的区别。即使直接修改了后备排序集，排序集的范围视图仍然有效。这是可行的，因为有序集的范围视图的端点是元素空间中的绝对点，而不是后备集合中的特定元素，如列表的情况。排序集的范围视图实际上只是集合的任何部分位于元素空间的指定部分中的窗口。对范围视图的更改将写回到后备排序集，反之亦然。因此，与列表上的范围视图不同，可以在很长一段时间内对已排序的集使用范围视图。

排序集提供三种范围视图操作。第一个`subSet`采用两个端点，如`subList`。端点不是索引，而是对象，必须与有序集合中的元素相比较，使用`Set`的比较器或其元素的自然顺序，无论`Set`使用哪个自定义。与`subList`一样，范围是半开放的，包括其低端点但不包括高端点。

因此，下面的代码行告诉你 `"doorbell"` 和 `"pickle"`之间有多少单词，包括`"doorbell"`但不包括 `"pickle"`，包含在名为 `dictionary`的字符串 `SortedSet`中：

```java
int count = dictionary.subSet("doorbell", "pickle").size();
```

以类似的方式，以下代码删除以字母`f`开头的所有元素。

```java
dictionary.subSet("f", "g").clear();
```

类似的技巧可以用来打印一个表格，告诉你每个字母开头的单词有多少个。

```java
for (char ch = 'a'; ch <= 'z'; ) {
    String from = String.valueOf(ch++);
    String to = String.valueOf(ch);
    System.out.println(from + ": " + dictionary.subSet(from, to).size());
}
```

假设您要查看包含其两个端点的闭区间，而不是开区间。如果元素类型允许计算元素空间中给定值的后继，则只需请求从`lowEndpoint`到`successor(highEndpoint)`的`subSet`。虽然它并不明显，但`String`的自然排序中的字符串`s`的后继是`s +"\0"` - 也就是说，附加了`null`字符的`s`。

因此，下面的代码告诉你 `"doorbell"` 和 `"pickle"`之间有多少单词，包括 `"doorbell"` 和 `"pickle"`，都包含在字典中。

```java
count = dictionary.subSet("doorbell", "pickle\0").size();
```

可以使用类似的技术来查看不包含端点的开区间。从`lowEndpoint`到`highEndpoint`的开区间视图是从 `successor(lowEndpoint)` 到`highEndpoint`的半开半闭区间。使用以下内容计算 `"doorbell"` 和 `"pickle"`之间的单词数，不包括两者。

```java
count = dictionary.subSet("doorbell\0", "pickle").size();
```

`SortedSet`接口包含另外两个 `range-view` 操作--`headSet`和`tailSet`，两者都采用单个`Object`参数。前者返回后备`SortedSet`的初始部分的视图，以指定对象为上界，但不包括指定的对象。后者返回后备`SortedSet`的最后部分的视图，从指定的对象开始并持续到后备`SortedSet`的末尾。因此，以下代码允许您将字典视为两个不相交的 `volumes` （`a-m`和`n-z`）。

```java
SortedSet<String> volume1 = dictionary.headSet("n");
SortedSet<String> volume2 = dictionary.tailSet("n");
```

**端点操作**

`SortedSet`接口包含返回有序集合中第一个和最后一个元素的操作，不出意外地称为`first`和`last`。除了它们的明显用途之外，`last`方法还可以作为`SortedSet`接口的明显缺陷的变通解决方法。你想对`SortedSet`做的一件事就是进入`Set`的内部并向前或向后迭代。从内部向前迭代很容易：只需获得一个`tailSet`并迭代它。不幸的是，没有简单的方法可以向后迭代。

以下习语获得元素空间中小于指定对象`o`的第一个元素。

```java
Object predecessor = ss.headSet(o).last();
```

这是从排序集内部的一个点向后移动一个元素的好方法。它可以重复应用以向后迭代，但这是非常低效的，需要查找返回的每个元素。

**比较器访问器**

`SortedSet`接口包含一个名为`comparator`的访问器方法，它返回用于对集合进行排序的`Comparator`；如果集合根据其元素的自然顺序排序，则返回`null`。提供此方法以便可以将排序的集合复制到具有相同排序的新排序集合中。它由前面描述的`SortedSet`构造函数使用。

### SortedMap 接口

[`SortedMap`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html) 是一个 [`Map`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) ，它按升序维护其元素，根据键的自然顺序排序，或根据创建`SortedMap`时提供的`Comparator`进行排序。 [Object Ordering](https://docs.oracle.com/javase/tutorial/collections/interfaces/order.html) 部分讨论了自然排序和 `Comparator`。`SortedMap`接口提供了常规`Map`操作和以下操作：

- `Range view` — 在排序 map 上执行任意范围操作
- `Endpoints` — 返回排序 map 的第一个或者最后一个键
- `Comparator access` — 返回 map 排序使用的 `Comparator`，如果存在的话

下面的接口是 [`SortedSet`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html) 的 `Map` 模拟：

```java
public interface SortedMap<K, V> extends Map<K, V>{
    Comparator<? super K> comparator();
    SortedMap<K, V> subMap(K fromKey, K toKey);
    SortedMap<K, V> headMap(K toKey);
    SortedMap<K, V> tailMap(K fromKey);
    K firstKey();
    K lastKey();
}
```

**Map 操作**

`SortedMap`继承自`Map`的操作在有序映射和普通映射上的行为相同，但有两个例外：

 - `iterator` 操作在任何有序映射的`Collection`视图上返回的 `Iterator` 按顺序遍历集合。
 - `Collection`视图的`toArray`操作返回的数组按顺序包含键，值或映射元素。

虽然接口无法保证，但所有Java平台的`SortedMap`实现中的`Collection`视图的`toString`方法依次返回包含视图所有元素的字符串。

**标准构造器**

按照惯例，所有通用`Map`实现都提供了一个接受`Map`类型参数的标准转换构造函数；`SortedMap`实现也不例外。在`TreeMap`中，此构造函数创建一个实例，根据其键的自然顺序对其条目进行排序。这可能是一个错误。最好动态检查以查看指定的`Map`实例是否为`SortedMap`，如果是，则根据相同的标准（比较器或自然排序）对新map进行排序。因为`TreeMap`采用了它所采用的方法，所以它还提供了一个构造函数，它接受`SortedMap`并返回一个新的`TreeMap`，它包含与给定`SortedMap`相同的映射，并根据相同的标准进行排序。请注意，它是参数的编译时类型，而不是其运行时类型，它确定是否优先于普通的映射构造函数调用`SortedMap`构造函数。

按照惯例，`SortedMap`实现还提供了一个构造函数，它接受`Comparator`并返回根据指定的`Comparator`排序的空映射。如果将`null`传递给此构造函数，它将返回一个`Map`，该`Map`根据其键的自然顺序对其映射进行排序。

**与 SortedSet 比较**

因为此接口是`SortedSet`的精确`Map`模拟，所以 [The SortedSet Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/sorted-set.html) 部分中的所有习语和代码示例都适用于`SortedMap`，只需进行一些简单的修改。

### 接口小结

核心集合接口是Java集合框架的基础。

Java Collections Framework层次结构由两个不同的接口树组成：

* 第一棵树以`Collection`接口开始，它提供了所有集合使用的基本功能，例如`add`和`remove`方法。它的子接口--`Set`，`List`和`Queue`--提供更专业的集合。
* `Set`接口不允许重复元素。这对于存储诸如一副纸牌或学生记录之类的集合非常有用。`Set`接口有一个子接口`SortedSet`，它提供了集合中元素的排序。
* `List`接口提供有序集合，适用于需要精确控制每个元素插入位置的情况。您可以按照其确切位置从`List`中检索元素。
* `Queue`接口支持附加的插入，提取和检查操作。`Queue`中的元素通常以FIFO为基础进行排序。
* `Deque`接口可在两端进行插入，删除和检查操作。`Deque`中的元素可采用LIFO和FIFO。

第二棵树以`Map`接口开始，它建立键和值的映射关系，类似于`Hashtable`。

* `Map`的子接口`SortedMap`按升序或按`Comparator`指定的顺序维护其键值对。

这些接口允许独立于其表示的细节来操纵集合。

## 聚合操作

**注意**: 为了更好地理解本章节中的概念，请先复习 [Lambda Expressions](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html) 和 [Method References](https://docs.oracle.com/javase/tutorial/java/javaOO/methodreferences.html) 。

你为什么要使用集合？您不是简单地将对象存储在集合中并将其保留在那里。在大多数情况下，您使用集合来检索存储在其中的元素。

再次考虑 [Lambda表达式](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html) 一节中描述的场景。假设您正在创建社交网络应用程序。您希望创建一项功能，使管理员能够对满足特定条件的社交网络应用程序成员执行任何类型的操作，例如发送消息。

和以前一样，假设此社交网络应用程序的成员由以下 [`Person`](https://docs.oracle.com/javase/tutorial/collections/streams/examples/Person.java) 类表示：

```java
public class Person {

    public enum Sex {
        MALE, FEMALE
    }

    String name;
    LocalDate birthday;
    Sex gender;
    String emailAddress;
    
    // ...

    public int getAge() {
        // ...
    }

    public String getName() {
        // ...
    }
}
```

以下示例使用`for-each`循环打印集合 `roster` 中包含的所有成员的名称：

```java
for (Person p : roster) {
    System.out.println(p.getName());
}
```

以下示例打印集合 `roster` 中包含的所有成员，但使用`forEach`聚合操作：

```java
roster
    .stream()
    .forEach(e -> System.out.println(e.getName());
```

虽然在此示例中，使用聚合操作的版本比使用`for-each`循环的版本长，但您会看到使用批量数据操作的版本对于更复杂的任务将更简洁。

本章节包含以下主题：

- [管线和流](https://docs.oracle.com/javase/tutorial/collections/streams/index.html#pipelines)
- [聚合操作与迭代器的差异](https://docs.oracle.com/javase/tutorial/collections/streams/index.html#differences)

在示例 [`BulkDataOperationsExamples`](https://docs.oracle.com/javase/tutorial/collections/streams/examples/BulkDataOperationsExamples.java) 中查找本节中描述的代码摘录。

**管线和流**

*管道*是一系列聚合操作。以下示例使用由聚合操作 `filter` 和`forEach`组成的管道打印集合 `roster` 中包含的男性成员：

```java
roster
    .stream()
    .filter(e -> e.getGender() == Person.Sex.MALE)
    .forEach(e -> System.out.println(e.getName()));
```

将此示例与以下内容进行比较，以使用for-each循环打印包含在集合 `roster` 中的男性成员：

```java
for (Person p : roster) {
    if (p.getGender() == Person.Sex.MALE) {
        System.out.println(p.getName());
    }
}
```

一个管道包含以下元素：

 - 源：这可以是集合，数组，生成器函数或I/O通道。在此示例中，源是集合 `roster`。

 - 零次或多次中间操作：中间操作（例如 `filter`）会生成新流。

     流是一系列元素。与集合不同，它不是存储元素的数据结构。相反，流通过管道从源传输值。此示例通过调用方法 `stream` 从集合 `roster` 创建流。

     `filter` 操作返回一个新流，该流包含与其谓词匹配的元素（此操作的参数）。在此示例中，谓词是lambda表达式 `e -> e.getGender() == Person.Sex.MALE`。如果对象`e`的`gender`字段的值为`Person.Sex.MALE`，则返回布尔值`true`。因此，此示例中的 `filter` 操作返回包含集合 `roster` 中所有男性成员的流。

 - 终结操作：终结操作（例如`forEach`）产生非流结果，例如基本数据类型值（如`double`类型的值），集合，或者在

     `forEach`的情况下，根本没有值。在此示例中，`forEach`操作的参数是lambda表达式 `e -> System.out.println(e.getName())`，它在对象`e`上调用方法`getName`。（Java运行时和编译器推断对象`e`的类型是`Person`。）

以下示例使用由聚合操作 `filter`，`mapToInt`和`average`组成的管道计算集合 `roster` 中包含的所有男性成员的平均年龄：

```java
double average = roster
    .stream()
    .filter(p -> p.getGender() == Person.Sex.MALE)
    .mapToInt(Person::getAge)
    .average()
    .getAsDouble();
```

`mapToInt`操作返回`IntStream`类型的新流（它是仅包含整数值的流）。该操作将其参数中指定的函数应用于特定流中的每个元素。在此示例中，函数是`Person::getAge`，它是一个返回成员年龄的方法引用。（或者，您可以使用lambda表达式 `e -> e.getAge()` 。）因此，此示例中的`mapToInt`操作返回一个流，该流包含集合 `roster` 中所有男性成员的年龄。

`average` 操作计算`IntStream`类型流中包含的元素的平均值。它返回一个`OptionalDouble`类型的对象。如果流不包含任何元素，则`average`操作返回一个空的`OptionalDouble`实例，并且调用`getAsDouble`方法会抛出`NoSuchElementException`。JDK包含许多终结操作，例如通过组合流的内容返回一个值的`average`。这些操作称为 *reduction operations* 。有关详细信息，请参阅 [Reduction](https://docs.oracle.com/javase/tutorial/collections/streams/reduction.html) 部分。

**聚合操作与迭代器的差异**

像`forEach`这样的聚合操作看起来就像迭代器一样。但是，它们有几个根本区别：

- **它们使用内部迭代器**: 聚合操作不包含 `next` 方法，以指示它们处理集合的下一个元素。使用内部委托，您的应用程序确定它迭代的集合，但JDK确定如何迭代集合。通过外部迭代，您的应用程序可以确定它迭代的集合以及迭代它的方式。但是，外部迭代只能按顺序迭代集合的元素。内部迭代没有此限制。它可以更容易地利用并行计算，这涉及将问题分解为子问题，同时解决这些问题，然后将解决方案的结果与子问题相结合。 有关更多信息，请参阅 [Parallelism](https://docs.oracle.com/javase/tutorial/collections/streams/parallelism.html) 一节。
- **它们处理来自流的元素**: 聚合操作处理流中的元素，而不是直接来自集合。因此，它们也称为流操作。
- **它们支持作为参数的行为**: 您可以将 [lambda表达式](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html) 指定为大多数聚合操作的参数。这使您可以自定义特定聚合操作的行为。

### Reduction

[Aggregate Operations](https://docs.oracle.com/javase/tutorial/collections/streams/index.html) 章节描述了下面的操作管线，它计算集合`roster`中所有男性成员的额平均年龄：

```java
double average = roster
    .stream()
    .filter(p -> p.getGender() == Person.Sex.MALE)
    .mapToInt(Person::getAge)
    .average()
    .getAsDouble();
```

JDK 包含很多终结操作（比如 [`average`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/IntStream.html#average--java/lang/reflect/Executable.html), [`sum`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/IntStream.html#sum--), [`min`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#min-java.util.Comparator-), [`max`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#max-java.util.Comparator-), 和 [`count`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#count--)）通过结合流的内容来返回一个值。这些操作被称为 *reduction operations*（还原操作）。JDK还包含另外一些还原操作，返回一个集合而不是单个值。很多还原操作执行某项特定任务，比如求平均值或者将元素分类。不过，JDK提供了通用的还原操作 [`reduce`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#reduce-T-java.util.function.BinaryOperator-) 和 [`collect`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#collect-java.util.function.Supplier-java.util.function.BiConsumer-java.util.function.BiConsumer-) ，本章节详细描述了这几个操作。

本章节涵盖以下主题：

- [Stream.reduce 方法](https://docs.oracle.com/javase/tutorial/collections/streams/reduction.html#reduce)
- [Stream.collect 方法](https://docs.oracle.com/javase/tutorial/collections/streams/reduction.html#collect)

你可以在示例 [`ReductionExamples`](https://docs.oracle.com/javase/tutorial/collections/streams/examples/ReductionExamples.java) 中找到本章节中的代码片段。

**Stream.reduce 方法**

[`Stream.reduce`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#reduce-T-java.util.function.BinaryOperator-) 方法是通用还原操作。考虑下面的管线，它计算集合`roster`中所有男性成语的年龄之和。它使用了[`Stream.sum`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/IntStream.html#sum--) 还原操作。

```java
Integer totalAge = roster
    .stream()
    .mapToInt(Person::getAge)
    .sum();
```

与下面的管线比较，它使用 `Stream.reduce` 操作来计算相同的值。

```java
Integer totalAgeReduce = roster
   .stream()
   .map(Person::getAge)
   .reduce(
       0,
       (a, b) -> a + b);
```

这个例子中的`reduce` 操作接受两个参数：

- `identity`: 如果流中没有元素，则`identity`元素既是还原的初始值又是默认结果。在这个例子中，`identity`元素是 0 ；如果集合 `roster`中没有成员，则这是年龄总和的初始值和默认值。

- `accumulator`: 累加器函数有两个参数：还原的部分结果（在本例中，是到目前为止所有处理过的整数的总和）和流的下一个元素（在本例中为一个整数）。它返回一个新的部分结果。在这个例子中，累加器函数是一个lambda表达式，它累加两个`Integer`值并返回一个`Integer`值：

  ```java
  (a, b) -> a + b
  ```

`reduce`操作总是返回一个新值。但是，累加器函数每次处理流的元素时也会返回一个新值。假设您要将流的元素还原为更复杂的对象，例如集合。这可能会妨碍您的应用程序的性能。如果你的`reduce`操作涉及向集合中添加元素，那么每次你的累加器函数处理一个元素时，它都会创建一个包含该元素的新集合，这是低效的。相反，更新现有集合会更有效。您可以使用 [`Stream.collect`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#collect-java.util.function.Supplier-java.util.function.BiConsumer-java.util.function.BiConsumer-) 执行此操作，下一节将介绍该方法。

**Stream.collect 方法**

`reduce` 方法每次处理一个元素都会产生一个新值。 [`collect`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#collect-java.util.function.Supplier-java.util.function.BiConsumer-java.util.function.BiConsumer-) 方法修改、变异现有的值。

考虑如何找到一个流的平均值。你需要两部分数据：流中值得总数和那些值的总和。不过，类似于`reduce`方法以及所有其他还原方法，`collect`方法返回单一值。你可以创建一个新的数据类型，包含成员变量，表示数值的总数和总和，如下面例子所示：

```java
class Averager implements IntConsumer
{
    private int total = 0;
    private int count = 0;
        
    public double average() {
        return count > 0 ? ((double) total)/count : 0;
    }
        
    public void accept(int i) { total += i; count++; }
    public void combine(Averager other) {
        total += other.total;
        count += other.count;
    }
}
```

下面的管线使用 `Averager` 类和 `collect` 方法来计算所有男性成语的平均年龄：

```java
Averager averageCollect = roster.stream()
    .filter(p -> p.getGender() == Person.Sex.MALE)
    .map(Person::getAge)
    .collect(Averager::new, Averager::accept, Averager::combine);
                   
System.out.println("Average age of male members: " +
    averageCollect.average());
```

例子中 `collect` 操作使用三个参数：

- `supplier`: 一个工厂函数，负责构建新的实例。它为`collect`操作创建结果容器的实例。在这个例子中，它是`Averager`类的实例。
- `accumulator`: 累加器函数将流元素合并到结果容器中。在这个例子中，它通过将`count`变量增加1，并将流元素的值添加到`total`成员变量，该元素是表示男性成员年龄的整数，来修改`Averager`结果容器。
- `combiner`: 组合器函数接受两个结果容器并合并其内容。在这个例子中，它通过将`count`变量与另一个`Averager`实例的`count`成员变量相加并将`total`成员变量与另一个`Averager`实例的`total`成员变量值相加来修改`Averager`结果容器。

注意下面的细节：

- `supplier`是一个 lambda 表达式 (或者是一个方法引用) 而不像是 `reduce` 操作中`identity`元素那样的值。
- 累加器和组合器函数都不返回值。
- 你可以对并行流使用`collect`操作。参考 [Parallelism](https://docs.oracle.com/javase/tutorial/collections/streams/parallelism.html) 章节获取更多细节。（如果你对一个并行流执行`collect`操作，则当组合器函数创建一个新对象（这个例子中就是`Averager`对象）时，JDK都会创建一个新的线程。因此，你不需要担心线程同步问题。）

尽管JDK为您提供了`average`操作来计算流中元素的平均值，但是如果需要从流的元素中计算多个值，则可以使用`collect`操作和自定义类。

`collect`操作最适合集合。以下示例使用`collect`操作将男性成员的名字放在集合中：

```java
List<String> namesOfMaleMembersCollect = roster
    .stream()
    .filter(p -> p.getGender() == Person.Sex.MALE)
    .map(p -> p.getName())
    .collect(Collectors.toList());
```

这个版本的`collect`操作接受一个 [`Collector`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collector.html) 类型的参数。这个类封装了在`collect`操作中作为参数使用的函数（`supplier`, `accumulator`, 和 `combiner` 函数）。

 [`Collectors`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html) 包含许多有用的还原操作，比如将元素累加到集合中或者按照各种标准将元素分类。这些还原操作返回`Collector`类的实例，因此你可以使用它们作为`collect`操作的参数。

这个例子使用 [`Collectors.toList`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html#toList--) 操作，将流元素累计到一个新的`List`实例中。与`Collectors`类中的大多数操作一样，`toList`操作符返回`Collector`的实例，而不是集合。

下面的例子将`roster`集合的成员按照性别分组：

```java
Map<Person.Sex, List<Person>> byGender =
    roster
        .stream()
        .collect(
            Collectors.groupingBy(Person::getGender));
```

 [`groupingBy`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html#groupingBy-java.util.function.Function-) 操作返回一个map，其键是应用指定为其参数的lambda表达式（称为*分类函数*）得到的值。在此示例中，返回的map包含两个键，`Person.Sex.MALE`和`Person.Sex.FEMALE`。键的对应值是包含流元素的`List`的实例，当由分类函数处理时，流元素对应于键值。例如，与键`Person.Sex.MALE`对应的值是包含所有男性成员的`List`的实例。

以下示例检索集合`roster`中每个成员的名称，并按性别对它们进行分组：

```java
Map<Person.Sex, List<String>> namesByGender =
    roster
        .stream()
        .collect(
            Collectors.groupingBy(
                Person::getGender,                      
                Collectors.mapping(
                    Person::getName,
                    Collectors.toList())));
```

这个例子中的 [`groupingBy`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html#groupingBy-java.util.function.Function-java.util.stream.Collector-) 操作有两个参数，一个分类函数和一个`Collector`实例。`Collector`参数称为*下游收集器*。这是Java运行时应用于另一个收集器的结果的收集器。因此，这个`groupingBy`操作使您能够将`collect`方法应用于`groupingBy`运算符创建的`List`值。此示例应用收集器 [`mapping`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html#mapping-java.util.function.Function-java.util.stream.Collector-java.util.stream.Collector-) ，它将映射函数`Person::getName`应用于流的每个元素。因此，生成的流只包含成员的名称。包含一个或多个下游收集器的管道（如此示例）称为*多级还原*。

以下示例检索每个性别的成员的总年龄：

```java
Map<Person.Sex, Integer> totalAgeByGender =
    roster
        .stream()
        .collect(
            Collectors.groupingBy(
                Person::getGender,                      
                Collectors.reducing(
                    0,
                    Person::getAge,
                    Integer::sum)));
```

[`reducing`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html#reducing-U-java.util.function.Function-java.util.function.BinaryOperator-) 操作接受三个参数：

 - `identity`：与`Stream.reduce`操作一样，如果流中没有元素，则`identity`元素既是还原的初始值又是默认结果。在这个例子中，`identity`元素是 0 ；如果不存在成员，则这是年龄总和的初始值和默认值。
 - `mapper`：`reducing`操作将此映射器函数应用于所有流元素。在此示例中，映射器检索每个成员的年龄。
 - `operation`：操作函数用于还原映射值。在此示例中，操作函数累加`Integer`值。

以下示例检索每个性别的成员的平均年龄：

```java
Map<Person.Sex, Double> averageAgeByGender = roster
    .stream()
    .collect(
        Collectors.groupingBy(
            Person::getGender,                      
            Collectors.averagingInt(Person::getAge)));
```

### Parallelism

并行计算涉及将问题划分为子问题，同时解决这些问题（并行地，每个子问题在单独的线程中运行），然后将子问题的结果组合到一起。Java SE提供 [fork/join framework](https://docs.oracle.com/javase/tutorial/essential/concurrency/forkjoin.html) ，使您可以更轻松地在应用程序中实现并行计算。但是，使用此框架，您必须指定问题如何细分（分区）。通过聚合操作，Java运行时为您执行此分区和组合解决方案。

在使用集合的应用程序中实现并行性的一个难点是集合不是线程安全的，这意味着多线程无法在不引入 [线程干扰](https://docs.oracle.com/javase/tutorial/essential/concurrency/interfere.html) 或者 [内存一致性错误](https://docs.oracle.com/javase/tutorial/essential/concurrency/memconsist.html).的情况下操作集合。Collections Framework提供 [synchronization wrappers](https://docs.oracle.com/javase/tutorial/collections/implementations/wrapper.html) ，它将自动同步机制添加到任意集合，使其成为线程安全的。但是，同步引入了 [线程竞争](https://docs.oracle.com/javase/tutorial/essential/concurrency/sync.html#thread_contention) 。您希望避免线程竞争，因为它会阻止线程并行运行。通过聚合操作和并行流，您可以实现与非线程安全集合的并行性，前提是在操作集合时不要修改集合。

请注意，并行性不一定会比串行执行操作更快，尽管可能有足够的数据和处理器内核。虽然聚合操作使您能够更轻松地实现并行性，但您仍有责任确定您的应用程序是否适合并行性。

本节包括以下主题：

- [并行执行流](https://docs.oracle.com/javase/tutorial/collections/streams/parallelism.html#executing_streams_in_parallel)
- [并发还原](https://docs.oracle.com/javase/tutorial/collections/streams/parallelism.html#concurrent_reduction)
- [排序](https://docs.oracle.com/javase/tutorial/collections/streams/parallelism.html#ordering)
- 副作用
  - [Laziness](https://docs.oracle.com/javase/tutorial/collections/streams/parallelism.html#laziness)
  - [Interference](https://docs.oracle.com/javase/tutorial/collections/streams/parallelism.html#interference)
  - [有状态的 Lambda 表达式](https://docs.oracle.com/javase/tutorial/collections/streams/parallelism.html#stateful_lambda_expressions)

你可以在 [`ParallelismExamples`](https://docs.oracle.com/javase/tutorial/collections/streams/examples/ParallelismExamples.java) 示例中看到本章节中的代码片段。

**并行操作流**

您可以串行或并行执行流。当流并行执行时，Java运行时将流分区为多个子流。聚合操作迭代并并行处理这些子流，然后组合结果。

创建流时，除非特别指定，否则它始终是串行流。要创建并行流，请调用操作 [`Collection.parallelStream`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html#parallelStream--) 。或者，调用操作 [`BaseStream.parallel`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/BaseStream.html#parallel--) 。例如，以下语句并行计算所有男性成员的平均年龄：

```java
double average = roster
    .parallelStream()
    .filter(p -> p.getGender() == Person.Sex.MALE)
    .mapToInt(Person::getAge)
    .average()
    .getAsDouble();
```

**并发还原**

再次考虑以下示例（在 [Reduction](https://docs.oracle.com/javase/tutorial/collections/streams/reduction.html) 部分中描述）按性别对成员进行分组。这个例子调用`collect`操作，它将集合`roster`还原为`Map`：

```java
Map<Person.Sex, List<Person>> byGender =
    roster
        .stream()
        .collect(
            Collectors.groupingBy(Person::getGender));
```

下面是等效的并发版本：

```java
ConcurrentMap<Person.Sex, List<Person>> byGender =
    roster
        .parallelStream()
        .collect(
            Collectors.groupingByConcurrent(Person::getGender));
```

这称为*并发还原*。如果包含`collect`操作的特定管线满足以下所有条件，Java运行时将执行并发还原：

- 该流是并行流。
- `collect` 操作的参数，那个收集器，拥有特性 [`Collector.Characteristics.CONCURRENT`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collector.Characteristics.html#CONCURRENT) 。为了确定收集器的该特性，调用 [`Collector.characteristics`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collector.Characteristics.html) 方法。
- 要么流是无序的，要么收集器拥有特性 [`Collector.Characteristics.UNORDERED`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collector.Characteristics.html#UNORDERED) 。为了保证流是无序的，调用 [`BaseStream.unordered`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/BaseStream.html#unordered--) 操作。

**注意**：此示例返回 [`ConcurrentMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentMap.html) 实例而不是`Map `并调用 [`groupingByConcurrent`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html#groupingByConcurrent-java.util.function.Function-) 操作而不是`groupingBy`。（有关`ConcurrentMap`的更多信息，请参见 [Concurrent Collections](https://docs.oracle.com/javase/tutorial/essential/concurrency/collections.html) 一节。）与操作`groupingByConcurrent`不同，操作` groupingBy`在并行流中表现不佳。（这是因为它通过键合并两个映射来运行，这在计算上成本高昂。）同样，操作[`Collectors.toConcurrentMap`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html#toConcurrentMap-java.util.function.Function-java.util.function.Function-) 使用并行流比使用 [`Collectors.toMap`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html#toMap-java.util.function.Function-java.util.function.Function-) 表现更好。

**排序**

管线处理流的元素的顺序取决于流是以串行还是并行方式执行，流的源和中间操作。例如，考虑以下示例，使用`forEach`操作多次打印`ArrayList`实例的元素：

```java
Integer[] intArray = {1, 2, 3, 4, 5, 6, 7, 8 };
List<Integer> listOfIntegers =
    new ArrayList<>(Arrays.asList(intArray));

System.out.println("listOfIntegers:");
listOfIntegers
    .stream()
    .forEach(e -> System.out.print(e + " "));
System.out.println("");

System.out.println("listOfIntegers sorted in reverse order:");
Comparator<Integer> normal = Integer::compare;
Comparator<Integer> reversed = normal.reversed(); 
Collections.sort(listOfIntegers, reversed);  
listOfIntegers
    .stream()
    .forEach(e -> System.out.print(e + " "));
System.out.println("");
     
System.out.println("Parallel stream");
listOfIntegers
    .parallelStream()
    .forEach(e -> System.out.print(e + " "));
System.out.println("");
    
System.out.println("Another parallel stream:");
listOfIntegers
    .parallelStream()
    .forEach(e -> System.out.print(e + " "));
System.out.println("");
     
System.out.println("With forEachOrdered:");
listOfIntegers
    .parallelStream()
    .forEachOrdered(e -> System.out.print(e + " "));
System.out.println("");
```

此示例包含五个管线。它打印输出类似于以下内容：

```
listOfIntegers:
1 2 3 4 5 6 7 8
listOfIntegers sorted in reverse order:
8 7 6 5 4 3 2 1
Parallel stream:
3 4 1 6 2 5 7 8
Another parallel stream:
6 3 1 5 7 8 4 2
With forEachOrdered:
8 7 6 5 4 3 2 1
```

此示例执行以下操作：

 - 第一个管线按照元素添加到列表的顺序打印列表`listOfIntegers`的元素。
 - 第二个管线在按方法 [`Collections.sort`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#sort-java.util.List-) 排序之后打印`listOfIntegers`的元素。
 - 第三和第四个管线以看起来随机的顺序打印列表的元素。请记住，流处理在处理流的元素时使用内部迭代。因此，当您并行执行流时，Java编译器和运行时确定处理流元素的顺序，以最大化并行计算的优势，除非流操作另有指定。
 - 第五个管线使用方法 [`forEachOrdered`](https://docs.oracle.com/javase/8/docs/api/java/util/stream/Stream.html#forEachOrdered-java.util.function.Consumer-) ，无论您是以串行还是并行方式执行流，它都按照源指定的顺序处理流的元素。请注意，如果对并行流使用`forEachOrdered`这样的操作，则可能会失去并行性的好处。

**副作用**

如果方法或表达式除了返回或产生值之外还修改计算机的状态，则该方法或表达式具有副作用。示例包括可变还原（使用`collect`操作的操作：请参阅 [Reduction](https://docs.oracle.com/javase/tutorial/collections/streams/reduction.html)  部分以获取更多信息）以及调用`System.out.println`方法进行调试。JDK很好地处理了管线中的某些副作用。特别地，`collect`方法被设计为以并行安全的方式执行具有副作用的最常见的流操作。像`forEach`和`peek`这样的操作是为副作用而设计的。返回`void`的lambda表达式，例如调用`System.out.println`的表达式，只能有副作用。即便如此，你应该小心使用`forEach`和`peek`操作；如果您对并行流使用其中一个操作，那么Java运行时可以从多个线程同时调用您指定为其参数的lambda表达式。另外，永远不要传递作为参数的lambda表达式，如果这些表达式在诸如`filter`和`map`之类的操作中具有副作用。以下部分讨论 [干扰](https://docs.oracle.com/javase/tutorial/collections/streams/parallelism.html#interference) and [有状态的 lambda 表达式](https://docs.oracle.com/javase/tutorial/collections/streams/parallelism.html#stateful_lambda_expressions) ，这两者都可能是副作用的来源，并且可能返回不一致或不可预测的结果，尤其是在并行流中。但是，首先讨论  [laziness](https://docs.oracle.com/javase/tutorial/collections/streams/parallelism.html#laziness)  的概念，因为它对干扰有直接影响。

**Laziness**

所有中间操作都是*惰性的*。如果表达式，方法或算法仅在需要时才计算其值，则它是惰性的。（如果立即评估或处理，则算法是*饥饿的*。）中间操作是惰性的，因为它们在终结操作开始之前不开始处理流的内容。懒惰地处理流使Java编译器和运行时能够优化它们处理流的方式。例如，在诸如 [Aggregate Operations](https://docs.oracle.com/javase/tutorial/collections/streams/index.html) 部分中描述的`filter` -`mapToInt`-`average`示例的管线中，`average`操作可以从`mapToInt`操作创建的流中获取前几个整数，它从`filter`操作中获取元素。`average`操作将重复此过程，直到它从流中获得所有必需元素，然后计算平均值。

**Interference**

流操作中的Lambda表达式不应相互*干扰*。在流水线处理流时修改流的源时会发生干扰。例如，以下代码尝试连接`List` `listOfStrings`中包含的字符串。但是，它会抛出`ConcurrentModificationException`：

```java
try {
    List<String> listOfStrings =
        new ArrayList<>(Arrays.asList("one", "two"));
         
    // This will fail as the peek operation will attempt to add the
    // string "three" to the source after the terminal operation has
    // commenced. 
             
    String concatenatedString = listOfStrings
        .stream()
        
        // Don't do this! Interference occurs here.
        .peek(s -> listOfStrings.add("three"))
        
        .reduce((a, b) -> a + " " + b)
        .get();
                 
    System.out.println("Concatenated string: " + concatenatedString);
         
} catch (Exception e) {
    System.out.println("Exception caught: " + e.toString());
}
```

这个例子利用`reduce`操作将`listOfStrings`中包含的字符串连接到`Optional<String>`值之后，这是一个终结操作。但是，这里的管线调用中间操作`peek`，它试图向`listOfStrings`添加一个新元素。请记住，所有中间操作都是懒惰的。这意味着此示例中的管线在调用操作`get`时开始执行，并在`get`操作完成时结束执行。`peek`操作的参数试图在执行管线期间修改流源，这会导致Java运行时抛出`ConcurrentModificationException`。

**有状态的 Lambda 表达式**

避免在流操作中使用*有状态lambda表达式*作为参数。有状态lambda表达式的结果取决于在执行管线期间可能更改的任何状态。下面的示例使用`map`中间操作将`List` `listOfIntegers`中的元素添加到新的`List`实例。它执行两次，首先使用串行流，然后使用并行流：

```java
List<Integer> serialStorage = new ArrayList<>();
     
System.out.println("Serial stream:");
listOfIntegers
    .stream()
    
    // Don't do this! It uses a stateful lambda expression.
    .map(e -> { serialStorage.add(e); return e; })
    
    .forEachOrdered(e -> System.out.print(e + " "));
System.out.println("");
     
serialStorage
    .stream()
    .forEachOrdered(e -> System.out.print(e + " "));
System.out.println("");

System.out.println("Parallel stream:");
List<Integer> parallelStorage = Collections.synchronizedList(
    new ArrayList<>());
listOfIntegers
    .parallelStream()
    
    // Don't do this! It uses a stateful lambda expression.
    .map(e -> { parallelStorage.add(e); return e; })
    
    .forEachOrdered(e -> System.out.print(e + " "));
System.out.println("");
     
parallelStorage
    .stream()
    .forEachOrdered(e -> System.out.print(e + " "));
System.out.println("");
```

lambda 表达式 `e -> { parallelStorage.add(e); return e; }` 是有状态的。每次执行该代码都可能产生不同的结果。该例子输出如下结果：

```
Serial stream:
8 7 6 5 4 3 2 1
8 7 6 5 4 3 2 1
Parallel stream:
8 7 6 5 4 3 2 1
1 3 6 2 4 5 8 7
```

无论流是以串行还是并行方式执行，`forEachOrdered`操作都按流指定的顺序处理元素。但是，当并行执行流时，`map`操作处理由Java运行时和编译器指定的流的元素。因此，每次运行代码时，lambda表达式 `e -> { parallelStorage.add(e); return e; }`添加元素到`List` `listOfIntegers`的顺序都会有所不同。为了保证确定性和可预测的结果，请确保流操作中的lambda表达式参数不具有状态。

**注意**：此示例调用方法 [`synchronizedList`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#synchronizedList-java.util.List-) 因此`List` `andlineStorage`是线程安全的。请记住，集合不是线程安全的。这意味着多个线程不应同时访问特定集合。假设在创建`parallelStorage`时不调用`synchronizedList`方法：

```java
List<Integer> parallelStorage = new ArrayList<>();
```

该示例行为不正常，因为多个线程访问和修改`parallelStorage`而没有像同步这样的机制来安排特定线程何时可以访问`List`实例。因此，该示例可以打印类似于以下内容的输出：

```
Parallel stream:
8 7 6 5 4 3 2 1
null 3 5 4 7 8 1 2
```

## 实现

实现是用来存储集合的数据对象，这些对象的类实现了 [接口](https://docs.oracle.com/javase/tutorial/collections/interfaces/index.html) 部分中描述的接口。本章节介绍下面几种实现：

- **通用实现** 是最普遍使用的实现，为日常使用设计。它们在标题为“通用实现”的表中总结。
- **专用实现** 为特殊情况使用设计，展现出非标准的性能特征、使用限制或者特殊行为。
- **并发实现** 为支持高并发设计，通常是以单线程性能为代价。这些实现是 `java.util.concurrent` 包的一部分。
- **包装器实现** 与其他类型的实现结合使用，通常是通用实现，来提供附加功能或者限制功能。
- **方便实现** 是迷你实现，通常通过静态工厂方法提供，为特殊集合（例如，单例集）的通用实现提供方便，有效的替代方案。
- **抽象实现** 是有助于构建自定义实现的骨架实现 - 稍后将在 [自定义集合实现](https://docs.oracle.com/javase/tutorial/collections/custom-implementations/index.html) 部分中进行介绍。一个高级主题，并不是特别困难，但相对较少的人需要这样做。

通用实现总结在下面表中。

| Interfaces | Hash table Implementations | Resizable array Implementations | Tree Implementations | Linked list Implementations | Hash table + Linked list Implementations |
| ---------- | -------------------------- | ------------------------------- | -------------------- | --------------------------- | ---------------------------------------- |
| `Set`      | `HashSet`                  |                                 | `TreeSet`            |                             | `LinkedHashSet`                          |
| `List`     |                            | `ArrayList`                     |                      | `LinkedList`                |                                          |
| `Queue`    |                            |                                 |                      |                             |                                          |
| `Deque`    |                            | `ArrayDeque`                    |                      | `LinkedList`                |                                          |
| `Map`      | `HashMap`                  |                                 | `TreeMap`            |                             | `LinkedHashMap`                          |

从表中可以看出，Java Collections Framework提供了几个 [`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html), [`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html) , 和 [`Map`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) 的通用实现。在每种情况下，一个实现 -  [`HashSet`](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html), [`ArrayList`](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html), and [`HashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html)  - 显然是大多数应用程序使用的，所有其他条件相同。注意 [`SortedSet`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html) 和 [`SortedMap`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html) 接口在表中没有。每个此类接口都有一个实现 [(`TreeSet`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html) 和 [`TreeMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html)) 出现在`Set`和`Map`行中。有两个通用的`Queue`实现 - [`LinkedList`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html)，它也是一个`List ` 实现，和 [`PriorityQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html)，此表省略。这两个实现提供了非常不同的语义：`LinkedList`提供FIFO语义，而`PriorityQueue`根据它们的值对其元素进行排序。

每个通用实现都提供其接口中包含的所有可选操作。所有都允许`null`元素，键和值。无同步（线程安全）。所有都具有*fail-fast迭代器*，它在迭代期间检测非法并发修改并快速且干净地失败，而不是在未来的未确定时间冒任意，不确定行为的风险。所有都是`Serializable`并且都支持公共`clone`方法。

这些实现是不同步的这一事实代表了对过去规则的突破：遗留集合`Vector`和`Hashtable`是同步的。采用本方法是因为当同步没有任何好处时经常使用集合。这些用途包括单线程使用，只读使用，以及用作进行自身同步的大型数据对象的一部分。一般来说，良好的API设计实践不会让用户为他们不使用的功能付出代价。此外，在某些情况下，不必要的同步可能导致死锁。

如果您需要线程安全的集合， [Wrapper Implementations](https://docs.oracle.com/javase/tutorial/collections/implementations/wrapper.html) 部分中描述的同步包装器允许*any*集合被转换成同步的集合。因此，同步对于通用实现是可选的，而对于遗留实现是必需的。此外，`java.util.concurrent`包提供了`BlockingQueue`接口的并发实现，它扩展了`Queue`，以及`ConcurrentMap`接口的并发实现，扩展了`Map`。这些实现提供了比仅仅同步实现更高的并发性。

通常，您应该考虑接口，而不是实现。这就是本节中没有编程示例的原因。在大多数情况下，实现的选择仅影响性能。在 [Interfaces](https://docs.oracle.com/javase/tutorial/collections/interfaces/index.html) 部分中提到的首选样式是在创建`Collection`时选择一个实现，并且 立即将新集合分配给相应接口类型的变量（或将集合传递给期望接口类型参数的方法）。通过这种方式，程序不会依赖于给定实现中的任何附加方法，让程序员可以随时根据性能问题或行为细节保证更改实现。

以下部分简要讨论了实现。 使用诸如*constant-time*，*log*，*linear*，*n log(n)*和*quadratic*之类的单词来描述实现的性能，以指代执行操作的时间复杂度的渐近上限。所有这一切都是冗长而拗口的，如果你不知道它意味着什么并不重要。如果您有兴趣了解更多信息，请参阅任何优秀的算法教科书。需要记住的一点是，这种性能指标有其局限性。有时，名义上较慢的实施可能会更快。如有疑问，请评估性能！

### Set 实现

`Set` 实现分为通用实现和专用实现两种。

**通用 Set 实现**

有三种通用的 [`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html) i实现 - [`HashSet`](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html), [`TreeSet`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeSet.html), 和 [`LinkedHashSet`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashSet.html) 。使用这三种中的哪一种通常都是很明显的。`HashSet`比`TreeSet`快得多（大多数操作的常量时间与对数时间）但不提供排序保证。如果需要使用`SortedSet`接口中的操作，或者需要按值进行迭代，请使用`TreeSet;` 否则，使用`HashSet`。可以肯定的是，大多数时候你最终都会使用`HashSet`。

`LinkedHashSet`在某种意义上介于`HashSet`和`TreeSet`之间。它实现为一个哈希表，其中包含一个链表，它提供了插入顺序迭代（最近最少插入为最新）并且运行速度几乎与`HashSet`一样快。`LinkedHashSet`实现使其客户端免受`HashSet`提供的未指定的，通常是混乱的排序的困扰，而不会导致与`TreeSet`相关的成本增加。

关于`HashSet`值得记住的一件事是，迭代次数是元素条目数和桶数（容量）之和的线性函数。因此，选择太高的初始容量会浪费空间和时间。另一方面，选择一个太低的初始容量会在每次强制增加容量时复制数据结构，从而浪费时间。如果未指定初始容量，则默认值为16。过去，选择素数作为初始容量有一些优势，不过现在已经不再奏效。在内部，容量总是四舍五入到2的幂。使用`int`构造函数指定初始容量。以下代码行分配一个初始容量为64的`HashSet`。

```java
Set<String> s = new HashSet<String>(64);
```

`HashSet`类还有一个称为加载因子的调整参数。如果您非常关心`HashSet`的空间消耗，请阅读`HashSet`文档以获取更多信息。否则，只接受默认值，不过这几乎总是正确的事情。

如果您接受默认加载因子但想要指定初始容量，请选择一个大约是您希望该组增长的大小的两倍的数字。如果您的猜测偏大，您可能会浪费一些空间，时间或两者，但这不太可能是一个大问题。

`LinkedHashSet`具有与`HashSet`相同的调整参数，但迭代时间不受容量影响。`TreeSet`没有调整参数。

**专用 Set 实现**

有两个专用的`Set`实现 - [`EnumSet`](https://docs.oracle.com/javase/8/docs/api/java/util/EnumSet.html) 和 [`CopyOnWriteArraySet`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CopyOnWriteArraySet.html) 。

`EnumSet`是枚举类型的高性能`Set`实现。枚举集的所有成员必须具有相同的枚举类型。在内部，它由位向量表示，通常是单个`long`。枚举集支持在枚举类型的范围上迭代。例如，给定星期几的枚举声明，您可以迭代工作日。`EnumSet`类提供了一个简单的静态工厂来帮你实现该功能。

```java
for (Day d : EnumSet.range(Day.MONDAY, Day.FRIDAY))
    System.out.println(d);
```

枚举集还为传统的位标志提供了丰富的，类型安全的替代品。

```java
EnumSet.of(Style.BOLD, Style.ITALIC)
```

`CopyOnWriteArraySet`是一个由*copy-on-write*数组备份的`Set`实现。所有可变操作，例如`add`, `set`, 和 `remove`，都是通过创建数组的新副本来实现的，不需要锁定。甚至迭代也可以安全地与元素插入和删除同时进行。与大多数`Set`实现不同，`add`，`remove`和`contains`方法需要与集合大小成比例的时间。此实现仅适用于很少修改但经常迭代的集合。它非常适合维护必须防止重复的事件处理程序列表。

### List 实现

`List` 实现分为通用实现和专用实现两种。

**通用 List 实现**

有两个通用的 [`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html) 实现-- [`ArrayList`](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayList.html) 和 [`LinkedList`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html) 。大多数情况下，您可能会使用`ArrayList`，它提供常量时间复杂度的指定位置访问，并且速度非常快。它不必为`List`中的每个元素分配节点对象，并且当它必须同时移动多个元素时，它可以利用`System.arraycopy`。可以将`ArrayList`视为没有同步开销的`Vector`。

如果经常将元素添加到`List`的开头或迭代`List`以从其内部删除元素，则应考虑使用`LinkedList`。这些操作在`LinkedList`中消耗常量时间，而在`ArrayList`中消耗线性时间。但是你的性能要付出很大的代价。指定位置访问在`LinkedList`中消耗线性时间，而在`ArrayList`中消耗常量时间。此外，`LinkedList`的时间复杂度中常数因子更大。如果您认为要使用`LinkedList`，请在做出选择之前使用`LinkedList`和`ArrayList`测量应用程序的性能：`ArrayList`通常更快。

`ArrayList`有一个调整参数 - 初始容量，它指的是`ArrayList`在增长之前可以容纳的元素数。`LinkedList`没有调优参数和七个可选操作，其中一个是`clone`。其他六个是 `addFirst`, `getFirst`, `removeFirst`, `addLast`, `getLast`, 和 `removeLast`。`LinkedList`也实现了`Queue`接口。

**专用 List 实现**

[`CopyOnWriteArrayList`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/CopyOnWriteArrayList.html) 是由copy-on-write数组备份的`List`实现。此实现在本质上类似于`CopyOnWriteArraySet`。即使在迭代期间也不需要同步，并且保证迭代器永远不会抛出`ConcurrentModificationException`。此实现非常适合维护事件处理程序列表，其中更改很少发生，并且遍历频繁且可能耗时。

如果需要同步，`Vector`将比用`Collections.synchronizedList`同步的`ArrayList`稍快一些。但`Vector`有大量的遗留操作，因此请务必小心使用`List`接口操作`Vector`，否则您将无法在以后替换该实现。

如果您的 `List` 大小固定 - 也就是说，您永远不会使用 `remove`，`add`或除`containsAll`之外的任何批量操作 - 您有第三个选项，绝对值得考虑。有关详细信息，请参阅 [便捷实现](https://docs.oracle.com/javase/tutorial/collections/implementations/convenience.html) 部分中的`Arrays.asList`。

### Map 实现

`Map` 实现分为通用实现、专用实现以及并发实现三种。

**通用 Map 实现**

三个通用 [`Map`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html) 实现是 [`HashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html), [`TreeMap`](https://docs.oracle.com/javase/8/docs/api/java/util/TreeMap.html) 和 [`LinkedHashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedHashMap.html) 。如果需要`SortedMap`操作或按键排序的`Collection`-view迭代，请使用`TreeMap`; 如果您想要最大速度而不关心迭代顺序，请使用`HashMap`; 如果您想要近`HashMap`性能和插入顺序迭代，请使用`LinkedHashMap`。在这方面，`Map`的情况类似于`Set`。同样， [Set Implementations](https://docs.oracle.com/javase/tutorial/collections/implementations/set.html) 部分中的其他所有内容也适用于`Map`实现。

`LinkedHashMap`提供了`LinkedHashSet`不具备的两个功能。创建`LinkedHashMap`时，可以基于键访问而不是插入来对其进行排序。换句话说，仅查找与键相关联的值就会将该键移动到`Map`的末尾。此外，`LinkedHashMap`提供`removeEldestEntry`方法，可以重写此方法以强制执行在将新映射添加到`Map`时自动删除过时映射的策略。这使得实现自定义缓存变得非常容易。

例如，此覆盖将允许`Map`包含多达100个条目，然后每次添加新条目时它将删除最旧条目，从而保持100个条目的稳定状态。

```java
private static final int MAX_ENTRIES = 100;

protected boolean removeEldestEntry(Map.Entry eldest) {
    return size() > MAX_ENTRIES;
}
```

**专用 Map 实现**

有三种特殊用途的`Map`实现 -  [`EnumMap`](https://docs.oracle.com/javase/8/docs/api/java/util/EnumMap.html), [`WeakHashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/WeakHashMap.html) 和 [`IdentityHashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/IdentityHashMap.html) 。`EnumMap`是一个内部实现为 `array` 的实现，是一个与枚举键一起使用的高性能`Map`实现。此实现将`Map`接口的丰富性和安全性与接近数组的速度相结合。如果要将枚举映射到值，则应始终优先使用`EnumMap`而不是数组。

`WeakHashMap`是`Map`接口的一个实现，它只存储对其键的弱引用。仅存储弱引用允许在其键不再在`WeakHashMap`之外引用时对键值对进行垃圾收集。此类提供了利用弱引用功能的最简单方法。它对于实现“类似注册表”的数据结构很有用，其中当任何线程不再可以访问其键时，条目的可用性就会消失。

`IdentityHashMap`是基于哈希表的基于id的`Map`实现。此类对于拓扑保留对象图转换非常有用，例如序列化或深度复制。 要执行此类转换，您需要维护一个基于id的“节点表”，以跟踪已经找到的对象。基于id的映射还用于维护动态调试器和类似系统中的对象到元信息映射。最后，基于id的映射有助于挫败基于恶意`equals`方法的“欺骗攻击”，因为`IdentityHashMap`从不在其键上调用`equals`方法。这种实现的另一个好处是它很快。

**并发 Map 实现**

[`java.util.concurrent`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/package-summary.html) 包中包含 [`ConcurrentMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentMap.html) 接口，该接口使用原子`putIfAbsent`，`remove`和`replace`方法，同时[`ConcurrentHashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentHashMap.html) 实现该接口。

`ConcurrentHashMap`是一个由哈希表备份的高度并发，高性能的实现。执行检索时，此实现永远不会阻塞，并允许客户端选择更新的并发级别。它旨在作为`Hashtable`的替代品：除了实现`ConcurrentMap`之外，它还支持`Hashtable`特有的所有遗留方法。同样，如果您不需要遗留操作，请小心使用`ConcurrentMap`接口对其进行操作。

### Queue 实现

`Queue` 实现分为通用实现和并发实现两类。

**通用 Queue 实现**

如上一节所述，`LinkedList`实现了`Queue`接口，为`add`，`poll`等提供了先进先出（FIFO）队列操作。

[`PriorityQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/PriorityQueue.html) 类是基于堆数据结构的优先级队列。此队列根据构造时指定的顺序对元素进行排序，这可以是元素的自然顺序或显式`Comparator`强加的排序。

队列检索操作 -  `poll`，`remove`，`peek`和`element` - 访问队列头部的元素。队列的头部是指定排序的最小元素。如果多个元素被判定为最小值，则队列头部是这些元素之一，此时排序规则被随机打破。

`PriorityQueue`及其迭代器实现了`Collection`和`Iterator`接口的所有可选方法。方法 `iterator` 中提供的迭代器不保证以任何特定顺序遍历`PriorityQueue`的元素。对于有序遍历，请考虑使用 `Arrays.sort(pq.toArray())`。

**并发 Queue 实现**

`java.util.concurrent`包中包含一组同步的`Queue`接口和类。[`BlockingQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/BlockingQueue.html) 使用等待队列在检索元素时变为非空的操作以及在存储元素时等待队列中产生可用的空间的操作来扩展`Queue`。此接口由以下类实现：

- [`LinkedBlockingQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/LinkedBlockingQueue.html) — 由链接节点支持的可选有界FIFO阻塞队列
- [`ArrayBlockingQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ArrayBlockingQueue.html) — 由数组支持的有界FIFO阻塞队列
- [`PriorityBlockingQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/PriorityBlockingQueue.html) — 由堆支持的无界阻塞优先级队列
- [`DelayQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/DelayQueue.html) — 由堆支持的基于时间的调度队列
- [`SynchronousQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/SynchronousQueue.html) — 一个使用`BlockingQueue`接口的简单集合点机制

在JDK 7中，[`TransferQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/TransferQueue.html) 是一个特殊的`BlockingQueue`，其中向队列添加元素的代码可以选择等待（阻塞）另一个线程中的代码来检索元素。`TransferQueue`有一个实现：

- [`LinkedTransferQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/LinkedTransferQueue.html) — 基于链接节点的无界`TransferQueue`


### Deque 实现

`Deque`接口，发音为“deck”，表示双端队列。`Deque`接口可以实现为各种类型的 `Collections`。 `Deque`接口实现分为通用和并发实现。

**通用 Deque 实现**

通用实现包括`LinkedList`和`ArrayDeque`类。`Deque`接口支持两端元素的插入，移除和检索。[`ArrayDeque`](https://docs.oracle.com/javase/8/docs/api/java/util/ArrayDeque.html) 类是`Deque`接口的可调整大小的数组实现，而 [`LinkedList`](https://docs.oracle.com/javase/8/docs/api/java/util/LinkedList.html) 类是列表实现。

`Deque`接口中的基本插入，删除和检索操作`addFirst`，`addLast`，`removeFirst`，`removeLast`，`getFirst`和`getLast`。 方法`addFirst`在头部添加一个元素，而`addLast`在`Deque`实例的尾部添加一个元素。

`LinkedList`实现比`ArrayDeque`实现更灵活。`LinkedList`实现所有可选的列表操作。`LinkedList`实现中允许使用`null`元素，但`ArrayDeque`实现中不允许使用`null`元素。

在效率方面，`ArrayDeque`比`LinkedList`更有效，可以在两端添加和删除操作。`LinkedList`实现中的最佳操作是在迭代期间删除当前元素。 LinkedList实现不是迭代的理想结构。

`LinkedList`实现比`ArrayDeque`实现消耗更多内存。对于`ArrayDeque`实例遍历，请使用以下任何一种方法：

**foreach**

`foreach` 很快，可以用于各种列表：

```java
ArrayDeque<String> aDeque = new ArrayDeque<String>();

. . .
for (String str : aDeque) {
    System.out.println(str);
}
```

**Iterator**

`Iterator`可用于各种数据类型列表的前向遍历。

```java
ArrayDeque<String> aDeque = new ArrayDeque<String>();
. . .
for (Iterator<String> iter = aDeque.iterator(); iter.hasNext();  ) {
    System.out.println(iter.next());
}
```

本教程中使用`ArrayDeque`类来实现`Deque`接口。[`ArrayDequeSample`](https://docs.oracle.com/javase/tutorial/collections/interfaces/examples/ArrayDequeSample.java)中提供了本教程中使用的示例的完整代码。`LinkedList`和`ArrayDeque`类都不支持多个线程的并发访问。

**并发 Deque 实现**

[`LinkedBlockingDeque`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/LinkedBlockingDeque.html) 类是`Deque`接口的并发实现。如果deque为空，那么诸如`takeFirst`和`takeLast`之类的方法会等到元素变为可用，然后检索并删除相同的元素。

### Wrapper 实现

包装器实现将所有实际工作委托给指定的集合，但在此集合提供的功能之上添加额外的功能。对于设计模式粉丝，这是装饰器模式的一个示例。虽然它看起来有点奇特，但它真的非常简单。

这些实现是匿名的，该库提供静态工厂方法，而不是提供公共类。所有这些实现都可以在 [`Collections`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html) 类中找到，它只包含静态方法。

**同步包装器**

同步包装器将自动同步（线程安全性）添加到任意集合。 六个核心集合接口 [`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html), [`Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html), [`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html), [`Map`](https://docs.oracle.com/javase/8/docs/api/java/util/Map.html),[`SortedSet`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedSet.html), 和 [`SortedMap`](https://docs.oracle.com/javase/8/docs/api/java/util/SortedMap.html) 中的每一个都有一个静态工厂方法。

```java
public static <T> Collection<T> synchronizedCollection(Collection<T> c);
public static <T> Set<T> synchronizedSet(Set<T> s);
public static <T> List<T> synchronizedList(List<T> list);
public static <K,V> Map<K,V> synchronizedMap(Map<K,V> m);
public static <T> SortedSet<T> synchronizedSortedSet(SortedSet<T> s);
public static <K,V> SortedMap<K,V> synchronizedSortedMap(SortedMap<K,V> m);
```

这些方法中的每一个都返回由指定集合备份的同步（线程安全）`Collection` 。为了保证串行访问，必须通过返回的集合完成对后备集合的所有访问。保证这一点的简单方法是不保留对后备集合的引用。使用以下技巧创建同步集合。

```java
List<Type> list = Collections.synchronizedList(new ArrayList<Type>());
```

以这种方式创建的集合与正常同步的集合（例如[`Vector`](https://docs.oracle.com/javase/8/docs/api/java/util/Vector.html)）一样具有线程安全性。

面对并发访问，用户必须在迭代时手动同步返回的集合。原因是迭代是通过对集合的多次调用来完成的，而这些操作必须组成一个单独的原子操作。以下是迭代包装器同步集合的习惯用法。

```java
Collection<Type> c = Collections.synchronizedCollection(myCollection);
synchronized(c) {
    for (Type e : c)
        foo(e);
}
```

如果使用显式迭代器，则必须从`synchronized`块中调用 `iterator` 方法。不遵循此建议可能会导致不确定的行为。迭代同步`Map`的`Collection`视图的习惯用法是类似的。当迭代任何`Collection`视图而不是在`Collection`视图本身上进行同步时，用户必须在同步`Map`上进行同步，如以下示例所示。

```java
Map<KeyType, ValType> m = Collections.synchronizedMap(new HashMap<KeyType, ValType>());
    ...
Set<KeyType> s = m.keySet();
    ...
// Synchronizing on m, not s!
synchronized(m) {
    while (KeyType k : s)
        foo(k);
}
```

使用包装器实现的一个小缺点是您无法执行包装实现的任何非接口操作。因此，例如，在前面的`List`示例中，您无法在包装的`ArrayList`上调用`ArrayList`的`ensureCapacity`操作。

**不可变包装器**

与为包装集合添加功能的同步包装器不同，不可修改的包装器可以消除功能。特别是，它们通过拦截将修改集合的操作并抛出`UnsupportedOperationException`来消除修改集合的能力。不可修改的包装器有两个主要用途，如下所示：

 - 在构建集合后使集合不可变。在这种情况下，最好不要维护对支持集合的引用。这绝对保证了不变性。
 - 允许某些客户端以只读方式访问您的数据结构。您保留对支持集合的引用，但分发对包装器的引用。通过这种方式，客户可以查看但不能修改，同时保持完全访问权限。

与同步包装器一样，六个核心`Collection`接口中的每一个都有一个静态工厂方法。

```java
public static <T> Collection<T> unmodifiableCollection(Collection<? extends T> c);
public static <T> Set<T> unmodifiableSet(Set<? extends T> s);
public static <T> List<T> unmodifiableList(List<? extends T> list);
public static <K,V> Map<K, V> unmodifiableMap(Map<? extends K, ? extends V> m);
public static <T> SortedSet<T> unmodifiableSortedSet(SortedSet<? extends T> s);
public static <K,V> SortedMap<K, V> unmodifiableSortedMap(SortedMap<K, ? extends V> m);
```

**受检查的接口包装器**

提供`Collections.checked`接口包装器以用于泛型集合。这些实现返回指定集合的动态类型安全视图，如果客户端尝试添加错误类型的元素，则会抛出`ClassCastException`。Java 语言中的泛型机制提供了编译时（静态）类型检查，但这种机制有可能被打破。动态类型安全的视图完全消除了这种可能性。

### 方便实现

本节描述了几种小型实现，当您不需要它们的全部功能时，它们比通用实现更方便，更高效。本节中的所有实现都是通过静态工厂方法而不是 `public` 类提供的。

**数组的列表视图**

[`Arrays.asList`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#asList-T...-) 方法返回其数组参数的`List`视图。对`List`的更改将写入数组，反之亦然。集合的大小是数组的大小，不能更改。如果在`List`上调用`add`或`remove`方法，将导致`UnsupportedOperationException`。

此实现的正常使用是作为基于数组和基于集合的API之间的桥梁。它允许您将数组传递给期望`Collection`或`List`的方法。但是，这种实现还有另一种用途。如果您需要固定大小的`List`，它比任何通用`List`实现更有效。这是习惯用法。

```java
List<String> list = Arrays.asList(new String[size]);
```

请注意，不保留对后备数组的引用。

**不可变的多重复制列表**

有时，您需要一个由同一元素的多个副本组成的不可变列表。`Collections.nCopies`方法返回这样的列表。该实现有两个主要用途。第一种是初始化新创建的`List`。例如，假设您想要一个最初由1,000个`null`元素组成的`ArrayList`。以下代码可以做到。

```java
List<Type> list = new ArrayList<Type>(Collections.nCopies(1000, (Type)null);
```

当然，每个元素的初始值不必为`null`。第二个主要用途是增加现有的`List`。例如，假设您要将69个字符串“fruit bat”添加到`List<String>`的末尾。目前尚不清楚你为什么要做这样的事情，但让我们假设你做了。以下是你如何做到的。

```java
lovablePets.addAll(Collections.nCopies(69, "fruit bat"));
```

通过使用带有索引和`Collection`的`addAll`形式，您可以将新元素添加到`List`的中间而不是结尾。

**不可变单例 Set**

有时您需要一个不可变的单例`Set`，它由一个指定的单个元素组成。[`Collections.singleton`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#singleton-T-) 方法返回这样的`Set`。此实现的一个用途是从`Collection`中删除所有出现的指定元素。

```java
c.removeAll(Collections.singleton(e));
```

相关的习惯用法从`Map`中删除映射到指定值的所有元素。例如，假设您有一个`Map` - `job` - 将人们映射到他们的工作范围，并假设您想要清除所有律师。以下代码将实现该操作。

```java
job.values().removeAll(Collections.singleton(LAWYER));
```

此实现的另一个用途是为编写为接受值集合的方法提供单个输入值。

**空 Set, List, 和 Map 常量**

[`Collections`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html) 类提供了返回空`Set`，`List`和`Map`的方法 -  [`emptySet`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#emptySet--), [`emptyList`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#emptyList--), 和 [`emptyMap`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#emptyMap--) 。这些常量的主要用途是当您不想提供任何值时作为采用值集合的方法的输入，如本示例所示。

```java
tourist.declarePurchases(Collections.emptySet());
```

### 小结

实现是用于存储集合的数据对象，它实现了 [Interfaces](https://docs.oracle.com/javase/tutorial/collections/interfaces/index.html) 课程中描述的接口。

Java Collections Framework提供了几个核心接口的通用实现：

* 对于`Set`接口，`HashSet`是最常用的实现。
* 对于`List`接口，`ArrayList`是最常用的实现。
* 对于`Map`接口，`HashMap`是最常用的实现。
* 对于`Queue`接口，`LinkedList`是最常用的实现。
* 对于`Deque`接口，`ArrayDeque`是最常用的实现。

每个通用实现都提供其接口中包含的所有可选操作。

Java Collections Framework还为需要非标准性能，使用限制或其他异常行为的情况提供了几种特殊用途的实现。

`java.util.concurrent`包中包含多个集合实现，这些实现是线程安全的，但不受单个排除锁的控制。

`Collections`类（与`Collection`接口相对）提供了对集合进行操作或返回集合的静态方法，这些方法称为包装器实现。

最后，有几种便利实现，当您不需要它们的全部功能时，它可以比通用实现更有效。通过静态工厂方法提供便捷实现。

## 算法

这里描述的*多态算法*是Java平台提供的可重用功能。所有这些都来自 [`Collections`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html) 类，所有这些都采用静态方法的形式， 第一个参数是要在其上执行操作的集合。Java平台提供的绝大多数算法都在 [`List`](https://docs.oracle.com/javase/8/docs/api/java/util/List.html) 实例上运行，但是有几个在任意 [`Collection`](https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html) 实例上运行。本节简要介绍以下算法：

- [排序](https://docs.oracle.com/javase/tutorial/collections/algorithms/index.html#sorting)
- [发牌](https://docs.oracle.com/javase/tutorial/collections/algorithms/index.html#shuffling)
- [常规数据操作](https://docs.oracle.com/javase/tutorial/collections/algorithms/index.html#rdm)
- [搜索](https://docs.oracle.com/javase/tutorial/collections/algorithms/index.html#searching)
- [组合](https://docs.oracle.com/javase/tutorial/collections/algorithms/index.html#composition)
- [寻找极值](https://docs.oracle.com/javase/tutorial/collections/algorithms/index.html#fev)

**排序**

`sort`算法重新排序`List`，使其元素按照排序关系按升序排列。提供了两种形式的操作。简单形式采用`List`并根据其元素'*自然排序*对其进行排序。如果您不熟悉自然排序的概念，请阅读 [Object Ordering](https://docs.oracle.com/javase/tutorial/collections/interfaces/order.html) 部分。

`sort`操作使用一种快速稳定的略微优化的*归并排序*算法：

 - **快速**：保证在 `n log(n)` 时间内运行，并且在接近有序的列表上运行得更快。经验测试显示它与高度优化的快速排序一样快。快速排序通常被认为比合并排序更快，但不稳定并且不保证 `n log(n)` 性能。
 - **稳定**：它不会重新排序相同的元素。如果您按照不同的属性对同一个列表重复排序，这一点很重要。如果邮件程序的用户按照邮寄日期对收件箱进行排序，然后按照发件人对其进行排序，则用户自然希望来自给定发件人的现在连续的邮件列表（仍然）将按邮寄日期排序。仅当采用第二种稳定排序时才能保证这一点。

以下 [`trivial program`](https://docs.oracle.com/javase/tutorial/collections/algorithms/examples/Sort.java) 以字典（按字母顺序）顺序打印出其参数。

```java
import java.util.*;

public class Sort {
    public static void main(String[] args) {
        List<String> list = Arrays.asList(args);
        Collections.sort(list);
        System.out.println(list);
    }
}
```

运行该程序：

```shell
% java Sort i walk the line
```

产生如下输出：

```
[i, line, the, walk]
```

该程序仅用于向您展示算法确实像它们看起来一样容易使用。

第二种形式的`sort`方法采用 [`Comparator`](https://docs.oracle.com/javase/8/docs/api/java/util/Comparator.html) 和`List`并使用该 `Comparator` 对列表元素进行排序。假设您想要以降序顺序打印出我们之前示例中的变位词组 - 首先是最大的变位词组。下面的示例向您展示了如何借助于`sort`方法的第二种形式来实现这一点。

回想一下，变位词组作为值存储在`Map`中，形式为`List`实例。修改后的打印代码遍历`Map`的值视图，将通过最小尺寸测试的每个`List`放入`List`的`List`中。然后代码使用期望`List`实例的`Comparator`对此`List`进行排序，并实现降序排序。最后，代码遍历排序的`List`，打印其元素（变位词组）。下面的代码替换了`Anagrams`示例中`main`方法末尾的打印代码。

```java
// Make a List of all anagram groups above size threshold.
List<List<String>> winners = new ArrayList<List<String>>();
for (List<String> l : m.values())
    if (l.size() >= minGroupSize)
        winners.add(l);

// Sort anagram groups according to size
Collections.sort(winners, new Comparator<List<String>>() {
    public int compare(List<String> o1, List<String> o2) {
        return o2.size() - o1.size();
    }});

// Print anagram groups.
for (List<String> l : winners)
    System.out.println(l.size() + ": " + l);
```

在 [The Map Interface](https://docs.oracle.com/javase/tutorial/collections/interfaces/map.html) 部分中同一个 [`same dictionary`](https://docs.oracle.com/javase/tutorial/collections/interfaces/examples/dictionary.txt) 上运行  [`the program`](https://docs.oracle.com/javase/tutorial/collections/algorithms/examples/Anagrams2.java) ，同样采用最小变位词组大小 8，产生以下输出。

```
12: [apers, apres, asper, pares, parse, pears, prase,
       presa, rapes, reaps, spare, spear]
11: [alerts, alters, artels, estral, laster, ratels,
       salter, slater, staler, stelar, talers]
10: [least, setal, slate, stale, steal, stela, taels,
       tales, teals, tesla]
9: [estrin, inerts, insert, inters, niters, nitres,
       sinter, triens, trines]
9: [capers, crapes, escarp, pacers, parsec, recaps,
       scrape, secpar, spacer]
9: [palest, palets, pastel, petals, plates, pleats,
       septal, staple, tepals]
9: [anestri, antsier, nastier, ratines, retains, retinas,
       retsina, stainer, stearin]
8: [lapse, leaps, pales, peals, pleas, salep, sepal, spale]
8: [aspers, parses, passer, prases, repass, spares,
       sparse, spears]
8: [enters, nester, renest, rentes, resent, tenser,
       ternes,��treens]
8: [arles, earls, lares, laser, lears, rales, reals, seral]
8: [earings, erasing, gainers, reagins, regains, reginas,
       searing, seringa]
8: [peris, piers, pries, prise, ripes, speir, spier, spire]
8: [ates, east, eats, etas, sate, seat, seta, teas]
8: [carets, cartes, caster, caters, crates, reacts,
       recast,��traces]
```

**发牌**

`shuffle`算法与`sort`相反，打乱了`List`中可能出现的任何顺序。也就是说，该算法基于来自随机源的输入重新排序`List`，假设使用理想的随机源，则所有可能的排列以相等的可能性发生。该算法在实现机会游戏时很有用。例如，它可以用于随机播放代表牌组的`Card`对象的`List`。此外，它对生成测试用例很有用。

此操作有两种形式：一种采用`List`并使用默认的随机源，另一种需要调用者提供 [Random](https://docs.oracle.com/javase/8/docs/api/java/util/Random.html) 对象用作随机源。该算法的代码用作 [`List` section](https://docs.oracle.com/javase/tutorial/collections/interfaces/list.html#shuffle) 中的示例。

**常规数据操作**

`Collections`类提供了五种算法，用于对`List`对象进行常规数据操作，所有这些都非常简单：

 - `reverse`  - 反转`List`中元素的顺序。
 - `fill`  - 用指定的值覆盖`List`中的每个元素。 此操作对于重新初始化`List`非常有用。
 - `copy`  - 接受两个参数，一个目标`List`和一个源`List`，并将源的元素复制到目的地，覆盖其内容。目标`List`必须至少与源一样长。如果它更长，目标`List`中的其余元素不受影响。
 - `swap`  - 将元素交换到`List`中的指定位置。
 - `addAll`  - 将所有指定的元素添加到`Collection`中。要添加的元素可以单独指定，也可以作为数组指定。

**搜索**

`binarySearch`算法在有序的`List`中搜索指定的元素。该算法有两种形式。第一个采用`List`和一个要搜索的元素（“搜索关键字”）两个参数。该形式假定`List`根据其元素的自然顺序按升序排序。除了`List`和搜索关键字之外，第二种形式还带有一个`Comparator`，并假定`List`按照指定的`Comparator`按升序排序。在调用`binarySearch`之前，`sort`算法可用于对`List`进行排序。

两种形式的返回值相同。如果`List`包含搜索关键字，则返回其索引。否则，则返回值为 `(-(插入点) - 1)`，其中插入点是将值插入`List`的点，或者第一个大于该值的元素的索引，或者`list.size()`，如果`List`中的所有元素都小于指定的值。当且仅当找到搜索关键字时，这个公认的丑陋公式保证返回值为`>= 0`。将布尔值`(found)`和整数`(index)`组合成一个`int`返回值基本上是一个不规范的做法。

以下习惯用法（可用于`binarySearch`操作的两种形式）查找指定的搜索关键字并将其插入适当的位置（如果它尚不存在）。

```java
int pos = Collections.binarySearch(list, key);
if (pos < 0)
   l.add(-pos-1, key);
```

**组合**

频率和不相交算法测试一个或多个 `Collections` 的组成的某些方面：

 - `frequency`  - 计算指定元素在指定集合中出现的次数
 - `disjoint` - 确定两个`Collections`是否不相交；也就是说，它们是否不包含任何共同的元素

**寻找极值**

`min`和`max`算法分别返回指定`Collection`中包含的最小和最大元素。这两种操作都有两种形式。简单形式只接受一个`Collection` 参数并根据元素的自然顺序返回最小（或最大）元素。第二种形式除了`Collection`之外还带有一个`Comparator` 参数，并根据指定的`Comparator`返回最小（或最大）元素。

## 自定义集合实现

许多程序员永远不需要实现自己的`Collections`类。您可以使用本章前面部分中描述的实现进行相当多的操作。但是，有一天你可能想编写自己的实现。借助Java平台提供的抽象实现，这很容易做到这一点。在我们讨论如何编写实现之前，让我们讨论一下为什么要编写一个自定义集合实现。

### 编写自定义集合实现的动机

以下列表说明了您可能希望实现的自定义集合的类型。它并非详尽无遗：

- **持久性：** 所有内置的`Collection`实现都驻留在主内存中，并在程序退出时消失。如果您希望下次程序启动时集合仍然存在，您可以通过在外部数据库上构建胶合代码来实现它。这样的集合可以由多个程序同时访问。
- **特定与应用：** 这是一个非常广泛的类别。一个例子是包含实时遥测数据的不可修改的 `Map` 。键可以表示位置，并且可以通过`get`操作从这些位置处的传感器读取值。
- **高性能，专用：** 许多数据结构利用受限制的使用来提供比通用实现更好的性能。例如，考虑一个包含多个连续相同元素值的`List`。在文本处理中经常出现的这种列表，可以是行程编码的 - 行程可以表示为包含重复元素和连续重复次数的对象。这个例子很有意思，因为它会影响性能的两个方面：它需要的空间更少，但是比`ArrayList`需要更多的时间。
- **高性能，通用：** Java Collections Framework的设计者试图为每个接口提供最佳的通用实现，但是可以使用很多数据结构，并且每天都会发明新的数据结构。也许你可以更快地拿出一些东西！
- **增强功能：** 假设您需要一个有效的包实现（也称为多重集）：一个 `Collection` ，它提供常量时间复杂度的包含元素检查，同时允许重复元素。在`HashMap`上实现这样的集合是相当简单的。
- **便利性：** 您可能希望获得除Java平台提供的便利之外的其他实现。例如，您可能经常需要表示连续范围的整数的`List`实例。
- **适配器：** 假设您使用的是具有自己的特殊集合API的旧API。您可以编写一个适配器实现，允许这些集合在Java Collections Framework中运行。适配器实现是一个很薄的胶合层，它包装一种类型的对象，并通过将后一种类型的操作转换为前者的操作，使它们的行为类似于另一种类型的对象。

### 如何编写自定义集合实现

编写自定义实现非常简单。Java Collections Framework提供了明确设计的抽象实现，以方便自定义实现。我们将从以下[`Arrays.asList`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#asList-T...-)实现的示例开始。

```java
public static <T> List<T> asList(T[] a) {
    return new MyArrayList<T>(a);
}

private static class MyArrayList<T> extends AbstractList<T> {

    private final T[] a;

    MyArrayList(T[] array) {
        a = array;
    }

    public T get(int index) {
        return a[index];
    }

    public T set(int index, T element) {
        T oldValue = a[index];
        a[index] = element;
        return oldValue;
    }

    public int size() {
        return a.length;
    }
}
```

信不信由你，这非常接近`java.util.Arrays`中包含的实现。就这么简单！您只要提供构造函数以及`get`，`set`和`size`方法，而`AbstractList`完成了所有其他方法。您可以自然获得`ListIterator`，批量操作，搜索操作，哈希值计算，比较和字符串表示。

假设您希望实现更快一点。抽象实现的API文档精确描述了每个方法的实现方式，因此您将知道要覆盖哪些方法以获得所需的性能。前面的实现的性能很好，但可以稍微改进一下。特别是，`toArray`方法迭代`List`，一次复制一个元素。鉴于内部表示，克隆数组的速度更快，更明智。

```java
public Object[] toArray() {
    return (Object[]) a.clone();
}
```

通过添加此覆盖以及更多类似的覆盖，此实现与`java.util.Arrays`中的实现完全相同。为了完全公开，使用其他抽象实现有点困难，因为你必须编写自己的迭代器，但它仍然不是那么困难。

下面的列表总结了抽象实现：

 -  [`AbstractCollection`](https://docs.oracle.com/javase/8/docs/api/java/util/AbstractCollection.html) - 既不是`Set`也不是`List`的`Collection`。您必须至少提供 `iterator` 和 `size` 方法。
 -  [`AbstractSet`](https://docs.oracle.com/javase/8/docs/api/java/util/AbstractSet.html) - 与`AbstractCollection`相同用途的`Set`。
 -  [`AbstractList`](https://docs.oracle.com/javase/8/docs/api/java/util/AbstractList.html) - 由随机访问数据存储（例如数组）作为后备的 `List` 。您必须至少提供 `positional access` 方法（`get` 以及可选的, `set`, `remove`, and `add`）和 `size` 方法。抽象类负责listIterator（和 `iterator`）。
 -  [`AbstractSequentialList`](https://docs.oracle.com/javase/8/docs/api/java/util/AbstractSequentialList.html) - 由顺序访问数据存储（例如链表）作为后备的`List`。您至少必须提供`listIterator`和`size`方法。抽象类负责位置访问方法。（这与`AbstractList`相反。）
 -  [`AbstractQueue`](https://docs.oracle.com/javase/8/docs/api/java/util/AbstractQueue.html) - 您必须至少提供`offer`，`peek`，`poll`和`size`方法以及支持`remove`的`iterator`。
 -  [`AbstractMap`](https://docs.oracle.com/javase/8/docs/api/java/util/AbstractMap.html) - 一个`Map`。您至少必须提供`entrySet`视图。这通常使用`AbstractSet`类实现。如果`Map`是可修改的，则还必须提供`put`方法。

编写自定义实现的过程如下：

1. 从前面的列表中选择适当的抽象实现类。
2. 提供类的所有抽象方法的实现。如果您的自定义集合是可修改的，则还必须覆盖一个或多个具体方法。抽象实现类的API文档将告诉您要覆盖哪些方法。
3. 测试并在必要时调试实现。您现在有一个可用的自定义集合实现。
4. 如果您担心性能，请阅读您继承其实现的所有方法的抽象实现类的API文档。如果有任何方法看起来太慢，请覆盖它们。如果覆盖任何方法，请确保在覆盖之前和之后测量方法的性能。您在调整性能方面付出的努力应该取决于实现将获得多少使用以及对其使用性能的关键程度。 （通常最好省略此步骤。）

## 互操作性

本章节中，你将学到关于互操作性的以下两个方便：

- [兼容性](https://docs.oracle.com/javase/tutorial/collections/interoperability/compatibility.html) ：本小节描述了如何集合如何使用老版本的集合API工作，这些旧集合API早于`Collection`被添加到Java平台。
- [API 设计](https://docs.oracle.com/javase/tutorial/collections/interoperability/api-design.html) ：本小节描述了如何设计新的API，以便它们可以相互无缝地互操作。

### 兼容性

Java Collections Framework旨在确保 [核心集合接口](https://docs.oracle.com/javase/tutorial/collections/interfaces/index.html) 与用于在Java平台早期版本中表示集合的类型之间的完全互操作性： [`Vector`](https://docs.oracle.com/javase/8/docs/api/java/util/Vector.html), [`Hashtable`](https://docs.oracle.com/javase/8/docs/api/java/util/Hashtable.html), [array](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html), 和 [`Enumeration`](https://docs.oracle.com/javase/8/docs/api/java/util/Enumeration.html)。在本节中，您将学习如何将旧集合转换为Java集合框架集合，反之亦然。

**向上兼容**

假设您正在使用一个API，该API返回旧集合，它与另一个需要实现集合接口的对象的API一起工作。为了使两个API顺利地互操作，您必须将旧版集合转换为现代集合。幸运的是，Java Collections Framework使这很容易。

假设旧API返回一个对象数组，而新API需要一个`Collection`。Collections Framework有一个方便的实现，允许将一组对象视为`List`。您使用`Arrays.asList`将数组传递给任何需要`Collection`或`List`的方法。

```java
Foo[] result = oldMethod(arg);
newMethod(Arrays.asList(result));
```

如果旧的API返回`Vector`或`Hashtable`，则根本没有工作要做，因为`Vector`被改进以实现`List`接口，并且`Hashtable`被改进以实现`Map`。因此，`Vector`可以直接传递给任何使用`Collection`或`List`的方法。

```java
Vector result = oldMethod(arg);
newMethod(result);
```

类似地，`Hashtable`可以直接传递给任何使用`Map`的方法。

```java
Hashtable result = oldMethod(arg);
newMethod(result);
```

不太常见的是，API可能会返回表示对象集合的`Enumeration`。`Collections.list`方法将 `Enumeration` 转换为`Collection`。

```java
Enumeration e = oldMethod(arg);
newMethod(Collections.list(e));
```

**向下兼容**

假设您正在使用一个API，该API返回现代集合，并与与另一个要求您传入旧集合的API一起工作。要使两个API平滑地互操作，您必须将现代集合转换为旧集合。同样，Java Collections Framework使这一过程变得简单。

假设新API返回一个`Collection`，旧API需要一个`Object`数组。您可能已经意识到，`Collection`接口包含为此情况明确设计的`toArray`方法。

```java
Collection c = newMethod();
oldMethod(c.toArray());
```

如果旧API需要`String`（或其他类型）数组而不是`Object`数组，该怎么办？你只需使用另一种形式的`toArray`--一个在输入上采用数组的形式。

```java
Collection c = newMethod();
oldMethod((String[]) c.toArray(new String[0]));
```

如果旧API需要`Vector`，则标准集合构造函数会派上用场。

```java
Collection c = newMethod();
oldMethod(new Vector(c));
```

旧API需要`Hashtable`的情况类似地处理。

```java
Map m = newMethod();
oldMethod(new Hashtable(m));
```

最后，如果旧API需要`Enumeration`，您会怎么做？这种情况并不常见，但它确实经常发生，[`Collections.enumeration`](https://docs.oracle.com/javase/8/docs/api/java/util/Collections.html#enumeration-java.util.Collection-) 方法被用来处理它。这是一个静态工厂方法，它接受`Collection`并基于`Collection`的元素返回`Enumeration`。

```java
Collection c = newMethod();
oldMethod(Collections.enumeration(c));
```

### API 设计

在这个简短但重要的部分中，您将学习一些简单的指导原则，使您的API能够与遵循这些指南的所有其他API无缝地互操作。从本质上讲，这些规则定义了在收集合世界中成为一个好的“公民”需要什么。

**参数**

如果您的API包含需要输入集合的方法，那么将相关参数类型声明为集合接口类型之一是至关重要的。永远不要使用实现类型，因为这会破坏基于接口的集合框架的目的，即允许操作集合而不考虑实现细节。

此外，您应该始终使用最不具体的类型。例如，如果`Collection`可以，则不需要`List`或`Set`。并不是你永远不应该在输入时需要`List`或`Set` ；如果方法依赖于其中一个接口的属性，则这样做是正确的。例如，Java平台提供的许多算法都需要输入`List`，因为它们依赖于列表的排序事实。但是，作为一般规则，输入时使用的最佳类型是最常用的接口类型：`Collection` 和 `Map`。

----

**警告：** 永远不要定义您自己的专用集合类，并在输入时需要此类的对象。因为这样做，您将失去Java Collections Framework提供的所有好处。

----

**返回值**

使用返回值比使用输入参数更灵活。返回实现或扩展其中一个集合接口的任何类型的对象都可以。这可以是接口之一，也可以是扩展或实现这些接口之一的专用类型。

例如，可以想象一个名为`ImageList`的图像处理包，它返回实现`List`的新类的对象。除了`List`操作之外，`ImageList`还可以支持任何特定于应用程序的操作。例如，它可能提供`indexImage`操作，该操作返回包含`ImageList`中每个图形的缩略图图像的图像。值得注意的是，即使API在输出上提供了`ImageList`实例，它也应该在输入上接受任意`Collection`（或者可能是`List`）实例。

从某种意义上说，返回值应该具有输入参数的相反行为：最好返回最具体的适用集合接口，而不是最常见的。例如，如果您确定要始终返回`SortedMap`，则应该为相关方法提供`SortedMap`的返回类型而不是`Map`。`SortedMap`实例比普通的`Map`实例更耗时，而且功能更强大。鉴于您的模块已经投入时间来构建`SortedMap`，因此让用户访问其增强的功能是很有意义的。此外，用户将能够将返回的对象传递给需要`SortedMap`的方法，以及接受任何`Map`的方法。

**遗留 APIs**

目前有很多API可以定义自己的临时集合类型。虽然这很不幸，但鉴于Java平台的最初两个主要版本中没有Collections Framework，这是既定的事实。假设您拥有其中一个API，这就是你能做的。

如果可能，请改进旧版集合类型以实现其中一个标准集合接口。然后，您返回的所有集合将与其他基于集合的API平滑地互操作。如果这是不可能的（例如，因为一个或多个预先存在的类型签名与标准集合接口冲突），请定义一个适配器类，它包装您的一个旧集合对象，使其可用作标准集合。 （`Adapter`类是 [自定义实现](https://docs.oracle.com/javase/tutorial/collections/custom-implementations/index.html) 的示例。）

如果可能，使用遵循输入准则的新调用来改进API，以接受标准集合接口的对象。此类调用可以与采用旧版集合类型的调用共存。如果这是不可能的，请为遗留类型提供构造函数或静态工厂，该构造函数或静态工厂接受其中一个标准接口的对象，并返回包含相同元素（或映射）的旧集合。这些方法中的任何一种都允许用户将任意集合传递到您的API中。

# lambda 表达式

在新手教程里有，不再重复。

# 聚合操作

在集合部分里有，不再重复。

# 将程序打包成 JAR 文件

Java™Archive（JAR）文件格式使您可以将多个文件打包到一个归档文件中。通常，JAR文件包含与applet和应用程序关联的类文件和辅助资源。

JAR 文件格式提供了很多好处：

- *安全*: 你可以对 JAR 文件内容进行数字签名。然后，识别出您的签名的用户可以选择授予您不具备的软件安全权限。
- *缩短下载时间*: 如果您的applet打包在JAR文件中，则可以在单个HTTP事务中将applet的类文件和相关资源下载到浏览器，而无需为每个文件打开新连接。
- *压缩*: JAR格式允许您压缩文件以实现高效存储。
- *打包为扩展插件*: 扩展框架提供了一种向Java核心平台添加功能的方法，JAR文件格式定义了扩展的打包方式。通过使用JAR文件格式，您也可以将软件转换为扩展插件。
- *包密封*: 可以选择密封存储在JAR文件中的包，以便包可以强制实现版本一致性。在JAR文件中封装包意味着必须在同一个JAR文件中找到该包中定义的所有类。
- *包版本化*: JAR文件可以保存有关其包含的文件的数据，例如提供者和版本信息。
- *可移植性*: 处理JAR文件的机制是Java平台核心API的标准组成部分。

本课程包含四个章节：

**[使用 JAR 文件: 基础](https://docs.oracle.com/javase/tutorial/deployment/jar/basicsindex.html)**

本节介绍如何执行基本JAR文件操作，以及如何运行打包在JAR文件中的软件。

**[使用 Manifest 文件: 基础](https://docs.oracle.com/javase/tutorial/deployment/jar/manifestindex.html)**

本节介绍清单文件以及如何自定义它们，以便您可以执行诸如密封包和设置应用程序入口点之类的操作。

**[签名和验证 JAR 文件](https://docs.oracle.com/javase/tutorial/deployment/jar/signindex.html)**

本节介绍如何对JAR文件进行数字签名并验证JAR文件的签名。

**[使用 JAR 相关 API](https://docs.oracle.com/javase/tutorial/deployment/jar/apiindex.html)**

本节介绍Java平台的一些JAR处理功能。JAR文件格式是Java平台扩展机制的重要组成部分。您可以在本教程的 [扩展机制](https://docs.oracle.com/javase/tutorial/ext/index.html) 中了解有关JAR文件的更多信息。

**附加参考**

Java Development Kit（JDK）的文档包含有关Jar工具的信息：

- [Java Archive (JAR) Files Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/jar/index.html)
- [JAR File Specification](https://docs.oracle.com/javase/8/docs/technotes/guides/jar/jar.html)

## 使用 JAR 文件：基础

JAR文件以ZIP文件格式打包，因此您可以将它们用于无损数据压缩，归档，解压缩和归档解包等任务。这些任务是JAR文件最常见的用途，您只需使用这些基本功能即可享受许多JAR文件优势。

如果您想利用JAR文件格式提供的高级功能（如电子签名），您首先需要熟悉基本操作。

要使用JAR文件执行基本任务，请使用Java Archive Tool作为Java Development Kit（JDK）的一部分提供。因为使用`jar`命令调用Java Archive工具，所以本教程将其称为“Jar工具”。

作为本节中介绍的一些主题的概要和预览，下表总结了常见的JAR文件操作：

| Operation                                | Command                                  |
| ---------------------------------------- | ---------------------------------------- |
| To create a JAR file                     | `jar cf *jar-file input-file(s)*`        |
| To view the contents of a JAR file       | `jar tf *jar-file*`                      |
| To extract the contents of a JAR file    | `jar xf *jar-file*`                      |
| To extract specific files from a JAR file | `jar xf *jar-file archived-file(s)*`     |
| To run an application packaged as a JAR file (requires the [`Main-class`](https://docs.oracle.com/javase/tutorial/deployment/jar/appman.html) manifest header) | `java -jar *app.jar*`                    |
| To invoke an applet packaged as a JAR file | `<applet code=*AppletClassName.class*         archive="*JarFileName.jar*"         width=*width* height=*height*> </applet> ` |

本节介绍如何执行最常见的JAR文件操作，并提供每个基本功能的示例：

**[创建 JAR 文件](https://docs.oracle.com/javase/tutorial/deployment/jar/build.html)**

本节介绍如何使用Jar工具将文件和目录打包到JAR文件中。

**[查看 JAR 文件内容](https://docs.oracle.com/javase/tutorial/deployment/jar/view.html)**

您可以显示JAR文件的目录，以查看它包含的内容，而无需实际解压缩JAR文件。

**[解压 JAR 文件](https://docs.oracle.com/javase/tutorial/deployment/jar/unpack.html)**

您可以使用Jar工具解压缩JAR文件。在提取文件时，Jar工具会复制所需的文件并将它们写入当前目录，从而重现文件在存档中的目录结构。

**[升级 JAR 文件](https://docs.oracle.com/javase/tutorial/deployment/jar/update.html)**

本节介绍如何通过修改其清单或添加文件来更新现有JAR文件的内容。

**[运行打包成 JAR 文件的软件](https://docs.oracle.com/javase/tutorial/deployment/jar/run.html)**

本节介绍如何调用和运行JAR文件中打包的applet和应用程序。

**附加参考**

JDK的文档包括Jar工具的参考页面：

- [Jar tool reference for the Windows platform](https://docs.oracle.com/javase/8/docs/technotes/tools/windows/jar.html)
- [Jar tool reference for UNIX-based platforms](https://docs.oracle.com/javase/8/docs/technotes/tools/unix/jar.html)

### 创建 JAR 文件

创建 JAR 文件的基本命令格式是：

```shell
jar cf jar-file input-file(s)
```

此命令中使用的选项和参数是：

 - `c`选项表示您要*创建* JAR文件。
 - `f`选项表示您希望输出重定向到*文件*而不是`stdout`。
 - `jar-file`是您希望生成的JAR文件具有的名称。您可以使用任何文件名作为JAR文件。按照惯例，JAR文件名被赋予`.jar`扩展名，但这不是必需的。
 - `input-file（s）`参数是一个以空格分隔的列表，其中包含您要包含在JAR文件中的一个或多个文件。`input-file（s）`参数可以包含通配符`*`符号。如果任何“输入文件”是目录，则这些目录的内容将以递归方式添加到JAR存档中。

`c`和`f`选项可以按任何顺序出现，但它们之间不能有任何空格。

此命令将生成压缩的JAR文件并将其放在当前目录中。 该命令还将为JAR存档生成 [默认清单文件](https://docs.oracle.com/javase/tutorial/deployment/jar/defman.html) 。

----

**注意：** JAR文件中的元数据（例如清单的条目名称，注释和内容）必须以UTF8编码。

----

您可以将以下任何附加选项添加到基本命令的`cf`选项中：

| Option     | Description                              |
| ---------- | ---------------------------------------- |
| `v`        | 在构建JAR文件时，在`stdout`上生成冗长的详细输出。详细输出在每个文件被添加到JAR文件中时告诉您它的名称。 |
| `0` (zero) | 表示您不希望压缩JAR文件。                           |
| `M`        | 表示不应生成默认清单文件。                            |
| `m`        | 用于包括现有清单文件中的清单信息。 使用此选项的格式为：`jar cmf jar-file  existing-manifest  input-file(s)`。参见 [修改清单文件](https://docs.oracle.com/javase/tutorial/deployment/jar/modman.html) 获取有关此选项的更多信息。**警告：** 清单必须以新行或回车结束。如果不以新行或回车结束，则不会正确解析最后一行。 |
| `-C`       | 在执行命令期间更改目录。请参阅下面的示例。                    |

------

**注意：** 创建JAR文件时，创建时间存储在JAR文件中。因此，即使JAR文件的内容没有更改，当您多次创建JAR文件时，生成的文件也不完全相同。在构建环境中使用JAR文件时，应该注意这一点。建议您使用清单文件中的版本控制信息而不是创建时间来控制JAR文件的版本。请参阅 [设置包版本信息](https://docs.oracle.com/javase/tutorial/deployment/jar/packageman.html) 部分。

----

**例子**

我们来看一个例子。一个简单的`TicTacToe`小程序。您可以通过从 [Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 下载JDK演示和示例包来查看此applet的源代码。此演示包含具有以下结构的类文件，音频文件和图像：

![TicTacToe folder Hierarchy](https://docs.oracle.com/javase/tutorial/figures/deployment/jar/ticTacToeJar.gif)

`audio`和`images`子目录包含applet使用的声音文件和GIF图像。

在线下载整个教程时，您可以从*jar/examples*目录中获取所有这些文件。要将此演示打包到名为`TicTacToe.jar`的单个JAR文件中，您可以从`TicTacToe`目录中运行此命令：

```
jar cvf TicTacToe.jar TicTacToe.class audio images
```

`audio`和`images`参数表示目录，因此Jar工具将递归地将它们及其内容放在JAR文件中。生成的JAR文件`TicTacToe.jar`将放在当前目录中。因为该命令使用`v`选项进行详细输出，所以在运行命令时会看到与此输出类似的内容：

```
adding: TicTacToe.class (in=3825) (out=2222) (deflated 41%)
adding: audio/ (in=0) (out=0) (stored 0%)
adding: audio/beep.au (in=4032) (out=3572) (deflated 11%)
adding: audio/ding.au (in=2566) (out=2055) (deflated 19%)
adding: audio/return.au (in=6558) (out=4401) (deflated 32%)
adding: audio/yahoo1.au (in=7834) (out=6985) (deflated 10%)
adding: audio/yahoo2.au (in=7463) (out=4607) (deflated 38%)
adding: images/ (in=0) (out=0) (stored 0%)
adding: images/cross.gif (in=157) (out=160) (deflated -1%)
adding: images/not.gif (in=158) (out=161) (deflated -1%)
```

您可以从此输出中看到JAR文件`TicTacToe.jar`已被压缩。Jar工具默认压缩文件。您可以使用`0`（零）选项关闭压缩功能，以便命令如下所示：

```
jar cvf0 TicTacToe.jar TicTacToe.class audio images
```

例如，您可能希望避免压缩，以提高浏览器加载JAR文件的速度。通常可以比压缩文件更快地加载未压缩的JAR文件，因为消除了在加载期间解压缩文件的需要。但是，需要权衡的是，对于较大的未压缩文件，网络上的下载时间可能会更长。

Jar工具将接受使用通配符`*`符号的参数。只要`TicTacToe`目录中没有任何不需要的文件，您就可以使用此替代命令来构造JAR文件：

```
jar cvf TicTacToe.jar *
```

尽管详细输出未指示它，但Jar工具会自动将清单文件添加到JAR存档中，路径名为“META-INF/MANIFEST.MF”。有关清单文件的信息，请参阅 [使用清单文件：基础知识](https://docs.oracle.com/javase/tutorial/deployment/jar/manifestindex.html) 部分。

在上面的示例中，归档中的文件保留了它们的相对路径名和目录结构。Jar工具提供`-C`选项，您可以使用该选项创建一个JAR文件，其中不保留已归档文件的相对路径。它以TAR的`-C`选项为模型。

例如，假设您想将TicTacToe演示使用的音频文件和gif图像放入JAR文件中，并且您希望所有文件都位于顶层，没有目录层次结构。你可以通过从`images`和`audio`目录的父目录发出这个命令来实现这个目的：

```
jar cf ImageAudio.jar -C images . -C audio .
```

此命令的`-C images`部分指示Jar工具转到`images`目录，后面的`.`指示Jar工具归档该目录的所有内容。然后命令的`-C audio .`部分对`audio`目录执行相同的操作。生成的JAR文件将具有以下目录：

```
META-INF/MANIFEST.MF
cross.gif
not.gif
beep.au
ding.au
return.au
yahoo1.au
yahoo2.au
```

相反，假设您使用的命令不使用`-C`选项：

```
jar cf ImageAudio.jar images audio
```

生成的JAR文件将具有以下目录：

```
META-INF/MANIFEST.MF
images/cross.gif
images/not.gif
audio/beep.au
audio/ding.au
audio/return.au
audio/yahoo1.au
audio/yahoo2.au
```

### 浏览 JAR 文件内容

浏览 JAR 文件内容的命令的基本格式如下：

```
jar tf jar-file
```

让我们看看这个命令中使用的选项和参数：

 -  `t`选项表示您要查看JAR文件的目录。
 -  `f`选项表示在命令行中指定要查看其内容的JAR文件。
 -  `jar-file`参数是要查看其内容的JAR文件的路径和名称。

`t`和`f`选项可以按任意顺序出现，但它们之间不能有任何空格。

此命令将向 `stdout` 显示JAR文件的目录。

您可以选择添加详细选项`v`，以在输出中生成有关文件大小和上次修改日期的其他信息。

**例子**

让我们使用Jar工具列出我们在上一节中创建的`TicTacToe.jar`文件的内容：

```
jar tf TicTacToe.jar
```

此命令将JAR文件的内容显示到`stdout`：

```
META-INF/MANIFEST.MF
TicTacToe.class
audio/
audio/beep.au
audio/ding.au
audio/return.au
audio/yahoo1.au
audio/yahoo2.au
images/
images/cross.gif
images/not.gif
```

JAR文件包含`TicTacToe`类文件以及音频和图像目录，如预期的那样。输出还显示JAR文件包含默认清单文件`META-INF/MANIFEST.MF`，该文件由JAR工具自动放置在归档中。有关更多信息，请参阅 [了解默认清单](https://docs.oracle.com/javase/tutorial/deployment/jar/defman.html) 部分。

无论您使用的平台或操作系统如何，所有路径名都以正斜杠显示。JAR文件中的路径始终是相对的; 例如，你永远不会看到以`C:`开头的路径。

如果使用`v`选项，JAR工具将显示其他信息：

```
jar tvf TicTacToe.jar
```

例如，TicTacToe JAR文件的详细输出看起来类似于：

```
    68 Thu Nov 01 20:00:40 PDT 2012 META-INF/MANIFEST.MF
   553 Mon Sep 24 21:57:48 PDT 2012 TicTacToe.class
  3708 Mon Sep 24 21:57:48 PDT 2012 TicTacToe.class
  9584 Mon Sep 24 21:57:48 PDT 2012 TicTacToe.java
     0 Mon Sep 24 21:57:48 PDT 2012 audio/
  4032 Mon Sep 24 21:57:48 PDT 2012 audio/beep.au
  2566 Mon Sep 24 21:57:48 PDT 2012 audio/ding.au
  6558 Mon Sep 24 21:57:48 PDT 2012 audio/return.au
  7834 Mon Sep 24 21:57:48 PDT 2012 audio/yahoo1.au
  7463 Mon Sep 24 21:57:48 PDT 2012 audio/yahoo2.au
   424 Mon Sep 24 21:57:48 PDT 2012 example1.html
     0 Mon Sep 24 21:57:48 PDT 2012 images/
   157 Mon Sep 24 21:57:48 PDT 2012 images/cross.gif
   158 Mon Sep 24 21:57:48 PDT 2012 images/not.gif
```

### 解压 JAR 文件内容

用于提取JAR文件内容的基本命令是：

```
jar xf jar-file [archived-file(s)]
```

让我们看一下这个命令中的选项和参数：

 -  `x`选项表示您要从JAR存档中提取文件。
 -  `f`选项表示要从中提取文件的JAR文件在命令行中指定，而不是通过`stdin`指定。
 -  `jar-file`参数是从中提取文件的JAR文件的文件名（或路径和文件名）。
 -  `archived-file(s)`是一个可选参数，由要从存档中提取的文件的空格分隔列表组成。如果此参数不存在，Jar工具将提取存档中的所有文件。

像往常一样，`x`和`f`选项在命令中出现的顺序无关紧要，但它们之间不能有空格。

在提取文件时，Jar工具会复制所需的文件并将它们写入当前目录，从而重现文件在存档中的目录结构。原始JAR文件保持不变。

----

**警告：** 当它提取文件时，Jar工具将覆盖与提取的文件具有相同路径名的任何现有文件。

----

**例子**

让我们从前面部分中使用的TicTacToe JAR文件中提取一些文件。回想一下`TicTacToe.jar`的内容是：

```
META-INF/MANIFEST.MF
TicTacToe.class
TicTacToe.class
TicTacToe.java
audio/
audio/beep.au
audio/ding.au
audio/return.au
audio/yahoo1.au
audio/yahoo2.au
example1.html
images/
images/cross.gif
images/not.gif
```

假设您要提取`TicTacToe`类文件和`cross.gif`图像文件，为此，您可以使用此命令：

```
jar xf TicTacToe.jar TicTacToe.class images/cross.gif
```

这个命令做了两件事：

 - 它将`TicTacToe.class`的副本放在当前目录中。
 - 它创建目录 `images`（如果它尚不存在），并在其中放置`cross.gif`的副本。

原始的TicTacToe JAR文件保持不变。

可以以相同的方式从JAR文件中提取所需的文件。当命令未指定要提取的文件时，Jar工具将提取存档中的所有文件。例如，您可以使用以下命令提取TicTacToe存档中的所有文件：

```
jar xf TicTacToe.jar
```

### 升级 JAR 文件

Jar工具提供了一个`u`选项，您可以通过该选项修改其清单或添加文件来更新现有JAR文件的内容。

添加文件的基本命令具有以下格式：

```
jar uf jar-file input-file(s)
```

在此命令中：

 -  `u`选项表示您要更新现有JAR文件。
 -  `f`选项表示要在命令行上指定要更新的JAR文件。
 -  `jar-file`是要更新的现有JAR文件。
 -  `input-file(s)`是一个以空格分隔的列表，其中包含要添加到JAR文件的一个或多个文件。

归档中已存在的文件与添加的文件具有相同的路径名将被覆盖。

创建新的JAR文件时，您可以选择使用`-C`选项来指示目录的更改。有关更多信息，请参阅 [创建JAR文件](https://docs.oracle.com/javase/tutorial/deployment/jar/build.html) 部分。

**例子**

回想 `TicTacToe.jar` 包含以下内容：

```
META-INF/MANIFEST.MF
TicTacToe.class
TicTacToe.class
TicTacToe.java
audio/
audio/beep.au
audio/ding.au
audio/return.au
audio/yahoo1.au
audio/yahoo2.au
example1.html
images/
images/cross.gif
images/not.gif
```

假设您要将文件`images/new.gif`添加到JAR文件中。您可以通过从`images`目录的父目录发出以下命令来完成此操作：

```
jar uf TicTacToe.jar images/new.gif
```

修订后的JAR文件将具有以下目录：

```
META-INF/MANIFEST.MF
TicTacToe.class
TicTacToe.class
TicTacToe.java
audio/
audio/beep.au
audio/ding.au
audio/return.au
audio/yahoo1.au
audio/yahoo2.au
example1.html
images/
images/cross.gif
images/not.gif
images/new.gif
```

您可以在执行命令期间使用`-C`选项“更改目录”。 例如：

```
jar uf TicTacToe.jar -C images new.gif
```

在将`new.gif`添加到JAR文件之前，此命令将转向`images`目录。当`new.gif`添加到存档时，`images`目录不会包含在`new.gif`的路径名中，从而产生如下内容的目录：

```
META-INF/MANIFEST.MF
META-INF/MANIFEST.MF
TicTacToe.class
TicTacToe.class
TicTacToe.java
audio/
audio/beep.au
audio/ding.au
audio/return.au
audio/yahoo1.au
audio/yahoo2.au
example1.html
images/
images/cross.gif
images/not.gif
new.gif
```

### 运行打包为 JAR 的软件

既然您已经学会了如何创建JAR文件，那么如何实际运行您打包的代码？考虑以下情况：

 - 您的JAR文件包含要在浏览器中运行的applet。
 - 您的JAR文件包含要从命令行启动的应用程序。
 - 您的JAR文件包含要用作扩展插件的代码。

本节将介绍前两种情况。[扩展机制教程](https://docs.oracle.com/javase/tutorial/ext/index.html) 涵盖了JAR文件作为扩展的使用。

**Applets 打包到 JAR 文件中**

要从HTML文件启动任何applet以在浏览器中运行，请使用`applet`标记。更多有关信息，请参阅 [Java Applets](https://docs.oracle.com/javase/tutorial/deployment/applet/index.html) 课程。如果将applet打包为JAR文件，则唯一需要做的就是使用*archive*参数指定JAR文件的相对路径。

例如，使用TicTacToe演示小程序。 HTML文件中显示applet的`applet`标记可以标记为：

```html
<applet code=TicTacToe.class 
        width="120" height="120">
</applet>
```

如果TicTacToe演示打包在名为`TicTacToe.jar`的JAR文件中，则可以通过添加 `archive` 参数来修改`applet`标记：

```html
<applet code=TicTacToe.class 
        archive="TicTacToe.jar"
        width="120" height="120">
</applet>
```

`archive`参数指定包含`TicTacToe.class`的JAR文件的相对路径。对于此示例，假定JAR文件和HTML文件位于同一目录中。如果不是，则必须在`archive`参数的值中包含JAR文件的相对路径。例如，如果JAR文件是名为`applets`的目录中HTML文件下面的一个目录，则`applet`标记将如下所示：

```html
<applet code=TicTacToe.class 
        archive="applets/TicTacToe.jar"
        width="120" height="120">
</applet>
```

**作为应用的 JAR 文件**

您可以使用Java启动程序（java命令）运行JAR打包的应用程序。基本命令是：

```
java -jar jar-file
```

`-jar`标志告诉启动器应用程序是以JAR文件格式打包的。您只能指定一个JAR文件，该文件必须包含所有特定于应用程序的代码。

在执行此命令之前，请确保运行时环境具有有关JAR文件中哪个类是应用程序入口点的信息。

要指示哪个类是应用程序的入口点，必须将一个`Main-Class`标头添加到JAR文件的清单中。该标头采用以下形式：

```
Main-Class: classname
```

标头的值`classname`是应用程序入口点的类的名称。

有关更多信息，请参阅 [设置应用程序的入口点](https://docs.oracle.com/javase/tutorial/deployment/jar/appman.html) 部分。

在清单文件中设置`Main-Class`后，您可以从命令行运行该应用程序：

```
java -jar app.jar
```

要从另一个目录中的JAR文件运行应用程序，必须指定该目录的路径： `java -jar path/app.jar`

## 使用清单文件：基础

JAR文件支持广泛的功能，包括电子签名，版本控制，封装密封等。什么赋予JAR文件这种多功能性？答案是JAR文件的清单。

清单是一个特殊文件，可以包含有关JAR文件中打包的文件的信息。通过定制清单包含的此“元”信息，您可以启用JAR文件以满足各种用途。

本课将解释清单文件的内容，并向您展示如何使用它，并提供基本功能的示例：

**[理解默认清单](https://docs.oracle.com/javase/tutorial/deployment/jar/defman.html)**

创建JAR文件时，会自动创建默认清单。本节介绍默认清单。

**[修改清单文件](https://docs.oracle.com/javase/tutorial/deployment/jar/modman.html)**

本节介绍修改清单文件的基本方法。后面的部分演示了您可能想要进行的具体修改。

**[设置应用入口点](https://docs.oracle.com/javase/tutorial/deployment/jar/appman.html)**

本节介绍如何使用清单文件中的`Main-Class`标头设置应用程序的入口点。

**[将类添加到 JAR  文件类路径中](https://docs.oracle.com/javase/tutorial/deployment/jar/downman.html)**

本节介绍如何在清单文件中使用`Class-Path`标头，以便在运行applet或应用程序时将其他JAR文件中的类添加到类路径中。

**[设定包版本信息](https://docs.oracle.com/javase/tutorial/deployment/jar/packageman.html)**

本节介绍如何在清单文件中使用程序包版本标头。

**[将包密封到 JAR 文件中](https://docs.oracle.com/javase/tutorial/deployment/jar/sealman.html)**

本节介绍如何通过修改清单文件来密封JAR文件中的包。

**[利用清单属性增强安全性](https://docs.oracle.com/javase/tutorial/deployment/jar/secman.html)**

本节介绍如何使用清单属性来提高applet或Java Web Start应用程序的安全性。

**附加信息**

[清单格式的规范](https://docs.oracle.com/javase/8/docs/technotes/guides/jar/jar.html#JARManifest) 是在线JDK文档的一部分。

### 理解默认清单

创建JAR文件时，它会自动禅城默认清单文件。归档中只能有一个清单文件，并且它始终具有路径名

```
META-INF/MANIFEST.MF
```

创建JAR文件时，默认清单文件只包含以下内容：

```
Manifest-Version: 1.0
Created-By: 1.7.0_06 (Oracle Corporation)
```

这些行显示清单的条目采用"header: value" 对的形式。标头的名称通过冒号与其值分隔。默认清单符合清单规范的1.0版，由JDK的1.7.0_06版本创建。

清单还可以包含有关存档中打包的其他文件的信息。究竟应该在清单中记录哪些文件信息取决于您打算如何使用JAR文件。默认清单不会假设它应该记录哪些关于其他文件的信息。

摘要信息不包含在默认清单中。要了解有关摘要和签名的更多信息，请参阅 [签名和验证JAR文件](https://docs.oracle.com/javase/tutorial/deployment/jar/signindex.html) 课程。

### 修改清单文件

您可以使用`m`命令行选项在创建JAR文件期间向清单添加自定义信息。本节介绍`m`选项。

Jar工具自动将带有路径名`META-INF/MANIFEST.MF`的默认清单放入您创建的任何JAR文件中。您可以通过修改默认清单来启用特殊JAR文件功能，例如包密封。通常，修改默认清单涉及向清单添加专用标头，以允许JAR文件执行特定的所需功能。

要修改清单，必须首先准备一个文本文件，其中包含要添加到清单的信息。然后，使用Jar工具的`m`选项将文件中的信息添加到清单中。

----

**警告：** 您要从中创建清单的文本文件必须以新行或回车符结束。如果不以新行或回车结束，则不会正确解析最后一行。

----

基本命令格式如下：

```
jar cfm jar-file manifest-addition input-file(s)
```

让我们看看这个命令中使用的选项和参数：

 -  `c`选项表示您要创建JAR文件。
 -  `m`选项表示您要将现有文件中的信息合并到正在创建的JAR文件的清单文件中。
 -  `f`选项表示您希望输出转到文件（您正在创建的JAR文件）而不是标准输出。
 -  `manifest-addition`是现有文本文件的名称（或路径和名称），其内容要添加到JAR文件清单的内容中。
 -  `jar-file`是您希望生成的JAR文件具有的名称。
 -  `input-file(s)`参数是一个以空格分隔的列表，其中包含要放置在JAR文件中的一个或多个文件。

`m`和`f`选项的顺序必须与相应的参数相同。

----

**注意：** 清单的内容必须以UTF-8编码。

----

本课程的其余部分演示了您可能要对清单文件进行的特定修改。

### 设定应用入口点

如果您有一个打包在JAR文件中的应用程序，则需要某种方法来指示JAR文件中的哪个类是应用程序的入口点。您可以使用清单中的`Main-Class`标头提供此信息，该标头具有以下一般形式：

```
Main-Class: classname
```

值`classname`是作为应用程序入口点的类的名称。

回想一下，入口点是一个具有签名 `public static void main(String[] args)` 的方法的类。

在清单中设置`Main-Class`标头后，然后使用以下形式的`java`命令运行JAR文件：

```
java -jar JAR-name
```

执行`Main-Class`标头中指定的类的 `main` 方法。

**例子**

我们想在运行JAR文件时在`MyPackage`包中的`MyClass`类中执行`main`方法。

我们首先创建一个名为`Manifest.txt`的文本文件，其中包含以下内容：

```
Main-Class: MyPackage.MyClass
```

----

**警告：** 文本文件必须以新行或回车结束。如果不以新行或回车结束，则不会正确解析最后一行。

----

然后，我们通过输入以下命令创建名为`MyJar.jar`的JAR文件：

```
jar cfm MyJar.jar Manifest.txt MyPackage/*.class
```

这将创建一个带有以下内容的清单的JAR文件：

```
Manifest-Version: 1.0
Created-By: 1.7.0_06 (Oracle Corporation)
Main-Class: MyPackage.MyClass
```

使用以下命令运行JAR文件时，`MyClass`的`main`方法将执行：

```
java -jar MyJar.jar
```

**使用 JAR 工具设定一个入口点**

'e'标志（用于'入口点'）创建或覆盖清单文件中的`Main-Class`属性。它可以在创建或更新JAR文件时使用。使用它指定应用程序入口点，而无需编辑或创建清单文件。

例如，此命令创建`app.jar`，其中清单中的`Main-Class`属性值设置为`MyApp`：

```
jar cfe app.jar MyApp MyApp.class
```

您可以通过运行以下命令直接调用此应用程序：

```
java -jar app.jar
```

如果入口点类名称在包中，则可以使用“.” （点）字符作为分隔符。例如，如果`Main.class`位于名为`foo`的包中，则可以通过以下方式指定入口点：

```
jar cfe Main.jar foo.Main foo/Main.class
```

### 添加类到 JAR 文件的类路径

您可能需要从JAR文件中引用其他JAR文件中的类。

例如，在典型情况下，applet打包在JAR文件中，该文件的清单引用别的JAR文件（或几个别的JAR文件）作为该applet的实用程序。

您可以指定要包含在applet或应用程序的清单文件中的`Class-Path`头字段中的类。`Class-Path`标头采用以下形式：

```
Class-Path: jar1-name jar2-name directory-name/jar3-name
```

通过在清单中使用`Class-Path`标头，可以避免在调用Java以运行应用程序时指定一个冗长的`-classpath`标志。

----

**注意：** `Class-Path`标头指向本地网络上的类或JAR文件，而不是JAR文件中的JAR文件或可通过Internet协议访问的类。要将JAR文件中的JAR文件中的类加载到类路径中，必须编写自定义代码来加载这些类。例如，如果`MyJar.jar`包含另一个名为`MyUtils.jar`的JAR文件，则不能使用`MyJar.jar`清单中的`Class-Path`标头将`MyUtils.jar`中的类加载到类路径中。

----

**例子**

我们希望将`MyUtils.jar`中的类加载到类路径中以便在`MyJar.jar`中使用。这两个JAR文件位于同一目录中。

我们首先创建一个名为`Manifest.txt`的文本文件，其中包含以下内容：

```
Class-Path: MyUtils.jar
```

----

**警告：** 文本文件必须以新行或回车结束。如果不以新行或回车结束，则不会正确解析最后一行。

----

然后，我们通过输入以下命令创建名为`MyJar.jar`的JAR文件：

```
jar cfm MyJar.jar Manifest.txt MyPackage/*.class
```

这将创建一个带有以下内容的清单的JAR文件：

```
Manifest-Version: 1.0
Class-Path: MyUtils.jar
Created-By: 1.7.0_06 (Oracle Corporation)
```

现在，当您运行`MyJar.jar`时，`MyUtils.jar`中的类将加载到类路径中。

### 设置包版本信息

您可能需要在JAR文件的清单中包含软件包版本信息。使用清单中的以下标头提供此信息：

| Header                   | Definition                              |
| ------------------------ | --------------------------------------- |
| `Name`                   | The name of the specification.          |
| `Specification-Title`    | The title of the specification.         |
| `Specification-Version`  | The version of the specification.       |
| `Specification-Vendor`   | The vendor of the specification.        |
| `Implementation-Title`   | The title of the implementation.        |
| `Implementation-Version` | The build number of the implementation. |
| `Implementation-Vendor`  | The vendor of the implementation.       |

可以为每个包分配一组这样的头。版本控制标题应直接显示在包的`Name`头下方。此示例显示所有版本控制标头：

```
Name: java/util/
Specification-Title: Java Utility Classes
Specification-Version: 1.2
Specification-Vendor: Example Tech, Inc.
Implementation-Title: java.util
Implementation-Version: build57
Implementation-Vendor: Example Tech, Inc.
```

有关包版本标头的更多信息，请参阅 [包版本控制规范](https://docs.oracle.com/javase/8/docs/technotes/guides/versioning/spec/versioning2.html#wp89936) 。

**例子**

我们希望在`MyJar.jar`的清单中包含上面示例中的标头。

我们首先创建一个名为`Manifest.txt`的文本文件，其中包含以下内容：

```
Name: java/util/
Specification-Title: Java Utility Classes
Specification-Version: 1.2
Specification-Vendor: Example Tech, Inc.
Implementation-Title: java.util 
Implementation-Version: build57
Implementation-Vendor: Example Tech, Inc.
```

----

**警告：** 文本文件必须以新行或回车结束。如果不以新行或回车结束，则不会正确解析最后一行。

----

然后，我们通过输入以下命令创建名为`MyJar.jar`的JAR文件：

```
jar cfm MyJar.jar Manifest.txt MyPackage/*.class
```

这将创建一个带有以下内容的清单的JAR文件：

```
Manifest-Version: 1.0
Created-By: 1.7.0_06 (Oracle Corporation)
Name: java/util/
Specification-Title: Java Utility Classes
Specification-Version: 1.2
Specification-Vendor: Example Tech, Inc.
Implementation-Title: java.util 
Implementation-Version: build57
Implementation-Vendor: Example Tech, Inc.
```

### 将包密封在 JAR 文件中

JAR文件中的包可以选择性地密封，这意味着该包中定义的所有类必须打包在同一个JAR文件中。例如，您可能希望密封包，以确保软件中类之间的版本一致性。

您通过在清单中添加`Sealed`标头来封装JAR文件中的包，该标头具有以下一般形式：

```
Name: myCompany/myPackage/
Sealed: true
```

值 `myCompany/myPackage/` 是要封装的包的名称。

请注意，包名称必须以“/”结尾。

**例子**

我们想在JAR文件`MyJar.jar`中密封两个包`firstPackage`和`secondPackage`。

我们首先创建一个名为`Manifest.txt`的文本文件，其中包含以下内容：

```
Name: myCompany/firstPackage/
Sealed: true

Name: myCompany/secondPackage/
Sealed: true
```

----

**警告：** 文本文件必须以新行或回车结束。如果不以新行或回车结束，则不会正确解析最后一行。

----

然后，我们通过输入以下命令创建名为`MyJar.jar`的JAR文件：

```
jar cfm MyJar.jar Manifest.txt MyPackage/*.class
```

这将创建一个带有以下内容的清单的JAR文件：

```
Manifest-Version: 1.0
Created-By: 1.7.0_06 (Oracle Corporation)
Name: myCompany/firstPackage/
Sealed: true
Name: myCompany/secondPackage/
Sealed: true
```

**密封的 JAR 文件**

如果要保证包中的所有类都来自相同的代码源，请使用JAR密封。密封的JAR指定由JAR定义的所有包都是密封的，除非在每个包的基础上被覆盖。

要密封JAR文件，请使用值为`true`的 `Sealed` 清单标头。 例如，

```
Sealed: true
```

指定此存档中的所有包都是密封的，除非显式覆盖清单条目中具有`Sealed`属性的特定包。

### 使用清单属性增强安全性

以下JAR文件清单属性可用于帮助确保applet或Java Web Start应用程序的安全性。只需要`Permissions`属性。

- `Permissions`属性用于确保应用请求仅仅在applet标签或用于调用应用程序的JNLP文件中指定的权限级别上。使用此属性可帮助防止某人重新部署使用您的证书签名的应用程序并在不同权限级别运行它。

  主JAR文件的清单中需要此属性。有关详细信息，请参阅Java平台标准版部署指南中的  [Permissions Attribute](https://docs.oracle.com/javase/8/docs/technotes/guides/deploy/manifest.html#JSDPG896) 。

- `Codebase`属性用于确保JAR文件的代码库仅限于特定域。使用此属性可防止某人出于恶意目的在其他网站上重新部署您的应用程序。有关详细信息，请参阅Java平台标准版部署指南中的 [Codebase Attribute](https://docs.oracle.com/javase/8/docs/technotes/guides/deploy/manifest.html#JSDPG897) 。

- `Application-Name`属性用于提供签名应用程序的安全提示中显示的标题。有关详细信息，请参阅Java平台标准版部署指南中的 [Application-Name Attribute](https://docs.oracle.com/javase/8/docs/technotes/guides/deploy/manifest.html#JSDPG899) 。

- `Application-Library-Allowable-Codebase`属性用于标识应该找到您的应用程序的位置。当JAR文件位于与JNLP文件或HTML页面不同的位置时，使用此属性可减少安全提示中显示的位置数。有关详细信息，请参阅Java平台标准版部署指南中的 [Application-Library-Allowable-Codebase Attribute](https://docs.oracle.com/javase/8/docs/technotes/guides/deploy/manifest.html#JSDPG900) 。

- `Caller-Allowable-Codebase`属性用于标识JavaScript代码可以从中调用应用程序的域。使用此属性可防止未知JavaScript代码访问您的应用程序。有关详细信息，请参阅Java平台标准版部署指南中的 [Caller-Allowable-Codebase Attribute](https://docs.oracle.com/javase/8/docs/technotes/guides/deploy/manifest.html#JSDPG901) 属性。

- `Entry-Point`属性用于标识允许用作RIA入口点的类。使用此属性可防止未经授权的代码从JAR文件中的其他可用入口点运行。有关详细信息，请参阅Java平台标准版部署指南中的 [Entry-Point Attribute](https://docs.oracle.com/javase/8/docs/technotes/guides/deploy/manifest.html#JSDPG902) 。

- `Trusted-Only`属性用于防止加载不受信任的组件。有关详细信息，请参阅Java平台标准版部署指南中的 [Trusted-Only Attribute](https://docs.oracle.com/javase/8/docs/technotes/guides/deploy/manifest.html#JSDPG903) 。

- `Trusted-Library`属性用于允许特权Java代码和沙箱Java代码之间的调用，而不会提示用户许可。有关详细信息，请参阅Java平台标准版部署指南中的 [Trusted-Library Attribute](https://docs.oracle.com/javase/8/docs/technotes/guides/deploy/manifest.html#JSDPG904) 。

有关将这些属性添加到清单文件的信息，请参阅 [修改清单文件](https://docs.oracle.com/javase/tutorial/deployment/jar/modman.html) 。

## 签名和验证 JAR 文件

您可以选择使用电子“签名”签署JAR文件。验证您的签名的用户可以授予您通常不具备的JAR捆绑软件安全权限。相反，您可以验证要使用的已签名JAR文件的签名。

本课程向您展示如何使用JDK中提供的工具来签名和验证JAR文件：

**[理解签名和验证](https://docs.oracle.com/javase/tutorial/deployment/jar/intro.html)**

如果您不熟悉签名和验证的概念，本节将帮助您。它包含相关术语的定义，签名提供的一些好处的解释，以及Java平台与JAR文件相关的签名机制的概述。

**[签名 JAR 文件](https://docs.oracle.com/javase/tutorial/deployment/jar/signing.html)**

在本节中，您将学习如何使用JDK™工具对JAR文件进行数字签名。

**[验证 JAR 文件](https://docs.oracle.com/javase/tutorial/deployment/jar/verify.html)**

本节介绍如何使用JDK工具集验证签名的JAR文件。

### 理解签名和验证

Java™平台使您能够对JAR文件进行数字签名。您对文件进行数字签名的原因与您使用笔和墨水签署纸质文档的原因相同 - 让读者知道您编写了文档，或者至少证明文档已获得您的批准。

例如，当您签署一封信时，每个认出您签名的人都可以确认您是否写了这封信。同样，当您对文件进行数字签名时，任何“识别”您的数字签名的人都知道该文件来自您。“识别”电子签名的过程称为验证。

签名JAR文件时，您还可以选择为签名添加时间戳。与在纸质文档上添加日期类似，签名的时间戳标识了JAR文件的签名时间。时间戳可用于验证用于签署JAR文件的证书在签名时是否有效。

签名和验证文件的能力是Java平台安全架构的重要组成部分。安全性由运行时生效的安全策略控制。您可以将策略配置为向applet和应用程序授予安全权限。例如，您可以向applet授予权限以执行正常情况下禁止的操作，例如读取和写入本地文件或运行本地可执行程序。如果您下载了一些由受信任实体签名的代码，则可以将该事实用作决定分配给代码的安全权限的标准。

一旦您（或您的浏览器）验证了applet来自可靠来源，您就可以让平台放宽安全限制，让applet执行通常情况下被禁止的操作。受信任的applet可以具有有效的策略文件指定的自由。

Java平台通过使用称为公钥和私钥的特殊数字来实现签名和验证。公钥和私钥成对出现，它们扮演互补角色。

私钥是电子“笔”，您可以使用它来签署文件。顾名思义，您的私钥只有您自己知道才能让其他人无法“伪造”您的签名。使用您的私钥签名的文件只能通过相应的公钥进行验证。

但是，单独的公钥和私钥不足以真正验证签名。即使您已验证签名文件包含匹配的密钥对，您仍需要某种方法来确认公钥实际上来自它声称来自的签名者。

因此，需要一个元素来进行签名和验证工作。该附加元素是签名者在签名的JAR文件中包含的证书。证书是来自公认的证书颁发机构的数字签名声明，表明谁拥有特定的公钥。认证机构是整个行业内可信赖的实体（通常是专门从事数字安全的公司），用于为密钥及其所有者签署和颁发证书。对于签名的JAR文件，证书指示谁拥有JAR文件中包含的公钥。

当您签署JAR文件时，您的公钥将与相关证书一起放在存档中，以便任何想要验证签名的人都可以轻松使用它。

总结数字签名：

 - 签名者使用私钥对JAR文件进行签名。
 - 相应的公钥与其证书一起放在JAR文件中，以便任何想要验证签名的人都可以使用它。

**摘要和签名文件**

签署JAR文件时，归档中的每个文件都会在归档的清单中提供摘要条目。以下是此类条目的示例：

```
Name: test/classes/ClassOne.class
SHA1-Digest: TD1GZt8G11dXY2p4olSZPc5Rj64=
```

摘要值是当文件被签名时文件内容的哈希或编码表示。当且仅当文件本身发生变化时，文件的摘要才会发生变化。

签名JAR文件时，会自动生成签名文件并将其放在JAR文件的`META-INF`目录中，该目录包含存档的清单。签名文件具有扩展名为`.SF`的文件名。以下是签名文件内容的示例：

```
Signature-Version: 1.0
SHA1-Digest-Manifest: h1yS+K9T7DyHtZrtI+LxvgqaMYM=
Created-By: 1.7.0_06 (Oracle Corporation)

Name: test/classes/ClassOne.class
SHA1-Digest: fcav7ShIG6i86xPepmitOVo4vWY=

Name: test/classes/ClassTwo.class
SHA1-Digest: xrQem9snnPhLySDiZyclMlsFdtM=

Name: test/images/ImageOne.gif
SHA1-Digest: kdHbE7kL9ZHLgK7akHttYV4XIa0=

Name: test/images/ImageTwo.gif
SHA1-Digest: mF0D5zpk68R4oaxEqoS9Q7nhm60=
```

如您所见，签名文件包含存档文件的摘要条目，这些文件看起来类似于清单中的摘要值条目。但是，虽然清单中的摘要值是根据文件本身计算的，但签名文件中的摘要值是根据清单中的相应条目计算的。签名文件还包含整个清单的摘要值（请参阅上例中的`SHA1-Digest-Manifest`标头）。

在验证签名的JAR文件时，将重新计算其每个文件的摘要，并将其与清单中记录的摘要进行比较，以确保JAR文件的内容自签名以来未发生更改。作为附加检查，重新计算清单文件本身的摘要值，并与签名文件中记录的值进行比较。

您可以在JDK™文档的 [Manifest Format](https://docs.oracle.com/javase/8/docs/technotes/guides/jar/jar.html#JAR_Manifest) 页面上阅读有关签名文件的其他信息。

**签名块文件**

除签名文件外，签名JAR文件时，签名块文件将自动放置在`META-INF`目录中。与清单文件或签名文件不同，签名块文件不是人类可读的。

签名块文件包含两个必要的验证元素：

 - 使用签名者的私钥生成的JAR文件的数字签名
 - 包含签名者公钥的证书，供想要验证签名JAR文件的任何人使用

签名块文件名通常具有`.DSA`扩展名，表示它们是由默认数字签名算法创建的。如果使用与其他标准算法相关联的密钥进行签名，则可以使用其他文件扩展名。

----

**相关文档**

有关密钥，证书和证书颁发机构的其他信息，请参阅

- [The JDK Security Tools](https://docs.oracle.com/javase/8/docs/technotes/tools/index.html#security)
- [X.509 Certificates](https://docs.oracle.com/javase/8/docs/technotes/guides/security/cert3.html)

有关Java平台安全体系结构的更多信息，请参阅下面的文档：

- [Security Features in Java SE](https://docs.oracle.com/javase/tutorial/security/index.html)
- [Java SE Security](http://www.oracle.com/technetwork/java/javase/tech/index-jsp-136007.html)
- [Security Tools](https://docs.oracle.com/javase/8/docs/technotes/tools/index.html#security)

### 签名 JAR 文件

您可以使用JAR签名和验证工具对JAR文件进行签名并为签名添加时间戳。您可以使用`jarsigner`命令调用JAR签名和验证工具，因此我们将其简称为“Jarsigner”。

要签署JAR文件，您必须首先拥有私钥。私钥及其关联的公钥证书存储在名为密钥库的受密码保护的数据库中。密钥库可以容纳许多潜在签名者的密钥。密钥库中的每个密钥都可以通过别名来标识，该别名通常是拥有密钥的签名者的名称。例如，属于丽塔琼斯的密钥可能具有别名“rita”。

用于签名JAR文件的命令的基本形式是：

```
jarsigner jar-file alias
```

在此命令中：

 -  `jar-file`是要签名的JAR文件的路径名。
 -  `alias` 是标识用于对JAR文件进行签名的私钥，以及密钥的关联证书的别名。

Jarsigner工具将提示您输入密钥库和别名的密码。

此命令的这种基本形式假定要使用的密钥库位于主目录中名为`.keystore`的文件中。它将分别创建名称为`x.SF`和`x.DSA`的签名和签名块文件，其中`x`是别名的前八个字母，全部转换为大写。此基本命令将使用签名的JAR文件覆盖原始JAR文件。

实际上，您可能希望使用一个或多个可用的命令选项。例如，鼓励为签名添加时间戳，以便用于部署应用程序的任何工具都可以验证用于签署JAR文件的证书在签名文件时是否有效。如果未包含时间戳，则Jarsigner工具会发出警告。

选项位于 `jar-file` 路径名之前。下表介绍了可用的选项：

| Option                           | Description                              |
| -------------------------------- | ---------------------------------------- |
| `-keystore` *url*                | 如果您不想使用`.keystore`缺省数据库，则指定要使用的密钥库。      |
| `-sigfile` *file*                | 如果您不希望从别名中获取基本名称，请指定`.SF`和`.DSA`文件的基本名称。文件必须仅由大写字母（A-Z），数字（0-9），连字符（ - ）和下划线（_）组成。 |
| `-signedjar` *file*              | 如果不希望使用签名文件覆盖原始未签名文件，则指定要生成的已签名JAR文件的名称。 |
| `-tsa` *url*                     | 使用URL标识的时间戳机构（TSA）为签名生成时间戳。              |
| `-tsacert` *alias*               | 使用别名标识的TSA公钥证书为签名生成时间戳。                  |
| `-altsigner` *class*             | 表示使用备用签名机制为签名添加时间戳。完全限定类名标识使用的类。         |
| `-altsignerpath` *classpathlist* | 提供`altsigner`选项标识的类的路径以及该类所依赖的任何JAR文件。   |

**例子**

让我们看一下使用Jarsigner工具签名JAR文件的几个示例。在这些示例中，我们将假设以下内容：

 - 你的别名是“johndoe”。
 - 要使用的密钥库位于当前工作目录中名为“mykeys”的文件中。
 - 要用于为签名添加时间戳的TSA位于http://tsa.url.example.com。

在这些假设下，您可以使用此命令对名为`app.jar`的JAR文件进行签名：

```
jarsigner -keystore mykeys -tsa http://tsa.url.example.com app.jar johndoe
```

系统将提示您输入密钥库和别名的密码。由于此命令不使用`-sigfile`选项，因此它创建的`.SF`和`.DSA`文件将命名为`JOHNDOE.SF`和`JOHNDOE.DSA`。由于该命令不使用`-signedjar`选项，因此生成的签名文件将覆盖`app.jar`的原始版本。

让我们来看看如果使用不同的选项组合会发生什么：

```
jarsigner -keystore mykeys -sigfile SIG -signedjar SignedApp.jar 
          -tsacert testalias app.jar johndoe
```

签名和签名块文件将分别命名为`SIG.SF`和`SIG.DSA`，签名的JAR文件`SignedApp.jar`将放在当前目录中。原始的未签名JAR文件将保持不变。此外，签名将带有标记为`testalias`的TSA公钥证书的时间戳。

**附加信息**

JAR签名和验证工具的完整参考页面是在线的：[Summary of Security Tools](https://docs.oracle.com/javase/8/docs/technotes/guides/security/SecurityToolsSummary.html) 

----

**注意：** 当证书是自签名时，应用程序的发布者将显示为`UNKNOWN`。有关更多信息，请参阅 [从显示为`UNKNOWN`的发布者运行应用程序是否安全？](http://www.java.com/en/download/faq/self_signed.xml) 。

----

### 验证已签名的 JAR 文件

通常，签名JAR文件的验证将由Java™运行时环境负责。您的浏览器将验证它下载的签名小程序。使用解释器的`-jar`选项调用的签名应用程序将由运行时环境验证。

但是，您可以使用`jarsigner`工具自行验证签名的JAR文件。您可能希望这样做，例如，测试您已准备好的已签名JAR文件。

用于验证签名JAR文件的基本命令是：

```
jarsigner -verify jar-file
```

此命令将验证JAR文件的签名，并确保存档中的文件自签名后未发生更改。如果验证成功，您将看到以下消息：

```
jar verified.
```

如果您尝试验证未签名的JAR文件，则会出现以下消息：

```
jar is unsigned. (signatures missing or not parsable)
```

如果验证失败，则会显示相应的消息。例如，如果自JAR文件签名以来JAR文件的内容已更改，则在尝试验证文件时将产生类似于以下内容的消息：

```
jarsigner: java.lang.SecurityException: invalid SHA1 
signature file digest for test/classes/Manifest.class
```

----

**注意：** 如果签名的JAR文件使用 `{java.home}/lib/security/java.security` 文件中的`jdk.jar.disabledAlgorithms` 安全属性中指定的任何算法，则JDK将签名的JAR文件作为未签名进行处理（其中`java.home`是您安装JRE的目录)。

----

## 使用 JAR 相关 API

Java平台包含几个用于JAR文件的类。其中一些API是：

- [`java.util.jar` 包](https://docs.oracle.com/javase/8/docs/api/java/util/jar/package-summary.html)
- [`java.net.JarURLConnection` 类](https://docs.oracle.com/javase/8/docs/api/java/net/JarURLConnection.html)
- [`java.net.URLClassLoader` 类](https://docs.oracle.com/javase/8/docs/api/java/net/URLClassLoader.html)

为了让您了解这些新API开辟的可能性，本课程将指导您完成名为`JarRunner`的示例应用程序的内部工作。

**例子 - The JarRunner Application**

JarRunner允许您通过在命令行上指定JAR文件的URL来运行捆绑在JAR文件中的应用程序。例如，如果名为`TargetApp`的应用程序捆绑在`http://www.example.com/TargetApp.jar`的JAR文件中，则可以使用以下命令运行该应用程序：

```
java JarRunner http://www.example.com/TargetApp.jar
```

为了让`JarRunner`工作，它必须能够执行以下任务，所有这些都是通过使用新API完成的：

 - 访问远程JAR文件并与其建立通信链接。
 - 检查JAR文件的清单，以查看存档中的哪些类是主类。
 - 在JAR文件中加载类。

`JarRunner`应用程序由两个类组成，`JarRunner`和`JarClassLoader`。`JarRunner`将大多数JAR处理任务委托给`JarClassLoader`类。`JarClassLoader`扩展`java.net.URLClassLoader`类。在继续学习之前，您可以浏览`JarRunner`和`JarClassLoader`类的源代码：

- [`JarRunner.java`](https://docs.oracle.com/javase/tutorial/deployment/jar/examples/JarRunner.java)
- [`JarClassLoader.java`](https://docs.oracle.com/javase/tutorial/deployment/jar/examples/JarClassLoader.java)

本课程包含两部分：

**[JarClassLoader 类](https://docs.oracle.com/javase/tutorial/deployment/jar/jarclassloader.html)**

本节将向您展示`JarClassLoader`如何使用一些新API来执行`JarRunner`应用程序所需的任务。

**[JarRunner 类](https://docs.oracle.com/javase/tutorial/deployment/jar/jarrunner.html)**

本节总结了包含`JarRunner`应用程序的`JarRunner`类。

### JarClassLoader 类

`JarClassLoader`类扩展了`java.net.URLClassLoader`。顾名思义，`URLClassLoader`旨在用于加载通过搜索一组URL访问的类和资源。URL可以引用目录或JAR文件。

除了子类化`URLClassLoader`之外，`JarClassLoader`还在其他两个与JAR相关的新API中使用，`java.util.jar`包和`java.net.JarURLConnectionclass`。在本节中，我们将详细介绍构造函数和`JarClassLoader`的两个方法。

**JarClassLoader 构造器**

构造函数将`java.net.URL`的实例作为参数。传递给此构造函数的URL将在`JarClassLoader`中的其他位置使用，以查找要从中加载类的JAR文件。

```java
public JarClassLoader(URL url) {
    super(new URL[] { url });
    this.url = url;
}
```

`URL`对象被传递给超类`URLClassLoader`的构造函数，该构造函数将`URL[]`数组而不是单个`URL`实例作为参数。

**getMainClassName 方法**

一旦使用打包为JAR的应用程序的URL构造了`JarClassLoader`对象，就需要一种方法来确定JAR文件中哪个类是应用程序的入口点。这是`getMainClassName`方法的工作：

```java
public String getMainClassName() throws IOException {
    URL u = new URL("jar", "", url + "!/");
    JarURLConnection uc = (JarURLConnection)u.openConnection();
    Attributes attr = uc.getMainAttributes();
    return attr != null
                   ? attr.getValue(Attributes.Name.MAIN_CLASS)
                   : null;
}
```

您可以回忆起打包为JAR的应用程序的入口点是由JAR文件清单的`Main-Class`标头指定的。要了解`getMainClassName`如何访问`Main-Class`标头值，让我们详细查看该方法，特别注意它使用的新JAR处理功能：

**JarURLConnection 类和 JAR URLs**

`getMainClassName`方法使用`java.net.JarURLConnection`类指定的JAR URL格式。JAR文件的URL语法如下例所示：

```
jar:http://www.example.com/jarfile.jar!/
```

终止分隔符 `!/` 表示URL引用整个JAR文件。分隔符后面的任何内容都引用特定的JAR文件内容，如下例所示：

```
jar:http://www.example.com/jarfile.jar!/mypackage/myclass.class
```

`getMainClassName` 方法的第一行是：

```
URL u = new URL("jar", "", url + "!/");
```

此语句构造一个表示JAR URL的新URL对象，将 `!/` 分隔符附加到用于创建`JarClassLoader`实例的URL。

**java.net.JarURLConnection 类**

此类表示应用程序和JAR文件之间的通信链接。它具有访问JAR文件清单的方法。`getMainClassName`的第二行是：

```
JarURLConnection uc = (JarURLConnection)u.openConnection();
```

在此语句中，在第一行中创建的URL实例将打开`URLConnection`。然后将`URLConnection`实例强制转换为`JarURLConnection`，以便它可以利用`JarURLConnection`的JAR处理功能。

**获取清单属性：java.util.jar.Attributes**

通过对JAR文件打开`JarURLConnection`，可以使用`JarURLConnection`的`getMainAttributes`方法访问JAR文件清单中的标头信息。此方法返回`java.util.jar.Attributes`的实例，该实例将JAR文件清单中的标题名称与其关联的字符串值进行映射。`getMainClassName`中的第三行创建一个`Attributes`对象：

```
Attributes attr = uc.getMainAttributes();
```

要获取清单的`Main-Class`标头的值，`getMainClassName`的第四行将调用`Attributes.getValue`方法：

```
return attr != null
               ? attr.getValue(Attributes.Name.MAIN_CLASS)
               : null;
```

方法的参数`Attributes.Name.MAIN_CLASS`指定它是您想要的`Main-Class`标头的值。（`Attributes.Name`类还提供静态字段，如`MANIFEST_VERSION`，`CLASS_PATH`和`SEALED`，用于指定其他标准清单头。）

**invokeClass 方法**

我们已经看到了`JarURLClassLoader`如何识别JAR捆绑应用程序中的主类。最后一个要考虑的方法是`JarURLClassLoader.invokeClass`，它可以调用主类来启动JAR绑定的应用程序：

```java
public void invokeClass(String name, String[] args)
    throws ClassNotFoundException,
           NoSuchMethodException,
           InvocationTargetException
{
    Class c = loadClass(name);
    Method m = c.getMethod("main", new Class[] { args.getClass() });
    m.setAccessible(true);
    int mods = m.getModifiers();
    if (m.getReturnType() != void.class || !Modifier.isStatic(mods) ||
        !Modifier.isPublic(mods)) {
        throw new NoSuchMethodException("main");
    }
    try {
        m.invoke(null, new Object[] { args });
    } catch (IllegalAccessException e) {
        // This should not happen, as we have disabled access checks
    }
}
```

`invokeClass`方法有两个参数：应用程序的入口点类的名称和要传递给入口点类的`main`方法的字符串参数数组。首先，加载主类：

```
Class c = loadClass(name);
```

`loadClass`方法继承自`java.lang.ClassLoader`。

加载主类后，`java.lang.reflect`包的反射API用于将参数传递给类并启动它。您可以参考 [The Reflection API](https://docs.oracle.com/javase/tutorial/reflect/index.html) 上的教程来查看反射。

### JarRunner 类

使用以下形式的命令启动JarRunner应用程序：

```
java JarRunner url [arguments]
```

在上一节中，我们已经看到了`JarClassLoader`如何从给定的URL中识别和加载打包为JAR应用程序的主类。因此，要完成`JarRunner`应用程序，我们需要能够从命令行获取URL和任何参数，并将它们传递给`JarClassLoader`的实例。这些任务属于`JarRunner`类，它是`JarRunner`应用程序的入口点。

首先，从命令行中指定的URL创建`java.net.URL`对象：

```java
public static void main(String[] args) {
    if (args.length < 1) {
        usage();
    }
    URL url = null;
    try {
        url = new URL(args[0]);
    } catch (MalformedURLException e) {
        fatal("Invalid URL: " + args[0]);
    }
```

如果`args.length < 1`，则表示命令行中未指定URL，因此将打印有用的提示消息。如果第一个命令行参数是一个有效的URL，则会创建一个新的`URL`对象来表示它。

接下来，JarRunner创建一个新的`JarClassLoader`实例，将构造函数传递给命令行中指定的URL：

```java
JarClassLoader cl = new JarClassLoader(url);
```

正如我们在上一节中看到的那样，JarRunner通过`JarClassLoader`进入JAR处理API。

传递给`JarClassLoader`构造函数的URL是您要运行的打包为JAR应用程序的URL。接下来，JarRunner调用类加载器的`getMainClassNamemethod`来识别应用程序的入口点类：

```java
String name = null;
try {
    name = cl.getMainClassName();
} catch (IOException e) {
    System.err.println("I/O error while loading JAR file:");
    e.printStackTrace();
    System.exit(1);
}
if (name == null) {
    fatal("Specified jar file does not contain a 'Main-Class'" +
          " manifest attribute");
}
```

关键声明以粗体突出显示。其他语句用于错误处理。

一旦`JarRunner`识别出应用程序的入口点类，只剩下两个步骤：将所有参数传递给应用程序并实际启动应用程序。 `JarRunner`使用以下代码执行这些步骤：

```java
// Get arguments for the application
String[] newArgs = new String[args.length - 1];
System.arraycopy(args, 1, newArgs, 0, newArgs.length);
// Invoke application's main class
try {
    cl.invokeClass(name, newArgs);
} catch (ClassNotFoundException e) {
    fatal("Class not found: " + name);
} catch (NoSuchMethodException e) {
    fatal("Class does not define a 'main' method: " + name);
} catch (InvocationTargetException e) {
    e.getTargetException().printStackTrace();
    System.exit(1);
}
```

回想一下，第一个命令行参数是打包为JAR的应用程序的URL。因此，传递给该应用程序的任何参数都在`args`数组中的元素`1`和更之前的元素中。`JarRunner`接受这些元素，并创建一个名为`newArgs`的新数组以传递给应用程序（上面的粗线）。然后，`JarRunner`将入口点的类名和新参数列表传递给`JarClassLoader`的`invokeClass`方法。正如我们在上一节中看到的，`invokeClass`将加载应用程序的入口点类，将所有参数传递给它，然后启动应用程序。

# 国际化

此课程中的课程教您如何使Java应用程序国际化。国际化的应用程序很容易适应世界各地最终用户的习俗和语言。

------

**注意：** 本教程的内容涵盖*核心*国际化功能，这是为桌面，企业和移动应用程序提供的其他功能所需的基础。 有关其他信息，请参阅 [Java Internationalization home page](http://www.oracle.com/technetwork/java/javase/tech/intl-139810.html) 。

----

[![trail icon](https://docs.oracle.com/javase/tutorial/images/internatsm.GIF)**介绍**](https://docs.oracle.com/javase/tutorial/i18n/intro/index.html) 定义术语*国际化*，提供快速示例程序，并提供可用于国际化现有程序的清单。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/internatsm.GIF)**设定 Locale**](https://docs.oracle.com/javase/tutorial/i18n/locale/index.html) 解释如何创建和使用 `Locale` 对象。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/internatsm.GIF)**隔离 Locale-Specific 数据**](https://docs.oracle.com/javase/tutorial/i18n/resbundle/index.html) 展示如何动态访问随着 `Locale` 变化的对象。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/internatsm.GIF)**格式化**](https://docs.oracle.com/javase/tutorial/i18n/format/index.html) 解释了如何根据`Locale`格式化数字，日期和文本消息，以及如何使用模式创建自定义格式。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/internatsm.GIF)**使用 Text**](https://docs.oracle.com/javase/tutorial/i18n/text/index.html) 提供了以与语言环境无关的方式操作文本的技术。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/internatsm.GIF)**网络资源的国际化**](https://docs.oracle.com/javase/tutorial/i18n/network/index.html) 解释了如何为IDN提供国际化。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/internatsm.GIF)**国际化服务提供者**](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/index.html) 解释了如何启用与语言环境相关的数据和服务的插件。

## 介绍

*国际化*是设计应用程序的过程，以便它可以适应各种语言和区域而无需进行更改。有时，国际化一词缩写为 i18n，因为第一个“i”和最后一个“n”之间有18个字母。

国际化程序具有以下特点：

 - 通过添加本地化数据，可以在全球范围内运行相同的可执行文件。
 - 文本元素（例如状态消息和GUI组件标签）在程序中不是硬编码的。相反，它们存储在源代码之外并动态检索。
 - 支持新语言不需要重新编译。
 - 与文化相关的数据（如日期和货币）以符合最终用户区域和语言的格式显示。
 - 它可以快速本地化。

*本地化*是通过添加特定于语言环境的组件和翻译文本来调整特定区域或语言的软件的过程。术语*本地化*通常缩写为l10n，因为“l”和“n”之间有10个字母。

本地化的主要任务是翻译用户界面元素和文档。本地化不仅涉及改变语言交互，还涉及其他相关更改，如数字显示，日期，货币等。其他类型的数据（如声音和图像）如果具有文化敏感性，则可能需要进行本地化。应用程序的国际化程度越高，就越容易将其本地化为特定的语言和字符编码方案。

起初国际化似乎有点令人生畏。阅读以下部分将有助于您轻松进入主题。

**[例子](https://docs.oracle.com/javase/tutorial/i18n/intro/quick.html)**

本节将逐步介绍如何将简单程序国际化。

**[清单](https://docs.oracle.com/javase/tutorial/i18n/intro/checklist.html)**

因此，您继承了需要国际化的程序，或者您计划确定新开发软件的要求。你可能不知道从哪里开始？看看这份清单。它总结了必要的国际化任务，并提供了本章相关课程的链接。

### 例子

如果您是国际化软件的新手，本课程适合您。本课程使用一个简单示例演示如何使程序国际化，以便以适当的语言显示文本消息。您将了解`Locale`和`ResourceBundle`对象如何协同工作以及如何使用属性文件。

**[国际化之前](https://docs.oracle.com/javase/tutorial/i18n/intro/before.html)**

源代码的第一个版本包含我们想要显示的消息的硬编码英语版本。 这不是您编写国际化软件的方式。

**[国际化之后](https://docs.oracle.com/javase/tutorial/i18n/intro/after.html)**

这是对国际化后源代码外观的预览。

**[运行例子程序](https://docs.oracle.com/javase/tutorial/i18n/intro/run.html)**

要运行示例程序，请在命令行中指定语言和国家/地区。 

**[例子程序国际化](https://docs.oracle.com/javase/tutorial/i18n/intro/steps.html)**

国际化该程序只需几步。你会惊讶于它是多么容易。

#### 国际化之前

假设您编写了一个显示三条消息的程序，如下所示：

```java
public class NotI18N {

    static public void main(String[] args) {

        System.out.println("Hello.");
        System.out.println("How are you?");
        System.out.println("Goodbye.");
    }
}
```

您已经决定该程序需要为居住在法国和德国的人们展示相同的信息。不幸的是，您的编程人员不是多语言的，因此需要您帮助将消息翻译成法语和德语。由于翻译人员不是程序员，因此您必须将消息从源代码中移出并转换为翻译人员可以编辑的文本文件。此外，程序必须足够灵活，以便能够以其他语言显示消息，但现在没有人知道这些语言是什么。

看起来该程序需要国际化。

#### 国际化之后

国际化计划的源代码如下。请注意，消息的文本不是硬编码的。

```java
import java.util.*;

public class I18NSample {

    static public void main(String[] args) {

        String language;
        String country;

        if (args.length != 2) {
            language = new String("en");
            country = new String("US");
        } else {
            language = new String(args[0]);
            country = new String(args[1]);
        }

        Locale currentLocale;
        ResourceBundle messages;

        currentLocale = new Locale(language, country);

        messages = ResourceBundle.getBundle("MessagesBundle", currentLocale);
        System.out.println(messages.getString("greetings"));
        System.out.println(messages.getString("inquiry"));
        System.out.println(messages.getString("farewell"));
    }
}
```

要编译和运行此程序，您需要以下源文件：

- [`I18NSample.java`](https://docs.oracle.com/javase/tutorial/i18n/intro/examples/I18NSample.java)
- [`MessagesBundle.properties`](https://docs.oracle.com/javase/tutorial/i18n/intro/examples/MessagesBundle.properties)
- [`MessagesBundle_de_DE.properties`](https://docs.oracle.com/javase/tutorial/i18n/intro/examples/MessagesBundle_de_DE.properties)
- [`MessagesBundle_en_US.properties`](https://docs.oracle.com/javase/tutorial/i18n/intro/examples/MessagesBundle_en_US.properties)
- [`MessagesBundle_fr_FR.properties`](https://docs.oracle.com/javase/tutorial/i18n/intro/examples/MessagesBundle_fr_FR.properties)

#### 运行例子程序

国际化程序是灵活的; 它允许最终用户在命令行上指定语言和国家/地区。在以下示例中，语言代码为`fr`（法语），国家/地区代码为`FR`（法国），因此程序以法语显示消息：

```
% java I18NSample fr FR
Bonjour.
Comment allez-vous?
Au revoir.
```

在下一个示例中，语言代码为`en`（英语），国家/地区代码为`US`（美国），因此程序以英语显示消息：

```
% java I18NSample en US
Hello.
How are you?
Goodbye.
```

#### 例子程序的国际化

如果你查看国际化的源代码，你会发现硬编码的英文消息已被删除。由于消息不再是硬编码的，并且因为语言代码是在运行时指定的，因此可以在全球范围内分发相同的可执行文件。本地化不需要重新编译。该程序已国际化。

您可能想知道消息文本的内容或语言和国家/地区代码的含义。别担心。 当您逐步完成示例程序的国际化过程时，您将了解这些概念。

**1. 创建 Properties 文件**

属性文件存储有关程序或环境特征的信息。属性文件采用纯文本格式。您可以使用几乎任何文本编辑器创建文件。

在示例中，属性文件存储要显示的消息的可翻译文本。在程序国际化之前，此文本的英文版本在`System.out.println`语句中进行了硬编码。默认属性文件名为`MessagesBundle.properties`，包含以下行：

```
greetings = Hello
farewell = Goodbye
inquiry = How are you?
```

现在消息在属性文件中，它们可以被翻译成各种语言。不需要更改源代码。法语翻译器创建了一个名为`MessagesBundle_fr_FR.properties`的属性文件，其中包含以下行：

```
greetings = Bonjour.
farewell = Au revoir.
inquiry = Comment allez-vous?
```

请注意，等号右侧的值已被翻译，但左侧的键未更改。这些键不能更改，因为它们将在您的程序获取翻译文本时被引用。

属性文件的名称很重要。例如，`MessagesBundle_fr_FR.properties`文件的名称包含`fr`语言代码和`FR`国家/地区代码。创建`Locale`对象时也会使用这些代码。

**2. 定义 Locale**

`Locale`对象标识特定语言和国家/地区。以下语句定义语言为英语且国家/地区为美国的 `Locale` ：

```
aLocale = new Locale("en","US");
```

下一个示例为加拿大和法国的法语创建`Locale`对象：

```
caLocale = new Locale("fr","CA");
frLocale = new Locale("fr","FR");
```

该计划非常灵活。该程序不是使用硬编码语言和国家/地区代码，而是在运行时从命令行获取它们：

```
String language = new String(args[0]);
String country = new String(args[1]);
currentLocale = new Locale(language, country);
```

`Locale` 对象只是标识符。定义`Locale` 后，将其传递给执行有用任务的其他对象，例如格式化日期和数字。这些对象是区域设置敏感的，因为它们的行为因`Locale` 而异。`ResourceBundle`是区域设置敏感对象的示例。

**3. 创建 ResourceBundle**

`ResourceBundle`对象包含特定于语言环境的对象。您使用`ResourceBundle`对象来隔离区域设置敏感数据，例如可翻译文本。在示例程序中，`ResourceBundle`由包含我们要显示的消息文本的属性文件支持。

`ResourceBundle`创建如下：

```
messages = ResourceBundle.getBundle("MessagesBundle", currentLocale);
```

传递给`getBundle`方法的参数标识将访问哪些属性文件。`MessagesBundle`的第一个参数引用了这个属性文件系列：

```
MessagesBundle_en_US.properties
MessagesBundle_fr_FR.properties
MessagesBundle_de_DE.properties
```

`Locale`是`getBundle`的第二个参数，它指定选择哪个`MessagesBundle`文件。创建 `Locale` 后，语言代码和国家/地区代码将传递给其构造函数。请注意，语言和国家/地区代码遵循属性文件名称中的`MessagesBundle`。

现在，您所要做的就是从`ResourceBundle`获取已翻译的消息。

**4. 从 ResourceBundle 获取文本**

属性文件包含键值对。值包含程序将显示的已翻译文本。使用`getString`方法从`ResourceBundle`获取已翻译的消息时指定消息对应的键。例如，要检索由问候键标识的消息，请按如下方式调用`getString`：

```
String msg1 = messages.getString("greetings");
```

示例程序使用键 `greetings` ，因为它反映了消息的内容，但它可能使用了另一个字符串，例如`s1`或`msg1`。请记住，键在程序中是硬编码的，并且必须存在于属性文件中。如果您的翻译人员意外地修改了属性文件中的键，则`getString`将无法找到消息。

**总结**

如您所见，国际化程序并不太难。它需要一些规划和一些额外的编码，但好处是巨大的。为了向您提供国际化过程的概述，本课程中的示例程序有意保持简单。在阅读下面的课程时，您将了解Java编程语言的更高级的国际化功能。

### 清单

首次编写时，许多程序都没有国际化。这些程序可能已经开始作为原型，或者它们可能不是用于国际分发。如果必须国际化现有程序，请执行以下步骤：

**识别文化依赖数据**

短信是最明显的数据形式，随文化而变化。 但是，其他类型的数据可能因地区或语言而异。 以下列表包含文化相关数据的示例：

 - 消息
 - GUI组件上的标签
- 在线帮助
 - 声音
 - 颜色
 - 图形
 - 图标
- 日期
 - 时间
 - 数字
 - 货币
- 计量单位
- 电话号码
 - 荣誉和个人头衔
 - 邮政地址
 - 页面布局

**将可翻译的文本隔离进入 Resource Bundles**

翻译费用昂贵。您可以通过隔离必须在`ResourceBundle`对象中转换的文本来帮助降低成本。可翻译文本包括状态消息，错误消息，日志文件条目和GUI组件标签。该文本被硬编码到尚未国际化的程序中。您需要找到显示给最终用户的所有硬编码文本。例如，您应该像这样清理代码：

```java
String buttonLabel = "OK";
// ...
JButton okButton = new JButton(buttonLabel);
```

有关详细信息，请参阅 [隔离特定于区域设置的数据](https://docs.oracle.com/javase/tutorial/i18n/resbundle/index.html) 部分。

**处理复合消息**

复合消息包含可变数据。在消息“磁盘包含1100个文件”中，整数1100可以变化。此消息难以翻译，因为句子中整数的位置在所有语言中都不相同。以下消息不可翻译，因为句子元素的顺序是通过连接硬编码的：

```java
Integer fileCount;
// ...
String diskStatus = "The disk contains " + fileCount.toString() + " files";
```

只要有可能，您应该避免构造复合消息，因为它们很难翻译。但是，如果您的应用程序需要复合消息，则可以使用 [消息](https://docs.oracle.com/javase/tutorial/i18n/format/messageintro.html) 一节中描述的技术处理它们。

**格式化数字和货币**

如果您的应用程序显示数字和货币，则必须以与语言环境无关的方式格式化它们。以下代码尚未国际化，因为它不会在所有国家/地区正确显示数字：

```java
Double amount;
TextField amountField;
// ...
String displayAmount = amount.toString();
amountField.setText(displayAmount);
```

您应该使用正确格式化数字的例程替换前面的代码。Java编程语言提供了几个格式化数字和货币的类。这些类在 [数字和货币](https://docs.oracle.com/javase/tutorial/i18n/format/numberintro.html) 部分中讨论。

**格式化日期和时间**

日期和时间格式因地区和语言而异。如果您的代码包含如下语句，则需要更改它：

```java
Date currentDate = new Date();
TextField dateField;
// ...
String dateString = currentDate.toString();
dateField.setText(dateString);
```

如果您使用日期格式化类，您的应用程序可以在世界各地正确显示日期和时间。有关示例和说明，请参阅 [日期和时间](https://docs.oracle.com/javase/tutorial/i18n/format/dateintro.html) 部分。

**使用 Unicode 字符属性**

以下代码尝试验证字符是否为字母：

```java
char ch;
// This code is incorrect
if ((ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z'))
```

注意这样的代码，因为它不适用于英语以外的语言。例如，`if`语句错过了德语单词`Grün`中的字符`ü`。

`Character`比较方法使用`Unicode`标准来标识字符属性。因此，您应该使用以下代码替换以前的代码：

```java
char ch;
// ...
if (Character.isLetter(ch))
```

有关字符比较方法的详细信息，请参阅 [检查字符属性](https://docs.oracle.com/javase/tutorial/i18n/text/charintro.html) 一节。

**比较字符串属性**

排序文本时，您经常比较字符串。如果显示文本，则不应使用`String`类的比较方法。尚未国际化的程序可能会比较字符串如下：

```java
String target;
String candidate;
// ...
if (target.equals(candidate)) {
// ...
if (target.compareTo(candidate) < 0) {
// ...
```

`String.equals`和`String.compareTo`方法执行二进制比较，在大多数语言中排序时无效。相反，您应该使用`Collator`类，这在 [比较字符串](https://docs.oracle.com/javase/tutorial/i18n/text/collationintro.html) 一节中有所描述。

**转换非Unicode文本**

Java编程语言中的字符以Unicode编码。如果您的应用程序处理非Unicode文本，您可能需要将其转换为Unicode。有关更多信息，请参阅 [转换非Unicode文本](https://docs.oracle.com/javase/tutorial/i18n/text/convertintro.html) 部分。

## 设定 Locale

国际化程序可以在全世界以不同方式显示信息。例如，该程序将在巴黎，东京和纽约显示不同的消息。如果本地化过程已经过微调，该程序将在纽约和伦敦显示不同的消息，以解释美国和英国英语之间的差异。国际化计划如何确定最终用户的适当语言和区域？简单。它引用了`Locale`对象。

`Locale`对象是语言和区域的特定组合的标识符。如果一个类根据`Locale`改变其行为，则称其对语言环境敏感。例如，`NumberFormat`类是区域设置敏感的，它返回的数字格式取决于`Locale`。因此，`NumberFormat`可以返回`902 300`（法国），或`902.300`（德国）或`902,300`（美国）的数字。区域设置对象只是标识符。实际工作（例如格式化和检测字边界）由区域设置敏感类的方法执行。

以下部分说明如何使用`Locale`对象：

**[创建 Locale](https://docs.oracle.com/javase/tutorial/i18n/locale/create.html)**

创建`Locale`对象时，通常指定语言代码和国家/地区代码。第三个参数，即变体，是可选的。

**[BCP 47 扩展](https://docs.oracle.com/javase/tutorial/i18n/locale/extensions.html)**

本节介绍如何将Unicode区域设置扩展或专用扩展添加到`Locale`。

**[识别可用 Locales](https://docs.oracle.com/javase/tutorial/i18n/locale/identify.html)**

区分区域设置的类仅支持某些 `Locale` 定义。本节介绍如何确定支持哪些`Locale`定义。

**[语言标签过滤和查找](https://docs.oracle.com/javase/tutorial/i18n/locale/matching.html)**

本节介绍语言标记，语言标记过滤和语言标记查找的国际化支持。

**[Locale 的作用域](https://docs.oracle.com/javase/tutorial/i18n/locale/scope.html)**

在Java平台上，您不能通过在运行应用程序之前设置环境变量来指定全局 `Locale` 。相反，您要么依赖默认的 `Locale` ，要么将 `Locale` 分配给每个区域设置敏感的对象。

**[语言环境敏感的服务 SPI](https://docs.oracle.com/javase/tutorial/i18n/locale/services.html)**

本节介绍如何启用与语言环境相关的数据和服务的插件。除了当前可用的语言环境之外，这些SPI（服务提供程序接口）还提供对更多语言环境的支持。

### 创建 Locale

有几种方法可以创建`Locale`对象。无论使用何种技术，创建都可以像指定语言代码一样简单。但是，您可以通过设置区域（也称为“国家/地区”）和变体代码来进一步区分区域设置。如果您使用的是JDK 7或更高版本，则还可以指定脚本代码和Unicode语言环境扩展。

创建`Locale`对象的四种方法是：

- [`Locale.Builder` 类](https://docs.oracle.com/javase/tutorial/i18n/locale/create.html#builder)
- [`Locale` 构造器](https://docs.oracle.com/javase/tutorial/i18n/locale/create.html#constructors)
- [`Locale.forLanguageTag` 工厂方法](https://docs.oracle.com/javase/tutorial/i18n/locale/create.html#factory)
- [`Locale` 常量](https://docs.oracle.com/javase/tutorial/i18n/locale/create.html#constants)

----

**版本说明:**  `Locale.Builder` 类和 `forLanguageTag` 方法被添加到 Java SE 7 发行版中。

----

**`LocaleBuilder` 类**

[`Locale.Builder`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.Builder.html) 实用程序类可用于构造符合IETF BCP 47语法的`Locale`对象。例如，要指定法语和加拿大的国家/地区，可以调用`Locale.Builder`构造函数，然后按如下方式链接`setter`方法：

```java
Locale aLocale = new Locale.Builder().setLanguage("fr").setRegion("CA").build();
```

下一个示例为美国和英国的英语创建`Locale`对象：

```java
Locale bLocale = new Locale.Builder().setLanguage("en").setRegion("US").build();
Locale cLocale = new Locale.Builder().setLanguage("en").setRegion("GB").build();
```

最后一个示例为俄语创建一个`Locale`对象：

```java
Locale dLocale = new Locale.Builder().setLanguage("ru").setScript("Cyrl").build();
```

**`Locale` 构造器**

`Locale`类中有三个可用于创建`Locale`对象的构造函数：

- [`Locale(String language)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#Locale-java.lang.String-)
- [`Locale(String language, String country)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#Locale-java.lang.String-java.lang.String-)
- [`Locale(String language, String country, String variant)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#Locale-java.lang.String-java.lang.String-java.lang.String-)

以下示例为加拿大的法语，美国和英国的英语以及俄语创建 `Locale` 对象。

```java
aLocale = new Locale("fr", "CA");
bLocale = new Locale("en", "US");
cLocale = new Locale("en", "GB");
dLocale = new Locale("ru");
```

在JDK 7之前的版本中，无法在`Locale`对象上设置脚本代码。

**`forLanguageTag` 工厂方法**

如果您的语言标记字符串符合IETF BCP 47标准，则可以使用Java SE 7发行版中引入的[`forLanguageTag(String)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#forLanguageTag-java.lang.String-) 工厂方法。例如：

```java
Locale aLocale = Locale.forLanguageTag("en-US");
Locale bLocale = Locale.forLanguageTag("ja-JP-u-ca-japanese");
```

**`Locale` 常量**

为方便起见，`Locale`类为某些语言和国家/地区提供常量。例如：

```java
cLocale = Locale.JAPAN;
dLocale = Locale.CANADA_FRENCH;
```

指定语言常量时，区域设置的区域部分未定义。接下来的三个语句创建等效的`Locale`对象：

```java
j1Locale = Locale.JAPANESE;
j2Locale = new Locale.Builder().setLanguage("ja").build();
j3Locale = new Locale("ja");
```

由以下三个语句创建的`Locale`对象也是等效的：

```java
j4Locale = Locale.JAPAN;
j5Locale = new Locale.Builder().setLanguage("ja").setRegion("JP").build();
j6Locale = new Locale("ja", "JP");
```

**编码**

以下部分讨论语言代码和可选脚本，区域和变体代码。

**语言编码**

语言代码是符合ISO 639标准的两个或三个小写字母。您可以在 http://www.loc.gov/standards/iso639-2/php/code_list.php 找到ISO 639代码的完整列表。

下表列出了一些语言代码。

| Language Code | Description |
| ------------- | ----------- |
| `de`          | German      |
| `en`          | English     |
| `fr`          | French      |
| `ru`          | Russian     |
| `ja`          | Japanese    |
| `jv`          | Javanese    |
| `ko`          | Korean      |
| `zh`          | Chinese     |

**脚本编码**

脚本代码以大写字母开头，后跟三个小写字母，符合ISO 15924标准。您可以在 http://unicode.org/iso15924/iso15924-codes.html 找到ISO 15924代码的完整列表。

下表列出了一些脚本代码。

| Script Code | Description |
| ----------- | ----------- |
| `Arab`      | Arabic      |
| `Cyrl`      | Cyrillic    |
| `Kana`      | Katakana    |
| `Latn`      | Latin       |

检索`Locale`的脚本信息有三种方法：

- [`getScript()`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#getScript--) –  返回`Locale`对象的4个字母的脚本代码。如果没有为语言环境定义脚本，则返回空字符串。
- [`getDisplayScript()`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#getDisplayScript--) – 返回适合显示给用户的语言环境脚本的名称。如果可能，将为默认语言环境本地化名称。因此，例如，如果脚本代码是“Latn”，则返回的脚本名称将是英语语言环境的字符串“Latin”。
- [`getDisplayScript(Locale)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#getDisplayScript-java.util.Locale-) – 如果可能，返回本地化的指定`Locale`的显示名称。

**区域编码**

区域（国家/地区）代码包含符合ISO 3166标准的两个或三个大写字母，或符合UN M.49标准的三个数字。可以在 http://www.chemie.fu-berlin.de/diverse/doc/ISO_3166.html 找到代码的副本。

下表包含几个示例国家和地区代码。

| A-2 Code | A-3 Code | Numeric Code | Description        |
| -------- | -------- | ------------ | ------------------ |
| `AU`     | `AUS`    | `036`        | Australia          |
| `BR`     | `BRA`    | `076`        | Brazil             |
| `CA`     | `CAN`    | `124`        | Canada             |
| `CN`     | `CHN`    | `156`        | China              |
| `DE`     | `DEU`    | `276`        | Germany            |
| `FR`     | `FRA`    | `250`        | France             |
| `IN`     | `IND`    | `356`        | India              |
| `RU`     | `RUS`    | `643`        | Russian Federation |
| `US`     | `USA`    | `840`        | United States      |

**变体编码**

可选的`variant`代码可用于进一步区分您的`Locale`。例如，变体代码可用于指示区域代码未涵盖的辩证差异。

------

**版本说明：** 在Java SE 7发行版之前，变体代码有时用于识别不是特定于语言或区域的差异。例如，它可能已被用于识别计算平台之间的差异，例如Windows或UNIX。根据IETF BCP 47标准，不鼓励使用此标准。

要定义与您的环境相关的非语言特定变体，请使用扩展机制，如 [BCP 47 Extensions](https://docs.oracle.com/javase/tutorial/i18n/locale/extensions.html) 中所述。

------

从符合IETF BCP 47标准的Java SE 7版本开始，变体代码专门用于指示定义语言或其方言的其他变体。IETF BCP 47标准对变体子标签强加了语法限制。您可以查看变体代码列表（搜索变体）<http://www.iana.org/assignments/language-subtag-registry> 。

例如，Java SE使用变体代码来支持泰语。按照惯例，`th`和`th_TH`语言环境的`NumberFormat`对象将使用常见的阿拉伯数字形状或阿拉伯数字来格式化泰语数字。但是，`th_TH_TH`语言环境的`NumberFormat`使用泰语数字形状。来自 [`ThaiDigits.java`](https://docs.oracle.com/javase/tutorial/i18n/locale/examples/ThaiDigits.java) 的摘录表明：

```java
String outputString = new String();
Locale[] thaiLocale = {
             new Locale("th"),
             new Locale("th", "TH"),
             new Locale("th", "TH", "TH")
         };

for (Locale locale : thaiLocale) {
    NumberFormat nf = NumberFormat.getNumberInstance(locale);
    outputString = outputString + locale.toString() + ": ";
    outputString = outputString + nf.format(573.34) + "\n";
}
```

以下是此示例的屏幕截图：

![Screenshot of Sample ThaiDigits.java](https://docs.oracle.com/javase/tutorial/figures/i18n/locale/thaidigits.jpg)

### BCP 47 扩展

Java SE 7版本符合IETF BCP 47标准，该标准支持向`Locale`添加扩展。任何单个字符都可用于表示扩展名，但有两个预定义的扩展代码：`'u'`指定Unicode语言环境扩展名，`'x'`指定专用扩展名。

Unicode语言环境扩展由Unicode公共区域设置数据存储库 [Common Locale Data Repository (CLDR)](http://cldr.unicode.org/) 项目定义。它们用于指定非语言特定的信息，例如日历或货币。私有扩展可用于指定任何其他信息，例如平台（例如，Windows，UNIX或Linux）或发布信息（例如，6u23或JDK 7）。

扩展名被指定为键/值对，其中键是单个字符（通常为 `'u'` 或 `'x'`）。格式良好的值具有以下格式：

```
SUBTAG ('-' SUBTAG)*
```

此格式中：

```
SUBTAG = [0-9a-zA-Z]{2,8}    For key='u'
SUBTAG = [0-9a-zA-Z]{1,8}    For key='x'
```

请注意，私有扩展允许使用单字符值。但是，Unicode语言环境扩展中的值最小为2个字符。

扩展字符串不区分大小写，但`Locale`类将所有键和值映射为小写。

[`getExtensionKeys()`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#getExtensionKeys--) 方法返回`Locale`的扩展键集（如果有）。[`getExtension(key)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#getExtension-char-) 方法返回指定键的值字符串（如果有）。

**Unicode Locale 扩展**

如前所述，Unicode语言环境扩展由 `'u'` 键代码或`UNICODE_LOCALE_EXTENSION`常量指定。值本身也由键/类型对指定。合法值在 [Unicode](http://www.unicode.org/) 网站的 [Key/Type Definitions](http://www.unicode.org/reports/tr35/#Key_Type_Definitions) 表中定义。键代码由两个字母字符指定。下表列出了Unicode语言环境扩展键：

| Key Code | Description          |
| -------- | -------------------- |
| ca       | calendar algorithm   |
| co       | collation type       |
| ka       | collation parameters |
| cu       | currency type        |
| nu       | number type          |
| va       | common variant type  |

------

注意：指定Unicode语言环境扩展（例如数字格式）并不保证底层平台的语言环境服务将遵循该请求。

------

下表显示了Unicode语言环境扩展的键/类型对的一些示例。

| Key/Type pair | Description                 |
| ------------- | --------------------------- |
| ca-buddhist   | Thai Buddhist calendar      |
| co-pinyin     | Pinyin ordering for Latin   |
| cu-usd        | U.S. dollars                |
| nu-jpanfin    | Japanese financial numerals |
| tz-aldav      | Europe/Andorra              |

以下字符串表示使用Linux平台的电话簿订购样式的德国所在国家/地区的德语语言环境。此示例还包含名为`"email"`的属性。

```
de-DE-u-email-co-phonebk-x-linux
```

以下`Locale`方法可用于访问有关Unicode语言环境扩展的信息。使用以前的德语语言环境示例描述了这些方法。

- [`getUnicodeLocaleKeys()`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#getUnicodeLocaleKeys--) – 如果语言环境没有，则返回Unicode语言环境键代码或空集。对于德语示例，这将返回包含单个字符串`"co"`的集合。
- [`getUnicodeLocaleType(String)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#getUnicodeLocaleType-java.lang.String-) – 返回与Unicode语言环境键代码关联的Unicode语言环境类型。为德语示例调用 `getUnicodeLocaleType("co")` 将返回字符串`"phonebk"`。
- [`getUnicodeLocaleAttributes()`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#getUnicodeLocaleAttributes--) – 返回与此语言环境关联的Unicode语言环境属性集（如果有）。在德语示例中，这将返回包含单个字符串 `"email"`的集合。

**私有用途扩展**

由`'x'`键代码或`PRIVATE_USE_EXTENSION`常量指定的私有使用扩展名可以是任何内容，只要该值格式良好即可。

以下是可能的私有使用扩展的示例：

```
x-jdk-1-7
x-linux
```

### 识别可用的区域设置

您可以使用有效语言和国家/地区代码的任意组合创建区域设置，但这并不意味着您可以使用它。请记住，`Locale`对象只是一个标识符。您将`Locale`对象传递给其他对象，然后执行实际工作。这些其他对象，我们称之为区域设置敏感的，不知道如何处理所有可能的`Locale`定义。

要查找区域设置敏感类可识别的区域设置定义类型，请调用`getAvailableLocales`方法。例如，要找出`DateFormat`类支持哪些`Locale`定义，您可以编写如下例程：

```java
import java.util.*;
import java.text.*;

public class Available {
    static public void main(String[] args) {
        Locale list[] = DateFormat.getAvailableLocales();
        for (Locale aLocale : list) {
            System.out.println(aLocale.toString());
        }
    }
}
```

请注意，`toString`返回的字符串包含语言和国家/地区代码，用下划线分隔：

```
ar_EG
be_BY
bg_BG
ca_ES
cs_CZ
da_DK
de_DE
...
```

如果要向最终用户显示区域设置名称列表，您应该向它们展示比`toString`返回的语言和国家/地区代码更容易理解的内容。您可以调用`Locale.getDisplayName`方法，该方法检索`Locale`对象的本地化`String`。例如，当前面的代码中的`toString`被`getDisplayName`替换时，程序将打印以下行：

```
Arabic (Egypt)
Belarussian (Belarus)
Bulgarian (Bulgaria)
Catalan (Spain)
Czech (Czech Republic)
Danish (Denmark)
German (Germany)
...
```

您可能会看到不同的区域设置列表，具体取决于Java平台实现。

### 语言标签过滤和查找

Java编程语言包含对语言标记，语言标记过滤和语言标记查找的国际化支持。这些功能由 [IETF BCP 47](http://tools.ietf.org/html/bcp47) 指定，其中包含 [RFC 5646 "Tags for Identifying Languages"](http://tools.ietf.org/html/rfc5646) 和 [RFC 4647 "Matching of Language Tags."](http://tools.ietf.org/html/rfc4647) 。本课程描述了如何在JDK中提供此支持。

**什么是语言标签？**

语言标签是特殊格式的字符串，提供有关特定语言的信息。语言标签可能是简单的（例如英语的“en”），也可能是复杂的（例如中文使用的“zh-cmn-Hans-CN”，普通话，简体中文），或介于两者之间的（ 例如“sr-Latn”，用拉丁文写成的塞尔维亚语）。语言标签由连字符分隔的“子标签”组成，在整个API文档中使用此术语。

[`java.util.Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 类提供对语言标记的支持。`Locale`包含几个不同的字段：语言（例如英语的“en”或日语的“ja”），脚本（例如拉丁语的“Latn”或西里尔语的“Cyrl”），国家（例如“US”表示 美国或法国的“FR”），变体（表示某种语言环境的变体）和扩展（它提供单个字符键到`String`值的映射，表示除语言标识之外的扩展）。要从语言标记`String`创建`Locale`对象，请调用 [`Locale.forLanguageTag(String)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#forLanguageTag-java.lang.String-) ，并将语言标记作为唯一参数传入。这样做会创建并返回一个新的`Locale`对象，以便在您的应用程序中使用。

例子1：

```java
package languagetagdemo;

import java.util.Locale;

public class LanguageTagDemo {
     public static void main(String[] args) {
         Locale l = Locale.forLanguageTag("en-US");
     }
}
```

请注意，Locale API仅要求您的语言标记在语法上格式良好。它不执行任何额外验证（例如检查标签是否在IANA语言子标签注册表中注册）。

**什么是语言范围？**

语言范围（由类 [`java.util.Locale.LanguageRange`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.LanguageRange.html) 表示）标识共享特定属性的语言标记集。语言范围分为基本或扩展，与语言标签类似，因为它们由连字符分隔的子标签组成。基本语言范围的示例包括“en”（英语），“ja-JP”（日语，日语）和“”（与任何语言标签匹配的特殊语言范围）。扩展语言范围的示例包括“-CH”（任何语言，瑞士），“es-”（西班牙语，任何地区）和“zh-Hant-”（繁体中文，任何地区）。

此外，语言范围可以存储在语言优先级列表中，这使得用户能够在加权列表中优先考虑他们的语言偏好。语言优先级列表通过将`LanguageRange`对象放入`java.util.List`来表示，然后可以将其传递给接受`LanguageRange`对象`List`的`Locale`方法。

**创建语言范围**

[`Locale.LanguageRange`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.LanguageRange.html) 类提供了两种不同的构造器来创建语言范围：

- `public Locale.LanguageRange(String range)`
- `public Locale.LanguageRange(String range, double weight)`

它们之间的唯一区别是第二个版本允许指定权重；如果将范围放入语言优先级列表，则将考虑此权重。

`Locale.LanguageRange`还指定了一些与这些构造函数一起使用的常量：

- `public static final double MAX_WEIGHT`
- `public static final double MIN_WEIGHT`

The `MAX_WEIGHT` constant holds a value of 1.0, which indicates that it is a good fit for the user. The `MIN_WEIGHT` constant holds a value of 0.0, indicating that it is not.

`MAX_WEIGHT`常量值为1.0，表示它非常适合用户。`MIN_WEIGHT`常量值为0.0，表示不适合用户。

例子2：

```java
package languagetagdemo;

import java.util.Locale;

public class LanguageTagDemo {

     public static void main(String[] args) {
         // Create Locale
         Locale l = Locale.forLanguageTag("en-US");

         // Define Some LanguageRange Objects
         Locale.LanguageRange range1 = new Locale.LanguageRange("en-US",Locale.LanguageRange.MAX_WEIGHT);
         Locale.LanguageRange range2 = new Locale.LanguageRange("en-GB*",0.5);
         Locale.LanguageRange range3 = new Locale.LanguageRange("fr-FR",Locale.LanguageRange.MIN_WEIGHT);
     }
}
```

示例2创建了三种语言范围：英语（美国），英语（英国）和法语（法国）。按照从最优选到最不优选的顺序对这些范围进行加权以表示用户的偏好。

**创建语言优先级列表**

您可以使用 [`LanguageRange.parse(String)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.LanguageRange.html#parse-java.lang.String-) 方法从语言范围列表中创建语言优先级列表。此方法接受逗号分隔语言范围列表，对给定范围内的每个语言范围执行语法检查，然后返回新创建的语言优先级列表。

有关“范围”参数所需格式的详细信息，请参阅此方法的API规范。

例子3：

```java
package languagetagdemo;

import java.util.Locale;

import java.util.List;

public class LanguageTagDemo {

    public static void main(String[] args) {

        // Create Locale

        Locale l = Locale.forLanguageTag("en-US");

        // Create a Language Priority List

        String ranges = "en-US;q=1.0,en-GB;q=0.5,fr-FR;q=0.0";

        List<Locale.LanguageRange> languageRanges = Locale.LanguageRange.parse(ranges)

    }
}
```

示例3创建与示例2相同的三种语言范围，但将它们存储在`String`对象中，该对象将传递给 `parse(String)` 方法。返回的`LanguageRange`对象列表是语言优先级列表。

**过滤语言标签**

语言标记过滤是将一组语言标记与用户的语言优先级列表进行匹配的过程。过滤结果将是所有匹配结果的完整列表。 `Locale`类定义了两个返回`Locale`对象列表的过滤器方法。他们的方法签名如下：

- [`public static List filter (List priorityList, Collection locales)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#filter-java.util.List-java.util.Collection-)
- [`public static List filter (List priorityList, Collection locales, Locale.FilteringMode mode)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#filter-java.util.List-java.util.Collection-java.util.Locale.FilteringMode-)

在这两种方法中，第一个参数指定用户的语言优先级列表，如上一节中所述。

第二个参数指定要匹配的`Locale`对象的集合。匹配本身将根据RFC 4647指定的规则进行。

第三个参数（如果提供）指定要使用的“过滤模式”。[`Locale.FilteringMode`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.FilteringMode.html) 枚举提供了许多不同的值可供选择，例如`AUTOSELECT_FILTERING`（用于基本语言范围过滤）或`EXTENDED_FILTERING`（用于扩展语言范围过滤）。

示例4提供了语言标记过滤的演示。

例4：

```java
package languagetagdemo;

import java.util.Locale;
import java.util.Collection;
import java.util.List;
import java.util.ArrayList;

public class LanguageTagDemo {

    public static void main(String[] args) {

        // Create a collection of Locale objects to filter
        Collection<Locale> locales = new ArrayList<>();
        locales.add(Locale.forLanguageTag("en-GB"));
        locales.add(Locale.forLanguageTag("ja"));
        locales.add(Locale.forLanguageTag("zh-cmn-Hans-CN"));
        locales.add(Locale.forLanguageTag("en-US"));

        // Express the user's preferences with a Language Priority List
        String ranges = "en-US;q=1.0,en-GB;q=0.5,fr-FR;q=0.0";
        List<Locale.LanguageRange> languageRanges = Locale.LanguageRange.parse(ranges);

        // Now filter the Locale objects, returning any matches
        List<Locale> results = Locale.filter(languageRanges,locales);

        // Print out the matches
        for(Locale l : results){
        System.out.println(l.toString());
        }
    }
}
```

程序的输出：

````
en_US
en_GB
````

此返回列表根据用户的语言优先级列表中指定的权重进行排序。

`Locale`类还定义了`filterTags`方法，用于将语言标记过滤为`String`对象。

方法签名如下：

- [`public static List filterTags (List priorityList, Collection tags)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#filterTags-java.util.List-java.util.Collection-)
- [`public static List filterTags (List priorityList, Collection tags, Locale.FilteringMode mode)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#filterTags-java.util.List-java.util.Collection-java.util.Locale.FilteringMode-)

示例5提供与示例4相同的搜索，但使用`String`对象而不是`Locale`对象。

例5：

```java
package languagetagdemo;

import java.util.Locale;
import java.util.Collection;
import java.util.List;
import java.util.ArrayList;

public class LanguageTagDemo {

    public static void main(String[] args) {

        // Create a collection of String objects to match against
        Collection<String> tags = new ArrayList<>();
        tags.add("en-GB");
        tags.add("ja");
        tags.add("zh-cmn-Hans-CN");
        tags.add("en-US");

        // Express user's preferences with a Language Priority List
        String ranges = "en-US;q=1.0,en-GB;q=0.5,fr-FR;q=0.0";
        List<Locale.LanguageRange> languageRanges = Locale.LanguageRange.parse(ranges);

        // Now search the locales for the best match
        List<String> results = Locale.filterTags(languageRanges,tags);

        // Print out the matches
        for(String s : results){
            System.out.println(s);
        }
    }
} 
```

和以前一样，搜索将匹配并返回“en-US”和“en-GB”（按此顺序）。

**执行语言标签查找**

与语言标记过滤相反，语言标记查找是将语言范围与语言标记集匹配并返回与该范围最匹配的一种语言标记的过程。RFC4647声明：“查找从可用标记列表中生成最符合用户首选项的单个结果，因此在需要单个项目（并且只能返回单个项目）的情况下，它非常有用。例如，如果一个进程要将一个人类可读的错误消息插入到协议头中，它可能会根据用户的语言优先级列表选择文本。由于该进程只能返回一个项目，因此它被强制选择一个项目， 它必须返回一些项目，即使内容的语言标签都没有与用户提供的语言优先级列表相匹配。“

例6：

```java
package languagetagdemo;

import java.util.Locale;
import java.util.Collection;
import java.util.List;
import java.util.ArrayList;

public class LanguageTagDemo {

    public static void main(String[] args) {

        // Create a collection of Locale objects to search
        Collection<Locale> locales = new ArrayList<>();
        locales.add(Locale.forLanguageTag("en-GB"));
        locales.add(Locale.forLanguageTag("ja"));
        locales.add(Locale.forLanguageTag("zh-cmn-Hans-CN"));
        locales.add(Locale.forLanguageTag("en-US"));

        // Express the user's preferences with a Language Priority List
        String ranges = "en-US;q=1.0,en-GB;q=0.5,fr-FR;q=0.0";
        List<Locale.LanguageRange> languageRanges = Locale.LanguageRange.parse(ranges);

        // Find the BEST match, and return just one result
        Locale result = Locale.lookup(languageRanges,locales);
        System.out.println(result.toString());
    }
}
```

与过滤示例相反，示例6中的查找演示返回最匹配的一个对象（在本例中为`en-US`）。为了保证完整性，示例7显示了如何使用`String`对象执行相同的查找。

例7：

```java
package languagetagdemo;

import java.util.Locale;
import java.util.Collection;
import java.util.List;
import java.util.ArrayList;

public class LanguageTagDemo {

    public static void main(String[] args) {
        // Create a collection of String objects to match against
        Collection<String> tags = new ArrayList<>();
        tags.add("en-GB");
        tags.add("ja");
        tags.add("zh-cmn-Hans-CN");
        tags.add("en-US");

        // Express user's preferences with a Language Priority List
        String ranges = "en-US;q=1.0,en-GB;q=0.5,fr-FR;q=0.0";
        List<Locale.LanguageRange> languageRanges = Locale.LanguageRange.parse(ranges);

        // Find the BEST match, and return just one result
        String result = Locale.lookupTag(languageRanges, tags);
        System.out.println(result);
    }
} 
```

此示例返回与用户的语言优先级列表最匹配的单个对象。

### Locale 的作用域

Java平台不要求您在整个程序中使用相同的`Locale`。如果愿意，可以为程序中的每个区域设置敏感对象分配不同的`Locale`。这种灵活性允许您开发多语言应用程序，可以显示多种语言的信息。

但是，大多数应用程序不是多语言的，它们的区域设置敏感对象依赖于默认的`Locale`。由Java虚拟机启动时设置，默认`Locale`对应于主机平台的区域设置。要确定Java虚拟机的默认`Locale`，请调用`Locale.getDefault`方法。

----

**注意：** 可以为两种类型的用途独立设置默认语言环境：格式设置用于格式化资源，显示设置用于菜单和对话框。在Java SE 7发行版中，[`Locale.getDefault(Locale.Category)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#getDefault-java.util.Locale.Category-) 方法采用 [`Locale.Category`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.Category.html) 参数。将`FORMAT`枚举传递给`getDefault(Locale.Category)` 方法将返回格式化资源的默认语言环境。同样，传递`DISPLAY`枚举返回UI使用的默认语言环境。相应的 [`setDefault(Locale.Category, Locale)`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html#setDefault-java.util.Locale.Category-java.util.Locale-) 方法允许设置所需类别的区域设置。无参数`getDefault`方法返回`DISPLAY`默认值。

在Windows平台上，根据Windows控制面板中的“标准和格式”和“显示语言”设置初始化这些默认值。

---

您不应以编程方式设置默认 `Locale` ，因为它由所有区域设置敏感类共享。

分布式计算提出了一些有趣的问题。例如，假设您正在设计一个应用程序服务器，它将接收来自不同国家/地区的客户端的请求。如果每个客户端的区域设置不同，那么服务器的区域设置应该是什么？也许服务器是多线程的，每个线程都设置为它所服务的客户端的`Locale`。或者，服务器和客户端之间传递的所有数据都应该是与语言环境无关的。

你应该选择哪种设计方法？如果可能，服务器和客户端之间传递的数据应该与语言环境无关。这通过使客户端负责以区域设置敏感的方式显示数据来简化服务器的设计。但是，如果服务器必须以特定于语言环境的形式存储数据，则此方法将不起作用。例如，服务器可能将相同数据的西班牙语，英语和法语版本存储在不同的数据库列中。在这种情况下，服务器可能希望查询客户端的`Locale`，因为`Locale`可能自上次请求以来已更改。

### 区域敏感服务SPI

此功能启用与区域设置相关的数据和服务的插件。通过这种方式，第三方能够在`java.text`和`java.util`包中提供大多数区域设置敏感类的实现。

SPI（服务提供者接口）的实现基于由服务提供者实现的抽象类和Java接口。在运行时，Java类加载机制用于动态定位和加载实现SPI的类。

您可以使用区域设置敏感服务SPI来提供以下区域设置敏感实现：

- `BreakIterator` 对象
- `Collator` 对象
- `Locale`类的语言代码，国家/地区代码和变体名称
- 时区名称
- 货币符号
- `DateFormat` 对象
- `DateFormatSymbol` 对象
- `NumberFormat` 对象
- `DecimalFormatSymbols` 对象

相应的SPI包含在`java.text.spi`和`java.util.spi`包中：

| `java.util.spi`                          | `java.text.spi`                          |
| ---------------------------------------- | ---------------------------------------- |
| `CurrencyNameProvider`<br />`LocaleServiceProvider`<br />`TimeZoneNameProvider`<br />`CalendarDataProvider` | `BreakIteratorProvider`<br />`CollatorProvider`<br />`DateFormatProvider`<br />`DateFormatSymbolsProvider`<br />`DecimalFormatSymbolsProvider`<br />`NumberFormatProvider` |

例如，如果要为新语言环境提供`NumberFormat`对象，则必须实现`java.text.spi.NumberFormatProvider`类。您需要扩展此类并实现其方法：

- `getCurrencyInstance(Locale locale)`
- `getIntegerInstance(Locale locale)`
- `getNumberInstance(Locale locale)`
- `getPercentInstance(Locale locale)`

```java
Locale loc = new Locale("da", "DK");
NumberFormat nf = NumberFormatProvider.getNumberInstance(loc);
```

这些方法首先检查Java运行时环境是否支持所请求的语言环境; 如果是这样，他们会使用这种支持。否则，这些方法会调用已安装提供程序的 `getAvailableLocales()` 方法以获取相应的接口，以查找支持所请求区域设置的提供程序。

## 隔离特定于语言的数据

必须根据最终用户的语言和区域的惯例来定制特定于语言环境的数据。用户界面显示的文本是区域设置特定数据的最明显示例。例如，在美国使用“Cancel”按钮的应用程序将在德国具有“Abbrechen”按钮。在其他国家/地区，此按钮将包含其他标签。显然你不想硬编码这个按钮标签。如果你能自动为给定的`Locale`获取正确的标签，那不是很好吗？幸运的是，只要您在`ResourceBundle`中隔离特定于语言环境的对象，就可以。

在本课程中，您将学习如何创建和访问`ResourceBundle`对象。如果您急于查看一些编码示例，请继续查看本课程的最后两节。然后，您可以回到前两个部分以获取有关`ResourceBundle`对象的一些概念性信息。

[关于 ResourceBundle 类](https://docs.oracle.com/javase/tutorial/i18n/resbundle/concept.html)

`ResourceBundle`对象包含特定于语言环境的对象。当您需要特定于语言环境的对象时，可以从`ResourceBundle`获取它，该`ResourceBundle`返回与最终用户的`Locale`匹配的对象。本节介绍`ResourceBundle`如何与`Locale`相关，并描述`ResourceBundle`子类。

[准备使用 ResourceBundle](https://docs.oracle.com/javase/tutorial/i18n/resbundle/prepare.html)

在创建`ResourceBundle`对象之前，您应该做一些计划。首先，确定程序中特定于语言环境的对象。然后将它们组织成类别并相应地将它们存储在不同的`ResourceBundle`对象中。

[用属性文件作为 ResourceBundle 的后备](https://docs.oracle.com/javase/tutorial/i18n/resbundle/propfile.html)

如果您的应用程序包含需要翻译成各种语言的`String`对象，则可以将这些`String`对象存储在`PropertyResourceBundle`中，该对象由一组属性文件备份。由于属性文件是简单的文本文件，因此翻译人员可以创建和维护这些文件。您不必更改源代码。在本节中，您将学习如何设置备份`PropertyResourceBundle`的属性文件。

[使用 ListResourceBundle](https://docs.oracle.com/javase/tutorial/i18n/resbundle/list.html)

`ListResourceBundle`类是`ResourceBundle`的子类，它使用列表管理特定于语言环境的对象。`ListResourceBundle`由类文件支持，这意味着每次需要支持其他语言环境时，您必须编写和编译新的源文件。但是，`ListResourceBundle`对象很有用，因为与属性文件不同，它们可以存储任何类型的特定于语言环境的对象。通过单步执行示例程序，本节演示了如何使用`ListResourceBundle`。

[自定义 Resource Bundle 加载](https://docs.oracle.com/javase/tutorial/i18n/resbundle/control.html)

本节介绍了改进`ResourceBundle.getBundle`工厂灵活性的新功能。`ResourceBundle.Control`类与用于加载资源包的工厂方法协作。这允许将资源包加载过程的每个步骤及其高速缓存控制视为单独的方法。

### 关于 ResourceBundle 类

**ResourceBundle 如何关联到 Locale**

从概念上讲，每个`ResourceBundle`是一组共享相同基本名称的相关子类。下面的列表显示了一组相关的子类。`ButtonLabel`是基本名称。基本名称后面的字符表示语言代码，国家/地区代码和`Locale`的变体。例如，`ButtonLabel_en_GB`匹配由英语（`en`）的语言代码和英国的国家代码（`GB`）指定的`Locale`。

```
ButtonLabel
ButtonLabel_de
ButtonLabel_en_GB
ButtonLabel_fr_CA_UNIX
```

要选择适当的`ResourceBundle`，请调用`ResourceBundle.getBundle`方法。下面的示例为与语言为“法语”，国家为“加拿大”和平台为UNIX匹配的`Locale`选择`ButtonLabel``ResourceBundle`。

```java
Locale currentLocale = new Locale("fr", "CA", "UNIX");
ResourceBundle introLabels = ResourceBundle.getBundle(
                                 "ButtonLabel", currentLocale);
```

如果指定的`Locale`的`ResourceBundle`类不存在，`getBundle`尝试找到最接近的匹配。例如，如果`ButtonLabel_fr_CA_UNIX`是所需的类，默认的`Locale`是`en_US`，`getBundle`将按以下顺序查找类：

```
ButtonLabel_fr_CA_UNIX
ButtonLabel_fr_CA
ButtonLabel_fr
ButtonLabel_en_US
ButtonLabel_en
ButtonLabel
```

请注意，`getBundle`在选择基类（`ButtonLabel`）之前，根据默认的`Locale`查找类。如果`getBundle`在前面的类列表中找不到匹配项，它会抛出一个`MissingResourceException`。为避免抛出此异常，应始终提供不带后缀的基类。

**`ListResourceBundle` 和 `PropertyResourceBundle`子类**

抽象类`ResourceBundle`有两个子类：`PropertyResourceBundle`和`ListResourceBundle`。

`PropertyResourceBundle`由属性文件支持。属性文件是包含可翻译文本的纯文本文件。属性文件不是Java源代码的一部分，它们只能包含`String`对象的值。如果需要存储其他类型的对象，请使用`ListResourceBundle`。 [使用属性文件备份ResourceBundle](https://docs.oracle.com/javase/tutorial/i18n/resbundle/propfile.html) 部分向您展示了如何使用`PropertyResourceBundle`。

`ListResourceBundle`类使用方便的列表管理资源。每个`ListResourceBundle`都由一个类文件支持。您可以将任何特定于语言环境的对象存储在`ListResourceBundle`中。要添加对其他`Locale`的支持，请创建另一个源文件并将其编译为类文件。 [使用ListResourceBundle](https://docs.oracle.com/javase/tutorial/i18n/resbundle/list.html) 部分有一个您可能会觉得有帮助的编码示例。

`ResourceBundle`类很灵活。 如果您首先将特定于语言环境的`String`对象放在`PropertyResourceBundle`中，然后决定使用`ListResourceBundle`，那么对您的代码没有任何影响。例如，以下对`getBundle`的调用将为适当的`Locale`检索`ResourceBundle`，无论`ButtonLabel`是由类还是属性文件备份：

```java
ResourceBundle introLabels = ResourceBundle.getBundle(
                                 "ButtonLabel", currentLocale);
```

**键值对**

`ResourceBundle`对象包含一组键值对。当你想从`ResourceBundle`中检索值时，你指定键，它必须是`String`。该值是特定于语言环境的对象。以下示例中的键是`OkKey`和`CancelKey`字符串：

```java
class ButtonLabel_en extends ListResourceBundle {
    // English version
    public Object[][] getContents() {
        return contents;
    }
    static final Object[][] contents = {
        {"OkKey", "OK"},
        {"CancelKey", "Cancel"},
    };
}
```

要从`ResourceBundle`检索`OK` `String`，您可以在调用`getString`时指定相应的键：

```java
String okLabel = ButtonLabel.getString("OkKey");
```

属性文件包含键值对。键位于等号的左侧，值位于右侧。每对都在单独一行上。值可以仅表示“String”对象。以下示例显示名为`ButtonLabel.properties`的属性文件的内容：

```
OkKey = OK
CancelKey = Cancel
```
### 准备使用 ResourceBundle 

**识别特定于语言的对象**

如果你的应用拥有一个用户界面，则它就包含很多特定于语言的对象。一开始，你应该通读你的源码来查找会随着`Locale`变化的对象。这些对象可能包含从以下类从实例化而来的对象：

- `String`
- `Image`
- `Color`
- `AudioClip`

你将注意到这个对象列表不包含表示数字、日期或者国家的对象。这些对象的显示会随着`Locale`变化，但是对象本身并不会变化。比如，你根据`Locale`格式化显示`Date`，但是无论`Locale`如何变化，你使用的都是同一个`Date`对象。这些对象就不能隔离到`ResourceBundle`中，而是使用特殊的语言敏感格式化类对它们进行格式化显示。你将在 [格式化](https://docs.oracle.com/javase/tutorial/i18n/format/index.html) 课程中 [日期和时间](https://docs.oracle.com/javase/tutorial/i18n/format/dateintro.html) 章节中学到如何做到这一点。

通常，这些保存在`ResourceBundle`中的对象都是预定义并随着产品发布的。这些对象在程序运行时不会变化。比如，你可以保存一个`Menu`标签到`ResourceBundle`中，因为它是特定于语言的，而且在程序运行起见不会发生变化。但是，你不应该将终端用户在`TextField`中输入的`String`对象放入`ResourceBundle`中，因为这种`String`会经常变化。它特定于程序的具体运行过程，而不是特定于程序运行环境的`Locale`设置。

通常，大多数你需要隔离到`ResourceBundle`中的对象都是`String`对象。不过，并不是所有的`String`对象都是特定于语言的。比如，如果一个`String`是一个交互过程使用的协议元素，它就不需要进行本地化，因为终端用户永远不会看到它。

某些`String`对象是否需要本地化并不是非常明显。日志文件就是个很好的例子。如果日志文件由一个程序写入而由另外一个程序读取，两个程序将日志文件作为通信的缓冲池。假定终端用户偶然想要检查该文件内容，那么该文件是否需要本地化？另一方面，如果终端用户很好检查该日志文件，则翻译就是得不偿失的。确定是否本地化该日志文件取决于几个因素：程序设计，使用便利性，翻译成本以及平台可支持性。

**组织 ResourceBundle 对象**

你可以按照所包含的对象类别将你的`ResourceBundle`对象分类。比如，你可能会希望加载一个订单入口窗口的所有的 GUI 标签到一个名为`OrderLabelsBundle`的`ResourceBundle`中。使用多个`ResourceBundle`对象有几个好处：

- 代码便于阅读和维护。
- 可以编码巨大的 `ResourceBundle` 对象，它可能需要很长时间来载入内存。
- 可以按需加载`ResourceBundle`从而减少内存占用。


### 使用属性文件作为 ResourceBundle 后备

本小节逐步讲解名为 [`PropertiesDemo`](https://docs.oracle.com/javase/tutorial/i18n/resbundle/examples/PropertiesDemo.java) 的示例程序。

**1. 创建默认 Properties 文件**

属性文件是一个简单的文本文件。你可以使用任何文本编辑器创建并维护属性文件。

你应该始终都创建默认属性文件。文件名以你的`ResourceBundle`基本名称开头并以`.properties`作为后缀。在`PropertiesDemo`程序中，该基本名称是`LabelBundle`。因而默认属性文件就叫做`LabelsBundle.properties`。该文件包含以下行：

```
# This is the default LabelsBundle.properties file
s1 = computer
s2 = disk
s3 = monitor
s4 = keyboard
```

请注意，在前面的文件中，注释行以井号（＃）开头。其他行包含键值对。键位于等号的左侧，值位于右侧。例如，`s2`是与值`disk`对应的键。键是任意的。我们可以叫它`s2`或者其他东西，比如`msg5`或`diskID`。但是，一旦定义，键就不应该改变，因为它在源代码中被引用。值可能会更改。实际上，当本地化程序员创建新属性文件以容纳其他语言时，他们会将值翻译为各种语言。

**2. 按需创建额外的 Properties 文件**

要支持其他语言环境，本地化程序员将创建一个包含已翻译值的新属性文件。不需要更改源代码，因为您的程序引用了键而不是值。

例如，要添加对德语的支持，您的本地化程序员将转换`LabelsBundle.properties`中的值，并将它们放在名为`LabelsBundle_de.properties`的文件中。请注意，此文件的名称（如默认文件的名称）以基本名称`LabelsBundle`开头，以`.properties`后缀结尾。但是，由于此文件适用于特定的`Locale`，因此基本名称后跟语言代码（de）。`LabelsBundle_de.properties`的内容如下：

```
# This is the LabelsBundle_de.properties file
s1 = Computer
s2 = Platte
s3 = Monitor
s4 = Tastatur
```

`PropertiesDemo` 示例程序连同下面3个属性文件一起发布：

```
LabelsBundle.properties
LabelsBundle_de.properties
LabelsBundle_fr.properties
```

**3. 指定 Locale**

`PropertiesDemo` 程序创建 `Locale` 对象如下：

```java
Locale[] supportedLocales = {
    Locale.FRENCH,
    Locale.GERMAN,
    Locale.ENGLISH
};
```

这些`Locale`对象应与前两个步骤中创建的属性文件匹配。例如，`Locale.FRENCH`对象对应于`LabelsBundle_fr.properties`文件。`Locale.ENGLISH`没有匹配的`LabelsBundle_en.properties`文件，因此将使用默认文件。

**4. 创建 ResourceBundle**

此步骤显示`Locale`，属性文件和`ResourceBundle`的关联方式。要创建`ResourceBundle`，请调用`getBundle`方法，指定基本名称和`Locale`：

```java
ResourceBundle labels = ResourceBundle.getBundle("LabelsBundle", currentLocale);
```

`getBundle`方法首先查找与基本名称和`Locale`匹配的类文件。如果找不到类文件，则检查属性文件。在`PropertiesDemo`程序中，我们使用属性文件而不是类文件来支持`ResourceBundle`。当`getBundle`方法找到正确的属性文件时，它返回一个`PropertyResourceBundle`对象，该对象包含属性文件中的键值对。

**5. 获取本地化的文本**

要从`ResourceBundle`检索已翻译的值，请按如下方式调用`getString`方法：

```java
String value = labels.getString(key);
```

`getString`返回的`String`对应于指定的键。如果存在指定区域设置的属性文件，则`String`使用正确的语言。

**6. 遍历所有的键**

此步骤是可选的。调试程序时，您可能希望获取`ResourceBundle`中所有键的值。`getKeys`方法返回`ResourceBundle`中所有键的`Enumeration`。您可以遍历`Enumeration`并使用`getString`方法获取每个值。以下代码行来自`PropertiesDemo`程序，展示了如何完成此操作：

```java
ResourceBundle labels = ResourceBundle.getBundle("LabelsBundle", currentLocale);
Enumeration bundleKeys = labels.getKeys();

while (bundleKeys.hasMoreElements()) {
    String key = (String)bundleKeys.nextElement();
    String value = labels.getString(key);
    System.out.println("key = " + key + ", " + "value = " + value);
}
```

**7. 运行示例程序**

运行`PropertiesDemo`程序会生成以下输出。前三行显示`getString`为各种`Locale`对象返回的值。当使用`getKeys`方法迭代键时，程序显示最后四行。

```
Locale = fr, key = s2, value = Disque dur
Locale = de, key = s2, value = Platte
Locale = en, key = s2, value = disk

key = s4, value = Clavier
key = s3, value = Moniteur
key = s2, value = Disque dur
key = s1, value = Ordinateur
```

### 使用 ListResourceBundle

本节说明了`ListResourceBundle`对象与名为`ListDemo`的示例程序的使用。下面的文本解释了创建`ListDemo`程序所涉及的每个步骤，以及支持它的`ListResourceBundle`子类。

**1. 创建 ListResourceBundle 子类**

`ListResourceBundle`由类文件备份。因此，第一步是为每个受支持的`Locale`创建一个类文件。在`ListDemo`程序中，`ListResourceBundle`的基本名称是`StatsBundle`。由于`ListDemo`支持三个`Locale`对象，因此它需要以下三个类文件：

```
StatsBundle_en_CA.class
StatsBundle_fr_FR.class
StatsBundle_ja_JP.class
```

日本的`StatsBundle`类在后面的源代码中定义。请注意，通过将语言和国家/地区代码附加到`ListResourceBundle`的基本名称来构造类名。在类内部，使用键值对初始化二维内容数组。键是每对中的第一个要素：`GDP`，`Population`和`Literacy`。键必须是`String`对象，并且它们在`StatsBundle`集合中的每个类中必须相同。值可以是任何类型的对象。在此示例中，值是两个`Integer`对象和一个`Double`对象。

```java
import java.util.*;
public class StatsBundle_ja_JP extends ListResourceBundle {
    public Object[][] getContents() {
        return contents;
    }

    private Object[][] contents = {
        { "GDP", new Integer(21300) },
        { "Population", new Integer(125449703) },
        { "Literacy", new Double(0.99) },
    };
}
```

**2. 指定 Locale**

`ListDemo` 程序定义 `Locale` 对象如下：

```java
Locale[] supportedLocales = {
    new Locale("en", "CA"),
    new Locale("ja", "JP"),
    new Locale("fr", "FR")
};
```

每个`Locale`对象对应一个`StatsBundle`类。例如，使用`ja`和`JP`代码定义的日语语言环境与`StatsBundle_ja_JP.class`匹配。

**3. 创建 ResourceBundle**

要创建`ListResourceBundle`，请调用`getBundle`方法。以下代码行指定类的基本名称（`StatsBundle`）和`Locale`：

```java
ResourceBundle stats = ResourceBundle.getBundle("StatsBundle", currentLocale);
```

`getBundle`方法搜索名称以`StatsBundle`开头的类，后面跟着指定`Locale`的语言和国家/地区代码。如果使用`ja`和`JP`代码创建`currentLocale`，则`getBundle`返回对应于`StatsBundle_ja_JP`类的`ListResourceBundle`。

**4. 获取本地化的对象**

现在该程序具有适当`Locale`的`ListResourceBundle`，它可以通过其键获取本地化对象。以下代码行通过使用`Literacy`键参数调用`getObject`来检索识字率。由于`getObject`返回一个对象，因此将其强制转换为`Double`：

```java
Double lit = (Double)stats.getObject("Literacy");
```

**5. 运行示例程序**

`ListDemo` 程序打印它通过 `getBundle` 方法获取到的数据：

```
Locale = en_CA
GDP = 24400
Population = 28802671
Literacy = 0.97

Locale = ja_JP
GDP = 21300
Population = 125449703
Literacy = 0.99

Locale = fr_FR
GDP = 20200
Population = 58317450
Literacy = 0.99
```

### 定制化 Resource Bundle 加载

在本课程的前面部分，您学习了如何创建和访问`ResourceBundle`类的对象。本节将扩展您的知识并解释如何从`ResourceBundle.Control`类功能中获益。

创建`ResourceBundle.Control`以指定如何查找和实例化资源包。它定义了一组回调方法，这些方法在资源包加载过程中由`ResourceBundle.getBundle`工厂方法调用。

与前面描述的`ResourceBundle.getBundle`方法不同，此`ResourceBundle.getBundle`方法使用指定的基本名称，默认语言环境和指定的控件定义资源包。

```java
public static final ResourceBundle getBundle(
    String baseName,
    ResourceBundle.Control cont
    // ...
```

指定的控件提供资源包加载过程的信息。

以下示例程序`RBControl.java`说明了如何为中文语言环境定义自己的搜索路径。

**1. 创建 `properties` 文件**

如前所述，您可以从类或属性文件加载资源。 这些文件包含以下语言环境的说明：

- `RBControl.properties` – 全局
- `RBControl_zh.properties` – 只用于语言：简体中文
- `RBControl_zh_cn.properties` – 只用于区域：中国
- `RBControl_zh_hk.properties` – 只用于区域：香港
- `RBControl_zh_tw.properties` – 台湾

在此示例中，应用程序为香港地区创建新的区域设置。

**2. 创建 `ResourceBundle` 实例**

与上一节中的示例一样，此应用程序通过调用`getBundle`方法创建`ResourceBundle`实例：

```java
private static void test(Locale locale) {
    ResourceBundle rb = ResourceBundle.getBundle(
                            "RBControl",
                            locale,
                            new ResourceBundle.Control() {
                                    // ...
                            }
                        );
```

`getBundle`方法使用`RBControl`前缀搜索属性文件。但是，此方法包含`Control`参数，该参数驱动搜索`Chineese`区域设置的过程。

**3. 调用 `getCandidateLocales` 方法**

`getCandidateLocales`方法返回`Locales`对象的列表，作为基本名称和语言环境的候选语言环境。

```java
new ResourceBundle.Control() {
    @Override
    public List<Locale> getCandidateLocales(
                            String baseName,
                            Locale locale) {
                // ...                                        
    }
}
```

默认实现返回`Locale`对象的列表，如下所示：`Locale(language, country)` 。

但是，重写此方法以实现以下特定行为：

```java
if (baseName == null)
    throw new NullPointerException();

if (locale.equals(new Locale("zh", "HK"))) {
    return Arrays.asList(
               locale,
               Locale.TAIWAN,
               // no Locale.CHINESE here
               Locale.ROOT);
} else if (locale.equals(Locale.TAIWAN)) {
    return Arrays.asList(
               locale,
               // no Locale.CHINESE here
               Locale.ROOT);
}
```

请注意，候选语言环境序列的最后一个元素必须是根区域设置。

**4. 调用 `test` 类**

为下面4个不同的区域调用`test`类：

```java
public static void main(String[] args) {
    test(Locale.CHINA);
    test(new Locale("zh", "HK"));
    test(Locale.TAIWAN);
    test(Locale.CANADA);
}
```

**5. 运行示例程序**

你将看到程序输出如下：

```
locale: zh_CN
        region: China
        language: Simplified Chinese
locale: zh_HK
        region: Hong Kong
        language: Traditional Chinese
locale: zh_TW
        region: Taiwan
        language: Traditional Chinese
locale: en_CA
        region: global
        language: English
```

请注意，新创建的分配了香港地区，因为它是在相应的属性文件中指定的。繁体中文被指定为台湾语言。

在`RBControl`示例中没有使用`ResourceBundle.Control`类的另外两个有趣的方法，但它们值得提及。`getTimeToLive`方法用于确定资源包在缓存中可以存在多长时间。如果缓存中资源包的时间限制已过期，则调用`needsReload`方法以确定是否需要重新加载资源包。

## 格式化

本课程介绍如何格式化数字、日期、时间和文本消息。因为终端用户能够看到这些数据元素，它们的格式必须符合各种自然传统。跟随下面的例子你将学会如何做到：

- 以语言敏感的方式格式化数据元素
- 保持代码的语言无关性
- 避免为特殊的语言编写格式化程序

**[数字和货币](https://docs.oracle.com/javase/tutorial/i18n/format/numberintro.html)**

本涨价解释了如何使用 `NumberFormat`, `DecimalFormat`, 和 `DecimalFormatSymbols` 类。

**[日期和时间](https://docs.oracle.com/javase/tutorial/i18n/format/dateintro.html)**

------

**版本提示：** 本章节使用了`java.util`包中的日期和时间 APIs 。而`java.time` APIs 在 JDK 8 中可用，提供了全面的日期和时间模型，是对`java.util`包中相关类的重大改进。`java.time` APIs 描述参见 [Date Time](https://docs.oracle.com/javase/tutorial/datetime/index.html) 章节。[Legacy Date-Time Code](https://docs.oracle.com/javase/tutorial/datetime/iso/legacy.html) 页面可能会有特殊意义。

------

本章节聚焦在 `DateFormat`, `SimpleDateFormat`, 和 `DateFormatSymbols` 类。

**[消息](https://docs.oracle.com/javase/tutorial/i18n/format/messageintro.html)**

本节介绍`MessageFormat`和`ChoiceFormat`类如何帮助您解决格式化文本消息时可能遇到的一些问题。

### 数字和货币

程序以与语言环境无关的方式存储和操作数字。在显示或打印数字之前，程序必须将其转换为区域设置敏感格式的字符串。例如，在法国，数字123456.78的格式应为123 456,78，在德国则应为123.456,78。在本节中，您将学习如何使程序独立于小数点，千位分隔符和其他格式设置属性的语言环境约定。

**[使用预定义格式](https://docs.oracle.com/javase/tutorial/i18n/format/numberFormat.html)**

使用`NumberFormat`类提供的工厂方法，您可以获取数字，货币和百分比的特定于语言环境的格式。

**[使用模式格式化](https://docs.oracle.com/javase/tutorial/i18n/format/decimalFormat.html)**

使用`DecimalFormat`类，您可以使用`String`模式指定数字的格式。`DecimalFormatSymbols`类允许您修改格式符号，如小数分隔符和减号。

#### 使用预定义格式

通过调用由 [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 类提供的方法，你可以根据 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 格式化数字、货币和百分比。接下来举例说明格式化技术的程序名为 [`NumberFormatDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/NumberFormatDemo.java) 。

**数字**

你可以使用 [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 方法来格式化基本类型的数字，比如`double`，以及它们对应的包装对象，比如 [`Double`](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html) 。

下面的例子代码根据 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 格式化 [`Double`](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html) ，调用 [`getNumberInstance`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html#getNumberInstance-java.util.Locale-) 方法返回一个特定于语言的 [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 实例。其中的 [`format`](https://docs.oracle.com/javase/8/docs/api/java/text/Format.html#format-java.lang.Object-) 方法接受 [`Double`](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html) 作为参数并返回 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 形式的格式化数字。

```java
static public void displayNumber(Locale currentLocale) {

    Integer quantity = new Integer(123456);
    Double amount = new Double(345987.246);
    NumberFormat numberFormatter;
    String quantityOut;
    String amountOut;

    numberFormatter = NumberFormat.getNumberInstance(currentLocale);
    quantityOut = numberFormatter.format(quantity);
    amountOut = numberFormatter.format(amount);
    System.out.println(quantityOut + "   " + currentLocale.toString());
    System.out.println(amountOut + "   " + currentLocale.toString());
}
```

此示例打印以下内容，它显示了相同数字的格式如何随`Locale`而变化：

```
123 456   fr_FR
345 987,246   fr_FR
123.456   de_DE
345.987,246   de_DE
123,456   en_US
345,987.246   en_US
```

**使用阿拉伯数字以外的数字形状**

默认情况下，当文本包含数字值时，将使用阿拉伯数字显示这些值。如果首选其他`Unicode`数字形状，请使用 [`java.awt.font.NumericShaper`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html) 类。`NumericShaper` API使您可以在任何`Unicode`数字形状中显示内部表示为ASCII值的数值。 有关详细信息，请参阅 [将拉丁数字转换为其他Unicode数字](https://docs.oracle.com/javase/tutorial/i18n/text/shapedDigits.html) 。

此外，某些区域设置具有变体代码，这些代码指定使用Unicode数字形状代替阿拉伯数字，例如泰语的区域设置。有关更多信息，请参阅 [创建区域设置](https://docs.oracle.com/javase/tutorial/i18n/locale/create.html) 中的 [变体代码](https://docs.oracle.com/javase/tutorial/i18n/locale/create.html#variant-code) 部分。

**货币**

如果您正在编写业务应用程序，则可能需要格式化和显示货币。您可以使用与数字相同的方式格式化货币，但调用 [`getCurrencyInstance`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html#getCurrencyInstance-java.util.Locale-) 以创建格式化器除外。当您调用 [`format`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html#format-double-) 方法时，它返回一个 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) ，其中包含格式化的数字和相应的货币符号。

下面的例子代码展示了如何以特定于语言的方式格式化货币：

```java
static public void displayCurrency( Locale currentLocale) {

    Double currencyAmount = new Double(9876543.21);
    Currency currentCurrency = Currency.getInstance(currentLocale);
    NumberFormat currencyFormatter = 
        NumberFormat.getCurrencyInstance(currentLocale);

    System.out.println(
        currentLocale.getDisplayName() + ", " +
        currentCurrency.getDisplayName() + ": " +
        currencyFormatter.format(currencyAmount));
}
```

上面程序输出：

```
French (France), Euro: 9 876 543,21 €
German (Germany), Euro: 9.876.543,21 €
English (United States), US Dollar: $9,876,543.21
```

乍一看，这个输出可能看起来不对，因为数值都是一样的。当然，9 876 543,21€ 不等于 $9,876,543.21。但是，请记住， [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 类不知道汇率。属于 [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 类的方法格式化货币但不转换它们。

请注意， [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 类的设计使得任何给定货币永远不会有多个 [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 实例。因此，没有公共构造函数。如前面的代码示例所示，您使用 [`getInstance`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html#getInstance-java.util.Locale-) 方法获取 [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 实例。

例子 [`InternationalizedMortgageCalculator.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/InternationalizedMortgageCalculator.java) 同样举例说明了如何使用 [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 类。（注意这个示例代码不会转化货币值。）下面使用 en-US 语言设置：

![Mortgage Calculator, en-US locale](https://docs.oracle.com/javase/tutorial/figures/i18n/format/mortgage-calculator-en-us.jpg)

下面使用了 en-UK 语言设置：

![Mortgage Calculator, en-UK locale](https://docs.oracle.com/javase/tutorial/figures/i18n/format/mortgage-calculator-en-uk.jpg)

例子 [`InternationalizedMortgageCalculator.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/InternationalizedMortgageCalculator.java) 需要以下资源文件：

- [`resources/Resources.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/resources/Resources.properties)
- [`resources/Resources_ar.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/resources/Resources_ar.properties)
- [`resources/Resources_fr.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/resources/Resources_fr.properties)

[`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 类包含其它方法可以检索其它货币相关信息：

- [`getAvailableCurrencies`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html#getAvailableCurrencies--) : 返回 JDK 中所有可用的货币

- [`getCurrencyCode`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html#getCurrencyCode--) : 返回 [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 实例的 ISO 4217 数字代码

- [`getSymbol`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html#getSymbol--) : 返回 [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 实例的符号。您可以选择将 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 对象指定为参数。请考虑以下摘录：

  ```java
  Locale enGBLocale = 
      new Locale.Builder().setLanguage("en").setRegion("GB").build();

  Locale enUSLocale =
      new Locale.Builder().setLanguage("en").setRegion("US").build();

  Currency currencyInstance = Currency.getInstance(enUSLocale);

  System.out.println(
      "Symbol for US Dollar, en-US locale: " +
      currencyInstance.getSymbol(enUSLocale));

  System.out.println(
      "Symbol for US Dollar, en-UK locale: " +
      currencyInstance.getSymbol(enGBLocale));
  ```

  输出如下：

  ```
  Symbol for US Dollar, en-US locale: $
  Symbol for US Dollar, en-UK locale: USD
  ```

  这个例子展示了货币符号会随着语言设置而变化。

- [`getDisplayName`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html#getDisplayName--) : 返回 [`Currency`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html) 实例的显示名称。与 [`getSymbol`](https://docs.oracle.com/javase/8/docs/api/java/util/Currency.html#getSymbol--) 方法一样，您可以选择指定 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 对象。

**对ISO 4217货币代码的可扩展支持**

[ISO 4217](http://www.iso.org/iso/support/faqs/faqs_widely_used_standards/widely_used_standards_other/currency_codes.htm) 是国际标准组织发布的标准。它指定三个字母的代码（和等效的三位数字代码）来表示货币和资金。该标准由外部机构维护，独立于Java SE平台发布。

假设一个国家换用不同的货币，ISO 4217维护机构就会发布货币更新。要实现此更新，从而在运行时取代默认货币，请创建名为`*<JAVA_HOME>*/lib/currency.properties`的属性文件。此文件包含ISO 3166国家/地区代码的键/值对以及ISO 4217货币数据。值部分由三个以逗号分隔的ISO 4217货币值组成：字母代码，数字代码和次要单元。 以散列字符（＃）开头的任何行都被视为注释行。 例如：

```
# Sample currency property for Canada
CA=CAD,124,2
```

`CAD`代表加元，`124`是加元的数字代码，`2`是次要单位，是货币表示小数货币所需的小数位数。例如，以下属性文件将默认加拿大货币取代为没有任何小于一美元的单位的加元：

```
CA=CAD,124,0
```

**百分比**

您还可以使用 [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 类的方法来设置百分比的格式。要获取特定于语言环境的格式化程序，请调用 [`getPercentInstance`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html#getPercentInstance-java.util.Locale-) 方法。使用此格式化程序，小数部分（例如0.75）显示为75％。

以下代码示例显示如何格式化百分比。

```java
static public void displayPercent(Locale currentLocale) {

    Double percent = new Double(0.75);
    NumberFormat percentFormatter;
    String percentOut;

    percentFormatter = NumberFormat.getPercentInstance(currentLocale);
    percentOut = percentFormatter.format(percent);
    System.out.println(percentOut + "   " + currentLocale.toString());
}
```

这个例子输出：

```
75 %   fr_FR
75%   de_DE
75%   en_US
```

#### 自定义格式

你可以使用`DecimalFormat`类来格式化十进制数字为特定于语言区域的字符串。这个类允许你控制前导和尾随的`0`，前缀和后缀，组（千）分隔符，以及小数点的显示。如果你希望改变格式化符号，比如小数点，你可以结合使用`DecimalFormatSymbols`和`DecimalFormat`类。这些类提供了数字格式化的极大弹性，不过它们也会使你的代码变得复杂。

下面将举例说明上述两个类的使用，下面的代码示例来自 [`DecimalFormatDemo`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/DecimalFormatDemo.java) 。

**构建模式**

你使用一个模式`String`来指定`DecimalFormat`的格式化属性。该模式决定了格式化之后的数字的样子。有关模式语法的完整描述，参考 [Number Format Pattern Syntax](https://docs.oracle.com/javase/tutorial/i18n/format/decimalFormat.html#numberpattern) 。

下面的例子创建一个格式化器，通过传递一个模式`String`给一个`DecimalFormat`构造器。`format`方法接受一个`double`值作为参数并返回`String`形式的格式化数字：

```java
DecimalFormat myFormatter = new DecimalFormat(pattern);
String output = myFormatter.format(value);
System.out.println(value + " " + pattern + " " + output);
```

上面代码的输出在下面表中列出。`value`是一个数字，一个`double`，将要被格式化。`pattern`是一个`String`，指定格式化属性。`output`是一个`String`，表示格式化的数字。

`DecimalFormatDemo` 程序的输出：

| `value`    | `pattern`         | `output`    | 解释                                       |
| ---------- | ----------------- | ----------- | ---------------------------------------- |
| 123456.789 | ###,###.###       | 123,456.789 | 井号 (#) 代表一个数字，逗号是千分位分隔符的占位符，点号是小数点占位符。   |
| 123456.789 | ###.##            | 123456.79   | `value` 小数点右边有3位数字，但是 `pattern` 只有两个。 `format` 方法通过舍入处理这种情况。 |
| 123.78     | 000000.000        | 000123.780  | `pattern` 指定前导和尾随`0`，因为`0`替代了模式中的井号 (#)。 |
| 12345.67   | $###,###.###      | $12,345.67  | `pattern` 中第一个字符是美元符号 ($)，注意它会直接出现在格式化 `output` 的最左边数字前面。 |
| 12345.67   | \u00A5###,###.### | ¥12,345.67  | `pattern` 使用 Unicode 编码 00A5 指定货币符号为日元 (J¥)。 |

**区域敏感的格式**

上面的例子为默认`Locale`创建一个`DecimalFormat`对象。如果你需要一个非默认`Locale`的`DecimalFormat`对象，你实例化一个`NumberFormat`然后将其转化为`DecimalFormat`。例子如下：

```java
NumberFormat nf = NumberFormat.getNumberInstance(loc);
DecimalFormat df = (DecimalFormat)nf;
df.applyPattern(pattern);
String output = df.format(value);
System.out.println(pattern + " " + output + " " + loc.toString());
```

运行前面的例子将产生下面的输出。格式化数字，下面结果中的第二列，随着`Locale`变化：

```
###,###.###      123,456.789     en_US
###,###.###      123.456,789     de_DE
###,###.###      123 456,789     fr_FR
```

到目前为止，这里讨论的格式模式遵循美国英语的惯例。例如，在模式`###,###.##`中，逗号是千位分隔符，句点表示小数点。如果最终用户没有接触到它，那么这个约定很好。但是，某些应用程序（如电子表格和报表生成器）允许最终用户定义自己的格式设置模式。对于这些应用程序，最终用户指定的格式模式应使用本地化表示法。在这些情况下，您需要在`DecimalFormat`对象上调用`applyLocalizedPattern`方法。

**修改格式化符号**

你可以使用 [DecimalFormatSymbols](https://docs.oracle.com/javase/8/docs/api/java/text/DecimalFormatSymbols.html) 类来改变由`format`方法产生而出现的格式化数字中的符号。这些符号包含小数点、千分位分隔符、负号、以及百分号等等。

下面的例子展示了`DecimalFormatSymbols`类的使用，它将一个奇怪的格式应用于数字。不常见的格式是调用`setDecimalSeparator`、`setGroupingSeparator`以及`setGroupingSize`方法的结果。

```java
DecimalFormatSymbols unusualSymbols = new DecimalFormatSymbols(currentLocale);
unusualSymbols.setDecimalSeparator('|');
unusualSymbols.setGroupingSeparator('^');

String strange = "#,##0.###";
DecimalFormat weirdFormatter = new DecimalFormat(strange, unusualSymbols);
weirdFormatter.setGroupingSize(4);

String bizarre = weirdFormatter.format(12345.678);
System.out.println(bizarre);

```

运行之后，输出下面这种包含栅栏的格式：

```
1^2345|678
```

**数字格式化模式语法**

你可以设计自己的数字格式化模式，这些模式需要遵循下面的 BNF 图定义的规则：

```
pattern    := subpattern{;subpattern}
subpattern := {prefix}integer{.fraction}{suffix}
prefix     := '\\u0000'..'\\uFFFD' - specialCharacters
suffix     := '\\u0000'..'\\uFFFD' - specialCharacters
integer    := '#'* '0'* '0'
fraction   := '0'* '#'*
```

其中使用的记号解释如下：

| Notation  | Description        |
| --------- | ------------------ |
| `X*`      | 0 个或者多个 X          |
| `(X | Y)` | X 或者 Y             |
| `X..Y`    | 从 X 到 Y 的闭区间中的任意字符 |
| `S - T`   | 存在于 S 而不存在于 T 中的字符 |
| `{X}`     | X 是可选的             |

在前面的 BNF 图中，第一个子模式指定了正数的格式。第二个子模式是可选的，指定负数的格式。

虽然未在 BNF 图中注明，但逗号可能出现在整数部分内。

在子模式中，您可以使用特殊符号指定格式。这些符号如下表所述：

| Symbol | Description                              |
| ------ | ---------------------------------------- |
| 0      | 一个数字                                     |
| #      | 一个数字，0 表示不存在                             |
| .      | 小数点占位符                                   |
| ,      | 千分位占位符                                   |
| E      | 为指数格式分隔尾数和指数                             |
| ;      | 分隔格式                                     |
| -      | 默认符号前缀                                   |
| %      | 乘以 100 并展示为百分数                           |
| ?      | 乘以 1000 并展示位千分数                          |
| ¤      | 货币符号，被货币记号替换。如果双重使用，则会被国际货币记号替换。如果在模式中使用，使用货币小数分隔符代替小数分隔符。 |
| X      | 任何其他字符都可以在前缀或后缀中使用                       |
| '      | 用来以单引号包括前缀或者后缀中的特殊字符                     |

### 日期和时间

------

**版本提示：**本节使用`java.util`包中的日期和时间 APIs。`java.time` APIs，在 JDK 8 版本中可用，提供了一个全面的日期和时间模型，相对于`java.util`中的类有了巨大的改进。`java.time` APIs 在 [Date Time](https://docs.oracle.com/javase/tutorial/datetime/index.html) 中描述。[Legacy Date-Time Code](https://docs.oracle.com/javase/tutorial/datetime/iso/legacy.html) 页面内容可能也有一定参考价值。

------

`Date`对象表示日期和时间。你不能显示或者打印`Date`对象，而必须首先将其适当地格式化为一个`String` 。那么什么才是“合适的”格式？首先，该格式应该遵循最终用户的`Locale`传统。比如，德国认为`20.4.09`是合法的日期，但是美国人则希望同样的日期显示为`4/20/09`。其次，该格式应该包含必要的信息。比如，一个度量网络性能的程序会报告流逝的毫秒数。一个在线约定日历可能不会展示毫秒数，但是它将显示日或者周。

本节解释格式化日期和时间的各种方法，并且以一种区域敏感的方式进行。如果你使用这些技术，你的程序就能在相应的`Locale`显示正确的日期和时间，同时你的源代码将保持独立于任何特定的`Locale` 。

**[使用预定义格式](https://docs.oracle.com/javase/tutorial/i18n/format/dateFormat.html)**

`DateFormat`类提供了特定于区域的预定义格式化风格，使用非常简单。

**[自定义格式](https://docs.oracle.com/javase/tutorial/i18n/format/simpleDateFormat.html)**

使用`SimpleDateFormat`类，你可以创建自定义的特定于区域的格式。

**[修改日期格式符号](https://docs.oracle.com/javase/tutorial/i18n/format/dateFormatSymbols.html)**

使用`DateFormatSymbols`类，你可以改变表示年、月、星期几以及其它格式化元素等名称的符号。

#### 使用预定义格式

------

**版本提示：**本节使用`java.util`包中的日期和时间 APIs。`java.time` APIs，在 JDK 8 版本中可用，提供了一个全面的日期和时间模型，相对于`java.util`中的类有了巨大的改进。`java.time` APIs 在 [Date Time](https://docs.oracle.com/javase/tutorial/datetime/index.html) 中描述。[Legacy Date-Time Code](https://docs.oracle.com/javase/tutorial/datetime/iso/legacy.html) 页面内容可能也有一定参考价值。

------

 [`DateFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/DateFormat.html) 类允许你以区域敏感的方式使用预定义风格格式化日期和时间。本节接下来将举例说明如何使用`DateFormat` 类。

**日期**

使用`DateFormat`类格式化日期分两个步骤。首先，使用`getDateInstance`方法创建一个格式化器。然后，调用`format`方法，将返回一个`String` 包含格式化的日期。下面的例子通过调用这两个方法格式化今天的日期：

```java
Date today;
String dateOut;
DateFormat dateFormatter;

dateFormatter = DateFormat.getDateInstance(DateFormat.DEFAULT, currentLocale);
today = new Date();
dateOut = dateFormatter.format(today);

System.out.println(dateOut + " " + currentLocale.toString());

```

代码输出如下。注意，格式化的日期随着`Locale`而变化。由于`DateFormat`是区域敏感的，它负责每个`Locale`的格式化细节：

```
30 juin 2009     fr_FR
30.06.2009       de_DE
Jun 30, 2009     en_US
```

前面的代码例子指定了`DEFAULT`格式化风格。该`DEFAULT`风格正好就是`DateFormat`类提供的预定义格式化风格之一。如下所示：

- DEFAULT
- SHORT
- MEDIUM
- LONG
- FULL

下表展示了每种格式化风格为 U.S. 和法国格式化日期的结果：

| Style     | U.S. Locale            | French Locale      |
| --------- | ---------------------- | ------------------ |
| `DEFAULT` | Jun 30, 2009           | 30 juin 2009       |
| `SHORT`   | 6/30/09                | 30/06/09           |
| `MEDIUM`  | Jun 30, 2009           | 30 juin 2009       |
| `LONG`    | June 30, 2009          | 30 juin 2009       |
| `FULL`    | Tuesday, June 30, 2009 | mardi 30 juin 2009 |

**时间**

`Date`对象同时表示日期和时间。使用`DateFormat`类格式化时间类似于格式化日期，除了你需要使用`getTimeInstance`方法创建格式化器，如下所示：

```java
DateFormat timeFormatter =
    DateFormat.getTimeInstance(DateFormat.DEFAULT, currentLocale);
```

下面的表格展示了用于 U.S. 和德国的各种预定义格式化风格：

| Style     | U.S. Locale    | German Locale |
| --------- | -------------- | ------------- |
| `DEFAULT` | 7:03:47 AM     | 7:03:47       |
| `SHORT`   | 7:03 AM        | 07:03         |
| `MEDIUM`  | 7:03:47 AM     | 07:03:07      |
| `LONG`    | 7:03:47 AM PDT | 07:03:45 PDT  |
| `FULL`    | 7:03:47 AM PDT | 7.03 Uhr PDT  |

**日期和时间**

为了在同一个`String`中显示日期和时间，使用`getDateTimeInstance`方法创建格式化器。第一个参数是日期风格，第二个参数是时间风格。第三个参数是`Locale`。如下所示：

```java
DateFormat formatter = DateFormat.getDateTimeInstance(
                           DateFormat.LONG, 
                           DateFormat.LONG, 
                           currentLocale);
```

下面的表格展示了用于 U.S. 和法国的日期和时间格式化风格：

| Style     | U.S. Locale                           | French Locale                  |
| --------- | ------------------------------------- | ------------------------------ |
| `DEFAULT` | Jun 30, 2009 7:03:47 AM               | 30 juin 2009 07:03:47          |
| `SHORT`   | 6/30/09 7:03 AM                       | 30/06/09 07:03                 |
| `MEDIUM`  | Jun 30, 2009 7:03:47 AM               | 30 juin 2009 07:03:47          |
| `LONG`    | June 30, 2009 7:03:47 AM PDT          | 30 juin 2009 07:03:47 PDT      |
| `FULL`    | Tuesday, June 30, 2009 7:03:47 AM PDT | mardi 30 juin 2009 07 h 03 PDT |

#### 自定义格式

------

**版本提示：**本节使用`java.util`包中的日期和时间 APIs。`java.time` APIs，在 JDK 8 版本中可用，提供了一个全面的日期和时间模型，相对于`java.util`中的类有了巨大的改进。`java.time` APIs 在 [Date Time](https://docs.oracle.com/javase/tutorial/datetime/index.html) 中描述。[Legacy Date-Time Code](https://docs.oracle.com/javase/tutorial/datetime/iso/legacy.html) 页面内容可能也有一定参考价值。

------

上一节中，介绍了`DateFormat`类提供的格式化风格。大多数情况下，这些预定义格式化已经够用了。然而，如果你希望创建自己的自定义格式，你可以使用 [`SimpleDateFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html) 类。

下面的例子展示了`SimpleDateFormat`类的方法。你可以在文件 [`SimpleDateFormatDemo`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/SimpleDateFormatDemo.java) 中找到完整的源码。

**关于模式**

当你创建一个`SimpleDateFormat`对象时，你指定一个模式`String`。模式`String`的内容确定了日期和时间的格式。模式语法的完整描述，参考 [Date Format Pattern Syntax](https://docs.oracle.com/javase/tutorial/i18n/format/simpleDateFormat.html#datepattern) 。

下面的代码格式化日期和时间，根据传递给`SimpleDateFormat`构造器的模式`String`。`format`方法返回的`String`包含了用于显示的格式化日期和时间。

```java
Date today;
String output;
SimpleDateFormat formatter;

formatter = new SimpleDateFormat(pattern, currentLocale);
today = new Date();
output = formatter.format(today);
System.out.println(pattern + " " + output);

```

下表展示了上面的代码示例为 U.S. `Locale`产生的格式化输出：

| Pattern                      | Output                        |
| ---------------------------- | ----------------------------- |
| dd.MM.yy                     | 30.06.09                      |
| yyyy.MM.dd G 'at' hh:mm:ss z | 2009.06.30 AD at 08:29:36 PDT |
| EEE, MMM d, ''yy             | Tue, Jun 30, '09              |
| h:mm a                       | 8:29 PM                       |
| H:mm                         | 8:29                          |
| H:mm:ss:SSS                  | 8:28:36:249                   |
| K:mm a,z                     | 8:29 AM,PDT                   |
| yyyy.MMMMM.dd GGG hh:mm aaa  | 2009.June.30 AD 08:29 AM      |

**模式和区域**

`SimpleDateFormat`类是区域敏感的。如果你不使用`Locale`参数实例化`SimpleDateFormat`，它将会按照默认`Locale`格式化日期和时间。格式化模式和`Locale`共同决定最终格式。对于相同的模式，`SimpleDateFormat`可以针对不同的`Locale`生成不同的格式化日期和时间。

下面的代码示例中，模式被硬编码到创建`SimpleDateFormat`对象的语句中：

```java
Date today;
String result;
SimpleDateFormat formatter;

formatter = new SimpleDateFormat("EEE d MMM yy", currentLocale);
today = new Date();
result = formatter.format(today);
System.out.println("Locale: " + currentLocale.toString());
System.out.println("Result: " + result);

```

当`CurrentLocale`被设定为不同的值时，前面的代码会产生如下输出：

```
Locale: fr_FR
Result: mar. 30 juin 09
Locale: de_DE
Result: Di 30 Jun 09
Locale: en_US
Result: Tue 30 Jun 09

```

**日期格式模式语法**

你可以使用下表中列出的符号来设计你自己用于格式化日期和时间的格式化模式：

| Symbol | Meaning              | Presentation  | Example               |
| ------ | -------------------- | ------------- | --------------------- |
| G      | era designator       | Text          | AD                    |
| y      | year                 | Number        | 2009                  |
| M      | month in year        | Text & Number | July & 07             |
| d      | day in month         | Number        | 10                    |
| h      | hour in am/pm (1-12) | Number        | 12                    |
| H      | hour in day (0-23)   | Number        | 0                     |
| m      | minute in hour       | Number        | 30                    |
| s      | second in minute     | Number        | 55                    |
| S      | millisecond          | Number        | 978                   |
| E      | day in week          | Text          | Tuesday               |
| D      | day in year          | Number        | 189                   |
| F      | day of week in month | Number        | 2 (2nd Wed in July)   |
| w      | week in year         | Number        | 27                    |
| W      | week in month        | Number        | 2                     |
| a      | am/pm marker         | Text          | PM                    |
| k      | hour in day (1-24)   | Number        | 24                    |
| K      | hour in am/pm (0-11) | Number        | 0                     |
| z      | time zone            | Text          | Pacific Standard Time |
| '      | escape for text      | Delimiter     | (none)                |
| '      | single quote         | Literal       | '                     |

不是字母的字符被视为带引号的文本。也就是说，即使它们没有包含在单引号内，它们也会出现在格式化文本中。

您指定的符号字母数也决定了格式。例如，如果“zz”模式导致“PDT”，则“zzzz”模式生成“Pacific Daylight Time.”。 下表总结了这些规则：

| Presentation  | Number of Symbols                    | Result                                   |
| ------------- | ------------------------------------ | ---------------------------------------- |
| Text          | 1 - 3                                | abbreviated form, if one exists          |
| Text          | >= 4                                 | full form                                |
| Number        | minimum number of digits is required | shorter numbers are padded with zeros (for a year, if the count of 'y' is 2, then the year is truncated to 2 digits) |
| Text & Number | 1 - 2                                | number form                              |
| Text & Number | 3                                    | text form                                |

#### 修改日期格式化符号

------

**版本提示：**本节使用`java.util`包中的日期和时间 APIs。`java.time` APIs，在 JDK 8 版本中可用，提供了一个全面的日期和时间模型，相对于`java.util`中的类有了巨大的改进。`java.time` APIs 在 [Date Time](https://docs.oracle.com/javase/tutorial/datetime/index.html) 中描述。[Legacy Date-Time Code](https://docs.oracle.com/javase/tutorial/datetime/iso/legacy.html) 页面内容可能也有一定参考价值。

------

`SimpleDateFormat`类的`format`方法返回一个由数字和符号组成的`String`。比如，在`String`“Friday, April 10,2009”中，“Friday”和"April"就是符号。如果`SimpleDateFormat`中包含的符号不符合你的需求，你可以使用 [`DateFormatSymbols`](https://docs.oracle.com/javase/8/docs/api/java/text/DateFormatSymbols.html) 修改这些符号。下表列出了`DateFormatSymbols`方法允许你修改这些符号：

| Setter Method      | Example of a Symbol the Method Modifies |
| ------------------ | --------------------------------------- |
| `setAmPmStrings`   | PM                                      |
| `setEras`          | AD                                      |
| `setMonths`        | December                                |
| `setShortMonths`   | Dec                                     |
| `setShortWeekdays` | Tue                                     |
| `setWeekdays`      | Tuesday                                 |
| `setZoneStrings`   | PST                                     |

以下示例调用`setShortWeekdays`将星期几的短名称从小写字符更改为大写字符。此示例的完整源代码位于  [`DateFormatSymbolsDemo`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/DateFormatSymbolsDemo.java) 中。`setShortWeekdays`的数组参数中的第一个元素是空`String`。因此，数组下标是从 1 开始的。`SimpleDateFormat`构造函数接受修改后的`DateFormatSymbols`对象作为参数。这是源代码：

```java
Date today;
String result;
SimpleDateFormat formatter;
DateFormatSymbols symbols;
String[] defaultDays;
String[] modifiedDays;

symbols = new DateFormatSymbols( new Locale("en", "US"));
defaultDays = symbols.getShortWeekdays();

for (int i = 0; i < defaultDays.length; i++) {
    System.out.print(defaultDays[i] + " ");
}
System.out.println();

String[] capitalDays = {
    "", "SUN", "MON",
    "TUE", "WED", "THU",
    "FRI", "SAT"
};
symbols.setShortWeekdays(capitalDays);

modifiedDays = symbols.getShortWeekdays();
for (int i = 0; i < modifiedDays.length; i++) {
    System.out.print(modifiedDays[i] + " ");
}
System.out.println();
System.out.println();

formatter = new SimpleDateFormat("E", symbols);
today = new Date();
result = formatter.format(today);
System.out.println("Today's day of the week: " + result);

```

上面的代码产生如下输出：

```
 Sun Mon Tue Wed Thu Fri Sat 
 SUN MON TUE WED THU FRI SAT 

Today's day of the week: MON
```

### 消息

我们都喜欢使用那些可以让我们知道什么东西正在运行的程序。程序通常通过显示状态和错误消息来及时通知我们。当然，这些消息需要被转化以便于全世界的终端用户理解。 [Isolating Locale-Specific Data](https://docs.oracle.com/javase/tutorial/i18n/resbundle/index.html) 章节讨论转化文本消息。通常，将一个消息`String`放到`ResourceBundle`中之后你的任务就完成了。不过，如果你的消息中携带了变量数据，你就必须执行某些额外步骤来准备转化。

*复合*消息包含变量数据。在下面的复合消息中，变量数据由下划线标出：

```html
The disk named MyDisk contains 300 files.
The current balance of account #34-09-222 is $2,745.72.
405,390 people have visited your website since January 1, 2009.
Delete all files older than 120 days.
```

您可能想通过连接短语和变量来构造前面列表中的最后一条消息，如下所示：

```java
double numDays;
ResourceBundle msgBundle;
// ...
String message = msgBundle.getString(
                     "deleteolder" +
                     numDays.toString() +
                     msgBundle.getString("days"));
```

此方法在英语环境下工作良好，但是在那些动词放在句子末尾的语言环境中不行。因为消息中的词语的顺序是硬编码的，你的本地化器将无法为所有语言创建语法正确的翻译。

当你需要使用复合消息时你应该如何编写你的本地化器？你可以使用`MessageFormat`类，就是本章节的主题。

------

**警告：**复合消息很难翻译，因为消息文本是分成若干片段的。如果你使用复合消息，本地化过程将更加耗时和消耗资源。因而你应该只在必要时才使用复合消息。

------

**[处理复合消息](https://docs.oracle.com/javase/tutorial/i18n/format/messageFormat.html)**

一条复合消息可能包含若干种变量：日期、时间、字符串、数字、货币、以及百分数。为了以区域无关的形式格式化复合消息，你可以构建一个可应用于`MessageFormat`对象的模式。

**[处理复数](https://docs.oracle.com/javase/tutorial/i18n/format/choiceFormat.html)**

如果复数和单数单词形式都可能，则消息中的单词通常会有所不同。使用`ChoiceFormat`类，您可以将数字映射到单词或短语，从而允许您构造语法正确的消息。

#### 处理复合消息

一条复合消息可能包含若干种变量：日期、时间、字符串、数字、货币、以及百分数。为了以区域无关的形式格式化复合消息，你可以构建一个可应用于`MessageFormat`对象的模式，并将该模式存储到一个`ResourceBundle`种。

接下来逐步分析例子程序，本节举例说明如何国际化一个复合消息。例子程序使用 [`MessageFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/MessageFormat.html) 类。例子程序的完整源码在文件 [`MessageFormatDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/MessageFormatDemo.java) 中。德国区域的属性放在 [`MessageBundle_de_DE.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/MessageBundle_de_DE.properties) 文件中。

**1. 标示消息中的变量**

假定你想要国际化下面的消息：

![The following line of text: At 1:15 on April 13, 1998, we detected 7 spaceships on the planet Mars.  The variable data (1:15, April 13,1998, 7, and Mars) have been underlined.](https://docs.oracle.com/javase/tutorial/figures/i18n/i18n-2.gif)

注意，我们已经用下划线标出变量数据并且标示出将使用何种对象类型来表示该数据。

**2. 将消息模式隔离到一个 ResourceBundle 中**

将消息保存到名为`MessageBundle`的`ResouceBundle`中。如下所示：

```java
ResourceBundle messages =
   ResourceBundle.getBundle("MessageBundle", currentLocale);
```

该`ResouceBundle`由对应各种`Locale`的属性文件支持。因为该`ResourceBundle`名为`MessageBundle`，则用于 U.S.English 的属性文件名为`MessageBundle_en_US.properties`。该文件的内容如下：

```
template = At {2,time,short} on {2,date,long}, \
    we detected {1,number,integer} spaceships on \
    the planet {0}.
planet = Mars
```

属性文件的第一行包含了消息模式。如果你比较该模式与第一步中展示的消息文本，你将会发现消息文本中的每个变量都被大括号包围的参数替换了。每个参数都以称为参数号的数字开头，该数值对应于持有参数值的`Object`数组中元素的下标。注意，模式中的参数号并没有一定顺序。你可以讲参数放在模式中任何位置。唯一的要求就是参数号在参数值数组中有对应的元素。

下一步讨论该参数值数组，但是首先让我们看看模式中每个参数。下表提供了有关参数的一些细节：

| Argument | Description |
|  |  |
| `{2,time,short}` | `Date`对象的时间部分，`short`风格指定`DateFormat.SHORT`格式化风格。 |
| `{2,date,long}` | `Date`对象的日期部分，同一个`Date`对象被用于时间和日期变量。在`Object`参数数组中持有该`Date`对象的元素的下标是 2。 |
| `{1,number,integer}` | 一个`Number`对象，进一步使用`integer`数字样式限定。 |
| `{0}` | `ResourceBundle`中对应于`planet`键的`String`。 |

有关参数语法的完整描述，参考 [`MessageFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/MessageFormat.html) 类的文档。

**3. 设置消息参数**

以下代码行为模式中的每个参数赋值。 `messageArguments`数组中元素的索引与模式中的参数号匹配。例如，索引1处的`Integer`元素对应于模式中的`{1,number,integer}`参数。因为它必须被翻译，元素0处的`String`对象将使用`getString`方法从`ResourceBundle`获取。以下是定义消息参数数组的代码：

```java
Object[] messageArguments = {
    messages.getString("planet"),
    new Integer(7),
    new Date()
};
```

**4. 创建格式化器**

接下来，创建一个`MessageFormat`对象。你设定`Locale`因为消息包含`Date`和`Number`对象，应该给以区域敏感的方式格式化。

```java
MessageFormat formatter = new MessageFormat("");
formatter.setLocale(currentLocale);
```

**5. 使用模式和参数格式化消息**

此步骤显示模式，消息参数和格式化程序如何一起工作。首先，使用`getString`方法从`ResourceBundle`获取模式`String`。模式的关键是“模板”。使用`applyPattern`方法将模式`String`传递给格式化器。然后通过调用`format`方法使用消息参数数组格式化消息。 `format`方法返回的`String`已准备好显示。所有这一切都只需两行代码即可完成：

```java
formatter.applyPattern(messages.getString("template"));
String output = formatter.format(messageArguments);
```

**6. 运行例子程序**

演示程序打印英语和德语语言环境的翻译消息，并正确格式化日期和时间变量。请注意，英语和德语动词（“detected”和“entdeckt”）位于相对于变量的不同位置：

```
currentLocale = en_US
At 10:16 AM on July 31, 2009, we detected 7
spaceships on the planet Mars.
currentLocale = de_DE
Um 10:16 am 31. Juli 2009 haben wir 7 Raumschiffe
auf dem Planeten Mars entdeckt.
```

#### 处理复数

如果复数和单数形式都可能，则消息中的单词可能会有所不同。使用`ChoiceFormat`类，您可以将数目映射到单词或短语，从而允许您构造语法正确的消息。

在英语中，单词的复数和单数形式通常是不同的。当您构建包含数量的消息时，这可能会出现问题。例如，如果您的消息报告磁盘上的文件数，则可能存在以下变化：

```
There are no files on XDisk.
There is one file on XDisk.
There are 2 files on XDisk.
```

解决此问题的最快方式就是创建如下的`MessageFormat`模式：

```
There are {0,number} file(s) on {1}.
```

很不幸，上面的模式产生的语法不正确：

```
There are 1 file(s) on XDisk.
```

你可以做的更好，你可以使用 [`ChoiceFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/ChoiceFormat.html) 类。在本节中你将看到如何处理消息中的复数。通过一个简单的例子[`ChoiceFormatDemo`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/ChoiceFormatDemo.java) 逐步展示。该程序也使用了`MessageFormat`类，该类在上一节中讨论。

**1. 定义消息模式**

首先，标示消息中的变量：

![Three lines of text, with the variables in each line highlighted.](https://docs.oracle.com/javase/tutorial/figures/i18n/i18n-3.gif)

接下来，用参数替换消息中的变量，创建一个能够应用于`MessageFormat`对象的模式：

```
There {0} on {1}.
```

磁盘名称的参数，由`{1}`表示，很容易处理。你只需像处理`MessageFormat`模式中的其它`String`变量一样处理它们。此参数匹配参数值数组中下标为 1 的元素。

处理参数`{0}`更加复杂一些，因为两个原因：

- 参数替换过程会随着文件数量而有所不同。为了在运行时构建该阶段，你需要将文件数量映射到一个特定的`String`。比如，数量 1 映射到包含`is one file`短语的`String`。`ChoiceFormat`类允许你执行必要的映射。
- 如果磁盘包含多个文件，该短语包含一个整数。`MessageFormat`类允许你在短语中插入一个整数。

**2. 创建一个 ResourceBundle**

因为消息文本必须被翻译，将它隔离到一个`ResourceBundle`中：

```java
ResourceBundle bundle = ResourceBundle.getBundle(
    "ChoiceBundle", currentLocale);
```

例子程序使用属性文件支持`ResourceBundle`。[`ChoiceBundle_en_US.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/ChoiceBundle_en_US.properties) 包含以下内容：

```
pattern = There {0} on {1}.
noFiles = are no files
oneFile = is one file
multipleFiles = are {2} files
```

此属性文件的内容展示了消息将如何被构建和格式化。第一行包含`MessageFormat`模式。其它的行包含替换模式中的参数`{0}`的短语。对应于`multipleFiles`键的短语包含参数`{2}`，将被一个数字替换。

这里是属性文件的法语版本， [`ChoiceBundle_fr_FR.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/ChoiceBundle_fr_FR.properties) ：

```
pattern = Il {0} sur {1}.
noFiles = n'y a pas de fichiers
oneFile = y a un fichier
multipleFiles = y a {2} fichiers
```

**3. 创建一个消息格式化器**

这一步实例化`MessageFormat`并设置它的`Locale`：

```java
MessageFormat messageForm = new MessageFormat("");
messageForm.setLocale(currentLocale);
```

**4. 创建 Choice Formatter**

`ChoiceFormat`对象允许你选择，基于一个`double`数字，一个特定的`String`。该`double`数字的范围，以及它所映射到的`String`对象，在数组中指定：

```java
double[] fileLimits = {0,1,2};
String [] fileStrings = {
    bundle.getString("noFiles"),
    bundle.getString("oneFile"),
    bundle.getString("multipleFiles")
};
```

`ChoiceFormat`将`double`数组中的每个元素映射到具有相同索引的`String`数组中的元素。在示例代码中，0 映射到通过调用`bundle.getString(“noFiles”)`返回的`String`。巧合的是，索引与`fileLimits`数组中的值相同。如果代码将`fileLimits[0]`设置为 7，那么`ChoiceFormat`会将数字 7 映射到`fileStrings[0]`。

在实例化`ChoiceFormat`时指定`double`和`String`数组：

```java
ChoiceFormat choiceForm = new ChoiceFormat(fileLimits, fileStrings);
```

**5. 应用该模式**

还记得你在第一步中创建的模式吗？是时候从`ResourceBundle`中获取它并将它应用于`MessageFormat`对象：

```java
String pattern = bundle.getString("pattern");
messageForm.applyPattern(pattern);
```

**6. 分配该格式**

这一步中你将第四步中创建的`ChoiceFormat`对象分配给`MessageFormat`对象：

```java
Format[] formats = {choiceForm, null, NumberFormat.getInstance()};
messageForm.setFormats(formats);
```

`setFormats`方法将`Format`对象分配给消息模式中的参数。在调用`setFormats`方法之前，必须调用`applyPattern`方法。下表显示了`Format`数组的元素如何对应于消息模式中的参数：

 `ChoiceFormatDemo` 程序的`Format` 数组

| Array Element                | Pattern Argument |
| ---------------------------- | ---------------- |
| `choiceForm`                 | `{0}`            |
| `null`                       | `{1}`            |
| `NumberFormat.getInstance()` | `{2}`            |

**7. 设置消息的参数和格式**

在运行时，程序将变量分配给它传递给`MessageFormat`对象的参数数组。数组中的元素对应于模式中的参数。例如，`messageArgument[1]`映射到模式参数`{1}`，它是一个包含磁盘名称的`String`。在上一步中，程序将`ChoiceFormat`对象分配给模式的参数`{0}`。因此，分配给`messageArgument[0]`的数字决定了`ChoiceFormat`对象选择哪个`String`。如果`messageArgument[0]`大于或等于2，则包含短语`is {2} files`的`String`将替换模式中的参数`{0}`。分配给`messageArgument[2]`的数字将代替模式参数`{2}`。这是尝试这个过程的代码：

```java
Object[] messageArguments = {null, "XDisk", null};

for (int numFiles = 0; numFiles < 4; numFiles++) {
    messageArguments[0] = new Integer(numFiles);
    messageArguments[2] = new Integer(numFiles);
    String result = messageForm.format(messageArguments);
    System.out.println(result);
}
```

**8. 运行示例程序**

将程序显示的消息与步骤2的`ResourceBundle`中的短语进行比较。请注意，`ChoiceFormat`对象选择正确的短语，`MessageFormat`对象用于构造正确的消息。 `ChoiceFormatDemo`程序的输出如下：

```
currentLocale = en_US
There are no files on XDisk.
There is one file on XDisk.
There are 2 files on XDisk.
There are 3 files on XDisk.

currentLocale = fr_FR
Il n'y a pas des fichiers sur XDisk.
Il y a un fichier sur XDisk.
Il y a 2 fichiers sur XDisk.
Il y a 3 fichiers sur XDisk.
```

## 使用文本

几乎所有具有用户界面的程序都操纵文本。在国际市场上，您的程序显示的文本必须符合来自世界各地的语言规则。Java编程语言提供了许多类，可帮助您以与语言环境无关的方式处理文本。

[检查字符属性](https://docs.oracle.com/javase/tutorial/i18n/text/charintro.html)

本章节解释如何使用`Character`比较方法来检测所有主要语言的字符属性。

[比较字符串](https://docs.oracle.com/javase/tutorial/i18n/text/collationintro.html)

本章节中你将学到如何使用`Collator`类执行区域无关的字符串比较。

[探测文本边界](https://docs.oracle.com/javase/tutorial/i18n/text/boundaryintro.html)

本章节展示`BreakIterator`类如何探测字符、词语、语句以及行边界。

[转化非Unicode文本](https://docs.oracle.com/javase/tutorial/i18n/text/convertintro.html)

世界各地的不同计算机系统以各种编码方案存储文本。本节介绍可帮助您在Unicode和其他编码之间转换文本的类。

[正则化 API](https://docs.oracle.com/javase/tutorial/i18n/text/normalizerapi.html)

本节解释如何使用正则化 API 来转化不同正则化形式的文本。

[通过 JTextComponent 类使用双向文本](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html)

本节讨论如何使用双向文本，该文本包含从左到右和从右到左两个方向运行的文本。

### 检查字符属性

您可以根据字符的属性对字符进行分类。例如，X 是大写字母，4 是十进制数字。检查字符属性是验证最终用户输入的数据的常用方法。例如，如果您在线销售图书，您的订单输入屏幕应验证数量字段中的字符是否都是数字。

不习惯编写全球化软件的开发人员可以通过将字符与字符常量进行比较来确定字符的属性。例如，他们可能会编写如下代码：

```java
char ch;
//...

// This code is WRONG!

// check if ch is a letter
if ((ch >= 'a' && ch <= 'z') || (ch >= 'A' && ch <= 'Z'))
    // ...

// check if ch is a digit
if (ch >= '0' && ch <= '9')
    // ...

// check if ch is a whitespace
if ((ch == ' ') || (ch =='\n') || (ch == '\t'))
    // ...
```

上面的代码时错误的，因为它只能用于英语和很少几种其它语言。为了国际化该程序，改成如下形式：

```java
char ch;
// ...

// This code is OK!

if (Character.isLetter(ch))
    // ...

if (Character.isDigit(ch))
    // ...

if (Character.isSpaceChar(ch))
    // ...
```

[`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) 方法依赖 Unicode 标准来确定字符的属性。Unicode 是一种支持世界主要语言的16位字符编码。在Java编程语言中，`char`值表示 Unicode 字符。如果使用适当的`Character`方法检查`char`的属性，则代码将适用于所有主要语言。例如，如果字符是中文，德语，阿拉伯语或其他语言的字母，则`Character.isLetter`方法返回`true`。

以下列表给出了一些最有用的`Character`比较方法。 `Character` API文档完全指定了方法。

- `isDigit`
- `isLetter`
- `isLetterOrDigit`
- `isLowerCase`
- `isUpperCase`
- `isSpaceChar`
- `isDefined`

`Character.getType`方法返回字符的 Unicode 类别。每个类别对应于`Character`类中定义的常量。例如，`getType`返回字符 A 的`Character.UPPERCASE_LETTER`常量。有关`getType`返回的类别常量的完整列表，请参阅[`Character`](https://docs.oracle.com /javase/8/docs/api/java/lang/Character.html) API文档。以下示例显示如何使用`getType`和`Character`类别常量。这些`if`语句中的所有表达式都是`true`：

```java
if (Character.getType('a') == Character.LOWERCASE_LETTER)
    // ...

if (Character.getType('R') == Character.UPPERCASE_LETTER)
    // ...

if (Character.getType('>') == Character.MATH_SYMBOL)
    // ...

if (Character.getType('_') == Character.CONNECTOR_PUNCTUATION)
    // ...
```

### 比较字符串

通过文本排序的应用程序执行频繁的字符串比较。例如，报表生成器在按字母顺序对字符串列表进行排序时执行字符串比较。

如果您的应用程序受众仅限于说英语的人，则可以使用`String.compareTo`方法执行字符串比较。 `String.compareTo`方法对两个字符串中的 Unicode 字符进行二进制比较。但是，对于大多数语言，不能依赖此二进制比较来对字符串进行排序，因为 Unicode 值与字符的相对顺序不对应。

幸运的是，[`Collator`](https://docs.oracle.com/javase/8/docs/api/java/text/Collator.html) 类允许您的应用程序对不同语言执行字符串比较。在本节中，您将学习如何在排序文本时使用`Collator`类。

**[执行区域无关的比较](https://docs.oracle.com/javase/tutorial/i18n/text/locale.html)**

排序规则定义字符串的排序顺序。这些规则因语言环境而异，因为各种自然语言对单词的排序方式不同。使用`Collator`类提供的预定义排序规则，您可以以与语言环境无关的方式对字符串进行排序。

**[自定义排序规则](https://docs.oracle.com/javase/tutorial/i18n/text/rule.html)**

在某些情况下，`Collator`类提供的预定义排序规则可能不适合您。例如，您可能希望使用`Collator`对其不支持的语言环境的语言对字符串进行排序。在这种情况下，您可以定义自己的排序规则，并将它们分配给`RuleBasedCollator`对象。

**[改进排序性能](https://docs.oracle.com/javase/tutorial/i18n/text/perform.html)**

使用`CollationKey`类，可以提高字符串比较的效率。此类将`String`对象转换为按照给定`Collator`的规则排序的键。

#### 执行区域无关比较

排序规则定义字符串的排序顺序。这些规则因语言环境而异，因为各种自然语言对单词的排序方式不同。您可以使用`Collator`类提供的预定义排序规则来以与语言环境无关的方式对字符串进行排序。

要实例化`Collator`类，请调用`getInstance`方法。通常，您为默认的`Locale`创建一个`Collator`，如下例所示：

```java
Collator myDefaultCollator = Collator.getInstance();
```

你也可以在创建`Collator`时指定一个特定的`Locale`，如下所示：

```java
Collator myFrenchCollator = Collator.getInstance(Locale.FRENCH);
```

`getInstance`方法返回一个`RuleBasedCollator`，它是`Collator`的具体子类。 `RuleBasedCollator`包含一组规则，用于确定您指定的语言环境的字符串的排序顺序。这些规则是为每个区域设置预定义的。因为规则封装在`RuleBasedCollator`中，所以您的程序不需要特殊的例程来处理随语言变化的排序规则。

您调用`Collator.compare`方法来执行与语言环境无关的字符串比较。当第一个字符串参数小于，等于或大于第二个字符串参数时，`compare`方法返回小于，等于或大于零的整数。下表包含对`Collator.compare`的一些示例调用：

| Example                            | Return Value | Explanation                 |
| ---------------------------------- | ------------ | --------------------------- |
| `myCollator.compare("abc", "def")` | `-1`         | `"abc"` is less than "def"  |
| `myCollator.compare("rtf", "rtf")` | `0`          | the two strings are equal   |
| `myCollator.compare("xyz", "abc")` | `1`          | "xyz" is greater than "abc" |

在执行排序操作时使用`compare`方法。名为[`CollatorDemo`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/CollatorDemo.java) 的示例程序使用`compare`方法对英语和法语单词数组进行排序。此程序显示当您使用两个不同的 collators 对相同的单词列表进行排序时会发生什么：

```java
Collator fr_FRCollator = Collator.getInstance(new Locale("fr","FR"));
Collator en_USCollator = Collator.getInstance(new Locale("en","US"));
```

排序方法称为`sortStrings`，可以与任何`Collator`一起使用。请注意，`sortStrings`方法调用`compare`方法：

```java
public static void sortStrings(Collator collator, String[] words) {
    String tmp;
    for (int i = 0; i < words.length; i++) {
        for (int j = i + 1; j < words.length; j++) { 
            if (collator.compare(words[i], words[j]) > 0) {
                tmp = words[i];
                words[i] = words[j];
                words[j] = tmp;
            }
        }
    }
}
```

英语`Collator`对单词进行了如下排序：

```
peach
péché
pêche
sin
```

根据法语的排序规则，前面的列表顺序错误。在法语中，péché应该在排序列表中跟随pêche。法语`Collator`正确排序单词数组，如下所示：

```
peach
pêche
péché
sin
```

#### 自定义排序规则

上一节讨论了如何使用区域设置的预定义规则来比较字符串。这些排序规则确定字符串的排序顺序。如果预定义的排序规则不符合您的需要，您可以设计自己的规则并将它们分配给`RuleBasedCollator`对象。

自定义的排序规则包含在传递给`RuleBasedCollator`构造函数的`String`对象中。这是一个简单的例子：

```java
String simpleRule = "< a < b < c < d";
RuleBasedCollator simpleCollator =  new RuleBasedCollator(simpleRule);
```

对于前一个例子中的`simpleCollator`对象，`a`小于`b`，小于`c`，依此类推。比较字符串时，`simpleCollator.compare`方法引用这些规则。用于构造排序规则的完整语法比这个简单示例更灵活，更复杂。有关语法的完整说明，请参阅[`RuleBasedCollator`](https://docs.oracle.com/javase/8/docs/api/java/text/RuleBasedCollator.html) 类的 API 文档。

下面的示例使用两个 collators 对西班牙语单词列表进行排序。此示例的完整源代码位于[`RulesDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/RulesDemo.java) 中。

`RulesDemo`程序首先定义英语和西班牙语的排序规则。该程序将以传统方式对西班牙语单词进行排序。当按照传统规则进行排序时，字母`ch`和`ll`及其大写等价物在排序顺序中各自具有自己的位置。这些字符对在比较它们时就好像是一个字符。例如，`ch`作为单个字母按照排序顺序中的`cz`排序。请注意两个 collators 的规则有何不同：

```java
String englishRules = (
    "< a,A < b,B < c,C < d,D < e,E < f,F " +
    "< g,G < h,H < i,I < j,J < k,K < l,L " +
    "< m,M < n,N < o,O < p,P < q,Q < r,R " +
    "< s,S < t,T < u,U < v,V < w,W < x,X " +
    "< y,Y < z,Z");

String smallnTilde = new String("\u00F1");    // ñ
String capitalNTilde = new String("\u00D1");  // Ñ

String traditionalSpanishRules = (
    "< a,A < b,B < c,C " +
    "< ch, cH, Ch, CH " +
    "< d,D < e,E < f,F " +
    "< g,G < h,H < i,I < j,J < k,K < l,L " +
    "< ll, lL, Ll, LL " +
    "< m,M < n,N " +
    "< " + smallnTilde + "," + capitalNTilde + " " +
    "< o,O < p,P < q,Q < r,R " +
    "< s,S < t,T < u,U < v,V < w,W < x,X " +
    "< y,Y < z,Z");
```

以下代码行创建了 collators 并调用了 sort 例程：

```java
try {
    RuleBasedCollator enCollator = new RuleBasedCollator(englishRules);
    RuleBasedCollator spCollator =
        new RuleBasedCollator(traditionalSpanishRules);

    sortStrings(enCollator, words);
    printStrings(words);
    System.out.println();

    sortStrings(spCollator, words);
    printStrings(words);
} catch (ParseException pe) {
    System.out.println("Parse exception for rules");
}
```

称为`sortStrings`的排序例程是通用的。它将根据任何`Collator`对象的规则对任何单词数组进行排序：

```java
public static void sortStrings(Collator collator, String[] words) {
    String tmp;
    for (int i = 0; i < words.length; i++) {
        for (int j = i + 1; j < words.length; j++) {
            if (collator.compare(words[i], words[j]) > 0) {
                tmp = words[i];
                words[i] = words[j];
                words[j] = tmp;
            }
        }
    }
}
```

使用英语排序规则排序时，单词数组如下：

```
chalina
curioso
llama
luz
```

将前面的列表与以下列表进行比较，后者根据传统的西班牙语排序规则进行排序：

```
curioso
chalina
luz
llama
```

#### 改进排序性能

对很长的字符串进行排序通常会非常耗时。如果你的排序算法反复比较字符串，你就可以使用`CollationKey`类来加速排序过程。

 [`CollationKey`](https://docs.oracle.com/javase/8/docs/api/java/text/CollationKey.html) 对象表示给定`String`和`Collator`的排序键。比较两个`CollationKey`对象涉及排序键的按位比较，并且比将`String`对象使用`Collator.compare`方法进行比较要快。但是，生成`CollationKey`对象需要时间。因此，如果要比较一个`String`，`Collator.compare`可以提供更好的性能。

下面的例子使用一个`CollationKey`对象来排序一个单词数组。该例子的源代码是 [`KeysDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/KeysDemo.java) 。

`KeysDemo`程序在`main`方法中创建了一个`CollationKey`对象数组。为了创建`CollationKey`，你可以调用`Collator`对象上的`getCollationKey`方法。你只能比较来自同一个`Collator`的两个`CollationKey`对象。该`main`方法如下：

```java
static public void main(String[] args) {
    Collator enUSCollator = Collator.getInstance(new Locale("en","US"));
    String [] words = {
        "peach",
        "apricot",
        "grape",
        "lemon"
    };

    CollationKey[] keys = new CollationKey[words.length];

    for (int k = 0; k < keys.length; k ++) {
        keys[k] = enUSCollator. getCollationKey(words[k]);
    }

    sortArray(keys);
    printArray(keys);
}
```

`sortArray`方法调用`CollationKey.compareTo`方法。`compareTo`方法返回一个小于、等于或者大于0的整数，如果`keys[i]`对象值小于、等于或者大于`keys[j]`对象值。注意该程序比较`CollationKey`对象，而不是来自初始单词数组的`String`对象。下面是`sortArray`方法代码：

```java
public static void sortArray(CollationKey[] keys) {
    CollationKey tmp;

    for (int i = 0; i < keys.length; i++) {
        for (int j = i + 1; j < keys.length; j++) {
            if (keys[i].compareTo(keys[j]) > 0) {
                tmp = keys[i];
                keys[i] = keys[j];
                keys[j] = tmp; 
            }
        }
    }
}
```

`KeysDemo`程序排序一个`CollationKey`对象数组，但是初始目标却是排序一个`String`对象数组。为了检索每个`CollationKey`所表示的`String`，该程序在`displayWords`方法中调用`getSourceString`，如下所示：

```java
static void displayWords(CollationKey[] keys) {
    for (int i = 0; i < keys.length; i++) {
        System.out.println(keys[i].getSourceString());
    }
}
```

 `displayWords` 方法打印如下内容：

```
apricot
grape
lemon
peach
```

### Unicode

*Unicode*是一种计算行业标准，旨在对全世界书面语言中使用的字符进行一致且唯一的编码。Unicode标准使用十六进制表示字符。例如，值 0x0041 表示拉丁字符 A。Unicode标准最初使用16位来设计字符，因为当时主要计算机是16位PC。

创建Java语言规范时，接受Unicode标准，并将`char`原语定义为16位数据类型，十六进制范围内的字符从 0x0000 到 0xFFFF。

由于16位编码支持2<sup>16</sup>（65,536）个字符，这不足以定义全世界使用的所有字符，因此Unicode标准扩展为 0x10FFFF，支持超过一百万个字符。Java编程语言中字符的定义无法从16位更改为32位，而不会导致数百万Java应用程序无法正常运行。为了纠正定义，开发了一种方案来处理无法以16位编码的字符。

值超出16位范围且在 0x10000 到 0x10FFFF 范围内的字符称为*补充字符*，并定义为一对`char`值。

本课程包含以下章节：

- [术语](https://docs.oracle.com/javase/tutorial/i18n/text/terminology.html) - 解释代码点和其他术语。
- [补充字符作为代理](https://docs.oracle.com/javase/tutorial/i18n/text/supplementaryChars.html) - 16位代理用于实现补充字符，这些补充字符不能作为单个原始`char`数据类型实现。
- [字符和字符串API](https://docs.oracle.com/javase/tutorial/i18n/text/characterClass.html) -`Character`，`String`相关的 API 以及相关的类的列表。
- [示例用法](https://docs.oracle.com/javase/tutorial/i18n/text/usage.html) - 提供了几个有用的代码片段。
- [设计注意事项](https://docs.oracle.com/javase/tutorial/i18n/text/design.html) - 要记住[设计注意事项](https://docs.oracle.com/javase/tutorial/i18n/text/design.html)，以确保您的应用程序可以使用任何语言脚本。
- [更多信息](https://docs.oracle.com/javase/tutorial/i18n/text/info.html) - 提供了更多资源的列表。

#### 术语

*字符*是具有语义值的最小文本单元。

*字符集*是可能由多种语言使用的字符集合。例如，拉丁字符集由英语和大多数欧洲语言使用，尽管希腊语字符集仅由希腊语使用。

*编码字符集*是一个字符集，其中每个字符被分配一个唯一的编号。

*代码点*是可以在编码字符集中使用的值。代码点是32位`int`数据类型，其中低21位表示有效代码点值，高11位表示0。

Unicode *代码单元*是一个16位的`char`值。例如，假设一个`String`包含字母“abc”，后跟 Deseret LONG I，用两个`char`值表示。该字符串包含四个字符，四个代码点，但包含五个代码单元。

要以Unicode表示字符，十六进制值以字符串 U+ 为前缀。Unicode标准的有效代码点范围是 U+0000 到 U+10FFFF，包括端点。拉丁字符A的代码点值是 U+0041。代表欧元货币的字符 € 具有代码点值 U+20AC。 Deseret 字母表中的第一个字母 LONG I 的代码点值为 U+10400。

下表显示了几个字符的代码点值：

| Character       | Unicode Code Point | Glyph                                    |
| --------------- | ------------------ | ---------------------------------------- |
| Latin A         | U+0041             | ![The Latin character A](https://docs.oracle.com/javase/tutorial/figures/i18n/000041.gif) |
| Latin sharp S   | U+00DF             | ![The Latin small letter sharp S](https://docs.oracle.com/javase/tutorial/figures/i18n/0000df.gif) |
| Han for East    | U+6771             | ![The Han character for east, eastern or eastward](https://docs.oracle.com/javase/tutorial/figures/i18n/006771.gif) |
| Deseret, LONG I | U+10400            | ![The Deseret capital letter long I](https://docs.oracle.com/javase/tutorial/figures/i18n/010400.gif) |

如前所述，在 U+10000 到 U+10FFFF 范围内的字符被称为补充字符。从 U+0000 到 U+FFFF 的字符集有时被称为*基本多语言平面（BMP）*。

更多术语可以在 [更多信息](https://docs.oracle.com/javase/tutorial/i18n/text/info.html) 页面上列出的*Unicode术语表*中找到。

#### 补充字符作为代理

为了支持补充字符而不更改`char`原始数据类型并导致与以前的Java程序不兼容，补充字符由一对称为代理项的代码点值定义。第一个代码点是从 U+D800 到 U+DBFF 的高代理范围，第二个代码点是从 U+DC00 到 U+DFFF 的低代理范围。例如，Deseret 字符 LONG I，U+10400，用这对代理值定义：U+D801和 U+DC00。

#### 字符和字符串 API

`Character`类封装了`char`数据类型。对于J2SE第5版，在`Character`类中添加了许多方法来支持补充字符。这些API分为两类：在`char`和代码点值之间转换的方法以及验证或映射代码点的有效性的方法。

本节描述了`Character`类中可用方法的子集。 有关可用API的完整列表，请参阅 [`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) 类规范。

**转换方法和 Character 类**

下表包含`Character`类中最有用的转换方法或便于转换的方法。 `codePointAt`和`codePointBefore`方法包含在此列表中，因为文本通常在字符序列中找到，例如`String`，并且这些方法可用于提取所需的子字符串。

| Method(s)                                | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| [`toChars(int codePoint, char[] dst, int dstIndex)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toChars-int-char:A-int-)<br />[`toChars(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toChars-int-) | 将指定的Unicode代码点转换为其UTF-16表示形式，并将其放在`char`数组中。示例用法：`Character.toChars(0x10400)` 。 |
| [`toCodePoint(char high, char low)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toCodePoint-char-char-) [`toCodePoint(CharSequence, int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toCodePoint-java.lang.CharSequence-int-)<br />[`toCodePoint(char[], int, int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#toCodePoint-char:A-int-int-) | 将指定的参数转换为其补充代码点值。不同的方法接受不同的输入格式。         |
| [`codePointAt(char[] a, int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointAt-char:A-int-)<br />[`codePointAt(char[] a, int index, int limit)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointAt-char:A-int-int-)<br />[`codePointAt(CharSequence seq, int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointAt-java.lang.CharSequence-int-) | 返回指定索引处的Unicode代码点。第三种方法采用`CharSequence`，第二种方法需要索引的上限。 |
| [`codePointBefore(char[] a, int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointBefore-char:A-int-)<br />[`codePointBefore(char[] a, int index, int start)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointBefore-char:A-int-int-)<br />[`codePointBefore(CharSequence seq, int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointBefore-java.lang.CharSequence-int-)<br />[`codePointBefore(char[], int, int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointBefore-char:A-int-int-) | 返回指定索引之前的Unicode代码点。第三种方法接受`CharSequence`，其他方法接受`char`数组。第二种方法需要索引下限。 |
| [`charCount(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#charCount-int-) | 为可由单个`char`表示的字符返回值1。为需要两个`char`s的补充字符返回值2。 |

**Character 类中的验证和映射方法**

前面使用`char`基本数据类型的一些方法，例如`isLowerCase(char)`和`isDigit(char)`，被支持补充字符的方法所取代，例如`isLowerCase(int)`和`isDigit(int)`。前面的方法仍然支持，但不能使用补充字符。要创建全局应用程序并确保代码与任何语言无缝协作，建议您使用这些方法的较新形式。

请注意，出于性能原因，大多数接受代码点的方法都不会验证代码点参数的有效性。您可以使用`isValidCodePoint`方法实现此目的。

下表列出了`Character`类中的一些验证和映射方法。

| Method(s)                                | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| [`isValidCodePoint(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isValidCodePoint-int-) | 如果代码点属于 0x0000 到 0x10FFFF 闭区间范围则返回`true`。 |
| [`isSupplementaryCodePoint(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isSupplementaryCodePoint-int-) | 如果代码点属于 0x10000 到 0x10FFFF 闭区间范围则返回`true`。 |
| [`isHighSurrogate(char)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isHighSurrogate-char-) | 如果指定`char`处于高代理范围 \uD800 到 \uDBFF 闭区间内时返回`true`。 |
| [`isLowSurrogate(char)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isLowSurrogate-char-) | 如果指定`char`处于低代理范围 \uDC00 到 \uDFFF 闭区间内时返回`true`。 |
| [`isSurrogatePair(char high, char low)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isSurrogatePair-char-char-) | 如果指定的高和低代理代码值表示有效的代理项对，则返回`true`。        |
| [`codePointCount(CharSequence, int, int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointCount-java.lang.CharSequence-int-int-)<br />[`codePointCount(char[], int, int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#codePointCount-char:A-int-int-) | 返回`CharSequence`或`char`数组中的Unicode代码点数。  |
| [`isLowerCase(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isLowerCase-int-) [`isUpperCase(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isUpperCase-int-) | 如果指定的Unicode代码点是小写或大写字符，则返回`true`。       |
| [`isDefined(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isDefined-int-) | 如果在Unicode标准中定义了指定的Unicode代码点，则返回`true`。 |
| [`isJavaIdentifierStart(char)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isJavaIdentifierStart-char-) [`isJavaIdentifierStart(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isJavaIdentifierStart-int-) | 如果允许指定的字符或Unicode代码点作为Java标识符中的第一个字符，则返回`true`。 |
| [`isLetter(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isLetter-int-) [`isDigit(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isDigit-int-) [`isLetterOrDigit(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#isLetterOrDigit-int-) | 如果指定的Unicode代码点是字母，数字或字母或数字，则返回`true`。   |
| [`getDirectionality(int)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html#getDirectionality-int-) | 返回给定Unicode代码点的Unicode方向性属性。             |
| [`Character.UnicodeBlock.of(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.UnicodeBlock.html#of-int-) | 返回表示包含给定Unicode代码点的Unicode块的对象，如果代码点不是已定义块的成员，则返回`null`。 |

**String 类中的方法**

`String`，`StringBuffer`和`StringBuilder`类也有使用补充字符的构造函数和方法。下表列出了一些常用方法。 有关可用API的完整列表，请参阅[`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html)，[`StringBuffer` ](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html)和[`StringBuilder`](https://docs.oracle.com/javase/8/docs/api /java/lang/StringBuilder.html)类的 javadoc。

| Constructor or Methods                   | Description                              |
| ---------------------------------------- | ---------------------------------------- |
| [`String(int[] codePoints, int offset, int count)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#String-int:A-int-int-) | 分配一个新的`String`实例，该实例包含Unicode代码点数组的子数组中的字符。 |
| [`String.codePointAt(int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#codePointAt-int-)<br />[`StringBuffer.codePointAt(int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html#codePointAt-int-)<br />[`StringBuilder.codePointAt(int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#codePointAt-int-) | 返回指定索引处的Unicode代码点。                      |
| [`String.codePointBefore(int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#codePointBefore-int-)<br />[`StringBuffer.codePointBefore(int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html#codePointBefore-int-)<br />[`StringBuilder.codePointBefore(int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#codePointBefore-int-) | 返回指定索引之前的Unicode代码点。                     |
| [`String.codePointCount(int beginIndex, int endIndex)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#codePointCount-int-int-) [`StringBuffer.codePointCount(int beginIndex, int endIndex)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html#codePointCount-int-int-) [`StringBuilder.codePointCount(int beginIndex, int endIndex)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#codePointCount-int-int-) | 返回指定范围内的Unicode代码点数。                     |
| [`StringBuffer.appendCodePoint(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html#appendCodePoint-int-) [`StringBuilder.appendCodePoint(int codePoint)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#appendCodePoint-int-) | 将指定代码点的字符串表示形式追加到序列中。                    |
| [`String.offsetByCodePoints(int index, int codePointOffset)`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#offsetByCodePoints-int-int-) [`StringBuffer.offsetByCodePoints(int index, int codePointOffset)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuffer.html#offsetByCodePoints-int-int-) [`StringBuilder.offsetByCodePoints(int index, int codePointOffset)`](https://docs.oracle.com/javase/8/docs/api/java/lang/StringBuilder.html#offsetByCodePoints-int-int-) | 返回给定索引偏移给定数量的代码点的索引。                     |

#### 例子

此页面包含一些代码片段，向您展示几个常见方案。

**从代码点创建 `String`**

```java
String newString(int codePoint) {
    return new String(Character.toChars(codePoint));
}
```

**从代码点创建`String`  - 针对BMP字符进行优化**

`Character.toChars`方法创建一个临时数组，该数组使用一次然后丢弃。如果这会对性能产生负面影响，则可以使用以下方法对BMP字符进行优化（由单个`char`值表示的字符）。在这种方法中，只为补充字符调用`toChars`。

```java
String newString(int codePoint) {
    if (Character.charCount(codePoint) == 1) {
        return String.valueOf(codePoint);
    } else {
        return new String(Character.toChars(codePoint));
    }
}
```

**批量创建 `String` 对象**

要创建大量字符串，前一个代码段的批量版本会重用`toChars`方法使用的数组。此方法为每个代码点创建一个单独的`String`实例，并针对BMP字符进行了优化。

```java
String[] newStrings(int[] codePoints) {
    String[] result = new String[codePoints.length];
    char[] codeUnits = new char[2];
    for (int i = 0; i < codePoints.length; i++) {
        int count = Character.toChars(codePoints[i], codeUnits, 0);
        result[i] = new String(codeUnits, 0, count);
    }
    return result;
}
```

**生成消息**

格式化API支持补充字符。以下示例是生成消息的简单方法。

```java
// recommended
System.out.printf("Character %c is invalid.%n", codePoint);
```

以下方法很简单并且避免了连接，这使得文本更难以本地化，因为并非所有语言都以与英语相同的顺序将数值插入到字符串中。

```java
// not recommended
System.out.println("Character " + String.valueOf(char) + " is invalid.");
```

#### 设计考量

要编写使用任何脚本无缝地为任何语言工作的代码，需要记住一些事项。

| Consideration                            | Reason                                   |
| ---------------------------------------- | ---------------------------------------- |
| 避免使用那些使用`char`数据类型的方法。                   | 避免使用`char`基本数据类型或使用`char`数据类型的方法，因为使用该数据类型的代码不适用于补充字符。对于采用`char`类型参数的方法，请使用相应的`int`方法（如果可用）。例如，使用`Character.isDigit(int)`方法而不是`Character.isDigit(char)`方法。 |
| 使用 `isValidCodePoint` 方法验证代码点值。          | 代码点被定义为`int`数据类型，它允许超出代码点值有效范围的值从 0x0000 到 0x10FFFF。出于性能原因，将代码点值作为参数的方法不会检查参数的有效性，但您可以使用`isValidCodePoint`方法来检查其值。 |
| 使用 `codePointCount` 方法来对字符计数。            | `String.length()`方法返回字符串中的代码单元数或16位`char`值。如果字符串包含增补字符，则计数可能会产生错误，因为它不会反映代码点的真实数量。要准确计算字符数（包括增补字符），请使用`codePointCount`方法。 |
| 使用 `String.toUpperCase(int codePoint)` 和 `String.toLowerCase(int codePoint)` 方法，而不是 `Character.toUpperCase(int codePoint)` 或者 `Character.toLowerCase(int codePoint)` 方法。 | 虽然`Character.toUpperCase(int)`和`Character.toLowerCase(int)`方法可以处理代码点值，但有些字符无法一对一转换。例如，小写的德语字符 ß 在转换为大写时变为两个字符 SS。同样，小希腊西格玛字符根据字符串中的位置而不同。`Character.toUpperCase(int)`和`Character.toLowerCase(int)`方法无法处理这些类型的情况; 但是，`String.toUpperCase`和`String.toLowerCase`方法正确处理这些情况。 |
| 请谨慎删除字符。                                 | 当调用索引指向补充字符的`StringBuilder.deleteCharAt(int index)`或`StringBuffer.deleteCharAt(int index)`方法时，只删除该字符的前半部分（第一个`char`值）。首先，在字符上调用`Character.charCount`方法，以确定是否必须删除一个或两个`char`值。 |
| 请谨慎逆序一个序列中的字符。                           | 当在包含增补字符的文本上调用`StringBuffer.reverse()`或`StringBuilder.reverse()`方法时，高和低代理对被反转，这导致不正确且可能无效的代理对。 |

#### 其它资源

For more information about supplementary characters, see the following resources.

- [Java 平台中的增补字符](http://www.oracle.com/technetwork/articles/javase/supplementary-142654.html)
- [Unicode联盟](http://unicode.org/)
- [Unicode术语表](http://unicode.org/glossary/)


### 探测文本边界

操作文本的应用程序需要定位文本中的边界。比如，考虑常见的文字处理软件功能：高亮一个字符、切分一个单词、移动光标到下一个语句，以及行尾单词的折行。为了执行这些功能，文字处理器必须能够探测文本中的逻辑边界。幸运的是，你不需要自己编写这种边界分析程序。你可以直接使用 [`BreakIterator`](https://docs.oracle.com/javase/8/docs/api/java/text/BreakIterator.html)  类提供的方法。

**[关于 BreakIterator 类](https://docs.oracle.com/javase/tutorial/i18n/text/about.html)**

本节讨论 `BreakIterator` 类的实例方法和虚拟光标。

**[字符边界](https://docs.oracle.com/javase/tutorial/i18n/text/char.html)**

本节中，你将学到用户字符和 Unicode 字符之间的差异，以及如何使用 `BreakIterator` 定位用户字符。

**[词汇边界](https://docs.oracle.com/javase/tutorial/i18n/text/word.html)**

如果你的应用程序需要选择或者定位文本中的单词，你将发现 `BreakIterator` 非常有用。

**[语句边界](https://docs.oracle.com/javase/tutorial/i18n/text/sentence.html)**

确定语句的边界可能是有问题的，因为语句这个术语在许多书面语言中含义并不明确。本节介绍几种你可能遇到的问题，以及 `BreakIterator` 类处理它们的方法。

**[行边界](https://docs.oracle.com/javase/tutorial/i18n/text/line.html)**

本节介绍如何使用 `BreakIterator` 类定义文本字符串中潜在的行。

#### 关于 BreakIterator 类

`BreakIterator` 类是区域敏感的，因为文本边界会因语言而不同。比如，不同的语言的断行语法规则是不同的。为了确定 `BreakIterator` 支持的区域，调用 `getAvailableLocales` 方法，如下：

```java
Locale[] locales = BreakIterator.getAvailableLocales();
```

你可以使用 `BreakIterator` 类分析四种边界：字符、单词、语句以及潜在断行。当实例化一个 `BreakIterator` 时，你调用合适的工厂方法：

- `getCharacterInstance`
- `getWordInstance`
- `getSentenceInstance`
- `getLineInstance`

每个 `BreakInterator` 实例只能够探测一种边界类型。如果你希望同时定位字符边界和单词边界，你需要创建两个单独的实例。

`BreakIterator` 拥有一个虚拟光标指向文本字符串中的当前边界。你可以在文本中使用`previous`和`next` 方法来移动该光标。比如，如果你已经使用`getWordInstance`创建了`BreakIterator`，每次你调用`next` 方法，该光标将移动到文本中的下一个单词边界。光标移动方法返回一个整数，表示边界的位置。此位置是文本字符串中将跟随边界的字符的索引。与字符串索引一样，边界从零开始。第一个边界处于位置0，最后一个边界是字符串的长度。下图显示了一行文本中`previous`和`next`方法检测到的单词边界：

[![The text 'Hope is the thing with feathers', with the boundaries indicated.](https://docs.oracle.com/javase/tutorial/figures/i18n/i18n-4.gif)](https://docs.oracle.com/javase/tutorial/figures/i18n/i18n-4.gif)
*此图片已缩小到适合页面。单击图像以其自然大小查看它。*

您应该仅将`BreakIterator`类与自然语言文本一起使用。要标记编程语言，请使用`StreamTokenizer`类。

以下部分给出了每种边界分析的示例。编码示例来自名为 [`BreakIteratorDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/BreakIteratorDemo.java) 的源代码文件。

#### 字符边界

如果你的应用允许终端用户高亮当个字符或者在文本中每次移动一个字符，就需要定位字符边界。为了创建一个`BreakIterator`实例来定位字符边界，调用`getCharacterInstance`方法，如下：

```java
BreakIterator characterIterator =
    BreakIterator.getCharacterInstance(currentLocale);
```

此类型的`BreakIterator`实例探测用户字符之间的边界，而不仅仅是 Unicode 字符。

一个用户字符可能由一个或者多个 Unicode 字符组成。比如，用户字符 ü 能够由结合 Unicode 字符 \u0075 (u) 和 \u00a8 (¨) 来构成。这不是最好的例子，因为用户字符 ü 还可以由单个的 Unicode 字符 \u00fc 表示。我们接下来使用阿拉伯语来举例。

阿拉伯语中的单词"房屋"是：

![The Arabic pictograph for House](https://docs.oracle.com/javase/tutorial/figures/i18n/i18n-5.gif)

这个单词包含三个用户字符，但是它是由下面六个 Unicode 字符组成：

```java
String house = "\u0628" + "\u064e" + "\u064a" + "\u0652" + "\u067a" + "\u064f";
```

`house`字符串中在位置1、3和5上的 Unicode 字符是变音符号。阿拉伯语中使用变音符号改变单词的含义。例子中的变音符号是非空格字符，因为它们出现在基本字符之上。在阿拉伯语的字处理软件中，你不能在屏幕上为每个字符串中的 Unicdoe 字符移动光标。相反，你必须为每个用户字符移动光标，而每个用户字符可能由多个 Unicode 字符组成。因此，你必须使用`BreakInterator`来扫描字符串中的用户字符。

例子程序 [`BreakIteratorDemo`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/BreakIteratorDemo.java) ，创建一个`BreakIterator`来扫描阿拉伯字符。改程序传递`BreakIterator`，以及之前创建的`String`对象，给名为`listPositions`的方法：

```java
BreakIterator arCharIterator = BreakIterator.getCharacterInstance(
                                   new Locale ("ar","SA"));
listPositions (house, arCharIterator);
```

`listPositions`方法使用一个`BreakIterator`来定位字符串中的字符边界。注意，`BreakIteratorDemo`使用`setText`方法将特定字符串分配给`BreakIterator`。改程序使用`first`方法来检索首个字符边界，然后调用`next`方法直到返回`BreakIterator.DONE`被返回。代码如下：

```java
static void listPositions(String target, BreakIterator iterator) {
                
    iterator.setText(target);
    int boundary = iterator.first();

    while (boundary != BreakIterator.DONE) {
        System.out.println (boundary);
        boundary = iterator.next();
    }
}
```

`listPositions`方法打印下面的字符串`house`中用户字符的字符边界位置。注意，其中的变音字符的位置没有列出：

```
0
2
4
6
```

#### 单词边界

通过调用`getWordIterator`方法来实例化`BreakIterator`以探测单词边界：

```java
BreakIterator wordIterator =
    BreakIterator.getWordInstance(currentLocale);
```

你将会希望创建这样一个`BreakIterator`，当你的应用程序需要操作单个词汇时。这些操作通常是常见的字处理功能，比如选择、剪切、粘贴以及拷贝等等。或者，你的应用程序可能需要搜索单词，同时它必须能够区别整个单词域简单的字符串。

当`BreakIterator`分析单词边界时，它区分单词和不属于单词一部分的字符。这些包含空格、制表符、标点符号以及大部分的符号等，两侧都是单词边界。

后面的示例（来自程序  [`BreakIteratorDemo`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/BreakIteratorDemo.java) ）标记了文本中的单词边界。该程序创建`BreakIterator`，然后调用`markBoundaries`方法：

```java
Locale currentLocale = new Locale ("en","US");

BreakIterator wordIterator =
    BreakIterator.getWordInstance(currentLocale);

String someText = "She stopped. " +
    "She said, \"Hello there,\" and then went " +
    "on.";

markBoundaries(someText, wordIterator);
```

`markBoundaries`方法在`BreakIteratorDemo.java`中定义。此方法通过在目标字符串下打印插入符号（^）来标记边界。在下面的代码中，注意`while`循环，其中`markBoundaries`通过调用`next`方法来扫描字符串：

```java
static void markBoundaries(String target, BreakIterator iterator) {

    StringBuffer markers = new StringBuffer();
    markers.setLength(target.length() + 1);
    for (int k = 0; k < markers.length(); k++) {
        markers.setCharAt(k,' ');
    }

    iterator.setText(target);
    int boundary = iterator.first();

    while (boundary != BreakIterator.DONE) {
        markers.setCharAt(boundary,'^');
        boundary = iterator.next();
    }

    System.out.println(target);
    System.out.println(markers);
}
```

`markBoundaries`方法的输出如下。注意插入符号（^）与标点符号和空格相关的位置：

```
She stopped.  She said, "Hello there," and then
^  ^^      ^^ ^  ^^   ^^^^    ^^    ^^^^  ^^   ^

went on.
^   ^^ ^^
```

`BreakIterator`类可以轻松地从文本中选择单词。您不必编写自己的例程来处理各种语言的标点符号规则， `BreakIterator`类为您完成此操作。

以下示例中的`extractWords`方法提取并打印给定字符串的单词。请注意，此方法使用`Character.isLetterOrDigit`来避免打印包含空格字符的“单词”。

```java
static void extractWords(String target, BreakIterator wordIterator) {

    wordIterator.setText(target);
    int start = wordIterator.first();
    int end = wordIterator.next();

    while (end != BreakIterator.DONE) {
        String word = target.substring(start,end);
        if (Character.isLetterOrDigit(word.charAt(0))) {
            System.out.println(word);
        }
        start = end;
        end = wordIterator.next();
    }
}
```

`BreakIteratorDemo`程序调用`extractWords`，并将其传递给前一个示例中使用的相同目标字符串。 `extractWords`方法打印出以下单词列表：

```
She
stopped
She
said
Hello
there
and
then
went
on
```

#### 语句边界

您可以使用`BreakIterator`来确定句子边界。首先使用`getSentenceInstance`方法创建`BreakIterator`：

```java
BreakIterator sentenceIterator =
    BreakIterator.getSentenceInstance(currentLocale);
```

为了显示句子边界，程序使用`markBoundaries`方法，该方法在  [Word Boundaries](https://docs.oracle.com/javase/tutorial/i18n/text/word.html) 一节中讨论。`markBoundaries`方法在字符串下面打印插入符号（^）以指示边界位置。这里有些例子：

```
She stopped.  She said, "Hello there," and then went on.
^             ^                                         ^

He's vanished!  What will we do?  It's up to us.
^               ^                 ^             ^

Please add 1.5 liters to the tank.
^                                 ^
```

#### 行边界

格式化文本或执行换行的应用程序必须找到潜在的换行符。您可以使用使用`getLineInstance`方法创建的`BreakIterator`找到这些换行符或边界：

```java
BreakIterator lineIterator =
    BreakIterator.getLineInstance(currentLocale);
```

此`BreakIterator`确定可以在下一行中断开以继续的文本在字符串中的位置。`BreakIterator`检测到的位置是潜在的换行符。屏幕上显示的实际换行符可能不一样。

下面的两个示例使用`BreakIteratorDemo.java`的`markBoundaries`方法来显示`BreakIterator`检测到的行边界。`markBoundaries`方法通过在目标字符串下面打印插入符号（^）来指示行边界。

根据`BreakIterator`，在一系列空白字符（空格，制表符，换行符）终止后会出现行边界。在以下示例中，请注意您可以在检测到的任何边界处断开行：

```
She stopped.  She said, "Hello there," and then went on.
^   ^         ^   ^     ^      ^     ^ ^   ^    ^    ^  ^
```

在连字符后立即发生潜在的换行：

```
There are twenty-four hours in a day.
^     ^   ^      ^    ^     ^  ^ ^   ^
```

下一个示例使用名为`formatLines`的方法将一长串文本分成固定长度的行。此方法使用`BreakIterator`来定位潜在的换行符。`formatLines`方法简短，而且由于`BreakIterator`，它与`locale`无关。下面是源代码：

```java
static void formatLines(
    String target, int maxLength,
    Locale currentLocale) {

    BreakIterator boundary = BreakIterator.
        getLineInstance(currentLocale);
    boundary.setText(target);
    int start = boundary.first();
    int end = boundary.next();
    int lineLength = 0;

    while (end != BreakIterator.DONE) {
        String word = target.substring(start,end);
        lineLength = lineLength + word.length();
        if (lineLength >= maxLength) {
            System.out.println();
            lineLength = word.length();
        }
        System.out.print(word);
        start = end;
        end = boundary.next();
    }
}
```

`BreakIteratorDemo`程序调用`formatLines`方法，如下所示：

```
String moreText =
    "She said, \"Hello there,\" and then " +
    "went on down the street. When she stopped " +
    "to look at the fur coats in a shop + "
    "window, her dog growled. \"Sorry Jake,\" " +
    "she said. \"I didn't know you would take " +
    "it personally.\"";

formatLines(moreText, 30, currentLocale);
```

 `formatLines` 的调用输出：

```
She said, "Hello there," and
then went on down the
street. When she stopped to
look at the fur coats in a
shop window, her dog
growled. "Sorry Jake," she
said. "I didn't know you
would take it personally."
```

### 将拉丁数字转化为其它 Unicode 数字

默认地，当文本包含数值时，那些数值使用拉丁数字显示。当需要使用其它 Unicode 数字字形时，使用 [`java.awt.font.NumericShaper`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html) 类。`NumericShaper` API 使得你可以以任何 Unicode 数字字形显示内部由 ASCII 编码表示的数值。

下面的代码片段，来自 [`ArabicDigits`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/ArabicDigits.java) 示例，显示了如何使用`NumericShaper`实例来转化拉丁数字为阿拉伯数字。确定字形的一行代码显示为粗体。

```java
ArabicDigitsPanel(String fontname) {
    HashMap map = new HashMap();
    Font font = new Font(fontname, Font.PLAIN, 60);
    map.put(TextAttribute.FONT, font);
    map.put(TextAttribute.NUMERIC_SHAPING,
        NumericShaper.getShaper(NumericShaper.ARABIC));

    FontRenderContext frc = new FontRenderContext(null, false, false);
    layout = new TextLayout(text, map, frc);
}

// ...

public void paint(Graphics g) {
    Graphics2D g2d = (Graphics2D)g;
    layout.draw(g2d, 10, 50);
}
```

用于阿拉伯数字的`NumericShaper`实例被获取并放入一个用于 [`TextLayout.NUMERIC_SHAPING`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/TextAttribute.html#NUMERIC_SHAPING) 属性键的`HashMap`。改散列映射被传入`TextLayout`接口。`paint`方法渲染文本之后，数字被期望中的脚本显示。这个例子中，拉丁数字0到9，显示为阿拉伯数字。

![ArabicDigits example output showing Arabic digits from 0 through 9](https://docs.oracle.com/javase/tutorial/figures/i18n/ArabicDigits.png)

前面的示例使用`NumericShaper.ARABIC`常量来检索所需的整形器，但`NumericShaper`类为许多语言提供常量。这些常量被定义为位掩码，并被称为`NumericShaper`的基于位掩码的常量。

**基于枚举的范围常量**

指定特定数字集的另一种方法是使用 [`NumericShaper.Range`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.Range.html) 枚举类型（枚举）。这个在Java SE 7发行版中引入的枚举也提供了一组常量。虽然这些常量是使用不同的机制定义的，但`NumericShaper.ARABIC`位掩码在功能上等同于`NumericShaper.Range.ARABIC`枚举，并且每个常量类型都有一个相应的`getShaper`方法：

- [`getShaper(int singleRange)`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getShaper-int-)
- [`getShaper(NumericShaper.Range singleRange)`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getShaper-java.awt.font.NumericShaper.Range-)

 [`ArabicDigitsEnum`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/ArabicDigitsEnum.java) 例子等同于上面的阿拉伯数字的例子，除了它使用了`NumericShaper.Range`枚举来指定语言脚本：

```java
ArabicDigitsEnumPanel(String fontname) {
    HashMap map = new HashMap();
    Font font = new Font(fontname, Font.PLAIN, 60);
    map.put(TextAttribute.FONT, font);
    map.put(TextAttribute.NUMERIC_SHAPING,
        NumericShaper.getShaper(NumericShaper.Range.ARABIC));
    FontRenderContext frc = new FontRenderContext(null, false, false);
    layout = new TextLayout(text, map, frc);
}
```

两种`getShaper` 方法都接受`singleRange`参数。使用其它常量类型，你可以指定一个特定脚本的数字范围。基于位掩码的常量能够通过`OR`组合使用，或者你可以创建一个`NumericShaper.Range`枚举集合。下面展示了如何使用每种常量类型定义范围：

```java
NumericShaper.MONGOLIAN | NumericShaper.THAI |
NumericShaper.TIBETAN
EnumSet.of(
    NumericShaper.Range.MONGOLIAN,
    NumericShaper.Range.THAI,
    NumericShaper.Range.TIBETAN)
```

你可以查询`NumericShaper`对象来确定它支持的范围，通过使用用于基于位掩码的造型器的 [`getRanges`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getRanges--) 方法，或者使用用于基于枚举的造型器的 [`getRangeSet`](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getRangeSet--) 方法。

------

注意：

您可以使用传统的基于位掩码的常量或基于`Range`枚举的常量。在决定使用哪个时，请考虑以下几点：

- `Range` API需要JDK 7或更高版本。
- `Range` API涵盖了比位掩码API更多的Unicode范围。
- 位掩码API比`Range` API快一点。

------

**根据语言上下文渲染数字**

 [`ArabicDigits`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/ArabicDigits.java) 示例旨在将造型器用于特定语言，但有时必须根据语言上下文呈现数字。例如，如果数字前面的文本使用泰语脚本，则首选泰语数字。如果文本以藏文显示，则首选藏文数字。

您可以使用`getContextualShaper`方法之一完成此操作：

- [getContextualShaper(int ranges)](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getContextualShaper-int-)
- [getContextualShaper(int ranges, int defaultContext)](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getContextualShaper-int-int-)
- [getContextualShaper(Set ranges)](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getContextualShaper-java.util.Set-)
- [getContextualShaper(Set ranges, NumericShaper.Range defaultContext)](https://docs.oracle.com/javase/8/docs/api/java/awt/font/NumericShaper.html#getContextualShaper-java.util.Set-java.awt.font.NumericShaper.Range-)

前两个方法使用位掩码常量，后两个使用枚举常量。接受`defaultContext`参数的方法使您可以指定在文本之前显示数值时使用的初始整形器。如果未定义默认上下文，则使用拉丁形状显示任何前导数字。

 [`ShapedDigits`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/ShapedDigits.java) 示例显示了整形器的工作方式。显示五个文本布局：

1. 第一种布局不使用整形器，所有数字均显示为拉丁文。
2. 无论语言上下文如何，第二种布局都将所有数字整形为阿拉伯数字。
3. 第三种布局采用了使用阿拉伯数字的上下文整形器。默认上下文定义为阿拉伯语。
4. 第四种布局采用使用阿拉伯数字的上下文整形器，但整形器不指定默认上下文。
5. 第五种布局采用了使用`ALL_RANGES`位掩码的上下文整形器，但整形器未指定默认上下文。

![ShapedDigits example output illustrating how contextual shapers work](https://docs.oracle.com/javase/tutorial/figures/i18n/ShapedDigits.png)

以下代码行显示了如何定义整形器，如果被使用了：

1. 没有使用整形器；
2. `NumericShaper arabic = NumericShaper.getShaper(NumericShaper.ARABIC);`
3. `NumericShaper contextualArabic = NumericShaper.getContextualShaper(NumericShaper.ARABIC, NumericShaper.ARABIC);`
4. `NumericShaper contextualArabicASCII = NumericShaper.getContextualShaper(NumericShaper.ARABIC);`
5. `NumericShaper contextualAll = NumericShaper.getContextualShaper(NumericShaper.ALL_RANGES);`

参考 [`ShapedDigits.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/ShapedDigits.java) 示例获取更多实现细节。

### 转化非 Unicode 文本

在Java编程语言中，`char`值表示Unicode字符。Unicode是一种支持世界主要语言的16位字符编码。您可以在[Unicode Consortium网站](http://www.unicode.org/) 上了解有关Unicode标准的更多信息。

很少有文本编辑器支持Unicode文本输入。我们用来编写本节代码示例的文本编辑器仅支持ASCII字符，限制为7位。为了表示不能用ASCII表示的Unicode字符，例如 ö，我们使用了`\uXXXX`转义序列。转义序列中的每个“X”都是十六进制数字。以下示例显示如何使用转义序列表示 ö 字符：

```java
String str = "\u00F6";
char c = '\u00F6';
Character letter = new Character('\u00F6');
```

世界各地的系统使用各种字符编码。目前，这些编码很少符合Unicode。因为您的程序需要Unicode中的字符，所以它从系统获取的文本数据必须转换为Unicode，反之亦然。当文本文件的编码与Java虚拟机的默认文件编码匹配时，文本文件中的数据将自动转换为Unicode。您可以通过使用它创建`OutputStreamWriter`并询问其规范名称来识别默认文件编码：

```java
OutputStreamWriter out = new OutputStreamWriter(new ByteArrayOutputStream());
System.out.println(out.getEncoding());
```

如果默认文件编码与您要处理的文本数据的编码不同，则必须自己执行转换。处理来自其他国家/地区或计算平台的文本时，您可能需要执行此操作。

本节讨论用于将非Unicode文本转换为Unicode的API。在使用这些API之前，您应该验证是否支持要转换为Unicode的字符编码。支持的字符编码列表不是Java编程语言规范的一部分。因此，API支持的字符编码可能随平台而变化。要查看Java Development Kit支持哪些编码，请参阅 [Supported Encodings](https://docs.oracle.com/javase/8/docs/technotes/guides/intl/encoding.doc.html) 文档。

下面的内容描述了将非Unicode文本转换为Unicode的两种技术。您可以将非Unicode字节数组转换为`String`对象，反之亦然。或者，您可以在Unicode字符流和非Unicode文本的字节流之间进行转换。

**[字节编码和字符串](https://docs.oracle.com/javase/tutorial/i18n/text/string.html)**

本节介绍如何将非Unicode字节数组转换为`String`对象，反之亦然。

**[字符和字节流](https://docs.oracle.com/javase/tutorial/i18n/text/stream.html)**

在本节中，您将学习如何在Unicode字符流和非Unicode文本字节流之间进行转换。

#### 字节编码和字符串

如果字节数组包含非Unicode文本，则可以使用`String`构造函数方法之一将文本转换为Unicode。相反，您可以使用`String.getBytes`方法将`String`对象转换为非Unicode字符的字节数组。调用这些方法之一时，请将编码标识符指定为其中一个参数。

下面的示例将在UTF-8和Unicode之间转换字符。UTF-8是Unicode的传输格式，对UNIX文件系统是安全的。该示例的完整源代码位于文件[`StringConverter.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/StringConverter.java) 中。

`StringConverter`程序首先创建一个包含Unicode字符的`String`：

```java
String original = new String("A" + "\u00ea" + "\u00f1" + "\u00fc" + "C");
```

打印时，名为`original`的`String`显示为：

```
AêñüC
```

要将`String`对象转换为UTF-8，请调用`getBytes`方法并将相应的编码标识符指定为参数。 `getBytes`方法返回UTF-8格式的字节数组。要从非Unicode字节数组创建`String`对象，请使用`encoding`参数调用`String`构造函数。进行这些调用的代码包含在`try`块中，以防指定的编码不受支持：

```java
try {
    byte[] utf8Bytes = original.getBytes("UTF8");
    byte[] defaultBytes = original.getBytes();

    String roundTrip = new String(utf8Bytes, "UTF8");
    System.out.println("roundTrip = " + roundTrip);
    System.out.println();
    printBytes(utf8Bytes, "utf8Bytes");
    System.out.println();
    printBytes(defaultBytes, "defaultBytes");
} 
catch (UnsupportedEncodingException e) {
    e.printStackTrace();
}
```

`StringConverter`程序打印出`utf8Bytes`和`defaultBytes`数组中的值以演示一个重要的点：转换后的文本的长度可能与源文本的长度不同。一些Unicode字符转换为单个字节，其他字符转换为成两字节或三字节字节。

`printBytes`方法通过调用`byteToHex`方法显示字节数组，该方法在源文件中定义，[`UnicodeFormatter.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/UnicodeFormatter.java) 。这是`printBytes`方法：

```java
public static void printBytes(byte[] array, String name) {
    for (int k = 0; k < array.length; k++) {
        System.out.println(name + "[" + k + "] = " + "0x" +
            UnicodeFormatter.byteToHex(array[k]));
    }
}
```

接下来是`printBytes`方法的输出。请注意，在两个数组中，只有第一个和最后一个字节A和C字符相同：

```
utf8Bytes[0] = 0x41
utf8Bytes[1] = 0xc3
utf8Bytes[2] = 0xaa
utf8Bytes[3] = 0xc3
utf8Bytes[4] = 0xb1
utf8Bytes[5] = 0xc3
utf8Bytes[6] = 0xbc
utf8Bytes[7] = 0x43
defaultBytes[0] = 0x41
defaultBytes[1] = 0xea
defaultBytes[2] = 0xf1
defaultBytes[3] = 0xfc
defaultBytes[4] = 0x43
```

#### 字符和字节流

`java.io`包提供了允许您在Unicode字符流和非Unicode文本的字节流之间进行转换的类。使用 [`InputStreamReader`](https://docs.oracle.com/javase/8/docs/api/java/io/InputStreamReader.html) 类，您可以将字节流转换为字符流。使用 [`OutputStreamWriter`](https://docs.oracle.com/javase/8/docs/api/java/io/OutputStreamWriter.html) 类将字符流转换为字节流。下图说明了转换过程：

![This figure represents the conversion process](https://docs.oracle.com/javase/tutorial/figures/i18n/i18n-6.gif)

创建`InputStreamReader`和`OutputStreamWriter`对象时，指定要转换的字节编码。例如，要将UTF-8编码的文本文件转换为Unicode，您可以创建一个`InputStreamReader`，如下所示：

```java
FileInputStream fis = new FileInputStream("test.txt");
InputStreamReader isr = new InputStreamReader(fis, "UTF8");
```

如果省略编码标识符，`InputStreamReader`和`OutputStreamWriter`依赖于默认编码。您可以通过调用`getEncoding`方法来确定`InputStreamReader`或`OutputStreamWriter`使用的编码，如下所示：

```java
InputStreamReader defaultReader = new InputStreamReader(fis);
String defaultEncoding = defaultReader.getEncoding();
```

下面的示例向您展示了如何使用`InputStreamReader`和`OutputStreamWriter`类执行字符集转换。此示例的完整源代码位于[`StreamConverter.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/StreamConverter.java) 中。该程序显示日文字符。在尝试之前，请验证系统上是否安装了相应的字体。如果您使用的是与1.1版兼容的JDK软件，请复制`font.properties`文件，然后将其替换为`font.properties.ja`文件。

`StreamConverter`程序将一个Unicode字符序列从`String`对象转换为以UTF-8编码的字节的`FileOutputStream`。执行转换的方法称为`writeOutput`：

```java
static void writeOutput(String str) {
    try {
        FileOutputStream fos = new FileOutputStream("test.txt");
        Writer out = new OutputStreamWriter(fos, "UTF8");
        out.write(str);
        out.close();
    } 
    catch (IOException e) {
        e.printStackTrace();
    }
}
```

`readInput`方法从`writeOutput`方法创建的文件中读取以UTF-8编码的字节。 `InputStreamReader`对象将UTF-8中的字节转换为Unicode，并将结果返回给`String`。 `readInput`方法如下：

```java
static String readInput() {
    StringBuffer buffer = new StringBuffer();
    try {
        FileInputStream fis = new FileInputStream("test.txt");
        InputStreamReader isr = new InputStreamReader(fis, "UTF8");
        Reader in = new BufferedReader(isr);
        int ch;
        while ((ch = in.read()) > -1) {
            buffer.append((char)ch);
        }
        in.close();
        return buffer.toString();
    } 
    catch (IOException e) {
        e.printStackTrace();
        return null;
    }
}
```

`StreamConverter`程序的`main`方法调用`writeOutput`方法来创建以UTF-8编码的字节文件。 `readInput`方法读取相同的文件，将字节转换回Unicode。 这是`main`方法的源代码：

```java
public static void main(String[] args) {
    String jaString = new String("\u65e5\u672c\u8a9e\u6587\u5b57\u5217");
    writeOutput(jaString); 
    String inputString = readInput();
    String displayString = jaString + " " + inputString;
    new ShowString(displayString, "Conversion Demo");
}
```

原始字符串（`jaString`）应该与新创建的字符串（`inputString`）相同。为了显示两个字符串是相同的，程序将它们连接起来并用`ShowString`对象显示它们。 `ShowString`类显示带有`Graphics.drawString`方法的字符串。该类的源代码位于 [`ShowString.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/ShowString.java) 中。当`StreamConverter`程序实例化`ShowString`时，会出现以下窗口。显示的字符重复验证两个字符串是否相同：

![This is a screens hot of the StreamConverter program](https://docs.oracle.com/javase/tutorial/figures/i18n/conversion.gif)

### 规范化文本

*规范化*是一个过程，通过它您可以执行某些文本转换，使其可以以前所未有的方式进行协调。假设您想要搜索或排序文本，在这种情况下，您需要将该文本规范化以考虑应该表示为相同文本的代码点。

什么可以规范化？当您需要转换使用变音符号的字符，更改所有字母大小写，分解连字或将半角片假名字符转换为全角字符等时，可以应用规范化。

根据 [Unicode Standard Annex #15](http://www.unicode.org/reports/tr15/) ，Normalizer的API支持以下四种在 [`java.text.Normalizer.Form`](https://docs.oracle.com/javase/8/docs/api/java/text/Normalizer.Form.html) 中定义的Unicode文本规范化形式：

- 规范化形式D（NFD）：规范分解
- 规范化形式C（NFC）：规范分解，然后是规范组合
- 规范化形式KD（NFKD）：兼容性分解
- 规范化形式KC（NFKC）：兼容性分解，然后是规范组合

让我们来看看如何通过使用这些规范化形式来规范化带有分音符的拉丁文小写字母“o”：

| Original word | NFC     | NFD           | NFKC    | NFKD          |
| ------------- | ------- | ------------- | ------- | ------------- |
| "schön"       | "schön" | "scho\u0308n" | "schön" | "scho\u0308n" |

您可以注意到原始单词在 NFC 和 NFKC 中保持不变。这是因为使用 NFD 和 NFKD，复合字符被映射到它们的规范分解。但是对于 NFC 和 NFKC，如果可能的话，将组合字符序列映射到组合。由于没有用于分解的组合，因此它在 NFC 和 NFKC 中被分解。

在下面的代码示例  [`NormSample.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/NormSample.java) 中，您还可以注意到另一个规范化功能。半宽和全宽片假名字符将具有相同的兼容性分解，因此是兼容性等价物。但是，它们不是规范的等价物。

为了确保您确实需要对文本进行规范化，可以使用`isNormalized`方法来确定给定的`char`值序列是否已规范化。如果此方法返回`false`，则表示您必须规范化此序列，并且应使用`normalize`方法，该方法根据指定的规范化形式规范化`char`值。例如，要将文本转换为规范的分解形式，您必须使用以下`normalize`方法：

```java
normalized_string = Normalizer.normalize(target_chars, Normalizer.Form.NFD);
```

此外，`normalize`方法会将重音重新排列为正确的规范顺序，因此您无需担心自己的重音重排。

以下示例表示一个应用程序，使您可以选择规范化形式和要规范化的模板：

------

**注意:**  如果您没有看到 applet 正在运行，则需要至少安装 [Java SE Development Kit (JDK) 7](http://www.oracle.com/technetwork/java/javase/downloads/index.html) 版本。

------

此 applet 的完整代码在 [`NormSample.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/NormSample.java) 中。

### 使用JTextComponent类的双向文本

本节讨论如何使用 [`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 类处理双向文本。双向文本是包含从左到右和从右到左两个方向运行的文本的文本。双向文本的示例是包含数字（从左到右运行）的阿拉伯文本（从右向左运行）。显示和管理双向文本更加困难。但是 [`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 会为您处理这些问题。

本节涵盖以下主题：

- [确定双向文本的方向](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html#directionality)
- [显示和移动插入光标](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html#displaying-and-moving-carets)
- [命中测试](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html#hit-testing)
- [高亮选择](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html#highlighting-selections)
- [设置组件方向](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html#setting-component-orientation)

有关这些问题的更多信息，或者如果您希望在处理这些问题时有更多控制权，请参阅在 [2D Graphics](https://docs.oracle.com/javase/tutorial/2d/index.html) 中的 [Working with Bidirectional Text](https://docs.oracle.com/javase/tutorial/2d/text/textlayoutbidirectionaltext.html) 。

**[确定双向文本方向]()**

例子 [`BidiTextComponentDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/BidiTextComponentDemo.java) ，基于 [`TextComponentDemo.java`](https://docs.oracle.com/javase/tutorial/uiswing/examples/components/index.html#TextComponentDemo) ，在 [`JTextPane`](https://docs.oracle.com/javase/8/docs/api/javax/swing/JTextPane.html) 对象中显示双向文本。大多数情况下，Java 平台能够确定双向 Unicode 文本的方向：

![BidiTextComponentDemo.java](https://docs.oracle.com/javase/tutorial/figures/i18n/text/biditextcomponentdemo.jpg)

**在JTextComponent对象中显式指定文本方向**

你可以指定 [`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 对象的 [`Document`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/Document.html) 对象的方向。比如，下面的语句指定 [`JTextPane`](https://docs.oracle.com/javase/8/docs/api/javax/swing/JTextPane.html) 对象`textPane`中的文本方向为从右到左：

```java
textPane.getDocument().putProperty(
    TextAttribute.RUN_DIRECTION,
    TextAttribute.RUN_DIRECTION_RTL);
```

另外，你可以基于区域设置特定 Swing 组件的方向。比如，下面的语句基于区域`ar-SA`设定`textPane`对象的方向：

```java
Locale arabicSaudiArabia = 
    new Locale.Builder().setLanguage("ar").setRegion("SA").build();

textPane.setComponentOrientation(
    ComponentOrientation.getOrientation(arabicSaudiArabia));
```

由于阿拉伯语的运行方向是从右到左，因此`textPane`对象中包含的文本的方向也是从右到左。

有关更多信息，请参阅 [Setting Component Orientation](https://docs.oracle.com/javase/tutorial/i18n/text/bidi.html#setting-component-orientation) 一节。

**[显示和移动插入光标]()**

在可编辑文本中，插入符号用于以图形方式表示当前插入点，即文本中将插入新字符的位置。在 [`BidiTextComponentDemo.java`](https://docs.oracle.com/javase/tutorial/i18n/text/examples/BidiTextComponentDemo.java) 示例中，插入符号包含一个小三角形，指向插入字符的显示方向。

默认情况下， [`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 对象创建一个键映射（类型为 [`Keymap`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/Keymap.html)），该键映射由所有[`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 实例共享为默认键映射。键映射允许应用程序将键击绑定到操作。默认键映射（对于支持插入符移动的[`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 对象）包括使用左右箭头键向前和向后移动插入符号之间的绑定，以支持在双向文本中移动插入符号。

**[命中测试]()**

通常，设备空间中的位置必须转换为文本偏移量。例如，当用户在可选文本上单击鼠标时，鼠标的位置将转换为文本偏移并用作选择范围的一端。从逻辑上讲，这与定位插入符相反。

您可以将插入符侦听器附加到 [`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 的实例。插入符号侦听器使您能够处理插入符号事件，这些事件在插入符号移动或文本组件中的选择发生更改时发生。使用 [`addCaretListener`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html#addCaretListener-javax.swing.event.CaretListener-) 方法附加插入符侦听器。有关更多信息，请参见 [How to Write a Caret Listener](https://docs.oracle.com/javase/tutorial/uiswing/events/caretlistener.html) 。

**[高亮选择]()**

所选字符范围由高亮区域以图形方式表示，高亮区域是以逆视频或不同背景颜色显示字形的区域。

[`JTextComponent`](https://docs.oracle.com/javase/8/docs/api/javax/swing/text/JTextComponent.html) 对象实现逻辑高亮显示。这意味着所选字符在文本模型中始终是连续的，并且允许突出显示区域不连续。以下是逻辑高亮的示例：

![BidiTextComponentDemo: logical highlighting](https://docs.oracle.com/javase/tutorial/figures/i18n/text/biditextcomponentdemo-selected.jpg)

**[设置组件方向]()**

Swing 的布局管理器了解区域设置如何影响UI，没有必要为每个区域设置创建新布局。例如，在文本从右向左流动的区域设置中，布局管理器将以相同的方向排列组件。

示例 [`InternationalizedMortgageCalculator.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/InternationalizedMortgageCalculator.java) 已本地化为 English, United States; English, United Kingdom; French, France; French, Canada; and Arabic, Saudi Arabia。

以下使用 en-US 语言环境：

![Mortgage Calculator, en-US locale](https://docs.oracle.com/javase/tutorial/figures/i18n/format/mortgage-calculator-en-us.jpg)

以下使用 ar-SA 语言环境：

![Mortgage Calculator, ar-SA locale](https://docs.oracle.com/javase/tutorial/figures/i18n/format/mortgage-calculator-ar-sa.jpg)

请注意，组件的布局方向与相应的区域设置相同：en-US从左到右，ar-SA从右到左。 [`InternationalizedMortgageCalculator.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/InternationalizedMortgageCalculator.java) 示例调用方法 [`applyComponentOrientation`](https://docs.oracle.com/javase/8/docs/api/java/awt/Component.html#applyComponentOrientation-java.awt.ComponentOrientation-) 和 [`getOrientation`](https://docs.oracle.com/javase/8/docs/api/java/awt/ComponentOrientation.html#getOrientation-java.util.Locale-) 以按区域设置指定其组件的方向：

```java
private static JFrame frame;

// ...

private static void createAndShowGUI(Locale currentLocale) {

    // Create and set up the window.
    // ...
    // Add contents to the window.
    // ...
    frame.applyComponentOrientation(
        ComponentOrientation.getOrientation(currentLocale));
    // ...
  }
```

例子 [`InternationalizedMortgageCalculator.java`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/InternationalizedMortgageCalculator.java) 需要以下资源文件：

- [`resources/Resources.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/resources/Resources.properties)
- [`resources/Resources_ar.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/resources/Resources_ar.properties)
- [`resources/Resources_fr.properties`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/resources/Resources_fr.properties)


## 国际化网络资源

在现代互联网社区中，许多用户不再满足于仅使用ASCII符号来标识域名或Web资源。例如，他们希望能够使用阿拉伯语或中文的原生字符注册新域名。这就是为什么网络资源的国际化是扩大万维网视野的基石。

本课程介绍网络域名资源的国际化。

### 域名国际化

过去，Internet域名仅包含ASCII符号。随着互联网的普及并被全世界采用，有必要支持域名的国际化，特别是支持包含Unicode字符的域名。

采用国际化域名应用程序（IDNA）机制作为将Unicode字符转换为标准ASCII域名的标准，从而保持域名系统的稳定性。该系统执行查找服务以将用户友好名称转换为网络地址。

国际化域名的示例：

- `http://清华大学.cn`
- `http://www.транспорт.com`

如果您按照这些链接进行操作，您将看到地址栏中表示的Unicode域名被ASCII字符串替换。

为了在应用程序中实现类似的功能， [`java.net.IDN`](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html) 类提供了在ASCII和非ASCII格式之间转换域名的方法。

| Method                                   | Purpose                                  |
| ---------------------------------------- | ---------------------------------------- |
| [`toASCII(String)`](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html#toASCII-java.lang.String-)<br />[`toASCII(String, flag)`](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html#toASCII-java.lang.String-int-) | 在将IDN发送到域名解析系统或将IDN写入需要ASCII字符的文件（例如DNS主文件）之前使用。如果输入字符串不符合[RFC 3490](http://www.ietf.org/rfc/rfc3490.txt)，则这些方法会抛出`IllegalArgumentException`。 |
| [`toUnicode(String)`](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html#toUnicode-java.lang.String-)<br />[`toUnicode(String, flag)`](https://docs.oracle.com/javase/8/docs/api/java/net/IDN.html#toUnicode-java.lang.String-int-) | 在向用户显示名称时使用，例如从DNS区域获取的名称。此方法将字符串从ASCII兼容编码（ACE）转换为Unicode代码点。这种方法永远不会失败。如果出现错误，输入字符串保持不变，并且不加修改地返回。 |

可选的`flag`参数指定转换过程的行为。`ALLOW_UNASSIGNED`标志允许包含在Unicode 3.2中未分配的代码点。`USE_STD3_ASCII_RULES`标志确保遵守STD-3 ASCII规则。您可以单独使用这些标志，也可以逻辑“或”在一起使用。如果不需要任何标志，请使用该方法的单参数版本。

## 国际化服务提供者

国际化服务提供商支持依赖于语言环境的数据和服务的插件。因为可以插入依赖于语言环境的数据和服务，所以第三方能够提供在`java.text`和`java.util`包中大多数区域设置敏感类的实现。

服务是一组编程接口和类，可以访问特定应用程序的功能或特性。服务提供者接口（SPI）是服务定义的公共接口和抽象类的集合。服务提供商实现SPI。服务提供程序使您可以创建可扩展的应用程序，您可以在不修改其原始代码库的情况下进行扩展。您可以使用新的插件或模块增强其功能。有关服务提供程序和可扩展应用程序的更多信息，请参阅 [Creating Extensible Applications](https://docs.oracle.com/javase/tutorial/ext/basics/spi.html) 。

你可以使用国际化服务提供商来提供下面这些区域敏感类的自定义实现：

- [`BreakIterator`](https://docs.oracle.com/javase/8/docs/api/java/text/BreakIterator.html) 对象
- [`Collator`](https://docs.oracle.com/javase/8/docs/api/java/text/Collator.html) 对象
- 语言编码，国家编码，以及 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 类的变种名称
- 时区名称
- 货币符号
- [`DateFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/DateFormat.html) 对象
- [`DateFormatSymbols`](https://docs.oracle.com/javase/8/docs/api/java/text/DateFormatSymbols.html) 对象
- [`NumberFormat`](https://docs.oracle.com/javase/8/docs/api/java/text/NumberFormat.html) 对象
- [`DecimalFormatSymbols`](https://docs.oracle.com/javase/8/docs/api/java/text/DecimalFormatSymbols.html) 对象

相应的 SPIs 被包含在 `java.text.spi` 和 `java.util.spi` 包中：

| `java.util.spi`                          | `java.text.spi`                          |
| ---------------------------------------- | ---------------------------------------- |
| [`CurrencyNameProvider`](https://docs.oracle.com/javase/8/docs/api/java/util/spi/CurrencyNameProvider.html)[`LocaleServiceProvider`](https://docs.oracle.com/javase/8/docs/api/java/util/spi/LocaleServiceProvider.html)[`TimeZoneNameProvider`](https://docs.oracle.com/javase/8/docs/api/java/util/spi/TimeZoneNameProvider.html) | [`BreakIteratorProvider`](https://docs.oracle.com/javase/8/docs/api/java/text/spi/BreakIteratorProvider.html)[`CollatorProvider`](https://docs.oracle.com/javase/8/docs/api/java/text/spi/CollatorProvider.html)[`DateFormatProvider`](https://docs.oracle.com/javase/8/docs/api/java/text/spi/DateFormatProvider.html)[`DateFormatSymbolsProvider`](https://docs.oracle.com/javase/8/docs/api/java/text/spi/DateFormatSymbolsProvider.html)[`DecimalFormatSymbolsProvider`](https://docs.oracle.com/javase/8/docs/api/java/text/spi/DecimalFormatSymbolsProvider.html)[`NumberFormatProvider`](https://docs.oracle.com/javase/8/docs/api/java/text/spi/NumberFormatProvider.html) |

比如，如果你希望为一个新的区域提供 `NumberFormat` 对象，实现 `java.text.spi.NumberFormatProvider` 类并实现以下方法：

- `getCurrencyInstance(Locale locale)`
- `getIntegerInstance(Locale locale)`
- `getNumberInstance(Locale locale)`
- `getPercentInstance(Locale locale)`

```java
Locale loc = new Locale("da", "DK");
NumberFormat nf = NumberFormatProvider.getNumberInstance(loc);
```

这些方法首先检查Java运行时环境是否支持所请求的语言环境。如果是这样，方法使用该支持。否则，这些方法会调用已安装提供程序的`getAvailableLocales`方法以获取适当的接口，以查找支持所请求区域设置的提供程序。

有关如何使用服务提供程序进行国际化的深入示例，请参阅 [Installing a Custom Resource Bundle as an Extension](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html)。本节介绍如何实现[`ResourceBundleControlProvider`](https://docs.oracle.com/javase/8/docs/api/java/util/spi/ResourceBundleControlProvider.html) 接口，该接口使您可以使用任何自定义`ResourceBundle.Control`类，而无需对应用程序的源代码进行任何其他更改。

### 作为扩展安装自定义资源包

 [Customizing Resource Bundle Loading](https://docs.oracle.com/javase/tutorial/i18n/resbundle/control.html) 一节介绍了如何更改资源包的加载方式。这涉及从[`ResourceBundle.Control`](https://docs.oracle.com/javase/8/docs/api/java/util/ResourceBundle.Control.html) 派生一个新类，然后通过调用以下方法检索资源包：

```java
ResourceBundle getBundle(
  String baseName,
  Locale targetLocale,
  ResourceBundle.Control control)
```

参数 `control` 是你的 `ResourceBundle.Control` 实现。

 [`java.util.spi.ResourceBundleControlProvider`](https://docs.oracle.com/javase/8/docs/api/java/util/spi/ResourceBundleControlProvider.html) 接口允许你改变下面方法加载资源包的方式：

```java
ResourceBundle getBundle(
  String baseName,
  Locale targetLocale)
```

请注意，此版本的 [`ResourceBundle.getBundle`](https://docs.oracle.com/javase/8/docs/api/java/util/ResourceBundle.html#getBundle-java.lang.String-java.util.Locale-) 方法不需要`ResourceBundle.Control`类的实例。`ResourceBundleControlProvider`是服务提供者接口（SPI）。SPI使您能够创建可扩展的应用程序，这些应用程序可以轻松扩展而无需修改其原始代码库。有关更多信息，请参阅 [Creating Extensible Applications](https://docs.oracle.com/javase/tutorial/ext/basics/spi.html) 。

要使用SPI，首先要通过实现类似`ResourceBundleControlProvider`的SPI来创建服务提供者。实现SPI时，指定它将如何提供服务。`ResourceBundleControlProvider` SPI提供的服务是在应用程序调用`ResourceBundle.getBundle(String baseName, Locale targetLocale)`方法时获取适当的`ResourceBundle.Control`实例。您将服务提供程序与Java扩展机制打包为已安装的扩展。运行应用程序时，不要在类路径中命名扩展名；运行时环境查找并加载这些扩展。

已安装的`ResourceBundleControlProvider` SPI实现替换了默认的`ResourceBundle.Control`类（它定义了默认的资源包加载过程）。因此，`ResourceBundleControlProvider`接口使您可以使用任何自定义`ResourceBundle.Control`类，而无需对应用程序的源代码进行任何其他更改。此外，此接口使您可以编写应用程序，而无需引用任何自定义ResourceBundle.Control类。

 [`RBCPTest.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/RBCPTest.java) 示例显示了如何实现`ResourceBundleControlProvider`接口以及如何将其打包为已安装的扩展。此示例包装在zip文件`RBCPTest.zip`中，包含以下文件：

- ```
  src
  ```

  - [`java.util.spi.ResourceBundleControlProvider`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/java.util.spi.ResourceBundleControlProvider)

  - [`RBCPTest.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/RBCPTest.java)

  - ```
    rbcp
    ```

    - [`PropertiesResourceBundleControl.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/PropertiesResourceBundleControl.java)
    - [`PropertiesResourceBundleControlProvider.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/PropertiesResourceBundleControlProvider.java)
    - [`XMLResourceBundleControl.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/XMLResourceBundleControl.java)
    - [`XMLResourceBundleControlProvider.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/XMLResourceBundleControlProvider.java)

  - ```
    resources
    ```

    - [`RBControl.properties`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/RBControl.properties)
    - [`RBControl_zh.properties`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/RBControl_zh.properties)
    - [`RBControl_zh_CN.properties`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/RBControl_zh_CN.properties)
    - [`RBControl_zh_HK.properties`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/RBControl_zh_HK.properties)
    - [`RBControl_zh_TW.properties`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/RBControl_zh_TW.properties)
    - [`XmlRB.xml`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/XmlRB.xml)
    - [`XmlRB_ja.xml`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/resources/XmlRB_ja.xml)

- ```
  lib
  ```

  - [`rbcontrolprovider.jar`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#package-provider)

- `build`: 包含打包在 `rbcontrolprovider.jar` 中的所有文件以及类文件 `RBCPTest.class`

- [`build.xml`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/build.xml)

下面的步骤向你展示了如何重新创建 `RBCPTest.zip` 文件的内容，`RBCPTest`例子如何工作，以及如何运行它：

1. [创建 ResourceBundle.Control 类实现](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#create-implementations-of-resourcebundle.control)
2. [实现 ResourceBundleControlProvider 接口](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#implement-resourcebundlecontrolprovider)
3. [在你的应用中调用方法 ResourceBundle.getBundle](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#invoke-resourcebundle.getbundle)
4. [通过创建配置文件来注册服务提供者](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#register-service-provider)
5. [将服务提供者、它需要的类和配置文件到一个 JAR 包中](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#package-provider)
6. [运行 RBCPTest 程序](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/resourcebundlecontrolprovider.html#run-rbcptest)

**[1. 创建 ResourceBundle.Control 类实现]()**

 [`RBCPTest.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/RBCPTest.java) 示例使用 `ResourseBundle.Control` 的两种实现：

- [`PropertiesResourceBundleControlProvider.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/PropertiesResourceBundleControlProvider.java):  `ResourceBundle.Control` 与在 [Customizing Resource Bundle Loading](https://docs.oracle.com/javase/tutorial/i18n/resbundle/control.html) 中定义的 `ResourceBundle.Control` 实现相同。
- [`XMLResourceBundleControl.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/XMLResourceBundleControl.java): 此 `ResourceBundle.Control` 实现使用方法 [`Properties.loadFromXML`](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html#loadFromXML-java.io.InputStream-)加载基于 XML 的资源包。

**XML 属性文件**

如 [Backing a ResourceBundle with Properties Files](https://docs.oracle.com/javase/tutorial/i18n/resbundle/propfile.html) 章节中所述，属性文件是简单的文本文件。其中每一行都是一个键值对。XML 属性文件类似于普通属性文件：它们同样包含键值对，除了是 XML 结构。下面的 XML 属性文件 `XmlRB.xml`：

```xml
<?xml version="1.0" encoding="UTF-8"?>

<!DOCTYPE properties [
<!ELEMENT properties ( comment?, entry* ) >
<!ATTLIST properties version CDATA #FIXED "1.0">
<!ELEMENT comment (#PCDATA) >
<!ELEMENT entry (#PCDATA) >
<!ATTLIST entry key CDATA #REQUIRED>
]>

<properties>
    <comment>Test data for RBCPTest.java</comment>
    <entry key="type">XML</entry>
</properties>
```

下面是等价的属性文本文件内容：

```
# Test data for RBCPTest.java
type = XML
```

所有的 XML 属性文件都具有相同的结构：

- 指定文档类型定义（DTD）的DOCTYPE声明：DTD定义XML文件的结构。**注意：**您可以在XML属性文件中使用以下DOCTYPE声明：

  ```
  <!DOCTYPE properties SYSTEM "http://java.sun.com/dtd/properties.dtd">  
  ```

  导出或导入属性时不访问系统URI（http://java.sun.com/dtd/properties.dtd）; 它是一个唯一标识XML属性文件的DTD的字符串。

- 根元素`<properties>`：此元素包含所有其他元素。

- 任意数量的`<comment>`元素：这些元素用于注释。

- 任意数量的`<entry>`元素：使用属性`key`指定键; 指定`<entry>`标签之间的键值。

参考 [`Properties`](https://docs.oracle.com/javase/8/docs/api/java/util/Properties.html) 类获取有关 XML 属性文件的更多信息。

**[2. 实现 ResourceBundleControlProvider 接口]()**

此接口包含一个方法，即 [`ResourceBundle.Control getControl(String baseName)`](https://docs.oracle.com/javase/8/docs/api/java/util/spi/ResourceBundleControlProvider.html#getControl-java.lang.String-) 方法。参数`baseName`是资源包的名称。在`getBundle`的方法定义中，指定应该在给定资源包名称的情况下返回的`ResourceBundle.Control`实例。

`RBCPTest`示例包含`ResourceBundleControlProvider`接口的两个实现，[`PropertiesResourceBundleControlProvider.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/PropertiesResourceBundleControlProvider.java) 和 [`XMLResourceBundleControlProvider.java`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/rbcp/XMLResourceBundleControlProvider.java)。如果资源包的基本名称以`resources.RBControl`开头（在此示例中，所有资源文件都包含在包 `resources`中），则`PropertiesResourceBundleControlProvider.getBundle`方法返回`PropertiesResourceBundleControl`的实例：

```java
package rbcp;

import java.util.ResourceBundle;
import java.util.spi.ResourceBundleControlProvider;

public class PropertiesResourceBundleControlProvider
    implements ResourceBundleControlProvider {
    static final ResourceBundle.Control PROPERTIESCONTROL =
        new PropertiesResourceBundleControl();

    public ResourceBundle.Control getControl(String baseName) {
        System.out.println("Class: " + getClass().getName() + ".getControl");
        System.out.println("    called for " + baseName);

        // Throws a NPE if baseName is null.
        if (baseName.startsWith("resources.RBControl")) {
            System.out.println("    returns " + PROPERTIESCONTROL);
            return PROPERTIESCONTROL;
        }
        System.out.println("    returns null");
        System.out.println();
        return null;
    }
}
```

类似地，如果资源包的基本名称以`resources.Xml`开头，则`XMLResourceBundleControlProvider.getControl`方法返回`XMLResourceBundleControl`的实例。

注意：您可以创建`ResourceBundleControlProvider`接口的一个实现，该实现返回`PropertiesResourceBundleControl`或`XMLResourceBundleControl`的实例，具体取决于基本名称。

**[3. 在你的应用中调用方法 ResourceBundle.getBundle]()**

 `RBCPTest` 类使用方法 [`ResourceBundle.getBundle`](https://docs.oracle.com/javase/8/docs/api/java/util/ResourceBundle.html#getBundle-java.lang.String-java.util.Locale-) 检索资源包：

```java
import java.io.*;
import java.net.*;
import java.util.*;

public class RBCPTest {
    public static void main(String[] args) {
        ResourceBundle rb = ResourceBundle.getBundle(
            "resources.XmlRB", Locale.ROOT);
        String type = rb.getString("type");
        System.out.println("Root locale. Key, type: " + type);
        System.out.println();

        rb = ResourceBundle.getBundle("resources.XmlRB", Locale.JAPAN);
        type = rb.getString("type");
        System.out.println("Japan locale. Key, type: " + type);
        System.out.println();

        test(Locale.CHINA);
        test(new Locale("zh", "HK"));
        test(Locale.TAIWAN);
        test(Locale.CANADA);
    }

    private static void test(Locale locale) {
        ResourceBundle rb = ResourceBundle.getBundle(
            "resources.RBControl", locale);
        System.out.println("locale: " + locale);
        System.out.println("    region: " + rb.getString("region"));
        System.out.println("    language: " + rb.getString("language"));
        System.out.println();
    }
}
```

请注意，此类中不会出现`ResourceBundle.Control`或`ResourceBundleControlProvider`的任何实现。由于`ResourceBundleControlProvider`接口使用Java扩展机制，因此运行时环境会查找并加载这些实现。但是，使用 [`ServiceLoader`](https://docs.oracle.com/javase/8/docs/api/java/util/ServiceLoader.html) 类加载与Java扩展机制一起安装的`ResourceBundleControlProvider`实现和其他服务提供程序。使用此类意味着您必须使用配置文件注册服务提供程序，这将在下一步中介绍。

**[4. 通过创建配置文件来注册服务提供者]()**

配置文件的名称是提供程序实现的接口或类的完全限定名称。配置文件包含提供程序的完全限定类名。 [`java.util.spi.ResourceBundleControlProvider`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/src/java.util.spi.ResourceBundleControlProvider) 文件包含`PropertiesResourceBundleControlProvider`和`XMLResourceBundleControlProvider`的完全限定名称，每行一个名称：

```java
rbcp.XMLResourceBundleControlProvider
rbcp.PropertiesResourceBundleControlProvider
```

**[5. 将服务提供者、它需要的类和配置文件到一个 JAR 包中]()**

编译源文件。从包含`build.xml`文件的目录，运行下面的命令：

```
javac -d build src/java.* src/rbcp/*.java
```

此命令将编译`src`目录中包含的源文件，并将类文件放在`build`目录中。在Windows上，请确保使用反斜杠（\）分隔目录和文件名。

创建一个JAR文件，其中包含以下目录结构中的已编译类文件，资源文件和配置文件：

- ```
  META-INF
  ```

  - ```
    services
    ```

    - `java.util.spi.ResourceBundleControlProvider`

- ```
  rbcp
  ```

  - `PropertiesResourceBundleControl.class`
  - `PropertiesResourceBundleControlProvider.class`
  - `XMLResourceBundleControl.class`
  - `XMLResourceBundleControlProvider.class`

- ```
  resources
  ```

  - `RBControl.properties`
  - `RBControl_zh.properties`
  - `RBControl_zh_CN.properties`
  - `RBControl_zh_HK.properties`
  - `RBControl_zh_TW.properties`
  - `XmlRB.xml`
  - `XmlRB_ja.xml`

请注意，配置文件`java.util.spi.ResourceBundleControlProvider`必须打包在目录`/META-INF/services`中。此示例将这些文件打包到`lib`目录中的JAR文件`rbcontrolprovider.jar`中。

参考 [Packaging Programs in JAR Files](https://docs.oracle.com/javase/tutorial/deployment/jar/index.html) 获取有关创建 JAR 文件的更多信息。

或者，下载并安装 [Apache Ant](http://ant.apache.org/) ，这是一个使您能够自动化构建过程的工具，例如编译Java文件和创建JAR文件。确保Apache Ant可执行文件位于`PATH`环境变量中，以便您可以从任何目录运行它。安装Apache Ant后，请按照下列步骤操作：

1. 编辑文件 [`build.xml`](https://docs.oracle.com/javase/tutorial/i18n/serviceproviders/examples/rbcpsample/build.xml) 并修改 `${JAVAC}` 为你的 Java 编译器、 `javac` 的完整路径名，修改 `${JAVA}` 为你的 Java 可执行运行时`java`的完整路径名。 

2. 从包含文件`build.xml`的同一目录运行以下命令：

   ```
   ant jar
   ```

   此命令编译Java源文件，并将它们以及所需的资源和配置文件打包到`lib`目录中的JAR文件`rbcontrolprovider.jar`中。

**[6. 运行 RBCPTest 程序]()**

在命令提示符处，从包含`build.xml`文件的目录运行以下命令：

```
java -Djava.ext.dirs=lib -cp build RBCPTest
```

此命令假定以下内容：

- 包含RBCPTest示例的已编译代码的JAR文件位于目录`lib`中。
- 编译的类`RBCPTest.class`位于 `build` 目录中。

或者，使用Apache Ant并从包含`build.xml`文件的目录运行以下命令：

```
ant run
```

安装Java扩展时，通常将扩展的JAR文件放在JRE的`lib/ext`目录中。但是，此命令指定包含具有系统属性`java.ext.dirs`的Java扩展的目录。

`RBCPTest`程序首先尝试使用基本名称`resources.XmlRB`和语言环境`Locale.ROOT`和`Local.JAPAN`检索资源包。检索这些资源包的程序输出类似于以下内容：

```
Class: rbcp.XMLResourceBundleControlProvider.getControl
    called for resources.XmlRB
    returns rbcp.XMLResourceBundleControl@16c1857
Root locale. Key, type: XML

Class: rbcp.XMLResourceBundleControlProvider.getControl
    called for resources.XmlRB
    returns rbcp.XMLResourceBundleControl@16c1857
Japan locale. Key, type: Value from Japan locale
```

该程序成功获取`XMLResourceBundleControl`的实例，并访问属性文件`XmlRB.xml`和`XmlRB_ja.xml`。

当`RBCPTest`程序尝试检索资源包时，它会调用配置文件`java.util.spi.ResourceBundleControlProvider`中定义的所有类。例如，当程序检索具有基本名称`resources.RBControl`和区域设置`Locale.CHINA`的资源包时，它将打印以下输出：

```
Class: rbcp.XMLResourceBundleControlProvider.getControl
    called for resources.RBControl
    returns null

Class: rbcp.PropertiesResourceBundleControlProvider.getControl
    called for resources.RBControl
    returns rbcp.PropertiesResourceBundleControl@1ad2911
locale: zh_CN
    region: China
    language: Simplified Chinese
```

# 反射

**反射的用途**

反射通常由程序使用，这些程序需要能够检查或修改在Java虚拟机中运行的应用程序的运行时行为。这是一个相对高级的功能，只有那些掌握了语言基础知识的开发人员才能使用。考虑到这一点，反射是一种强大的技术，可以使应用程序执行本来不可能的操作。

- 可扩展性功能
  应用程序可以通过使用完全限定名称创建可扩展性对象的实例来使用外部的用户定义类。
- 类浏览器和可视化开发环境
  类浏览器需要能够枚举类的成员。可视化开发环境可以从利用反射中可用的类型信息中受益，以帮助开发人员编写正确的代码。
- 调试器和测试工具
  调试器需要能够检查类上的私有成员。测试工具可以利用反射系统地调用类上定义的可发现的set API，以确保测试套件中的高级代码覆盖率。

**反射的缺点**

反思是强大的，但不应随意使用。如果可以在不使用反射的情况下执行操作，则优选避免使用它。通过反射访问代码时，应牢记以下问题。

- 性能开销
  由于反射涉及动态解析的类型，因此无法执行某些Java虚拟机优化。因此，反射操作的性能低于非反射操作，并且应避免在性能敏感应用程序中频繁调用的代码段中。
- 安全限制
  反射需要运行时权限，在安全管理器下运行时可能不具有此权限。对于必须在受限安全上下文中运行的代码，例如在Applet中，这是一个重要的考虑因素。
- 接触内部构件
  由于反射允许代码执行在非反射代码中非法的操作，例如访问私有字段和方法，因此使用反射会导致意外的副作用，这可能导致代码功能失常并可能破坏可移植性。反射代码打破了抽象，因此可能会通过升级平台来改变行为。

**内容**

此课程包含用于访问和操作类，字段，方法和构造函数的反射的常见用法。包含代码示例，提示和疑难解答信息。

- [![trail icon](https://docs.oracle.com/javase/tutorial/images/reflectionsm.GIF)**类**](https://docs.oracle.com/javase/tutorial/reflect/class/index.html)

  本课程展示了获取 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 对象的各种方法，并使用它来检查类属性，包括类的声明和内容。

- [![trail icon](https://docs.oracle.com/javase/tutorial/images/reflectionsm.GIF)**成员**](https://docs.oracle.com/javase/tutorial/reflect/member/index.html)

  本课程描述如何使用反射 API查找类的字段，方法和构造函数。提供了用于设置和获取字段值，调用方法以及使用特定构造函数创建对象的新实例的示例。

- [![trail icon](https://docs.oracle.com/javase/tutorial/images/reflectionsm.GIF)**数组和枚举类型**](https://docs.oracle.com/javase/tutorial/reflect/special/index.html)

  本课介绍两种特殊类型的类：在运行时生成的数组和枚举类型，它们定义唯一的命名对象实例。示例代码显示了如何检索数组的组件类型以及如何设置和获取具有数组或枚举类型的字段。

------

**注意：** 此课程中的示例旨在用于试验反射 API。因此，异常的处理与生产代码中使用的不同。特别是，在生产代码中，建议不要转储用户可见的堆栈跟踪信息。

------

## 类

每个类型要么是引用类型要么是基本类型，类、枚举以及数组（全部集成自[`java.lang.Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)）以及所有的接口都是引用类型。引用类型的例子包括[`java.lang.String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) ，所有基本数据类型的包装类，比如 [`java.lang.Double`](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html) ，接口 [`java.io.Serializable`](https://docs.oracle.com/javase/8/docs/api/java/io/Serializable.html) ，以及枚举 [`javax.swing.SortOrder`](https://docs.oracle.com/javase/8/docs/api/javax/swing/SortOrder.html) 。基本数据类型是固定的： `boolean`, `byte`, `short`, `int`, `long`, `char`, `float`, and `double` 。

对于每种类型的对象，Java虚拟机都实例化 [`java.lang.Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 的不可变实例，该实例提供检查对象的运行时属性的方法，包括其成员和类型信息。 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 还提供了创建新类和对象的功能。最重要的是，它是所有反射 API的入口点。本课程介绍了最常用的涉及类的反射操作：

- [Retrieving Class Objects](https://docs.oracle.com/javase/tutorial/reflect/class/classNew.html) 描述获取 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 的方法
- [Examining Class Modifiers and Types](https://docs.oracle.com/javase/tutorial/reflect/class/classModifiers.html) 展示如何访问类声明信息
- [Discovering Class Members](https://docs.oracle.com/javase/tutorial/reflect/class/classMembers.html) 举例说明如何列出构造器、字段、方法以及内部类
- [Troubleshooting](https://docs.oracle.com/javase/tutorial/reflect/class/classTrouble.html) 描述使用 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 时通常可能发生的错误


### 获取 Class 对象

所有反射操作的入口点都是 [`java.lang.Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html)。除了 [`java.lang.reflect.ReflectPermission`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/ReflectPermission.html) 。所有 [`java.lang.reflect`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/package-summary.html)  包中的类都没有`public` 的构造方法。为了获取这些类，必须调用 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 上的合适的方法。下面是集中获取 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 的几种方法，取决于代码是否能够访问一个对象，类名称，类型，或者一个已经存在的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html)。

**Object.getClass()**

如果一个对象实例可用，那么获取它的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 的最简单的方法就是调用[`Object.getClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#getClass--) 。当然，这仅仅适用于继承自 [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 的引用类型。如下所示：

```java
Class c = "foo".getClass();
```

为 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 返回 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) ：

```java
Class c = System.console().getClass();
```

通过`static`的方法 [`System.console()`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#console--) 返回与虚拟机关联的独一无二的控制台。 [`getClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#getClass--) 方法返回值就是对应于 [`java.io.Console`](https://docs.oracle.com/javase/8/docs/api/java/io/Console.html) 的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。

```java
enum E { A, B }
Class c = A.getClass();
```

`A` 是枚举类型 `E`的一个实例，因此 [`getClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#getClass--) 返回对应于枚举类型`E`的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。

```java
byte[] bytes = new byte[1024];
Class c = bytes.getClass();
```

因为数组是 [`Objects`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)，所以也可能对一个数组实例调用 [`getClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#getClass--) 。返回的[`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 对应于元素类型为`byte`的数组。

```java
import java.util.HashSet;
import java.util.Set;

Set<String> s = new HashSet<String>();
Class c = s.getClass();
```

这种情况下， [`java.util.Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html) 是 [`java.util.HashSet`](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html) 类型对象的一个接口， [`getClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#getClass--) 返回对应于 [`java.util.HashSet`](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html) 的[`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。

**`.class` 语法**

如果类型可用但没有实例，则可以通过在类型名称后附加`.class`来获取 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。这也是获取基本类型的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 的最简单方法。

```java
boolean b;
Class c = b.getClass();   // compile-time error

Class c = boolean.class;  // correct
```

注意，语句`boolean.getClass()`会产生一个编译错误，因为`boolean`是一个基本数据类型而不能被间接引用。`.class`语法返回对应于`boolean`类型的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。

```java
Class c = java.io.PrintStream.class;
```

变量`c`是对应于类型 [`java.io.PrintStream`](https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html) 的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) ：

```java
Class c = int[][][].class;
```

`.class`语法可以被用于获取对应于给定类型的多维数组的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。

**Class.forName()**

如果类的全限定名可用，则可能通过静态方法[`Class.forName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#forName-java.lang.String-) 来获取对应的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。这不能用于基本数据类型。用于数组类名称的语法由[`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--) 描述。该语法适用于引用类型和基本数据类型。

```java
Class c = Class.forName("com.duke.MyLocaleServiceProvider");
```

此语句将由给定的全限定名创建一个类。

```java
Class cDoubleArray = Class.forName("[D");

Class cStringArray = Class.forName("[[Ljava.lang.String;");
```

变量`cDoubleArray`将包含对应于基本类型`double`的数组的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) （即与`double[].class`相同）。`cStringArray`变量将包含对应于二维`String`数组的`Class`（即与`String[][].class`相同）。

**基本数据类型包装器的`TYPE`字段**

`.class`语法是获取基本类型的`Class`的更方便和首选的方法。然而，还有另一种获得`Class`的方法。每个基本类型和`void`在`java.lang`中都有一个包装类，用于将基本类型装箱到引用类型。每个包装类都包含一个名为`TYPE`的字段，该字段等于要包装的基本类型的`Class`。

```java
Class c = Double.TYPE;
```

当需要一个`Object`时，就需要使用`java.lang.Double`包装基本数据类型`double`，`Double.TYPE`的值等于`double.class`。

```java
Class c = Void.TYPE;
```

[`Void.TYPE`](https://docs.oracle.com/javase/8/docs/api/java/lang/Void.html#TYPE) 等于 `void.class` 。

**返回类的方法**

很多反射 API 会返回类，不过这些返回的类只能在已经直接或者间接获取到`Class`之后才能访问。

- [`Class.getSuperclass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getSuperclass--)

  返回给定类的超类。

  ```java
  Class c = javax.swing.JButton.class.getSuperclass();
  ```

   [`javax.swing.JButton`](https://docs.oracle.com/javase/8/docs/api/javax/swing/JButton.html) 的超类是 [`javax.swing.AbstractButton`](https://docs.oracle.com/javase/8/docs/api/javax/swing/AbstractButton.html) 。

- [`Class.getClasses()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getClasses--)

  返回作为类成员的所有`public`类、接口、以及枚举，包括继承来的成员。

  ```java
  Class<?>[] c = Character.class.getClasses(); 
  ```

  [`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) 包含两个成员类 [`Character.Subset`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.Subset.html) 和 [`Character.UnicodeBlock`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.UnicodeBlock.html) 。

- [`Class.getDeclaredClasses()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredClasses--)

  返回所有的类接口，以及在类中显式声明的枚举。

  ```java
  Class<?>[] c = Character.class.getDeclaredClasses(); 
  ```

  [`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) 包含两个类成员 [`Character.Subset`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.Subset.html) 和 [`Character.UnicodeBlock`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.UnicodeBlock.html) 以及一个私有类成员 `Character.CharacterCache` 。

- [`Class.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaringClass--) 

  [`java.lang.reflect.Field.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#getDeclaringClass--) 

  [`java.lang.reflect.Method.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getDeclaringClass--) 

  [`java.lang.reflect.Constructor.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#getDeclaringClass--)

  返回声明这些成员的`Class` 。 [Anonymous Class Declarations](https://docs.oracle.com/javase/specs/jls/se7/html/jls-15.html#jls-15.9.5) 将没有声明类，但是有一个封闭类。

  ```java
  import java.lang.reflect.Field;  

  Field f = System.class.getField("out"); 
  Class c = f.getDeclaringClass();
  ```

  字段 [`out`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#out) 被声明在 [`System`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html) 中。

  ```java
  public class MyClass {
      static Object o = new Object() {
          public void m() {} 
      };
      static Class<c> = o.getClass().getEnclosingClass();
  }
  ```

  `o`定义的匿名类的声明类为`null`。

- [`Class.getEnclosingClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnclosingClass--)

  返回类的直接封闭类。

  ```java
  Class c = Thread.State.class().getEnclosingClass();
  ```

  枚举 [`Thread.State`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.State.html) 的封闭类是 [`Thread`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html) 。

  ```java
  public class MyClass {
      static Object o = new Object() { 
          public void m() {} 
      };
      static Class<c> = o.getClass().getEnclosingClass();
  }
  ```

  由`o`定义的匿名类由`MyClass`包围。

### 检查类修饰符和类型

一个类声明中可以包含一个或者多个修饰符，这些修饰符影响它的运行时行为：

- 访问修饰符：`public`，`protected`，`private`
- 强制覆盖修饰符：`abstract`
- 限制为单个实例的修饰符：`static`
- 禁止值修改修饰符：`final`
- 强制严格浮点数行为修饰符：`strictfp`
- 注解

并不是所有的修饰符都能用于所有的类。比如，接口就不能是`final`的，而枚举不能是`abstract` 。[`java.lang.reflect.Modifier`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Modifier.html) 包含所有可能的修饰符的声明。它同样包含可以被用于对 [`Class.getModifiers()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getModifiers--) 返回的修饰符的集合进行解码的方法。

 [`ClassDeclarationSpy`](https://docs.oracle.com/javase/tutorial/reflect/class/example/ClassDeclarationSpy.java) 示例展示了如何获取一个类的声明组件，包括修饰符，泛型类型参数，实现的接口，以及继承路径等。由于 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 实现了 [`java.lang.reflect.AnnotatedElement`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AnnotatedElement.html) 接口，因此它也可能查询运行时注解。

```java
import java.lang.annotation.Annotation;
import java.lang.reflect.Modifier;
import java.lang.reflect.Type;
import java.lang.reflect.TypeVariable;
import java.util.Arrays;
import java.util.ArrayList;
import java.util.List;
import static java.lang.System.out;

public class ClassDeclarationSpy {
    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    out.format("Class:%n  %s%n%n", c.getCanonicalName());
	    out.format("Modifiers:%n  %s%n%n",
		       Modifier.toString(c.getModifiers()));

	    out.format("Type Parameters:%n");
	    TypeVariable[] tv = c.getTypeParameters();
	    if (tv.length != 0) {
		out.format("  ");
		for (TypeVariable t : tv)
		    out.format("%s ", t.getName());
		out.format("%n%n");
	    } else {
		out.format("  -- No Type Parameters --%n%n");
	    }

	    out.format("Implemented Interfaces:%n");
	    Type[] intfs = c.getGenericInterfaces();
	    if (intfs.length != 0) {
		for (Type intf : intfs)
		    out.format("  %s%n", intf.toString());
		out.format("%n");
	    } else {
		out.format("  -- No Implemented Interfaces --%n%n");
	    }

	    out.format("Inheritance Path:%n");
	    List<Class> l = new ArrayList<Class>();
	    printAncestor(c, l);
	    if (l.size() != 0) {
		for (Class<?> cl : l)
		    out.format("  %s%n", cl.getCanonicalName());
		out.format("%n");
	    } else {
		out.format("  -- No Super Classes --%n%n");
	    }

	    out.format("Annotations:%n");
	    Annotation[] ann = c.getAnnotations();
	    if (ann.length != 0) {
		for (Annotation a : ann)
		    out.format("  %s%n", a.toString());
		out.format("%n");
	    } else {
		out.format("  -- No Annotations --%n%n");
	    }

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }

    private static void printAncestor(Class<?> c, List<Class> l) {
	Class<?> ancestor = c.getSuperclass();
 	if (ancestor != null) {
	    l.add(ancestor);
	    printAncestor(ancestor, l);
 	}
    }
}
```

接下来是一些输出样本。用户输入以斜体显示。

$ *java ClassDeclarationSpy java.util.concurrent.ConcurrentNavigableMap*

```
Class:
  java.util.concurrent.ConcurrentNavigableMap

Modifiers:
  public abstract interface

Type Parameters:
  K V

Implemented Interfaces:
  java.util.concurrent.ConcurrentMap<K, V>
  java.util.NavigableMap<K, V>

Inheritance Path:
  -- No Super Classes --

Annotations:
  -- No Annotations --
```

下面是实际的源代码中 [`java.util.concurrent.ConcurrentNavigableMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentNavigableMap.html) 的声明：

```java
public interface ConcurrentNavigableMap<K,V>
    extends ConcurrentMap<K,V>, NavigableMap<K,V>
```

注意，由于这是一个接口，因而隐含是`abstract`的。编译器会为所有接口添加此修饰符。同时，此声明包含两个泛型类型参数，`K`和`V`。示例代码简单打印出这些参数的名称，但是我们可以通过 [`java.lang.reflect.TypeVariable`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/TypeVariable.html) 中的方法获取有关它们的更多信息。如上面所示，接口同样可以实现其它接口。

$ *java ClassDeclarationSpy "[Ljava.lang.String;"*

```
Class:
  java.lang.String[]

Modifiers:
  public abstract final

Type Parameters:
  -- No Type Parameters --

Implemented Interfaces:
  interface java.lang.Cloneable
  interface java.io.Serializable

Inheritance Path:
  java.lang.Object

Annotations:
  -- No Annotations --
```

由于数组是运行时对象，因此所有类型信息都由Java虚拟机定义。特别是，数组实现了 [`Cloneable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Cloneable.html) and [`java.io.Serializable`](https://docs.oracle.com/javase/8/docs/api/java/io/Serializable.html) ，它们的直接超类总是[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)。

$ *java ClassDeclarationSpy java.io.InterruptedIOException*

```
Class:
  java.io.InterruptedIOException

Modifiers:
  public

Type Parameters:
  -- No Type Parameters --

Implemented Interfaces:
  -- No Implemented Interfaces --

Inheritance Path:
  java.io.IOException
  java.lang.Exception
  java.lang.Throwable
  java.lang.Object

Annotations:
  -- No Annotations --
```

从继承路径可以推断出 [`java.io.InterruptedIOException`](https://docs.oracle.com/javase/8/docs/api/java/io/InterruptedIOException.html) 是一个受检查异常，因为继承路径中不存在 [`RuntimeException`](https://docs.oracle.com/javase/8/docs/api/java/lang/RuntimeException.html) 。

$ *java ClassDeclarationSpy java.security.Identity*

```
Class:
  java.security.Identity

Modifiers:
  public abstract

Type Parameters:
  -- No Type Parameters --

Implemented Interfaces:
  interface java.security.Principal
  interface java.io.Serializable

Inheritance Path:
  java.lang.Object

Annotations:
  @java.lang.Deprecated()
```

输出展示了 [`java.security.Identity`](https://docs.oracle.com/javase/8/docs/api/java/security/Identity.html)，一个废弃的 API，拥有注解 [`java.lang.Deprecated`](https://docs.oracle.com/javase/8/docs/api/java/lang/Deprecated.html) 。反射代码可以使用它来检测已弃用的API。

------

**注意：** 并非所有注解都可通过反射获得。只有那些具有 [`RUNTIME`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html#RUNTIME) 的 [`java.lang.annotation.RetentionPolicy`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html) 的注解才是可以访问的。在 Java 语言中预定义的 [`@Deprecated`](https://docs.oracle.com/javase/8/docs/api/java/lang/Deprecated.html) ， [`@Override`](https://docs.oracle.com/javase/8/docs/api/java/lang/Override.html) ，和 [`@SuppressWarnings`](https://docs.oracle.com/javase/8/docs/api/java/lang/SuppressWarnings.html) 这三个注解中，只有 [`@Deprecated`](https://docs.oracle.com/javase/8/docs/api/java/lang/Deprecated.html) 在运行时可用。

------

### 发现类成员

 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 中提供了两类用于访问字段，方法和构造函数的方法：枚举这些成员的方法和搜索特定成员的方法。还有一些不同的方法可以访问直接在类上声明的成员，而不是用于搜索继承成员的超接口和超类的方法。下表提供了所有成员定位方法及其特征的摘要。

| [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) API | List of members? | Inherited members? | Private members? |
| ---------------------------------------- | ---------------- | ------------------ | ---------------- |
| [`getDeclaredField()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredField-java.lang.String-) | no               | no                 | yes              |
| [`getField()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getField-java.lang.String-) | no               | yes                | no               |
| [`getDeclaredFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredFields--) | yes              | no                 | yes              |
| [`getFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getFields--) | yes              | yes                | no               |

| [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) API | List of members? | Inherited members? | Private members? |
| ---------------------------------------- | ---------------- | ------------------ | ---------------- |
| [`getDeclaredMethod()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredMethod-java.lang.String-java.lang.Class...-) | no               | no                 | yes              |
| [`getMethod()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getMethod-java.lang.String-java.lang.Class...-) | no               | yes                | no               |
| [`getDeclaredMethods()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredMethods--) | yes              | no                 | yes              |
| [`getMethods()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getMethods--) | yes              | yes                | no               |

| [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) API | List of members? | Inherited members? | Private members? |
| ---------------------------------------- | ---------------- | ------------------ | ---------------- |
| [`getDeclaredConstructor()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredConstructor-java.lang.Class...-) | no               | N/A                | yes              |
| [`getConstructor()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getConstructor-java.lang.Class...-) | no               | N/A                | no               |
| [`getDeclaredConstructors()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredConstructors--) | yes              | N/A                | yes              |
| [`getConstructors()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getConstructors--) | yes              | N/A                | no               |

N/A：构造器不会被继承。

给定类名并说明对哪些成员感兴趣， [`ClassSpy`](https://docs.oracle.com/javase/tutorial/reflect/class/example/ClassSpy.java) 示例使用 `get*s()` 方法来确定所有公共元素的列表，包括任何继承的元素。

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;
import java.lang.reflect.Member;
import static java.lang.System.out;

enum ClassMember { CONSTRUCTOR, FIELD, METHOD, CLASS, ALL }

public class ClassSpy {
    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    out.format("Class:%n  %s%n%n", c.getCanonicalName());

	    Package p = c.getPackage();
	    out.format("Package:%n  %s%n%n",
		       (p != null ? p.getName() : "-- No Package --"));

	    for (int i = 1; i < args.length; i++) {
		switch (ClassMember.valueOf(args[i])) {
		case CONSTRUCTOR:
		    printMembers(c.getConstructors(), "Constructor");
		    break;
		case FIELD:
		    printMembers(c.getFields(), "Fields");
		    break;
		case METHOD:
		    printMembers(c.getMethods(), "Methods");
		    break;
		case CLASS:
		    printClasses(c);
		    break;
		case ALL:
		    printMembers(c.getConstructors(), "Constuctors");
		    printMembers(c.getFields(), "Fields");
		    printMembers(c.getMethods(), "Methods");
		    printClasses(c);
		    break;
		default:
		    assert false;
		}
	    }

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }

    private static void printMembers(Member[] mbrs, String s) {
	out.format("%s:%n", s);
	for (Member mbr : mbrs) {
	    if (mbr instanceof Field)
		out.format("  %s%n", ((Field)mbr).toGenericString());
	    else if (mbr instanceof Constructor)
		out.format("  %s%n", ((Constructor)mbr).toGenericString());
	    else if (mbr instanceof Method)
		out.format("  %s%n", ((Method)mbr).toGenericString());
	}
	if (mbrs.length == 0)
	    out.format("  -- No %s --%n", s);
	out.format("%n");
    }

    private static void printClasses(Class<?> c) {
	out.format("Classes:%n");
	Class<?>[] clss = c.getClasses();
	for (Class<?> cls : clss)
	    out.format("  %s%n", cls.getCanonicalName());
	if (clss.length == 0)
	    out.format("  -- No member interfaces, classes, or enums --%n");
	out.format("%n");
    }
}

```

这个例子比较紧凑；但是 `printMembers()` 方法稍微有些尴尬，因为 [`java.lang.reflect.Member`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Member.html) 接口自最早的反射实现以来就已存在，并且在引入泛型时无法修改它以包含更有用的 `getGenericString()` 方法。唯一的选择是如示例所示进行测试和转换，用`printConstructors()`，`printFields()`和`printMethods()`替换此方法，或者对 [`Member.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Member.html#getName--) 的相对备用结果感到满意。

输出样本及其解释如下。 用户输入以斜体显示。

$ *java ClassSpy java.lang.ClassCastException CONSTRUCTOR*

```
Class:
  java.lang.ClassCastException

Package:
  java.lang

Constructor:
  public java.lang.ClassCastException()
  public java.lang.ClassCastException(java.lang.String)

```

由于构造函数是无法继承的，因此找不到直接超类 [`RuntimeException`](https://docs.oracle.com/javase/8/docs/api/java/lang/RuntimeException.html) 和其他超类中定义的异常链接机制构造函数（具有 [`Throwable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Throwable.html) 参数的构造函数）。

$ *java ClassSpy java.nio.channels.ReadableByteChannel METHOD*

```
Class:
  java.nio.channels.ReadableByteChannel

Package:
  java.nio.channels

Methods:
  public abstract int java.nio.channels.ReadableByteChannel.read
    (java.nio.ByteBuffer) throws java.io.IOException
  public abstract void java.nio.channels.Channel.close() throws
    java.io.IOException
  public abstract boolean java.nio.channels.Channel.isOpen()

```

接口 [`java.nio.channels.ReadableByteChannel`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/ReadableByteChannel.html) 定义了 [`read()`](https://docs.oracle.com/javase/8/docs/api/java/nio/channels/ReadableByteChannel.html#read-java.nio.ByteBuffer-) 。其余方法继承自超级接口。通过将 `get*s()` 替换为 `getDeclared*s()`，可以很容易地修改此代码以仅列出实际在类中声明的方法。

$ *java ClassSpy ClassMember FIELD METHOD*

```
Class:
  ClassMember

Package:
  -- No Package --

Fields:
  public static final ClassMember ClassMember.CONSTRUCTOR
  public static final ClassMember ClassMember.FIELD
  public static final ClassMember ClassMember.METHOD
  public static final ClassMember ClassMember.CLASS
  public static final ClassMember ClassMember.ALL

Methods:
  public static ClassMember ClassMember.valueOf(java.lang.String)
  public static ClassMember[] ClassMember.values()
  public final int java.lang.Enum.hashCode()
  public final int java.lang.Enum.compareTo(E)
  public int java.lang.Enum.compareTo(java.lang.Object)
  public final java.lang.String java.lang.Enum.name()
  public final boolean java.lang.Enum.equals(java.lang.Object)
  public java.lang.String java.lang.Enum.toString()
  public static <T> T java.lang.Enum.valueOf
    (java.lang.Class<T>,java.lang.String)
  public final java.lang.Class<E> java.lang.Enum.getDeclaringClass()
  public final int java.lang.Enum.ordinal()
  public final native java.lang.Class<?> java.lang.Object.getClass()
  public final native void java.lang.Object.wait(long) throws
    java.lang.InterruptedException
  public final void java.lang.Object.wait(long,int) throws
    java.lang.InterruptedException
  public final void java.lang.Object.wait() hrows java.lang.InterruptedException
  public final native void java.lang.Object.notify()
  public final native void java.lang.Object.notifyAll()

```

在这些结果的字段部分中，列出了枚举常量。虽然这些是专业性字段，但将它们与其他字段区分开来可能是有用的。可以修改此示例以使用 [`java.lang.reflect.Field.isEnumConstant()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isEnumConstant--) 来实现此目的。此课程的后续部分中的  [`EnumSpy`](https://docs.oracle.com/javase/tutorial/reflect/special/example/EnumSpy.java) 示例 [Examining Enums](https://docs.oracle.com/javase/tutorial/reflect/special/enumMembers.html) 包含可能的实现。

在输出的方法部分中，观察方法名称包含声明类的名称。因此，`toString()`方法由 [`Enum`](https://docs.oracle.com/javase/8/docs/api/java/lang/Enum.html#toString--) 实现，而不是从 [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 继承。可以使用 [`Field.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#getDeclaringClass--) 修改代码以使其更加明显。以下片段说明了潜在解决方案的一部分。

```java
if (mbr instanceof Field) {
    Field f = (Field)mbr;
    out.format("  %s%n", f.toGenericString());
    out.format("  -- declared in: %s%n", f.getDeclaringClass());
}
```

### 故障排除

下面的例子展示了当在类上使用反射时可能遇到的典型错误。

**编译器警告: "Note: ... uses unchecked or unsafe operations"**

当一个方法被调用时，参数值的类型被检查，并且可能被转化。[`ClassWarning`](https://docs.oracle.com/javase/tutorial/reflect/class/example/ClassWarning.java) 调用 [`getMethod()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getMethod-java.lang.String-java.lang.Class...-) 可能会产生一个典型的不受检查的转换警告：

```java
import java.lang.reflect.Method;

public class ClassWarning {
    void m() {
	try {
	    Class c = ClassWarning.class;
	    Method m = c.getMethod("m");  // warning

        // production code should handle this exception more gracefully
	} catch (NoSuchMethodException x) {
    	    x.printStackTrace();
    	}
    }
}
```

$ *javac ClassWarning.java*

```
Note: ClassWarning.java uses unchecked or unsafe operations.
Note: Recompile with -Xlint:unchecked for details.
```

$ *javac -Xlint:unchecked ClassWarning.java*

```
ClassWarning.java:6: warning: [unchecked] unchecked call to getMethod
  (String,Class<?>...) as a member of the raw type Class
Method m = c.getMethod("m");  // warning
                      ^
1 warning
```

许多类库方法已经使用范型声明进行了改造，包括 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 中的几个方法。由于`c`被声明为*raw*类型(没有类型参数)，同时 [`getMethod()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getMethod-java.lang.String-java.lang.Class...-) 方法的对应参数是一个参数化类型，会发生一个不受检查的转换。编译器需要生成警告。(参考 [*The Java Language Specification, Java SE 7 Edition*](https://docs.oracle.com/javase/specs/jls/se7/html/index.html) 章节 [Unchecked Conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.9) 和 [Method Invocation Conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.3) )

存在两种可能的解决方案。比较好的是修改`c`的声明来包含一个合适的范型类型。这种情况下，声明 应该是：

```java
Class<?> c = warn.getClass();
```

另外，警告应该使用预定义注解 [`@SuppressWarnings`](https://docs.oracle.com/javase/8/docs/api/java/lang/SuppressWarnings.html) 在有问题的语句之前被显式支持。

```java
Class c = ClassWarning.class;
@SuppressWarnings("unchecked")
Method m = c.getMethod("m");  
// warning gone
```

------

**提示：**作为一般原则，警告不应该被忽略，因为它们可能表明存在错误。应适当使用参数化声明。如果这不可能（可能是因为应用程序必须与库供应商的代码交互），请使用[`@SuppressWarnings`](https://docs.oracle.com/javase/8/docs/api/java/lang/SuppressWarnings.html) 注解违规行。

------

**当构造器不可访问时的实例化异常**

如果尝试创建类的一个新的实例，而类的无参构造器不可见，[`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 将抛出一个 [`InstantiationException`](https://docs.oracle.com/javase/8/docs/api/java/lang/InstantiationException.html) 。 [`ClassTrouble`](https://docs.oracle.com/javase/tutorial/reflect/class/example/ClassTrouble.java) 例子展示了结果追踪栈：

```java
class Cls {
    private Cls() {}
}

public class ClassTrouble {
    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName("Cls");
	    c.newInstance();  // InstantiationException

        // production code should handle these exceptions more gracefully
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java ClassTrouble*

```
java.lang.IllegalAccessException: Class ClassTrouble can not access a member of
  class Cls with modifiers "private"
        at sun.reflect.Reflection.ensureMemberAccess(Reflection.java:65)
        at java.lang.Class.newInstance0(Class.java:349)
        at java.lang.Class.newInstance(Class.java:308)
        at ClassTrouble.main(ClassTrouble.java:9)
```

[`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 的行为非常像 `new` 关键字，同样也会因为相同的原因而失败。在反射中典型的解决方案是利用 [`java.lang.reflect.AccessibleObject`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html) 类的优点，该类提供了压制访问控制检查的能力。不过，这种方法将无法工作，因为 [`java.lang.Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 并没有扩展 [`AccessibleObject`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html) 。所以，唯一的解决方案就是修改代码，使用 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) ，它扩展了 [`AccessibleObject`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html)。

------

**提示：**通常，由于 [Members](https://docs.oracle.com/javase/tutorial/reflect/member/index.html) 课程 [Creating New Class Instances](https://docs.oracle.com/javase/tutorial/reflect/member/ctorInstance.html) 章节中描述的原因，应该使用 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 。

------

使用 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 的潜在问题的更多的例子可以在 [Members](https://docs.oracle.com/javase/tutorial/reflect/member/index.html) 课程的 [Constructor Troubleshooting](https://docs.oracle.com/javase/tutorial/reflect/member/ctorTrouble.html) 章节中找到。

## 成员

反射定义了一个接口 [`java.lang.reflect.Member`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Member.html) ，被 [`java.lang.reflect.Field`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html) ，[`java.lang.reflect.Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html) ， 和 [`java.lang.reflect.Constructor`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html) 实现。这些对象将在本章中讨论。对每个成员，本课程将介绍相关的 API 来获取声明和类型信息，任何专属于该成员的操作（比如，设定字段值或者调用一个方法），以及可能常见的错误。接下来我们将使用代码样本和相关输出来说明每个概念，其近似于一些预期的反射应用场景。

------

**注意：** 根据 [*The Java Language Specification, Java SE 7 Edition*](https://docs.oracle.com/javase/specs/jls/se7/html/index.html) ，类的成员是继承的类主体组件，包括字段，方法，嵌套类，接口，以及枚举类型。由于构造器无法被继承，它们不是成员。这一点不同于 [`java.lang.reflect.Member`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Member.html) 的实现类。

------

**字段**

字段拥有类型和值两种属性。 [`java.lang.reflect.Field`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html) 类提供了相关的方法来访问字段的类型信息，设定和获取给定对象的一个字段的值。

- [获取字段类型](https://docs.oracle.com/javase/tutorial/reflect/member/fieldTypes.html) 描述如何获取字段的声明和泛型类型
- [检索和解析字段修饰符](https://docs.oracle.com/javase/tutorial/reflect/member/fieldModifiers.html) 展示如何获取字段声明中修饰符部分，比如 `public` 或者 `transient`
- [获取和设定字段值](https://docs.oracle.com/javase/tutorial/reflect/member/fieldValues.html) 举例说明如何访问字段值
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/member/fieldTrouble.html) 描述某些常见可能导致困惑的编码错误

**方法**

方法拥有返回值，参数，可能会抛出异常。 [`java.lang.reflect.Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html) 类提供了相关的方法来获取参数和返回值的类型信息。它也可以被用于调用给定对象上的方法。

- [获取方法类型信息](https://docs.oracle.com/javase/tutorial/reflect/member/methodType.html) 展示如何列出类中声明的方法，并获取类型信息
- [获取方法参数名称](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html) 展示如何获取一个方法或者构造器参数的名称和其它信息
- [获取并解析方法修饰符](https://docs.oracle.com/javase/tutorial/reflect/member/methodModifiers.html) 描述如何访问并解码与方法关联的修饰符及其它信息
- [调用方法](https://docs.oracle.com/javase/tutorial/reflect/member/methodInvocation.html) 举例说明如何执行一个方法并获取它的返回值
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/member/methodTrouble.html) 涵盖查找或者调用方法时的常见错误

**构造器**

用于构造器的反射 API 定义在 [`java.lang.reflect.Constructor`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html) 中，类似于用于方法的 API，除了两处意外：首先，构造器没有返回值；其次，构造器的调用创建一个跟定类的新的实例对象。

- [查找构造器](https://docs.oracle.com/javase/tutorial/reflect/member/ctorLocation.html) 举例说明如何获取携带特定参数的构造器
- [获取并解析构造器修饰符](https://docs.oracle.com/javase/tutorial/reflect/member/ctorModifiers.html) 展示如何获取构造器声明中的修饰符及有关该构造器的其它信息
- [创建新的类实例](https://docs.oracle.com/javase/tutorial/reflect/member/ctorInstance.html) 展示如何通过调用构造器实例化一个对象实例
- [故障排除Troubleshooting](https://docs.oracle.com/javase/tutorial/reflect/member/ctorTrouble.html) 描述在查找或者调用构造器时的常见错误

### 字段

*字段*是类、接口、或者枚举值。 [`java.lang.reflect.Field`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html) 类中的方法能够获取字段的信息，比如字段名称、类型、修饰符、以及注解。（ [Classes](https://docs.oracle.com/javase/tutorial/reflect/class/index.html) 课程中 [Examining Class Modifiers and Types](https://docs.oracle.com/javase/tutorial/reflect/class/classModifiers.html) 章节描述了如何获取注解。）同时还有方法可以动态访问和修改字段值。这些内容都包含在以下章节中：

- [获取字段类型](https://docs.oracle.com/javase/tutorial/reflect/member/fieldTypes.html) 描述如何获取字段声明和泛型类型
- [获取并解析字段修饰符](https://docs.oracle.com/javase/tutorial/reflect/member/fieldModifiers.html) 展示如何获取字段声明中的修饰符部分，比如 `public` 或者 `transient`
- [获取和设置字段值](https://docs.oracle.com/javase/tutorial/reflect/member/fieldValues.html) 举例说明如何访问字段值
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/member/fieldTrouble.html) 描述可能会导致迷惑的常见代码错误

当编写类似于类浏览器的应用程序时，查找哪些字段属于某个特定的类可能时很有用的。一个类的字段通过调用 [`Class.getFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getFields--) 方法来识别。 [`getFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getFields--) 方法返回一个 [`Field`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html) 对象数组，每个可访问的公共字段对应其中一个对象。

如果公共字段是以下任何一个的成员，则可以访问该字段：

- 这个类
- 这个类的超类
- 此类实现的接口
- 从此类实现的接口扩展的接口

字段可以是类（实例）字段，例如 [`java.io.Reader.lock`](https://docs.oracle.com/javase/8/docs/api/java/io/Reader.html#lock) ，静态字段，例如 [`java.lang.Integer.MAX_VALUE`](https://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html#MAX_VALUE)，或枚举常量，例如 [`java.lang.Thread.State.WAITING`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.State.html#WAITING) 。

#### 获取字段类型

字段，要么是基本数据类型，要么是引用类型。基本数据类型有 8 中：`boolean`，`byte`，`short`，`int` ，`long` ，`char`，`float`，以及`double`。引用类型是 [`java.lang.Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 的直接或者间接子类，包括接口、数组、以及枚举类型。

 [`FieldSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/FieldSpy.java) 示例给定一个全限定二进制类名，打印字段类型和泛型类型以及字段名。

```java
import java.lang.reflect.Field;
import java.util.List;

public class FieldSpy<T> {
    public boolean[][] b = {{ false, false }, { true, true } };
    public String name  = "Alice";
    public List<Integer> list;
    public T val;

    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    Field f = c.getField(args[1]);
	    System.out.format("Type: %s%n", f.getType());
	    System.out.format("GenericType: %s%n", f.getGenericType());

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	}
    }
}
```

示例输出获取到的类中的 3 个`public`字段类型（`b`，`name`，以及参数化类型的`list`）。接下来，用户输入用斜体表示：

$ *java FieldSpy FieldSpy b*

```
Type: class [[Z
GenericType: class [[Z
```

$ *java FieldSpy FieldSpy name*

```
Type: class java.lang.String
GenericType: class java.lang.String
```

$ *java FieldSpy FieldSpy list*

```
Type: interface java.util.List
GenericType: java.util.List<java.lang.Integer>
```

$ *java FieldSpy FieldSpy val*

```
Type: class java.lang.Object
GenericType: T
```

字段`b`的类型是布尔值的二维数组。类型名称的语法参见 [`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--) 。

字段`val`的类型被报告为 `java.lang.Object` ，因为泛型是通过类型擦除实现，编译期类型擦除会清除根性类型的所有类型信息。因此`T`被类型变量的上界所取代，这种情况下，是`java.lang.Object` 。

[`Field.getGenericType()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#getGenericType--) 将查询类文件中的签名属性（如果存在）。如果该属性不可用，则它会退化到 [`Field.getType()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#getType--) ，而这不会因为泛型的引入而改变。对于某些*Foo*值，使用名称 `getGeneric*Foo*` 反射的其他方法也是类似地实现的。

#### 获取并解析字段修饰符

一些修饰符可以作为字段声明的一部分出现：

- 访问修饰符： `public` ， `protected` ， 以及 `private`
- 控制运行时行为的特定于字段的修饰符： `transient` 和 `volatile`
- 限制为单实例的修饰符： `static`
- 禁止值修改的修饰符： `final`
- 注解

方法 [`Field.getModifiers()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#getModifiers--) 可以被用来返回字段声明中的修饰符的集合的整数表示。该整数中表示修饰符的数据位定义在 [`java.lang.reflect.Modifier`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Modifier.html) 中。

 [`FieldModifierSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/FieldModifierSpy.java) 示例展示了如何搜索使用给定修饰符的字段。它还能通过调用 [`Field.isSynthetic()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isSynthetic--) 来确定所定位的字段是否是合成的(编译器生成的)，通过调用[`Field.isEnumCostant()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isEnumConstant--) 确定字段是否是一个枚举常量。

```java
import java.lang.reflect.Field;
import java.lang.reflect.Modifier;
import static java.lang.System.out;

enum Spy { BLACK , WHITE }

public class FieldModifierSpy {
    volatile int share;
    int instance;
    class Inner {}

    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    int searchMods = 0x0;
	    for (int i = 1; i < args.length; i++) {
		searchMods |= modifierFromString(args[i]);
	    }

	    Field[] flds = c.getDeclaredFields();
	    out.format("Fields in Class '%s' containing modifiers:  %s%n",
		       c.getName(),
		       Modifier.toString(searchMods));
	    boolean found = false;
	    for (Field f : flds) {
		int foundMods = f.getModifiers();
		// Require all of the requested modifiers to be present
		if ((foundMods & searchMods) == searchMods) {
		    out.format("%-8s [ synthetic=%-5b enum_constant=%-5b ]%n",
			       f.getName(), f.isSynthetic(),
			       f.isEnumConstant());
		    found = true;
		}
	    }

	    if (!found) {
		out.format("No matching fields%n");
	    }

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }

    private static int modifierFromString(String s) {
	int m = 0x0;
	if ("public".equals(s))           m |= Modifier.PUBLIC;
	else if ("protected".equals(s))   m |= Modifier.PROTECTED;
	else if ("private".equals(s))     m |= Modifier.PRIVATE;
	else if ("static".equals(s))      m |= Modifier.STATIC;
	else if ("final".equals(s))       m |= Modifier.FINAL;
	else if ("transient".equals(s))   m |= Modifier.TRANSIENT;
	else if ("volatile".equals(s))    m |= Modifier.VOLATILE;
	return m;
    }
}
```

上面的例子输出如下：

$ *java FieldModifierSpy FieldModifierSpy volatile*

```
Fields in Class 'FieldModifierSpy' containing modifiers:  volatile
share    [ synthetic=false enum_constant=false ]
```

$ *java FieldModifierSpy Spy public*

```
Fields in Class 'Spy' containing modifiers:  public
BLACK    [ synthetic=false enum_constant=true  ]
WHITE    [ synthetic=false enum_constant=true  ]
```

$ *java FieldModifierSpy FieldModifierSpy\$Inner final*

```
Fields in Class 'FieldModifierSpy$Inner' containing modifiers:  final
this$0   [ synthetic=true  enum_constant=false ]
```

$ *java FieldModifierSpy Spy private static final*

```
Fields in Class 'Spy' containing modifiers:  private static final
$VALUES  [ synthetic=true  enum_constant=false ]
```

注意，某些字段没有在原始代码中声明，同样也被输出了出来。这是因为编译器将产生一些*合成字段*，这些字段在运行时会使用到。为了检测一个字段是否是合成字段，例子中调用了 [`Field.isSynthetic()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isSynthetic--) 。合成字段集合时编译器依赖的：但是常用的字段包括内部使用的`this$0`（比如作为非静态成员类的嵌套类），用于引用最外层的封闭类，枚举使用的`$VALUES`来实现隐式定义的静态方法`values()`。合成类成员的名称是未指定的，并且在不同编译器实现或发行版中可能不相同。这些和其他合成字段将包含在 [`Class.getDeclaredFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredFields--) 返回的数组中，但不是由 [`Class.getField()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getField-java.lang.String-) 标识的，因为合成成员通常不是`public`的。

因为 [`Field`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html) 实现了接口 [`java.lang.reflect.AnnotatedElement`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AnnotatedElement.html) ，它就可能使用 [`java.lang.annotation.RetentionPolicy.RUNTIME`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html#RUNTIME) 检索任何运行时注解。获取注解的例子在章节 [Examining Class Modifiers and Types](https://docs.oracle.com/javase/tutorial/reflect/class/classModifiers.html) 中。

#### 获取和设定字段值

给定一个类的实例，可以使用反射来设置该类中的字段值。这通常仅在特殊情况下才能使用，比如当不可能以通常方式设置值时。由于此类访问通常违反了该类的设计意图，因此应谨慎使用。

[`Book`](https://docs.oracle.com/javase/tutorial/reflect/member/example/Book.java) 类说明了如何设置`long`，`array`和`enum`类型字段的值。获取和设置其他基本数据类型的方法在[`Field`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#method_summary) 中描述。

```java
import java.lang.reflect.Field;
import java.util.Arrays;
import static java.lang.System.out;

enum Tweedle { DEE, DUM }

public class Book {
    public long chapters = 0;
    public String[] characters = { "Alice", "White Rabbit" };
    public Tweedle twin = Tweedle.DEE;

    public static void main(String... args) {
	Book book = new Book();
	String fmt = "%6S:  %-12s = %s%n";

	try {
	    Class<?> c = book.getClass();

	    Field chap = c.getDeclaredField("chapters");
	    out.format(fmt, "before", "chapters", book.chapters);
  	    chap.setLong(book, 12);
	    out.format(fmt, "after", "chapters", chap.getLong(book));

	    Field chars = c.getDeclaredField("characters");
	    out.format(fmt, "before", "characters",
		       Arrays.asList(book.characters));
	    String[] newChars = { "Queen", "King" };
	    chars.set(book, newChars);
	    out.format(fmt, "after", "characters",
		       Arrays.asList(book.characters));

	    Field t = c.getDeclaredField("twin");
	    out.format(fmt, "before", "twin", book.twin);
	    t.set(book, Tweedle.DUM);
	    out.format(fmt, "after", "twin", t.get(book));

        // production code should handle these exceptions more gracefully
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

输出如下：

$ *java Book*

```
BEFORE:  chapters     = 0
 AFTER:  chapters     = 12
BEFORE:  characters   = [Alice, White Rabbit]
 AFTER:  characters   = [Queen, King]
BEFORE:  twin         = DEE
 AFTER:  twin         = DUM
```

------

注意：

通过反射设置字段值会产生一定的性能开销，因为必须进行很多额外操作，例如验证访问权限。从运行时的角度来看，效果是相同的，并且操作是原子的，就像在类代码中直接更改了值一样。

使用反射可能会导致某些运行时优化丢失。例如，以下代码很可能由Java虚拟机优化：

```java
int x = 1;
x = 2;
x = 3;
```

使用 `Field.set*()` 的等效代码就可能不会被虚拟机优化。

------

#### 故障排除

这里介绍几种开发者通常可能会碰到的问题，同时解释它们发生的原因以及解决方法。

**不可转化类型导致的 IllegalArgumentException**

 [`FieldTrouble`](https://docs.oracle.com/javase/tutorial/reflect/member/example/FieldTrouble.java) 示例将产生 [`IllegalArgumentException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html). [`Field.setInt()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#setInt-java.lang.Object-int-) 被调用来将一个引用类型`Integer`字段的值设置为一个基本数据类型的值。在非反射等价形式`Integer val = 42`中，编译器将原始类型`42`转换（或*装箱*）为引用类型为`new Integer（42）`，以便其类型检查接受该语句。使用反射时，类型检查仅在运行时进行，因此没有机会对值进行装箱。

```java
import java.lang.reflect.Field;

public class FieldTrouble {
    public Integer val;

    public static void main(String... args) {
	FieldTrouble ft = new FieldTrouble();
	try {
	    Class<?> c = ft.getClass();
	    Field f = c.getDeclaredField("val");
  	    f.setInt(ft, 42);               // IllegalArgumentException

        // production code should handle these exceptions more gracefully
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
 	} catch (IllegalAccessException x) {
 	    x.printStackTrace();
	}
    }
}
```

$ *java FieldTrouble*

```
Exception in thread "main" java.lang.IllegalArgumentException: Can not set
  java.lang.Object field FieldTrouble.val to (long)42
        at sun.reflect.UnsafeFieldAccessorImpl.throwSetIllegalArgumentException
          (UnsafeFieldAccessorImpl.java:146)
        at sun.reflect.UnsafeFieldAccessorImpl.throwSetIllegalArgumentException
          (UnsafeFieldAccessorImpl.java:174)
        at sun.reflect.UnsafeObjectFieldAccessorImpl.setLong
          (UnsafeObjectFieldAccessorImpl.java:102)
        at java.lang.reflect.Field.setLong(Field.java:831)
        at FieldTrouble.main(FieldTrouble.java:11)
```

为了消除此异常，应该使用 [`Field.set(Object obj, Object value)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#set-java.lang.Object-java.lang.Object-) 方法调用替换有问题的代码：

```java
f.set(ft, new Integer(43));
```

------

**提示：**当使用反射来设置或者获取字段时，编译器没有机会执行自动装箱。它只能转化那些[`Class.isAssignableFrom()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isAssignableFrom-java.lang.Class-) 规范中描述的有关数据类型。此示例应该会失败，因为在这种编程方式验证一个特定的转化是否可行的测试中  `isAssignableFrom()`  将会返回`false`：

```java
Integer.class.isAssignableFrom(int.class) == false
```

类似的，从基本数据类型到引用类型的自动转化在反射中也是不可能的。

```java
int.class.isAssignableFrom(Integer.class) == false
```

------

**非`public`字段导致的 NoSuchFieldException**

精明的读者可能会注意到，如果前面显示的 [`FieldSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/FieldSpy.java) 示例用于获取非`public`字段，它将失败：

$ *java FieldSpy java.lang.String count*

```
java.lang.NoSuchFieldException: count
        at java.lang.Class.getField(Class.java:1519)
        at FieldSpy.main(FieldSpy.java:12)
```

------

**提示：** [`Class.getField()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getField-java.lang.String  - )和[`Class.getFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getFields--)方法返回由`Class`对象表示的类，枚举或接口的*public*成员字段。要检索`Class`中声明（但不是继承）的所有字段，请使用[`Class.getDeclaredFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredFields--) 方法。

------

**修改`final`字段时发生 IllegalAccessException**

如果尝试获取或设置`private`或其他不可访问的字段或设置`final`字段的值（不管其访问修饰符是啥）的值，则可能抛出 [`IllegalAccessException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalAccessException.html) 。

[`FieldTroubleToo`](https://docs.oracle.com/javase/tutorial/reflect/member/example/FieldTroubleToo.java) 示例说明了尝试设置`final`字段时产生的堆栈跟踪信息。

```java
import java.lang.reflect.Field;

public class FieldTroubleToo {
    public final boolean b = true;

    public static void main(String... args) {
	FieldTroubleToo ft = new FieldTroubleToo();
	try {
	    Class<?> c = ft.getClass();
	    Field f = c.getDeclaredField("b");
// 	    f.setAccessible(true);  // solution
	    f.setBoolean(ft, Boolean.FALSE);   // IllegalAccessException

        // production code should handle these exceptions more gracefully
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	} catch (IllegalArgumentException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java FieldTroubleToo*

```
java.lang.IllegalAccessException: Can not set final boolean field
  FieldTroubleToo.b to (boolean)false
        at sun.reflect.UnsafeFieldAccessorImpl.
          throwFinalFieldIllegalAccessException(UnsafeFieldAccessorImpl.java:55)
        at sun.reflect.UnsafeFieldAccessorImpl.
          throwFinalFieldIllegalAccessException(UnsafeFieldAccessorImpl.java:63)
        at sun.reflect.UnsafeQualifiedBooleanFieldAccessorImpl.setBoolean
          (UnsafeQualifiedBooleanFieldAccessorImpl.java:78)
        at java.lang.reflect.Field.setBoolean(Field.java:686)
        at FieldTroubleToo.main(FieldTroubleToo.java:12)
```

------

**提示：**存在一个访问限制，它阻止在初始化类之后设置`final`字段。但是，被声明为扩展了[`AccessibleObject`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html)的`Field`，提供了抑制此校验功能的能力。

如果 [`AccessibleObject.setAccessible()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html#setAccessible-boolean-) 成功，则后续操作 此字段值不会因为此问题而失败。这可能会产生意想不到的副作用：例如，有时原始值将继续被应用程序的某些部分使用，即使该值已被修改。[`AccessibleObject.setAccessible()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html#setAccessible-boolean-) 只有在安全上下文允许该操作时才会成功。

------

### 方法

*方法*包含可以调用的可执行代码。方法被继承、以及在非反射代码行为中的诸如重载，重写和隐藏都由编译器强制执行。相反，反射代码使得方法选择可以被限制在特定的类而不考虑其超类。可以访问超类方法，但可以确定它们的声明类：如果没有反射，这是不可能以编程方式实现的，并且是许多微妙错误的根源。

[`java.lang.reflect.Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html) 类提供了访问方法修饰符、返回类型、参数、注解以及抛出异常等相关信息的 API。它还可以被用于调用方法。下面章节包含这些主题：

- [获取方法类型信息](https://docs.oracle.com/javase/tutorial/reflect/member/methodType.html) 展示如何列出一个类中声明的方法并获取方法类型信息
- [获取方法参数名称](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html) 展示如何获取方法或者构造器方法参数的名称以及其他信息
- [获取并解析方法修饰符](https://docs.oracle.com/javase/tutorial/reflect/member/methodModifiers.html) 描述如何访问并解析与方法有关的修饰符以及其他信息
- [调用方法](https://docs.oracle.com/javase/tutorial/reflect/member/methodInvocation.html) 展示如何执行方法并获取其返回值
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/member/methodTrouble.html) 涵盖查找或者调用方法时可能发生的错误

#### 获取方法类型信息

方法声明包含方法名称、修饰符、参数、返回类型、以及抛出的异常列表。 [`java.lang.reflect.Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html) 类提供了获取这些信息的方法。

 [`MethodSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodSpy.java) 示例展示了如何列出给定的类中所有声明的方法。同时获取所有给定名称的方法的返回类型、参数以及异常类型。

```java
import java.lang.reflect.Method;
import java.lang.reflect.Type;
import static java.lang.System.out;

public class MethodSpy {
    private static final String  fmt = "%24s: %s%n";

    // for the morbidly curious
    <E extends RuntimeException> void genericThrow() throws E {}

    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    Method[] allMethods = c.getDeclaredMethods();
	    for (Method m : allMethods) {
		if (!m.getName().equals(args[1])) {
		    continue;
		}
		out.format("%s%n", m.toGenericString());

		out.format(fmt, "ReturnType", m.getReturnType());
		out.format(fmt, "GenericReturnType", m.getGenericReturnType());

		Class<?>[] pType  = m.getParameterTypes();
		Type[] gpType = m.getGenericParameterTypes();
		for (int i = 0; i < pType.length; i++) {
		    out.format(fmt,"ParameterType", pType[i]);
		    out.format(fmt,"GenericParameterType", gpType[i]);
		}

		Class<?>[] xType  = m.getExceptionTypes();
		Type[] gxType = m.getGenericExceptionTypes();
		for (int i = 0; i < xType.length; i++) {
		    out.format(fmt,"ExceptionType", xType[i]);
		    out.format(fmt,"GenericExceptionType", gxType[i]);
		}
	    }

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

下面是 [`Class.getConstructor()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getConstructor-java.lang.Class...-) 的输出，它的参数具有参数化类型，而且参数个数可变。

$ *java MethodSpy java.lang.Class getConstructor*

```
public java.lang.reflect.Constructor<T> java.lang.Class.getConstructor
  (java.lang.Class<?>[]) throws java.lang.NoSuchMethodException,
  java.lang.SecurityException
              ReturnType: class java.lang.reflect.Constructor
       GenericReturnType: java.lang.reflect.Constructor<T>
           ParameterType: class [Ljava.lang.Class;
    GenericParameterType: java.lang.Class<?>[]
           ExceptionType: class java.lang.NoSuchMethodException
    GenericExceptionType: class java.lang.NoSuchMethodException
           ExceptionType: class java.lang.SecurityException
    GenericExceptionType: class java.lang.SecurityException
```

下面是源代码中实际的方法声明：

```java
public Constructor<T> getConstructor(Class<?>... parameterTypes)
```

首先，注意其返回类型和参数类型都是泛型。 [`Method.getGenericReturnType()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getGenericReturnType--) 将从类文件中查询签名属性，如果该类文件存在。如果属性不可用，该方法会退化为 [`Method.getReturnType()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getReturnType--) ，此方法在引入泛型前后没有变化。名为`getGeneric*Foo*()`的方法来通过反射获取*Foo*的某些值的实现与此类似。

其次，注意最后一个（仅仅是最后一个）参数，`parameterType` ，是数量可变的`java.lang.Class`类型的参数。通常表现为`java.lang.Class`类型数据的一维数组。这种参数可以通过调用 [`Method.isVarArgs()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#isVarArgs--) 来区别于显式的 `java.lang.Class` 类型数组参数。`Method.get*Types()`方法的返回值语法在 [`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--) 中描述。

下面的例子展示了泛型返回类型方法。

$ *java MethodSpy java.lang.Class cast*

```
public T java.lang.Class.cast(java.lang.Object)
              ReturnType: class java.lang.Object
       GenericReturnType: T
           ParameterType: class java.lang.Object
    GenericParameterType: class java.lang.Object
```

方法 [`Class.cast()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#cast-java.lang.Object-) 的泛型返回类型被报告为 `java.lang.Object`，因为泛型是通过类型擦除实现，类型擦除会在编译期清楚所有的泛型相关的类型信息。`T`的擦除由 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 的声明定义：

```java
public final class Class<T> implements ...
```

因此，`T`被类型变量的上界替换，这种情况下，就是 `java.lang.Object` 。

最后一个示例说明了具有多个重载的方法的输出。

$ *java MethodSpy java.io.PrintStream format*

```
public java.io.PrintStream java.io.PrintStream.format
  (java.util.Locale,java.lang.String,java.lang.Object[])
              ReturnType: class java.io.PrintStream
       GenericReturnType: class java.io.PrintStream
           ParameterType: class java.util.Locale
    GenericParameterType: class java.util.Locale
           ParameterType: class java.lang.String
    GenericParameterType: class java.lang.String
           ParameterType: class [Ljava.lang.Object;
    GenericParameterType: class [Ljava.lang.Object;
public java.io.PrintStream java.io.PrintStream.format
  (java.lang.String,java.lang.Object[])
              ReturnType: class java.io.PrintStream
       GenericReturnType: class java.io.PrintStream
           ParameterType: class java.lang.String
    GenericParameterType: class java.lang.String
           ParameterType: class [Ljava.lang.Object;
    GenericParameterType: class [Ljava.lang.Object;
```

如果发现同一个方法的多个重载，它们都会被 [`Class.getDeclaredMethods()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredMethods--) 返回。由于 `format()` 有两个重载（携带 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 的和不携带的），都会被 `MethodSpy` 展示。

------

**注意：** [`Method.getGenericExceptionTypes()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getGenericExceptionTypes--) 存在，因为声明抛出泛型异常类型的方法是可能的。不过这种情况很罕见，因为我们不可能捕获泛型异常类型。

------

#### 获取方法参数名称

通过方法 [`java.lang.reflect.Executable.getParameters`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Executable.html#getParameters--) 你可以获取任何方法或者构造器的形式参数名称。（ [`Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html) 和 [`Constructor`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Executable.html) 类扩展了 [`Executable`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Executable.html) 类，因而继承了方法`Executable.getParameters` 。）然而，默认情况下`.class`文件并没有保存形式参数名称。这是因为许多生成和使用类文件的工具都不希望较大的`.class`文件尺寸来包含形式参数名称。特别地，如果这些工具必须处理更大的`.class`文件，则 Java 虚拟机将使用更多的内存。另外，某些参数名称，比如`secret`或者`password`，可能会暴露安全敏感方法的信息。

为了将形式参数名称保存到特定`.class`文件中，使得反射 API 可以获取形式参数名称，使用携带`-paramdters`参数的`javac`编译器命令编译该源代码文件。

 [`MethodParameterSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodParameterSpy.java) 示例展示了如何获取给定类的所有方法和构造器的形式参数名称。该示例同时打印出有关每个参数的其它信息。

下面的命令打印 [`ExampleMethods`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ExampleMethods.java) 类中方法和构造器参数的形式参数名称。

**注意：** 记住使用`-parameters`编译器参数来编译示例`ExampleMethods` 。

```
java MethodParameterSpy ExampleMethods
```

该命令输出如下内容：

```
Number of constructors: 1

Constructor #1
public ExampleMethods()

Number of declared constructors: 1

Declared constructor #1
public ExampleMethods()

Number of methods: 4

Method #1
public boolean ExampleMethods.simpleMethod(java.lang.String,int)
             Return type: boolean
     Generic return type: boolean
         Parameter class: class java.lang.String
          Parameter name: stringParam
               Modifiers: 0
            Is implicit?: false
        Is name present?: true
           Is synthetic?: false
         Parameter class: int
          Parameter name: intParam
               Modifiers: 0
            Is implicit?: false
        Is name present?: true
           Is synthetic?: false

Method #2
public int ExampleMethods.varArgsMethod(java.lang.String...)
             Return type: int
     Generic return type: int
         Parameter class: class [Ljava.lang.String;
          Parameter name: manyStrings
               Modifiers: 0
            Is implicit?: false
        Is name present?: true
           Is synthetic?: false

Method #3
public boolean ExampleMethods.methodWithList(java.util.List<java.lang.String>)
             Return type: boolean
     Generic return type: boolean
         Parameter class: interface java.util.List
          Parameter name: listParam
               Modifiers: 0
            Is implicit?: false
        Is name present?: true
           Is synthetic?: false

Method #4
public <T> void ExampleMethods.genericMethod(T[],java.util.Collection<T>)
             Return type: void
     Generic return type: void
         Parameter class: class [Ljava.lang.Object;
          Parameter name: a
               Modifiers: 0
            Is implicit?: false
        Is name present?: true
           Is synthetic?: false
         Parameter class: interface java.util.Collection
          Parameter name: c
               Modifiers: 0
            Is implicit?: false
        Is name present?: true
           Is synthetic?: false
```

 `MethodParameterSpy` 示例使用下面的方法，这些方法来自 [`Parameter`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html) 类：

- [`getType`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html#getType--): 返回一个 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 对象来标识参数的声明类型。

- [`getName`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html#getName--): 返回参数的名称。如果参数名称存在，则本方法返回由`.class`文件提供的名称。否则，本方法合成一个`arg*N*`形式的参数名称，其中的`*N*`是该参数在方法声明中的索引下标。

  比如，假定你编译 `ExampleMethods` 而没有指定 `-parameters` 编译器参数。示例 `MethodParameterSpy` 将为 `ExampleMethods.simpleMethod` 方法打印下面的内容：

  ```
  public boolean ExampleMethods.simpleMethod(java.lang.String,int)
               Return type: boolean
       Generic return type: boolean
           Parameter class: class java.lang.String
            Parameter name: arg0
                 Modifiers: 0
              Is implicit?: false
          Is name present?: false
             Is synthetic?: false
           Parameter class: int
            Parameter name: arg1
                 Modifiers: 0
              Is implicit?: false
          Is name present?: false
             Is synthetic?: false
  ```

- [`getModifiers`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html#getModifiers--) : 返回表示形式参数拥有的各种特性的一个整数。该值是以下各个值之和，如果适用于形式参数。

  | Value (in decimal) | Value (in hexadecimal | Description                         |
  | ------------------ | --------------------- | ----------------------------------- |
  | 16                 | 0x0010                | 形式参数声明为 `final`                     |
  | 4096               | 0x1000                | 形式参数是合成的。另外，你可以调用方法 `isSynthetic`   |
  | 32768              | 0x8000                | 参数在源代码中隐式声明。另外，你可以调用方法 `isImplicit` |

- [`isImplicit`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html#isImplicit--): 如果参数在源代码中隐式声明，则返回`true`。参考 [Implicit and Synthetic Parameters](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html#implcit_and_synthetic) 获取更多信息。

- [`isNamePresent`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html#isNamePresent--): 如果按照`.class`文件中有参数名称则返回`true`。

- [`isSynthetic`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html#isSynthetic--): 如果参数在源代码中既没有隐式声明也没有显式声明，则返回`true`。参考 [Implicit and Synthetic Parameters](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html#implcit_and_synthetic) 获取更多信息。

**[隐式和合成参数]()**

某些构造器是在源代码中隐式声明的，如果它们没有显式写出来。比如， [`ExampleMethods`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ExampleMethods.java) 示例并不包含一个构造器。一个默认构造器将隐式声明。 `MethodParameterSpy` 示例打印有关为`ExampleMethods`隐式声明的构造器的信息：

```
Number of declared constructors: 1
public ExampleMethods()
```

考虑下面来自 [`MethodParameterExamples`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodParameterExamples.java) 的片段：

```java
public class MethodParameterExamples {
    public class InnerClass { }
}
```

`InnerClass`类是一个非静态 [nested class](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html) 或内部类。内部类的构造函数也是隐式声明的。但是，此构造函数将包含一个参数。当Java编译器编译`InnerClass`时，它会创建一个`.class`文件，该文件代表示似于以下内容的代码：

```java
public class MethodParameterExamples {
    public class InnerClass {
        final MethodParameterExamples parent;
        InnerClass(final MethodParameterExamples this$0) {
            parent = this$0; 
        }
    }
}
```

`InnerClass`构造器包含一个参数，该参数类型是包含`InnerClass`的类，也就是`MethodParameterExamples`。接下来，示例`MethodParameterExamples` 打印如下内容：

```
public MethodParameterExamples$InnerClass(MethodParameterExamples)
         Parameter class: class MethodParameterExamples
          Parameter name: this$0
               Modifiers: 32784
            Is implicit?: true
        Is name present?: true
           Is synthetic?: false
```

由于`InnerClass`的构造器是隐式声明的，它的参数也就是隐式的。

**注意**:

- Java 编译器为内部类的构造器创建形式参数以允许编译器传递一个来自创建表达式的引用（表示该内部类所在的直接外部类实例）给成员类的构造器。
- 值 32784 意味着`InnerClass`构造器的参数同时是`final`（16）和隐式（32768）的。
- Java 编程语言本身允许在变量名称中使用美元符号`$`，不过，按照惯例，我们并不会这么做。

如果Java编译器生成的构造与源代码中显式或隐式声明的构造不对应，则将其标记为合成构造，除非它们是类初始化方法。合成构造是由编译器生成的组件，这些组件在不同的实现中有所不同。请考虑以下摘自 [`MethodParameterExamples`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodParameterExamples.java) 的片段：

```java
public class MethodParameterExamples {
    enum Colors {
        RED, WHITE;
    }
}
```

当Java编译器遇到`enum`构造时，它会创建几个与`.class`文件结构兼容的方法，并提供`enum`构造的预期功能。例如，Java编译器将为`enum`构造`Colors`创建一个`.class`文件。代表类似于以下内容的代码：

```java
final class Colors extends java.lang.Enum<Colors> {
    public final static Colors RED = new Colors("RED", 0);
    public final static Colors BLUE = new Colors("WHITE", 1);
 
    private final static values = new Colors[]{ RED, BLUE };
 
    private Colors(String name, int ordinal) {
        super(name, ordinal);
    }
 
    public static Colors[] values(){
        return values;
    }
 
    public static Colors valueOf(String name){
        return (Colors)java.lang.Enum.valueOf(Colors.class, name);
    }
}
```

Java编译器为此 `enum` 构造创建三个构造函数和方法：`Colors(String name, int ordinal)`, `Colors[] values()`, and `Colors valueOf(String name)`。 `values` 和 `valueOf` 是隐式声明的。因此，它们的形式参数名也被隐式声明。

 `enum` 构造函数 `Colors(String name, int ordinal)` 是默认构造函数，它是隐式声明的。但是，此隐式声明构造函数的形式参数（`name`和`ordinal`）并不是隐式声明的。由于这些形式参数既未明确声明也未隐式声明，因此它们是合成的。（`enum`构造的默认构造函数的形式参数不是隐式声明的，因为不同的编译器不需要在这个构造函数的形式上达成一致；另一个Java编译器可能为它指定不同的形式参数。当编译器编译使用枚举常量的表达式时，它们仅依赖于枚举构造的公共静态字段，这些字段是隐式声明的，而不是它们的构造函数或这些常量的初始化方式。）

因此，示例`MethodParameterExample`打印有关`enum`构造`Colors`的以下内容：

```
enum Colors:

Number of constructors: 0

Number of declared constructors: 1

Declared constructor #1
private MethodParameterExamples$Colors()
         Parameter class: class java.lang.String
          Parameter name: $enum$name
               Modifiers: 4096
            Is implicit?: false
        Is name present?: true
           Is synthetic?: true
         Parameter class: int
          Parameter name: $enum$ordinal
               Modifiers: 4096
            Is implicit?: false
        Is name present?: true
           Is synthetic?: true

Number of methods: 2

Method #1
public static MethodParameterExamples$Colors[]
    MethodParameterExamples$Colors.values()
             Return type: class [LMethodParameterExamples$Colors;
     Generic return type: class [LMethodParameterExamples$Colors;

Method #2
public static MethodParameterExamples$Colors
    MethodParameterExamples$Colors.valueOf(java.lang.String)
             Return type: class MethodParameterExamples$Colors
     Generic return type: class MethodParameterExamples$Colors
         Parameter class: class java.lang.String
          Parameter name: name
               Modifiers: 32768
            Is implicit?: true
        Is name present?: true
           Is synthetic?: false
```

有关隐式声明的构造的更多信息，请参阅 [Java Language Specification](https://docs.oracle.com/javase/specs/) ，包括在Reflection API中显示为隐式的参数。

#### 获取并解析方法修饰符

可以作为方法声明一部分的修饰符有下面这几种：

- 访问修饰符 `public`, `protected`, 和 `private`
- 限定为一个实例的修饰符 `static`
- 禁止值修改修饰符 `final`
- 需要重载修饰符 `abstract`
- 阻止重入修饰符 `synchronized`
- 表示以别的编程语言实现的修饰符 `native`
- 强制限制静态浮点数行为修饰符 `strictfp`
- 注解

 [`MethodModifierSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodModifierSpy.java) 示例列出了给定名称方法的所有修饰符。它同时显示该方法是否是合成的（由编译器生成的），是否是可变参数的，或者是否是一个桥接方法（由编译器生成以支持泛型接口）。

```java
import java.lang.reflect.Method;
import java.lang.reflect.Modifier;
import static java.lang.System.out;

public class MethodModifierSpy {

    private static int count;
    private static synchronized void inc() { count++; }
    private static synchronized int cnt() { return count; }

    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    Method[] allMethods = c.getDeclaredMethods();
	    for (Method m : allMethods) {
		if (!m.getName().equals(args[1])) {
		    continue;
		}
		out.format("%s%n", m.toGenericString());
		out.format("  Modifiers:  %s%n",
			   Modifier.toString(m.getModifiers()));
		out.format("  [ synthetic=%-5b var_args=%-5b bridge=%-5b ]%n",
			   m.isSynthetic(), m.isVarArgs(), m.isBridge());
		inc();
	    }
	    out.format("%d matching overload%s found%n", cnt(),
		       (cnt() == 1 ? "" : "s"));

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

上面的例子产生的部分输出如下：

$ *java MethodModifierSpy java.lang.Object wait*

```
public final void java.lang.Object.wait() throws java.lang.InterruptedException
  Modifiers:  public final
  [ synthetic=false var_args=false bridge=false ]
public final void java.lang.Object.wait(long,int)
  throws java.lang.InterruptedException
  Modifiers:  public final
  [ synthetic=false var_args=false bridge=false ]
public final native void java.lang.Object.wait(long)
  throws java.lang.InterruptedException
  Modifiers:  public final native
  [ synthetic=false var_args=false bridge=false ]
3 matching overloads found
```

$ *java MethodModifierSpy java.lang.StrictMath toRadians*

```
public static double java.lang.StrictMath.toRadians(double)
  Modifiers:  public static strictfp
  [ synthetic=false var_args=false bridge=false ]
1 matching overload found
```

$ *java MethodModifierSpy MethodModifierSpy inc*

```
private synchronized void MethodModifierSpy.inc()
  Modifiers: private synchronized
  [ synthetic=false var_args=false bridge=false ]
1 matching overload found
```

$ *java MethodModifierSpy java.lang.Class getConstructor*

```
public java.lang.reflect.Constructor<T> java.lang.Class.getConstructor
  (java.lang.Class<T>[]) throws java.lang.NoSuchMethodException,
  java.lang.SecurityException
  Modifiers: public transient
  [ synthetic=false var_args=true bridge=false ]
1 matching overload found
```

$ *java MethodModifierSpy java.lang.String compareTo*

```
public int java.lang.String.compareTo(java.lang.String)
  Modifiers: public
  [ synthetic=false var_args=false bridge=false ]
public int java.lang.String.compareTo(java.lang.Object)
  Modifiers: public volatile
  [ synthetic=true  var_args=false bridge=true  ]
2 matching overloads found
```

注意 [`Method.isVarArgs()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#isVarArgs--) 为 [`Class.getConstructor()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getConstructor-java.lang.Class...-) 返回`true`。这表示该方法声明如下：

```java
public Constructor<T> getConstructor(Class<?>... parameterTypes)
```

而不是：

```java
public Constructor<T> getConstructor(Class<?> [] parameterTypes)
```

注意关于 [`String.compareTo()`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#compareTo-java.lang.String-) 的输出包含两个方法。该方法在`String.java`中的声明：

```java
public int compareTo(String anotherString);
```

以及一个合成的或者编译器生成的桥接方法。这是因为 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 实现了参数化接口 [`Comparable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html) 。在参数擦除过程中，继承的方法 [`Comparable.compareTo()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html#compareTo-T-) 的参数类型从`java.lang.Object`变成`java.lang.String`。由于`Comparable`中的`compareTo`方法的参数类型不再符合类型擦除后的`String` ，就不能发生重载了。在所有其它环境下，这将导致一个编译期错误，因为该接口并未被实现。桥接方法的引入避免了此问题。

[`Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html) 实现了 [`java.lang.reflect.AnnotatedElement`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AnnotatedElement.html) 。因此任何使用 [`java.lang.annotation.RetentionPolicy.RUNTIME`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html#RUNTIME) 的运行时注解都能被检索到。检索注解的例子参考 [Examining Class Modifiers and Types](https://docs.oracle.com/javase/tutorial/reflect/class/classModifiers.html) 。

#### 调用方法

反射提供了一种在类上调用方法的方法。通常，只有在无法在非反射代码中将类的实例强制转换为所需类型时才需要这样做。使用 [`java.lang.reflect.Method.invoke()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-) 调用方法。第一个参数是要在其上调用此特定方法的对象实例。（如果方法是`static`的，则第一个参数应为`null`。）后续参数是方法的参数。如果底层方法抛出异常，它将被 [`java.lang.reflect.InvocationTargetException`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html) 包装。可以使用异常链接机制的 [`InvocationTargetException.getCause()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html#getCause--) 方法检索方法的原始异常。

**查找并调用特定声明的方法**

考虑一个测试套件，它使用反射来调用给定类中的`private`方法。 [`Deet`](https://docs.oracle.com/javase/tutorial/reflect/member/example/Deet.java) 示例在一个类中搜索方法名以`test`开头、拥有一个布尔值返回值、以及单独一个 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 参数的`public`方法，然后调用每个匹配到的方法：

```java
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.lang.reflect.Type;
import java.util.Locale;
import static java.lang.System.out;
import static java.lang.System.err;

public class Deet<T> {
    private boolean testDeet(Locale l) {
	// getISO3Language() may throw a MissingResourceException
	out.format("Locale = %s, ISO Language Code = %s%n", l.getDisplayName(), l.getISO3Language());
	return true;
    }

    private int testFoo(Locale l) { return 0; }
    private boolean testBar() { return true; }

    public static void main(String... args) {
	if (args.length != 4) {
	    err.format("Usage: java Deet <classname> <langauge> <country> <variant>%n");
	    return;
	}

	try {
	    Class<?> c = Class.forName(args[0]);
	    Object t = c.newInstance();

	    Method[] allMethods = c.getDeclaredMethods();
	    for (Method m : allMethods) {
		String mname = m.getName();
		if (!mname.startsWith("test")
		    || (m.getGenericReturnType() != boolean.class)) {
		    continue;
		}
 		Type[] pType = m.getGenericParameterTypes();
 		if ((pType.length != 1)
		    || Locale.class.isAssignableFrom(pType[0].getClass())) {
 		    continue;
 		}

		out.format("invoking %s()%n", mname);
		try {
		    m.setAccessible(true);
		    Object o = m.invoke(t, new Locale(args[1], args[2], args[3]));
		    out.format("%s() returned %b%n", mname, (Boolean) o);

		// Handle any exceptions thrown by method to be invoked.
		} catch (InvocationTargetException x) {
		    Throwable cause = x.getCause();
		    err.format("invocation of %s failed: %s%n",
			       mname, cause.getMessage());
		}
	    }

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

`Deet`调用 [`getDeclaredMethods()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredMethods--) ，该方法将返回类中显式声明的所有方法。同时，[`Class.isAssignableFrom()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isAssignableFrom-java.lang.Class-) 被用于确定这些方法的参数是否能够匹配到方法调用。技术上来说该代码应该可以测试以下语句是否为`true`，因为 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 是`final`的：

```java
Locale.class == pType[0].getClass()
```

不过， [`Class.isAssignableFrom()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isAssignableFrom-java.lang.Class-) 更加通用。

$ *java Deet Deet ja JP JP*

```
invoking testDeet()
Locale = Japanese (Japan,JP), 
ISO Language Code = jpn
testDeet() returned true
```

$ *java Deet Deet xx XX XX*

```
invoking testDeet()
invocation of testDeet failed: 
Couldn't find 3-letter language code for xx
```

首先，请注意只有 `testDeet()` 符合代码强制执行的声明限制。其次，当向 `testDeet()` 传递一个无效参数时，它会抛出一个不受检查的 [`java.util.MissingResourceException`](https://docs.oracle.com/javase/8/docs/api/java/util/MissingResourceException.html) 。反射过程中，在处理已检查和未检查的异常方面没有区别。它们都包含在 [`InvocationTargetException`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html) 中。

**调用可变参数方法**

[`Method.invoke()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-) 可用于将可变数量的参数传递给方法。要理解的关键概念是实现变量数量可变的方法，就好像变量参数被打包在一个数组中一样。

 [`InvokeMain`](https://docs.oracle.com/javase/tutorial/reflect/member/example/InvokeMain.java) 示例说明了如何在任何类中调用 `main()` 入口点并传递在运行时确定的一组参数。

```java
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;
import java.util.Arrays;

public class InvokeMain {
    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    Class[] argTypes = new Class[] { String[].class };
	    Method main = c.getDeclaredMethod("main", argTypes);
  	    String[] mainArgs = Arrays.copyOfRange(args, 1, args.length);
	    System.out.format("invoking %s.main()%n", c.getName());
	    main.invoke(null, (Object)mainArgs);

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	}
    }
}
```

首先，为了找到 `main()` 方法，代码搜索名为`main`的方法，参数是一个`String`数组，因为`main()`是静态的，`null`是`Method.invoke()`的第一个参数。第二个参数是要传递的参数数组。

$ *java InvokeMain Deet Deet ja JP JP*

```
invoking Deet.main()
invoking testDeet()
Locale = Japanese (Japan,JP), 
ISO Language Code = jpn
testDeet() returned true
```

#### 故障排除

本节包含开发人员在使用反射来查找，调用或获取有关方法的信息时可能遇到的问题的示例。

**类型擦除导致的 NoSuchMethodException**

 [`MethodTrouble`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodTrouble.java) 示例展示了当在一个类中搜索特定方法的代码没有考虑类型擦除时将会发生什么：

```java
import java.lang.reflect.Method;

public class MethodTrouble<T>  {
    public void lookup(T t) {}
    public void find(Integer i) {}

    public static void main(String... args) {
	try {
	    String mName = args[0];
	    Class cArg = Class.forName(args[1]);
	    Class<?> c = (new MethodTrouble<Integer>()).getClass();
	    Method m = c.getMethod(mName, cArg);
	    System.out.format("Found:%n  %s%n", m.toGenericString());

        // production code should handle these exceptions more gracefully
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java MethodTrouble lookup java.lang.Integer*

```java
java.lang.NoSuchMethodException: MethodTrouble.lookup(java.lang.Integer)
        at java.lang.Class.getMethod(Class.java:1605)
        at MethodTrouble.main(MethodTrouble.java:12)
```

$ *java MethodTrouble lookup java.lang.Object*

```
Found:
  public void MethodTrouble.lookup(T)
```

当一个方法被声明为使用泛型类型参数，编译器将使用泛型类型的上界替换该泛型类型。示例中的情况下，`T`的上界是`Object`。因此，当代码搜索`lookup(Integer)`时，找不到方法，尽管`MethodTrouble`示例被创建如下：

```java
Class<?> c = (new MethodTrouble<Integer>()).getClass();
```

寻找 `lookup(Object)` 意料之中的成功。

$ *java MethodTrouble find java.lang.Integer*

```
Found:
  public void MethodTrouble.find(java.lang.Integer)
```

$ *java MethodTrouble find java.lang.Object*

```
java.lang.NoSuchMethodException: MethodTrouble.find(java.lang.Object)
        at java.lang.Class.getMethod(Class.java:1605)
        at MethodTrouble.main(MethodTrouble.java:12)
```

这种情况下，`find()`没有泛型参数，因而 [`getMethod()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getMethod-java.lang.String-java.lang.Class...-) 方法搜索的方法的参数类型必须精确匹配。

------

**提示：** 当搜索方法时永远传递参数化类型的类型上界。

------

**调用方法时发生 IllegalAccessException**

试图调用一个`private`或者其它的不可访问方法时将抛出 [`IllegalAccessException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalAccessException.html) 。

 [`MethodTroubleAgain`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodTroubleAgain.java) 示例展示一个典型的调用栈轨迹，它由调用其它类中的一个`private`方法尝试产生。

```java
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

class AnotherClass {
    private void m() {}
}

public class MethodTroubleAgain {
    public static void main(String... args) {
	AnotherClass ac = new AnotherClass();
	try {
	    Class<?> c = ac.getClass();
 	    Method m = c.getDeclaredMethod("m");
//  	    m.setAccessible(true);      // solution
 	    Object o = m.invoke(ac);    // IllegalAccessException

        // production code should handle these exceptions more gracefully
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

异常栈如下：

$ *java MethodTroubleAgain*

```
java.lang.IllegalAccessException: Class MethodTroubleAgain can not access a
  member of class AnotherClass with modifiers "private"
        at sun.reflect.Reflection.ensureMemberAccess(Reflection.java:65)
        at java.lang.reflect.Method.invoke(Method.java:588)
        at MethodTroubleAgain.main(MethodTroubleAgain.java:15)
```

------

**提示：**存在访问限制，阻止反射调用通常无法通过直接调用访问的方法。（这包括---但不限于 - 单独的类中的`private`方法和单独的`private`类中`public`方法。）但是，声明`Method`扩展了`AccessibleObject`，它提供了通过`AccessibleObject.setAccessible()`来抑制此检查的能力。如果成功，则此方法对象的后续调用不会因此问题而失败。

------

**来自 `Method.invoke()` 的 IllegalArgumentException**

[`Method.invoke()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-) has been retrofitted to be a variable-arity method. This is an enormous convenience, however it can lead to unexpected behavior. The [`MethodTroubleToo`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodTroubleToo.java)example shows various ways in which [`Method.invoke()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-) can produce confusing results.

[`Method.invoke()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-) 已被改进为可变参数方法。这是一个巨大的便利，但它可能导致意外的行为。 [`MethodTroubleToo`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodTroubleToo.java) 示例显示了 [`Method.invoke()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-)  可以产生令人困惑的结果的各种方法。

```java
import java.lang.reflect.Method;

public class MethodTroubleToo {
    public void ping() { System.out.format("PONG!%n"); }

    public static void main(String... args) {
	try {
	    MethodTroubleToo mtt = new MethodTroubleToo();
	    Method m = MethodTroubleToo.class.getMethod("ping");

 	    switch(Integer.parseInt(args[0])) {
	    case 0:
  		m.invoke(mtt);                 // works
		break;
	    case 1:
 		m.invoke(mtt, null);           // works (expect compiler warning)
		break;
	    case 2:
		Object arg2 = null;
		m.invoke(mtt, arg2);           // IllegalArgumentException
		break;
	    case 3:
		m.invoke(mtt, new Object[0]);  // works
		break;
	    case 4:
		Object arg4 = new Object[0];
		m.invoke(mtt, arg4);           // IllegalArgumentException
		break;
	    default:
		System.out.format("Test not found%n");
	    }

        // production code should handle these exceptions more gracefully
	} catch (Exception x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java MethodTroubleToo 0*

```
PONG!
```

除了第一个参数， [`Method.invoke()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-) 的所有参数都是可选的，它们可以被忽略，当方法被以无参方式调用时。

$ *java MethodTroubleToo 1*

```
PONG!
```

这种情况下该代码会产生编译器警告，因为`null`是不明确的。

$ *javac MethodTroubleToo.java*

```
MethodTroubleToo.java:16: warning: non-varargs call of varargs method with
  inexact argument type for last parameter;
 		m.invoke(mtt, null);           // works (expect compiler warning)
 		              ^
  cast to Object for a varargs call
  cast to Object[] for a non-varargs call and to suppress this warning
1 warning
```

无法确定`null`是表示空数组参数还是第一个参数是`null`。

$ *java MethodTroubleToo 2*

```
java.lang.IllegalArgumentException: wrong number of arguments
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke
          (NativeMethodAccessorImpl.java:39)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke
          (DelegatingMethodAccessorImpl.java:25)
        at java.lang.reflect.Method.invoke(Method.java:597)
        at MethodTroubleToo.main(MethodTroubleToo.java:21)
```

尽管参数为`null`，但由于类型是`Object`而`ping()`完全不需要参数，因此失败。

$ *java MethodTroubleToo 3*

```
PONG!
```

这是有效的，因为 `new Object[0]` 创建一个空数组，而对于可变参数方法，这相当于不传递任何可选参数。

$ *java MethodTroubleToo 4*

```
java.lang.IllegalArgumentException: wrong number of arguments
        at sun.reflect.NativeMethodAccessorImpl.invoke0
          (Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke
          (NativeMethodAccessorImpl.java:39)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke
          (DelegatingMethodAccessorImpl.java:25)
        at java.lang.reflect.Method.invoke(Method.java:597)
        at MethodTroubleToo.main(MethodTroubleToo.java:28)
```

不同于前面的例子，如果空数组被存储在一个 [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 中，则它会被作为一个 [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 对待。此时失败的原因与第二种情况相同， `ping()` 不期待任何参数。

------

**提示：**当声明方法 `foo(Object... o)` 时，编译器会将传递给`foo()` 的所有参数放入`Object`类型的数组中。`foo()`的实现与声明为`foo(Object[] o)`的实现相同。理解这可能有助于避免上述类型问题。

------

**当调用方法失败时产生的 InvocationTargetException**

 [`InvocationTargetException`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html) 包装调用方法对象时生成的所有异常（已检查和未检查）。 [`MethodTroubleReturns`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodTroubleReturns.java) 示例显示如何检索被调用方法抛出的原始异常。

```java
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class MethodTroubleReturns {
    private void drinkMe(int liters) {
	if (liters < 0)
	    throw new IllegalArgumentException("I can't drink a negative amount of liquid");
    }

    public static void main(String... args) {
	try {
	    MethodTroubleReturns mtr  = new MethodTroubleReturns();
 	    Class<?> c = mtr.getClass();
   	    Method m = c.getDeclaredMethod("drinkMe", int.class);
	    m.invoke(mtr, -1);

        // production code should handle these exceptions more gracefully
	} catch (InvocationTargetException x) {
	    Throwable cause = x.getCause();
	    System.err.format("drinkMe() failed: %s%n", cause.getMessage());
	} catch (Exception x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java MethodTroubleReturns*

```
drinkMe() failed: I can't drink a negative amount of liquid
```

------

**提示：**如果抛出 [`InvocationTargetException`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html) ，则该方法被调用。问题的诊断与直接调用该方法并抛出 [`getCause()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html#getCause--) 检索的异常相同。此异常并不表示反射包或其用法存在问题。

------

### 构造器

构造器被用来创建类的实例对象。它执行的典型操作是需要再方法被调用或者字段被访问之前初始化类实例对象。构造器用于无法被继承。

类似于方法，反射提供了发现和检索类的构造器的 API ，同时可以获取注入修饰符、参数、注解以及抛出异常等声明信息。新的类实例还可以使用一个特定的构造器创建。当使用构造器时涉及到的关键类是 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 和 [`java.lang.reflect.Constructor`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html) 。与构造器相关的一般操作在下面的章节中介绍。

- [查找构造器](https://docs.oracle.com/javase/tutorial/reflect/member/ctorLocation.html) 展示如何获取携带特定参数的构造器
- [检索并解析构造器修饰符](https://docs.oracle.com/javase/tutorial/reflect/member/ctorModifiers.html) 展示如何获取构造器声明修饰符以及有关构造器的其它信息
- [创建新的类实例](https://docs.oracle.com/javase/tutorial/reflect/member/ctorInstance.html) 展示如何实例化一个对象实例，通过调用它的构造器
- [故障修复Troubleshooting](https://docs.oracle.com/javase/tutorial/reflect/member/ctorTrouble.html) 描述在查找或者调用构造器时可能遇到的常见错误

#### 查找构造器

构造器声明包含名称、修饰符、参数以及可抛出的异常列表。[`java.lang.reflect.Constructor`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html) 类提供了获取这些信息的方法。

 [`ConstructorSift`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ConstructorSift.java) 示例展示了如何在一个类中查找声明的携带给定参数类型的构造器。

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.Type;
import static java.lang.System.out;

public class ConstructorSift {
    public static void main(String... args) {
	try {
	    Class<?> cArg = Class.forName(args[1]);

	    Class<?> c = Class.forName(args[0]);
	    Constructor[] allConstructors = c.getDeclaredConstructors();
	    for (Constructor ctor : allConstructors) {
		Class<?>[] pType  = ctor.getParameterTypes();
		for (int i = 0; i < pType.length; i++) {
		    if (pType[i].equals(cArg)) {
			out.format("%s%n", ctor.toGenericString());

			Type[] gpType = ctor.getGenericParameterTypes();
			for (int j = 0; j < gpType.length; j++) {
			    char ch = (pType[j].equals(cArg) ? '*' : ' ');
			    out.format("%7c%s[%d]: %s%n", ch,
				       "GenericParameterType", j, gpType[j]);
			}
			break;
		    }
		}
	    }

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

[`Method.getGenericParameterTypes()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getGenericParameterTypes--) 将在类文件中查找方法签名属性，如果它存在。如果属性不可用，该方法就会退化为 [`Method.getParameterType()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getParameterType--) ，此方法在引入泛型时没有变化。另一个名为`getGeneric*Foo*()*`的方法通过反射获取某些`Foo`的值，实现类似。`Method.get*Types()`的返回值语法在 [`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--) 中描述。

下面是 [`java.util.Formatter`](https://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html) 中所有携带 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 参数的构造器的输出：

$ *java ConstructorSift java.util.Formatter java.util.Locale*

```
public
java.util.Formatter(java.io.OutputStream,java.lang.String,java.util.Locale)
throws java.io.UnsupportedEncodingException
       GenericParameterType[0]: class java.io.OutputStream
       GenericParameterType[1]: class java.lang.String
      *GenericParameterType[2]: class java.util.Locale
public java.util.Formatter(java.lang.String,java.lang.String,java.util.Locale)
throws java.io.FileNotFoundException,java.io.UnsupportedEncodingException
       GenericParameterType[0]: class java.lang.String
       GenericParameterType[1]: class java.lang.String
      *GenericParameterType[2]: class java.util.Locale
public java.util.Formatter(java.lang.Appendable,java.util.Locale)
       GenericParameterType[0]: interface java.lang.Appendable
      *GenericParameterType[1]: class java.util.Locale
public java.util.Formatter(java.util.Locale)
      *GenericParameterType[0]: class java.util.Locale
public java.util.Formatter(java.io.File,java.lang.String,java.util.Locale)
throws java.io.FileNotFoundException,java.io.UnsupportedEncodingException
       GenericParameterType[0]: class java.io.File
       GenericParameterType[1]: class java.lang.String
      *GenericParameterType[2]: class java.util.Locale
```

下面的例子输出展示了如何在 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 中搜索`char[]`类型参数。

$ *java ConstructorSift java.lang.String "[C"*

```
java.lang.String(int,int,char[])
       GenericParameterType[0]: int
       GenericParameterType[1]: int
      *GenericParameterType[2]: class [C
public java.lang.String(char[],int,int)
      *GenericParameterType[0]: class [C
       GenericParameterType[1]: int
       GenericParameterType[2]: int
public java.lang.String(char[])
      *GenericParameterType[0]: class [C
```

 [`Class.forName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#forName-java.lang.String-) 接受的表示引用类型和基本数据类型的数组的语法在 [`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--) 中描述。注意，首先列出的构造器是`package-private`，而不是`public`。它被返回是因为示例代码使用了 [`Class.getDeclaredConstructors()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredConstructors--) 而不是 [`Class.getConstructors()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getConstructors--) ，后者只返回`public`构造器。

这个示例展示了搜索可变参数个数，需要使用数组语法：

$ *java ConstructorSift java.lang.ProcessBuilder "[Ljava.lang.String;"*

```
public java.lang.ProcessBuilder(java.lang.String[])
      *GenericParameterType[0]: class [Ljava.lang.String;
```

这是源代码中实际的 [`ProcessBuilder`](https://docs.oracle.com/javase/8/docs/api/java/lang/ProcessBuilder.html#ProcessBuilder-java.lang.String...-) 构造器声明。

```java
public ProcessBuilder(String... command)
```

参数被表示为一个一维数组，元素类型为`java.lang.String`。可以通过调用 [`Constructor.isVarArgs()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#isVarArgs--) 区别于显式声明为`java.lang.String`数组的参数。

最后的示例输出声明为携带泛型类型参数的构造器：

$ *java ConstructorSift java.util.HashMap java.util.Map*

```
public java.util.HashMap(java.util.Map<? extends K, ? extends V>)
      *GenericParameterType[0]: java.util.Map<? extends K, ? extends V>
```

构造器的异常类型可以通过与检索方法类似的方式查找。参考 [Obtaining Method Type Information](https://docs.oracle.com/javase/tutorial/reflect/member/methodType.html) 章节中描述的 [`MethodSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodSpy.java) 示例获取更多细节。

#### 检索并解析构造器修饰符

由于构造器在语言中的特殊角色，相对于普通方法，只有少数几个修饰符可用于构造器：

- 访问修饰符： `public` ， `protected` ，和 `private`
- 注解

 [`ConstructorAccess`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ConstructorAccess.java) 示例在给定类中检索具有特定访问修饰符的构造器。它还显示构造器是否是合成的（编译器生成的）或者是否是可变参数的。

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.Modifier;
import java.lang.reflect.Type;
import static java.lang.System.out;

public class ConstructorAccess {
    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    Constructor[] allConstructors = c.getDeclaredConstructors();
	    for (Constructor ctor : allConstructors) {
		int searchMod = modifierFromString(args[1]);
		int mods = accessModifiers(ctor.getModifiers());
		if (searchMod == mods) {
		    out.format("%s%n", ctor.toGenericString());
		    out.format("  [ synthetic=%-5b var_args=%-5b ]%n",
			       ctor.isSynthetic(), ctor.isVarArgs());
		}
	    }

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }

    private static int accessModifiers(int m) {
	return m & (Modifier.PUBLIC | Modifier.PRIVATE | Modifier.PROTECTED);
    }

    private static int modifierFromString(String s) {
	if ("public".equals(s))               return Modifier.PUBLIC;
	else if ("protected".equals(s))       return Modifier.PROTECTED;
	else if ("private".equals(s))         return Modifier.PRIVATE;
	else if ("package-private".equals(s)) return 0;
	else return -1;
    }
}
```

不存在对应于`package-private`访问的显式 [`Modifier`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Modifier.html) 常量，因此有必要检查所有三种访问修饰符都不存在的情况以标识一个`package-private`构造器。

下面的输出展示了 [`java.io.File`](https://docs.oracle.com/javase/8/docs/api/java/io/File.html) 中的`private`构造器：

$ *java ConstructorAccess java.io.File private*

```
private java.io.File(java.lang.String,int)
  [ synthetic=false var_args=false ]
private java.io.File(java.lang.String,java.io.File)
  [ synthetic=false var_args=false ]
```

合成构造器很少见，不过 [`SyntheticConstructor`](https://docs.oracle.com/javase/tutorial/reflect/member/example/SyntheticConstructor.java) 示例展示了这种情况可能发生的典型情况：

```java
public class SyntheticConstructor {
    private SyntheticConstructor() {}
    class Inner {
	// Compiler will generate a synthetic constructor since
	// SyntheticConstructor() is private.
	Inner() { new SyntheticConstructor(); }
    }
}
```

$ *java ConstructorAccess SyntheticConstructor package-private*

```
SyntheticConstructor(SyntheticConstructor$1)
  [ synthetic=true  var_args=false ]
```

因为内部类构造器引用它所在的外部类的`private`构造器，编译器必须生成一个`package-private`构造器。参数类型 `SyntheticConstructor$1` 是任意的，依赖于编译器实现。依赖于任何合成的或者非`public`类成员的代码都是不可移植的。

构造器实现了 [`java.lang.reflect.AnnotatedElement`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AnnotatedElement.html) ，提供了检索携带 [`java.lang.annotation.RetentionPolicy.RUNTIME`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html#RUNTIME) 的运行时注解的方法。获取注解的例子参考 [Examining Class Modifiers and Types](https://docs.oracle.com/javase/tutorial/reflect/class/classModifiers.html) 章节。

#### 创建新的类实例

存在两种反射式方法来创建类实例： [`java.lang.reflect.Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 和 [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 。前者相对较好，因此在这些例子中使用。因为：

- [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 只能调用无参构造器，而 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 可以调用任何构造器，无论有多少个参数。
- [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 抛出构造器抛出的任何异常，无论是受检查的异常还是不受检查的异常。[`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 始终将抛出的异常包装为 [`InvocationTargetException`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html).
- [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 需要构造器是可见的； [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 在某些环境下可以调用 `private` 构造器。

有时可能需要从仅在构造之后设置的对象检索内部状态。考虑一种需要获取 [`java.io.Console`](https://docs.oracle.com/javase/8/docs/api/java/io/Console.html) 使用的内部字符集的场景。（`Console`字符集存储在私有字段中，不一定与  [`java.nio.charset.Charset.defaultCharset()`](https://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html#defaultCharset--) 返回的Java虚拟机缺省字符集相同。[`ConsoleCharset`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ConsoleCharset.java) 示例显示了如何实现此目的：

```java
import java.io.Console;
import java.nio.charset.Charset;
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import static java.lang.System.out;

public class ConsoleCharset {
    public static void main(String... args) {
	Constructor[] ctors = Console.class.getDeclaredConstructors();
	Constructor ctor = null;
	for (int i = 0; i < ctors.length; i++) {
	    ctor = ctors[i];
	    if (ctor.getGenericParameterTypes().length == 0)
		break;
	}

	try {
	    ctor.setAccessible(true);
 	    Console c = (Console)ctor.newInstance();
	    Field f = c.getClass().getDeclaredField("cs");
	    f.setAccessible(true);
	    out.format("Console charset         :  %s%n", f.get(c));
	    out.format("Charset.defaultCharset():  %s%n",
		       Charset.defaultCharset());

        // production code should handle these exceptions more gracefully
	} catch (InstantiationException x) {
	    x.printStackTrace();
 	} catch (InvocationTargetException x) {
 	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	}
    }
}
```

------

**注意：**

[`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 只有当构造器是无参的并且是可访问时才会成功。否则，有必要像上面的例子那样使用[`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 。

------

例子在 UNIX 系统上的输出：

$ *java ConsoleCharset*

```
Console charset          :  ISO-8859-1
Charset.defaultCharset() :  ISO-8859-1
```

例子在 Windows 系统上的输出：

C:\> *java ConsoleCharset*

```
Console charset          :  IBM437
Charset.defaultCharset() :  windows-1252
```

 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 的另一个常见应用是调用带参数的构造函数。 [`RestoreAliases`](https://docs.oracle.com/javase/tutorial/reflect/member/example/RestoreAliases.java) 示例查找特定的单参数构造函数并调用它：

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import java.util.HashMap;
import java.util.Map;
import java.util.Set;
import static java.lang.System.out;

class EmailAliases {
    private Set<String> aliases;
    private EmailAliases(HashMap<String, String> h) {
	aliases = h.keySet();
    }

    public void printKeys() {
	out.format("Mail keys:%n");
	for (String k : aliases)
	    out.format("  %s%n", k);
    }
}

public class RestoreAliases {

    private static Map<String, String> defaultAliases = new HashMap<String, String>();
    static {
	defaultAliases.put("Duke", "duke@i-love-java");
	defaultAliases.put("Fang", "fang@evil-jealous-twin");
    }

    public static void main(String... args) {
	try {
	    Constructor ctor = EmailAliases.class.getDeclaredConstructor(HashMap.class);
	    ctor.setAccessible(true);
	    EmailAliases email = (EmailAliases)ctor.newInstance(defaultAliases);
	    email.printKeys();

        // production code should handle these exceptions more gracefully
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	}
    }
}
```

此示例使用 [`Class.getDeclaredConstructor()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredConstructor-java.lang.Class...-) 来查找具有 [`java.util.HashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html) 类型的单个参数的构造函数。请注意，传递`HashMap.class`就足够了，因为任何`get*Constructor()`方法的参数需要类只用于类型目的。由于 [类型擦除](https://docs.oracle.com/javase/specs/jls/se7/html/jls-4.html#jls-4.6) ，以下表达式的计算结果为`true`：

```java
HashMap.class == defaultAliases.getClass()
```

此例子然后创建一个新的类实例，通过 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 使用构造器：

$ *java RestoreAliases*

```
Mail keys:
  Duke
  Fang
```

#### 故障排除

在尝试通过反射调用构造函数时，开发人员有时会遇到以下问题。

**丢失无参构造器导致的 InstantiationException**

 [`ConstructorTrouble`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ConstructorTrouble.java) 例子展示了当代码试图通过使用 [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 创建类的新实例，而不存在可访问的无参构造器情况下将会发生什么。

```java
public class ConstructorTrouble {
    private ConstructorTrouble(int i) {}

    public static void main(String... args){
	try {
	    Class<?> c = Class.forName("ConstructorTrouble");
	    Object o = c.newInstance();  // InstantiationException

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java ConstructorTrouble*

```
java.lang.InstantiationException: ConstructorTrouble
        at java.lang.Class.newInstance0(Class.java:340)
        at java.lang.Class.newInstance(Class.java:308)
        at ConstructorTrouble.main(ConstructorTrouble.java:7)
```

------

提示：可能发生 [`InstantiationException`](https://docs.oracle.com/javase/8/docs/api/java/lang/InstantiationException.html) 的原因有很多。在这种情况下，问题是带有`int`参数的构造函数的存在会阻止编译器生成缺省（或零参数）构造函数，并且代码中没有显式的零参数构造函数。请记住，[`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 的行为与`new`关键字非常相似，并且只要`new`失败就会失败。

------

**`Class.newInstance()` 抛出 `Unexpected Exception`**

 [`ConstructorTroubleToo`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ConstructorTroubleToo.java) 例子展示了 [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 的一个无法解决的问题。名义上，它传播由构造器抛出的所有异常，受检查的和不受检查的异常：

```java
import java.lang.reflect.InvocationTargetException;
import static java.lang.System.err;

public class ConstructorTroubleToo {
    public ConstructorTroubleToo() {
 	throw new RuntimeException("exception in constructor");
    }

    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName("ConstructorTroubleToo");
	    // Method propagetes any exception thrown by the constructor
	    // (including checked exceptions).
	    if (args.length > 0 && args[0].equals("class")) {
		Object o = c.newInstance();
	    } else {
		Object o = c.getConstructor().newInstance();
	    }

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	    err.format("%n%nCaught exception: %s%n", x.getCause());
	}
    }
}
```

$ *java ConstructorTroubleToo class*

```
Exception in thread "main" java.lang.RuntimeException: exception in constructor
        at ConstructorTroubleToo.<init>(ConstructorTroubleToo.java:6)
        at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
        at sun.reflect.NativeConstructorAccessorImpl.newInstance
          (NativeConstructorAccessorImpl.java:39)
        at sun.reflect.DelegatingConstructorAccessorImpl.newInstance
          (DelegatingConstructorAccessorImpl.java:27)
        at java.lang.reflect.Constructor.newInstance(Constructor.java:513)
        at java.lang.Class.newInstance0(Class.java:355)
        at java.lang.Class.newInstance(Class.java:308)
        at ConstructorTroubleToo.main(ConstructorTroubleToo.java:15)
```

这种情况是反射所特有的。通常，编写忽略已检查异常的代码是不可能的，因为它不会通过编译。可以使用 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 而不是 [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 来包装构造函数抛出的任何异常。

$ *java ConstructorTroubleToo*

```
java.lang.reflect.InvocationTargetException
        at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
        at sun.reflect.NativeConstructorAccessorImpl.newInstance
          (NativeConstructorAccessorImpl.java:39)
        at sun.reflect.DelegatingConstructorAccessorImpl.newInstance
          (DelegatingConstructorAccessorImpl.java:27)
        at java.lang.reflect.Constructor.newInstance(Constructor.java:513)
        at ConstructorTroubleToo.main(ConstructorTroubleToo.java:17)
Caused by: java.lang.RuntimeException: exception in constructor
        at ConstructorTroubleToo.<init>(ConstructorTroubleToo.java:6)
        ... 5 more


Caught exception: java.lang.RuntimeException: exception in constructor

```

如果抛出 [`InvocationTargetException`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html) ，则调用该方法。问题的诊断与直接调用构造函数并抛出[`InvocationTargetException.getCause()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html#getCause--) 检索的异常相同。此异常并不表示反射包或其用法存在问题。

------

**提示：**最好在 [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 上使用 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) ，因为前一个API允许检查和处理构造函数抛出的任意异常。

------

**定位或调用正确的构造函数时出现问题**

 [`ConstructorTroubleAgain`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ConstructorTroubleAgain.java) 类展示各种不正确的代码标识和调用期待中的构造器的方法：

```java
import java.lang.reflect.InvocationTargetException;
import static java.lang.System.out;

public class ConstructorTroubleAgain {
    public ConstructorTroubleAgain() {}

    public ConstructorTroubleAgain(Integer i) {}

    public ConstructorTroubleAgain(Object o) {
	out.format("Constructor passed Object%n");
    }

    public ConstructorTroubleAgain(String s) {
	out.format("Constructor passed String%n");
    }

    public static void main(String... args){
	String argType = (args.length == 0 ? "" : args[0]);
	try {
	    Class<?> c = Class.forName("ConstructorTroubleAgain");
	    if ("".equals(argType)) {
		// IllegalArgumentException: wrong number of arguments
		Object o = c.getConstructor().newInstance("foo");
	    } else if ("int".equals(argType)) {
		// NoSuchMethodException - looking for int, have Integer
		Object o = c.getConstructor(int.class);
	    } else if ("Object".equals(argType)) {
		// newInstance() does not perform method resolution
		Object o = c.getConstructor(Object.class).newInstance("foo");
	    } else {
		assert false;
	    }

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java ConstructorTroubleAgain*

```
Exception in thread "main" java.lang.IllegalArgumentException: wrong number of
  arguments
        at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
        at sun.reflect.NativeConstructorAccessorImpl.newInstance
          (NativeConstructorAccessorImpl.java:39)
        at sun.reflect.DelegatingConstructorAccessorImpl.newInstance
          (DelegatingConstructorAccessorImpl.java:27)
        at java.lang.reflect.Constructor.newInstance(Constructor.java:513)
        at ConstructorTroubleAgain.main(ConstructorTroubleAgain.java:23)
```

抛出 [`IllegalArgumentException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html) ，因为请求了零参数构造函数并尝试传递参数。如果构造函数传递了错误类型的参数，则会抛出相同的异常。

$ *java ConstructorTroubleAgain int*

```
java.lang.NoSuchMethodException: ConstructorTroubleAgain.<init>(int)
        at java.lang.Class.getConstructor0(Class.java:2706)
        at java.lang.Class.getConstructor(Class.java:1657)
        at ConstructorTroubleAgain.main(ConstructorTroubleAgain.java:26)
```

如果开发人员错误地认为反射将是自动装箱或拆箱类型，则可能会发生此异常。装箱（将基元转换为引用类型）仅在编译期间发生。反射中没有机会发生此操作，因此在查找构造函数时必须使用特定类型。

$ *java ConstructorTroubleAgain Object*

```
Constructor passed Object
```

在这里，可能需要调用带有 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 参数的构造函数，因为 `newInstance()` 是使用更具体的`String`类型调用的。但是为时已晚！找到的构造函数已经是具有 [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 参数的构造函数。`newInstance()` 不会尝试进行方法解析；它只是对现有的构造函数对象进行操作。

------

**提示：**`new`和 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 之间的一个重要区别是`new`执行方法参数类型检查，装箱和方法解析。这些都不会发生在反射中，必须做出明确的选择。

------

**尝试调用不可访问的构造器时发生 IllegalAccessException**

 [`IllegalAccessException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalAccessException.html) 会被抛出，如果尝试调用一个`private`或者其它不可访问的构造器。下面的例子展示了产生的异常栈跟踪信息：

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;

class Deny {
    private Deny() {
	System.out.format("Deny constructor%n");
    }
}

public class ConstructorTroubleAccess {
    public static void main(String... args) {
	try {
	    Constructor c = Deny.class.getDeclaredConstructor();
//  	    c.setAccessible(true);   // solution
	    c.newInstance();

        // production code should handle these exceptions more gracefully
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java ConstructorTroubleAccess*

```
java.lang.IllegalAccessException: Class ConstructorTroubleAccess can not access
  a member of class Deny with modifiers "private"
        at sun.reflect.Reflection.ensureMemberAccess(Reflection.java:65)
        at java.lang.reflect.Constructor.newInstance(Constructor.java:505)
        at ConstructorTroubleAccess.main(ConstructorTroubleAccess.java:15)
```

------

**提示：**存在一个访问限制，它阻止了通常无法通过直接调用访问的构造函数的反射调用。（这包括但不限于单独类中的私有构造函数和单独私有类中的公共构造函数。）但是，`Constructor` 声明为扩展了[`AccessibleObject`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html) ，它提供了通过[`AccessibleObject.setAccessible()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html#setAccessible-boolean-)来抑制此检查的功能。

------

## 数组和枚举类型

从 Java 虚拟机角度看来，数组和枚举类型也仅仅是类而已。 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 中的许多方法都可以用于它们。反射提供了一些特殊的 API 给数组和枚举。本课程使用一系列代码示例描述如何将这些类型的对象区别于其它类对象，并在其上执行操作。同时也解释了可能遇到的各种错误。

**数组**

数组拥有元素类型以及一个长度属性（该属性并不是该类型的一部分）。数组可以整体被修改，或者以元素为单位修改。反射提供了 [`java.lang.reflect.Array`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html) 用来实现后一种操作。

- [识别数组类型](https://docs.oracle.com/javase/tutorial/reflect/special/arrayComponents.html) 描述如何确定一个类成员是一个字段还是数组类型。
- [创建新数组](https://docs.oracle.com/javase/tutorial/reflect/special/arrayInstance.html) 展示如何创建包含简单或者复杂类型元素的数组。
- [获取和设定数组以及它们的元素](https://docs.oracle.com/javase/tutorial/reflect/special/arraySetGet.html) 展示如何访问数组类型字段或者单独访问数组元素。
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/special/arrayTrouble.html) 涵盖常见错误和编程误解。

**枚举类型**

在反射代码中，枚举类型的处理与普通类型没有什么区别。 [`Class.isEnum()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isEnum--) 告诉我们是否一个 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 表示并且`enum` 。 [`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--) 检索枚举类中定义的枚举常量。[`java.lang.reflect.Field.isEnumConstant()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isEnumConstant--) 指出一个字段是否是枚举类型。

- [检查枚举](https://docs.oracle.com/javase/tutorial/reflect/special/enumMembers.html) 展示如何检索一个枚举常量以及任何其它字段、构造器、以及方法。
- [获取和设定枚举类型字段](https://docs.oracle.com/javase/tutorial/reflect/special/enumSetGet.html) 展示如何获取和设置一个使用枚举常量值的字段。
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/special/enumTrouble.html) 描述有关枚举的常见错误。

### 数组

数组是引用类型的对象，它包含固定数量的相同类型的元素，数组的长度是不可变的。创建数组实例需要了解长度和元素类型。每个元素可以是基本类型（例如，`byte`，`int`或`double`），引用类型（例如，`String`，`Object`，或者 `java.nio.CharBuffer`）或数组。多维数组实际上只是包含数组类型元素的数组。

数组在 Java 虚拟机内部实现。数组上的方法都是继承自 [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 。数组的长度不是它的类型的一部分，数组拥有一个`length`字段，可以通过 [`java.lang.reflect.Array.getLength()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#getLength-java.lang.Object-) 访问。

反射提供了方法来访问数组类型和数组元素类型，创建新的数组，以及检索或者设定数组元素值。下面的章节包含数组操作的例子：

- [识别数组类型](https://docs.oracle.com/javase/tutorial/reflect/special/arrayComponents.html) 描述如何确定一个类成员是否是数组类型字段
- [创建新数组](https://docs.oracle.com/javase/tutorial/reflect/special/arrayInstance.html) 展示如何创建简单元素类型和复杂元素类型的数组实例
- [获取和设定数组以及它们的元素](https://docs.oracle.com/javase/tutorial/reflect/special/arraySetGet.html) 展示如何访问数组类型字段或者单独访问数组元素。
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/special/arrayTrouble.html) 涵盖常见错误和编程误解。

所有这些操作都通过 [`java.lang.reflect.Array`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html) 中的`static`方法来支持。

#### 识别数组类型

数组类型可以通过调用 [`Class.isArray()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isArray--) 来识别。为了获取 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 使用本课程的 [Retrieving Class Objects](https://docs.oracle.com/javase/tutorial/reflect/class/classNew.html) 章节中描述的方法之一。

 [`ArrayFind`](https://docs.oracle.com/javase/tutorial/reflect/special/example/ArrayFind.java) 示例识别命名的类中的数组类型的字段，并报告它们的元素类型。

```java
import java.lang.reflect.Field;
import java.lang.reflect.Type;
import static java.lang.System.out;

public class ArrayFind {
    public static void main(String... args) {
	boolean found = false;
 	try {
	    Class<?> cls = Class.forName(args[0]);
	    Field[] flds = cls.getDeclaredFields();
	    for (Field f : flds) {
 		Class<?> c = f.getType();
		if (c.isArray()) {
		    found = true;
		    out.format("%s%n"
                               + "           Field: %s%n"
			       + "            Type: %s%n"
			       + "  Component Type: %s%n",
			       f, f.getName(), c, c.getComponentType());
		}
	    }
	    if (!found) {
		out.format("No array fields%n");
	    }

        // production code should handle this exception more gracefully
 	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

在 [`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--) 中描述了`Class.get*Type()` 的返回值的语法。类型名称开头的'`[`'字符数表示数组的维数（即嵌套深度）。

输出样本如下。用户输入以斜体显示。一个原始类型`byte`的数组：

$ *java ArrayFind java.nio.ByteBuffer*

```
final byte[] java.nio.ByteBuffer.hb
           Field: hb
            Type: class [B
  Component Type: byte
```

引用类型 [`StackTraceElement`](https://docs.oracle.com/javase/8/docs/api/java/lang/StackTraceElement.html) 的数组：

$ *java ArrayFind java.lang.Throwable*

```
private java.lang.StackTraceElement[] java.lang.Throwable.stackTrace
           Field: stackTrace
            Type: class [Ljava.lang.StackTraceElement;
  Component Type: class java.lang.StackTraceElement
```

`predefined`是一个引用类型 [`java.awt.Cursor`](https://docs.oracle.com/javase/8/docs/api/java/awt/Cursor.html) 的一维数组，` cursorProperties`是引用类型 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 的二维数组：

$ *java ArrayFind java.awt.Cursor*

```
protected static java.awt.Cursor[] java.awt.Cursor.predefined
           Field: predefined
            Type: class [Ljava.awt.Cursor;
  Component Type: class java.awt.Cursor
static final java.lang.String[][] java.awt.Cursor.cursorProperties
           Field: cursorProperties
            Type: class [[Ljava.lang.String;
  Component Type: class [Ljava.lang.String;
```

#### 创建新数组

与非反射式代码一样，反射通过 [`java.lang.reflect.Array.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#newInstance-java.lang.Class-int-) 支持动态创建任意类型和维度的数组的能力。考虑[`ArrayCreator`](https://docs.oracle.com/javase/tutorial/reflect/special/example/ArrayCreator.java) ，一个基本的适用于动态创建数组的翻译器。将被解析的语法如下：

```
fully_qualified_class_name variable_name[] = 
     { val1, val2, val3, ... }
```

假设`fully_qualified_class_name`表示一个具有构造函数的类，该构造函数具有单个 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 参数。数组的大小由提供的值的数量决定。下面的例子将构造一个`fully_qualified_class_name`数组的实例，并用`val1`，`val2`等给出的实例填充它的值。（这个例子假设熟悉 [`Class.getConstructor()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getConstructor-java.lang.Class...-) 和[`java.lang.reflect.Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 。关于 [`Constructor`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html) 反射 API 的讨论参见 [Creating New Class Instances](https://docs.oracle.com/javase/tutorial/reflect/member/ctorInstance.html) 部分。）

```java
import java.lang.reflect.Array;
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.util.regex.Pattern;
import java.util.regex.Matcher;
import java.util.Arrays;
import static java.lang.System.out;

public class ArrayCreator {
    private static String s = "java.math.BigInteger bi[] = { 123, 234, 345 }";
    private static Pattern p = Pattern.compile("^\\s*(\\S+)\\s*\\w+\\[\\].*\\{\\s*([^}]+)\\s*\\}");

    public static void main(String... args) {
        Matcher m = p.matcher(s);

        if (m.find()) {
            String cName = m.group(1);
            String[] cVals = m.group(2).split("[\\s,]+");
            int n = cVals.length;

            try {
                Class<?> c = Class.forName(cName);
                Object o = Array.newInstance(c, n);
                for (int i = 0; i < n; i++) {
                    String v = cVals[i];
                    Constructor ctor = c.getConstructor(String.class);
                    Object val = ctor.newInstance(v);
                    Array.set(o, i, val);
                }

                Object[] oo = (Object[])o;
                out.format("%s[] = %s%n", cName, Arrays.toString(oo));

            // production code should handle these exceptions more gracefully
            } catch (ClassNotFoundException x) {
                x.printStackTrace();
            } catch (NoSuchMethodException x) {
                x.printStackTrace();
            } catch (IllegalAccessException x) {
                x.printStackTrace();
            } catch (InstantiationException x) {
                x.printStackTrace();
            } catch (InvocationTargetException x) {
                x.printStackTrace();
            }
        }
    }
}
```

$ *java ArrayCreator*

```
java.math.BigInteger [] = [123, 234, 345]
```

上面的例子显示了一种可能需要通过反射创建数组的情况; 即如果直到运行时才知道元素类型。在这种情况下，代码使用 [`Class.forName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#forName--) 来获取所需元素类型的类，然后在设置相应的数组值之前调用特定的构造函数来初始化数组的每个元素。

#### 获取和设置数组和数组元素

正如在非反射代码中一样，可以整体地或逐个元素设置或检索数组元素。要一次设置整个数组，请使用[`java.lang.reflect.Field.set(Object obj, Object value)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#set-java.lang.Object-java.lang.Object-) 。要检索整个数组，请使用 [`Field.get(Object)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#get-java.lang.Object-) 。可以使用[`java.lang.reflect.Array`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html) 中的方法设置或检索单个元素。

[`Array`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html) 提供了 `set*Foo*()` 和 `get*Foo*()`形式的方法用于设置和获取任何基本类型的元素。例如，`int`数组的元素可以用[`Array.setInt(Object array, int index, int value)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#setInt-java.lang.Objectint-int-) 设置，可以使用 [`Array.getInt(Object array, int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#getInt-java.lang.Object-int-) 获取。

这些方法支持数据类型的自动扩宽。因此，[`Array.setShort()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#getShort-java.lang.Object-int-) 可以被用来设定`int`类型数组，因为 16 位的`short`可以被扩宽为 32 位的`int`，而不会丢失数据。另一方面，在`int`数组上调用 [`Array.setLong()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#setLong-java.lang.Object-int-long-) 将会导致抛出  [`IllegalArgumentException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html) ，因为 64 位的`long`无法在不丢失信息的情况下缩窄为 32 位的`int`。无论传递的实际值是否可以在目标数据类型中准确表示，都是如此。[*The Java Language Specification, Java SE 7 Edition*](https://docs.oracle.com/javase/specs/jls/se7/html/index.html) ， [Widening Primitive Conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.2) 和 [Narrowing Primitive Conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.3) 包含有关数据类型扩宽和缩窄转换的完整讨论。

引用类型数组的元素(包括数组的数组)可以使用 [`Array.set(Object array, int index, int value)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#set-java.lang.Object-int-int-) 和 [`Array.get(Object array, int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#get-java.lang.Object-int-) 设定和检索。

**设定类型数组的字段**

[`GrowBufferedReader`](https://docs.oracle.com/javase/tutorial/reflect/special/example/GrowBufferedReader.java) 示例说明了如何替换数组类型字段的值。在这种情况下，代码替换[`java.io.BufferedReader`](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html) 的后备数组为更大的一个。（这假设原始`BufferedReader`的创建是在不可修改的代码中，否则，简单地使用备用构造函数 [`BufferedReader(java.io.Reader in, int size)`](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html#BufferedReader-java.io.Reader-int-) 将是无意义的，它接受输入缓冲区大小。）

```java
import java.io.BufferedReader;
import java.io.CharArrayReader;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.lang.reflect.Field;
import java.util.Arrays;
import static java.lang.System.out;

public class GrowBufferedReader {
    private static final int srcBufSize = 10 * 1024;
    private static char[] src = new char[srcBufSize];
    static {
	src[srcBufSize - 1] = 'x';
    }
    private static CharArrayReader car = new CharArrayReader(src);

    public static void main(String... args) {
	try {
	    BufferedReader br = new BufferedReader(car);

	    Class<?> c = br.getClass();
	    Field f = c.getDeclaredField("cb");

	    // cb is a private field
	    f.setAccessible(true);
	    char[] cbVal = char[].class.cast(f.get(br));

	    char[] newVal = Arrays.copyOf(cbVal, cbVal.length * 2);
	    if (args.length > 0 && args[0].equals("grow"))
		f.set(br, newVal);

	    for (int i = 0; i < srcBufSize; i++)
		br.read();

	    // see if the new backing array is being used
	    if (newVal[srcBufSize - 1] == src[srcBufSize - 1])
		out.format("Using new backing array, size=%d%n", newVal.length);
	    else
		out.format("Using original backing array, size=%d%n", cbVal.length);

        // production code should handle these exceptions more gracefully
	} catch (FileNotFoundException x) {
	    x.printStackTrace();
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (IOException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java GrowBufferedReader grow*

```
Using new backing array, size=16384
```

$ *java GrowBufferedReader*

```
Using original backing array, size=8192
```

请注意，上面的示例使用了数组实用程序方法 [`java.util.Arrays.copyOf()`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#copyOf-char:A-int-) 。[`java.util.Arrays`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html) 包含许多在数组上操作时很方便的方法。

**访问多维数组的元素**

多维数组只是嵌套数组。二维数组是一维数组的数组。三维数组是二维数组的数组，依此类推。 [`CreateMatrix`](https://docs.oracle.com/javase/tutorial/reflect/special/example/CreateMatrix.java) 示例说明了如何使用反射创建和初始化多维数组。

```java
import java.lang.reflect.Array;
import static java.lang.System.out;

public class CreateMatrix {
    public static void main(String... args) {
        Object matrix = Array.newInstance(int.class, 2, 2);
        Object row0 = Array.get(matrix, 0);
        Object row1 = Array.get(matrix, 1);

        Array.setInt(row0, 0, 1);
        Array.setInt(row0, 1, 2);
        Array.setInt(row1, 0, 3);
        Array.setInt(row1, 1, 4);

        for (int i = 0; i < 2; i++)
            for (int j = 0; j < 2; j++)
                out.format("matrix[%d][%d] = %d%n", i, j, ((int[][])matrix)[i][j]);
    }
}
```

$ *java CreateMatrix*

```
matrix[0][0] = 1
matrix[0][1] = 2
matrix[1][0] = 3
matrix[1][1] = 4
```

使用以下代码片段可以获得相同的结果：

```java
Object matrix = Array.newInstance(int.class, 2);
Object row0 = Array.newInstance(int.class, 2);
Object row1 = Array.newInstance(int.class, 2);

Array.setInt(row0, 0, 1);
Array.setInt(row0, 1, 2);
Array.setInt(row1, 0, 3);
Array.setInt(row1, 1, 4);

Array.set(matrix, 0, row0);
Array.set(matrix, 1, row1);
```

变量参数 [`Array.newInstance(Class componentType, int... dimensions)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#newInstance-java.lang.Class-int...-) 提供了一种创建多维数组的便捷方法，但仍需要使用多维数组是嵌套数组的原则来初始化元素。（为此目的，反射不提供多个索引的 `get`/`set` 方法。）

#### 故障排除

接下面举例说明在操作数组时可能遇到的典型错误。

**不可转化类型导致的 IllegalArgumentException**

 [`ArrayTroubleAgain`](https://docs.oracle.com/javase/tutorial/reflect/special/example/ArrayTroubleAgain.java) 示例将产生 [`IllegalArgumentException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html) 。 [`Array.setInt()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#setInt-java.lang.Object-int-int-) 被调用以设定一个元素的值，该元素是引用类型`Integer`，赋予它的值是基本数据类型`int`值。在非反射式等待代码`ary[0]=0`中，编译器将转化（或者装箱）值`1`为引用类型`new Integer(1)`，从而该语句将通过类型检查。当使用反射时，类型检查只会在运行时发生，因而没有机会进行类型装箱。

```java
import java.lang.reflect.Array;
import static java.lang.System.err;

public class ArrayTroubleAgain {
    public static void main(String... args) {
	Integer[] ary = new Integer[2];
	try {
	    Array.setInt(ary, 0, 1);  // IllegalArgumentException

        // production code should handle these exceptions more gracefully
	} catch (IllegalArgumentException x) {
	    err.format("Unable to box%n");
	} catch (ArrayIndexOutOfBoundsException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java ArrayTroubleAgain*

```
Unable to box
```

为了消除此异常，有问题的代码行应该修改为如下对 [`Array.set(Object array, int index, Object value)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#set-java.lang.Object-int-java.lang.Object-) 的调用：

```java
Array.set(ary, 0, new Integer(1));
```

------

**提示：**

当使用反射设置或者获取数组元素时，编译器没有机会执行自动装箱。它仅仅可以转化那些在 `Class.isAssignableFrom()` 规范中描述的相关类型。上面的例子会失败，因为在这个测试中 `isAssignableFrom()` 将返回 `false`。该方法可以被用来校验一个特定转化是否可行：

```java
Integer.class.isAssignableFrom(int.class) == false 
```

类似地，从基本数据类型向引用类型的自动转化在反射中也是不可能的。

```java
int.class.isAssignableFrom(Integer.class) == false
```

------

**空数组导致的 ArrayIndexOutOfBoundsException**

 [`ArrayTrouble`](https://docs.oracle.com/javase/tutorial/reflect/special/example/ArrayTrouble.java) 示例展示了当试图访问一个长度为 0 的数组的元素时将会发生的错误。

```java
import java.lang.reflect.Array;
import static java.lang.System.out;

public class ArrayTrouble {
    public static void main(String... args) {
        Object o = Array.newInstance(int.class, 0);
        int[] i = (int[])o;
        int[] j = new int[0];
        out.format("i.length = %d, j.length = %d, args.length = %d%n",
                   i.length, j.length, args.length);
        Array.getInt(o, 0);  // ArrayIndexOutOfBoundsException
    }
}
```

$ *java ArrayTrouble*

```
i.length = 0, j.length = 0, args.length = 0
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException
        at java.lang.reflect.Array.getInt(Native Method)
        at ArrayTrouble.main(ArrayTrouble.java:11)
```

------

**提示：**没有元素的数组（空数组）是可能存在的。尽管在通常的代码中很少见，还是有可能会发生意外的反射的情况。当然，不可能设定或者获取一个空数组的元素值，因为这种操作会抛出 [`ArrayIndexOutOfBoundsException`](https://docs.oracle.com/javase/8/docs/api/java/lang/ArrayIndexOutOfBoundsException.html) 。

------

**试图类型缩窄导致的 IllegalArgumentException**

 [`ArrayTroubleToo`](https://docs.oracle.com/javase/tutorial/reflect/special/example/ArrayTroubleToo.java) 示例包含会失败的代码，这些代码试图执行某些可能会导致数据丢失的操作。

```java
import java.lang.reflect.Array;
import static java.lang.System.out;

public class ArrayTroubleToo {
    public static void main(String... args) {
        Object o = new int[2];
        Array.setShort(o, 0, (short)2);  // widening, succeeds
        Array.setLong(o, 1, 2L);         // narrowing, fails
    }
}
```

$ *java ArrayTroubleToo*

```
Exception in thread "main" java.lang.IllegalArgumentException: argument type
  mismatch
        at java.lang.reflect.Array.setLong(Native Method)
        at ArrayTroubleToo.main(ArrayTroubleToo.java:9)
```

------

**提示：**`Array.set*()` 和 `Array.get*()` 方法将执行自动类型扩宽转化，但是如果试图进行类型缩窄就会抛出 [`IllegalArgumentException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html) 。关于类型扩宽和缩窄的完整讨论参见 [*The Java Language Specification, Java SE 7 Edition*](https://docs.oracle.com/javase/specs/jls/se7/html/index.html) 中的 [Widening Primitive Conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.2) 和 [Narrowing Primitive Conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.3) 章节。

------

### 枚举类型

枚举是一个语言结构，用来定义类型安全的枚举，可以被用于需要一个固定的命名值集合的情况。所有枚举都隐式扩展 [`java.lang.Enum`](https://docs.oracle.com/javase/8/docs/api/java/lang/Enum.html) 。枚举可以包含一个或者多个枚举常量，定义了该枚举类型的独特实例。一个枚举声明定义一个枚举类型，类似于普通的类，它可以包含诸如字段、方法、构造器（有些额外限制）等成员。

因为枚举也是类，反射就不需要显式定义 `java.lang.reflect.Enum` 类。唯一专用于枚举的反射 API 是 [`Class.isEnum()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isEnum--) ，[`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--) ，和 [`java.lang.reflect.Field.isEnumConstant()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isEnumConstant--)。大部分对枚举的反射操作与其它类没啥两样。比如，枚举常量作为枚举类型中的`public static final`字段实现。下面的章节展示如何为枚举使用  [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 和 [`java.lang.reflect.Field`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html) 。 

- [检查枚举](https://docs.oracle.com/javase/tutorial/reflect/special/enumMembers.html) 展示如何获取枚举常量以及任何其它字段、构造器以及方法
- [获取并设定枚举类型的字段](https://docs.oracle.com/javase/tutorial/reflect/special/enumSetGet.html) 展示如何设定和获取枚举常量值字段
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/special/enumTrouble.html) 描述枚举有关的常见错误

对枚举的介绍，请参考 [Enum Types](https://docs.oracle.com/javase/tutorial/java/javaOO/enum.html) 章节。

#### 检查枚举

反射提供了3个枚举专属 API：

- [`Class.isEnum()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isEnum--)

  指明这个类是否表示一个枚举类型

- [`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--)

  按照声明顺序检索由该枚举类定义的枚举常量的列表

- [`java.lang.reflect.Field.isEnumConstant()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isEnumConstant--)

  指明该字段是否表示一个枚举类型元素

有时候我们需要动态地检索枚举常量列表：在非反射式代码中，通过调用枚举上隐式声明的`static`方法  [`values()`](https://docs.oracle.com/javase/specs/jls/se7/html/jls-8.html) 来实现。如果一个枚举类型实例不可用，则获得可能值列表的唯一方法就是调用 [`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--) ，因为枚举类型是不可能实例化的。

给定一个全限定类名， [`EnumConstants`](https://docs.oracle.com/javase/tutorial/reflect/special/example/EnumConstants.java) 示例展示如何使用 [`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--) 检索一个枚举类型中的枚举常量的有序列表。

```java
import java.util.Arrays;
import static java.lang.System.out;

enum Eon { HADEAN, ARCHAEAN, PROTEROZOIC, PHANEROZOIC }

public class EnumConstants {
    public static void main(String... args) {
	try {
	    Class<?> c = (args.length == 0 ? Eon.class : Class.forName(args[0]));
	    out.format("Enum name:  %s%nEnum constants:  %s%n",
		       c.getName(), Arrays.asList(c.getEnumConstants()));
	    if (c == Eon.class)
		out.format("  Eon.values():  %s%n",
			   Arrays.asList(Eon.values()));

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

部分输出如下：

$ *java EnumConstants java.lang.annotation.RetentionPolicy*

```
Enum name:  java.lang.annotation.RetentionPolicy
Enum constants:  [SOURCE, CLASS, RUNTIME]
```

$ *java EnumConstants java.util.concurrent.TimeUnit*

```
Enum name:  java.util.concurrent.TimeUnit
Enum constants:  [NANOSECONDS, MICROSECONDS, 
                  MILLISECONDS, SECONDS, 
                  MINUTES, HOURS, DAYS]
```

这个例子还展示了 [`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--) 的返回值等于调用枚举类型上的`values()`方法的返回值。

$ *java EnumConstants*

```
Enum name:  Eon
Enum constants:  [HADEAN, ARCHAEAN, 
                  PROTEROZOIC, PHANEROZOIC]
Eon.values():  [HADEAN, ARCHAEAN, 
                PROTEROZOIC, PHANEROZOIC]
```

由于枚举是类，因此可以使用此课程的 [Fields](https://docs.oracle.com/javase/tutorial/reflect/member/field.html) ， [Methods](https://docs.oracle.com/javase/tutorial/reflect/member/method.html) ， 和 [Constructors](https://docs.oracle.com/javase/tutorial/reflect/member/ctor.html) 部分中描述的相同反射 API 获取其他信息。[`EnumSpy`](https://docs.oracle.com/javase/tutorial/reflect/special/example/EnumSpy.java)说明了如何使用这些API获取有关枚举声明的其他信息。该示例使用 [`Class.isEnum()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isEnum--) 来限制检查的类集合。它还使用 [`Field.isEnumConstant()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isEnumConstant--) 来区分枚举常量与枚举声明中的其他字段（并非所有字段都是枚举常量）。

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;
import java.lang.reflect.Member;
import java.util.List;
import java.util.ArrayList;
import static java.lang.System.out;

public class EnumSpy {
    private static final String fmt = "  %11s:  %s %s%n";

    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    if (!c.isEnum()) {
		out.format("%s is not an enum type%n", c);
		return;
	    }
	    out.format("Class:  %s%n", c);

	    Field[] flds = c.getDeclaredFields();
	    List<Field> cst = new ArrayList<Field>();  // enum constants
	    List<Field> mbr = new ArrayList<Field>();  // member fields
	    for (Field f : flds) {
		if (f.isEnumConstant())
		    cst.add(f);
		else
		    mbr.add(f);
	    }
	    if (!cst.isEmpty())
		print(cst, "Constant");
	    if (!mbr.isEmpty())
		print(mbr, "Field");

	    Constructor[] ctors = c.getDeclaredConstructors();
	    for (Constructor ctor : ctors) {
		out.format(fmt, "Constructor", ctor.toGenericString(),
			   synthetic(ctor));
	    }

	    Method[] mths = c.getDeclaredMethods();
	    for (Method m : mths) {
		out.format(fmt, "Method", m.toGenericString(),
			   synthetic(m));
	    }

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }

    private static void print(List<Field> lst, String s) {
	for (Field f : lst) {
 	    out.format(fmt, s, f.toGenericString(), synthetic(f));
	}
    }

    private static String synthetic(Member m) {
	return (m.isSynthetic() ? "[ synthetic ]" : "");
    }
}
```

$ *java EnumSpy java.lang.annotation.RetentionPolicy*

```
Class:  class java.lang.annotation.RetentionPolicy
     Constant:  public static final java.lang.annotation.RetentionPolicy
                  java.lang.annotation.RetentionPolicy.SOURCE 
     Constant:  public static final java.lang.annotation.RetentionPolicy
                  java.lang.annotation.RetentionPolicy.CLASS 
     Constant:  public static final java.lang.annotation.RetentionPolicy 
                  java.lang.annotation.RetentionPolicy.RUNTIME 
        Field:  private static final java.lang.annotation.RetentionPolicy[] 
                  java.lang.annotation.RetentionPolicy. [ synthetic ]
  Constructor:  private java.lang.annotation.RetentionPolicy() 
       Method:  public static java.lang.annotation.RetentionPolicy[]
                  java.lang.annotation.RetentionPolicy.values() 
       Method:  public static java.lang.annotation.RetentionPolicy
                  java.lang.annotation.RetentionPolicy.valueOf(java.lang.String) 

```

输出表明 [`java.lang.annotation.RetentionPolicy`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html) 声明只包含 3 个枚举常量。枚举常量作为`public static final`字段暴露。字段、构造器、以及方法都是编译器生成的。`$VALUES`字段与`values()`方法的实现有关。

------

**注意：**由于各种原因，包括对枚举类型的演化的支持，枚举常量的声明顺序很重要。 [`Class.getFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getFields--) 和 [`Class.getDeclaredFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredFields--) 不保证返回值的顺序与源代码中的声明顺序匹配。如果应用程序需要排序，请使用 [`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--) 。

------

 [`java.util.concurrent.TimeUnit`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/TimeUnit.html) 的输出显示了更复杂的枚举是可能的。该类包括几个方法以及声明为`static final`的其他字段，这些字段不是枚举常量。

$ *java EnumSpy java.util.concurrent.TimeUnit*

```
Class:  class java.util.concurrent.TimeUnit
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.NANOSECONDS
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.MICROSECONDS
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.MILLISECONDS
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.SECONDS
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.MINUTES
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.HOURS
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.DAYS
        Field:  static final long java.util.concurrent.TimeUnit.C0
        Field:  static final long java.util.concurrent.TimeUnit.C1
        Field:  static final long java.util.concurrent.TimeUnit.C2
        Field:  static final long java.util.concurrent.TimeUnit.C3
        Field:  static final long java.util.concurrent.TimeUnit.C4
        Field:  static final long java.util.concurrent.TimeUnit.C5
        Field:  static final long java.util.concurrent.TimeUnit.C6
        Field:  static final long java.util.concurrent.TimeUnit.MAX
        Field:  private static final java.util.concurrent.TimeUnit[] 
                  java.util.concurrent.TimeUnit. [ synthetic ]
  Constructor:  private java.util.concurrent.TimeUnit()
  Constructor:  java.util.concurrent.TimeUnit
                  (java.lang.String,int,java.util.concurrent.TimeUnit)
                  [ synthetic ]
       Method:  public static java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.valueOf(java.lang.String)
       Method:  public static java.util.concurrent.TimeUnit[] 
                  java.util.concurrent.TimeUnit.values()
       Method:  public void java.util.concurrent.TimeUnit.sleep(long) 
                  throws java.lang.InterruptedException
       Method:  public long java.util.concurrent.TimeUnit.toNanos(long)
       Method:  public long java.util.concurrent.TimeUnit.convert
                  (long,java.util.concurrent.TimeUnit)
       Method:  abstract int java.util.concurrent.TimeUnit.excessNanos
                  (long,long)
       Method:  public void java.util.concurrent.TimeUnit.timedJoin
                  (java.lang.Thread,long) throws java.lang.InterruptedException
       Method:  public void java.util.concurrent.TimeUnit.timedWait
                  (java.lang.Object,long) throws java.lang.InterruptedException
       Method:  public long java.util.concurrent.TimeUnit.toDays(long)
       Method:  public long java.util.concurrent.TimeUnit.toHours(long)
       Method:  public long java.util.concurrent.TimeUnit.toMicros(long)
       Method:  public long java.util.concurrent.TimeUnit.toMillis(long)
       Method:  public long java.util.concurrent.TimeUnit.toMinutes(long)
       Method:  public long java.util.concurrent.TimeUnit.toSeconds(long)
       Method:  static long java.util.concurrent.TimeUnit.x(long,long,long)
```

#### 获取和设定枚举类型字段

存储枚举的字段像其它任何引用类型字段一样存取，使用 [`Field.set()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#set-java.lang.Object-java.lang.Object-) 和 [`Field.get()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#get-java.lang.Object-) 。有关访问字段的更多信息，参考 [Fields](https://docs.oracle.com/javase/tutorial/reflect/member/field.html) 章节。

考虑需要动态修改服务器应用程序中日志跟踪级别的应用程序，该应用程序通常在运行时不允许此更改。假设服务器对象的实例可用。 [`SetTrace`](https://docs.oracle.com/javase/tutorial/reflect/special/example/SetTrace.java) 示例显示了代码如何将枚举的 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 表示形式转换为枚举类型，并检索和设置存储枚举的字段的值。

```java
import java.lang.reflect.Field;
import static java.lang.System.out;

enum TraceLevel { OFF, LOW, MEDIUM, HIGH, DEBUG }

class MyServer {
    private TraceLevel level = TraceLevel.OFF;
}

public class SetTrace {
    public static void main(String... args) {
	TraceLevel newLevel = TraceLevel.valueOf(args[0]);

	try {
	    MyServer svr = new MyServer();
	    Class<?> c = svr.getClass();
	    Field f = c.getDeclaredField("level");
	    f.setAccessible(true);
	    TraceLevel oldLevel = (TraceLevel)f.get(svr);
	    out.format("Original trace level:  %s%n", oldLevel);

	    if (oldLevel != newLevel) {
 		f.set(svr, newLevel);
		out.format("    New  trace level:  %s%n", f.get(svr));
	    }

        // production code should handle these exceptions more gracefully
	} catch (IllegalArgumentException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	}
    }
}
```

由于枚举常量是单例的，`==`和`!=`操作符可以被用来比较相同类型的枚举常量。

$ *java SetTrace OFF*

```
Original trace level:  OFF
```

$ *java SetTrace DEBUG*

```
Original trace level:  OFF
New  trace level:  DEBUG
```

#### 故障排除

下面介绍在使用枚举类型时常见的错误。

**试图实例化枚举类型导致的 IllegalArgumentException**

如前面提到过的，实例化枚举类型是被禁止的。下面的例子试图这么干：

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import static java.lang.System.out;

enum Charge {
    POSITIVE, NEGATIVE, NEUTRAL;
    Charge() {
	out.format("under construction%n");
    }
}

public class EnumTrouble {

    public static void main(String... args) {
	try {
	    Class<?> c = Charge.class;

 	    Constructor[] ctors = c.getDeclaredConstructors();
 	    for (Constructor ctor : ctors) {
		out.format("Constructor: %s%n",  ctor.toGenericString());
 		ctor.setAccessible(true);
 		ctor.newInstance();
 	    }

        // production code should handle these exceptions more gracefully
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java EnumTrouble*

```
Constructor: private Charge()
Exception in thread "main" java.lang.IllegalArgumentException: Cannot
  reflectively create enum objects
        at java.lang.reflect.Constructor.newInstance(Constructor.java:511)
        at EnumTrouble.main(EnumTrouble.java:22)
```

------

**提示：**尝试显式实例化枚举是一个编译时错误，因为这会阻止定义的枚举常量是唯一的。这种限制也在反射代码中强制执行。尝试使用其默认构造函数实例化类的代码应首先调用 [`Class.isEnum()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isEnum--) 以确定该类是否为枚举。

------

**使用不兼容的枚举类型设定字段值导致的 IllegalArgumentException**

存储枚举的字段必须使用适当的枚举类型设置。（实际上，必须使用兼容类型设置任何类型的字段。）下面的示例会产生预期的错误。

```java
import java.lang.reflect.Field;

enum E0 { A, B }
enum E1 { A, B }

class ETest {
    private E0 fld = E0.A;
}

public class EnumTroubleToo {
    public static void main(String... args) {
	try {
	    ETest test = new ETest();
	    Field f = test.getClass().getDeclaredField("fld");
	    f.setAccessible(true);
 	    f.set(test, E1.A);  // IllegalArgumentException

        // production code should handle these exceptions more gracefully
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java EnumTroubleToo*

```
Exception in thread "main" java.lang.IllegalArgumentException: Can not set E0
  field ETest.fld to E1
        at sun.reflect.UnsafeFieldAccessorImpl.throwSetIllegalArgumentException
          (UnsafeFieldAccessorImpl.java:146)
        at sun.reflect.UnsafeFieldAccessorImpl.throwSetIllegalArgumentException
          (UnsafeFieldAccessorImpl.java:150)
        at sun.reflect.UnsafeObjectFieldAccessorImpl.set
          (UnsafeObjectFieldAccessorImpl.java:63)
        at java.lang.reflect.Field.set(Field.java:657)
        at EnumTroubleToo.main(EnumTroubleToo.java:16)
```

------

**提示：**严格地说，任何尝试将类型`X`的字段设置为类型`Y`的值只有在以下语句成立时才能成功：

```
X.class.isAssignableFrom（Y.class）== true
```

可以修改代码以执行以下测试以验证类型是否兼容：

```
if (f.getType().isAssignableFrom(E0.class))
    // compatible
else
    // expect IllegalArgumentException
```

------

