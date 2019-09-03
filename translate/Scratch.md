## MBeans 介绍

本课程介绍了JMX API的基本概念，即托管bean或MBean。

MBean是一个托管Java对象，类似于JavaBeans组件，它遵循JMX规范中提出的设计模式。MBean可以表示设备，应用程序或需要管理的任何资源。MBean公开了一个由以下内容组成的管理界面：

 - 一组可读或可写属性，或两者兼而有之。
 - 一组可调用的操作。
 - 自我描述。

管理接口在MBean实例的整个生命周期中不会更改。MBean还可以在发生某些预定义事件时发出通知。

JMX规范定义了五种类型的MBean：

 - 标准MBean
 - 动态MBean
 - 打开MBean
 - 模型MBean
 - MXBeans

此课程中的示例仅演示了最简单的MBean类型，即标准MBean和MXBeans。

### 标准 MBeans

This section presents an example of a straightforward, standard MBean.

A standard MBean is defined by writing a Java interface called `SomethingMBean` and a Java class called `Something` that implements that interface. Every method in the interface defines either an attribute or an operation in the MBean. By default, every method defines an operation. Attributes and operations are methods that follow certain design patterns. A standard MBean is composed of an MBean interface and a class. The MBean interface lists the methods for all exposed attributes and operations. The class implements this interface and provides the functionality of the instrumented resource.

The following sections examine an example of a standard MBean and a simple JMX technology-enabled agent (JMX agent) that manages the MBean.

**MBean 接口**

