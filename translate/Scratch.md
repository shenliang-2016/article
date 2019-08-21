## 与遗留代码互操作

目前为止，我们所有的例子都假定一个理想化的世界，所有人都使用最新版本的编程语言，当然支持范型。

然而，真实的世界并不是如此。数百万行的代码已经用老版本的编程语言写成，而这些代码并不会一夜改变。

稍后，在 [Converting Legacy Code to Use Generics](https://docs.oracle.com/javase/tutorial/extra/generics/convert.html) 章节中，我们会将这些老代码转换为使用范型的版本。这一章节中，我们将聚焦在一个更简单的问题上：遗留代码和范型代码如何互操作？这个问题有两个部分：在范型代码中使用遗留代码，以及在遗留代码中使用范型代码。

**在范型代码中使用遗留代码**

如何在享用你的范型代码的好处的同时，使用老版本代码？

作为一个例子，假定你希望使用 `com.Example.widgets` 。Example.com 的人们推出了一个库存控制系统，其亮点如下：

```java
package com.Example.widgets;

public interface Part {...}

public class Inventory {
    /**
     * Adds a new Assembly to the inventory database.
     * The assembly is given the name name, and 
     * consists of a set parts specified by parts. 
     * All elements of the collection parts
     * must support the Part interface.
     **/ 
    public static void addAssembly(String name, Collection parts) {...}
    public static Assembly getAssembly(String name) {...}
}

public interface Assembly {
    // Returns a collection of Parts
    Collection getParts();
}
```

现在，你可能想要添加使用上面 API 的新的代码。它可以很好地确保你始终可以使用合适的参数调用 `addAssembly()` 。也就是说，你传递的集合确实是一个 `Part` 类型的 `Collection` 。当然，范型是为此量身定制的：

```java
package com.mycompany.inventory;

import com.Example.widgets.*;

public class Blade implements Part {
    ...
}

public class Guillotine implements Part {
}

public class Main {
    public static void main(String[] args) {
        Collection<Part> c = new ArrayList<Part>();
        c.add(new Guillotine()) ;
        c.add(new Blade());
        Inventory.addAssembly("thingee", c);
        Collection<Part> k = Inventory.getAssembly("thingee").getParts();
    }
}
```

当我们调用 `addAssembly` 时，它期望第二个参数是 `Collection` 类型的。实际参数是 `Collection<Part>` 类型。这样可以工作，但是为什么？毕竟，大部分集合不包含 `Part` 对象，因此通常情况下，编译器无法获知 `Collection` 类型表示那种类型的集合。

在合适的范型代码中，`Collection` 将始终伴随着类型参数。当一个范型类型诸如 `Colleciton` 不使用类型参数时，它被称为一个*原始类型*。

大部分人的第一直觉反应就是 `Collection` 就是意味着 `Collection<Object>` 。然而，如我们之前所见，在需要 `Collection<Object>` 的地方传入 `Collection<Part>` 是不安全的。更准确的说法应该是，`Collection` 表示某种未知类型的集合，就像 `Collection<?>` 。

但是，那也不对！考虑 `getParts()` 的调用，返回一个 `Collection` 。然后被赋值给 `k` ，这是一个 `Collection<Part>` 。如果方法调用的结果是一个 `Collection<?>` ，该赋值将会出错。

实际上，该赋值是合法的，不过会产生一个*不受检查的警告*。该警告是必要的，因为事实上编译器确实无法保证它的类型正确性。我们没有办法检查 `getAssembly()` 中的遗留代码以确保返回的集合确实是 `Part` 对象的集合。代码中使用的类型是 `Collection` ，因此我们可以合法地将所有类型的对象插入到这样的集合中。

因此，这算是一个错误吗？理论上说，是的。但是从实践上来说，如果范型代码要调用遗留代码，就不得不允许这种情况。这取决于你，程序员，为了在这种情况下满足你的需求，该赋值是安全的，因为 `getAssembly()` 的契约表示它会返回一个 `Part` 类的集合，即使类型签名没有说明这一点。

因此，原始类型非常类似于通配符类型，但是它们并没有进行严格的类型检查。这是一个深思熟虑的设计决策，允许反省与预先存在的遗留代码互操作。

从范型代码调用遗留代码本质上是危险的; 一旦将通用代码与非泛型遗留代码混合，泛型类型系统通常提供的所有安全保证都是无效的。但是，这仍然比没有使用泛型更好。至少你知道你的代码是一致的。

目前有非常多的非范型化代码，然后有范型代码，并且不可避免地会出现需要混合的情况。

如果您发现必须混合使用旧代码和范型代码，请密切注意未经检查的警告。仔细考虑如何保证产生警告的代码的安全性。

如果你仍然犯了错误会发生什么，如果导致警告的代码确实不是类型安全的？我们来看看这种情况。在此过程中，我们将深入了解编译器的工作原理。

**擦除和翻译**

```java
public String loophole(Integer x) {
    List<String> ys = new LinkedList<String>();
    List xs = ys;
    xs.add(x); // Compile-time unchecked warning
    return ys.iterator().next();
}
```

在这里，我们给定一个字符串列表别名和一个普通的旧列表。我们在列表中插入一个`Integer`，并尝试提取一个`String`。这显然是错误的。如果我们忽略警告并尝试执行此代码，它将精确地在我们尝试使用错误类型的位置失败。在运行时，此代码的行为类似于：

```java
public String loophole(Integer x) {
    List ys = new LinkedList;
    List xs = ys;
    xs.add(x); 
    return(String) ys.iterator().next(); // run time error
}
```

当我们从列表中提取一个元素，并尝试通过将其转化为`String`以作为一个字符串处理时，我们将得到一个`ClassCastException`。完全相同的事情发生在`loophole()`的范型版本上。

原因是，Java编译器将泛型实现为称为*擦除*的前端转换。您可以（几乎）将其视为源代码到源代码的转换，从而将范型版本`loophole()`转换为非泛型版本。

因此**，即使存在未经检查的警告，Java虚拟机的类型安全性和完整性也不会存在风险**。

基本上，擦除消除（或*擦除*）所有泛型类型信息。抛出尖括号之间的所有类型信息，例如，将参数化类型`List<String>`转换为`List`。所有剩余的类型变量使用都由类型变量的上限（通常`Object`）替换。并且，只要结果代码不是类型正确的，就会插入适当类型的强制转换，如`loophole`的最后一行。

擦除的全部细节超出了本教程的范围，但我们刚刚给出的简单描述与事实相差无几。了解一下这一点很好，特别是如果你想做更复杂的事情，比如将现有的API转换为使用泛型（参见 [转换遗留代码以使用泛型](https://docs.oracle.com/javase/tutorial/extra/generics/convert.html)部分），或者只是想了解为什么事情就是这样。

**在遗留代码中使用范型代码**

现在让我们考虑相反的情况。假设 Example.com 选择将他们的 API 转化为使用范型的版本，但是并不能保证所有的客户端代码都做了同样的转化。因此现在代码如下：

```java
package com.Example.widgets;

public interface Part { 
    ...
}

public class Inventory {
    /**
     * Adds a new Assembly to the inventory database.
     * The assembly is given the name name, and 
     * consists of a set parts specified by parts. 
     * All elements of the collection parts
     * must support the Part interface.
     **/ 
    public static void addAssembly(String name, Collection<Part> parts) {...}
    public static Assembly getAssembly(String name) {...}
}

public interface Assembly {
    // Returns a collection of Parts
    Collection<Part> getParts();
}
```

同时客户端代码如下：

```java
package com.mycompany.inventory;

import com.Example.widgets.*;

public class Blade implements Part {
...
}

public class Guillotine implements Part {
}

public class Main {
    public static void main(String[] args) {
        Collection c = new ArrayList();
        c.add(new Guillotine()) ;
        c.add(new Blade());

        // 1: unchecked warning
        Inventory.addAssembly("thingee", c);

        Collection k = Inventory.getAssembly("thingee").getParts();
    }
}
```

客户端代码是在引入泛型之前编写的，但它使用了包`com.Example.widgets`和集合库，两者都使用泛型类型。客户端代码中泛型类型声明的所有用法都是原始类型。

第 1 行产生一个未检查的警告，因为在一个期望传递`Part`类型的`Collection`的地方传入了一个原始`Collection` 。且编译器不能确保原始的`Collection`真是`Part`类型的`Collection`。

作为替代方法，您可以使用 source 1.4 标志编译客户端代码，确保不生成任何警告。但是，在这种情况下，您将无法使用JDK 5.0 中引入的任何新语言功能。

