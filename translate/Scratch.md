## 成员

反射定义了一个接口 [`java.lang.reflect.Member`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Member.html) ，被 [`java.lang.reflect.Field`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html) ，[`java.lang.reflect.Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html) ， 和 [`java.lang.reflect.Constructor`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html) 实现。这些对象将在本章中讨论。对每个成员，本课程将介绍相关的 API 来获取声明和类型信息，任何专属于该成员的操作（比如，设定字段值或者调用一个方法），以及可能常见的错误。接下来我们将使用代码样本和相关输出来说明每个概念，其近似于一些预期的反射应用场景。

----

**注意：** 根据 [*The Java Language Specification, Java SE 7 Edition*](https://docs.oracle.com/javase/specs/jls/se7/html/index.html) ，类的成员是继承的类主体组件，包括字段，方法，嵌套类，接口，以及枚举类型。由于构造器无法被继承，它们不是成员。这一点不同于 [`java.lang.reflect.Member`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Member.html) 的实现类。

----

**字段**

字段拥有类型和值两种属性。 [`java.lang.reflect.Field`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html) 类提供了相关的方法来访问字段的类型信息，设定和获取给定对象的一个字段的值。

- [获取字段类型](https://docs.oracle.com/javase/tutorial/reflect/member/fieldTypes.html) 描述如何获取字段的声明和泛型类型
- [检索和解析字段修饰符](https://docs.oracle.com/javase/tutorial/reflect/member/fieldModifiers.html) 展示如何获取字段声明中修饰符部分，比如 `public` 或者 `transient`
- [获取和设定字段值](https://docs.oracle.com/javase/tutorial/reflect/member/fieldValues.html) 举例说明如何访问字段值
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/member/fieldTrouble.html) 描述某些常见可能导致困惑的编码错误

**方法**

方法拥有返回值，参数，可能会抛出异常。 [`java.lang.reflect.Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html) 类提供了相关的方法来获取参数和返回值的类型信息。它也可以被用于调用给定对象上的方法。

- [获取方法类型信息](https://docs.oracle.com/javase/tutorial/reflect/member/methodType.html) 展示如何列出类中声明的方法，并获取类型信息
- [获取方法参数名称](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html) 展示如何获取一个方法或者构造器参数的名称和其它信息
- [获取并解析方法修饰符](https://docs.oracle.com/javase/tutorial/reflect/member/methodModifiers.html) 描述如何访问并解码与方法关联的修饰符及其它信息
- [调用方法](https://docs.oracle.com/javase/tutorial/reflect/member/methodInvocation.html) 举例说明如何执行一个方法并获取它的返回值
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/member/methodTrouble.html) 涵盖查找或者调用方法时的常见错误

**构造器**

用于构造器的反射 API 定义在 [`java.lang.reflect.Constructor`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Constructor.html) 中，类似于用于方法的 API，除了两处意外：首先，构造器没有返回值；其次，构造器的调用创建一个跟定类的新的实例对象。

- [查找构造器](https://docs.oracle.com/javase/tutorial/reflect/member/ctorLocation.html) 举例说明如何获取携带特定参数的构造器
- [获取并解析构造器修饰符](https://docs.oracle.com/javase/tutorial/reflect/member/ctorModifiers.html) 展示如何获取构造器声明中的修饰符及有关该构造器的其它信息
- [创建新的类实例](https://docs.oracle.com/javase/tutorial/reflect/member/ctorInstance.html) 展示如何通过调用构造器实例化一个对象实例
- [故障排除Troubleshooting](https://docs.oracle.com/javase/tutorial/reflect/member/ctorTrouble.html) 描述在查找或者调用构造器时的常见错误

### 字段

