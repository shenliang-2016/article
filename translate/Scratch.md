## 类字面量作为运行时类型符号

JDK 5.0中的一个变化是类 `java.lang.Class` 的的泛型化。这是一个有趣的例子，它将泛型化用于容器类以外的东西。

既然 `Class`有一个类型参数 `T`，你可能会问，`T` 代表什么？它代表 `Class` 对象所表示的类型。

例如， `String.class` 的类型是 `Class <String>`，`Serializable.class` 的类型是 `Class <Serializable>`。这可用于改善反射代码的类型安全性。

特别是，由于 `Class` 中的 `newInstance()`方法现在返回一个 `T`，因此在反射创建对象时可以获得更精确的类型。

例如，假设您需要编写一个执行数据库查询的实用程序方法，查询以 SQL 字符串形式给出，返回数据库中与该查询匹配的对象集合。

一种方法是显式传入工厂对象，编写如下代码：

```java
interface Factory<T> { T make();} 

public <T> Collection<T> select(Factory<T> factory, String statement) { 
    Collection<T> result = new ArrayList<T>(); 

    /* Run sql query using jdbc */  
    for (/* Iterate over jdbc results. */) { 
        T item = factory.make();
        /* Use reflection and set all of item's 
         * fields from sql results. 
         */ 
        result.add(item); 
    } 
    return result; 
}
```

你可以这样调用：

```java
select(new Factory<EmpInfo>(){ 
    public EmpInfo make() {
        return new EmpInfo();
    }}, "selection string");
```

或者你可以声明一个 `EmpInfoFactory` 类来支持该 `Factory` 接口：

```java
class EmpInfoFactory implements Factory<EmpInfo> {
    ...
    public EmpInfo make() { 
        return new EmpInfo();
    }
}
```

并调用之：

```java
select(getMyEmpInfoFactory(), "selection string");
```

这种解决方案的缺点是它需要以下两个条件之一：

- 在调用点使用详细的匿名工厂类，或者
- 为使用的每个类型声明一个工厂类并在调用点传递一个工厂实例，这多少有点不自然。

使用类字面量作为方法对象更加自然，该字面量接下来可以被反射机制使用。如今（不用泛型）该代码可能写成：

```java
Collection emps = sqlUtility.select(EmpInfo.class, "select * from emps");
...
public static Collection select(Class c, String sqlStatement) { 
    Collection result = new ArrayList();
    /* Run sql query using jdbc. */
    for (/* Iterate over jdbc results. */ ) { 
        Object item = c.newInstance(); 
        /* Use reflection and set all of item's
         * fields from sql results. 
         */  
        result.add(item); 
    } 
    return result; 
}
```

不过，这不会给我们一个期待中的精确类型的集合。现在 `Class` 类是泛型化的，我们可以这样写：

```java
Collection<EmpInfo> 
    emps = sqlUtility.select(EmpInfo.class, "select * from emps");
...
public static <T> Collection<T> select(Class<T> c, String sqlStatement) { 
    Collection<T> result = new ArrayList<T>();
    /* Run sql query using jdbc. */
    for (/* Iterate over jdbc results. */ ) { 
        T item = c.newInstance(); 
        /* Use reflection and set all of item's
         * fields from sql results. 
         */  
        result.add(item);
    } 
    return result; 
} 
```

上面的代码以类型安全的方式给了我们一个精确类型的集合。

这种将类字面量作为运行时类型符号的技术很有用。例如，这是一种习惯用法，广泛用于操作注解的新 API 中。

## 通配符的有趣用法

本章节中，我们将考虑一些更高级的通配符用法。我们已经看过一些有界通配符的用法，比如从数据结构中读取数据。现在考虑相反的场景，一种只能写入的数据结构。接口 `Sink` 就是此类数据结构的一个简单例子：

```java
interface Sink<T> {
    flush(T t);
}
```

我们可以入下面代码中这样使用它为例。方法 `writeAll()` 被设计为倾倒集合 `coll` 中的所有元素到 `snk` 中，并返回倾倒的最后一个元素。

```java
public static <T> T writeAll(Collection<T> coll, Sink<T> snk) {
    T last;
    for (T t : coll) {
        last = t;
        snk.flush(last);
    }
    return last;
}
...
Sink<Object> s;
Collection<String> cs;
String str = writeAll(cs, s); // Illegal call.
```

入代码所写，调用 `writeAll()` 是非法的，因为没有有效的类型参数能被推断出来，`String` 和 `Object` 都不是 `T` 的合适类型，因为 `Collection` 元素和 `Sink` 元素必须是相同类型。

我们可以解决此问题，通过修改 `writeAll()` 方法签名如下，使用通配符：

```java
public static <T> T writeAll(Collection<? extends T>, Sink<T>) {...}
...
// Call is OK, but wrong return type. 
String str = writeAll(cs, s);
```

