### 创建一个自定义 JMX 客户端

前面的内容向您展示了如何创建JMX技术MBean和MXBeans，以及如何使用JMX代理注册它们。但是，前面的所有示例都使用了现有的JMX客户端JConsole。本课将演示如何创建自己的自定义JMX客户端。

自定义JMX客户端的示例，客户端包含在`jmx_examples.zip`中。此JMX客户端与前面课程中看到的相同MBean，MXBean和JMX代理进行交互。由于`Client`类的大小，它将在以下部分中以分块的形式进行讲解。

**导入 JMX Remote API 类**

为了能够创建与从JMX客户端远程运行的JMX代理的连接，您需要使用 [`javax.management.remote`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/package-summary.html) 中的类。

```java
package com.example;
...

import javax.management.remote.JMXConnector;
import javax.management.remote.JMXConnectorFactory;
import javax.management.remote.JMXServiceURL;

public class Client {
...

```

`Client`类将创建 [`JMXConnector`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXConnector.html) 实例，它需要 [`JMXConnectorFactory`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXConnectorFactory.html) 和 [`JMXServiceURL`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXServiceURL.html) 。

**创建通知监听器**

JMX客户端需要一个通知处理程序，以侦听和处理可能由在JMX代理的MBean服务器中注册的MBean发送的任何通知。JMX客户端的通知处理程序是 [`NotificationListener`](https://docs.oracle.com/javase/8/docs/api/javax/management/NotificationListener.html) 接口的实例，如下所示：

```java
... 

public static class ClientListener implements NotificationListener {

    public void handleNotification(Notification notification,
            Object handback) {
        echo("\nReceived notification:");
        echo("\tClassName: " + notification.getClass().getName());
        echo("\tSource: " + notification.getSource());
        echo("\tType: " + notification.getType());
        echo("\tMessage: " + notification.getMessage());
        if (notification instanceof AttributeChangeNotification) {
            AttributeChangeNotification acn =
                (AttributeChangeNotification) notification;
            echo("\tAttributeName: " + acn.getAttributeName());
            echo("\tAttributeType: " + acn.getAttributeType());
            echo("\tNewValue: " + acn.getNewValue());
            echo("\tOldValue: " + acn.getOldValue());
        }
    }
}    
...       

```

此通知侦听器确定其收到的任何通知的来源，并检索通知中存储的信息。然后，它根据接收的通知类型对通知信息执行不同的动作。在这种情况下，当侦听器收到 [`AttributeChangeNotification`](https://docs.oracle.com/javase/8/docs/api/javax/management/AttributeChangeNotification.html) 类型的通知时，它将通过调用`AttributeChangeNotification`方法`getAttributeName`，`getAttributeType`，`getNewValue`和`getOldValue`来获取已更改的MBean属性的名称和类型，以及其旧值和新值。

下面的代码创建一个新的 `ClientListener` 实例：

```java
ClientListener listener = new ClientListener();
```

**创建 RMI 连接器客户端**

`Client`类创建一个RMI连接器客户端，该客户端配置为连接到启动JMX代理`Main`时将启动的RMI连接器服务器。这将允许JMX客户端与JMX代理进行交互，就像它们在同一台机器上运行一样。

```java
...
    
public static void main(String[] args) throws Exception {

echo("\nCreate an RMI connector client and " +
    "connect it to the RMI connector server");
JMXServiceURL url = 
    new JMXServiceURL("service:jmx:rmi:///jndi/rmi://:9999/jmxrmi");
JMXConnector jmxc = JMXConnectorFactory.connect(url, null);
...        

```

如您所见， `Client` 定义了一个名为`url`的 [`JMXServiceURL`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXServiceURL.html) ，它表示连接器客户端期望找到连接器服务器的位置。此URL允许连接器客户端从运行在本地主机的端口`9999`上的RMI注册表中检索RMI连接器服务器存根`jmxrmi`，并连接到RMI连接器服务器。

通过这样识别的RMI注册表，可以创建连接器客户端。连接器客户端`jmxc`是 [`JMXConnector`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXConnector.html) 接口的一个实例，由 [`JMXConnectorFactory`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXConnectorFactory.html) 的`connect()`方法创建。`connect()`方法在调用时传递参数`url`和`null`环境映射。

**连接到 Remote MBean Server**

在RMI连接到位后，JMX客户端必须连接到远程MBean服务器，以便它可以与远程JMX代理程序在其中注册的各种MBean进行交互。

```java
...
        
MBeanServerConnection mbsc = 
    jmxc.getMBeanServerConnection();
                
...     

```

然后通过调用`JMXConnector`实例`jmxc`的`getMBeanServerConnection()`方法创建名为`mbsc`的 [`MBeanServerConnection`](https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServerConnection.html) 实例。

连接器客户端现在连接到由JMX代理创建的MBean服务器，并且可以注册MBean并对它们执行操作，连接对两端保持完全透明。

首先，客户端定义一些简单的操作来发现有关代理的MBean服务器中找到的MBean的信息。

```java
...
        
echo("\nDomains:");
String domains[] = mbsc.getDomains();
Arrays.sort(domains);
for (String domain : domains) {
    echo("\tDomain = " + domain);
}
        
...
        
echo("\nMBeanServer default domain = " + mbsc.getDefaultDomain());

echo("\nMBean count = " +  mbsc.getMBeanCount());
echo("\nQuery MBeanServer MBeans:");
Set<ObjectName> names = 
    new TreeSet<ObjectName>(mbsc.queryNames(null, null));
for (ObjectName name : names) {
    echo("\tObjectName = " + name);
}
      
...
        
```

客户端调用`MBeanServerConnection`的各种方法，以获取运行不同MBean的域，MBean服务器中注册的MBean数，以及它发现的每个MBean的对象名。

**通过代理在 Remote MBeans 上执行操作**

客户端通过创建MBean代理，通过MBean服务器连接访问MBean服务器中的`Hello` MBean。此MBean代理是客户端的本地代理，并模拟远程MBean。

```java
...

ObjectName mbeanName = new ObjectName("com.example:type=Hello");
HelloMBean mbeanProxy = JMX.newMBeanProxy(mbsc, mbeanName, 
                                          HelloMBean.class, true);

echo("\nAdd notification listener...");
mbsc.addNotificationListener(mbeanName, listener, null, null);

echo("\nCacheSize = " + mbeanProxy.getCacheSize());

mbeanProxy.setCacheSize(150);

echo("\nWaiting for notification...");
sleep(2000);
echo("\nCacheSize = " + mbeanProxy.getCacheSize());
echo("\nInvoke sayHello() in Hello MBean...");
mbeanProxy.sayHello();

echo("\nInvoke add(2, 3) in Hello MBean...");
echo("\nadd(2, 3) = " + mbeanProxy.add(2, 3));

waitForEnterPressed();
        
...
        
```

MBean代理允许您通过Java接口访问MBean，允许您在代理上进行调用，而不必编写冗长的代码来访问远程MBean。通过调用`javax.management.JMX`类中的方法`newMBeanProxy()`，向其传递MBean的`MBeanServerConnection`，对象名，MBean接口的类名和`true`，来表示代理必须表现为一个`NotificationBroadcaster` ，从而创建`Hello`的MBean代理。JMX客户端现在可以执行`Hello`定义的操作（如同它们是本地注册的MBean的操作）。JMX客户端还添加了通知侦听器并更改了MBean的`CacheSize`属性，以使其发送通知。

**通过代理在 Remote MXBeans上执行操作**

您可以使用与创建MBean代理完全相同的方式为MXBean创建代理。

```java
...
        
ObjectName mxbeanName = new ObjectName ("com.example:type=QueueSampler");
QueueSamplerMXBean mxbeanProxy = JMX.newMXBeanProxy(mbsc, 
    mxbeanName,  QueueSamplerMXBean.class);
QueueSample queue1 = mxbeanProxy.getQueueSample();
echo("\nQueueSample.Date = " + queue1.getDate());
echo("QueueSample.Head = " + queue1.getHead());
echo("QueueSample.Size = " + queue1.getSize());
echo("\nInvoke clearQueue() in QueueSampler MXBean...");
mxbeanProxy.clearQueue();

QueueSample queue2 = mxbeanProxy.getQueueSample();
echo("\nQueueSample.Date = " +  queue2.getDate());
echo("QueueSample.Head = " + queue2.getHead());
echo("QueueSample.Size = " + queue2.getSize());

...

```

如上所示，要为MXBean创建代理，您所要做的就是调用`JMX.newMXBeanProxy`而不是`newMBeanProxy`。MXBean代理`mxbeanProxy`允许客户端调用`QueueSample` MXBean的操作，就好像它们是本地注册的MXBean的操作一样。

**关闭连接**

一旦JMX客户端获得了所需的所有信息并在远程JMX代理的MBean服务器上的MBean上执行了所有必需的操作，就必须关闭连接。

```
jmxc.close();
```

通过调用 [`JMXConnector.close`](https://docs.oracle.com/javase/8/docs/api/javax/management/remote/JMXConnector.html#close--) 方法关闭连接。

**运行自定义 JMX Client 示例**

This example requires version 6 of the Java SE platform. To monitor the `Main` JMX agent remotely using a custom JMX client [`Client`](https://docs.oracle.com/javase/tutorial/jmx/examples/Client.java), follow these steps:

1. 如果尚未执行此操作，请将`jmx_examples.zip`保存到`work_dir`目录中。

2. 在终端窗口中使用以下命令解压缩示例类包。

   ```
   unzip jmx_examples.zip
   ```

3. 编译`work_dir`目录中的示例Java类。

   ```
   javac com/example/*.java
   ```

4. 启动`Main`应用程序，指定公开`Main`以进行远程管理的属性：

   ```
   java -Dcom.sun.management.jmxremote.port=9999 \
        -Dcom.sun.management.jmxremote.authenticate=false \
        -Dcom.sun.management.jmxremote.ssl=false \ 
        com.example.Main
   ```

   生成`Main`正在等待某事发生的确认。

5. 在另一个终端窗口中启动`Client`应用程序：

   ```
   java com.example.Client
   ```

   显示已获取`MBeanServerConnection`的确认。

6. 按Enter键。

   显示由`Main`启动的MBean服务器中注册的所有MBean的域。

7. 再次按Enter键。

   将显示MBean服务器中注册的MBean数，以及所有这些MBean的对象名。显示的MBean包括在Java VM中运行的所有标准平台MXBeans，以及由`Main`在MBean服务器中注册的`Hello` MBean和`QueueSampler` MXBean。

8. 再次按Enter键。

   `Hello` MBeans 的操作由`Client`调用，结果如下：

    - 向`Client`添加通知侦听器以侦听来自`Main`的通知。
    - `CacheSize`属性的值从`200`更改为`150`。
    - 在启动`Main`的终端窗口中，显示`CacheSize`属性更改的确认。
    - 在启动`Client`的终端窗口中，显示`Main`的通知，通知`Client` `ClientSize`属性更改。
    - 调用`Hello` MBean的`sayHello`操作。
    - 在您启动`Main`的终端窗口中，显示消息“Hello world”。
    - 调用`Hello` MBean的`add`操作，值为`2`和`3`作为参数。结果由`Client`显示。

9. 再次按Enter键。

   客户端调用`QueueSampler` MXBean的操作，结果如下：

    - 显示`QueueSample`值`date`，`head`和`size`。
    - 调用`clearQueue`操作。

10. 再次按Enter键。

    `Client` 关闭与MBean服务器的连接，并显示确认。

