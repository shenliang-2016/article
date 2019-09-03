## 远程管理

JMX API使您可以使用基于JMX技术的连接器（JMX连接器）执行资源的远程管理。JMX连接器使远程基于Java技术的客户端可以访问MBean服务器。连接器的客户端导出与MBean服务器基本相同的接口。

JMX连接器由连接器客户端和连接器服务器组成。连接器服务器连接到MBean服务器并侦听来自客户端的连接请求。连接器客户端负责与连接器服务器建立连接。连接器客户端通常位于与连接器服务器不同的Java虚拟机（Java VM）中，并且通常在不同的计算机上运行。JMX API定义了基于远程方法调用（RMI）的标准连接协议。此协议使您可以从远程位置将JMX客户端连接到MBean服务器中的MBean，并对MBean执行操作，就像操作是在本地执行一样。

Java SE平台提供了一种开箱即用的方法，可以使用JMX API的标准RMI连接器远程监控应用程序。开箱即用的RMI连接器自动公开应用程序以进行远程管理，而无需您自己创建专用的远程连接器服务器。通过使用正确的属性启动Java应用程序来激活开箱即用的远程管理代理。然后，与JMX技术兼容的监控和管理应用程序可以连接到这些应用程序并远程监控它们。

### 通过 JConsole 公开资源以进行远程管理

如果使用现成的远程管理代理和现有的监视和管理工具（如JConsole），则使用JMX API公开Java应用程序以进行远程管理非常简单。

要公开远程管理应用程序，需要使用正确的属性启动它。此示例显示如何公开 [`Main`](https://docs.oracle.com/javase/tutorial/jmx/examples/Main.java)  JMX代理以进行远程管理。

------

安全考虑：

为简单起见，在此示例中禁用了身份验证和加密安全机制。 但是，在实际环境中实现远程管理时，应实现这些安全机制。[What Next?](https://docs.oracle.com/javase/tutorial/jmx/end.html)  提供指向其他JMX技术文档的指针，其中显示了如何激活安全机制。

------

此示例需要Java SE平台的第6版。 要远程监视`Main` JMX代理，请按照下列步骤操作：

1. 如果尚未执行此操作，请将`jmx_examples.zip`保存到`work_dir`目录中。

2. 在终端窗口中使用以下命令解压缩示例类包。

   ```
   unzip jmx_examples.zip
   ```

3. 编译`work_dir`目录中的示例Java类。

   ```
   javac com/example/*.java
   ```

4. 启动`Main`应用程序，指定公开`Main`以进行远程管理的属性。（对于Windows，使用`^`而不是反斜杠`\`将长命令拆分为多行）：

   ```
   java -Dcom.sun.management.jmxremote.port=9999 \
        -Dcom.sun.management.jmxremote.authenticate=false \
        -Dcom.sun.management.jmxremote.ssl=false \
        com.example.Main
   ```

   生成`Main`正在等待某事发生的确认。

5. 在另一台机器上的另一个终端窗口中启动JConsole：

   ```
   jconsole
   ```

   将显示“新建连接”对话框，其中列出了可以在本地连接的正在运行的JMX代理。

6. 选择“远程进程”，然后在“远程进程”字段中键入以下内容：

   ```
   hostname:9999
   ```

   在此地址中，`hostname`是运行`Main`应用程序的远程计算机的名称，`9999`是开箱即用的JMX连接器将连接的端口号。

7. 单击连接。

   显示`Main`正在运行与其中的Java虚拟机（Java VM）的当前活动的摘要。

8. 单击MBeans选项卡。

   此面板显示当前在远程MBean服务器中注册的所有MBean。

9. 在左侧框架中，展开MBean树中的`com.example`节点。

   您会看到`Main`创建并注册的示例MBean `Hello`。如果单击`Hello`，则会在MBean树中看到其关联的`Attributes`和`Operations`节点，即使它在另一台计算机上运行。

10. 要关闭JConsole，请选择Connection  -> Exit。

