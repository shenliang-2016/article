# [Java 8 Lambda 表达式详解](https://segmentfault.com/a/1190000009186509)

[![img](https://avatar-static.segmentfault.com/868/271/868271510-54cb382abb7a1_small) java](https://segmentfault.com/t/java)

发布于 2017-04-25

![img](https://sponsor.segmentfault.com/lg.php?bannerid=0&campaignid=0&zoneid=25&loc=https%3A%2F%2Fsegmentfault.com%2Fa%2F1190000009186509&referer=https%3A%2F%2Fwww.baidu.com%2Flink%3Furl%3DaN_PidNnsvKEzD5HFvqQZJl23DOHPQKHvAzGxlQpQBw7qtfWQ_sU1a_wAvU4ScgVQt09PXD98IladH5Lj0V7GK%26wd%3D%26eqid%3Da11b5e4400156214000000065fab4ea2&cb=8d10a12194)

> 版权声明：本文由*吴仙杰*创作整理，转载请注明出处：https://segmentfault.com/a/1190000009186509

## 1. 引言

在 Java 8 以前，若我们想要把某些功能传递给某些方法，总要去写匿名类。以前注册事件监听器的写法与下面的示例代码就很像：

```java
manager.addScheduleListener(new ScheduleListener() {
    @Override
    public void onSchedule(ScheduleEvent e) {        
        // Event listener implementation goes here...
    }
});
```

这里我们添加了一些自定义代码到 Schedule 监听器中，需要先定义匿名内部类，然后传递一些功能到 `onSchedule` 方法中。

正是 Java 在作为参数传递普通方法或功能的限制，Java 8 增加了一个全新语言级别的功能，称为 **Lambda 表达式**。

## 2. 为什么 Java 需要 Lambda 表达式

Java 是**面向对象**语言，除了原始数据类型之处，Java 中的所有内容都是一个对象。而在**函数式**语言中，我们只需要给函数分配变量，并将这个函数作为参数传递给其它函数就可实现特定的功能。JavaScript 就是功能编程语言的典范（闭包）。

Lambda 表达式的加入，使得 Java 拥有了函数式编程的能力。在其它语言中，Lambda 表达式的类型是一个函数；但在 Java 中，Lambda 表达式被表示为对象，因此它们必须绑定到被称为**功能接口**的特定对象类型。

## 3. Lambda 表达式简介

Lambda 表达式是一个匿名函数（对于 Java 而言并不很准确，但这里我们不纠结这个问题）。简单来说，这是一种没有声明的方法，即没有访问修饰符，返回值声明和名称。

在仅使用一次方法的地方特别有用，方法定义很短。它为我们节省了，如包含类声明和编写单独方法的工作。

Java 中的 Lambda 表达式通常使用语法是 `(argument) -> (body)`，比如：

```java
(arg1, arg2...) -> { body }

(type1 arg1, type2 arg2...) -> { body }
```

以下是 Lambda 表达式的一些示例：

```java
(int a, int b) -> {  return a + b; }

() -> System.out.println("Hello World");

(String s) -> { System.out.println(s); }

() -> 42

() -> { return 3.1415 };
```

### 3.1 Lambda 表达式的结构

Lambda 表达式的结构：

- Lambda 表达式可以具有零个，一个或多个参数。
- 可以显式声明参数的类型，也可以由编译器自动从上下文推断参数的类型。例如 `(int a)` 与刚才相同 `(a)`。
- 参数用小括号括起来，用逗号分隔。例如 `(a, b)` 或 `(int a, int b)` 或 `(String a, int b, float c)`。
- 空括号用于表示一组空的参数。例如 `() -> 42`。
- 当有且仅有一个参数时，如果不显式指明类型，则不必使用小括号。例如 `a -> return a*a`。
- Lambda 表达式的正文可以包含零条，一条或多条语句。
- 如果 Lambda 表达式的正文只有一条语句，则大括号可不用写，且表达式的返回值类型要与匿名函数的返回类型相同。
- 如果 Lambda 表达式的正文有一条以上的语句必须包含在大括号（代码块）中，且表达式的返回值类型要与匿名函数的返回类型相同。

## 4. 方法引用

### 4.1 从 Lambda 表达式到双冒号操作符

使用 Lambda 表达式，我们已经看到代码可以变得非常简洁。

例如，要创建一个比较器，以下语法就足够了

```java
Comparator c = (Person p1, Person p2) -> p1.getAge().compareTo(p2.getAge());
```

然后，使用类型推断：

```java
Comparator c = (p1, p2) -> p1.getAge().compareTo(p2.getAge());
```

但是，我们可以使上面的代码更具表现力和可读性吗？我们来看一下：

```java
Comparator c = Comparator.comparing(Person::getAge);
```

使用 `::` 运算符作为 Lambda 调用特定方法的缩写，并且拥有更好的可读性。

### 4.2 使用方式

双冒号（`::`）操作符是 Java 中的**方法引用**。 当们使用一个方法的引用时，目标引用放在 `::` 之前，目标引用提供的方法名称放在 `::` 之后，即 `目标引用::方法`。比如：

```java
Person::getAge;
```

在 `Person` 类中定义的方法 `getAge` 的方法引用。

然后我们可以使用 `Function` 对象进行操作：

```java
// 获取 getAge 方法的 Function 对象
Function<Person, Integer> getAge = Person::getAge;
// 传参数调用 getAge 方法
Integer age = getAge.apply(p);
```

我们引用 `getAge`，然后将其应用于正确的参数。

目标引用的参数类型是 `Function<T,R>`，`T` 表示传入类型，`R` 表示返回类型。比如，表达式 `person -> person.getAge();`，传入参数是 `person`，返回值是 `person.getAge()`，那么方法引用 `Person::getAge` 就对应着 `Function<Person,Integer>` 类型。

## 5. 什么是功能接口（Functional interface）

在 Java 中，功能接口（Functional interface）指**只有一个**抽象方法的接口。

`java.lang.Runnable` 是一个功能接口，在 `Runnable` 中只有一个方法的声明 `void run()`。我们使用匿名内部类实例化功能接口的对象，而使用 Lambda 表达式，可以简化写法。

每个 Lambda 表达式都可以隐式地分配给功能接口。例如，我们可以从 Lambda 表达式创建 `Runnable` 接口的引用，如下所示：

```java
Runnable r = () -> System.out.println("hello world");
```

当我们不指定功能接口时，这种类型的转换会被编译器自动处理。例如：

```java
new Thread(
    () -> System.out.println("hello world")
).start();
```

在上面的代码中，编译器会自动推断，Lambda 表达式可以从 `Thread` 类的构造函数签名（`public Thread(Runnable r) { }`）转换为 `Runnable` 接口。

`@FunctionalInterface` 是在 Java 8 中添加的一个新注解，用于指示接口类型，声明接口为 Java 语言规范定义的功能接口。Java 8 还声明了 Lambda 表达式可以使用的功能接口的数量。当您注释的接口不是有效的功能接口时， `@FunctionalInterface` 会产生编译器级错误。

以下是自定义功能接口的示例：

```java
package com.wuxianjiezh.demo.lambda;

@FunctionalInterface
public interface WorkerInterface {

    public void doSomeWork();
}
```

正如其定义所述，功能接口只能有一个抽象方法。如果我们尝试在其中添加一个抽象方法，则会抛出编译时错误。例如：

```java
package com.wuxianjiezh.demo.lambda;

@FunctionalInterface
public interface WorkerInterface {

    public void doWork();
    public void doMoreWork();
}
```

错误：

```
Error:(3, 1) java: 意外的 @FunctionalInterface 注释
  com.wuxianjiezh.demo.lambda.WorkerInterface 不是函数接口
    在 接口 com.wuxianjiezh.demo.lambda.WorkerInterface 中找到多个非覆盖抽象方法
```

一旦定义了功能接口，我们就可以利用 Lambda 表达式调用。例如：

```java
package com.wuxianjiezh.demo.lambda;

@FunctionalInterface
public interface WorkerInterface {

    public void doWork();
}

class WorkTest {

    public static void main(String[] args) {
        // 通过匿名内部类调用
        WorkerInterface work = new WorkerInterface() {
            @Override
            public void doWork() {
                System.out.println("通过匿名内部类调用");
            }
        };
        work.doWork();
        
        // 通过 Lambda 表达式调用
        // Lambda 表达式实际上是一个对象。
        // 我们可以将 Lambda 表达式赋值给一个变量，就可像其它对象一样调用。
        work = ()-> System.out.println("通过 Lambda 表达式调用");
        work.doWork();
    }
}
```

运行结果：

```
通过匿名内部类调用
通过 Lambda 表达式调用
```

## 6. Lambda 表达式的例子

### 6.1 线程初始化

线程可以初始化如下：

```java
// Old way
new Thread(new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello world");
    }
}).start();

// New way
new Thread(
    () -> System.out.println("Hello world")
).start();
```

### 6.2 事件处理

事件处理可以用 Java 8 使用 Lambda 表达式来完成。以下代码显示了将 `ActionListener` 添加到 UI 组件的新旧方式：

```java
// Old way
button.addActionListener(new ActionListener() {
    @Override
    public void actionPerformed(ActionEvent e) {
        System.out.println("Hello world");
    }
});

// New way
button.addActionListener( (e) -> {
        System.out.println("Hello world");
});
```

### 6.3 遍例输出（方法引用）

输出给定数组的所有元素的简单代码。请注意，还有一种使用 Lambda 表达式的方式。

```java
// old way
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7);
for (Integer n : list) {
    System.out.println(n);
}

// 使用 -> 的 Lambda 表达式
list.forEach(n -> System.out.println(n));

// 使用 :: 的 Lambda 表达式
list.forEach(System.out::println);
```

### 6.4 逻辑操作

输出通过逻辑判断的数据。

```java
package com.wuxianjiezh.demo.lambda;

import java.util.Arrays;
import java.util.List;
import java.util.function.Predicate;

public class Main {

    public static void main(String[] args) {
        List<Integer> list = Arrays.asList(1, 2, 3, 4, 5, 6, 7);

        System.out.print("输出所有数字：");
        evaluate(list, (n) -> true);

        System.out.print("不输出：");
        evaluate(list, (n) -> false);

        System.out.print("输出偶数：");
        evaluate(list, (n) -> n % 2 == 0);

        System.out.print("输出奇数：");
        evaluate(list, (n) -> n % 2 == 1);

        System.out.print("输出大于 5 的数字：");
        evaluate(list, (n) -> n > 5);
    }

    public static void evaluate(List<Integer> list, Predicate<Integer> predicate) {
        for (Integer n : list) {
            if (predicate.test(n)) {
                System.out.print(n + " ");
            }
        }
        System.out.println();
    }
}
```

运行结果：

```
输出所有数字：1 2 3 4 5 6 7 
不输出：
输出偶数：2 4 6 
输出奇数：1 3 5 7 
输出大于 5 的数字：6 7 
```

### 6.4 Stream API 示例

`java.util.stream.Stream`接口 和 Lambda 表达式一样，都是 Java 8 新引入的。所有 `Stream` 的操作必须以 Lambda 表达式为参数。`Stream` 接口中带有大量有用的方法，比如 `map()` 的作用就是将 input Stream 的每个元素，映射成output Stream 的另外一个元素。

下面的例子，我们将 Lambda 表达式 `x -> x*x` 传递给 `map()` 方法，将其应用于流的所有元素。之后，我们使用 `forEach` 打印列表的所有元素。

```java
// old way
List<Integer> list = Arrays.asList(1,2,3,4,5,6,7);
for(Integer n : list) {
    int x = n * n;
    System.out.println(x);
}

// new way
List<Integer> list = Arrays.asList(1,2,3,4,5,6,7);
list.stream().map((x) -> x*x).forEach(System.out::println);
```

下面的示例中，我们给定一个列表，然后求列表中每个元素的平方和。这个例子中，我们使用了 `reduce()` 方法，这个方法的主要作用是把 Stream 元素组合起来。

```java
// old way
List<Integer> list = Arrays.asList(1,2,3,4,5,6,7);
int sum = 0;
for(Integer n : list) {
    int x = n * n;
    sum = sum + x;
}
System.out.println(sum);

// new way
List<Integer> list = Arrays.asList(1,2,3,4,5,6,7);
int sum = list.stream().map(x -> x*x).reduce((x,y) -> x + y).get();
System.out.println(sum);
```

## 7. Lambda 表达式和匿名类之间的区别

- `this` 关键字。对于匿名类 `this` 关键字解析为匿名类，而对于 Lambda 表达式，`this` 关键字解析为包含写入 Lambda 的类。
- 编译方式。Java 编译器编译 Lambda 表达式时，会将其转换为类的私有方法，再进行动态绑定。