基本 MBean 接口的例子 [`HelloMBean`](https://docs.oracle.com/javase/tutorial/jmx/examples/HelloMBean.java) ：

```java
package com.example; 
 
public interface HelloMBean { 
 
    public void sayHello(); 
    public int add(int x, int y); 
    
    public String getName(); 
     
    public int getCacheSize(); 
    public void setCacheSize(int size); 
} 
```

按照惯例，MBean接口采用实现它的Java类的名称，并添加后缀MBean。在上面例子这种情况下，接口称为`HelloMBean`。实现此接口的`Hello`类将在下一节中介绍。

根据JMX规范，除了可由MBean管理的应用程序调用的命名和类型操作之外，MBean接口还包含可读且可写的命名和类型属性。`HelloMBean`接口声明了两个操作：Java方法`add()`和`sayHello()`。

`HelloMBean`声明了两个属性：`Name`是只读字符串，`CacheSize`是一个可以读写的整数。声明了`getter`和`setter`方法，以允许托管应用程序访问并可能更改属性值。根据JMX规范的定义，`getter`是任何不返回`void`且名称以`get`开头的公共方法。`getter`使管理器能够读取属性的值，该属性的类型是返回对象的类型。`setter`是任何公共方法，它接受一个参数，其名称以`set`开头。`setter`使管理器能够在属性中写入一个新值，其类型与参数的类型相同。

以下部分显示了这些操作和属性的实现。

**MBean 实现**

下面的 [`Hello`](https://docs.oracle.com/javase/tutorial/jmx/examples/Hello.java) Java 类实现了 `HelloMBean` MBean 接口：

```java
package com.example; 
 
public class Hello ... 
    implements HelloMBean { 
    public void sayHello() { 
        System.out.println("hello, world"); 
    } 
     
    public int add(int x, int y) { 
        return x + y; 
    } 
     
    public String getName() { 
        return this.name; 
    }  
     
    public int getCacheSize() { 
        return this.cacheSize; 
    } 
     
    public synchronized void setCacheSize(int size) {
        ...
    
        this.cacheSize = size; 
        System.out.println("Cache size now " + this.cacheSize); 
    } 
    ...
     
    private final String name = "Reginald"; 
    private int cacheSize = DEFAULT_CACHE_SIZE; 
    private static final int 
        DEFAULT_CACHE_SIZE = 200; 
}
```

`Hello`类直截了当地提供了`HelloMBean`声明的操作和属性的定义。`sayHello()`和`add()`操作非常简单，但实际操作可以根据需要简单或复杂。

该类还定义了获取`Name`属性以及获取和设置`CacheSize`属性的方法。在此示例中，`Name`属性值永远不会更改。但是，在实际情况中，此属性可能会随托管资源的运行而更改。例如，该属性可能表示正常运行时间或内存使用情况等统计信息。这里，该属性仅仅是`Reginald`的名称。

调用`setCacheSize`方法使您可以从其声明的默认值`200`更改`CacheSize`属性。在实际方案中，更改`CacheSize`属性可能需要执行其他操作，例如丢弃条目或分配新条目。此示例仅打印一条消息以确认缓存大小已更改。但是，可以定义更复杂的操作，而不是简单调用`println()`。

使用`Hello` MBean及其定义的接口，它们现在可用于管理它们所代表的资源，如以下部分所示。

**创建 JMX 代理用以管理资源**

一旦资源由MBean检测，该资源的管理由JMX代理执行。

JMX代理的核心组件是MBean服务器。MBean服务器是注册MBean的托管对象服务器。JMX代理还包括一组用于管理MBean的服务。有关MBean服务器实现的详细信息，请参阅  [`MBeanServer`](https://docs.oracle.com/javase/8/docs/api/javax/management/MBeanServer.html) 接口的API文档。

后面的`Main`类表示基本的JMX代理：

```java
package com.example; 
 
import java.lang.management.*; 
import javax.management.*; 
 
public class Main { 
 
    public static void main(String[] args) 
        throws Exception { 
     
        MBeanServer mbs = ManagementFactory.getPlatformMBeanServer(); 
        ObjectName name = new ObjectName("com.example:type=Hello"); 
        Hello mbean = new Hello(); 
        mbs.registerMBean(mbean, name); 
          
        ...
     
        System.out.println("Waiting forever..."); 
        Thread.sleep(Long.MAX_VALUE); 
    } 
} 
```

JMX代理`Main`首先通过调用`java.lang.management.ManagementFactory`类的`getPlatformMBeanServer()`方法获取由平台创建和初始化的MBean服务器。如果平台尚未创建MBean服务器，则`getPlatformMBeanServer()`通过调用JMX方法`MBeanServerFactory.createMBeanServer()`自动创建MBean服务器。`Main`获取的`MBeanServer`实例名为`mbs`。

接下来，`Main`定义它将创建的MBean实例的对象名称。每个JMX MBean都必须具有对象名称。对象名称是JMX类`ObjectName`的实例，必须符合JMX规范定义的语法。即，对象名称必须包含域和键属性列表。在`Main`定义的对象名称中，域是`com.example`（包含示例MBean的包）。此外，key-property声明此对象的类型为`Hello`。

创建名为`mbean`的`Hello`对象的实例。然后，通过将对象和对象名称传递给对JMX方法`MBeanServer.registerMBean()`的调用，将名为`mbean`的`Hello`对象注册为MBean服务器`mbs`中具有对象名称的MBean。

在MBean服务器中注册了`Hello` MBean后，`Main`只是等待对`Hello`执行管理操作。在此示例中，这些管理操作正在调用`sayHello()`和`add()`，以及获取和设置属性值。

**运行该标准 MBean 示例**

在检查了示例类之后，您现在可以运行该示例。在此示例中，JConsole用于与MBean交互。

若要运行该示例，请按照下列步骤操作：

1. 将JMX API示例类包`jmx_examples.zip`保存到您的工作目录`work_dir`。

2. 在终端窗口中使用以下命令解压缩示例类包。

   ```
   unzip jmx_examples.zip
   ```

3. 编译`work_dir`目录中的示例Java类。

   ```
   javac com/example/*.java
   ```

4. 如果您运行的是Java Development Kit（JDK）版本6，请使用以下命令启动Main应用程序。

   ```
   java com.example.Main
   ```

   如果您运行的是早于版本6的JDK版本，则需要使用指定的以下选项启动Main应用程序，以公开应用程序以进行监视和管理。

   ```
   java -Dcom.sun.management.jmxremote example.Main
   ```

   显示`Main`正在等待某事发生的确认。

5. 在同一台计算机上的另一个终端窗口中启动JConsole。

   ```
   jconsole
   ```

   将显示“新建连接”对话框，其中列出了可以连接的正在运行的JMX代理的列表。

6. 在“新建连接”对话框中，从列表中选择`com.example.Main`，然后单击“连接”。

   将显示平台当前活动的摘要。

7. 单击MBeans选项卡。

   此面板显示当前在MBean服务器中注册的所有MBean。

8. 在左侧框架中，展开MBean树中的`com.example`节点。

   您会看到Main创建并注册的示例MBean `Hello`。如果单击`Hello`，则会在MBean树中看到其关联的`Attributes`和`Operations`节点。

9. 展开MBean树中的`Hello` MBean的`Attributes`节点。

   显示由`Hello`类定义的MBean属性。

10. 将`CacheSize`属性的值更改为150。

    在您启动`Main`的终端窗口中，将生成此属性更改的确认。

11. 展开MBean树中的`Hello` MBean的`Operations`节点。

    `Hello` MBean声明的两个操作，`sayHello()`和`add()`是可见的。

12. 单击`sayHello`按钮调用`sayHello()`操作。

    JConsole对话框通知您已成功调用该方法。消息“hello，world”在`Main`运行的终端窗口中生成。

13. 为`add()`操作提供两个整数以添加并单击“添加”按钮。

    答案显示在JConsole对话框中。

14. 要关闭JConsole，请选择Connection  -> Exit。

