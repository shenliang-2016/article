# Java 管理扩展(JMX)

 **Java Management Extensions (JMX)** 课程提供了有关 JMX 技术的介绍。该技术包含在 Java 平台标准版中。本课程中的例子展示了如何使用 JMX 中最重要的特性。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)JMX 技术概述](https://docs.oracle.com/javase/tutorial/jmx/overview/index.html) 简要介绍了 JMX 技术，包括它的目标和主要特性。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)MBeans 介绍](https://docs.oracle.com/javase/tutorial/jmx/mbeans/index.html) 介绍 JMX 技术的基础概念，*管理 beans*，也被称为**MBeans**。本课程也将介绍MXBeans。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)通知](https://docs.oracle.com/javase/tutorial/jmx/notifs/index.html) 介绍 JMX 技术中的通知机制。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)远程管理](https://docs.oracle.com/javase/tutorial/jmx/remote/index.html) 展示如何实现 JMX API 的管理能力并创建一个 JMX 客户端应用。

[![trail icon](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)延伸学习](https://docs.oracle.com/javase/tutorial/jmx/end.html) 介绍有关 JMX 技术的更进一步的资料。

## JMX 技术概述

Java Management Extensions（JMX）技术是Java平台标准版（Java SE平台）的标准部分。JMX技术已添加到Java 2平台标准版（J2SE）5.0版本的平台中。

JMX技术提供了一种简单，标准的方式来管理应用程序，设备和服务等资源。由于JMX技术是动态的，因此您可以使用它来监视和管理资源的创建，安装和实施。您还可以使用JMX技术来监视和管理Java虚拟机（Java VM）。

JMX规范定义了Java编程语言中的体系结构，设计模式，API和服务，用于管理和监视应用程序和网络。

使用JMX技术，给定资源由一个或多个Java对象（称为 Managed Beans 或 MBeans）进行检测。这些 MBeans 在核心管理的对象服务器中注册，称为 MBean 服务器。MBean 服务器充当管理代理程序，可以在大多数已为Java编程语言启用的设备上运行。

规范定义了用于管理已正确配置以进行管理的任何资源的JMX代理。JMX代理由MBean服务器和一组用于处理MBean的服务组成，MBean服务器在其中注册MBean。通过这种方式，JMX代理可以直接控制资源并使其可用于远程管理应用程序。

检测资源的方式完全独立于管理基础结构。因此，无论管理应用程序如何实现，都可以使资源易于管理。

JMX技术定义了标准连接器（称为JMX连接器），使您可以从远程管理应用程序访问JMX代理。使用不同协议的JMX连接器提供相同的管理接口。因此，无论使用何种通信协议，管理应用程序都可以透明地管理资源。只要这些系统或应用程序支持JMX代理，JMX代理也可以由不符合JMX规范的系统或应用程序使用。

### 为什么要使用 JMX 技术？

JMX技术为开发人员提供了一种灵活的方法来检测基于Java技术的应用程序（Java应用程序），创建智能代理，实现分布式管理中间件和管理器，并将这些解决方案顺利集成到现有的管理和监视系统中。

* JMX技术使Java应用程序无需大量投资即可进行管理。
  基于JMX技术的代理（JMX代理）可以在大多数支持Java技术的设备上运行。因此，Java应用程序可以变得易于管理，而对其设计几乎没有影响。Java应用程序只需要嵌入一个托管对象服务器，并使其某些功能可用作在对象服务器中注册的一个或多个托管bean（MBean）。这就是从管理基础设施中受益所需的一切。
* JMX技术提供了管理Java应用程序，系统和网络的标准方法。
  例如，Java平台企业版（Java EE）5 Application Server符合JMX体系结构，因此可以使用JMX技术进行管理。
* JMX技术可用于Java VM的开箱即用管理。
  Java虚拟机（Java VM）使用JMX技术进行了高度定制化。您可以启动JMX代理以访问内置Java VM检测，从而远程监视和管理Java VM。
* JMX技术提供可扩展的动态管理架构。
  每个JMX代理服务都是一个独立的模块，可以根据需要插入管理代理程序。这种基于组件的方法意味着JMX解决方案可以从小型设备扩展到大型电信交换机等。 JMX规范提供了一组核心代理服务。可以在管理基础架构中开发和动态加载，卸载或更新其他服务。
* JMX技术利用现有的标准Java技术。
  只要需要，JMX规范就会引用现有的Java规范，例如Java命名和目录接口（J.N.D.I.）API。
* 可以从NetBeans IDE模块创建基于JMX技术的应用程序（JMX应用程序）。
  您可以从NetBeans更新中心（在NetBeans界面中选择工具 - >更新中心）获取模块，该模块使您可以使用NetBeans IDE创建JMX应用程序。这降低了JMX应用程序的开发成本。
* JMX技术与现有管理解决方案和新兴技术相集成。
  JMX API是任何管理系统供应商都可以实现的开放接口。 JMX解决方案可以使用查找和发现服务以及Jini网络技术和服务定位协议（SLP）等协议。

### JMX 技术架构

JMX 技术可以分为三个层次如下：

- 插桩
- JMX 代理
- 远程管理

**插桩**

要使用JMX技术管理资源，必须首先使用Java编程语言检测资源。您使用称为*MBeans*的Java对象来实现对资源插桩的访问。MBean必须遵循JMX规范中定义的设计模式和接口。这样做可确保所有MBean以标准化方式提供托管资源工具。除了标准MBean之外，JMX规范还定义了一种称为*MXBean*的特殊类型的MBean。MXBean是仅引用预定义数据类型集的MBean。存在其他类型的MBean，但本课程将集中在标准MBean和MXBeans上。

一旦资源由MBean插桩检测，就可以通过JMX代理进行管理。MBean不需要了解它们将运行的JMX代理。

MBean设计灵活，简单且易于实施。应用程序，系统和网络的开发人员可以以标准方式管理其产品，而无需了解或投资复杂的管理系统。可以用最少的努力使现有资源易于管理。

此外，JMX规范的检测层次提供了通知机制。此机制使MBean能够生成通知事件并将其传播到其他层次的组件。

**JMX 代理**

基于JMX技术的代理（JMX代理）是一种标准管理代理，可直接控制资源并使其可用于远程管理应用程序。JMX代理通常与它们控制的资源位于同一台机器上，但这种布置不是必需的。

JMX代理的核心组件是**MBean服务器**，这是一个在其中注册MBean的托管对象服务器。JMX代理还包括一组用于管理MBean的服务，以及至少一个允许管理应用程序访问的通信适配器或连接器。

实现JMX代理时，您不需要知道它将管理的资源的语义或功能。事实上，JMX代理甚至不需要知道它将服务哪些资源，因为任何符合JMX规范的资源都可以使用任何提供资源所需服务的JMX代理。同样，JMX代理不需要知道将访问它的管理应用程序的功能。

**远程管理**

可以通过许多不同方式访问JMX技术工具，可以通过现有管理协议（如简单网络管理协议 SNMP ）或通过专有协议进行访问。 MBean服务器依赖于协议适配器和连接器，以便从代理的Java虚拟机（Java VM）之外的管理应用程序访问JMX代理。

每个适配器都提供通过MBean服务器中注册的所有MBean的特定协议的视图。例如，HTML适配器可以在浏览器中显示MBean。

连接器提供管理器端接口，用于处理管理器和JMX代理之间的通信。每个连接器通过不同的协议提供相同的远程管理接口。当远程管理应用程序使用此接口时，无论协议如何，它都可以通过网络透明地连接到JMX代理。 JMX技术提供了一种标准解决方案，用于将JMX技术工具导出到基于Java远程方法调用（Java RMI）的远程应用程序。

### 虚拟机监控和管理

JMX技术还可用于监视和管理Java虚拟机（Java VM）。

Java VM具有内置检测功能，使您可以使用JMX技术监视和管理它。这些内置管理实用程序通常被称为Java VM的*开箱即用*管理工具。为了监视和管理Java VM的不同方面，Java VM包括一个平台MBean服务器和特殊的MXBeans，供符合JMX规范的管理应用程序使用。

**平台 MXBeans 和平台 MBean 服务**

*platform MXBeans*是一组MXBeans，随Java SE平台一起提供，用于监视和管理Java VM以及Java Runtime Environment（JRE）的其他组件。每个平台MXBean都封装了Java VM功能的一部分，例如类加载系统，即时（JIT）编译系统，垃圾收集器等。通过使用符合JMX规范的监视和管理工具，可以显示和交互这些MXBean，使您能够监视和管理这些不同的VM功能。一个这样的监视和管理工具是Java SE平台的 JConsole 图形用户界面。

Java SE平台提供标准的*平台MBean服务器*，其中注册了这些平台MXBean。平台MBean服务器还可以注册您要创建的任何其他MBean。

**JConsole**

Java SE平台包括 JConsole 监视和管理工具，该工具符合JMX规范。JConsole 使用Java VM的丰富工具（平台MXBeans）来提供有关Java平台上运行的应用程序的性能和资源消耗的信息。

**开箱即用的管理实践**

由于实现JMX技术的标准监视和管理实用程序内置于Java SE平台中，因此您可以在不必编写任何一行JMX API代码的情况下查看现成的JMX技术。您可以通过启动Java应用程序然后使用JConsole对其进行监视来实现。

**使用 JConsole 监控应用**

此过程说明如何监视Notepad Java应用程序。在版本6之前的Java SE平台版本下，需要使用以下选项启动要使用JConsole监视的应用程序。

```
-Dcom.sun.management.jmxremote
```

但是，随Java SE 6平台提供的JConsole版本可以附加到支持Attach API的任何本地应用程序。换句话说，JACsole会自动检测在Java SE 6 HotSpot VM中启动的任何应用程序，而不需要使用上述命令行选项启动。

1. 通过在终端窗口中使用以下命令启动Notepad Java应用程序：

   ```
   java -jar 
       jdk_home/demo/jfc/Notepad/Notepad.jar
   ```

   其中`jdk_home`是安装Java Development Kit（JDK）的目录。如果您没有运行Java SE平台的第6版，则需要使用以下命令：

   ```
   java -Dcom.sun.management.jmxremote -jar 
         jdk_home/demo/jfc/Notepad/Notepad.jar
   ```

2. 打开记事本后，在不同的终端窗口中，使用以下命令启动JConsole：

   ```
   jconsole
   ```

   将显示“新建连接”对话框。

3. 在“新建连接”对话框中，选择

   ```
   Notepad.jar
   ```

   从“本地进程”列表中，单击“连接”按钮。

   JConsole打开并将自身连接到`Notepad.jar`进程。当JConsole打开时，您将看到与记事本相关的监视和管理信息的概述。例如，您可以查看应用程序正在使用的堆内存量，应用程序当前运行的线程数以及应用程序消耗的中央处理单元（CPU）容量。

4. 单击不同的JConsole选项卡。

   每个选项卡都提供有关运行记事本的Java VM的不同功能区域的更多详细信息。所有提供的信息都是从该踪迹中提到的各种JMX技术MXBeans中获得的。所有平台MXBeans都可以显示在MBeans选项卡中。MBeans选项卡将在此跟踪的下一部分中进行检查。

5. 

6. 要关闭JConsole，请选择Connection  -> Exit。