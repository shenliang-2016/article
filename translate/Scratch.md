# 泛型

***by Gilad Bracha***

这个期待已久的类型系统增强版在 J2SE 5.0 中引入，允许类型或方法对各种类型的对象进行操作，同时提供编译时类型安全性。它为集合框架增加了编译时类型安全性，并消除了转型的苦差事。

- [介绍](https://docs.oracle.com/javase/tutorial/extra/generics/intro.html)
- [定义简单泛型](https://docs.oracle.com/javase/tutorial/extra/generics/simple.html)
- [泛型和子类型](https://docs.oracle.com/javase/tutorial/extra/generics/subtype.html)
- [通配符](https://docs.oracle.com/javase/tutorial/extra/generics/wildcards.html)
- [泛型方法](https://docs.oracle.com/javase/tutorial/extra/generics/methods.html)
- [与遗留代码的互操作](https://docs.oracle.com/javase/tutorial/extra/generics/legacy.html)
- [良好的打印](https://docs.oracle.com/javase/tutorial/extra/generics/fineprint.html)
- [类字面常量作为运行时类型符号](https://docs.oracle.com/javase/tutorial/extra/generics/literals.html)
- [通配符的更多用法](https://docs.oracle.com/javase/tutorial/extra/generics/morefun.html)
- [遗留代码适配泛型](https://docs.oracle.com/javase/tutorial/extra/generics/convert.html)
- [参考文献](https://docs.oracle.com/javase/tutorial/extra/generics/acknowledgements.html)

## 介绍

JDK 5.0 引入了若干新的扩展到 Java 编程语言中。其中之一是引入了*泛型*。

本课程介绍泛型。你可能熟悉其它语言中的类似结构，特别是 C++ 中的模板。如果是这样，你将看到它们之前的异同。如果你并不熟悉其它的类似结构，非常好，你可以从头开始，而且不会有任何错误概念的干扰。

泛型允许你在类型之上进行抽象。大部分的例子都是容器类型，比如那些集合框架体系结构中的类型。

下面是一个典型的排序应用：

```java
List myIntList = new LinkedList(); // 1
myIntList.add(new Integer(0)); // 2
Integer x = (Integer) myIntList.iterator().next(); // 3        
```

第三行的转型有点烦人。典型地，程序员直到放入特定列表中的具体是什么类型的数据。然而，转型是基础的。编译器只能保证迭代器返回`Object` 。为了保证为`Integer` 变量的赋值是类型安全的，就必须转型。

当然，这种转型同时也引入了干扰。他同时引入了运行时错误的可能性，因为程序员可能会犯错误。

程序员如何才能实际表达他们的意图，将一个列表标记为只能包含特定类型的数据？这是泛型背后的核心目标。下面这个代码片段使用泛型做到这一点：

```java
List<Integer> 
    myIntList = new LinkedList<Integer>(); // 1'
myIntList.add(new Integer(0)); // 2'
Integer x = myIntList.iterator().next(); // 3'
```

注意，变量`myIntList` 的类型声明。它表明这不仅仅是一个任意的`List` ，而是一个`Integer`的`List`，写做`List<Integer>`。我们说该`List`是一个泛型接口，携带了类型参数。这种情况下，类型参数是`Integer`。我们通常也会在创建列表对象时指定一个类型参数。

同时，注意第三行代码中的转型没有了。

现在，你可能认为我们所做的就是绕过了干扰。相对于在第三行中将数据转型为`Integer` ，我们现在将`Integer` 作为第一行代码中的类型参数。不过，这里仍然有个显著不同。编译器现在可以在编译期检查程序的类型正确性。当我们说`myIntList` 被使用类型`List<Integer>` 声明时，这告诉我们有关变量`myIntlist` 的一些信息，无论在何时何处使用该变量，编译器将保证这些信息始终为 `true` 。相对而言，转型告诉我们的信息只是程序员认为在那个代码处这个信息是真的。

泛型的单纯的好处，特别是在大型程序中，显著提高了代码可读性和鲁棒性。

## 定义简单泛型

这里是 `java.util` 包中的 `List` 和 `Iterator` 接口定义中的片段：

```java
public interface List <E> {
    void add(E x);
    Iterator<E> iterator();
}

public interface Iterator<E> {
    E next();
    boolean hasNext();
}
```

这些代码你应该很熟悉，除了其中的大括号。那些大括号是接口 `List` 和 `Iterator` 的*形式类型参数*声明。

类型参数可以被使用在泛型声明中的各处，基本上就是你使用普通类型的位置（尽管存在一些特殊限制，参考 [The Fine Print](https://docs.oracle.com/javase/tutorial/extra/generics/fineprint.html) ）。

本章节中，我们看到泛型类型声明 `List` 的*调用*，比如 `List<Integer>` 。在该调用中（通常称为*参数化类型*），所有出现的形式类型参数（例子中的 `E`）都会被*实际类型参数*（例子中的 `Integer`）替换。

你可以将 `List<Integer>` 想象为 `List` 的一个特殊版本，其中的 `E` 会被 `Integer` 统一替换：

```java
public interface IntegerList {
    void add(Integer x);
    Iterator<Integer> iterator();
}
```

这种直觉可能会有助于理解，但是也可能导致误解。

它是有用的，因为参数化类型 `List<Integer>` 确实具有类似这种扩展的方法。

它具有误导性，因为泛型声明永远不会以这种方式扩展。不能存在代码副本，源代码、二进制文件、磁盘以及内存中都没有。如果你是一个 C++ 程序员，你讲理解这一点显然不同于 C++ 模板。

反省类型声明一次性编译，并转化为单个类文件，就像其他普通的类或者接口声明。

类型参数类似于方法或构造函数中使用的普通参数。就像方法具有描述其操作的值的种类的形式值参数一样，泛型声明具有形式类型参数。调用方法时，将使用实际参数替换形式参数，并评估方法体。调用泛型声明时，实际的类型参数将替换形式类型参数。

关于命名约定的说明。我们建议您使用简洁（单个字符，如果可能）但令人回味的名称为形式类型参数。最好避免使用小写字符，这样可以很容易地将形式类型参数与普通类和接口区分开来。许多容器类型使用 `E` 作为元素，如上例所示。我们将在后面的示例中看到一些其他约定。

## 泛型和子类型

让我们来测试一下你对泛型的理解。下面的代码合法吗？

```java
List<String> ls = new ArrayList<String>(); // 1
List<Object> lo = ls; // 2 
```

第一行自然是合法的。有问题的部分是第二行。归结起来的根本问题是：一个 `String` 的 `List` 究竟是不是一个 `Object` 的 `List` ？大多数人直觉的答案是：“当然是！”

好的，继续看接下来几行代码：

```java
lo.add(new Object()); // 3
String s = ls.get(0); // 4: Attempts to assign an Object to a String!
```

此时，我们已经创建了 `ls` 和一个它的别名 `lo` 。通过别名 `lo` 访问 `ls` ，一个 `String` 列表。我们可以将任意对象插入该列表。作为结果，`ls` 不在仅仅包含 `String` ，然后当我们试图从其中获取数据时，我们就会遇到问题。

Java 编译器当然将阻止这一切的发生。第二行代码将会导致一个编译期错误。

通常，如果 `Foo` 是一个 `Bar` 的子类型（子类或者子接口），同时 `G` 是泛型类型声明，那么 `G<Foo>` 并不是 `G<Bar>` 的子类。这一点可能是你需要理解的泛型概念中最难的部分，因为这一点显然不同于我们的直觉。

我们不应该假定集合不会发生变化。我们的直觉会误导我们认为这些东西是不可变的。

比如，如果汽车供应商向人口普查部门提供司机清单，这看起来是合理的。我们认为 `List<Driver` 是一个 `List<Person>` ，假定 `Driver` 是 `Person` 的子类型。事实上，被传递的是司机注册表的副本。否则，人口普查部门可以将不是司机的人员添加到司机注册表中，破坏了 DMV 的记录。

为了处理这种排序情况，考虑更加灵活的泛型类型是有用的。到目前为止我们看到的规则是相当严格的。

