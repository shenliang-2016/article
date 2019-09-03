### MXBeans

本节介绍一种特殊类型的MBean，称为MXBeans。

MXBean是一种MBean，仅引用一组预定义的数据类型。通过这种方式，您可以确保任何客户端（包括远程客户端）都可以使用您的MBean，而无需客户端访问表示MBean类型的特定于模型的类。MXBeans提供了将相关值捆绑在一起的便捷方式，而无需特别配置客户端来处理捆绑包。

与标准MBean的方式相同，MXBean是通过编写名为`SomethingMXBean`的Java接口和实现该接口的Java类来定义的。但是，与标准MBean不同，MXBeans不需要将Java类称为`Something`。接口中的每个方法都定义MXBean中的属性或操作。注解`@MXBean`也可用于修饰Java接口，而不是要求接口的名称后跟MXBean后缀。

MXBeans存在于Java 2平台标准版（J2SE）5.0软件的`java.lang.management`包中。但是，除了`java.lang.management`中定义的标准集之外，用户现在还可以定义自己的MXBean。

MXBeans背后的主要思想是MXBean接口中引用的`java.lang.management.MemoryUsage`等类型，在本例中为`java.lang.management.MemoryMXBean`，它们被映射到一组标准类型，即包`javax.management.openmbean`中定义的*Open类型*。确切的映射规则出现在MXBean规范中。但是，一般原则是简单类型（如`int`或`String`）保持不变，而复杂类型（如`MemoryUsage`）则映射到标准类型`CompositeDataSupport`。

MXBean示例包含以下文件，这些文件位于`jmx_examples.zip`中：

 -  `QueueSamplerMXBean`接口
 -  实现MXBean接口的`QueueSampler`类
 -  由MXBean接口中的`getQueueSample()`方法返回的`QueueSample` Java类型
 -  `Main`，设置和运行示例的程序

MXBean示例使用这些类来执行以下操作：

 - 定义管理`Queue<String>`类型资源的简单MXBean
 - 在MXBean中声明一个`getter`，`getQueueSample`，它在调用时获取队列的快照，并返回一个Java类`QueueSample`，它将以下值捆绑在一起：
       - 拍摄快照的时间
       - 队列大小
       - 在给定时间排队的队长
 - 在MBean服务器中注册MXBean

**MXBean 接口**

