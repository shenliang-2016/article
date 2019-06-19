#### 监控目录和文件变化

您是否曾经发现自己使用IDE或其他编辑器编辑文件，并出现一个对话框，通知您文件系统中的某个打开文件已更改并需要重新加载？ 或者，与NetBeans IDE一样，应用程序只是在不通知您的情况下安静地更新文件。以下示例对话框显示了此通知在免费编辑器 [jEdit](http://sourceforge.net/projects/jedit/) 中的显示方式：

![Sample jEdit Dialog stating: The following files were changed on disk by another program.](https://docs.oracle.com/javase/tutorial/figures/essential/io-jEditDialog.png)

`jEdit`对话框显示检测到修改过的文件

要实现此功能（称为文件更改通知），程序必须能够检测文件系统上相关目录的内容。一种方法是轮询文件系统以查找更改，但这种方法效率低下。它不能扩展到具有数百个要监视的打开文件或目录的应用程序。

`java.nio.file`包提供了一个名为`Watch Service API`的文件更改通知API。此API使您可以使用监视服务注册目录（或多个目录）。注册时，您告诉服务您感兴趣的事件类型：文件创建，文件删除或文件修改。当服务检测到感兴趣的事件时，它将被转发到注册的进程。已注册的进程有一个线程（或一个线程池），专门用于监视它已注册的任何事件。当一个事件进入时，它会根据需要进行处理。

本章节涵盖以下内容：

- [监控服务概览](https://docs.oracle.com/javase/tutorial/essential/io/notification.html#overview)
- [试一试](https://docs.oracle.com/javase/tutorial/essential/io/notification.html#try)
- [创建监控服务并注册事件](https://docs.oracle.com/javase/tutorial/essential/io/notification.html#register)
- [事件处理](https://docs.oracle.com/javase/tutorial/essential/io/notification.html#process)
- [获取文件名](https://docs.oracle.com/javase/tutorial/essential/io/notification.html#name)
- [此 API 的使用时机](https://docs.oracle.com/javase/tutorial/essential/io/notification.html#concerns)

**监控服务概览**

`WatchService` API相当底层，允许自定义。您可以按原样使用它，也可以选择在此机制之上创建高级API，以便它适合您的特定需求。

以下是实现监视服务所需的基本步骤：

 - 为文件系统创建`WatchService` “观察者”。
 - 对于要监视的每个目录，请将其注册到观察程序。注册目录时，您可以指定要通知的事件类型。您为每个注册的目录收到一个`WatchKey`实例。
 - 实现无限循环以等待传入事件。当事件发生时，`WatchKey`将发出信号并放入观察者的队列中。
 - 从观察者的队列中检索`WatchKey`。您可以从`WatchKey`中获取文件名。
 - 检索`WatchKey`的每个待处理事件（可能有多个事件）并根据需要进行处理。
 - 重置`WatchKey`，然后继续等待事件。
 - 关闭服务：当线程退出或关闭时（通过调用其`closed`方法），监视服务退出。

`WatchKeys`是线程安全的，可以与`java.nio.concurrent`包一起使用。您可以将 [线程池](https://docs.oracle.com/javase/tutorial/essential/concurrency/pools.html) 专用于此工作。

**试一试**

因为此API更高级，所以在继续之前尝试一下。将 [`WatchDir`](https://docs.oracle.com/javase/tutorial/essential/io/examples/WatchDir.java) 示例保存到您的计算机，然后进行编译。创建将传递给示例的`test`目录。`WatchDir`使用单个线程来处理所有事件，因此它在等待事件时阻止键盘输入。在单独的窗口中或在后台运行程序，如下所示：

```
java WatchDir test &
```

在`test`目录中创建，删除和编辑文件。发生任何这些事件时，会向控制台输出一条消息。完成后，删除`test`目录并退出`WatchDir`。或者，如果您愿意，可以手动终止该过程。

您还可以通过指定`-r`选项来查看整个文件树。指定`-r`时，`WatchDir`遍历文件树，使用监视服务注册每个目录。

**创建监控服务并注册事件**

第一步是使用`FileSystem`类中的 [`newWatchService`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/FileSystem.html#newWatchService--) 方法创建一个新的 [`WatchService`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchService.html) ，如下所示：

```java
WatchService watcher = FileSystems.getDefault().newWatchService();
```

接下来，使用监视服务注册一个或多个对象。可以注册实现 [`Watchable`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Watchable.html) 接口的任何对象。`Path`类实现`Watchable`接口，因此每个要监视的目录都注册为`Path`对象。

与任何`Watchable`一样，`Path类`实现两个 `register` 方法。此页面使用双参数版本， [`register(WatchService, WatchEvent.Kind...)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Path.html#register-java.nio.file.WatchService-java.nio.file.WatchEvent.Kind...-) 。（三参数版本采用`WatchEvent.Modifier`，目前尚未实现。）

使用监视服务注册对象时，可以指定要监视的事件类型。支持的 [`StandardWatchEventKinds`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/StandardWatchEventKinds.html) 事件类型如下：

- `ENTRY_CREATE` – 目录实体被创建
- `ENTRY_DELETE` – 目录实体被删除
- `ENTRY_MODIFY` – 目录实体被修改
- `OVERFLOW` – 表示事件可能已丢失或丢弃。您无需注册`OVERFLOW`事件即可接收它。

以下代码段显示了如何为所有三种事件类型注册`Path`实例：

```java
import static java.nio.file.StandardWatchEventKinds.*;

Path dir = ...;
try {
    WatchKey key = dir.register(watcher,
                           ENTRY_CREATE,
                           ENTRY_DELETE,
                           ENTRY_MODIFY);
} catch (IOException x) {
    System.err.println(x);
}
```

**事件处理**

事件处理循环中事件的顺序如下：

1. 获取一个`WatchKey`。提供了3个方法：
   - [`poll`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchService.html#poll--) – 返回排队的键（如果可用）。如果不可用，则立即返回`null`值。
   - [`poll(long, TimeUnit)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchService.html#poll-long-java.util.concurrent.TimeUnit-) – 返回排队的键（如果有）。如果排队的键不能立即可用，程序将等待指定的时间。`TimeUnit`参数确定指定的时间是纳秒，毫秒还是某个其他时间单位。
   - [`take`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchService.html#take--) – 返回排队的键。如果没有可用的排队键，则此方法将等待。
2. 处理`WatchKey`对应的等待事件。您从 [`pollEvents`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchKey.html#pollEvents--) 方法获取 [`WatchEvents`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchEvent.html) 的 `List` 。
3. 使用 [`kind`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchEvent.html#kind--) 方法检索事件类型。无论`WatchKey`注册的是什么事件，都可以收到`OVERFLOW`事件。您可以选择处理它或忽略它，但您应该测试这种情况。
4. 检索与事件关联的文件名。文件名存储为事件的上下文，因此 [`context`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchEvent.html#context--) 方法用于检索它。
5. 处理完`WatchKey`事件后，需要通过调用 [`reset`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchEvent.html#reset--) 将`WatchKey`恢复到 `ready` 状态。如果此方法返回`false`，则该`WatchKey`不再有效，并且循环可以退出。这一步非常重要。如果您未能调用`reset`，则此`WatchKey`不会再接收任何事件。

`WatchKey`是有状态的，在任何给定时刻，它的状态可能是下面中的一个：

- `Ready` 表示`WatchKey`已准备好接受事件。首次创建时，`WatchKey`处于就绪状态。
- `Signaled` 表示一个或多个事件已排队。一旦发出`WatchKey`信号，它就不再处于就绪状态，直到调用 [`reset`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchKey.html#reset--) 方法。
- `Invalid` 表示`WatchKey`不再有效。发生以下事件之一时会进入此状态：
  - 该过程使用 [`cancel`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchKey.html#cancel--) 方法明确取消`WatchKey`。
  - 目录变为不可访问。
  - 监控服务被 [关闭](https://docs.oracle.com/javase/8/docs/api/java/nio/file/WatchService.html#close--) 。

以下是事件处理循环的示例。它取自 [`Email`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Email.java) 示例，该示例监视目录，等待新文件出现。当新文件可用时，将使用 [`probeContentType(Path)`](https://docs.oracle.com/javase/8/docs/api/java/nio/file/Files.html#probeContentType-java.nio.file.Path-) 方法检查它是否为`text/plain`文件。目的是将`text/plain`文件通过电子邮件发送到一个地址别名，但该实现细节留给读者。

监控服务API特有的方法以粗体显示：

```java
for (;;) {

    // wait for key to be signaled
    WatchKey key;
    try {
        key = watcher.take();
    } catch (InterruptedException x) {
        return;
    }

    for (WatchEvent<?> event: key.pollEvents()) {
        WatchEvent.Kind<?> kind = event.kind();

        // This key is registered only
        // for ENTRY_CREATE events,
        // but an OVERFLOW event can
        // occur regardless if events
        // are lost or discarded.
        if (kind == OVERFLOW) {
            continue;
        }

        // The filename is the
        // context of the event.
        WatchEvent<Path> ev = (WatchEvent<Path>)event;
        Path filename = ev.context();

        // Verify that the new
        //  file is a text file.
        try {
            // Resolve the filename against the directory.
            // If the filename is "test" and the directory is "foo",
            // the resolved name is "test/foo".
            Path child = dir.resolve(filename);
            if (!Files.probeContentType(child).equals("text/plain")) {
                System.err.format("New file '%s'" +
                    " is not a plain text file.%n", filename);
                continue;
            }
        } catch (IOException x) {
            System.err.println(x);
            continue;
        }

        // Email the file to the
        //  specified email alias.
        System.out.format("Emailing file %s%n", filename);
        //Details left to reader....
    }

    // Reset the key -- this step is critical if you want to
    // receive further watch events.  If the key is no longer valid,
    // the directory is inaccessible so exit the loop.
    boolean valid = key.reset();
    if (!valid) {
        break;
    }
}
```

**获取文件名**

从事件上下文中检索文件名。[`Email`](https://docs.oracle.com/javase/tutorial/essential/io/examples/Email.java) 示例使用以下代码检索文件名：

```java
WatchEvent<Path> ev = (WatchEvent<Path>)event;
Path filename = ev.context();
```

编译 `Email` 示例时，它会生成以下错误：

```
Note: Email.java uses unchecked or unsafe operations.
Note: Recompile with -Xlint:unchecked for details.
```

此错误是将`WatchEvent<T>`强制转换为 `WatchEvent<Path>`的代码行的结果。[`WatchDir`](https://docs.oracle.com/javase/tutorial/essential/io/examples/WatchDir.java) 示例通过创建一个抑制未经检查的警告的实用程序强制转换方法来避免此错误，如下所示：

```java
@SuppressWarnings("unchecked")
static <T> WatchEvent<T> cast(WatchEvent<?> event) {
    return (WatchEvent<Path>)event;
}
```

如果不熟悉 `@SuppressWarnings` 语法，参考 [注解](https://docs.oracle.com/javase/tutorial/java/annotations/index.html) 。

**使用时机**

Watch Service API专为需要通知文件更改事件的应用程序而设计。它非常适合任何应用程序，如编辑器或IDE，可能有许多打开的文件，需要确保文件与文件系统同步。它也非常适合于监视目录的应用程序服务器，可能等待`.jsp`或`.jar`文件变化，以便随时部署它们。

此API不适用于索引硬盘驱动器。大多数文件系统实现都具有文件更改通知的本机支持。Watch Service API在可用的情况下利用此支持。但是，当文件系统不支持此机制时，Watch Service将轮询文件系统，等待事件。

