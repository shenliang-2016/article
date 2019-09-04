# Java命名和目录接口

此课程描述了JNDI™（Java命名和目录接口），用于访问目录和命名服务的API。在这里，您将了解基本的命名和目录服务，以及如何使用JNDI编写简单的应用程序来使用这些服务。最流行的目录服务LDAP用于说明使用JNDI来访问目录服务。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**命名和目录概念**](https://docs.oracle.com/javase/tutorial/jndi/concepts/index.html) 从此处开始，了解命名和目录概念的概述。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**JNDI概述**](https://docs.oracle.com/javase/tutorial/jndi/overview/index.html) 为您提供JNDI及其架构和包装的概述。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**软件设置**](https://docs.oracle.com/javase/tutorial/jndi/software/index.html) 描述设置运行此课程中描述的示例以及任何其他JNDI应用程序所需的环境所涉及的说明和步骤。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**命名和目录操作**](https://docs.oracle.com/javase/tutorial/jndi/ops/index.html) 描述各种命名和目录操作，并通过大量使用JNDI访问命名/目录服务的示例来演示它们。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**LDAP用户的高级主题**](https://docs.oracle.com/javase/tutorial/jndi/ldap/index.html) LDAP用户的专业课程。它讨论了如何将JNDI建模为LDAP API，如何在生产环境中执行LDAP身份验证，SSL和管理连接。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**访问目录中的对象**](https://docs.oracle.com/javase/tutorial/jndi/objects/index.html) 显示如何将应用程序与目录集成，以便可以在目录中存储和检索Java对象。

[![图像表示子弹](https://docs.oracle.com/javase/tutorial/images/networkingIcon.gif)**JDK 5.0和JDK 6中的功能介绍**](https://docs.oracle.com/javase/tutorial/jndi/newstuff/index.html) **JDK 5.0和JDK 6**中可用的JNDI和LDAP服务提供程序中的功能。

------

**注意：**本教程的基础是位于 <https://docs.oracle.com/javase/jndi/tutorial/> 的独立JNDI教程。最后在Java 2 SDK标准版v 1.4.2下更新的独立JNDI教程提供了有关JNDI的全面内容，但不再受支持。本教程摘录了standlone教程的基础知识，并包含Java平台标准版5.0和6版本中添加到JNDI的功能。

旧的JNDI教程在 [docs.oracle.com](https://docs.oracle.com/javase/jndi/tutorial/) 上保存为存档。

## 名称和目录概念

**命名概念**

任何计算机系统中的一个基础设施就是所谓的*命名服务*——将名称关联到对象，因而对象可以基于它们的名称被找到。在使用任何计算机程序或者系统时，你始终都会不断命名一个又一个对象。比如，当你使用一个电子邮件系统时，你必须提供收件人姓名。围殴了访问计算机中的文件，你必须提供文件名。命名服务允许你通过名称来查询对象。

![A name is used to reference an object.](https://docs.oracle.com/javase/tutorial/figures/jndi/naming-system.gif)

命名服务的最主要功能就是将人类友好的名称映射到对象，比如一个地址、标识符、或者计算机程序使用的对象。

比如，[Internet Domain Name System (DNS)](http://www.ietf.org/rfc/rfc1034.txt) 将机器名称映射到 IP 地址：

```
www.example.com ==> 192.0.2.5
```

文件系统将文件名映射到文件引用，程序可以使用文件名访问该文件的内容。

```
c:\bin\autoexec.bat ==> File Reference
```

这两个例子也展示了存在命名服务的广泛范围——从命名Internet上的对象到命名本地文件系统上的文件。

**名称**

为了在命名系统中查找对象，你给出对象的名称。命名系统决定了名称必须遵循的语法规则。该语法有时候被称为时命名系统的*命名约定*。一个名称有若干组成部分。名称的表示由标记名称组件的组件分隔符组成。

| Naming System    | Component Separator | Names                       |
| ---------------- | ------------------- | --------------------------- |
| UNIX file system | "/"                 | /usr/hello                  |
| DNS              | "."                 | sales.Wiz.COM               |
| LDAP             | "," and "="         | cn=Rosanna Lee, o=Sun, c=US |

UNIX文件系统的命名约定是文件是从其相对于文件系统根目录的路径命名的，路径中的每个组件都使用正斜杠字符（“/”）从左到右分隔。例如，UNIX路径名`/usr/hello`在文件目录`usr`中命名文件`hello`，该目录位于文件系统的根目录中。

DNS命名约定要求DNS名称中的组件从右到左排序，并由点字符（“.”）分隔。因此DNS名称`sales.Wiz.COM`命名一个名为`sales`的DNS条目，相对于DNS条目`Wiz.COM`。反过来，DNS条目`Wiz.COM`就是在`COM`条目中命名名为`Wiz`的条目。

[Lightweight Directory Access Protocol (LDAP)](http://www.ietf.org/rfc/rfc2251.txt) 命名约定名称组件顺序从右到左排列，使用逗号`,`分隔。因此 LDAP 名称`cn=Rosanna Lee, o=Sun, c=US`命名一个 LDAP 实体`cn=Rosanna Lee`，相对于实体`o=Sun`，反过来，相对于 `c=US`。LDAP 的另外一条命名规则就是每个名称组件必须是名/值对，其中名称和取值以等号`=`分隔。

**绑定**

名称与对象的关联被称为*绑定*。一个文件名被绑定到一个文件。

DNS 包含机器名称映射到 IP 地址的绑定。一个 LDAP 名称被绑定到一个 LDAP 实体。

**引用和地址**

依赖于命名服务，某些对象不能直接由命名服务存储，也就是说，对象的一份副本都能放在命名服务内部。相反，它们必须通过引用存储，也就是说，在命名服务中放置对象的*指针*或者*引用*。引用表达如何访问该对象的信息。典型地，它是一种紧凑的表示，可以被用于对象通信，对象本身可能包含更完整的状态信息。使用一弄，你可以联系对象并获取对象的更多信息。

例如，飞机对象可能包含飞机乘客和机组人员的列表，飞行计划，燃料和仪表状态，以及航班号和起飞时间。相比之下，飞机对象引用可能仅包含其航班号和起飞时间。该引用是关于飞机对象的信息的更紧凑的表示，并且可以用于获得附加信息。又例如，使用文件引用访问文件对象。又例如，打印机对象可能包含打印机的状态，例如其当前队列和纸盘中的纸张数量。另一方面，打印机对象引用可能仅包含有关如何到达打印机的信息，例如其打印服务器名称和打印协议。

尽管通常引用能够包含任意信息，将其内容视为*地址*（或者通信端点）还是有用的：也就是关于如何访问对象的特定信息。

为了简单，在不需要明确区分的情况下，本教程使用“对象”表示对象和对象引用。

**上下文**

*上下文*是名称—对象的绑定集合。每个上下文都有相应的命名约定。上下文始终会提供一个查找（解析）操作，该操作返回对象，典型地，它还提供诸如绑定名称、解绑名称、以及列出绑定名称等操作。上下文对象中的名称能够被绑定到另一个具有相同命名约定的上下文对象（称为*子上下文*）。

![Several examples of contexts, bound to subcontexts.](https://docs.oracle.com/javase/tutorial/figures/jndi/context.gif)

UNIX文件系统中的文件目录（例如`/usr`）表示上下文。相对于另一个文件目录命名的文件目录表示子上下文（UNIX用户将其称为子目录）。也就是说，在文件目录`/usr/bin`中，目录`bin`是`usr`的子上下文。DNS域（例如`COM`）表示上下文。相对于另一个DNS域命名的DNS域表示子上下文。对于DNS域`Sun.COM`，DNS域`Sun`是`COM`的子上下文。

最后，LDAP条目（例如`c=us`）表示上下文。相对于另一个LDAP条目命名的LDAP条目表示子上下文。对于LDAP条目`o=sun, c=us`，条目`o=sun`是`c=us`的子上下文。

**名称系统和命名空间**

*命名系统*是相同类型的相互连接的一组上下文（它们具有相同的命名约定）并提供一组通用操作。

实现DNS的系统是命名系统。使用LDAP进行通信的系统是命名系统。

命名系统为其客户提供*命名服务*，以执行与命名相关的操作。命名服务通过其自己的接口访问。DNS提供命名服务，将机器名称映射到IP地址。LDAP提供了一个命名服务，可将LDAP名称映射到LDAP条目。文件系统提供命名服务，将文件名映射到文件和目录。

命名空间是命名系统中所有可能名称的集合。UNIX文件系统具有一个名称空间，该名称空间由该文件系统中的所有文件和目录名称组成。DNS命名空间包含DNS域和条目的名称。LDAP名称空间包含LDAP条目的名称。

### 目录概念

很多命名服务都使用*目录服务*进行了扩展。目录服务将名称关联到对象，同时还将这些对象关联到一些*属性*。

目录服务 = 命名服务 + 对象包含的属性。

你不仅可以通过名称查找对象，还可以获得对象的属性，或者基于属性搜索对象。

![Diagram showing a directory system: a name references a directory object which contains attributes.](https://docs.oracle.com/javase/tutorial/figures/jndi/directory-system.gif)

一个例子是电话公司的目录服务。它将用户的姓名映射到他的地址和电话号码。计算机的目录服务非常类似于电话公司的目录服务，因为它们都可用于存储诸如电话号码和地址之类的信息。然而，计算机的目录服务功能更强大，因为它可以在线获得，并且可以用于存储可供用户，程序甚至计算机本身和其他计算机使用的各种信息。

*目录对象*表示计算环境中的一个对象。目录对象可以被用于，诸如，表示打印机、人、计算机、或者一个网络。目录对象包含描述它所表示的对象的*属性*。

**属性**

目录对象可以具有属性。例如，打印机可能由目录对象表示，该目录对象具有其速度，分辨率和颜色作为属性。用户可能由目录对象表示，该目录对象具有用户的电子邮件地址，各种电话号码，邮政地址和计算机帐户信息作为属性。

属性具有属性标识符和一组属性值。属性标识符是标识独立于其值的属性的标记。例如，两个不同的计算机帐户可能具有`"mail"`属性；`"mail"`是属性标识符。属性值是属性的内容。例如，电子邮件地址可能包含：

```
Attribute Identifier : Attribute Value
                 mail   john.smith@example.com
```

**目录和目录服务**

*目录*是一组相互连接的目录对象。目录服务是一种服务，它提供用于创建，添加，删除和修改与目录中的对象关联的属性的操作。该服务通过自己的接口访问。

存在许多目录服务的例子。

 - 网络信息服务（NIS）
      NIS是UNIX操作系统上可用的目录服务，用于存储与系统相关的信息，例如与机器，网络，打印机和用户相关的信息。
 - [Oracle Directory Server](http://www.oracle.com/technetwork/testcontent/index-085178.html)
      Oracle Directory Server是基于Internet标准LDAP的通用目录服务。

**搜索服务**

您可以通过将目录对象的名称提供给目录服务来查找目录对象。或者，许多目录（例如基于LDAP的目录）支持搜索的概念。搜索时，不能提供名称，而是提供由逻辑表达式组成的查询，在该表达式中指定一个或多个对象必须具有的属性。该查询称为搜索过滤器。这种搜索方式有时称为反向查找或基于内容的搜索。目录服务搜索并返回满足搜索过滤器的对象。

例如，您可以查询目录服务以查找：

 - 属性`"age"`超过 40 的所有用户。
 - 所有 IP 地址以`"192.113.50"`开头的机器。

**组合命名和目录服务**

目录通常将其对象排列在层次结构中。例如，LDAP将所有目录对象排列在树中，称为*目录信息树（DIT）*。例如，在DIT中，组织对象可能既包含人员对象又包含组对象。当以这种方式排列目录对象时，除了属性容器之外，它们还起到命名上下文的作用。

