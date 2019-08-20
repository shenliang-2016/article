## 数组和枚举类型

从 Java 虚拟机角度看来，数组和枚举类型也仅仅是类而已。 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 中的许多方法都可以用于它们。反射提供了一些特殊的 API 给数组和枚举。本课程使用一系列代码示例描述如何将这些类型的对象区别于其它类对象，并在其上执行操作。同时也解释了可能遇到的各种错误。

**数组**

数组拥有元素类型以及一个长度属性（该属性并不是该类型的一部分）。数组可以整体被修改，或者以元素为单位修改。反射提供了 [`java.lang.reflect.Array`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html) 用来实现后一种操作。

- [识别数组类型](https://docs.oracle.com/javase/tutorial/reflect/special/arrayComponents.html) 描述如何确定一个类成员是一个字段还是数组类型。
- [创建新数组](https://docs.oracle.com/javase/tutorial/reflect/special/arrayInstance.html) 展示如何创建包含简单或者复杂类型元素的数组。
- [获取和设定数组以及它们的元素](https://docs.oracle.com/javase/tutorial/reflect/special/arraySetGet.html) 展示如何访问数组类型字段或者单独访问数组元素。
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/special/arrayTrouble.html) 涵盖常见错误和编程误解。

**枚举类型**

在反射代码中，枚举类型的处理与普通类型没有什么区别。 [`Class.isEnum()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#isEnum--) 告诉我们是否一个 [`Class`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html) 表示并且`enum` 。 [`Class.getEnumConstants()`](https://docs.oracle.com/javase/8/docs/api/java/lang/Class.html#getEnumConstants--) 检索枚举类中定义的枚举常量。[`java.lang.reflect.Field.isEnumConstant()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#isEnumConstant--) 指出一个字段是否是枚举类型。

- [检查枚举](https://docs.oracle.com/javase/tutorial/reflect/special/enumMembers.html) 展示如何检索一个枚举常量以及任何其它字段、构造器、以及方法。
- [获取和设定枚举类型字段](https://docs.oracle.com/javase/tutorial/reflect/special/enumSetGet.html) 展示如何获取和设置一个使用枚举常量值的字段。
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/special/enumTrouble.html) 描述有关枚举的常见错误。

### 数组

数组是引用类型的对象，它包含固定数量的相同类型的元素，数组的长度是不可变的。创建数组实例需要了解长度和元素类型。每个元素可以是基本类型（例如，`byte`，`int`或`double`），引用类型（例如，`String`，`Object`，或者 `java.nio.CharBuffer`）或数组。多维数组实际上只是包含数组类型元素的数组。

数组在 Java 虚拟机内部实现。数组上的方法都是继承自 [`Object`](https://docs.oracle.com/javase/8/docs/api/java/lang/Object.html) 。数组的长度不是它的类型的一部分，数组拥有一个`length`字段，可以通过 [`java.lang.reflect.Array.getLength()`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html#getLength-java.lang.Object-) 访问。

反射提供了方法来访问数组类型和数组元素类型，创建新的数组，以及检索或者设定数组元素值。下面的章节包含数组操作的例子：

- [识别数组类型](https://docs.oracle.com/javase/tutorial/reflect/special/arrayComponents.html) 描述如何确定一个类成员是否是数组类型字段
- [创建新数组](https://docs.oracle.com/javase/tutorial/reflect/special/arrayInstance.html) 展示如何创建简单元素类型和复杂元素类型的数组实例
- [获取和设定数组以及它们的元素](https://docs.oracle.com/javase/tutorial/reflect/special/arraySetGet.html) 展示如何访问数组类型字段或者单独访问数组元素。
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/special/arrayTrouble.html) 涵盖常见错误和编程误解。

所有这些操作都通过 [`java.lang.reflect.Array`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Array.html) 中的`static`方法来支持。

