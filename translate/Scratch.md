## 重构遗留代码以使用泛型

前面，我们展示了新版本代码和遗留代码如何互操作。现在，看看更困难的问题，泛型化老代码。

如果你决定要重构老代码以使用泛型，你就需要谨慎考虑对 API 的修改。

您需要确保泛型 API 不会过度限制；它必须继续支持 API 的原始契约。再次考虑 `java.util.Collection` 中的一些示例。泛型化之前的 API 如下所示：

```java
interface Collection {
    public boolean containsAll(Collection c);
    public boolean addAll(Collection c);
}
```

最直接的泛型化尝试可能如下：

```java
interface Collection<E> {

    public boolean containsAll(Collection<E> c);
    public boolean addAll(Collection<E> c);
}
```

尽管这是类型安全的，它却并没有遵循原始 API 的契约。`containsAll()` 方法使用任何类型的输入集合。只有当传入集合实际上只包含 `E` 类型实例时，它才会成功。但是：

* 传入集合的静态类型可能不同，可能因为调用者并不知道被传入的集合的精确类型，或者因为它是一个 `Collection<S>` ，其中的 `S` 是 `E` 的一个子类。
* 使用不同类型的集合调用 `containsAll()` 是完全合法的。该程序可以工作，返回 `false` 。

在 `addAll()` 情况下，我们应该能够添加任何由 `E` 的子类组成的集合。我们在 [Generic Methods](https://docs.oracle.com/javase/tutorial/extra/generics/methods.html) 章节中看到了如何正确处理这种情况。

您还需要确保修订后的 API 保持与旧客户端的二进制兼容性。这意味着 API 的擦除必须与原始的，未经过泛型化的 API 相同。在大多数情况下，这自然会失败，但有一些微妙的情况。我们将研究我们遇到过的最微妙的案例之一，即 `Collections.max()` 方法。正如我们在  [More Fun with Wildcards](https://docs.oracle.com/javase/tutorial/extra/generics/morefun.html) 部分中看到的那样，`max()` 的合理签名是：

```java
public static <T extends Comparable<? super T>> 
        T max(Collection<T> coll)
```

这很好，除了此签名的擦除是：

```java
public static Comparable max(Collection coll)
```

不同于原始的 `max()` 签名：

```java
public static Object max(Collection coll)
```

本来当然可以早已指定了这个 `max()` 签名，但是这并没有发生，同时所有的调用 `Collections.max()` 的老版本的二进制类文件都依赖于返回 `Object` 的签名。

我们可以强制擦除不同，通过为形式类型参数 `T` 显式指定一个界内的超类。

```java
public static <T extends Object & Comparable<? super T>> 
        T max(Collection<T> coll)
```

这是一个给定*多个边界*的类型参数的例子，使用语法`T1 & T2 ... & Tn` 。一个具有多个边界的类型变量被认为是边界列表中的所有类型的子类。当使用多个边界时，边界列表中第一个出现的类型会被作为类型变量的擦除。

最终，我们应该记得 `max` 只从它的输入集合中读取数据，因此适用于 `T` 的任何子类的集合。

这将我们指引到 JDK 中实际使用的方法签名：

```java
public static <T extends Object & Comparable<? super T>> 
        T max(Collection<? extends T> coll)
```

在实践中出现如此复杂的事情是非常罕见的，但类库设计者应该准备好在转换现有 API 时的全面考量。

需要注意的另一个问题是*协变返回*，即改进子类中方法的返回类型。您不应该在旧 API 中利用此功能。为了了解原因，让我们看一个例子。

假设您的原始 API 具有以下形式：

```java
public class Foo {
    // Factory. Should create an instance of 
    // whatever class it is declared in.
    public Foo create() {
        ...
    }
}

public class Bar extends Foo {
    // Actually creates a Bar.
    public Foo create() {
        ...
    }
}
```

利用协变返回的优点，你将其修改为：

```java
public class Foo {
    // Factory. Should create an instance of 
    // whatever class it is declared in.
    public Foo create() {
        ...
    }
}

public class Bar extends Foo {
    // Actually creates a Bar.
    public Bar create() {
        ...
    }
}
```

现在，假定你的代码的一个第三方客户端编写如下代码：

```java
public class Baz extends Bar {
    // Actually creates a Baz.
    public Foo create() {
        ...
    }
}
```

Java 虚拟机不直接支持覆盖具有不同返回类型的方法。编译器支持此功能。因此，除非重新编译 `Baz` 类，否则它将无法正确覆盖 `Bar` 的 `create()` 方法。此外，`Baz` 必须被修改，因为代码将在编写时被拒绝 - `Baz` 中的 `create()` 的返回类型不是 `Bar` 中 `create()` 的返回类型的子类型。

## 致谢

Erik Ernst, Christian Plesner Hansen, Jeff Norton, Mads Torgersen, Peter von der Ahe and Philip Wadler 为此课程贡献了宝贵资料。

感谢 David Biesack, Bruce Chapman, David Flanagan, Neal Gafter, Orjan Petersson, Scott Seligman, Yoshiki Shibata and Kresten Krab Thorup 为此课程的早期版本提供了珍贵的反馈。如果有遗漏，深表抱歉！