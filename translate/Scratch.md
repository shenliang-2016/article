#### 下界通配符

[上界通配符](https://docs.oracle.com/javase/tutorial/java/generics/upperBounded.html) 章节展示上界通配符约束未知类型是使用`extends`关键字表示的特定类型或者特定类型的子类型。类似的，下界通配符约束未知类型为特定类型或者特定类型的超类。

下界通配符使用通配符'`?`'表示，后面跟随 `super` 关键字，随后是它的下界：`<? super A>` 。

------

**注意：** 你可以为一个通配符指定上界或者下界，但是不能同时指定两者。

------

假设您要编写一个将`Integer`对象放入列表的方法。为了最大限度地提高灵活性，您希望该方法可以处理`List <Integer>`，`List <Number>`和`List <Object> ` - 任何可以保存`Integer`值的方法。

要编写适用于`Integer`列表和`Integer`超类型的方法，例如`Integer`，`Number`和`Object`，您可以指定`List<? super Integer>`。`List <Integer>`一词比`List<? super Integer>`更具限制性。因为前者仅匹配`Integer`类型的列表，而后者匹配任何类型为`Integer`的超类型的列表。

以下代码将数字1到10添加到列表的末尾：

```java
public static void addNumbers(List<? super Integer> list) {
    for (int i = 1; i <= 10; i++) {
        list.add(i);
    }
}
```

[通配符使用向导](https://docs.oracle.com/javase/tutorial/java/generics/wildcardGuidelines.html) 章节介绍了上界通配符和下界通配符的使用时机。

#### 通配符和子类型化

如 [泛型，继承以及子类型化](https://docs.oracle.com/javase/tutorial/java/generics/inheritance.html) 中所述，泛型类后者泛型接口之间不仅仅通过类型相关联。不过，你可以使用通配符在泛型类或者接口之间建立某种关系。

给定下面两个普通的非泛型类：

```java
class A { /* ... */ }
class B extends A { /* ... */ }
```

编写下面的代码是合理的：

```java
B b = new B();
A a = b;
```

此示例显示常规类的继承遵循此子类型规则：如果B扩展A，则类B是类A的子类型。此规则不适用于泛型类型：

```java
List<B> lb = new ArrayList<>();
List<A> la = lb;   // compile-time error
```

鉴于`Integer`是`Number`的子类型，`List <Integer>`和`List <Number>`之间的关系是什么？

![diagram showing that the common parent of List<Number> and List<Integer> is the list of unknown type](https://docs.oracle.com/javase/tutorial/figures/java/generics-listParent.gif)

公共父类是List <?>。

尽管`Integer`是`Number`的子类型，但`List <Integer>`不是`List <Number>`的子类型，实际上，这两种类型不相关。`List <Number>`和`List <Integer>`的公共父类是List <?>。

为了在这些类之间创建关系以便代码可以通过`List <Integer>`的元素访问`Number`的方法，请使用上限的通配符：

```java
List<? extends Integer> intList = new ArrayList<>();
List<? extends Number>  numList = intList;  // OK. List<? extends Integer> is a subtype of List<? extends Number>
```

因为`Integer`是`Number`的子类型，而`numList`是`Number`对象的列表，所以`intList`（`Integer`对象列表）和`numList`之间现在存在关系。下图显示了使用上限和下限通配符声明的多个`List`类之间的关系。

![diagram showing that List<Integer> is a subtype of both List<? extends Integer> and List<?super Integer>. List<? extends Integer> is a subtype of List<? extends Number> which is a subtype of List<?>. List<Number> is a subtype of List<? super Number> and List>? extends Number>. List<? super Number> is a subtype of List<? super Integer> which is a subtype of List<?>.](https://docs.oracle.com/javase/tutorial/figures/java/generics-wildcardSubtyping.gif)

几个通用`List`类声明的层次结构。

[通配符使用向导](https://docs.oracle.com/javase/tutorial/java/generics/wildcardGuidelines.html) 章节介绍了上界通配符和下界通配符的使用效果。

#### 通配符捕获和帮助方法

某些情况下，编译器推断通配符的类型。比如，一个列表可以定义为`List<?>`，但是，当计算一个表达式时，编译器从代码推断特定类型。该场景被称为*通配符捕获*。

大部分情况下，你不需要担心通配符捕获，除非你看到包含 "capture of" 的错误消息。

[`WildcardError`](https://docs.oracle.com/javase/tutorial/java/generics/examples/WildcardError.java) 例子在编译时产生捕获错误：

```java
import java.util.List;

public class WildcardError {

    void foo(List<?> i) {
        i.set(0, i.get(0));
    }
}
```

在此示例中，编译器将`i`输入参数处理为`Object`类型。当`foo`方法调用 [List.set(int, E)](https://docs.oracle.com/javase/8/docs/api/java/util/List.html#set-int-E-) 时，编译器无法确认插入到列表中的对象的类型，并产生错误。发生此类错误时，通常意味着编译器认为您为变量分配了错误的类型。由于这个原因，泛型被添加到Java语言中 - 在编译时强制类型安全。

由 Oracle 的 JDK 7 `javac`实现编译时，`WildcardError`示例生成以下错误：

```shell
WildcardError.java:6: error: method set in interface List<E> cannot be applied to given types;
    i.set(0, i.get(0));
     ^
  required: int,CAP#1
  found: int,Object
  reason: actual argument Object cannot be converted to CAP#1 by method invocation conversion
  where E is a type-variable:
    E extends Object declared in interface List
  where CAP#1 is a fresh type-variable:
    CAP#1 extends Object from capture of ?
1 error
```

在此示例中，代码尝试执行安全操作，那么如何解决编译器错误？ 您可以通过编写捕获通配符的私有帮助程序方法来解决它。在这种情况下，您可以通过创建私有帮助器方法`fooHelper`来解决此问题，如`WildcardFixed`中所示：

```java
public class WildcardFixed {

    void foo(List<?> i) {
        fooHelper(i);
    }


    // Helper method created so that the wildcard can be captured
    // through type inference.
    private <T> void fooHelper(List<T> l) {
        l.set(0, l.get(0));
    }

}
```

在辅助方法帮助下，编译器使用推断来确定调用中T是CAP＃1（捕获变量）。该示例现在已成功编译。

按照惯例，辅助方法通常命名为`*originalMethodName*Helper`。

现在考虑一个更复杂的例子， [`WildcardErrorBad`](https://docs.oracle.com/javase/tutorial/java/generics/examples/WildcardErrorBad.java)：

```java
import java.util.List;

public class WildcardErrorBad {

    void swapFirst(List<? extends Number> l1, List<? extends Number> l2) {
      Number temp = l1.get(0);
      l1.set(0, l2.get(0)); // expected a CAP#1 extends Number,
                            // got a CAP#2 extends Number;
                            // same bound, but different types
      l2.set(0, temp);	    // expected a CAP#1 extends Number,
                            // got a Number
    }
}
```

在此示例中，代码尝试进行不安全的操作。例如，考虑以下对`swapFirst`方法的调用：

```java
List<Integer> li = Arrays.asList(1, 2, 3);
List<Double>  ld = Arrays.asList(10.10, 20.20, 30.30);
swapFirst(li, ld);
```

`List <Integer>`和`List <Double>`都符合`List <？extends Number>`，从`Integer`值列表中取一个项目并尝试将其放入`Double`值列表中显然是不正确的。

使用Oracle的JDK `javac`编译器编译代码会产生以下错误：

```shell
WildcardErrorBad.java:7: error: method set in interface List<E> cannot be applied to given types;
      l1.set(0, l2.get(0)); // expected a CAP#1 extends Number,
        ^
  required: int,CAP#1
  found: int,Number
  reason: actual argument Number cannot be converted to CAP#1 by method invocation conversion
  where E is a type-variable:
    E extends Object declared in interface List
  where CAP#1 is a fresh type-variable:
    CAP#1 extends Number from capture of ? extends Number
WildcardErrorBad.java:10: error: method set in interface List<E> cannot be applied to given types;
      l2.set(0, temp);      // expected a CAP#1 extends Number,
        ^
  required: int,CAP#1
  found: int,Number
  reason: actual argument Number cannot be converted to CAP#1 by method invocation conversion
  where E is a type-variable:
    E extends Object declared in interface List
  where CAP#1 is a fresh type-variable:
    CAP#1 extends Number from capture of ? extends Number
WildcardErrorBad.java:15: error: method set in interface List<E> cannot be applied to given types;
        i.set(0, i.get(0));
         ^
  required: int,CAP#1
  found: int,Object
  reason: actual argument Object cannot be converted to CAP#1 by method invocation conversion
  where E is a type-variable:
    E extends Object declared in interface List
  where CAP#1 is a fresh type-variable:
    CAP#1 extends Object from capture of ?
3 errors
```

没有帮助方法来解决这个问题，因为代码根本就是错误的。