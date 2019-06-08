#### 创建异常类

当面对选择要抛出的异常类型时，您可以使用其他人编写的异常 -  Java平台提供了许多可以使用的异常类 - 或者您可以编写自己的异常类。如果您对以下任何问题的回答是肯定的，您应该编写自己的异常类；否则，你可能会使用别人的。

 - 您是否需要Java平台中未提供的异常类型？
 - 它是否可以帮助用户将他们的异常与其他供应商编写的类别所引发的异常区分开来？
 - 您的代码是否会抛出多个相关异常？
 - 如果您使用其他人的异常，用户是否可以访问这些异常？ 一个类似的问题是，你的包是否是独立且自包含的？

**例子**

Suppose you are writing a linked list class. The class supports the following methods, among others:

- **objectAt(int n)** — Returns the object in the `n`th position in the list. Throws an exception if the argument is less than 0 or more than the number of objects currently in the list.
- **firstObject()** — Returns the first object in the list. Throws an exception if the list contains no objects.
- **indexOf(Object o)** — Searches the list for the specified `Object` and returns its position in the list. Throws an exception if the object passed into the method is not in the list.

The linked list class can throw multiple exceptions, and it would be convenient to be able to catch all exceptions thrown by the linked list with one exception handler. Also, if you plan to distribute your linked list in a package, all related code should be packaged together. Thus, the linked list should provide its own set of exception classes.

The next figure illustrates one possible class hierarchy for the exceptions thrown by the linked list.

![A possible class hierarchy for the exceptions thrown by a linked list.](https://docs.oracle.com/javase/tutorial/figures/essential/exceptions-hierarchy.gif)

Example exception class hierarchy.

**选择一个超类**

Any `Exception` subclass can be used as the parent class of `LinkedListException`. However, a quick perusal of those subclasses shows that they are inappropriate because they are either too specialized or completely unrelated to `LinkedListException`. Therefore, the parent class of `LinkedListException` should be `Exception`.

Most applets and applications you write will throw objects that are `Exception`s. `Error`s are normally used for serious, hard errors in the system, such as those that prevent the JVM from running.

------

**Note:** For readable code, it's good practice to append the string `Exception` to the names of all classes that inherit (directly or indirectly) from the `Exception` class.

------