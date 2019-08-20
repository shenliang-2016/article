#### 检索并解析构造器修饰符

由于构造器在语言中的特殊角色，相对于普通方法，只有少数几个修饰符可用于构造器：

- 访问修饰符： `public` ， `protected` ，和 `private`
- 注解

 [`ConstructorAccess`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ConstructorAccess.java) 示例在给定类中检索具有特定访问修饰符的构造器。它还显示构造器是否是合成的（编译器生成的）或者是否是可变参数的。

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.Modifier;
import java.lang.reflect.Type;
import static java.lang.System.out;

public class ConstructorAccess {
    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    Constructor[] allConstructors = c.getDeclaredConstructors();
	    for (Constructor ctor : allConstructors) {
		int searchMod = modifierFromString(args[1]);
		int mods = accessModifiers(ctor.getModifiers());
		if (searchMod == mods) {
		    out.format("%s%n", ctor.toGenericString());
		    out.format("  [ synthetic=%-5b var_args=%-5b ]%n",
			       ctor.isSynthetic(), ctor.isVarArgs());
		}
	    }

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }

    private static int accessModifiers(int m) {
	return m & (Modifier.PUBLIC | Modifier.PRIVATE | Modifier.PROTECTED);
    }

    private static int modifierFromString(String s) {
	if ("public".equals(s))               return Modifier.PUBLIC;
	else if ("protected".equals(s))       return Modifier.PROTECTED;
	else if ("private".equals(s))         return Modifier.PRIVATE;
	else if ("package-private".equals(s)) return 0;
	else return -1;
    }
}
```

不存在对应于`package-private`访问的显式 [`Modifier`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Modifier.html) 常量，因此有必要检查所有三种访问修饰符都不存在的情况以标识一个`package-private`构造器。

下面的输出展示了 [`java.io.File`](https://docs.oracle.com/javase/8/docs/api/java/io/File.html) 中的`private`构造器：

$ *java ConstructorAccess java.io.File private*

```
private java.io.File(java.lang.String,int)
  [ synthetic=false var_args=false ]
private java.io.File(java.lang.String,java.io.File)
  [ synthetic=false var_args=false ]
```

合成构造器很少见，不过 [`SyntheticConstructor`](https://docs.oracle.com/javase/tutorial/reflect/member/example/SyntheticConstructor.java) 示例展示了这种情况可能发生的典型情况：

```java
public class SyntheticConstructor {
    private SyntheticConstructor() {}
    class Inner {
	// Compiler will generate a synthetic constructor since
	// SyntheticConstructor() is private.
	Inner() { new SyntheticConstructor(); }
    }
}
```

$ *java ConstructorAccess SyntheticConstructor package-private*

```
SyntheticConstructor(SyntheticConstructor$1)
  [ synthetic=true  var_args=false ]