这个调用现在是合法的，但是赋值会出错，因为返回类型推断为 `Object` ，因为 `T` 匹配 `s` 的元素类型，该类型是 `Object` 。

可用的解决方案是使用我们还没有看过的有界通配符：有*下界*的通配符。语法 `? super T` 表示一个未知类型，该类型是 `T` 的超类（或者 `T` 自己，注意超类关系是自指的）。这就是我们已经在使用的有界通配符的双重身份，另外一种是 `? extends T` 表示一个未知类型，该类型是 `T` 的子类。

```java
public static <T> T writeAll(Collection<T> coll, Sink<? super T> snk) {
    ...
}
String str = writeAll(cs, s); // Yes! 
```

使用这种语法，方法调用是合法的，并且推断出来的类型是期望的 `String` 。

现在让我们转向一个更现实的例子。`java.util.TreeSet <E>`  表示已排序的 `E` 类型元素的树。构造 `TreeSet` 的一种方法是将 `Comparator` 对象传递给构造函数。该比较器将用于根据所需的顺序对 `TreeSet` 的元素进行排序。

```java
TreeSet(Comparator<E> c) 
```

 `Comparator` 接口很基本：

```java
interface Comparator<T> {
    int compare(T fst, T snd);
}
```

假设我们想要创建一个 `TreeSet <String>` 并传入一个合适的比较器，我们需要传递一个可以比较 `String` 的 `Comparator`。这可以通过 `Comparator <String>` 完成，但 `Comparator <Object>` 也可以。但是，我们将无法在 `Comparator <Object>` 上调用上面给出的构造函数。我们可以使用更低下界的有界通配符来获得我们想要的灵活性：

```java
TreeSet(Comparator<? super E> c) 
```

该代码允许使用任何适用的比较器。

作为使用下限有界通配符的最后一个示例，让我们看一下 `Collections.max()` 方法，它返回作为参数传递给它的集合中的最大元素。现在，为了使 `max()` 工作，传入的集合的所有元素都必须实现 `Comparable` 。此外，它们必须可以*彼此*比较。

首次尝试泛型化此方法签名会产生：

```java
public static <T extends Comparable<T>> T max(Collection<T> coll)
```

也就是说，该方法采用可以与自身比较的某种类型 `T` 的集合，并返回该类型的元素。但是，此代码过于严格。要了解原因，请考虑可以与任意对象比较的类型：

```java
class Foo implements Comparable<Object> {
    ...
}
Collection<Foo> cf = ... ;
Collections.max(cf); // Should work.
```

`cf` 的每个元素都可以与 `cf` 中的其他元素相比较，因为每个这样的元素都是 `Foo`，可以与任何对象相比较，特别是与另一个 `Foo` 相比较。但是，使用上面的签名，我们发现该调用被拒绝。推断出的类型必须是 `Foo`，但 `Foo` 并没有实现 `Comparable <Foo>` 。

`T` 不必可以与其本身相比较。所需要的只是 `T` 可以与其超类型之一相比较。这给了我们：

```java
public static <T extends Comparable<? super T>> 
        T max(Collection<T> coll)
```

请注意，`Collections.max()` 的实际签名更复杂。我们将在下一节 [Converting Legacy Code to Use Generics](https://docs.oracle.com/javase/tutorial/extra/generics/convert.html) 中介绍它。这种推理几乎适用于任何类型的 `Comparable` 用法：你总是想使用  `Comparable<? **super** T>`。

通常，如果您的 API 只使用类型参数 `T` 作为参数，则其使用应该利用较低的有界通配符（`? super T`）。相反，如果 API 仅返回 `T`，您将通过使用上限有通配符（`? extends T`）为您的客户端提供更大的灵活性。

**通配符捕获**

现在应该很清楚了，给定：

```java
Set<?> unknownSet = new HashSet<String>();
...
/* Add an element  t to a Set s. */ 
public static <T> void addToSet(Set<T> s, T t) {
    ...
}
```

下面的调用是非法的：

```java
addToSet(unknownSet, "abc"); // Illegal.
```

传递的实际集合是一个字符串集合没有区别；重要的是，作为参数传递的表达式是一个未知类型集合，不能保证是一个字符串集合，特别是任何类型的集合。

现在，请考虑以下代码：

```java
class Collections {
    ...
    <T> public static Set<T> unmodifiableSet(Set<T> set) {
        ...
    }
}
...
Set<?> s = Collections.unmodifiableSet(unknownSet); // This works! Why?
```

看来这不应该被允许。但是，看看这个特定的调用，允许它是完全安全的。毕竟，`unmodifiableSet()` 适用于任何类型的 `Set`，无论其元素类型如何。

由于这种情况相对频繁地出现，因此有一个特殊规则允许在非常特定的情况下使用这些代码，在这种情况下可以证明代码是安全的。此规则称为*通配符捕获*，允许编译器将通配符的未知类型推断为泛型方法的类型参数。

