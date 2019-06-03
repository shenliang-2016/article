### 通配符

在泛型代码中，问号`?`被称为*通配符*，表示一个未知的类型。通配符能够被用在各种情景中：作为参数、字段或者局部变量的类型，有时候也作为一个返回类型。通配符永远不会被用来作为泛型方法声明、泛型类实例创建的类型参数，或者一个超类型。

接下来的章节详细讨论通配符，包括上界通配符、下界通配符，以及通配符捕获。

#### 上界通配符

您可以使用上限通配符来放宽对变量的限制。例如，假设您要编写一个适用于`List <Integer>`，`List <Double>`，*和*`List <Number>`的方法。你可以通过使用上限的通配符来实现这一点。

要声明一个上限通配符，请使用通配符（`?`），后跟`extends`关键字，后跟*上限*。注意，在这种情况下，`extends`在一般意义上用于表示“扩展”（在类中）或“实现”（在接口中）。

要编写适用于`Number`列表和`Number`子类的方法，如`Integer`，`Double`和`Float`，你可以指定`List <？ extends Number>`。术语`List <Number>`比`List <？extends Number>`更具限制性。因为前者只匹配一个类型为`Number`的列表，而后者匹配一个类型为`Number`或其任何子类的列表。

考虑下面的 `process` 方法：

```java
public static void process(List<? extends Foo> list) { /* ... */ }
```

上界通配符 `<? extends Foo>`，其中的 `Foo` 是任何类型，匹配到 `Foo` 以及 `Foo`的任何子类。 `process` 方法能够处理元素类型为 `Foo`的列表：

```java
public static void process(List<? extends Foo> list) {
    for (Foo elem : list) {
        // ...
    }
}
```

在`foreach`子句中，`elem`变量遍历列表中的每个元素。现在可以在`elem`上使用`Foo`类中定义的任何方法。

`sumOfList`方法返回列表中数字的总和：

```java
public static double sumOfList(List<? extends Number> list) {
    double s = 0.0;
    for (Number n : list)
        s += n.doubleValue();
    return s;
}
```

下面的代码，使用 `Integer` 对象列表，打印结果 `sum = 6.0`：

```java
List<Integer> li = Arrays.asList(1, 2, 3);
System.out.println("sum = " + sumOfList(li));
```

`Double`值列表可以使用相同的`sumOfList`方法。以下代码打印`sum = 7.0`：

```java
List<Double> ld = Arrays.asList(1.2, 2.3, 3.5);
System.out.println("sum = " + sumOfList(ld));
```