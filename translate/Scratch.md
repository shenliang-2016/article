### 类型推断

类型推断是 Java 编译器的一种能力，通过检查每个方法调用以及相应的方法声明来确定可应用于方法调用的类型参数。该推断算法确定参数的类型，如果可能，结果被赋值的类型，或者返回值类型。最后，类型推断算法尝试找出所有参数的最精确的类型。

下面的例子说明了上面这一点，类型推断确定传递给`pick`方法的第二个参数是`Serializable`类型：

```java
static <T> T pick(T a1, T a2) { return a2; }
Serializable s = pick("d", new ArrayList<String>());
```

**类型推断和泛型方法**

[泛型方法](https://docs.oracle.com/javase/tutorial/java/generics/methods.html) 向你介绍了类型推断，它使得你可以像调用普通方法那样调用泛型方法，而不需要使用尖括号说明类型参数。考虑下面的例子[`BoxDemo`](https://docs.oracle.com/javase/tutorial/java/generics/examples/BoxDemo.java)，需要 [`Box`](https://docs.oracle.com/javase/tutorial/java/generics/examples/Box.java) 类：

```java
public class BoxDemo {

  public static <U> void addBox(U u, 
      java.util.List<Box<U>> boxes) {
    Box<U> box = new Box<>();
    box.set(u);
    boxes.add(box);
  }

  public static <U> void outputBoxes(java.util.List<Box<U>> boxes) {
    int counter = 0;
    for (Box<U> box: boxes) {
      U boxContents = box.get();
      System.out.println("Box #" + counter + " contains [" +
             boxContents.toString() + "]");
      counter++;
    }
  }

  public static void main(String[] args) {
    java.util.ArrayList<Box<Integer>> listOfIntegerBoxes =
      new java.util.ArrayList<>();
    BoxDemo.<Integer>addBox(Integer.valueOf(10), listOfIntegerBoxes);
    BoxDemo.addBox(Integer.valueOf(20), listOfIntegerBoxes);
    BoxDemo.addBox(Integer.valueOf(30), listOfIntegerBoxes);
    BoxDemo.outputBoxes(listOfIntegerBoxes);
  }
}
```

程序输出：

```shell
Box #0 contains [10]
Box #1 contains [20]
Box #2 contains [30]
```

泛型方法`addBox`定义了一个名为`u`的类型参数。一般地，Java 编译器可以推断泛型方法调用的类型参数。因此，大部分情况下，你不需要指定它们。比如，为了调用泛型方法`addBox`，你可以随着一个类型*见证者*指定类型参数，如下所示：

```java
BoxDemo.<Integer>addBox(Integer.valueOf(10), listOfIntegerBoxes);
```

不过，如果你忽略该类型见证者，Java 编译器将会自动推断出类型参数是`Integer`：

```java
BoxDemo.addBox(Integer.valueOf(20), listOfIntegerBoxes);
```

**类型推断和泛型类实例化**

由于编译器可以从上下文中推断出类型参数，你就可以在调用泛型类的构造方法时使用空的类型参数列表 `<>`。这个空的尖括号被称为 [菱形表示法](https://docs.oracle.com/javase/tutorial/java/generics/types.html#diamond) 。

例如，考虑下面的变量声明：

```java
Map<String, List<String>> myMap = new HashMap<String, List<String>>();
```

您可以使用一组空的类型参数（<>）替换构造函数的参数化类型：

```java
Map<String, List<String>> myMap = new HashMap<>();
```

请注意，要在泛型类实例化期间利用类型推断，必须使用菱形表示法。在以下示例中，编译器生成未经检查的转换警告，因为`HashMap()`构造函数引用`HashMap`原始类型，而不是`Map <String，List <String >>`类型：

```java
Map<String, List<String>> myMap = new HashMap(); // unchecked conversion warning
```

**类型推断与泛型类或者非泛型类的泛型构造方法**

请注意，构造函数在泛型和非泛型类中都可以是通用的（换句话说，声明它们自己的形式类型参数）。请考虑以下示例：

```java
class MyClass<X> {
  <T> MyClass(T t) {
    // ...
  }
}
```

考虑下面的`MyClass`类的实例化：

```java
new MyClass<Integer>("")
```

此语句创建参数化类型`MyClass <Integer>`的实例；该语句显式指定泛型类`MyClass <X>`的形式类型参数`X`的类型`Integer`。请注意，此泛型类的构造函数包含一个正式的类型参数`T` 。编译器推断出此泛型类的构造函数的形式类型参数`T`的类型`String`（因为此构造函数的实际参数是`String`对象）。

Java SE 7之前版本的编译器能够推断泛型构造函数的实际类型参数，类似于泛型方法。但是，如果使用菱形表示法`<>`，Java SE 7及更高版本中的编译器可以推断出要实例化的泛型类的实际类型参数。请考虑以下示例：

```java
MyClass<Integer> myObject = new MyClass<>("");
```

在此示例中，编译器为通用类`MyClass <X>`的形式类型参数`X`推断类型`Integer`。它推断出此泛型类的构造函数的形式类型参数`T`的类型`String`。

------

**注意：** 要注意推理算法仅使用调用参数，目标类型，并且可能使用明显的预期返回类型来推断类型。推理算法不使用程序中稍后的结果。

------

**目标类型**

Java编译器利用目标类型来推断泛型方法调用的类型参数。表达式的目标类型是Java编译器所期望的数据类型，具体取决于表达式的出现位置。考虑方法`Collections.emptyList`，声明如下：

```java
static <T> List<T> emptyList();
```

考虑下面的赋值语句：

```java
List<String> listOne = Collections.emptyList();
```

此语句需要`List <String>`的实例；此数据类型是目标类型。因为方法`emptyList`返回`List <T>`类型的值，所以编译器推断类型参数`T`必须是`String`值。这适用于Java SE 7和8。或者，您可以使用类型见证并指定`T`的值，如下所示：

```java
List<String> listOne = Collections.<String>emptyList();
```

不过，这样做在当前上下文中是不必要的。它在其它上下文中是必要的。考虑如下方法：

```java
void processStringList(List<String> stringList) {
    // process stringList
}
```

假设您要使用空列表调用方法`processStringList`。 在Java SE 7中，以下语句不能通过编译：

```java
processStringList(Collections.emptyList());
```

Java SE 7 编译器产生类似下面的错误信息：

```shell
List<Object> cannot be converted to List<String>
```

编译器需要类型参数`T`的值，因此它以`Object`值开头。因此，`Collections.emptyList`的调用返回`List <Object>`类型的值，该值与方法`processStringList`不兼容。因此，在Java SE 7中，您必须指定类型参数，如下所示：

```java
processStringList(Collections.<String>emptyList());
```

Java SE 8中不再需要这样。目标类型的概念已经扩展为包含方法参数，例如方法`processStringList`的参数。在这种情况下，`processStringList`需要一个`List <String>`类型的参数。方法`Collections.emptyList`返回`List <T>`的值，因此使用`List <String>`的目标类型，编译器推断类型参数`T`的值为`String`。因此，在Java SE 8中，以下语句可以通过编译：

```java
processStringList(Collections.emptyList());
```

参考 [Lambda 表达式](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html) 中的 [目标类型](https://docs.oracle.com/javase/tutorial/java/javaOO/lambdaexpressions.html#target-typing) 获取更多信息。