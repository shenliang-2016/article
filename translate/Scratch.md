方法声明包含方法名称、修饰符、参数、返回类型、以及抛出的异常列表。 [`java.lang.reflect.Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html) 类提供了获取这些信息的方法。

 [`MethodSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodSpy.java) 示例展示了如何列出给定的类中所有声明的方法。同时获取所有给定名称的方法的返回类型、参数以及异常类型。

```java
import java.lang.reflect.Method;
import java.lang.reflect.Type;
import static java.lang.System.out;

public class MethodSpy {
    private static final String  fmt = "%24s: %s%n";

    // for the morbidly curious
    <E extends RuntimeException> void genericThrow() throws E {}

    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    Method[] allMethods = c.getDeclaredMethods();
	    for (Method m : allMethods) {
		if (!m.getName().equals(args[1])) {
		    continue;
		}
		out.format("%s%n", m.toGenericString());

		out.format(fmt, "ReturnType", m.getReturnType());
		out.format(fmt, "GenericReturnType", m.getGenericReturnType());

		Class<?>[] pType  = m.getParameterTypes();
		Type[] gpType = m.getGenericParameterTypes();
		for (int i = 0; i < pType.length; i++) {
		    out.format(fmt,"ParameterType", pType[i]);
		    out.format(fmt,"GenericParameterType", gpType[i]);
		}

		Class<?>[] xType  = m.getExceptionTypes();
		Type[] gxType = m.getGenericExceptionTypes();
		for (int i = 0; i < xType.length; i++) {
		    out.format(fmt,"ExceptionType", xType[i]);
		    out.format(fmt,"GenericExceptionType", gxType[i]);
		}
	    }

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

下面是 [`Class.getConstructor()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getConstructor-java.lang.Class...-) 的输出，它的参数具有参数化类型，而且参数个数可变。

$ *java MethodSpy java.lang.Class getConstructor*

```
public java.lang.reflect.Constructor<T> java.lang.Class.getConstructor
  (java.lang.Class<?>[]) throws java.lang.NoSuchMethodException,
  java.lang.SecurityException
              ReturnType: class java.lang.reflect.Constructor
       GenericReturnType: java.lang.reflect.Constructor<T>
           ParameterType: class [Ljava.lang.Class;
    GenericParameterType: java.lang.Class<?>[]
           ExceptionType: class java.lang.NoSuchMethodException
    GenericExceptionType: class java.lang.NoSuchMethodException
           ExceptionType: class java.lang.SecurityException
    GenericExceptionType: class java.lang.SecurityException
```

下面是源代码中实际的方法声明：

```java
public Constructor<T> getConstructor(Class<?>... parameterTypes)
```

首先，注意其返回类型和参数类型都是泛型。 [`Method.getGenericReturnType()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getGenericReturnType--) 将从类文件中查询签名属性，如果该类文件存在。如果属性不可用，该方法会退化为 [`Method.getReturnType()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getReturnType--) ，此方法在引入泛型前后没有变化。名为`getGeneric*Foo*()`的方法来通过反射获取*Foo*的某些值的实现与此类似。

其次，注意最后一个（仅仅是最后一个）参数，`parameterType` ，是数量可变的`java.lang.Class`类型的参数。通常表现为`java.lang.Class`类型数据的一维数组。这种参数可以通过调用 [`Method.isVarArgs()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#isVarArgs--) 来区别于显式的 `java.lang.Class` 类型数组参数。`Method.get*Types()`方法的返回值语法在 [`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--) 中描述。

下面的例子展示了泛型返回类型方法。

$ *java MethodSpy java.lang.Class cast*

```
public T java.lang.Class.cast(java.lang.Object)
              ReturnType: class java.lang.Object
       GenericReturnType: T
           ParameterType: class java.lang.Object
    GenericParameterType: class java.lang.Object
```

方法 [`Class.cast()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#cast-java.lang.Object-) 的泛型返回类型被报告为 `java.lang.Object`，因为泛型是通过类型擦除实现，类型擦除会在编译期清楚所有的泛型相关的类型信息。`T`的擦除由 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 的声明定义：

```java
public final class Class<T> implements ...
```

因此，`T`被类型变量的上界替换，这种情况下，就是 `java.lang.Object` 。

最后一个示例说明了具有多个重载的方法的输出。

$ *java MethodSpy java.io.PrintStream format*

```
public java.io.PrintStream java.io.PrintStream.format
  (java.util.Locale,java.lang.String,java.lang.Object[])
              ReturnType: class java.io.PrintStream
       GenericReturnType: class java.io.PrintStream
           ParameterType: class java.util.Locale
    GenericParameterType: class java.util.Locale
           ParameterType: class java.lang.String
    GenericParameterType: class java.lang.String
           ParameterType: class [Ljava.lang.Object;
    GenericParameterType: class [Ljava.lang.Object;
public java.io.PrintStream java.io.PrintStream.format
  (java.lang.String,java.lang.Object[])
              ReturnType: class java.io.PrintStream
       GenericReturnType: class java.io.PrintStream
           ParameterType: class java.lang.String
    GenericParameterType: class java.lang.String
           ParameterType: class [Ljava.lang.Object;
    GenericParameterType: class [Ljava.lang.Object;
```

如果发现同一个方法的多个重载，它们都会被 [`Class.getDeclaredMethods()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredMethods--) 返回。由于 `format()` 有两个重载（携带 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 的和不携带的），都会被 `MethodSpy` 展示。

----

**注意：** [`Method.getGenericExceptionTypes()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getGenericExceptionTypes--) 存在，因为声明抛出泛型异常类型的方法是可能的。不过这种情况很罕见，因为我们不可能捕获泛型异常类型。

----

