#### 通配符使用向导

学习使用泛型编程时，更令人困惑的一个方面是确定何时使用上界通配符以及何时使用下界通配符。此页面提供了设计代码时要遵循的一些准则。

出于本讨论的目的，将变量视为提供两个函数之一是有帮助的：

- **一个“in”变量**

  “in”变量向代码提供数据。想象一下带有两个参数的复制方法：`copy(src, dest)`。`src`参数提供要复制的数据，因此它是“in”参数。

- **一个“out”变量**

  “out”变量保存数据以供其他地方使用。在复制示例中，`copy(src, dest)`，`dest`参数接受数据，因此它是“out”参数。

当然，一些变量既用于“in”又用于“out”目的 - 这种情况也在指南中得到解决。

在决定是否使用通配符以及适合使用哪种类型的通配符时，可以使用“in”和“out”原则。以下列表提供了遵循的准则：

------

通配符指南：

 - 使用`extends`关键字定义带有上限通配符的“in”变量。
 - 使用`super`关键字定义带有下限通配符的“out”变量。
 - 如果可以使用`Object`类中定义的方法访问“in”变量，请使用无界通配符。
 - 如果代码需要作为“in”和“out”变量访问变量，请不要使用通配符。

------

这些指南不适用于方法的返回类型。应该避免使用通配符作为返回类型，因为它强制程序员使用代码来处理通配符。

 `List<? extends ...>` 可以被非正式地认为是只读的，但这不是一个严格的保证。假设您有以下两个类：

```java
class NaturalNumber {

    private int i;

    public NaturalNumber(int i) { this.i = i; }
    // ...
}

class EvenNumber extends NaturalNumber {

    public EvenNumber(int i) { super(i); }
    // ...
}
```

考虑如下代码：

```java
List<EvenNumber> le = new ArrayList<>();
List<? extends NaturalNumber> ln = le;
ln.add(new NaturalNumber(35));  // compile-time error
```

因为`List <EvenNumber>`是`List <? extends NaturalNumber>`，你可以将`le`赋给`ln`。但是你不能使用`ln`将自然数添加到偶数列表中。列表中的以下操作是可能的：

 - 您可以添加`null`。
 - 你可以调用`clear`。
 - 您可以获取迭代器并调用`remove`。
 - 您可以捕获通配符并写入从列表中读取的元素。

你可以看到 `List<? extends NaturalNumber>` 在严格意义上不是只读的，但您可能会这样想，因为您无法存储新元素或更改列表中的现有元素。

