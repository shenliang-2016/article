### 方法

*方法*包含可以调用的可执行代码。方法被继承、以及在非反射代码行为中的诸如重载，重写和隐藏都由编译器强制执行。相反，反射代码使得方法选择可以被限制在特定的类而不考虑其超类。可以访问超类方法，但可以确定它们的声明类：如果没有反射，这是不可能以编程方式实现的，并且是许多微妙错误的根源。

[`java.lang.reflect.Method`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Method.html) 类提供了访问方法修饰符、返回类型、参数、注解以及抛出异常等相关信息的 API。它还可以被用于调用方法。下面章节包含这些主题：

- [获取方法类型信息](https://docs.oracle.com/javase/tutorial/reflect/member/methodType.html) 展示如何列出一个类中声明的方法并获取方法类型信息
- [获取方法参数名称](https://docs.oracle.com/javase/tutorial/reflect/member/methodparameterreflection.html) 展示如何获取方法或者构造器方法参数的名称以及其他信息
- [获取并解析方法修饰符](https://docs.oracle.com/javase/tutorial/reflect/member/methodModifiers.html) 描述如何访问并解析与方法有关的修饰符以及其他信息
- [调用方法](https://docs.oracle.com/javase/tutorial/reflect/member/methodInvocation.html) 展示如何执行方法并获取其返回值
- [故障排除](https://docs.oracle.com/javase/tutorial/reflect/member/methodTrouble.html) 涵盖查找或者调用方法时可能发生的错误

#### 获取方法类型信息

