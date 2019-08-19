#### 获取并解析方法修饰符

可以作为方法声明一部分的修饰符有下面这几种：

- 访问修饰符 `public`, `protected`, 和 `private`
- 限定为一个实例的修饰符 `static`
- 禁止值修改修饰符 `final`
- 需要重载修饰符 `abstract`
- 阻止重入修饰符 `synchronized`
- 表示以别的编程语言实现的修饰符 `native`
- 强制限制静态浮点数行为修饰符 `strictfp`
- 注解

 [`MethodModifierSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodModifierSpy.java) 示例列出了给定名称方法的所有修饰符。它同时显示该方法是否是合成的（由编译器生成的），是否是可变参数的，或者是否是一个桥接方法（由编译器生成以支持泛型接口）。

```java
import java.lang.reflect.Method;
import java.lang.reflect.Modifier;
import static java.lang.System.out;

public class MethodModifierSpy {

    private static int count;
    private static synchronized void inc() { count++; }
    private static synchronized int cnt() { return count; }

    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    Method[] allMethods = c.getDeclaredMethods();
	    for (Method m : allMethods) {
		if (!m.getName().equals(args[1])) {
		    continue;
		}
		out.format("%s%n", m.toGenericString());
		out.format("  Modifiers:  %s%n",
			   Modifier.toString(m.getModifiers()));
		out.format("  [ synthetic=%-5b var_args=%-5b bridge=%-5b ]%n",
			   m.isSynthetic(), m.isVarArgs(), m.isBridge());
		inc();
	    }
	    out.format("%d matching overload%s found%n", cnt(),
		       (cnt() == 1 ? "" : "s"));

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

上面的例子产生的部分输出如下：

$ *java MethodModifierSpy java.lang.Object wait*

```
public final void java.lang.Object.wait() throws java.lang.InterruptedException
  Modifiers:  public final
  [ synthetic=false var_args=false bridge=false ]
public final void java.lang.Object.wait(long,int)
  throws java.lang.InterruptedException
  Modifiers:  public final
  [ synthetic=false var_args=false bridge=false ]
public final native void java.lang.Object.wait(long)
  throws java.lang.InterruptedException
  Modifiers:  public final native
  [ synthetic=false var_args=false bridge=false ]
3 matching overloads found
```

$ *java MethodModifierSpy java.lang.StrictMath toRadians*

```
public static double java.lang.StrictMath.toRadians(double)
  Modifiers:  public static strictfp
  [ synthetic=false var_args=false bridge=false ]
1 matching overload found
```

$ *java MethodModifierSpy MethodModifierSpy inc*

```
private synchronized void MethodModifierSpy.inc()
  Modifiers: private synchronized
  [ synthetic=false var_args=false bridge=false ]
1 matching overload found
```

$ *java MethodModifierSpy java.lang.Class getConstructor*

```
public java.lang.reflect.Constructor<T> java.lang.Class.getConstructor
  (java.lang.Class<T>[]) throws java.lang.NoSuchMethodException,
  java.lang.SecurityException
  Modifiers: public transient
  [ synthetic=false var_args=true bridge=false ]
1 matching overload found
```

$ *java MethodModifierSpy java.lang.String compareTo*

```
public int java.lang.String.compareTo(java.lang.String)
  Modifiers: public
  [ synthetic=false var_args=false bridge=false ]
public int java.lang.String.compareTo(java.lang.Object)
  Modifiers: public volatile
  [ synthetic=true  var_args=false bridge=true  ]
2 matching overloads found
```

注意 [`Method.isVarArgs()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#isVarArgs--) 为 [`Class.getConstructor()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getConstructor-java.lang.Class...-) 返回`true`。这表示该方法声明如下：

```java
public Constructor<T> getConstructor(Class<?>... parameterTypes)
```

而不是：

```java
public Constructor<T> getConstructor(Class<?> [] parameterTypes)
```

注意关于 [`String.compareTo()`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html#compareTo-java.lang.String-) 的输出包含两个方法。该方法在`String.java`中的声明：

```java
public int compareTo(String anotherString);
```

以及一个合成的或者编译器生成的桥接方法。这是因为 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 实现了参数化接口 [`Comparable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html) 。在参数擦除过程中，继承的方法 [`Comparable.compareTo()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Comparable.html#compareTo-T-) 的参数类型从`java.lang.Object`变成`java.lang.String`。由于`Comparable`中的`compareTo`方法的参数类型不再符合类型擦除后的`String` ，就不能发生重载了。在所有其它环境下，这将导致一个编译期错误，因为该接口并未被实现。桥接方法的引入避免了此问题。

[`Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html) 实现了 [`java.lang.reflect.AnnotatedElement`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AnnotatedElement.html) 。因此任何使用 [`java.lang.annotation.RetentionPolicy.RUNTIME`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html#RUNTIME) 的运行时注解都能被检索到。检索注解的例子参考 [Examining Class Modifiers and Types](https://docs.oracle.com/javase/tutorial/reflect/class/classModifiers.html) 。

