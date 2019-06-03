#### 无界通配符

无界通配符类型使用通配符`?`来说明，比如，`List<?>`。这被称为未知类型列表。无界通配符在两种场景下是非常有用的：

- 如果你正在编写一个方法，该方法可以使用`Object`类中提供的功能实现。
- 当代码使用泛型类中不依赖类型参数方法时。比如 `List.size` 或者 `List.clear`。事实上，`Class<?>` 是如此常用，因为`Class<?>`中大部分方法都不依赖 `T`。

考虑下面的方法 `printList`：

```java
public static void printList(List<Object> list) {
    for (Object elem : list)
        System.out.println(elem + " ");
    System.out.println();
}
```

`printList`的目标是打印任何类型的列表，但它无法实现该目标 - 它只打印一个`Object`实例列表；它不能打印`List <Integer>`，`List <String>`，`List <Double>`等等，因为它们不是`List <Object>`的子类型。 要编写通用的`printList`方法，请使用`List <？>`：

```java
public static void printList(List<?> list) {
    for (Object elem: list)
        System.out.print(elem + " ");
    System.out.println();
}
```

因为对任何具体的类型 `A`, `List<A>` 都是 `List<?>`的子类，你可以使用 `printList` 来打印任何类型元素的列表：

```java
List<Integer> li = Arrays.asList(1, 2, 3);
List<String>  ls = Arrays.asList("one", "two", "three");
printList(li);
printList(ls);
```

------

**注意：**  [`Arrays.asList`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#asList-T...-) 方法被用在本手册中的所有例子中。此静态工厂方法转化给定的数据并且返回一个固定长度的列表。

------

注意`List <Object>`和`List <？>`是不一样的。您可以将`Object`或`Object`的任何子类型插入到`List <Object>`中。但是你只能将`null`插入`List <？>`。[通配符使用指南](https://docs.oracle.com/javase/tutorial/java/generics/wildcardGuidelines.html) 部分提供了有关如何确定特定情况下应使用哪种通配符（如果有）的更多信息。

