#### 获取方法参数名称

通过方法 [`java.lang.reflect.Executable.getParameters`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Executable.html#getParameters--) 你可以获取任何方法或者构造器的形式参数名称。（ [`Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html) 和 [`Constructor`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Executable.html) 类扩展了 [`Executable`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Executable.html) 类，因而继承了方法`Executable.getParameters` 。）然而，默认情况下`.class`文件并没有保存形式参数名称。这是因为许多生成和使用类文件的工具都不希望较大的`.class`文件尺寸来包含形式参数名称。特别地，如果这些工具必须处理更大的`.class`文件，则 Java 虚拟机将使用更多的内存。另外，某些参数名称，比如`secret`或者`password`，可能会暴露安全敏感方法的信息。

为了将形式参数名称保存到特定`.class`文件中，使得反射 API 可以获取形式参数名称，使用携带`-paramdters`参数的`javac`编译器命令编译该源代码文件。

 [`MethodParameterSpy`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodParameterSpy.java) 示例展示了如何获取给定类的所有方法和构造器的形式参数名称。该示例同时打印出有关每个参数的其它信息。

下面的命令打印 [`ExampleMethods`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ExampleMethods.java) 类中方法和构造器参数的形式参数名称。

**注意：** 记住使用`-parameters`编译器参数来编译示例`ExampleMethods` 。

```
java MethodParameterSpy ExampleMethods
```

该命令输出如下内容：

```
Number of constructors: 1

Constructor #1
public ExampleMethods()

Number of declared constructors: 1

Declared constructor #1
public ExampleMethods()

Number of methods: 4

Method #1
public boolean ExampleMethods.simpleMethod(java.lang.String,int)
             Return type: boolean
     Generic return type: boolean
         Parameter class: class java.lang.String
          Parameter name: stringParam
               Modifiers: 0
            Is implicit?: false
        Is name present?: true
           Is synthetic?: false
         Parameter class: int
          Parameter name: intParam
               Modifiers: 0
            Is implicit?: false
        Is name present?: true
           Is synthetic?: false

Method #2
public int ExampleMethods.varArgsMethod(java.lang.String...)
             Return type: int
     Generic return type: int
         Parameter class: class [Ljava.lang.String;
          Parameter name: manyStrings
               Modifiers: 0
            Is implicit?: false
        Is name present?: true
           Is synthetic?: false

Method #3
public boolean ExampleMethods.methodWithList(java.util.List<java.lang.String>)
             Return type: boolean
     Generic return type: boolean
         Parameter class: interface java.util.List
          Parameter name: listParam
               Modifiers: 0
            Is implicit?: false
        Is name present?: true
           Is synthetic?: false

Method #4
public <T> void ExampleMethods.genericMethod(T[],java.util.Collection<T>)
             Return type: void
     Generic return type: void
         Parameter class: class [Ljava.lang.Object;
          Parameter name: a
               Modifiers: 0
            Is implicit?: false
        Is name present?: true
           Is synthetic?: false
         Parameter class: interface java.util.Collection
          Parameter name: c
               Modifiers: 0
            Is implicit?: false
        Is name present?: true
           Is synthetic?: false
```

 `MethodParameterSpy` 示例使用下面的方法，这些方法来自 [`Parameter`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html) 类：

- [`getType`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html#getType--): 返回一个 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 对象来标识参数的声明类型。

- [`getName`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html#getName--): 返回参数的名称。如果参数名称存在，则本方法返回由`.class`文件提供的名称。否则，本方法合成一个`arg*N*`形式的参数名称，其中的`*N*`是该参数在方法声明中的索引下标。

  比如，假定你编译 `ExampleMethods` 而没有指定 `-parameters` 编译器参数。示例 `MethodParameterSpy` 将为 `ExampleMethods.simpleMethod` 方法打印下面的内容：

  ```
  public boolean ExampleMethods.simpleMethod(java.lang.String,int)
               Return type: boolean
       Generic return type: boolean
           Parameter class: class java.lang.String
            Parameter name: arg0
                 Modifiers: 0
              Is implicit?: false
          Is name present?: false
             Is synthetic?: false
           Parameter class: int
            Parameter name: arg1
                 Modifiers: 0
              Is implicit?: false
          Is name present?: false
             Is synthetic?: false
  ```

- [`getModifiers`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html#getModifiers--) : 返回表示形式参数拥有的各种特性的一个整数。该值是以下各个值之和，如果适用于形式参数。

  | Value (in decimal) | Value (in hexadecimal | Description                         |
  | ------------------ | --------------------- | ----------------------------------- |
  | 16                 | 0x0010                | 形式参数声明为 `final`                     |
  | 4096               | 0x1000                | 形式参数是合成的。另外，你可以调用方法 `isSynthetic`   |
  | 32768              | 0x8000                | 参数在源代码中隐式声明。另外，你可以调用方法 `isImplicit` |

- [`isImplicit`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html#isImplicit--): 如果参数在源代码中隐式声明，则返回`true`。参考 [Implicit and Synthetic Parameters](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html#implcit_and_synthetic) 获取更多信息。

- [`isNamePresent`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html#isNamePresent--): 如果按照`.class`文件中有参数名称则返回`true`。

- [`isSynthetic`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Parameter.html#isSynthetic--): 如果参数在源代码中既没有隐式声明也没有显式声明，则返回`true`。参考 [Implicit and Synthetic Parameters](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html#implcit_and_synthetic) 获取更多信息。

**[隐式和合成参数]()**

某些构造器是在源代码中隐式声明的，如果它们没有显式写出来。比如， [`ExampleMethods`](https://docs.oracle.com/javase/tutorial/reflect/member/example/ExampleMethods.java) 示例并不包含一个构造器。一个默认构造器将隐式声明。 `MethodParameterSpy` 示例打印有关为`ExampleMethods`隐式声明的构造器的信息：

```
Number of declared constructors: 1
public ExampleMethods()
```

考虑下面来自 [`MethodParameterExamples`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodParameterExamples.java) 的片段：

```java
public class MethodParameterExamples {
    public class InnerClass { }
}
```

`InnerClass`类是一个非静态 [nested class](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html) 或内部类。内部类的构造函数也是隐式声明的。但是，此构造函数将包含一个参数。当Java编译器编译`InnerClass`时，它会创建一个`.class`文件，该文件代表示似于以下内容的代码：

```java
public class MethodParameterExamples {
    public class InnerClass {
        final MethodParameterExamples parent;
        InnerClass(final MethodParameterExamples this$0) {
            parent = this$0; 
        }
    }
}
```

`InnerClass`构造器包含一个参数，该参数类型是包含`InnerClass`的类，也就是`MethodParameterExamples`。接下来，示例`MethodParameterExamples` 打印如下内容：

```
public MethodParameterExamples$InnerClass(MethodParameterExamples)
         Parameter class: class MethodParameterExamples
          Parameter name: this$0
               Modifiers: 32784
            Is implicit?: true
        Is name present?: true
           Is synthetic?: false
```

由于`InnerClass`的构造器是隐式声明的，它的参数也就是隐式的。

**注意**:

- Java 编译器为内部类的构造器创建形式参数以允许编译器传递一个来自创建表达式的引用（表示该内部类所在的直接外部类实例）给成员类的构造器。
- 值 32784 意味着`InnerClass`构造器的参数同时是`final`（16）和隐式（32768）的。
- Java 编程语言本身允许在变量名称中使用美元符号`$`，不过，按照惯例，我们并不会这么做。

如果Java编译器生成的构造与源代码中显式或隐式声明的构造不对应，则将其标记为合成构造，除非它们是类初始化方法。合成构造是由编译器生成的组件，这些组件在不同的实现中有所不同。请考虑以下摘自 [`MethodParameterExamples`](https://docs.oracle.com/javase/tutorial/reflect/member/example/MethodParameterExamples.java) 的片段：

```java
public class MethodParameterExamples {
    enum Colors {
        RED, WHITE;
    }
}
```

当Java编译器遇到`enum`构造时，它会创建几个与`.class`文件结构兼容的方法，并提供`enum`构造的预期功能。例如，Java编译器将为`enum`构造`Colors`创建一个`.class`文件。代表类似于以下内容的代码：

```java
final class Colors extends java.lang.Enum<Colors> {
    public final static Colors RED = new Colors("RED", 0);
    public final static Colors BLUE = new Colors("WHITE", 1);
 
    private final static values = new Colors[]{ RED, BLUE };
 
    private Colors(String name, int ordinal) {
        super(name, ordinal);
    }
 
    public static Colors[] values(){
        return values;
    }
 
    public static Colors valueOf(String name){
        return (Colors)java.lang.Enum.valueOf(Colors.class, name);
    }
}
```

Java编译器为此 `enum` 构造创建三个构造函数和方法：`Colors(String name, int ordinal)`, `Colors[] values()`, and `Colors valueOf(String name)`。 `values` 和 `valueOf` 是隐式声明的。因此，它们的形式参数名也被隐式声明。

 `enum` 构造函数 `Colors(String name, int ordinal)` 是默认构造函数，它是隐式声明的。但是，此隐式声明构造函数的形式参数（`name`和`ordinal`）并不是隐式声明的。由于这些形式参数既未明确声明也未隐式声明，因此它们是合成的。（`enum`构造的默认构造函数的形式参数不是隐式声明的，因为不同的编译器不需要在这个构造函数的形式上达成一致；另一个Java编译器可能为它指定不同的形式参数。当编译器编译使用枚举常量的表达式时，它们仅依赖于枚举构造的公共静态字段，这些字段是隐式声明的，而不是它们的构造函数或这些常量的初始化方式。）

因此，示例`MethodParameterExample`打印有关`enum`构造`Colors`的以下内容：

```
enum Colors:

Number of constructors: 0

Number of declared constructors: 1

Declared constructor #1
private MethodParameterExamples$Colors()
         Parameter class: class java.lang.String
          Parameter name: $enum$name
               Modifiers: 4096
            Is implicit?: false
        Is name present?: true
           Is synthetic?: true
         Parameter class: int
          Parameter name: $enum$ordinal
               Modifiers: 4096
            Is implicit?: false
        Is name present?: true
           Is synthetic?: true

Number of methods: 2

Method #1
public static MethodParameterExamples$Colors[]
    MethodParameterExamples$Colors.values()
             Return type: class [LMethodParameterExamples$Colors;
     Generic return type: class [LMethodParameterExamples$Colors;

Method #2
public static MethodParameterExamples$Colors
    MethodParameterExamples$Colors.valueOf(java.lang.String)
             Return type: class MethodParameterExamples$Colors
     Generic return type: class MethodParameterExamples$Colors
         Parameter class: class java.lang.String
          Parameter name: name
               Modifiers: 32768
            Is implicit?: true
        Is name present?: true
           Is synthetic?: false
```

有关隐式声明的构造的更多信息，请参阅 [Java Language Specification](https://docs.oracle.com/javase/specs/) ，包括在Reflection API中显示为隐式的参数。

