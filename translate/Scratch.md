## 编写 RMI 服务器

计算引擎服务器接受来自客户端的任务，执行任务，返回结果。服务器代码由接口和类组成。接口定义了可以从客户端调用的方法。实质上，该接口定义了远程对象的客户端视图。对应的类提供了接口实现。

[设计远程接口](https://docs.oracle.com/javase/tutorial/rmi/designing.html)

本节介绍 `Compute` 接口，提供客户端和服务器之间的连接。你将同时学到 RMI API ，它支持了该通信过程。

[实现远程接口](https://docs.oracle.com/javase/tutorial/rmi/implementing.html)

本节研究实现 `Compute` 接口的类，也就是远程对象实现。该类同时提供了构成服务器程序的其它代码，包括一个 `main` 方法来创建远程对象实例，使用 RMI 注册表注册它，并配置一个安全管理器。

### 设计远程接口

计算引擎的核心是一个协议，它允许将任务提交给计算引擎，计算引擎运行这些任务，将这些任务的结果返回给客户端。此协议在计算引擎支持的接口中表示。该协议的远程通信如下图所示。

![remote communication between a client and the compute engine](https://docs.oracle.com/javase/tutorial/figures/rmi/rmi-3.gif)

每个接口都包含一个方法。计算引擎的远程接口`Compute` 可以将任务提交给引擎。客户端接口 `Task` 定义计算引擎如何执行提交的任务。

 [`compute.Compute`](https://docs.oracle.com/javase/tutorial/rmi/examples/compute/Compute.java) 接口定义了可远程访问的部分，计算引擎本身。下面是 `Compute` 接口的源代码：

```java
package compute;

import java.rmi.Remote;
import java.rmi.RemoteException;

public interface Compute extends Remote {
    <T> T executeTask(Task<T> t) throws RemoteException;
}
```

通过扩展接口`java.rmi.Remote`，`Compute`接口将自己标识为这样一个接口，其方法可以从另一个 Java 虚拟机调用。实现此接口的任何对象都可以是远程对象。

作为远程接口的成员，`executeTask`方法是一种远程方法。因此，必须将此方法定义为能够抛出`java.rmi.RemoteException`。RMI 系统从远程方法调用抛出此异常，以指示发生了通信故障或协议错误。`RemoteException`是一个已检查的异常，因此任何调用远程方法的代码都需要通过捕获它或在其`throws`子句中声明它来处理此异常。

计算引擎所需的第二个接口是`Task`接口，它是`Compute`接口中`executeTask`方法的参数类型。 [`compute.Task`](https://docs.oracle.com/javase/tutorial/rmi/examples/compute/Task.java) 接口定义了计算引擎与它需要做的工作之间的接口，提供开始工作的方式。这是`Task`接口的源代码：

```java
package compute;

public interface Task<T> {
    T execute();
}
```

`Task`接口定义了一个单独的方法`execute`，它没有参数，也没有抛出异常。因为接口不扩展`Remote`，所以此接口中的方法不需要在`throws`子句中列出`java.rmi.RemoteException`。

`Task`接口有一个类型参数`T`，它表示任务计算的结果类型。该接口的`execute`方法返回计算结果，因此其返回类型为`T`。

反过来，`Compute`接口的`executeTask`方法返回传递给它的`Task`实例的执行结果。因此，`executeTask`方法有自己的类型参数`T`，它将自己的返回类型与传递的`Task`实例的结果类型相关联。

RMI 使用 Java 对象序列化机制在 Java 虚拟机之间按值传输对象。对于要被视为可序列化的对象，其类必须实现`java.io.Serializable`标记接口。因此，实现`Task`接口的类也必须实现`Serializable`，用于任务结果的对象类也必须实现。

只要它们是`Task`类型的实现，可以通过`Compute`对象运行不同类型的任务。实现此接口的类可以包含计算任务所需的任何数据以及计算所需的任何其他方法。

以下解释 RMI 如何使这个简单的计算引擎成为可能。因为 RMI 可以假设`Task`对象是用Java编程语言编写的，所以计算引擎之前不知道的`Task`对象的实现会根据需要由 RMI 下载到计算引擎的 Java 虚拟机中。此功能使计算引擎的客户端能够定义要在服务器计算机上运行的新类型的任务，而无需在该计算机上显式安装代码。

由`ComputeEngine`类实现的计算引擎实现了`Compute`接口，通过调用`executeTask`方法，可以将不同的任务提交给它。这些任务使用任务执行的`execute`方法运行，并将结果返回给远程客户端。