#### 识别数组类型

数组类型可以通过调用 [`Class.isArray()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isArray--) 来识别。为了获取 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 使用本课程的 [Retrieving Class Objects](https://docs.oracle.com/javase/tutorial/reflect/class/classNew.html) 章节中描述的方法之一。

 [`ArrayFind`](https://docs.oracle.com/javase/tutorial/reflect/special/example/ArrayFind.java) 示例识别命名的类中的数组类型的字段，并报告它们的元素类型。

```java
import java.lang.reflect.Field;
import java.lang.reflect.Type;
import static java.lang.System.out;

public class ArrayFind {
    public static void main(String... args) {
	boolean found = false;
 	try {
	    Class<?> cls = Class.forName(args[0]);
	    Field[] flds = cls.getDeclaredFields();
	    for (Field f : flds) {
 		Class<?> c = f.getType();
		if (c.isArray()) {
		    found = true;
		    out.format("%s%n"
                               + "           Field: %s%n"
			       + "            Type: %s%n"
			       + "  Component Type: %s%n",
			       f, f.getName(), c, c.getComponentType());
		}
	    }
	    if (!found) {
		out.format("No array fields%n");
	    }

        // production code should handle this exception more gracefully
 	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

在 [`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--) 中描述了`Class.get*Type()` 的返回值的语法。类型名称开头的'`[`'字符数表示数组的维数（即嵌套深度）。

输出样本如下。用户输入以斜体显示。一个原始类型`byte`的数组：

$ *java ArrayFind java.nio.ByteBuffer*

```
final byte[] java.nio.ByteBuffer.hb
           Field: hb
            Type: class [B
  Component Type: byte
```

引用类型 [`StackTraceElement`](https://docs.oracle.com/javase/8/docs/api/java/lang/StackTraceElement.html) 的数组：

$ *java ArrayFind java.lang.Throwable*

```
private java.lang.StackTraceElement[] java.lang.Throwable.stackTrace
           Field: stackTrace
            Type: class [Ljava.lang.StackTraceElement;
  Component Type: class java.lang.StackTraceElement
```

`predefined`是一个引用类型 [`java.awt.Cursor`](https://docs.oracle.com/javase/8/docs/api/java/awt/Cursor.html) 的一维数组，` cursorProperties`是引用类型 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 的二维数组：

$ *java ArrayFind java.awt.Cursor*

```
protected static java.awt.Cursor[] java.awt.Cursor.predefined
           Field: predefined
            Type: class [Ljava.awt.Cursor;
  Component Type: class java.awt.Cursor
static final java.lang.String[][] java.awt.Cursor.cursorProperties
           Field: cursorProperties
            Type: class [[Ljava.lang.String;
  Component Type: class [Ljava.lang.String;
```

#### 创建新数组

与非反射式代码一样，反射通过 [`java.lang.reflect.Array.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#newInstance-java.lang.Class-int-) 支持动态创建任意类型和维度的数组的能力。考虑[`ArrayCreator`](https://docs.oracle.com/javase/tutorial/reflect/special/example/ArrayCreator.java) ，一个基本的适用于动态创建数组的翻译器。将被解析的语法如下：

```
fully_qualified_class_name variable_name[] = 
     { val1, val2, val3, ... }
```

假设`fully_qualified_class_name`表示一个具有构造函数的类，该构造函数具有单个 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 参数。数组的大小由提供的值的数量决定。下面的例子将构造一个`fully_qualified_class_name`数组的实例，并用`val1`，`val2`等给出的实例填充它的值。（这个例子假设熟悉 [`Class.getConstructor()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getConstructor-java.lang.Class...-) 和[`java.lang.reflect.Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 。关于 [`Constructor`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html) 反射 API 的讨论参见 [Creating New Class Instances](https://docs.oracle.com/javase/tutorial/reflect/member/ctorInstance.html) 部分。）

```java
import java.lang.reflect.Array;
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import java.util.regex.Pattern;
import java.util.regex.Matcher;
import java.util.Arrays;
import static java.lang.System.out;

public class ArrayCreator {
    private static String s = "java.math.BigInteger bi[] = { 123, 234, 345 }";
    private static Pattern p = Pattern.compile("^\\s*(\\S+)\\s*\\w+\\[\\].*\\{\\s*([^}]+)\\s*\\}");

    public static void main(String... args) {
        Matcher m = p.matcher(s);

        if (m.find()) {
            String cName = m.group(1);
            String[] cVals = m.group(2).split("[\\s,]+");
            int n = cVals.length;

            try {
                Class<?> c = Class.forName(cName);
                Object o = Array.newInstance(c, n);
                for (int i = 0; i < n; i++) {
                    String v = cVals[i];
                    Constructor ctor = c.getConstructor(String.class);
                    Object val = ctor.newInstance(v);
                    Array.set(o, i, val);
                }

                Object[] oo = (Object[])o;
                out.format("%s[] = %s%n", cName, Arrays.toString(oo));

            // production code should handle these exceptions more gracefully
            } catch (ClassNotFoundException x) {
                x.printStackTrace();
            } catch (NoSuchMethodException x) {
                x.printStackTrace();
            } catch (IllegalAccessException x) {
                x.printStackTrace();
            } catch (InstantiationException x) {
                x.printStackTrace();
            } catch (InvocationTargetException x) {
                x.printStackTrace();
            }
        }
    }
}
```

$ *java ArrayCreator*

````
java.math.BigInteger [] = [123, 234, 345]
````

上面的例子显示了一种可能需要通过反射创建数组的情况; 即如果直到运行时才知道元素类型。在这种情况下，代码使用 [`Class.forName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#forName--) 来获取所需元素类型的类，然后在设置相应的数组值之前调用特定的构造函数来初始化数组的每个元素。

#### 获取和设置数组和数组元素

正如在非反射代码中一样，可以整体地或逐个元素设置或检索数组元素。要一次设置整个数组，请使用[`java.lang.reflect.Field.set(Object obj, Object value)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#set-java.lang.Object-java.lang.Object-) 。要检索整个数组，请使用 [`Field.get(Object)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#get-java.lang.Object-) 。可以使用[`java.lang.reflect.Array`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html) 中的方法设置或检索单个元素。

[`Array`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html) 提供了 `set*Foo*()` 和 `get*Foo*()`形式的方法用于设置和获取任何基本类型的元素。例如，`int`数组的元素可以用[`Array.setInt(Object array, int index, int value)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#setInt-java.lang.Objectint-int-) 设置，可以使用 [`Array.getInt(Object array, int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#getInt-java.lang.Object-int-) 获取。

这些方法支持数据类型的自动扩宽。因此，[`Array.setShort()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#getShort-java.lang.Object-int-) 可以被用来设定`int`类型数组，因为 16 位的`short`可以被扩宽为 32 位的`int`，而不会丢失数据。另一方面，在`int`数组上调用 [`Array.setLong()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#setLong-java.lang.Object-int-long-) 将会导致抛出  [`IllegalArgumentException`](https://docs.oracle.com/javase/8/docs/api/java/lang/IllegalArgumentException.html) ，因为 64 位的`long`无法在不丢失信息的情况下缩窄为 32 位的`int`。无论传递的实际值是否可以在目标数据类型中准确表示，都是如此。[*The Java Language Specification, Java SE 7 Edition*](https://docs.oracle.com/javase/specs/jls/se7/html/index.html) ， [Widening Primitive Conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.2) 和 [Narrowing Primitive Conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.3) 包含有关数据类型扩宽和缩窄转换的完整讨论。

引用类型数组的元素(包括数组的数组)可以使用 [`Array.set(Object array, int index, int value)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#set-java.lang.Object-int-int-) 和 [`Array.get(Object array, int index)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#get-java.lang.Object-int-) 设定和检索。

**设定类型数组的字段**

[`GrowBufferedReader`](https://docs.oracle.com/javase/tutorial/reflect/special/example/GrowBufferedReader.java) 示例说明了如何替换数组类型字段的值。在这种情况下，代码替换[`java.io.BufferedReader`](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html) 的后备数组为更大的一个。（这假设原始`BufferedReader`的创建是在不可修改的代码中，否则，简单地使用备用构造函数 [`BufferedReader(java.io.Reader in, int size)`](https://docs.oracle.com/javase/8/docs/api/java/io/BufferedReader.html#BufferedReader-java.io.Reader-int-) 将是无意义的，它接受输入缓冲区大小。）

```java
import java.io.BufferedReader;
import java.io.CharArrayReader;
import java.io.FileNotFoundException;
import java.io.IOException;
import java.lang.reflect.Field;
import java.util.Arrays;
import static java.lang.System.out;

public class GrowBufferedReader {
    private static final int srcBufSize = 10 * 1024;
    private static char[] src = new char[srcBufSize];
    static {
	src[srcBufSize - 1] = 'x';
    }
    private static CharArrayReader car = new CharArrayReader(src);

    public static void main(String... args) {
	try {
	    BufferedReader br = new BufferedReader(car);

	    Class<?> c = br.getClass();
	    Field f = c.getDeclaredField("cb");

	    // cb is a private field
	    f.setAccessible(true);
	    char[] cbVal = char[].class.cast(f.get(br));

	    char[] newVal = Arrays.copyOf(cbVal, cbVal.length * 2);
	    if (args.length > 0 && args[0].equals("grow"))
		f.set(br, newVal);

	    for (int i = 0; i < srcBufSize; i++)
		br.read();

	    // see if the new backing array is being used
	    if (newVal[srcBufSize - 1] == src[srcBufSize - 1])
		out.format("Using new backing array, size=%d%n", newVal.length);
	    else
		out.format("Using original backing array, size=%d%n", cbVal.length);

        // production code should handle these exceptions more gracefully
	} catch (FileNotFoundException x) {
	    x.printStackTrace();
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (IOException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java GrowBufferedReader grow*

````
Using new backing array, size=16384
````

$ *java GrowBufferedReader*

````
Using original backing array, size=8192
````

请注意，上面的示例使用了数组实用程序方法 [`java.util.Arrays.copyOf()`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html#copyOf-char:A-int-) 。[`java.util.Arrays`](https://docs.oracle.com/javase/8/docs/api/java/util/Arrays.html) 包含许多在数组上操作时很方便的方法。

**访问多维数组的元素**

多维数组只是嵌套数组。二维数组是一维数组的数组。三维数组是二维数组的数组，依此类推。 [`CreateMatrix`](https://docs.oracle.com/javase/tutorial/reflect/special/example/CreateMatrix.java) 示例说明了如何使用反射创建和初始化多维数组。

```java
import java.lang.reflect.Array;
import static java.lang.System.out;

public class CreateMatrix {
    public static void main(String... args) {
        Object matrix = Array.newInstance(int.class, 2, 2);
        Object row0 = Array.get(matrix, 0);
        Object row1 = Array.get(matrix, 1);

        Array.setInt(row0, 0, 1);
        Array.setInt(row0, 1, 2);
        Array.setInt(row1, 0, 3);
        Array.setInt(row1, 1, 4);

        for (int i = 0; i < 2; i++)
            for (int j = 0; j < 2; j++)
                out.format("matrix[%d][%d] = %d%n", i, j, ((int[][])matrix)[i][j]);
    }
}
```

$ *java CreateMatrix*

````
matrix[0][0] = 1
matrix[0][1] = 2
matrix[1][0] = 3
matrix[1][1] = 4
````

使用以下代码片段可以获得相同的结果：

```java
Object matrix = Array.newInstance(int.class, 2);
Object row0 = Array.newInstance(int.class, 2);
Object row1 = Array.newInstance(int.class, 2);

Array.setInt(row0, 0, 1);
Array.setInt(row0, 1, 2);
Array.setInt(row1, 0, 3);
Array.setInt(row1, 1, 4);

Array.set(matrix, 0, row0);
Array.set(matrix, 1, row1);
```

变量参数 [`Array.newInstance(Class componentType, int... dimensions)`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#newInstance-java.lang.Class-int...-) 提供了一种创建多维数组的便捷方法，但仍需要使用多维数组是嵌套数组的原则来初始化元素。（为此目的，反射不提供多个索引的 `get`/`set` 方法。）

