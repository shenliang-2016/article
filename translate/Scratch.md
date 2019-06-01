**类型参数命名约定**

按照约定，类型参数名称应该是单个的大写字母。这一点与你所知道的变量的命名完全不同，不过理由很充分：如果不这么约定，就很难区分类型变量和原始的类或者接口名称。

最常用的类型参数名称有：

* E - Element（在 Java 集合框架中广泛应用）
* K - Key
* N - Number
* T - Type
* V - Value
* S, U, V etc - 第二、第三、第四类型

你将看到这些名称贯穿整个 Java SE API 和本文的剩余章节。

**调用及实例化泛型类型**

为了引用你的代码中的泛型`Box`类，你必须执行一个*泛型类型调用*，该调用将使用某种具体类型替换 `T` ，比如 `Integer`：

```java
Box<Integer> integerBox;
```

您可以将泛型类型调用视为与普通方法调用类似，但不是将参数传递给方法，而是将*类型参数*  - `Integer`在这种情况下传递给`Box`类本身。

------

`Type Parameter`和`Type Argument`术语：

  许多开发人员可以互换地使用术语`Type Parameter`和`Type Argument`，但这些术语并不相同。编码时，提供`Type Parameter`以创建参数化类型。 因此，`Foo <T>`中的`T`是一个`Type Parameter`，而`Foo <String> f`中的`String`是一个类`Type Argument`。本课程在使用这些术语时会遵循此定义。

------

与任何其他变量声明一样，此代码实际上并不创建新的`Box`对象。它只是声明`integerBox`将保存对`Integer`的`Box`的引用，这就是`Box <Integer>`的含义。

泛型类型的调用通常称为*参数化类型*。

要实例化这个类，像往常一样使用`new`关键字，但在类名和括号之间放置`<Integer>`：

```java
Box<Integer> integerBox = new Box<Integer>();
```

**菱形表示法**

在Java SE 7及更高版本中，只要编译器可以从上下文中确定或推断类型参数，就可以用一组空的类型参数（<>）替换调用泛型类的构造函数所需的类型参数。这对尖括号`<>`非正式地称为*菱形表示法*。例如，您可以使用以下语句创建`Box <Integer>`的实例：

````java
Box<Integer> integerBox = new Box<>();
````

有关菱形表示法和类型推断的更多信息，请参阅 [Type Inference](https://docs.oracle.com/javase/tutorial/java/generics/genTypeInference.html) 。

**多个类型参数**

如前所述，一个泛型 类型可以拥有多个类型参数，如下面例子：

````java
public interface Pair<K, V> {
    public K getKey();
    public V getValue();
}

public class OrderedPair<K, V> implements Pair<K, V> {

    private K key;
    private V value;

    public OrderedPair(K key, V value) {
	this.key = key;
	this.value = value;
    }

    public K getKey()	{ return key; }
    public V getValue() { return value; }
}
````

下面的两条语句创建两个`OrderedPair`类对象实例：

````java
Pair<String, Integer> p1 = new OrderedPair<String, Integer>("Even", 8);
Pair<String, String>  p2 = new OrderedPair<String, String>("hello", "world");
````

代码 `new OrderedPair<String, Integer>`，实例化 `K` 作为一个 `String` 对象， `V` 作为一个 `Integer`对象。因此， `OrderedPair`的构造器的参数类型就是 `String` 和 `Integer`。由于 [自动装箱](https://docs.oracle.com/javase/tutorial/java/data/autoboxing.html) 机制，传递 `String` 和 `int` 给该类也是合法的。

如 [菱形表示法](https://docs.oracle.com/javase/tutorial/java/generics/types.html#diamond) 中所述，由于 Java 编译器能够从 `OrderedPair<String, Integer>` 声明推断出 `K` 和 `V` 的类型，使用菱形表示法将上述语句简化为：

```java
OrderedPair<String, Integer> p1 = new OrderedPair<>("Even", 8);
OrderedPair<String, String>  p2 = new OrderedPair<>("hello", "world");
```

创建泛型接口的约定和创建泛型类的约定一样。

**参数化类型**

您还可以用参数化类型（即`List <String>`）替换类型参数（即`K`或`V`）。例如，使用`OrderedPair <K，V>`示例：

```java
OrderedPair<String, Box<Integer>> p = new OrderedPair<>("primes", new Box<Integer>(...));
```

