#### 故障排除

在尝试通过反射调用构造函数时，开发人员有时会遇到以下问题。

**丢失无参构造器导致的 InstantiationException**

 [`ConstructorTrouble`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ConstructorTrouble.java) 例子展示了当代码试图通过使用 [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 创建类的新实例，而不存在可访问的无参构造器情况下将会发生什么。

```java
public class ConstructorTrouble {
    private ConstructorTrouble(int i) {}

    public static void main(String... args){
	try {
	    Class<?> c = Class.forName("ConstructorTrouble");
	    Object o = c.newInstance();  // InstantiationException

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java ConstructorTrouble*

```
java.lang.InstantiationException: ConstructorTrouble
        at java.lang.Class.newInstance0(Class.java:340)
        at java.lang.Class.newInstance(Class.java:308)
        at ConstructorTrouble.main(ConstructorTrouble.java:7)
```

------

提示：可能发生 [`InstantiationException`](https://docs.oracle.com/javase/8/docs/api/java/lang/InstantiationException.html) 的原因有很多。在这种情况下，问题是带有`int`参数的构造函数的存在会阻止编译器生成缺省（或零参数）构造函数，并且代码中没有显式的零参数构造函数。请记住，[`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 的行为与`new`关键字非常相似，并且只要`new`失败就会失败。

------

**`Class.newInstance()` 抛出 `Unexpected Exception`**

 [`ConstructorTroubleToo`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ConstructorTroubleToo.java) 例子展示了 [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 的一个无法解决的问题。名义上，它传播由构造器抛出的所有异常，受检查的和不受检查的异常：

```java
import java.lang.reflect.InvocationTargetException;
import static java.lang.System.err;

public class ConstructorTroubleToo {
    public ConstructorTroubleToo() {
 	throw new RuntimeException("exception in constructor");
    }

    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName("ConstructorTroubleToo");
	    // Method propagetes any exception thrown by the constructor
	    // (including checked exceptions).
	    if (args.length > 0 && args[0].equals("class")) {
		Object o = c.newInstance();
	    } else {
		Object o = c.getConstructor().newInstance();
	    }

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	    err.format("%n%nCaught exception: %s%n", x.getCause());
	}
    }
}
```

$ *java ConstructorTroubleToo class*

```
Exception in thread "main" java.lang.RuntimeException: exception in constructor
        at ConstructorTroubleToo.<init>(ConstructorTroubleToo.java:6)
        at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
        at sun.reflect.NativeConstructorAccessorImpl.newInstance
          (NativeConstructorAccessorImpl.java:39)
        at sun.reflect.DelegatingConstructorAccessorImpl.newInstance
          (DelegatingConstructorAccessorImpl.java:27)
        at java.lang.reflect.Constructor.newInstance(Constructor.java:513)
        at java.lang.Class.newInstance0(Class.java:355)
        at java.lang.Class.newInstance(Class.java:308)
        at ConstructorTroubleToo.main(ConstructorTroubleToo.java:15)
```

这种情况是反射所特有的。通常，编写忽略已检查异常的代码是不可能的，因为它不会通过编译。可以使用 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 而不是 [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 来包装构造函数抛出的任何异常。

$ *java ConstructorTroubleToo*

```
java.lang.reflect.InvocationTargetException
        at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
        at sun.reflect.NativeConstructorAccessorImpl.newInstance
          (NativeConstructorAccessorImpl.java:39)
        at sun.reflect.DelegatingConstructorAccessorImpl.newInstance
          (DelegatingConstructorAccessorImpl.java:27)
        at java.lang.reflect.Constructor.newInstance(Constructor.java:513)
        at ConstructorTroubleToo.main(ConstructorTroubleToo.java:17)
Caused by: java.lang.RuntimeException: exception in constructor
        at ConstructorTroubleToo.<init>(ConstructorTroubleToo.java:6)
        ... 5 more


Caught exception: java.lang.RuntimeException: exception in constructor

```

如果抛出 [`InvocationTargetException`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html) ，则调用该方法。问题的诊断与直接调用构造函数并抛出[`InvocationTargetException.getCause()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html#getCause--) 检索的异常相同。此异常并不表示反射包或其用法存在问题。

------

**提示：**最好在 [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 上使用 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) ，因为前一个API允许检查和处理构造函数抛出的任意异常。

------

**定位或调用正确的构造函数时出现问题**

 [`ConstructorTroubleAgain`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ConstructorTroubleAgain.java) 类展示各种不正确的代码标识和调用期待中的构造器的方法：

```java
import java.lang.reflect.InvocationTargetException;
import static java.lang.System.out;

public class ConstructorTroubleAgain {
    public ConstructorTroubleAgain() {}

    public ConstructorTroubleAgain(Integer i) {}

    public ConstructorTroubleAgain(Object o) {
	out.format("Constructor passed Object%n");
    }

    public ConstructorTroubleAgain(String s) {
	out.format("Constructor passed String%n");
    }

    public static void main(String... args){
	String argType = (args.length == 0 ? "" : args[0]);
	try {
	    Class<?> c = Class.forName("ConstructorTroubleAgain");
	    if ("".equals(argType)) {
		// IllegalArgumentException: wrong number of arguments
		Object o = c.getConstructor().newInstance("foo");
	    } else if ("int".equals(argType)) {
		// NoSuchMethodException - looking for int, have Integer
		Object o = c.getConstructor(int.class);
	    } else if ("Object".equals(argType)) {
		// newInstance() does not perform method resolution
		Object o = c.getConstructor(Object.class).newInstance("foo");
	    } else {
		assert false;
	    }

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java ConstructorTroubleAgain*

```
Exception in thread "main" java.lang.IllegalArgumentException: wrong number of
  arguments
        at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
        at sun.reflect.NativeConstructorAccessorImpl.newInstance
          (NativeConstructorAccessorImpl.java:39)
        at sun.reflect.DelegatingConstructorAccessorImpl.newInstance
          (DelegatingConstructorAccessorImpl.java:27)
        at java.lang.reflect.Constructor.newInstance(Constructor.java:513)
        at ConstructorTroubleAgain.main(ConstructorTroubleAgain.java:23)
```

抛出 [`IllegalArgumentException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html) ，因为请求了零参数构造函数并尝试传递参数。如果构造函数传递了错误类型的参数，则会抛出相同的异常。

$ *java ConstructorTroubleAgain int*

```
java.lang.NoSuchMethodException: ConstructorTroubleAgain.<init>(int)
        at java.lang.Class.getConstructor0(Class.java:2706)
        at java.lang.Class.getConstructor(Class.java:1657)
        at ConstructorTroubleAgain.main(ConstructorTroubleAgain.java:26)
```

如果开发人员错误地认为反射将是自动装箱或拆箱类型，则可能会发生此异常。装箱（将基元转换为引用类型）仅在编译期间发生。反射中没有机会发生此操作，因此在查找构造函数时必须使用特定类型。

$ *java ConstructorTroubleAgain Object*

```
Constructor passed Object
```

在这里，可能需要调用带有 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 参数的构造函数，因为 `newInstance()` 是使用更具体的`String`类型调用的。但是为时已晚！找到的构造函数已经是具有 [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 参数的构造函数。`newInstance()` 不会尝试进行方法解析；它只是对现有的构造函数对象进行操作。

------

**提示：**`new`和 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 之间的一个重要区别是`new`执行方法参数类型检查，装箱和方法解析。这些都不会发生在反射中，必须做出明确的选择。

------

**尝试调用不可访问的构造器时发生 IllegalAccessException**

 [`IllegalAccessException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalAccessException.html) 会被抛出，如果尝试调用一个`private`或者其它不可访问的构造器。下面的例子展示了产生的异常栈跟踪信息：

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;

class Deny {
    private Deny() {
	System.out.format("Deny constructor%n");
    }
}

public class ConstructorTroubleAccess {
    public static void main(String... args) {
	try {
	    Constructor c = Deny.class.getDeclaredConstructor();
//  	    c.setAccessible(true);   // solution
	    c.newInstance();

        // production code should handle these exceptions more gracefully
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java ConstructorTroubleAccess*

```
java.lang.IllegalAccessException: Class ConstructorTroubleAccess can not access
  a member of class Deny with modifiers "private"
        at sun.reflect.Reflection.ensureMemberAccess(Reflection.java:65)
        at java.lang.reflect.Constructor.newInstance(Constructor.java:505)
        at ConstructorTroubleAccess.main(ConstructorTroubleAccess.java:15)
```

------

**提示：**存在一个访问限制，它阻止了通常无法通过直接调用访问的构造函数的反射调用。（这包括但不限于单独类中的私有构造函数和单独私有类中的公共构造函数。）但是，`Constructor` 声明为扩展了[`AccessibleObject`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html) ，它提供了通过[`AccessibleObject.setAccessible()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html#setAccessible-boolean-)来抑制此检查的功能。

------

