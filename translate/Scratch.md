## 优雅的打印

**泛型类被它的所有调用者共享**

下面的代码片段将会打印出什么？

```java
List <String> l1 = new ArrayList<String>();
List<Integer> l2 = new ArrayList<Integer>();
System.out.println(l1.getClass() == l2.getClass());
```

你可能会回答 `false` ，不过这是错误的。它会打印 `true` ，因为所有的泛型类实例都具有相同的运行时类型，无论它们的实际类型参数是否相同。

事实上，使得一个类成为泛型化类的就是这样的事实：它对所有可能的类型参数都具有相同的行为；同一个类看起来拥有许多不同的类型。

因此，泛型类的 `static` 变量和方法也由所有的实例共享。这就是为什么在静态方法或初始化程序中、或在静态变量或初始化程序的声明中引用类型声明的类型参数是非法的。

**转型和 InstanceOf**

泛型类由它的所有实例共享这一事实的另一层含义是，如果实例是一个泛型类型的特定调用实例，则请求该实例是没有意义的。

```java
Collection cs = new ArrayList<String>();
// Illegal.
if (cs instanceof Collection<String>) { ... }
```

类似的，这样的转型

```java
// Unchecked warning,
Collection<String> cstr = (Collection<String>) cs;
```

导致一个不受检查的警告，因为运行时系统并不会为你执行这个检查。

同样的情况也适用于类型变量：

```java
// Unchecked warning. 
<T> T badCast(T t, Object o) {
    return (T) o;
}
```

类型变量在运行时不存在。这意味着它们不会产生任何时间或者空间上的性能开销，这很好。然而不幸的是，这同时也意味着你不能在转型中放心地使用它们。

**数组**

数组对象的元素类型可能不是类型变量或者参数化类型，除非它是（无界的）通配符类型。你可以声明数组*类型*，其元素类型是类型参数或者参数化类型，但是不能声明这样的数组*对象*。

事实就是如此，尽管很烦人。这种限制很有必要，它可以避免下面这种情况：

```java
// Not really allowed.
List<String>[] lsa = new List<String>[10];
Object o = lsa;
Object[] oa = (Object[]) o;
List<Integer> li = new ArrayList<Integer>();
li.add(new Integer(3));
// Unsound, but passes run time store check
oa[1] = li;

// Run-time error: ClassCastException.
String s = lsa[1].get(0);
```

如果参数化类型元素的数组是允许的，上面的例子将会没有任何不受检查的警告而通过编译，然后在运行时失败。泛型的核心设计目标就是类型安全。特别是，Java 语言被设计为保证：**如果你的整个应用已经无任何不受检查警告地通过 javac-source 1.5 编译，则它是类型安全的。**

不过，你仍然可以使用通配符数组。下面的代码变体放弃使用数组对象和元素类型是参数化的数组类型。结果是，我们必须显式转型来从数组中获取 `String` 。

```java
// OK, array of unbounded wildcard type.
List<?>[] lsa = new List<?>[10];
Object o = lsa;
Object[] oa = (Object[]) o;
List<Integer> li = new ArrayList<Integer>();
li.add(new Integer(3));
// Correct.
oa[1] = li;
// Run time error, but cast is explicit.
String s = (String) lsa[1].get(0);
```

在下一个变体中，将发生编译错误，我们避免创建其元素类型已经参数化的数组对象，但仍然使用具有参数化元素类型的数组类型。

```java
// Error.
List<String>[] lsa = new List<?>[10];
```

类似地，试图创建一个其元素类型是一个类型变量的数组对象将导致编译错误。

```java
<T> T[] makeArray(T t) {
    return new T[100]; // Error.
}
```

由于类型变量在运行时不存在，我们将无法确定实际的数组类型。

绕开此类限制的方法是使用类字面量作为运行时类型符号，如下一章节 [Class Literals as Runtime-Type Tokens](https://docs.oracle.com/javase/tutorial/extra/generics/literals.html) 中所述。

