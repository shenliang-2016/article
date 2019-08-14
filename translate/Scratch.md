### 获取 Class 对象

所有反射操作的入口点都是 [`java.lang.Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html)。除了 [`java.lang.reflect.ReflectPermission`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/ReflectPermission.html) 。所有 [`java.lang.reflect`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/package-summary.html)  包中的类都没有`public` 的构造方法。为了获取这些类，必须调用 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 上的合适的方法。下面是集中获取 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 的几种方法，取决于代码是否能够访问一个对象，类名称，类型，或者一个已经存在的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html)。

**Object.getClass()**

如果一个对象实例可用，那么获取它的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 的最简单的方法就是调用[`Object.getClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#getClass--) 。当然，这仅仅适用于继承自 [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 的引用类型。如下所示：

```java
Class c = "foo".getClass();
```

为 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 返回 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) ：

```java
Class c = System.console().getClass();
```

通过`static`的方法 [`System.console()`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#console--) 返回与虚拟机关联的独一无二的控制台。 [`getClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#getClass--) 方法返回值就是对应于 [`java.io.Console`](https://docs.oracle.com/javase/8/docs/api/java/io/Console.html) 的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。

```java
enum E { A, B }
Class c = A.getClass();
```

`A` 是枚举类型 `E`的一个实例，因此 [`getClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#getClass--) 返回对应于枚举类型`E`的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。

```java
byte[] bytes = new byte[1024];
Class c = bytes.getClass();
```

因为数组是 [`Objects`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)，所以也可能对一个数组实例调用 [`getClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#getClass--) 。返回的[`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 对应于元素类型为`byte`的数组。

```java
import java.util.HashSet;
import java.util.Set;

Set<String> s = new HashSet<String>();
Class c = s.getClass();
```

这种情况下， [`java.util.Set`](https://docs.oracle.com/javase/8/docs/api/java/util/Set.html) 是 [`java.util.HashSet`](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html) 类型对象的一个接口， [`getClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html#getClass--) 返回对应于 [`java.util.HashSet`](https://docs.oracle.com/javase/8/docs/api/java/util/HashSet.html) 的[`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。

**`.class` 语法**

如果类型可用但没有实例，则可以通过在类型名称后附加`.class`来获取 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。这也是获取基本类型的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 的最简单方法。

```java
boolean b;
Class c = b.getClass();   // compile-time error

Class c = boolean.class;  // correct
```

注意，语句`boolean.getClass()`会产生一个编译错误，因为`boolean`是一个基本数据类型而不能被间接引用。`.class`语法返回对应于`boolean`类型的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。

```java
Class c = java.io.PrintStream.class;
```

变量`c`是对应于类型 [`java.io.PrintStream`](https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html) 的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) ：

```java
Class c = int[][][].class;
```

`.class`语法可以被用于获取对应于给定类型的多维数组的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。

**Class.forName()**

如果类的全限定名可用，则可能通过静态方法[`Class.forName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#forName-java.lang.String-) 来获取对应的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 。这不能用于基本数据类型。用于数组类名称的语法由[`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--) 描述。该语法适用于引用类型和基本数据类型。

```java
Class c = Class.forName("com.duke.MyLocaleServiceProvider");
```

此语句将由给定的全限定名创建一个类。

```java
Class cDoubleArray = Class.forName("[D");

Class cStringArray = Class.forName("[[Ljava.lang.String;");
```

变量`cDoubleArray`将包含对应于基本类型`double`的数组的 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) （即与`double[].class`相同）。`cStringArray`变量将包含对应于二维`String`数组的`Class`（即与`String[][].class`相同）。

**基本数据类型包装器的`TYPE`字段**

`.class`语法是获取基本类型的`Class`的更方便和首选的方法。然而，还有另一种获得`Class`的方法。每个基本类型和`void`在`java.lang`中都有一个包装类，用于将基本类型装箱到引用类型。每个包装类都包含一个名为`TYPE`的字段，该字段等于要包装的基本类型的`Class`。

```java
Class c = Double.TYPE;
```

当需要一个`Object`时，就需要使用`java.lang.Double`包装基本数据类型`double`，`Double.TYPE`的值等于`double.class`。

```java
Class c = Void.TYPE;
```

[`Void.TYPE`](https://docs.oracle.com/javase/8/docs/api/java/lang/Void.html#TYPE) 等于 `void.class` 。

**返回类的方法**

很多反射 API 会返回类，不过这些返回的类只能在已经直接或者间接获取到`Class`之后才能访问。

- [`Class.getSuperclass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getSuperclass--)

  返回给定类的超类。

  `````java
  Class c = javax.swing.JButton.class.getSuperclass();
  `````

   [`javax.swing.JButton`](https://docs.oracle.com/javase/8/docs/api/javax/swing/JButton.html) 的超类是 [`javax.swing.AbstractButton`](https://docs.oracle.com/javase/8/docs/api/javax/swing/AbstractButton.html) 。

- [`Class.getClasses()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getClasses--)

  返回作为类成员的所有`public`类、接口、以及枚举，包括继承来的成员。

  ````java
  Class<?>[] c = Character.class.getClasses(); 
  ````

  [`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) 包含两个成员类 [`Character.Subset`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.Subset.html) 和 [`Character.UnicodeBlock`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.UnicodeBlock.html) 。

- [`Class.getDeclaredClasses()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredClasses--)

  返回所有的类接口，以及在类中显式声明的枚举。

  ````java
  Class<?>[] c = Character.class.getDeclaredClasses(); 
  ````

  [`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) 包含两个类成员 [`Character.Subset`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.Subset.html) 和 [`Character.UnicodeBlock`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.UnicodeBlock.html) 以及一个私有类成员 `Character.CharacterCache` 。

- [`Class.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaringClass--) 

  [`java.lang.reflect.Field.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#getDeclaringClass--) 

  [`java.lang.reflect.Method.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getDeclaringClass--) 

  [`java.lang.reflect.Constructor.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#getDeclaringClass--)

  返回声明这些成员的`Class` 。 [Anonymous Class Declarations](https://docs.oracle.com/javase/specs/jls/se7/html/jls-15.html#jls-15.9.5) 将没有声明类，但是有一个封闭类。

  ````java
  import java.lang.reflect.Field;  

  Field f = System.class.getField("out"); 
  Class c = f.getDeclaringClass();
  ````

  字段 [`out`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#out) 被声明在 [`System`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html) 中。

  ````java
  public class MyClass {
      static Object o = new Object() {
          public void m() {} 
      };
      static Class<c> = o.getClass().getEnclosingClass();
  }
  ````

  `o`定义的匿名类的声明类为`null`。

- [`Class.getEnclosingClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnclosingClass--)

  返回类的直接封闭类。

  ````java
  Class c = Thread.State.class().getEnclosingClass();
  ````

  枚举 [`Thread.State`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.State.html) 的封闭类是 [`Thread`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html) 。

  ````java
  public class MyClass {
      static Object o = new Object() { 
          public void m() {} 
      };
      static Class<c> = o.getClass().getEnclosingClass();
  }
  ````

  由`o`定义的匿名类由`MyClass`包围。

