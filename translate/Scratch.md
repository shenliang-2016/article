### 构造器

构造器被用来创建类的实例对象。它执行的典型操作是需要再方法被调用或者字段被访问之前初始化类实例对象。构造器用于无法被继承。

类似于方法，反射提供了发现和检索类的构造器的 API ，同时可以获取注入修饰符、参数、注解以及抛出异常等声明信息。新的类实例还可以使用一个特定的构造器创建。当使用构造器时涉及到的关键类是 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 和 [`java.lang.reflect.Constructor`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html) 。与构造器相关的一般操作在下面的章节中介绍。

- [查找构造器](https://docs.oracle.com/javase/tutorial/reflect/member/ctorLocation.html) 展示如何获取携带特定参数的构造器
- [检索并解析构造器修饰符](https://docs.oracle.com/javase/tutorial/reflect/member/ctorModifiers.html) 展示如何获取构造器声明修饰符以及有关构造器的其它信息
- [创建新的类实例](https://docs.oracle.com/javase/tutorial/reflect/member/ctorInstance.html) 展示如何实例化一个对象实例，通过调用它的构造器
- [故障修复Troubleshooting](https://docs.oracle.com/javase/tutorial/reflect/member/ctorTrouble.html) 描述在查找或者调用构造器时可能遇到的常见错误

#### 查找构造器

构造器声明包含名称、修饰符、参数以及可抛出的异常列表。[`java.lang.reflect.Constructor`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html) 类提供了获取这些信息的方法。

 [`ConstructorSift`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ConstructorSift.java) 示例展示了如何在一个类中查找声明的携带给定参数类型的构造器。

```java
import java.lang.reflect.Constructor;
import java.lang.reflect.Type;
import static java.lang.System.out;

public class ConstructorSift {
    public static void main(String... args) {
	try {
	    Class<?> cArg = Class.forName(args[1]);

	    Class<?> c = Class.forName(args[0]);
	    Constructor[] allConstructors = c.getDeclaredConstructors();
	    for (Constructor ctor : allConstructors) {
		Class<?>[] pType  = ctor.getParameterTypes();
		for (int i = 0; i < pType.length; i++) {
		    if (pType[i].equals(cArg)) {
			out.format("%s%n", ctor.toGenericString());

			Type[] gpType = ctor.getGenericParameterTypes();
			for (int j = 0; j < gpType.length; j++) {
			    char ch = (pType[j].equals(cArg) ? '*' : ' ');
			    out.format("%7c%s[%d]: %s%n", ch,
				       "GenericParameterType", j, gpType[j]);
			}
			break;
		    }
		}
	    }

        // production code should handle this exception more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

[`Method.getGenericParameterTypes()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getGenericParameterTypes--) 将在类文件中查找方法签名属性，如果它存在。如果属性不可用，该方法就会退化为 [`Method.getParameterType()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html#getParameterType--) ，此方法在引入泛型时没有变化。另一个名为`getGeneric*Foo*()*`的方法通过反射获取某些`Foo`的值，实现类似。`Method.get*Types()`的返回值语法在 [`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--) 中描述。

下面是 [`java.util.Formatter`](https://docs.oracle.com/javase/8/docs/api/java/util/Formatter.html) 中所有携带 [`Locale`](https://docs.oracle.com/javase/8/docs/api/java/util/Locale.html) 参数的构造器的输出：

$ *java ConstructorSift java.util.Formatter java.util.Locale*

```
public
java.util.Formatter(java.io.OutputStream,java.lang.String,java.util.Locale)
throws java.io.UnsupportedEncodingException
       GenericParameterType[0]: class java.io.OutputStream
       GenericParameterType[1]: class java.lang.String
      *GenericParameterType[2]: class java.util.Locale
public java.util.Formatter(java.lang.String,java.lang.String,java.util.Locale)
throws java.io.FileNotFoundException,java.io.UnsupportedEncodingException
       GenericParameterType[0]: class java.lang.String
       GenericParameterType[1]: class java.lang.String
      *GenericParameterType[2]: class java.util.Locale
public java.util.Formatter(java.lang.Appendable,java.util.Locale)
       GenericParameterType[0]: interface java.lang.Appendable
      *GenericParameterType[1]: class java.util.Locale
public java.util.Formatter(java.util.Locale)
      *GenericParameterType[0]: class java.util.Locale
public java.util.Formatter(java.io.File,java.lang.String,java.util.Locale)
throws java.io.FileNotFoundException,java.io.UnsupportedEncodingException
       GenericParameterType[0]: class java.io.File
       GenericParameterType[1]: class java.lang.String
      *GenericParameterType[2]: class java.util.Locale
```

下面的例子输出展示了如何在 [`String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) 中搜索`char[]`类型参数。

$ *java ConstructorSift java.lang.String "[C"*

```
java.lang.String(int,int,char[])
       GenericParameterType[0]: int
       GenericParameterType[1]: int
      *GenericParameterType[2]: class [C
public java.lang.String(char[],int,int)
      *GenericParameterType[0]: class [C
       GenericParameterType[1]: int
       GenericParameterType[2]: int
public java.lang.String(char[])
      *GenericParameterType[0]: class [C
```

 [`Class.forName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#forName-java.lang.String-) 接受的表示引用类型和基本数据类型的数组的语法在 [`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--) 中描述。注意，首先列出的构造器是`package-private`，而不是`public`。它被返回是因为示例代码使用了 [`Class.getDeclaredConstructors()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getDeclaredConstructors--) 而不是 [`Class.getConstructors()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getConstructors--) ，后者只返回`public`构造器。

这个示例展示了搜索可变参数个数，需要使用数组语法：

$ *java ConstructorSift java.lang.ProcessBuilder "[Ljava.lang.String;"*

```
public java.lang.ProcessBuilder(java.lang.String[])
      *GenericParameterType[0]: class [Ljava.lang.String;
```

这是源代码中实际的 [`ProcessBuilder`](https://docs.oracle.com/javase/8/docs/api/java/lang/ProcessBuilder.html#ProcessBuilder-java.lang.String...-) 构造器声明。

```java
public ProcessBuilder(String... command)
```

参数被表示为一个一维数组，元素类型为`java.lang.String`。可以通过调用 [`Constructor.isVarArgs()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#isVarArgs--) 区别于显式声明为`java.lang.String`数组的参数。

最后的示例输出声明为携带泛型类型参数的构造器：

$ *java ConstructorSift java.util.HashMap java.util.Map*

```
public java.util.HashMap(java.util.Map<? extends K, ? extends V>)
      *GenericParameterType[0]: java.util.Map<? extends K, ? extends V>
```

构造器的异常类型可以通过与检索方法类似的方式查找。参考 [Obtaining Method Type Information](https://docs.oracle.com/javase/tutorial/reflect/member/methodType.html) 章节中描述的 [`MethodSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodSpy.java) 示例获取更多细节。