```

因为内部类构造器引用它所在的外部类的`private`构造器，编译器必须生成一个`package-private`构造器。参数类型 `SyntheticConstructor$1` 是任意的，依赖于编译器实现。依赖于任何合成的或者非`public`类成员的代码都是不可移植的。

构造器实现了 [`java.lang.reflect.AnnotatedElement`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AnnotatedElement.html) ，提供了检索携带 [`java.lang.annotation.RetentionPolicy.RUNTIME`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html#RUNTIME) 的运行时注解的方法。获取注解的例子参考 [Examining Class Modifiers and Types](https://docs.oracle.com/javase/tutorial/reflect/class/classModifiers.html) 章节。

#### 创建新的类实例

存在两种反射式方法来创建类实例： [`java.lang.reflect.Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 和 [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 。前者相对较好，因此在这些例子中使用。因为：

- [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 只能调用无参构造器，而 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 可以调用任何构造器，无论有多少个参数。
- [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 抛出构造器抛出的任何异常，无论是受检查的异常还是不受检查的异常。[`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 始终将抛出的异常包装为 [`InvocationTargetException`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/InvocationTargetException.html).
- [`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 需要构造器是可见的； [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 在某些环境下可以调用 `private` 构造器。

有时可能需要从仅在构造之后设置的对象检索内部状态。考虑一种需要获取 [`java.io.Console`](https://docs.oracle.com/javase/8/docs/api/java/io/Console.html) 使用的内部字符集的场景。（`Console`字符集存储在私有字段中，不一定与  [`java.nio.charset.Charset.defaultCharset()`](https://docs.oracle.com/javase/8/docs/api/java/nio/charset/Charset.html#defaultCharset--) 返回的Java虚拟机缺省字符集相同。[`ConsoleCharset`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ConsoleCharset.java) 示例显示了如何实现此目的：

```java
import java.io.Console;
import java.nio.charset.Charset;
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import static java.lang.System.out;

public class ConsoleCharset {
    public static void main(String... args) {
	Constructor[] ctors = Console.class.getDeclaredConstructors();
	Constructor ctor = null;
	for (int i = 0; i < ctors.length; i++) {
	    ctor = ctors[i];
	    if (ctor.getGenericParameterTypes().length == 0)
		break;
	}

	try {
	    ctor.setAccessible(true);
 	    Console c = (Console)ctor.newInstance();
	    Field f = c.getClass().getDeclaredField("cs");
	    f.setAccessible(true);
	    out.format("Console charset         :  %s%n", f.get(c));
	    out.format("Charset.defaultCharset():  %s%n",
		       Charset.defaultCharset());

        // production code should handle these exceptions more gracefully
	} catch (InstantiationException x) {
	    x.printStackTrace();
 	} catch (InvocationTargetException x) {
 	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	}
    }
}
```

------

**注意：**

[`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 只有当构造器是无参的并且是可访问时才会成功。否则，有必要像上面的例子那样使用[`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 。

------

例子在 UNIX 系统上的输出：

$ *java ConsoleCharset*

```
Console charset          :  ISO-8859-1
Charset.defaultCharset() :  ISO-8859-1
```

例子在 Windows 系统上的输出：

C:\> *java ConsoleCharset*

```
Console charset          :  IBM437
Charset.defaultCharset() :  windows-1252
```

 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 的另一个常见应用是调用带参数的构造函数。 [`RestoreAliases`](https://docs.oracle.com/javase/tutorial/reflect/member/example/RestoreAliases.java) 示例查找特定的单参数构造函数并调用它：

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.InvocationTargetException;
import java.util.HashMap;
import java.util.Map;
import java.util.Set;
import static java.lang.System.out;

class EmailAliases {
    private Set<String> aliases;
    private EmailAliases(HashMap<String, String> h) {
	aliases = h.keySet();
    }

    public void printKeys() {
	out.format("Mail keys:%n");
	for (String k : aliases)
	    out.format("  %s%n", k);
    }
}

public class RestoreAliases {

    private static Map<String, String> defaultAliases = new HashMap<String, String>();
    static {
	defaultAliases.put("Duke", "duke@i-love-java");
	defaultAliases.put("Fang", "fang@evil-jealous-twin");
    }

    public static void main(String... args) {
	try {
	    Constructor ctor = EmailAliases.class.getDeclaredConstructor(HashMap.class);
	    ctor.setAccessible(true);
	    EmailAliases email = (EmailAliases)ctor.newInstance(defaultAliases);
	    email.printKeys();

        // production code should handle these exceptions more gracefully
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	} catch (NoSuchMethodException x) {
	    x.printStackTrace();
	}
    }
}
```

此示例使用 [`Class.getDeclaredConstructor()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredConstructor-java.lang.Class...-) 来查找具有 [`java.util.HashMap`](https://docs.oracle.com/javase/8/docs/api/java/util/HashMap.html) 类型的单个参数的构造函数。请注意，传递`HashMap.class`就足够了，因为任何`get*Constructor()`方法的参数需要类只用于类型目的。由于 [类型擦除](https://docs.oracle.com/javase/specs/jls/se7/html/jls-4.html#jls-4.6) ，以下表达式的计算结果为`true`：

```java
HashMap.class == defaultAliases.getClass()
```

此例子然后创建一个新的类实例，通过 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 使用构造器：

$ *java RestoreAliases*

```
Mail keys:
  Duke
  Fang
```

