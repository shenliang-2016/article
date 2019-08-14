### 故障排除

下面的例子展示了当在类上使用反射时可能遇到的典型错误。

**编译器警告: "Note: ... uses unchecked or unsafe operations"**

当一个方法被调用时，参数值的类型被检查，并且可能被转化。[`ClassWarning`](https://docs.oracle.com/javase/tutorial/reflect/class/example/ClassWarning.java) 调用 [`getMethod()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getMethod-java.lang.String-java.lang.Class...-) 可能会产生一个典型的不受检查的转换警告：

```java
import java.lang.reflect.Method;

public class ClassWarning {
    void m() {
	try {
	    Class c = ClassWarning.class;
	    Method m = c.getMethod("m");  // warning

        // production code should handle this exception more gracefully
	} catch (NoSuchMethodException x) {
    	    x.printStackTrace();
    	}
    }
}
```

$ *javac ClassWarning.java*

````
Note: ClassWarning.java uses unchecked or unsafe operations.
Note: Recompile with -Xlint:unchecked for details.
````

$ *javac -Xlint:unchecked ClassWarning.java*

````
ClassWarning.java:6: warning: [unchecked] unchecked call to getMethod
  (String,Class<?>...) as a member of the raw type Class
Method m = c.getMethod("m");  // warning
                      ^
1 warning
````

许多类库方法已经使用范型声明进行了改造，包括 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 中的几个方法。由于`c`被声明为*raw*类型(没有类型参数)，同时 [`getMethod()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getMethod-java.lang.String-java.lang.Class...-) 方法的对应参数是一个参数化类型，会发生一个不受检查的转换。编译器需要生成警告。(参考 [*The Java Language Specification, Java SE 7 Edition*](https://docs.oracle.com/javase/specs/jls/se7/html/index.html) 章节 [Unchecked Conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.1.9) 和 [Method Invocation Conversion](https://docs.oracle.com/javase/specs/jls/se7/html/jls-5.html#jls-5.3) )

存在两种可能的解决方案。比较好的是修改`c`的声明来包含一个合适的范型类型。这种情况下，声明 应该是：

```java
Class<?> c = warn.getClass();
```

另外，警告应该使用预定义注解 [`@SuppressWarnings`](https://docs.oracle.com/javase/8/docs/api/java/lang/SuppressWarnings.html) 在有问题的语句之前被显式支持。

```java
Class c = ClassWarning.class;
@SuppressWarnings("unchecked")
Method m = c.getMethod("m");  
// warning gone
```

------

**提示：**作为一般原则，警告不应该被忽略，因为它们可能表明存在错误。应适当使用参数化声明。如果这不可能（可能是因为应用程序必须与库供应商的代码交互），请使用[`@SuppressWarnings`](https://docs.oracle.com/javase/8/docs/api/java/lang/SuppressWarnings.html) 注解违规行。

------

**当构造器不可访问时的实例化异常**

如果尝试创建类的一个新的实例，而类的无参构造器不可见，[`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 将抛出一个 [`InstantiationException`](https://docs.oracle.com/javase/8/docs/api/java/lang/InstantiationException.html) 。 [`ClassTrouble`](https://docs.oracle.com/javase/tutorial/reflect/class/example/ClassTrouble.java) 例子展示了结果追踪栈：

```java
class Cls {
    private Cls() {}
}

public class ClassTrouble {
    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName("Cls");
	    c.newInstance();  // InstantiationException

        // production code should handle these exceptions more gracefully
	} catch (InstantiationException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	}
    }
}
```

$ *java ClassTrouble*

````
java.lang.IllegalAccessException: Class ClassTrouble can not access a member of
  class Cls with modifiers "private"
        at sun.reflect.Reflection.ensureMemberAccess(Reflection.java:65)
        at java.lang.Class.newInstance0(Class.java:349)
        at java.lang.Class.newInstance(Class.java:308)
        at ClassTrouble.main(ClassTrouble.java:9)
````

[`Class.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#newInstance--) 的行为非常像 `new` 关键字，同样也会因为相同的原因而失败。在反射中典型的解决方案是利用 [`java.lang.reflect.AccessibleObject`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html) 类的优点，该类提供了压制访问控制检查的能力。不过，这种方法将无法工作，因为 [`java.lang.Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 并没有扩展 [`AccessibleObject`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html) 。所以，唯一的解决方案就是修改代码，使用 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) ，它扩展了 [`AccessibleObject`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/AccessibleObject.html)。

------

**提示：**通常，由于 [Members](https://docs.oracle.com/javase/tutorial/reflect/member/index.html) 课程 [Creating New Class Instances](https://docs.oracle.com/javase/tutorial/reflect/member/ctorInstance.html) 章节中描述的原因，应该使用 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 。

------

使用 [`Constructor.newInstance()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html#newInstance-java.lang.Object...-) 的潜在问题的更多的例子可以在 [Members](https://docs.oracle.com/javase/tutorial/reflect/member/index.html) 课程的 [Constructor Troubleshooting](https://docs.oracle.com/javase/tutorial/reflect/member/ctorTrouble.html) 章节中找到。

