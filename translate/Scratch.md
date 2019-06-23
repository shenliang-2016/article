#### 安全管理器

*安全管理器*是定义应用程序安全策略的对象。此策略指定不安全或敏感的操作。安全策略不允许的任何操作都会导致抛出 [`SecurityException`](https://docs.oracle.com/javase/8/docs/api/java/lang/SecurityException.html) 。应用程序还可以查询其安全管理器以发现允许的操作。

通常，Web applet与浏览器或Java Web Start插件提供的安全管理器一起运行。其他类型的应用程序通常在没有安全管理器的情况下运行，除非应用程序本身定义一个。否则 如果没有安全管理器，则该应用程序没有安全策略，其运行没有任何限制。

本节介绍应用程序如何与现有安全管理器进行交互。有关更多详细信息，包括有关如何设计安全管理器的信息，请参阅 [Security Guide](https://docs.oracle.com/javase/8/docs/technotes/guides/security/index.html) 。

**与安全管理器交互**

安全管理器是 [`SecurityManager`](https://docs.oracle.com/javase/8/docs/api/java/lang/SecurityManager.html) 类型的对象；要获取对此对象的引用，请调用`System.getSecurityManager`。

```java
SecurityManager appsm = System.getSecurityManager();
```

如果没有安全管理器，则此方法返回`null`。

一旦应用程序具有对安全管理器对象的引用，它就可以请求执行特定事务的权限。标准库中的许多类都是这样做的。例如，以退出状态终止Java虚拟机的`System.exit`调用`SecurityManager.checkExit`以确保当前线程具有关闭应用程序的权限。

`SecurityManager`类定义了许多用于验证其他类型操作的其他方法。例如，`SecurityManager.checkAccess`验证线程访问，`SecurityManager.checkPropertyAccess`验证对指定属性的访问。每个操作或一组操作都有自己的 `check*XXX*()` 方法。

此外， `check*XXX*()` 方法的集合表示已经受到安全管理器保护的操作集。通常，应用程序不必直接调用任何 `check*XXX*()` 方法。

**识别安全违规**

在没有安全管理器的情况下，许多常规操作在使用安全管理器运行时都会抛出`SecurityException`。即使在调用未记录为抛出`SecurityException`的方法时也是如此。例如，请考虑以下用于读取文件的代码：

```java
reader = new FileReader("xanadu.txt");
```

在缺少安全管理器的情况下，如果`xanadu.txt`存在且可读，则此语句无错误地执行。但是假设此语句插入到Web applet中，该applet通常在不允许文件输入的安全管理器下运行。可能会导致以下错误消息：

```shell
appletviewer fileApplet.html
Exception in thread "AWT-EventQueue-1" java.security.AccessControlException: access denied (java.io.FilePermission characteroutput.txt write)
        at java.security.AccessControlContext.checkPermission(AccessControlContext.java:323)
        at java.security.AccessController.checkPermission(AccessController.java:546)
        at java.lang.SecurityManager.checkPermission(SecurityManager.java:532)
        at java.lang.SecurityManager.checkWrite(SecurityManager.java:962)
        at java.io.FileOutputStream.<init>(FileOutputStream.java:169)
        at java.io.FileOutputStream.<init>(FileOutputStream.java:70)
        at java.io.FileWriter.<init>(FileWriter.java:46)
...
```

请注意，在这种情况下抛出的特定异常 [`java.security.AccessControlException`](https://docs.oracle.com/javase/8/docs/api/java/security/AccessControlException.html) 是`SecurityException`的子类。

#### 系统中的其它方法

本节介绍了前面几节中未介绍的`System`中的一些方法。

`arrayCopy`方法有效地在数组之间复制数据。有关更多信息，请参阅 [Language Basics](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/index.html) 课程中的 [Arrays](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/arrays.html) 。

 [`currentTimeMillis`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#currentTimeMillis--) 和 [`nanoTime`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#nanoTime--) 方法可用于测量应用程序执行期间的时间间隔。要以毫秒为单位测量时间间隔，请在间隔的开始和结束时调用`currentTimeMillis`两次，并减去从第二次调用返回的第一个值。同样，调用`nanoTime`两次测量纳秒单位的时间间隔。

----

**注意：** `currentTimeMillis`和`nanoTime`的准确性受操作系统提供的时间服务的限制。不要假设`currentTimeMillis`精确到最接近的毫秒，或者`nanoTime`精确到最接近的纳秒。此外，`currentTimeMillis`和`nanoTime`都不应用于确定当前时间。使用高级方法，例如 [`java.util.Calendar.getInstance`](https://docs.oracle.com/javase/8/docs/api/java/util/Calendar.html#getInstance--) 。

----

 [`exit`](https://docs.oracle.com/javase/8/docs/api/java/lang/System.html#exit-int-) 方法使Java虚拟机关闭，并使用参数指定的整数退出状态码。退出状态码可用于启动应用程序的进程。按照惯例，退出状态码为`0`表示应用程序正常终止，而任何其他值都是错误代码。

