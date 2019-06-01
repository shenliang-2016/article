### 泛型类型

*泛型类型*是一个泛型类或者接口，进行了类型参数化。下面的`Box`类将被改写来说明这个概念。

**简单版本的`Box`类**

检查一个非泛型的`Box`类，操作任意类型的对象。它只需要两个方法：`set`方法来添加对象到盒子里，`get`方法从盒子里拿到对象。

````java
public class Box {
    private Object object;

    public void set(Object object) { this.object = object; }
    public Object get() { return object; }
}
````

由于它的方法接受或返回一个`Object`，只要它不是基本数据类型之一，你就可以自由地传入任何你想要传入的东西。在编译时无法验证类的使用方式。代码的一部分可能会在框中放置一个`Integer`，并期望从中获取`Integer`，而代码的另一部分可能会错误地传入`String`，从而导致运行时错误。

**`Box`类的泛型版本**

泛型类以下面的形式定义：

````java
class name<T1, T2, ..., Tn> { /* ... */ }
````

类型餐多户部分，由尖括号 `<>` 分隔，跟随着类名。它给出了*类型参数*，也被称为*类型变量* `T1`, `T2`, ..., 以及 `Tn`。

要更新`Box`类以使用泛型，可以通过将代码“`public class Box`”更改为“`public class Box <T>`”来创建*泛型类型声明*。这引入了类型变量`T`，可以在类中的任何地方使用。

通过此更改，`Box`类变为：

```java
/**
 * Generic version of the Box class.
 * @param <T> the type of the value being boxed
 */
public class Box<T> {
    // T stands for "Type"
    private T t;

    public void set(T t) { this.t = t; }
    public T get() { return t; }
}
```

如您所见，所有出现的`Object`都被`T`取代。类型变量可以是您指定的任何**非原始**类型：任何类类型，任何接口类型，任何数组类型，甚至是其他类型变量。

可以应用相同的技术来创建通用接口。

