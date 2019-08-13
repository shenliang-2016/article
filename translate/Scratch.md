## 类

每个类型要么是引用类型要么是基本类型，类、枚举以及数组（全部集成自[`java.lang.Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html)）以及所有的接口都是引用类型。引用类型的例子包括[`java.lang.String`](https://docs.oracle.com/javase/8/docs/api/java/lang/String.html) ，所有基本数据类型的包装类，比如 [`java.lang.Double`](https://docs.oracle.com/javase/8/docs/api/java/lang/Double.html) ，接口 [`java.io.Serializable`](https://docs.oracle.com/javase/8/docs/api/java/io/Serializable.html) ，以及枚举 [`javax.swing.SortOrder`](https://docs.oracle.com/javase/8/docs/api/javax/swing/SortOrder.html) 。基本数据类型是固定的： `boolean`, `byte`, `short`, `int`, `long`, `char`, `float`, and `double` 。

对于每种类型的对象，Java虚拟机都实例化 [`java.lang.Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 的不可变实例，该实例提供检查对象的运行时属性的方法，包括其成员和类型信息。 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 还提供了创建新类和对象的功能。最重要的是，它是所有反射 API的入口点。本课程介绍了最常用的涉及类的反射操作：

- [Retrieving Class Objects](https://docs.oracle.com/javase/tutorial/reflect/class/classNew.html) 描述获取 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 的方法
- [Examining Class Modifiers and Types](https://docs.oracle.com/javase/tutorial/reflect/class/classModifiers.html) 展示如何访问类声明信息
- [Discovering Class Members](https://docs.oracle.com/javase/tutorial/reflect/class/classMembers.html) 举例说明如何列出构造器、字段、方法以及内部类
- [Troubleshooting](https://docs.oracle.com/javase/tutorial/reflect/class/classTrouble.html) 描述使用 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 时通常可能发生的错误

