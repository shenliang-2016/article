#### 原始类型

*原始类型*是没有任何类型参数的泛型类或者泛型接口。比如，给定泛型 `Box` 类：

```java
public class Box<T> {
    public void set(T t) { /* ... */ }
    // ...
}
```

为了创建一个参数化类型 `Box<T>`，你给出一个实际的类型参数来取代先前的类型参数 `T`：

```java
Box<Integer> intBox = new Box<>();
```

如果实际类型参数被忽略，你就会创建一个原始类型 `Box<T>`：

```java
Box rawBox = new Box();
```

也就是说， `Box` 是泛型类型 `Box<T>`的原始类型。不过，一个非泛型类或者接口类型不是原始类型。

原始类型出现在遗留代码中，因为大量 API 类，比如`Collections`类，编写的年代还没有引入泛型。当使用原始类型时，你实际上得到的是泛型出现之前的行为 - 一个`Box`会返回给你一个`Object`。为了保持向后兼容性，将一个参数化类型赋值给它的原始类型是允许的：

```java
Box<String> stringBox = new Box<>();
Box rawBox = stringBox;               // OK
```

但是，如果你赋值一个原始类型给一个参数化类型，你将得到一个警告：

```java
Box rawBox = new Box();           // rawBox is a raw type of Box<T>
Box<Integer> intBox = rawBox;     // warning: unchecked conversion
```

当你使用一个原始类型来调用对应的泛型类型定义的泛型方法是，你也会得到一个警告：

```java
Box<String> stringBox = new Box<>();
Box rawBox = stringBox;
rawBox.set(8);  // warning: unchecked invocation to set(T)
```

警告表明该原始类型绕过了泛型类型检查，将不安全代码捕获推迟到了运行时。因此，你应该避免使用原始类型。

[类型擦除](https://docs.oracle.com/javase/tutorial/java/generics/erasure.html) 章节包含更多有关 Java 编译器使用原始类型的信息。

**不受检查的错误信息**

如前所述，当混合使用遗留代码和泛型代码时，你可能会遇到类似下面的警告消息：

```shell
Note: Example.java uses unchecked or unsafe operations.
Note: Recompile with -Xlint:unchecked for details.
```

这些可能发生在使用老的使用原始类型的 API 时，如下面例子所示：

```java
public class WarningDemo {
    public static void main(String[] args){
        Box<Integer> bi;
        bi = createBox();
    }

    static Box createBox(){
        return new Box();
    }
}
```

术语“unchecked”表示编译器没有足够的类型信息来执行确保类型安全所必需的所有类型检查。默认情下，“unchecked”警告被禁用，尽管编译器提供了提示。要查看所有“unchecked”警告，请使用`-Xlint：unchecked`重新编译。

使用`-Xlint：unchecked`重新编译前一个示例会显示以下附加信息：

```shell
WarningDemo.java:4: warning: [unchecked] unchecked conversion
found   : Box
required: Box<java.lang.Integer>
        bi = createBox();
                      ^
1 warning
```

要完全禁用未检查的警告，请使用`-Xlint：-unchecked`标志。`@SuppressWarnings`（“unchecked”）注解会抑制未经检查的警告。如果您不熟悉`@SuppressWarnings`语法，请参阅 [注解](https://docs.oracle.com/javase/tutorial/java/annotations/index.html) 。

### 泛型方法

*泛型方法*是引入它们自己的类型参数的方法。这类似于声明泛型类型，但类型参数的范围仅限于声明它的方法。允许使用静态和非静态泛型方法，以及泛型类构造函数。

泛型方法的语法包括一个类型参数列表，在尖括号内，它出现在方法的返回类型之前。对于静态泛型方法，类型参数部分必须出现在方法的返回类型之前。

`Util`类包含一个泛型方法`compare`，它比较两个`Pair`对象：

```java
public class Util {
    public static <K, V> boolean compare(Pair<K, V> p1, Pair<K, V> p2) {
        return p1.getKey().equals(p2.getKey()) &&
               p1.getValue().equals(p2.getValue());
    }
}

public class Pair<K, V> {

    private K key;
    private V value;

    public Pair(K key, V value) {
        this.key = key;
        this.value = value;
    }

    public void setKey(K key) { this.key = key; }
    public void setValue(V value) { this.value = value; }
    public K getKey()   { return key; }
    public V getValue() { return value; }
}
```

调用该方法的完整语法：

```java
Pair<Integer, String> p1 = new Pair<>(1, "apple");
Pair<Integer, String> p2 = new Pair<>(2, "pear");
boolean same = Util.<Integer, String>compare(p1, p2);
```

代码中已明确提供类型，如粗体所示。通常，这可以省略，编译器将推断所需的类型：

```java
Pair<Integer, String> p1 = new Pair<>(1, "apple");
Pair<Integer, String> p2 = new Pair<>(2, "pear");
boolean same = Util.compare(p1, p2);
```

此功能称为*类型推断*，允许您将泛型方法作为普通方法调用，而无需在尖括号之间指定类型。本主题将在下一节 [类型推断](https://docs.oracle.com/javase/tutorial/java/generics/genTypeInference.html) 中进一步讨论。

