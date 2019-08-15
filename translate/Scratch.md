#### 获取字段类型

字段，要么是基本数据类型，要么是引用类型。基本数据类型有 8 中：`boolean`，`byte`，`short`，`int` ，`long` ，`char`，`float`，以及`double`。引用类型是 [`java.lang.Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 的直接或者间接子类，包括接口、数组、以及枚举类型。

 [`FieldSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/FieldSpy.java) 示例给定一个全限定二进制类名，打印字段类型和泛型类型以及字段名。

```java
import java.lang.reflect.Field;
import java.util.List;

public class FieldSpy<T> {
    public boolean[][] b = {{ false, false }, { true, true } };
    public String name  = "Alice";
    public List<Integer> list;
    public T val;

    public static void main(String... args) {
	try {
	    Class<?> c = Class.forName(args[0]);
	    Field f = c.getField(args[1]);
	    System.out.format("Type: %s%n", f.getType());
	    System.out.format("GenericType: %s%n", f.getGenericType());

        // production code should handle these exceptions more gracefully
	} catch (ClassNotFoundException x) {
	    x.printStackTrace();
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	}
    }
}
```

示例输出获取到的类中的 3 个`public`字段类型（`b`，`name`，以及参数化类型的`list`）。接下来，用户输入用斜体表示：

$ *java FieldSpy FieldSpy b*

```
Type: class [[Z
GenericType: class [[Z
```

$ *java FieldSpy FieldSpy name*

````
Type: class java.lang.String
GenericType: class java.lang.String
````

$ *java FieldSpy FieldSpy list*

````
Type: interface java.util.List
GenericType: java.util.List<java.lang.Integer>
````

$ *java FieldSpy FieldSpy val*

````
Type: class java.lang.Object
GenericType: T
````

字段`b`的类型是布尔值的二维数组。类型名称的语法参见 [`Class.getName()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getName--) 。

字段`val`的类型被报告为 `java.lang.Object` ，因为泛型是通过类型擦除实现，编译期类型擦除会清除根性类型的所有类型信息。因此`T`被类型变量的上界所取代，这种情况下，是`java.lang.Object` 。

[`Field.getGenericType()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#getGenericType--) 将查询类文件中的签名属性（如果存在）。如果该属性不可用，则它会退化到 [`Field.getType()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#getType--) ，而这不会因为泛型的引入而改变。对于某些*Foo*值，使用名称 `getGeneric*Foo*` 反射的其他方法也是类似地实现的。

