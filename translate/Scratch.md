## 通配符

考虑编写打印集合中所有元素的程序。下面是你在 Java 5.0 版本之前的可能写法：

```java
void printCollection(Collection c) {
    Iterator i = c.iterator();
    for (k = 0; k < c.size(); k++) {
        System.out.println(i.next());
    }
}
```

下面是一个单纯的使用泛型的版本（同时使用了新版本的 `for` 循环语法）：

```java
void printCollection(Collection<Object> c) {
    for (Object e : c) {
        System.out.println(e);
    }
}
```

问题在于，新版本的代码相比于老版本代码通用性差了很多。因为老版本代码可以接受任何类型的集合作为参数，但是新版本的代码只能使用 `Collection<Object>` ，当时，正如我们前面强调的，它并不是所有集合的超类！

那么，什么才是所有集合的超类？写做 `Collection<?>` （发音为“collection of unknown”），也就是说，一个元素类型匹配任何东西的集合。它被称为**通配符类型**，顾名思义。我们可以这么写：

```java
void printCollection(Collection<?> c) {
    for (Object e : c) {
        System.out.println(e);
    }
}
```

现在，我们可以使用任意类型的集合来调用新版本代码。注意在 `printCollection()` 内部，我们仍然能够从 `c` 中读取元素并给予它们类型 `Object` 。这永远是安全的，因为无论实际集合元素是什么类型，它都包含对象。然而，向其中添加任意对象却是不安全的：

```java
Collection<?> c = new ArrayList<String>();
c.add(new Object()); // Compile time error
```

因为我们不知道 `c` 的元素类型代表什么，我们不能添加对象到其中。`add()` 方法使用类型 `E` 的参数，也就是集合的元素类型。当实际类型参数是 `?` 时，它代表一些未知类型。我们传递给 `add` 的任何参数都必须是这个未知类型的子类。因为我们不知道这个类型是什么，我们也就不能传递任何参数进去。唯一的例外是 `null` ，它是每种类型的成员。

另一方面，给定一个 `List<?>` ，我们能够调用 `get()` 并使用其结果。结果类型是一个未知类型，但是我们始终知道它就是一个对象。因此，将 `get()` 方法的结果赋值给一个 `Object` 类型的变量，或者将其作为 `Object` 类型参数传递都是安全的。

**有界通配符**

考虑一个简单的绘图程序，可以绘制诸如长方形和圆形等形状。为了在程序中表示这些形状，你可以定义如下类体系结构：

```java
public abstract class Shape {
    public abstract void draw(Canvas c);
}

public class Circle extends Shape {
    private int x, y, radius;
    public void draw(Canvas c) {
        ...
    }
}

public class Rectangle extends Shape {
    private int x, y, width, height;
    public void draw(Canvas c) {
        ...
    }
}
```

这些形状可以被绘制到画布上：

```java
public class Canvas {
    public void draw(Shape s) {
        s.draw(this);
   }
}
```

任何绘制将包含一系列的形状。假定它们表示为一个列表，方便的做法是在 `Canvas` 中有一个方法类绘制它们：

```java
public void drawAll(List<Shape> shapes) {
    for (Shape s: shapes) {
        s.draw(this);
   }
}
```

现在，类型规则规定 `drawAll()` 只能被在一个确切的 `Shape` 列表上调用。它不能，比如，被在 `List<Circle>` 上调用。这很不幸，因为所有的方法确实是从该列表中读取形状，因此它也应该可以被在 `List<Circle>` 上调用。其实我们需要的是接受任何形状的列表的方法：

```java
public void drawAll(List<? extends Shape> shapes) {
    ...
}
```

这里有个很小的但是很重要的区别：我们已经使用 `List<? extends Shape>` 替换了类型 `List<Shape>` 。现在 `drawAll()` 将接受任何 `Shape` 的子类的列表，因而我们现在可以如愿在 `List<Circle>` 上调用它。

`List<? extends Shapte>` 是一个*有界通配符*的例子。其中的 `?` 表示一个未知类型，就像我们前面看到的通配符。然而，这种情况下，我们知道这个未知类型实际上是 `Shape` 的子类。（注意：它可以是 `Shape` 本身，或者是一些子类，它不需要字面上扩展 `Shape` 。）我们将 `Shape` 称为通配符的*上界* 。

这就是通常情况下为了使用通配符的灵活性而需要付出的代价。代价是现在在方法体中写入 `Shape` 是非法的。比如，下面的写法是不允许的：

```java
public void addRectangle(List<? extends Shape> shapes) {
    // Compile-time error!
    shapes.add(0, new Rectangle());
}
```

你应该能够指出为什么上面的代码是不允许的。`shapes.add()` 的第二个参数的类型是 `? extends Shape` ，一个 `Shape` 的未知子类型。因为我们不知道它是什么类型，我们也就不知道它是不是 `Rectangle` 的超类。它可能是也可能不是那个超类，因此在那里传递 `Rectangel` 是不安全的。

有界通配符正是人们处理DMV将其数据传递给人口普查局的例子中所需要的。我们的示例假定数据通过从名称（表示为字符串）到人（由引用类型（如`Person`或其子类型，如`Driver`）表示）的映射来表示。`Map <K，V>`是一个泛型类型的示例，它采用两个类型参数，表示映射的键和值。

再次，请注意形式类型参数的命名约定 - 键为`K`，值为`V` 。

```java
public class Census {
    public static void addRegistry(Map<String, ? extends Person> registry) {
}
...

Map<String, Driver> allDrivers = ... ;
Census.addRegistry(allDrivers);
```

