#### 获取并解析字段修饰符

一些修饰符可以作为字段声明的一部分出现：

- 访问修饰符： `public` ， `protected` ， 以及 `private`
- 控制运行时行为的特定于字段的修饰符： `transient` 和 `volatile`
- 限制为单实例的修饰符： `static`
- 禁止值修改的修饰符： `final`
- 注解

方法 [`Field.getModifiers()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#getModifiers--) 可以被用来返回字段声明中的修饰符的集合的整数表示。该整数中表示修饰符的数据位定义在 [`java.lang.reflect.Modifier`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Modifier.html) 中。

 [`FieldModifierSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/FieldModifierSpy.java) 示例展示了如何搜索使用给定修饰符的字段。它还能通过调用 [`Field.isSynthetic()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isSynthetic--) 来确定所定位的字段是否是合成的(编译器生成的)，通过调用[`Field.isEnumCostant()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isEnumConstant--) 确定字段是否是一个枚举常量。

```java
import java.lang.reflect.Field;
import java.lang.reflect.Modifier;
import static java.lang.System.out;

enum Spy { BLACK , WHITE }

public class FieldModifierSpy {
    volatile int share;
    int instance;
    class Inner {}

    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    int searchMods = 0x0;
	    for (int i = 1; i < args.length; i++) {
		searchMods |= modifierFromString(args[i]);
	    }

	    Field[] flds = c.getDeclaredFields();
	    out.format("Fields in Class '%s' containing modifiers:  %s%n",
		       c.getName(),
		       Modifier.toString(searchMods));
	    boolean found = false;
	    for (Field f : flds) {
		int foundMods = f.getModifiers();
		// Require all of the requested modifiers to be present
		if ((foundMods & searchMods) == searchMods) {
		    out.format("%-8s [ synthetic=%-5b enum_constant=%-5b ]%n",
			       f.getName(), f.isSynthetic(),
			       f.isEnumConstant());
		    found = true;
		}
	    }

	    if (!found) {
		out.format("No matching fields%n");
	    }

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }

    private static int modifierFromString(String s) {
	int m = 0x0;
	if ("public".equals(s))           m |= Modifier.PUBLIC;
	else if ("protected".equals(s))   m |= Modifier.PROTECTED;
	else if ("private".equals(s))     m |= Modifier.PRIVATE;
	else if ("static".equals(s))      m |= Modifier.STATIC;
	else if ("final".equals(s))       m |= Modifier.FINAL;
	else if ("transient".equals(s))   m |= Modifier.TRANSIENT;
	else if ("volatile".equals(s))    m |= Modifier.VOLATILE;
	return m;
    }
}
```

上面的例子输出如下：

$ *java FieldModifierSpy FieldModifierSpy volatile*

```
Fields in Class 'FieldModifierSpy' containing modifiers:  volatile
share    [ synthetic=false enum_constant=false ]
```

$ *java FieldModifierSpy Spy public*

````
Fields in Class 'Spy' containing modifiers:  public
BLACK    [ synthetic=false enum_constant=true  ]
WHITE    [ synthetic=false enum_constant=true  ]
````

$ *java FieldModifierSpy FieldModifierSpy\$Inner final*

````
Fields in Class 'FieldModifierSpy$Inner' containing modifiers:  final
this$0   [ synthetic=true  enum_constant=false ]
````

$ *java FieldModifierSpy Spy private static final*

````
Fields in Class 'Spy' containing modifiers:  private static final
$VALUES  [ synthetic=true  enum_constant=false ]
````

注意，某些字段没有在原始代码中声明，同样也被输出了出来。这是因为编译器将产生一些*合成字段*，这些字段在运行时会使用到。为了检测一个字段是否是合成字段，例子中调用了 [`Field.isSynthetic()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isSynthetic--) 。合成字段集合时编译器依赖的：但是常用的字段包括内部使用的`this$0`（比如作为非静态成员类的嵌套类），用于引用最外层的封闭类，枚举使用的`$VALUES`来实现隐式定义的静态方法`values()`。合成类成员的名称是未指定的，并且在不同编译器实现或发行版中可能不相同。这些和其他合成字段将包含在 [`Class.getDeclaredFields()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredFields--) 返回的数组中，但不是由 [`Class.getField()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getField-java.lang.String-) 标识的，因为合成成员通常不是`public`的。

因为 [`Field`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html) 实现了接口 [`java.lang.reflect.AnnotatedElement`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AnnotatedElement.html) ，它就可能使用 [`java.lang.annotation.RetentionPolicy.RUNTIME`](https://docs.oracle.com/javase/8/docs/api/java/lang/annotation/RetentionPolicy.html#RUNTIME) 检索任何运行时注解。获取注解的例子在章节 [Examining Class Modifiers and Types](https://docs.oracle.com/javase/tutorial/reflect/class/classModifiers.html) 中。

