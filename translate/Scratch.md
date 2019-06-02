### 有界的类型参数

有时您可能希望限制可用作参数化类型中的类型参数的类型。例如，对数字进行操作的方法可能只想接受`Number`或其子类的实例。这是*有界类型参数*的用途。

要声明有界类型参数，请列出类型参数的名称，后跟`extends`关键字，后跟*上限*，在此示例中为`Number`。注意，在这种情况下，`extends`在一般意义上用于表示“扩展”（如在类中）或“实现”（如在接口中）。

```java
public class Box<T> {

    private T t;          

    public void set(T t) {
        this.t = t;
    }

    public T get() {
        return t;
    }

    public <U extends Number> void inspect(U u){
        System.out.println("T: " + t.getClass().getName());
        System.out.println("U: " + u.getClass().getName());
    }

    public static void main(String[] args) {
        Box<Integer> integerBox = new Box<Integer>();
        integerBox.set(new Integer(10));
        integerBox.inspect("some text"); // error: this is still String!
    }
}
```

通过修改我们的泛型方法来包含这个有界类型参数，编译现在将失败，因为我们调用`inspect`仍然包含一个`String`：

```shell
Box.java:21: <U>inspect(U) in Box<java.lang.Integer> cannot
  be applied to (java.lang.String)
                        integerBox.inspect("10");
                                  ^
1 error
```

除了限制可用于实例化泛型类型的类型之外，有界类型参数还允许您调用边界中定义的方法：

```java
public class NaturalNumber<T extends Integer> {

    private T n;

    public NaturalNumber(T n)  { this.n = n; }

    public boolean isEven() {
        return n.intValue() % 2 == 0;
    }

    // ...
}
```

`isEven`方法通过`n`调用`Integer`类中定义的`intValue`方法。

**多个边界**

前面的示例说明了使用带有单个边界的类型参数，但是类型参数可以具有*多个边界*：

```java
<T extends B1 & B2 & B3>
```

具有多个边界的类型变量是边界中列出的所有类型的子类型。如果其中一个边界是类，则必须首先指定它。 例如：

```java
Class A { /* ... */ }
interface B { /* ... */ }
interface C { /* ... */ }

class D <T extends A & B & C> { /* ... */ }
```

如果未首先指定边界中的`A`，则会出现编译时错误：

```java
class D <T extends B & A & C> { /* ... */ }  // compile-time error
```

#### 泛型方法和有界类型参数

有界类型参数是泛型算法实现的关键。考虑以下方法来计算数组`T[]`中大于指定元素`elem`的元素数。

```java
public static <T> int countGreaterThan(T[] anArray, T elem) {
    int count = 0;
    for (T e : anArray)
        if (e > elem)  // compiler error
            ++count;
    return count;
}
```

该方法的实现很简单，但它不能编译，因为大于运算符（`>`）仅适用于基本数据类型，如`short`，`int`，`double`，`long`，`float`， `byte`和`char`。你不能使用`>`运算符来比较对象。要解决此问题，请使用由`Comparable <T>`接口限定的类型参数：

```java
public interface Comparable<T> {
    public int compareTo(T o);
}
```

代码的结果将是：

```java
public static <T extends Comparable<T>> int countGreaterThan(T[] anArray, T elem) {
    int count = 0;
    for (T e : anArray)
        if (e.compareTo(elem) > 0)
            ++count;
    return count;
}
```