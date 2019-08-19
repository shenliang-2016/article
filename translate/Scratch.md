#### 故障排除

本节包含开发人员在使用反射来查找，调用或获取有关方法的信息时可能遇到的问题的示例。

**类型擦除导致的 NoSuchMethodException**

 [`MethodTrouble`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodTrouble.java) 示例展示了当在一个类中搜索特定方法的代码没有考虑类型擦除时将会发生什么：

```java
import java.lang.reflect.Method;

public class MethodTrouble<T>  {
    public void lookup(T t) {}
    public void find(Integer i) {}

    public static void main(String... args) {
	try {
	    String mName = args[0];
	    Class cArg = Class.forName(args[1]);
	    Class<?> c = (new MethodTrouble<Integer>()).getClass();
	    Method m = c.getMethod(mName, cArg);
	    System.out.format("Found:%n  %s%n", m.toGenericString());

        // production code should handle these exceptions more gracefully
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java MethodTrouble lookup java.lang.Integer*

```java
java.lang.NoSuchMethodException: MethodTrouble.lookup(java.lang.Integer)
        at java.lang.Class.getMethod(Class.java:1605)
        at MethodTrouble.main(MethodTrouble.java:12)
```

$ *java MethodTrouble lookup java.lang.Object*

```
Found:
  public void MethodTrouble.lookup(T)
```

当一个方法被声明为使用泛型类型参数，编译器将使用泛型类型的上界替换该泛型类型。示例中的情况下，`T`的上界是`Object`。因此，当代码搜索`lookup(Integer)`时，找不到方法，尽管`MethodTrouble`示例被创建如下：

```java
Class<?> c = (new MethodTrouble<Integer>()).getClass();
```

寻找 `lookup(Object)` 意料之中的成功。

$ *java MethodTrouble find java.lang.Integer*

```
Found:
  public void MethodTrouble.find(java.lang.Integer)
```

$ *java MethodTrouble find java.lang.Object*

````
java.lang.NoSuchMethodException: MethodTrouble.find(java.lang.Object)
        at java.lang.Class.getMethod(Class.java:1605)
        at MethodTrouble.main(MethodTrouble.java:12)
````

这种情况下，`find()`没有泛型参数，因而 [`getMethod()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getMethod-java.lang.String-java.lang.Class...-) 方法搜索的方法的参数类型必须精确匹配。

------

**提示：** 当搜索方法时永远传递参数化类型的类型上界。

------

**调用方法时发生 IllegalAccessException**

