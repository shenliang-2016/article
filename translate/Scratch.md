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

If the type is available but there is no instance then it is possible to obtain a [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) by appending `".class"` to the name of the type. This is also the easiest way to obtain the [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) for a primitive type.

```
boolean b;
Class c = b.getClass();   // compile-time error

Class c = boolean.class;  // correct
```

Note that the statement `boolean.getClass()` would produce a compile-time error because a `boolean` is a primitive type and cannot be dereferenced. The `.class` syntax returns the [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) corresponding to the type `boolean`.

```
Class c = java.io.PrintStream.class;
```

The variable `c` will be the [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) corresponding to the type [`java.io.PrintStream`](https://docs.oracle.com/javase/8/docs/api/java/io/PrintStream.html).

```
Class c = int[][][].class;
```

The `.class` syntax may be used to retrieve a [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) corresponding to a multi-dimensional array of a given type.

## Class.forName()

If the fully-qualified name of a class is available, it is possible to get the corresponding [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) using the static method[`Class.forName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#forName-java.lang.String-). This cannot be used for primitive types. The syntax for names of array classes is described by[`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--). This syntax is applicable to references and primitive types.

```
Class c = Class.forName("com.duke.MyLocaleServiceProvider");
```

This statement will create a class from the given fully-qualified name.

```
Class cDoubleArray = Class.forName("[D");

Class cStringArray = Class.forName("[[Ljava.lang.String;");
```

The variable `cDoubleArray` will contain the [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) corresponding to an array of primitive type `double` (i.e. the same as `double[].class`). The `cStringArray` variable will contain the [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) corresponding to a two-dimensional array of[`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) (i.e. identical to `String[][].class`).

## TYPE Field for Primitive Type Wrappers

The `.class` syntax is a more convenient and the preferred way to obtain the [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) for a primitive type; however there is another way to acquire the [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html). Each of the primitive types and `void` has a wrapper class in [`java.lang`](https://docs.oracle.com/javase/8/docs/api/java/lang/package-summary.html) that is used for boxing of primitive types to reference types. Each wrapper class contains a field named `TYPE` which is equal to the [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) for the primitive type being wrapped.

```
Class c = Double.TYPE;
```

There is a class [`java.lang.Double`](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html) which is used to wrap the primitive type `double` whenever an [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) is required. The value of [`Double.TYPE`](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html#TYPE) is identical to that of `double.class`.

```
Class c = Void.TYPE;
```

[`Void.TYPE`](https://docs.oracle.com/javase/8/docs/api/java/lang/Void.html#TYPE) is identical to `void.class`.

## Methods that Return Classes

There are several Reflection APIs which return classes but these may only be accessed if a [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) has already been obtained either directly or indirectly.

- [`Class.getSuperclass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getSuperclass--)

  Returns the super class for the given class.`Class c = javax.swing.JButton.class.getSuperclass(); `The super class of [`javax.swing.JButton`](https://docs.oracle.com/javase/8/docs/api/javax/swing/JButton.html) is [`javax.swing.AbstractButton`](https://docs.oracle.com/javase/8/docs/api/javax/swing/AbstractButton.html).

- [`Class.getClasses()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getClasses--)

  Returns all the public classes, interfaces, and enums that are members of the class including inherited members.`Class<?>[] c = Character.class.getClasses(); `[`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) contains two member classes [`Character.Subset`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.Subset.html) and [`Character.UnicodeBlock`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.UnicodeBlock.html).

- [`Class.getDeclaredClasses()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredClasses--)

  Returns all of the classes interfaces, and enums that are explicitly declared in this class.`Class<?>[] c = Character.class.getDeclaredClasses(); `[`Character`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.html) contains two public member classes [`Character.Subset`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.Subset.html) and [`Character.UnicodeBlock`](https://docs.oracle.com/javase/8/docs/api/java/lang/Character.UnicodeBlock.html) and one private class `Character.CharacterCache`.

- [`Class.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaringClass--) [`java.lang.reflect.Field.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#getDeclaringClass--) [`java.lang.reflect.Method.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getDeclaringClass--) [`java.lang.reflect.Constructor.getDeclaringClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#getDeclaringClass--)

  Returns the [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) in which these members were declared. [Anonymous Class Declarations](https://docs.oracle.com/javase/specs/jls/se7/html/jls-15.html#jls-15.9.5) will not have a declaring class but will have an enclosing class.`import java.lang.reflect.Field;  Field f = System.class.getField("out"); Class c = f.getDeclaringClass(); `The field [`out`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#out) is declared in [`System`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html).`public class MyClass {     static Object o = new Object() {         public void m() {}      };     static Class<c> = o.getClass().getEnclosingClass(); } `The declaring class of the anonymous class defined by `o` is `null`.

- [`Class.getEnclosingClass()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnclosingClass--)

  Returns the immediately enclosing class of the class.`Class c = Thread.State.class().getEnclosingClass(); `The enclosing class of the enum [`Thread.State`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.State.html) is [`Thread`](https://docs.oracle.com/javase/8/docs/api/java/lang/Thread.html).`public class MyClass {     static Object o = new Object() {          public void m() {}      };     static Class<c> = o.getClass().getEnclosingClass(); } `The anonymous class defined by `o` is enclosed by `MyClass`.