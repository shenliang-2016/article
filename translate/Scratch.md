### 枚举类型

枚举是一个语言结构，用来定义类型安全的枚举，可以被用于需要一个固定的命名值集合的情况。所有枚举都隐式扩展 [`java.lang.Enum`](https://docs.oracle.com/javase/8/docs/api/java/lang/Enum.html) 。枚举可以包含一个或者多个枚举常量，定义了该枚举类型的独特实例。一个枚举声明定义一个枚举类型，类似于普通的类，它可以包含诸如字段、方法、构造器（有些额外限制）等成员。

因为枚举也是类，反射就不需要显式定义 `java.lang.reflect.Enum` 类。唯一专用于枚举的反射 API 是 [`Class.isEnum()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isEnum--) ，[`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--) ，和 [`java.lang.reflect.Field.isEnumConstant()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isEnumConstant--)。大部分对枚举的反射操作与其它类没啥两样。比如，枚举常量作为枚举类型中的`public static final`字段实现。下面的章节展示如何为枚举使用  [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 和 [`java.lang.reflect.Field`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html) 。 

- [检查枚举](https://docs.oracle.com/javase/tutorial/reflect/special/enumMembers.html) 展示如何获取枚举常量以及任何其它字段、构造器以及方法
- [获取并设定枚举类型的字段](https://docs.oracle.com/javase/tutorial/reflect/special/enumSetGet.html) 展示如何设定和获取枚举常量值字段
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/special/enumTrouble.html) 描述枚举有关的常见错误

对枚举的介绍，请参考 [Enum Types](https://docs.oracle.com/javase/tutorial/java/javaOO/enum.html) 章节。

#### 检查枚举

反射提供了3个枚举专属 API：

- [`Class.isEnum()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isEnum--)

  指明这个类是否表示一个枚举类型

- [`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--)

  按照声明顺序检索由该枚举类定义的枚举常量的列表

- [`java.lang.reflect.Field.isEnumConstant()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isEnumConstant--)

  指明该字段是否表示一个枚举类型元素

有时候我们需要动态地检索枚举常量列表：在非反射式代码中，通过调用枚举上隐式声明的`static`方法  [`values()`](https://docs.oracle.com/javase/specs/jls/se7/html/jls-8.html) 来实现。如果一个枚举类型实例不可用，则获得可能值列表的唯一方法就是调用 [`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--) ，因为枚举类型是不可能实例化的。

给定一个全限定类名， [`EnumConstants`](https://docs.oracle.com/javase/tutorial/reflect/special/example/EnumConstants.java) 示例展示如何使用 [`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--) 检索一个枚举类型中的枚举常量的有序列表。

```java
import java.util.Arrays;
import static java.lang.System.out;

enum Eon { HADEAN, ARCHAEAN, PROTEROZOIC, PHANEROZOIC }

public class EnumConstants {
    public static void main(String... args) {
	try {
	    Class<?> c = (args.length == 0 ? Eon.class : Class.forName(args[0]));
	    out.format("Enum name:  %s%nEnum constants:  %s%n",
		       c.getName(), Arrays.asList(c.getEnumConstants()));
	    if (c == Eon.class)
		out.format("  Eon.values():  %s%n",
			   Arrays.asList(Eon.values()));

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

部分输出如下：

$ *java EnumConstants java.lang.annotation.RetentionPolicy*

```
Enum name:  java.lang.annotation.RetentionPolicy
Enum constants:  [SOURCE, CLASS, RUNTIME]
```

$ *java EnumConstants java.util.concurrent.TimeUnit*

```
Enum name:  java.util.concurrent.TimeUnit
Enum constants:  [NANOSECONDS, MICROSECONDS, 
                  MILLISECONDS, SECONDS, 
                  MINUTES, HOURS, DAYS]
```

这个例子还展示了 [`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--) 的返回值等于调用枚举类型上的`values()`方法的返回值。

$ *java EnumConstants*

```
Enum name:  Eon
Enum constants:  [HADEAN, ARCHAEAN, 
                  PROTEROZOIC, PHANEROZOIC]
Eon.values():  [HADEAN, ARCHAEAN, 
                PROTEROZOIC, PHANEROZOIC]
```

由于枚举是类，因此可以使用此课程的 [Fields](https://docs.oracle.com/javase/tutorial/reflect/member/field.html) ， [Methods](https://docs.oracle.com/javase/tutorial/reflect/member/method.html) ， 和 [Constructors](https://docs.oracle.com/javase/tutorial/reflect/member/ctor.html) 部分中描述的相同反射 API 获取其他信息。[`EnumSpy`](https://docs.oracle.com/javase/tutorial/reflect/special/example/EnumSpy.java)说明了如何使用这些API获取有关枚举声明的其他信息。该示例使用 [`Class.isEnum()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isEnum--) 来限制检查的类集合。它还使用 [`Field.isEnumConstant()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isEnumConstant--) 来区分枚举常量与枚举声明中的其他字段（并非所有字段都是枚举常量）。

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.Field;
import java.lang.reflect.Method;
import java.lang.reflect.Member;
import java.util.List;
import java.util.ArrayList;
import static java.lang.System.out;

public class EnumSpy {
    private static final String fmt = "  %11s:  %s %s%n";

    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    if (!c.isEnum()) {
		out.format("%s is not an enum type%n", c);
		return;
	    }
	    out.format("Class:  %s%n", c);

	    Field[] flds = c.getDeclaredFields();
	    List<Field> cst = new ArrayList<Field>();  // enum constants
	    List<Field> mbr = new ArrayList<Field>();  // member fields
	    for (Field f : flds) {
		if (f.isEnumConstant())
		    cst.add(f);
		else
		    mbr.add(f);
	    }
	    if (!cst.isEmpty())
		print(cst, "Constant");
	    if (!mbr.isEmpty())
		print(mbr, "Field");

	    Constructor[] ctors = c.getDeclaredConstructors();
	    for (Constructor ctor : ctors) {
		out.format(fmt, "Constructor", ctor.toGenericString(),
			   synthetic(ctor));
	    }

	    Method[] mths = c.getDeclaredMethods();
	    for (Method m : mths) {
		out.format(fmt, "Method", m.toGenericString(),
			   synthetic(m));
	    }

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }

    private static void print(List<Field> lst, String s) {
	for (Field f : lst) {
 	    out.format(fmt, s, f.toGenericString(), synthetic(f));
	}
    }

    private static String synthetic(Member m) {
	return (m.isSynthetic() ? "[ synthetic ]" : "");
    }
}
```

$ *java EnumSpy java.lang.annotation.RetentionPolicy*

```
Class:  class java.lang.annotation.RetentionPolicy
     Constant:  public static final java.lang.annotation.RetentionPolicy
                  java.lang.annotation.RetentionPolicy.SOURCE 
     Constant:  public static final java.lang.annotation.RetentionPolicy
                  java.lang.annotation.RetentionPolicy.CLASS 
     Constant:  public static final java.lang.annotation.RetentionPolicy 
                  java.lang.annotation.RetentionPolicy.RUNTIME 
        Field:  private static final java.lang.annotation.RetentionPolicy[] 
                  java.lang.annotation.RetentionPolicy. [ synthetic ]
  Constructor:  private java.lang.annotation.RetentionPolicy() 
       Method:  public static java.lang.annotation.RetentionPolicy[]
                  java.lang.annotation.RetentionPolicy.values() 
       Method:  public static java.lang.annotation.RetentionPolicy
                  java.lang.annotation.RetentionPolicy.valueOf(java.lang.String) 

```

输出表明 [`java.lang.annotation.RetentionPolicy`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html) 声明只包含 3 个枚举常量。枚举常量作为`public static final`字段暴露。字段、构造器、以及方法都是编译器生成的。`$VALUES`字段与`values()`方法的实现有关。

------

**注意：**由于各种原因，包括对枚举类型的演化的支持，枚举常量的声明顺序很重要。 [`Class.getFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getFields--) 和 [`Class.getDeclaredFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredFields--) 不保证返回值的顺序与源代码中的声明顺序匹配。如果应用程序需要排序，请使用 [`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--) 。

------

 [`java.util.concurrent.TimeUnit`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/TimeUnit.html) 的输出显示了更复杂的枚举是可能的。该类包括几个方法以及声明为`static final`的其他字段，这些字段不是枚举常量。

$ *java EnumSpy java.util.concurrent.TimeUnit*

```
Class:  class java.util.concurrent.TimeUnit
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.NANOSECONDS
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.MICROSECONDS
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.MILLISECONDS
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.SECONDS
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.MINUTES
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.HOURS
     Constant:  public static final java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.DAYS
        Field:  static final long java.util.concurrent.TimeUnit.C0
        Field:  static final long java.util.concurrent.TimeUnit.C1
        Field:  static final long java.util.concurrent.TimeUnit.C2
        Field:  static final long java.util.concurrent.TimeUnit.C3
        Field:  static final long java.util.concurrent.TimeUnit.C4
        Field:  static final long java.util.concurrent.TimeUnit.C5
        Field:  static final long java.util.concurrent.TimeUnit.C6
        Field:  static final long java.util.concurrent.TimeUnit.MAX
        Field:  private static final java.util.concurrent.TimeUnit[] 
                  java.util.concurrent.TimeUnit. [ synthetic ]
  Constructor:  private java.util.concurrent.TimeUnit()
  Constructor:  java.util.concurrent.TimeUnit
                  (java.lang.String,int,java.util.concurrent.TimeUnit)
                  [ synthetic ]
       Method:  public static java.util.concurrent.TimeUnit
                  java.util.concurrent.TimeUnit.valueOf(java.lang.String)
       Method:  public static java.util.concurrent.TimeUnit[] 
                  java.util.concurrent.TimeUnit.values()
       Method:  public void java.util.concurrent.TimeUnit.sleep(long) 
                  throws java.lang.InterruptedException
       Method:  public long java.util.concurrent.TimeUnit.toNanos(long)
       Method:  public long java.util.concurrent.TimeUnit.convert
                  (long,java.util.concurrent.TimeUnit)
       Method:  abstract int java.util.concurrent.TimeUnit.excessNanos
                  (long,long)
       Method:  public void java.util.concurrent.TimeUnit.timedJoin
                  (java.lang.Thread,long) throws java.lang.InterruptedException
       Method:  public void java.util.concurrent.TimeUnit.timedWait
                  (java.lang.Object,long) throws java.lang.InterruptedException
       Method:  public long java.util.concurrent.TimeUnit.toDays(long)
       Method:  public long java.util.concurrent.TimeUnit.toHours(long)
       Method:  public long java.util.concurrent.TimeUnit.toMicros(long)
       Method:  public long java.util.concurrent.TimeUnit.toMillis(long)
       Method:  public long java.util.concurrent.TimeUnit.toMinutes(long)
       Method:  public long java.util.concurrent.TimeUnit.toSeconds(long)
       Method:  static long java.util.concurrent.TimeUnit.x(long,long,long)
```

#### 获取和设定枚举类型字段

存储枚举的字段像其它任何引用类型字段一样存取，使用 [`Field.set()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#set-java.lang.Object-java.lang.Object-) 和 [`Field.get()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#get-java.lang.Object-) 。有关访问字段的更多信息，参考 [Fields](https://docs.oracle.com/javase/tutorial/reflect/member/field.html) 章节。

考虑需要动态修改服务器应用程序中日志跟踪级别的应用程序，该应用程序通常在运行时不允许此更改。假设服务器对象的实例可用。 [`SetTrace`](https://docs.oracle.com/javase/tutorial/reflect/special/example/SetTrace.java) 示例显示了代码如何将枚举的 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 表示形式转换为枚举类型，并检索和设置存储枚举的字段的值。

```java
import java.lang.reflect.Field;
import static java.lang.System.out;

enum TraceLevel { OFF, LOW, MEDIUM, HIGH, DEBUG }

class MyServer {
    private TraceLevel level = TraceLevel.OFF;
}

public class SetTrace {
    public static void main(String... args) {
	TraceLevel newLevel = TraceLevel.valueOf(args[0]);

	try {
	    MyServer svr = new MyServer();
	    Class<?> c = svr.getClass();
	    Field f = c.getDeclaredField("level");
	    f.setAccessible(true);
	    TraceLevel oldLevel = (TraceLevel)f.get(svr);
	    out.format("Original trace level:  %s%n", oldLevel);

	    if (oldLevel != newLevel) {
 		f.set(svr, newLevel);
		out.format("    New  trace level:  %s%n", f.get(svr));
	    }

        // production code should handle these exceptions more gracefully
	} catch (IllegalArgumentException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	}
    }
}
```

由于枚举常量是单例的，`==`和`!=`操作符可以被用来比较相同类型的枚举常量。

$ *java SetTrace OFF*

```
Original trace level:  OFF
```

$ *java SetTrace DEBUG*

    Original trace level:  OFF
    New  trace level:  DEBUG

#### 故障排除

下面介绍在使用枚举类型时常见的错误。

**试图实例化枚举类型导致的 IllegalArgumentException**

如前面提到过的，实例化枚举类型是被禁止的。下面的例子试图这么干：

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.InvocationTargetException;
import static java.lang.System.out;

enum Charge {
    POSITIVE, NEGATIVE, NEUTRAL;
    Charge() {
	out.format("under construction%n");
    }
}

public class EnumTrouble {

    public static void main(String... args) {
	try {
	    Class<?> c = Charge.class;

 	    Constructor[] ctors = c.getDeclaredConstructors();
 	    for (Constructor ctor : ctors) {
		out.format("Constructor: %s%n",  ctor.toGenericString());
 		ctor.setAccessible(true);
 		ctor.newInstance();
 	    }

        // production code should handle these exceptions more gracefully
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (InvocationTargetException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java EnumTrouble*

```
Constructor: private Charge()
Exception in thread "main" java.lang.IllegalArgumentException: Cannot
  reflectively create enum objects
        at java.lang.reflect.Constructor.newInstance(Constructor.java:511)
        at EnumTrouble.main(EnumTrouble.java:22)
```

------

**提示：**尝试显式实例化枚举是一个编译时错误，因为这会阻止定义的枚举常量是唯一的。这种限制也在反射代码中强制执行。尝试使用其默认构造函数实例化类的代码应首先调用 [`Class.isEnum()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isEnum--) 以确定该类是否为枚举。

------

**使用不兼容的枚举类型设定字段值导致的 IllegalArgumentException**

存储枚举的字段必须使用适当的枚举类型设置。（实际上，必须使用兼容类型设置任何类型的字段。）下面的示例会产生预期的错误。

```java
import java.lang.reflect.Field;

enum E0 { A, B }
enum E1 { A, B }

class ETest {
    private E0 fld = E0.A;
}

public class EnumTroubleToo {
    public static void main(String... args) {
	try {
	    ETest test = new ETest();
	    Field f = test.getClass().getDeclaredField("fld");
	    f.setAccessible(true);
 	    f.set(test, E1.A);  // IllegalArgumentException

        // production code should handle these exceptions more gracefully
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java EnumTroubleToo*

```
Exception in thread "main" java.lang.IllegalArgumentException: Can not set E0
  field ETest.fld to E1
        at sun.reflect.UnsafeFieldAccessorImpl.throwSetIllegalArgumentException
          (UnsafeFieldAccessorImpl.java:146)
        at sun.reflect.UnsafeFieldAccessorImpl.throwSetIllegalArgumentException
          (UnsafeFieldAccessorImpl.java:150)
        at sun.reflect.UnsafeObjectFieldAccessorImpl.set
          (UnsafeObjectFieldAccessorImpl.java:63)
        at java.lang.reflect.Field.set(Field.java:657)
        at EnumTroubleToo.main(EnumTroubleToo.java:16)
```

------

**提示：**严格地说，任何尝试将类型`X`的字段设置为类型`Y`的值只有在以下语句成立时才能成功：

````
X.class.isAssignableFrom（Y.class）== true
````

可以修改代码以执行以下测试以验证类型是否兼容：

```
if (f.getType().isAssignableFrom(E0.class))
    // compatible
else
    // expect IllegalArgumentException
```

----

