## 泛型方法

考虑编写一个方法，接受一个对象数组和一个集合，并将数组中的所有对象全部放入集合中。下面是第一种尝试：

```java
static void fromArrayToCollection(Object[] a, Collection<?> c) {
    for (Object o : a) { 
        c.add(o); // compile-time error
    }
}
```

现在，你应该已经学会了避免初学者错误地尝试使用 `Collection<Object>` 作为集合参数的类型。你可能已经能够意识到也不能使用 `Collection<?>` 。回想一下，你不能将对象放进未知类型的集合中。

处理此类问题的方法是使用*泛型方法*，类似于类型声明，方法声明可以泛型化，也就是说，通过一个或者多个类型参数进行参数化。

```java
static <T> void fromArrayToCollection(T[] a, Collection<T> c) {
    for (T o : a) {
        c.add(o); // Correct
    }
}
```

我们可以使用任何类型的集合调用此方法，该集合元素类型是该数组元素的类型的子类型。

```java
Object[] oa = new Object[100];
Collection<Object> co = new ArrayList<Object>();

// T inferred to be Object
fromArrayToCollection(oa, co); 

String[] sa = new String[100];
Collection<String> cs = new ArrayList<String>();

// T inferred to be String
fromArrayToCollection(sa, cs);

// T inferred to be Object
fromArrayToCollection(sa, co);

Integer[] ia = new Integer[100];
Float[] fa = new Float[100];
Number[] na = new Number[100];
Collection<Number> cn = new ArrayList<Number>();

// T inferred to be Number
fromArrayToCollection(ia, cn);

// T inferred to be Number
fromArrayToCollection(fa, cn);

// T inferred to be Number
fromArrayToCollection(na, cn);

// T inferred to be Object
fromArrayToCollection(na, co);

// compile-time error
fromArrayToCollection(na, cs);
```

注意，我们不是必须传递实际类型参数给泛型方法。编译器为我们推断该类型参数，基于实际参数的类型。它将通常推断可以使得调用成功的最精准的类型参数。

这里出现一个问题：我应该何时使用泛型方法，何时使用通配符类型？为了理解问题的答案，让我们来检查 `Collection` 类库中的某些方法：

```java
interface Collection<E> {
    public boolean containsAll(Collection<?> c);
    public boolean addAll(Collection<? extends E> c);
}
```

使用泛型方法之后：

```java
interface Collection<E> {
    public <T> boolean containsAll(Collection<T> c);
    public <T extends E> boolean addAll(Collection<T> c);
    // Hey, type variables can have bounds too!
}
```

不过，在 `containAll` 和 `addAll` 方法中，类型参数 `T` 只使用一次。方法的返回类型不依赖该类型参数，或者任何其他方法参数（这个例子很简单，方法只有一个参数）。这就告诉我们类型参数正在被用于多态。它的唯一影响就是允许各种实际参数类型可以在不同调用点使用。如果是这种场景，我们就应该使用通配符。通配符被设计为支持灵活的子类型化，也就是我们试图在这里表达的。

泛型方法允许类型参数被用于表示方法的一个或者多个参数的类型与/或该方法的返回类型之间的依赖关系。如果不存在这种依赖关系，就不应该使用泛型方法。

串联使用泛型方法和通配符是可能的。如下面的方法 `Collections.copy()` ：

```java
class Collections {
    public static <T> void copy(List<T> dest, List<? extends T> src) {
    ...
}
```

注意两个参数类型之间的依赖关系。从源列表`src`复制的任何对象必须可分配给目标列表`dst`的元素类型`T`。所以`src`的元素类型可以是`T`的任何子类型 - 我们不关心具体是哪个。`copy`的签名使用类型参数表示依赖关系，但对第二个参数的元素类型使用通配符。

我们可以用另一种方式为这种方法编写签名，而不使用通配符：

```java
class Collections {
    public static <T, S extends T> void copy(List<T> dest, List<S> src) {
    ...
}
```

这很好，但是第一个类型参数既用于`dst`的类型又用于第二个类型参数的边界，`S`，`S`本身仅使用一次，在`src`的类型中 - 没有别的东西依赖它。这表明我们可以用通配符替换`S` 。使用通配符比声明显式类型参数更清晰，更简洁，因此应尽可能优先使用通配符。

通配符还具有以下优点：它们可以在方法签名之外使用，如字段类型，局部变量和数组。这是一个例子。

回到我们的形状绘制问题，假设我们想要保留绘图请求的历史记录。我们可以在类`Shape`中的静态变量中维护历史记录，并让`drawAll()`将其传入的参数存储到历史记录字段中。

```java
static List<List<? extends Shape>> 
    history = new ArrayList<List<? extends Shape>>();

public void drawAll(List<? extends Shape> shapes) {
    history.addLast(shapes);
    for (Shape s: shapes) {
        s.draw(this);
    }
}
```

最后，再次让我们注意用于类型参数的命名约定。我们使用`T`作为类型，只要没有更具体的类型来区分它。泛型方法通常就是这种情况。如果有多个类型参数，我们可能会使用字母表中与`T`相邻的字母，例如`S` 。如果泛型方法出现在泛型类中，最好避免对方法和类的类型参数使用相同的名称，避免混淆。这同样适用于嵌套泛型类。

