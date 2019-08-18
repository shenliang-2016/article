#### 故障排除

这里介绍几种开发者通常可能会碰到的问题，同时解释它们发生的原因以及解决方法。

**不可转化类型导致的 IllegalArgumentException**

 [`FieldTrouble`](https://docs.oracle.com/javase/tutorial/reflect/member/example/FieldTrouble.java) 示例将产生 [`IllegalArgumentException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html). [`Field.setInt()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#setInt-java.lang.Object-int-) 被调用来将一个引用类型`Integer`字段的值设置为一个基本数据类型的值。在非反射等价形式`Integer val = 42`中，编译器将原始类型`42`转换（或*装箱*）为引用类型为`new Integer（42）`，以便其类型检查接受该语句。使用反射时，类型检查仅在运行时进行，因此没有机会对值进行装箱。

```java
import java.lang.reflect.Field;

public class FieldTrouble {
    public Integer val;

    public static void main(String... args) {
	FieldTrouble ft = new FieldTrouble();
	try {
	    Class<?> c = ft.getClass();
	    Field f = c.getDeclaredField("val");
  	    f.setInt(ft, 42);               // IllegalArgumentException

        // production code should handle these exceptions more gracefully
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
 	} catch (IllegalAccessException x) {
 	    x.printStackTrace();
	}
    }
}
```

$ *java FieldTrouble*

````
Exception in thread "main" java.lang.IllegalArgumentException: Can not set
  java.lang.Object field FieldTrouble.val to (long)42
        at sun.reflect.UnsafeFieldAccessorImpl.throwSetIllegalArgumentException
          (UnsafeFieldAccessorImpl.java:146)
        at sun.reflect.UnsafeFieldAccessorImpl.throwSetIllegalArgumentException
          (UnsafeFieldAccessorImpl.java:174)
        at sun.reflect.UnsafeObjectFieldAccessorImpl.setLong
          (UnsafeObjectFieldAccessorImpl.java:102)
        at java.lang.reflect.Field.setLong(Field.java:831)
        at FieldTrouble.main(FieldTrouble.java:11)
````

为了消除此异常，应该使用 [`Field.set(Object obj, Object value)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#set-java.lang.Object-java.lang.Object-) 方法调用替换有问题的代码：

```java
f.set(ft, new Integer(43));
```

----

**提示：**当使用反射来设置或者获取字段时，编译器没有机会执行自动装箱。它只能转化那些[`Class.isAssignableFrom()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isAssignableFrom-java.lang.Class-) 规范中描述的有关数据类型。此示例应该会失败，因为在这种编程方式验证一个特定的转化是否可行的测试中  `isAssignableFrom()`  将会返回`false`：

```java
Integer.class.isAssignableFrom(int.class) == false
```

类似的，从基本数据类型到引用类型的自动转化在反射中也是不可能的。

```java
int.class.isAssignableFrom(Integer.class) == false
```

----

**非`public`字段导致的 NoSuchFieldException**

精明的读者可能会注意到，如果前面显示的 [`FieldSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/FieldSpy.java) 示例用于获取非`public`字段，它将失败：

$ *java FieldSpy java.lang.String count*

```
java.lang.NoSuchFieldException: count
        at java.lang.Class.getField(Class.java:1519)
        at FieldSpy.main(FieldSpy.java:12)
```

----

**提示：** [`Class.getField()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getField-java.lang.String  - )和[`Class.getFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getFields--)方法返回由`Class`对象表示的类，枚举或接口的*public*成员字段。要检索`Class`中声明（但不是继承）的所有字段，请使用[`Class.getDeclaredFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredFields--) 方法。

----

**修改`final`字段时发生 IllegalAccessException**

如果尝试获取或设置`private`或其他不可访问的字段或设置`final`字段的值（不管其访问修饰符是啥）的值，则可能抛出 [`IllegalAccessException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalAccessException.html) 。

[`FieldTroubleToo`](https://docs.oracle.com/javase/tutorial/reflect/member/example/FieldTroubleToo.java) 示例说明了尝试设置`final`字段时产生的堆栈跟踪信息。

```java
import java.lang.reflect.Field;

public class FieldTroubleToo {
    public final boolean b = true;

    public static void main(String... args) {
	FieldTroubleToo ft = new FieldTroubleToo();
	try {
	    Class<?> c = ft.getClass();
	    Field f = c.getDeclaredField("b");
// 	    f.setAccessible(true);  // solution
	    f.setBoolean(ft, Boolean.FALSE);   // IllegalAccessException

        // production code should handle these exceptions more gracefully
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	} catch (IllegalArgumentException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java FieldTroubleToo*

````
java.lang.IllegalAccessException: Can not set final boolean field
  FieldTroubleToo.b to (boolean)false
        at sun.reflect.UnsafeFieldAccessorImpl.
          throwFinalFieldIllegalAccessException(UnsafeFieldAccessorImpl.java:55)
        at sun.reflect.UnsafeFieldAccessorImpl.
          throwFinalFieldIllegalAccessException(UnsafeFieldAccessorImpl.java:63)
        at sun.reflect.UnsafeQualifiedBooleanFieldAccessorImpl.setBoolean
          (UnsafeQualifiedBooleanFieldAccessorImpl.java:78)
        at java.lang.reflect.Field.setBoolean(Field.java:686)
        at FieldTroubleToo.main(FieldTroubleToo.java:12)
````

----

**提示：**存在一个访问限制，它阻止在初始化类之后设置`final`字段。但是，被声明为扩展了[`AccessibleObject`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html)的`Field`，提供了抑制此校验功能的能力。

如果 [`AccessibleObject.setAccessible()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html#setAccessible-boolean-) 成功，则后续操作 此字段值不会因为此问题而失败。这可能会产生意想不到的副作用：例如，有时原始值将继续被应用程序的某些部分使用，即使该值已被修改。[`AccessibleObject.setAccessible()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html#setAccessible-boolean-) 只有在安全上下文允许该操作时才会成功。

----

