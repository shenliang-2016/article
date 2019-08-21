#### 故障排除

接下面举例说明在操作数组时可能遇到的典型错误。

**不可转化类型导致的 IllegalArgumentException**

 [`ArrayTroubleAgain`](https://docs.oracle.com/javase/tutorial/reflect/special/example/ArrayTroubleAgain.java) 示例将产生 [`IllegalArgumentException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html) 。 [`Array.setInt()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#setInt-java.lang.Object-int-int-) 被调用以设定一个元素的值，该元素是引用类型`Integer`，赋予它的值是基本数据类型`int`值。在非反射式等待代码`ary[0]=0`中，编译器将转化（或者装箱）值`1`为引用类型`new Integer(1)`，从而该语句将通过类型检查。当使用反射时，类型检查只会在运行时发生，因而没有机会进行类型装箱。

```java
import java.lang.reflect.Array;
import static java.lang.System.err;

public class ArrayTroubleAgain {
    public static void main(String... args) {
	Integer[] ary = new Integer[2];
	try {
	    Array.setInt(ary, 0, 1);  // IllegalArgumentException

        // production code should handle these exceptions more gracefully
	} catch (IllegalArgumentException x) {
	    err.format("Unable to box%n");
	} catch (ArrayIndexOutOfBoundsException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java ArrayTroubleAgain*

```
Unable to box
```

为了消除此异常，有问题的代码行应该修改为如下对 [`Array.set(Object array, int index, Object value)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#set-java.lang.Object-int-java.lang.Object-) 的调用：

```java
Array.set(ary, 0, new Integer(1));
```

----

**提示：**

当使用反射设置或者获取数组元素时，编译器没有机会执行自动装箱。它仅仅可以转化那些在 `Class.isAssignableFrom()` 规范中描述的相关类型。上面的例子会失败，因为在这个测试中 `isAssignableFrom()` 将返回 `false`。该方法可以被用来校验一个特定转化是否可行：

```java
Integer.class.isAssignableFrom(int.class) == false 
```

类似地，从基本数据类型向引用类型的自动转化在反射中也是不可能的。

```java
int.class.isAssignableFrom(Integer.class) == false
```

----

**空数组导致的 ArrayIndexOutOfBoundsException**

 [`ArrayTrouble`](https://docs.oracle.com/javase/tutorial/reflect/special/example/ArrayTrouble.java) 示例展示了当试图访问一个长度为 0 的数组的元素时将会发生的错误。

```java
import java.lang.reflect.Array;
import static java.lang.System.out;

public class ArrayTrouble {
    public static void main(String... args) {
        Object o = Array.newInstance(int.class, 0);
        int[] i = (int[])o;
        int[] j = new int[0];
        out.format("i.length = %d, j.length = %d, args.length = %d%n",
                   i.length, j.length, args.length);
        Array.getInt(o, 0);  // ArrayIndexOutOfBoundsException
    }
}
```

$ *java ArrayTrouble*

```
i.length = 0, j.length = 0, args.length = 0
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException
        at java.lang.reflect.Array.getInt(Native Method)
        at ArrayTrouble.main(ArrayTrouble.java:11)
```

------

**提示：**没有元素的数组（空数组）是可能存在的。尽管在通常的代码中很少见，还是有可能会发生意外的反射的情况。当然，不可能设定或者获取一个空数组的元素值，因为这种操作会抛出 [`ArrayIndexOutOfBoundsException`](https://docs.oracle.com/javase/8/docs/api/java/lang/ArrayIndexOutOfBoundsException.html) 。

------

**试图类型缩窄导致的 IllegalArgumentException**

 [`ArrayTroubleToo`](https://docs.oracle.com/javase/tutorial/reflect/special/example/ArrayTroubleToo.java) 示例包含会失败的代码，这些代码试图执行某些可能会导致数据丢失的操作。

```java
import java.lang.reflect.Array;
import static java.lang.System.out;

public class ArrayTroubleToo {
    public static void main(String... args) {
        Object o = new int[2];
        Array.setShort(o, 0, (short)2);  // widening, succeeds
        Array.setLong(o, 1, 2L);         // narrowing, fails
    }
}
```

$ *java ArrayTroubleToo*

```
Exception in thread "main" java.lang.IllegalArgumentException: argument type
  mismatch
        at java.lang.reflect.Array.setLong(Native Method)
        at ArrayTroubleToo.main(ArrayTroubleToo.java:9)
```

------

**提示：**`Array.set*()` 和 `Array.get*()` 方法将执行自动类型扩宽转化，但是如果试图进行类型缩窄就会抛出 [`IllegalArgumentException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html) 。关于类型扩宽和缩窄的完整讨论参见 [*The Java Language Specification, Java SE 7 Edition*](https://docs.oracle.com/javase/specs/jls/se7/html/index.html) 中的 [Widening Primitive Conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.2) 和 [Narrowing Primitive Conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.3) 章节。

------

