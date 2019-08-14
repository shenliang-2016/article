### 检查类修饰符和类型

一个类声明中可以包含一个或者多个修饰符，这些修饰符影响它的运行时行为：

* 访问修饰符：`public`，`protected`，`private`
* 强制覆盖修饰符：`abstract`
* 限制为单个实例的修饰符：`static`
* 禁止值修改修饰符：`final`
* 强制严格浮点数行为修饰符：`strictfp`
* 注解

并不是所有的修饰符都能用于所有的类。比如，接口就不能是`final`的，而枚举不能是`abstract` 。[`java.lang.reflect.Modifier`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Modifier.html) 包含所有可能的修饰符的声明。它同样包含可以被用于对 [`Class.getModifiers()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getModifiers--) 返回的修饰符的集合进行解码的方法。

 [`ClassDeclarationSpy`](https://docs.oracle.com/javase/tutorial/reflect/class/example/ClassDeclarationSpy.java) 示例展示了如何获取一个类的声明组件，包括修饰符，泛型类型参数，实现的接口，以及继承路径等。由于 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 实现了 [`java.lang.reflect.AnnotatedElement`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AnnotatedElement.html) 接口，因此它也可能查询运行时注解。

```java
import java.lang.annotation.Annotation;
import java.lang.reflect.Modifier;
import java.lang.reflect.Type;
import java.lang.reflect.TypeVariable;
import java.util.Arrays;
import java.util.ArrayList;
import java.util.List;
import static java.lang.System.out;

public class ClassDeclarationSpy {
    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    out.format("Class:%n  %s%n%n", c.getCanonicalName());
	    out.format("Modifiers:%n  %s%n%n",
		       Modifier.toString(c.getModifiers()));

	    out.format("Type Parameters:%n");
	    TypeVariable[] tv = c.getTypeParameters();
	    if (tv.length != 0) {
		out.format("  ");
		for (TypeVariable t : tv)
		    out.format("%s ", t.getName());
		out.format("%n%n");
	    } else {
		out.format("  -- No Type Parameters --%n%n");
	    }

	    out.format("Implemented Interfaces:%n");
	    Type[] intfs = c.getGenericInterfaces();
	    if (intfs.length != 0) {
		for (Type intf : intfs)
		    out.format("  %s%n", intf.toString());
		out.format("%n");
	    } else {
		out.format("  -- No Implemented Interfaces --%n%n");
	    }

	    out.format("Inheritance Path:%n");
	    List<Class> l = new ArrayList<Class>();
	    printAncestor(c, l);
	    if (l.size() != 0) {
		for (Class<?> cl : l)
		    out.format("  %s%n", cl.getCanonicalName());
		out.format("%n");
	    } else {
		out.format("  -- No Super Classes --%n%n");
	    }

	    out.format("Annotations:%n");
	    Annotation[] ann = c.getAnnotations();
	    if (ann.length != 0) {
		for (Annotation a : ann)
		    out.format("  %s%n", a.toString());
		out.format("%n");
	    } else {
		out.format("  -- No Annotations --%n%n");
	    }

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }

    private static void printAncestor(Class<?> c, List<Class> l) {
	Class<?> ancestor = c.getSuperclass();
 	if (ancestor != null) {
	    l.add(ancestor);
	    printAncestor(ancestor, l);
 	}
    }
}
```

接下来是一些输出样本。用户输入以斜体显示。

$ *java ClassDeclarationSpy java.util.concurrent.ConcurrentNavigableMap*

```
Class:
  java.util.concurrent.ConcurrentNavigableMap

Modifiers:
  public abstract interface

Type Parameters:
  K V

Implemented Interfaces:
  java.util.concurrent.ConcurrentMap<K, V>
  java.util.NavigableMap<K, V>

Inheritance Path:
  -- No Super Classes --

Annotations:
  -- No Annotations --
```

下面是实际的源代码中 [`java.util.concurrent.ConcurrentNavigableMap`](https://docs.oracle.com/javase/8/docs/api/java/util/concurrent/ConcurrentNavigableMap.html) 的声明：

```java
public interface ConcurrentNavigableMap<K,V>
    extends ConcurrentMap<K,V>, NavigableMap<K,V>
```

注意，由于这是一个接口，因而隐含是`abstract`的。编译器会为所有接口添加此修饰符。同时，此声明包含两个泛型类型参数，`K`和`V`。示例代码简单打印出这些参数的名称，但是我们可以通过 [`java.lang.reflect.TypeVariable`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/TypeVariable.html) 中的方法获取有关它们的更多信息。如上面所示，接口同样可以实现其它接口。

$ *java ClassDeclarationSpy "[Ljava.lang.String;"*

```
Class:
  java.lang.String[]

Modifiers:
  public abstract final

Type Parameters:
  -- No Type Parameters --

Implemented Interfaces:
  interface java.lang.Cloneable
  interface java.io.Serializable

Inheritance Path:
  java.lang.Object

Annotations:
  -- No Annotations --
```

由于数组是运行时对象，因此所有类型信息都由Java虚拟机定义。特别是，数组实现了 [`Cloneable`](https://docs.oracle.com/javase/8/docs/api/java/lang/Cloneable.html) and [`java.io.Serializable`](https://docs.oracle.com/javase/8/docs/api/java/io/Serializable.html) ，它们的直接超类总是[`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)。

$ *java ClassDeclarationSpy java.io.InterruptedIOException*

```
Class:
  java.io.InterruptedIOException

Modifiers:
  public

Type Parameters:
  -- No Type Parameters --

Implemented Interfaces:
  -- No Implemented Interfaces --

Inheritance Path:
  java.io.IOException
  java.lang.Exception
  java.lang.Throwable
  java.lang.Object

Annotations:
  -- No Annotations --
```

从继承路径可以推断出 [`java.io.InterruptedIOException`](https://docs.oracle.com/javase/8/docs/api/java/io/InterruptedIOException.html) 是一个受检查异常，因为继承路径中不存在 [`RuntimeException`](https://docs.oracle.com/javase/8/docs/api/java/lang/RuntimeException.html) 。

$ *java ClassDeclarationSpy java.security.Identity*

```
Class:
  java.security.Identity

Modifiers:
  public abstract

Type Parameters:
  -- No Type Parameters --

Implemented Interfaces:
  interface java.security.Principal
  interface java.io.Serializable

Inheritance Path:
  java.lang.Object

Annotations:
  @java.lang.Deprecated()
```

输出展示了 [`java.security.Identity`](https://docs.oracle.com/javase/8/docs/api/java/security/Identity.html)，一个废弃的 API，拥有注解 [`java.lang.Deprecated`](https://docs.oracle.com/javase/8/docs/api/java/lang/Deprecated.html) 。反射代码可以使用它来检测已弃用的API。

------

**注意：** 并非所有注解都可通过反射获得。只有那些具有 [`RUNTIME`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html#RUNTIME) 的 [`java.lang.annotation.RetentionPolicy`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html) 的注解才是可以访问的。在 Java 语言中预定义的 [`@Deprecated`](https://docs.oracle.com/javase/8/docs/api/java/lang/Deprecated.html) ， [`@Override`](https://docs.oracle.com/javase/8/docs/api/java/lang/Override.html) ，和 [`@SuppressWarnings`](https://docs.oracle.com/javase/8/docs/api/java/lang/SuppressWarnings.html) 这三个注解中，只有 [`@Deprecated`](https://docs.oracle.com/javase/8/docs/api/java/lang/Deprecated.html) 在运行时可用。

------