试图调用一个`private`或者其它的不可访问方法时将抛出 [`IllegalAccessException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalAccessException.html) 。

 [`MethodTroubleAgain`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodTroubleAgain.java) 示例展示一个典型的调用栈轨迹，它由调用其它类中的一个`private`方法尝试产生。

```java
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

class AnotherClass {
    private void m() {}
}

public class MethodTroubleAgain {
    public static void main(String... args) {
	AnotherClass ac = new AnotherClass();
	try {
	    Class<?> c = ac.getClass();
 	    Method m = c.getDeclaredMethod("m");
//  	    m.setAccessible(true);      // solution
 	    Object o = m.invoke(ac);    // IllegalAccessException

        // production code should handle these exceptions more gracefully
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

异常栈如下：

$ *java MethodTroubleAgain*

```
java.lang.IllegalAccessException: Class MethodTroubleAgain can not access a
  member of class AnotherClass with modifiers "private"
        at sun.reflect.Reflection.ensureMemberAccess(Reflection.java:65)
        at java.lang.reflect.Method.invoke(Method.java:588)
        at MethodTroubleAgain.main(MethodTroubleAgain.java:15)
```

------

**提示：**存在访问限制，阻止反射调用通常无法通过直接调用访问的方法。（这包括---但不限于 - 单独的类中的`private`方法和单独的`private`类中`public`方法。）但是，声明`Method`扩展了`AccessibleObject`，它提供了通过`AccessibleObject.setAccessible()`来抑制此检查的能力。如果成功，则此方法对象的后续调用不会因此问题而失败。

------

**来自 `Method.invoke()` 的 IllegalArgumentException**

[`Method.invoke()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-) has been retrofitted to be a variable-arity method. This is an enormous convenience, however it can lead to unexpected behavior. The [`MethodTroubleToo`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodTroubleToo.java)example shows various ways in which [`Method.invoke()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-) can produce confusing results.

[`Method.invoke()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-) 已被改进为可变参数方法。这是一个巨大的便利，但它可能导致意外的行为。 [`MethodTroubleToo`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodTroubleToo.java) 示例显示了 [`Method.invoke()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-)  可以产生令人困惑的结果的各种方法。

```java
import java.lang.reflect.Method;

public class MethodTroubleToo {
    public void ping() { System.out.format("PONG!%n"); }

    public static void main(String... args) {
	try {
	    MethodTroubleToo mtt = new MethodTroubleToo();
	    Method m = MethodTroubleToo.class.getMethod("ping");

 	    switch(Integer.parseInt(args[0])) {
	    case 0:
  		m.invoke(mtt);                 // works
		break;
	    case 1:
 		m.invoke(mtt, null);           // works (expect compiler warning)
		break;
	    case 2:
		Object arg2 = null;
		m.invoke(mtt, arg2);           // IllegalArgumentException
		break;
	    case 3:
		m.invoke(mtt, new Object[0]);  // works
		break;
	    case 4:
		Object arg4 = new Object[0];
		m.invoke(mtt, arg4);           // IllegalArgumentException
		break;
	    default:
		System.out.format("Test not found%n");
	    }

        // production code should handle these exceptions more gracefully
	} catch (Exception x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java MethodTroubleToo 0*

```
PONG!
```

除了第一个参数， [`Method.invoke()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#invoke-java.lang.Object-java.lang.Object...-) 的所有参数都是可选的，它们可以被忽略，当方法被以无参方式调用时。

$ *java MethodTroubleToo 1*

```
PONG!
```

这种情况下该代码会产生编译器警告，因为`null`是不明确的。

$ *javac MethodTroubleToo.java*

```
MethodTroubleToo.java:16: warning: non-varargs call of varargs method with
  inexact argument type for last parameter;
 		m.invoke(mtt, null);           // works (expect compiler warning)
 		              ^
  cast to Object for a varargs call
  cast to Object[] for a non-varargs call and to suppress this warning
1 warning
```

无法确定`null`是表示空数组参数还是第一个参数是`null`。

$ *java MethodTroubleToo 2*

```
java.lang.IllegalArgumentException: wrong number of arguments
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke
          (NativeMethodAccessorImpl.java:39)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke
          (DelegatingMethodAccessorImpl.java:25)
        at java.lang.reflect.Method.invoke(Method.java:597)
        at MethodTroubleToo.main(MethodTroubleToo.java:21)
```

尽管参数为`null`，但由于类型是`Object`而`ping()`完全不需要参数，因此失败。

$ *java MethodTroubleToo 3*

```
PONG!
```

这是有效的，因为 `new Object[0]` 创建一个空数组，而对于可变参数方法，这相当于不传递任何可选参数。

$ *java MethodTroubleToo 4*

```
java.lang.IllegalArgumentException: wrong number of arguments
        at sun.reflect.NativeMethodAccessorImpl.invoke0
          (Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke
          (NativeMethodAccessorImpl.java:39)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke
          (DelegatingMethodAccessorImpl.java:25)
        at java.lang.reflect.Method.invoke(Method.java:597)
        at MethodTroubleToo.main(MethodTroubleToo.java:28)
```

不同于前面的例子，如果空数组被存储在一个 [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 中，则它会被作为一个 [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 对待。此时失败的原因与第二种情况相同， `ping()` 不期待任何参数。

------

**提示：**当声明方法 `foo(Object... o)` 时，编译器会将传递给`foo()` 的所有参数放入`Object`类型的数组中。`foo()`的实现与声明为`foo(Object[] o)`的实现相同。理解这可能有助于避免上述类型问题。

----

**当调用方法失败时产生的 InvocationTargetException**

 [`InvocationTargetException`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html) 包装调用方法对象时生成的所有异常（已检查和未检查）。 [`MethodTroubleReturns`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodTroubleReturns.java) 示例显示如何检索被调用方法抛出的原始异常。

```java
import java.lang.reflect.InvocationTargetException;
import java.lang.reflect.Method;

public class MethodTroubleReturns {
    private void drinkMe(int liters) {
	if (liters < 0)
	    throw new IllegalArgumentException("I can't drink a negative amount of liquid");
    }

    public static void main(String... args) {
	try {
	    MethodTroubleReturns mtr  = new MethodTroubleReturns();
 	    Class<?> c = mtr.getClass();
   	    Method m = c.getDeclaredMethod("drinkMe", int.class);
	    m.invoke(mtr, -1);

        // production code should handle these exceptions more gracefully
	} catch (InvocationTargetException x) {
	    Throwable cause = x.getCause();
	    System.err.format("drinkMe() failed: %s%n", cause.getMessage());
	} catch (Exception x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java MethodTroubleReturns*

```
drinkMe() failed: I can't drink a negative amount of liquid
```

------

**提示：**如果抛出 [`InvocationTargetException`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html) ，则该方法被调用。问题的诊断与直接调用该方法并抛出 [`getCause()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html#getCause--) 检索的异常相同。此异常并不表示反射包或其用法存在问题。

------

