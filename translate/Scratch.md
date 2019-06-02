### 泛型，继承和子类型

如您所知，只要类型兼容，就可以将一种类型的对象分配给另一种类型的对象。例如，您可以将`Integer`对象分配给`Object`，因为`Object`是`Integer`的超类型之一：

```java
Object someObject = new Object();
Integer someInteger = new Integer(10);
someObject = someInteger;   // OK
```

在面向对象的术语中，这被称为“is a”关系。由于`Integer` *是*一种`Object`，因此允许赋值。但是`Integer`也是一种`Number`，所以下面的代码也是有效的：

```java
public void someMethod(Number n) { /* ... */ }

someMethod(new Integer(10));   // OK
someMethod(new Double(10.1));   // OK
```

泛型也是如此。您可以执行泛型类型调用，将`Number`作为其类型参数传递，如果参数与`Number`兼容，则允许任何后续的`add`调用：

```java
Box<Number> box = new Box<Number>();
box.add(new Integer(10));   // OK
box.add(new Double(10.1));  // OK
```

现在考虑下面的方法：

```java
public void boxTest(Box<Number> n) { /* ... */ }
```

它接受什么类型的参数？ 通过查看其签名，您可以看到它接受一个类型为`Box <Number>`的参数。但是，这是什么意思？ 您是否允许传递`Box <Integer>`或`Box <Double>`，如您所料？ 答案是“不”，因为`Box <Integer>`和`Box <Double>`不是`Box <Number>`的子类型。

在使用泛型编程时，这是一个常见的误解，但这是一个需要学习的重要概念。

![diagram showing that Box<Integer> is not a subtype of Box<Number>](https://docs.oracle.com/javase/tutorial/figures/java/generics-subtypeRelationship.gif)

`Box<Integer>` 不是 `Box<Number>` 的子类型，尽管 `Integer` 是 `Number`的子类型。

------

**注意：**给定两个具体类型`A`和`B`（例如，`Number`和`Integer`），`MyClass <A>`与`MyClass <B>`无关，无论`A`和`B`是否相关。`MyClass <A>`和`MyClass <B>`的公共父类是`Object`。

有关如何在类型参数相关时在两个泛型类之间创建类似子类型关系的信息，请参阅 [通配符和子类型](https://docs.oracle.com/javase/tutorial/java/generics/subtyping.html) 。

------

**泛型类和子类化**

您可以通过扩展或实现通用类或接口来对其进行子类型化。一个类或接口的类型参数与另一个类的类型参数之间的关系由`extends`和`implements`子句决定。

使用`Collections`类作为例子，`ArrayList <E>`实现`List <E>`，`List <E>扩展Collection <E>`。 所以`ArrayList <String>`是`List <String>`的子类型，它是`Collection <String>`的子类型。只要不改变类型参数，就会在类型之间保留子类型关系。

![diagram showing a sample collections hierarchy: ArrayList<String> is a subtype of List<String>, which is a subtype of Collection<String>.](https://docs.oracle.com/javase/tutorial/figures/java/generics-sampleHierarchy.gif)

现在假设我们想要定义我们自己的列表接口`PayloadList`，它将泛型类型`P`的可选值与每个元素相关联。它的声明可能如下：

```java
interface PayloadList<E,P> extends List<E> {
  void setPayload(int index, P val);
  ...
}
```

`PayloadList`的以下参数化是`List <String>`的子类型：

- `PayloadList<String,String>`
- `PayloadList<String,Integer>`
- `PayloadList<String,Exception>`

![diagram showing an example PayLoadList hierarchy: PayloadList<String, String> is a subtype of List<String>, which is a subtype of Collection<String>. At the same level of PayloadList<String,String> is PayloadList<String, Integer> and PayloadList<String, Exceptions>.](https://docs.oracle.com/javase/tutorial/figures/java/generics-payloadListHierarchy.gif)