下面的代码展示了示例 [`QueueSamplerMXBean`](https://docs.oracle.com/javase/tutorial/jmx/examples/QueueSamplerMXBean.java) MXBean 接口：

```java
package com.example; 
 
public interface QueueSamplerMXBean { 
    public QueueSample getQueueSample(); 
    public void clearQueue(); 
} 
```

请注意，您声明MXBean接口的方式与声明标准MBean接口的方式完全相同。`QueueSamplerMXBean`接口声明了一个`getter`，`getQueueSample`和一个`clearQueue`操作。

**定义 MXBean 操作**

MXBean操作在`QueueSampler`示例类中声明，如下所示：

```java
package com.example; 
 
import java.util.Date; 
import java.util.Queue; 
 
public class QueueSampler 
                implements QueueSamplerMXBean { 
     
    private Queue<String> queue; 
         
    public QueueSampler (Queue<String> queue) { 
        this.queue = queue; 
    } 
         
    public QueueSample getQueueSample() { 
        synchronized (queue) { 
            return new QueueSample(new Date(), 
                           queue.size(), queue.peek()); 
        } 
    } 
         
    public void clearQueue() { 
        synchronized (queue) { 
            queue.clear(); 
        } 
    } 
} 
```

`QueueSampler`定义MXBean接口声明的`getQueueSample()` `getter`和`clearQueue()`操作。 `getQueueSample()`操作返回`QueueSample` Java类型的实例，该实例是使用`java.util.Queue`方法`peek()`和`size()`返回的值以及`java.util.Date`的实例创建的。

**定义MXBean接口返回的Java类型**

`QueueSampler`返回的`QueueSample`实例在`QueueSample`类中定义，如下所示：

```java
package com.example; 
 
import java.beans.ConstructorProperties; 
import java.util.Date; 
 
public class QueueSample { 
     
    private final Date date; 
    private final int size; 
    private final String head; 
         
    @ConstructorProperties({"date", "size", "head"}) 
    public QueueSample(Date date, int size, 
                        String head) { 
        this.date = date; 
        this.size = size; 
        this.head = head; 
    } 
         
    public Date getDate() { 
        return date; 
    } 
         
    public int getSize() { 
        return size; 
    } 
         
    public String getHead() { 
        return head; 
    } 
}   
```

在`QueueSample`类中，MXBean框架调用`QueueSample`中的所有`getter`以将给定实例转换为`CompositeData`实例，并使用`@ConstructorProperties`注解从`CompositeData`实例重建`QueueSample`实例。

**在MBean Server中创建和注册MXBean**

到目前为止，已经定义了以下内容：MXBean接口和实现它的类，以及返回的Java类型。接下来，必须在MBean服务器中创建并注册MXBean。这些`Main`示例JMX代理执行的操作与标准MBean示例中使用的相同，但相关代码未显示在 [Standard MBean](https://docs.oracle.com/javase/tutorial/jmx/mbeans/standard.html) 课程中。

```java
package com.example; 
 
import java.lang.management.ManagementFactory; 
import java.util.Queue; 
import java.util.concurrent.ArrayBlockingQueue; 
import javax.management.MBeanServer; 
import javax.management.ObjectName; 
 
public class Main { 
 
    public static void main(String[] args) throws Exception { 
        MBeanServer mbs = 
            ManagementFactory.getPlatformMBeanServer(); 
                
        ...  
        ObjectName mxbeanName = new ObjectName("com.example:type=QueueSampler");
        
        Queue<String> queue = new ArrayBlockingQueue<String>(10);
        queue.add("Request-1");
        queue.add("Request-2");
        queue.add("Request-3");
        QueueSampler mxbean = new QueueSampler(queue);
        
        mbs.registerMBean(mxbean, mxbeanName);
                 
        System.out.println("Waiting..."); 
        Thread.sleep(Long.MAX_VALUE); 
    } 
} 
```

`Main`类执行以下操作：

 - 获取平台MBean服务器。
 - 为MXBean `QueueSampler`创建对象名称。
 - 为要处理的`QueueSampler` MXBean创建`Queue`实例。
 - 将`Queue`实例提供给新创建的`QueueSampler` MXBean。
 - 以与标准MBean完全相同的方式在MBean服务器中注册MXBean。

**运行 MXBean 示例**

MXBean示例使用您在标准MBeans部分中使用的`jmx_examples.zip`包中的类。此示例需要Java SE平台的第6版。 要运行MXBeans示例，请执行以下步骤：

1. 如果尚未执行此操作，请将`jmx_examples.zip`保存到`work_dir`目录中。

2. 在终端窗口中使用以下命令解压缩示例类包。

   ```
   unzip jmx_examples.zip
   ```

3. 编译`work_dir`目录中的示例Java类。

   ```
   javac com/example/*.java
   ```

4. 启动主应用程序。生成`Main`正在等待某事发生的确认。

   ```
   java com.example.Main
   ```

5. 在同一台计算机上的另一个终端窗口中启动JConsole。 将显示“新建连接”对话框，其中列出了可以连接的正在运行的JMX代理的列表。

   ```
   jconsole
   ```

6. 在“新建连接”对话框中，从列表中选择`com.example.Main`，然后单击“连接”。

   将显示平台当前活动的摘要。

7. 单击MBeans选项卡。

   此面板显示当前在MBean服务器中注册的所有MBean。

8. 在左侧框架中，展开MBean树中的`com.example`节点。

   您将看到`Main`创建并注册的示例MBean `QueueSampler`。如果单击`QueueSampler`，则会在MBean树中看到其关联的`Attributes`和`Operations`节点。

9. 展开“属性”节点。

   您会看到`QueueSample`属性出现在右窗格中，其值为`javax.management.openmbean.CompositeDataSupport`。

10. 双击`CompositeDataSupport`值。

    您会看到`QueueSample`值的日期，头部和大小，因为MXBean框架已将`QueueSample`实例转换为`CompositeData`。如果您已将`QueueSampler`定义为标准MBean而不是MXBean，则JConsole将找不到`QueueSample`类，因为它不在其类路径中。如果`QueueSampler`是标准MBean，则在检索`QueueSample`属性值时会收到`ClassNotFoundException`消息。JConsole发现`QueueSampler`的事实证明了在通过JConsole等通用JMX客户端连接到JMX代理时使用MXBeans的有用性。

11. 展开“操作”节点。

    将显示一个用于调用`clearQueue`操作的按钮。

12. 单击`clearQueue`按钮。

    显示已成功调用该方法的确认。

13. 再次展开`Attributes`节点，然后双击`CompositeDataSupport`值。

    头部和大小值已重置。

14. 要关闭JConsole，请选择Connection  -> Exit。

