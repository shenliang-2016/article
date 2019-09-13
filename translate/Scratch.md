### LDAP 设置

以下是构建访问 LDAP 目录服务器的 Java 应用程序所涉及的步骤。

1.安装 [Java Platform](https://docs.oracle.com/javase/tutorial/jndi/software/content.html) 软件。
2.获取 [之前](https://docs.oracle.com/javase/tutorial/jndi/software/index.html#SERVER) 中讨论的目录服务器软件。
3.使用所需的架构配置目录服务器。要使用本教程中的示例，需要在服务器上配置特殊的 [schema](https://docs.oracle.com/javase/tutorial/jndi/software/content.html#SCHEMA) 。
4.使用所需内容填充目录服务器。要使用本教程中的示例，需要在服务器上填充特殊的 [content](https://docs.oracle.com/javase/tutorial/jndi/software/content.html#LDIF) 。
5.编写 JNDI 应用程序以访问目录，编译并运目录服务器以获得所需的结果。 JNDI 示例将在 [下一课](https://docs.oracle.com/javase/tutorial/jndi/ops/index.html) 中介绍。

前两个步骤在上一节中介绍。本课程的其余部分将讨论步骤三和步骤四。涉及编写 JNDI 应用程序的步骤五将在下一课中介绍，该课程将介绍如何编写 JNDI 应用程序以对目录执行各种操作。

一旦您设置了目录，或者已经指示您的程序与现有目录进行通信，您可以在那里找到哪种信息？

可以将目录视为由名称到对象绑定组成。 也就是说，目录中的每个对象都具有相应的名称。您可以通过查找其名称来检索目录中的对象。

存储在目录中的还有属性。除了具有名称之外，目录中的对象还具有可选的属性集。您可以向目录询问对象的属性，并要求它搜索具有某些属性的对象。

**步骤3：目录模式**

模式指定目录可能包含的对象类型。本教程使用条目填充目录，其中一些条目需要特殊的模式定义。要容纳这些条目，您必须首先关闭服务器中的模式检查，或者将本教程附带的模式文件添加到服务器。这两项任务通常由目录服务器的管理员执行。

本教程附带两个必须安装的模式文件：

- [`Schema for Java objects`](https://docs.oracle.com/javase/tutorial/jndi/software/config/java.schema)
- [`Schema for CORBA objects`](https://docs.oracle.com/javase/tutorial/jndi/software/config/corba.schema)

这些文件的格式是正式描述，可能无法直接复制并粘贴到服务器配置文件中。具体地，属性语法以 [RFC 2252](http://www.ietf.org/rfc/rfc2252.txt) 的形式描述。

不同的目录服务器具有不同的配置其架构的方式。本教程包含一些用于在目录服务器上安装 Java 和 CORBA 模式的工具，这些模式允许通过 LDAP 修改其模式。以下是工具可以执行的任务列表。

1. [`Create Java Schema`](https://docs.oracle.com/javase/tutorial/jndi/software/config/CreateJavaSchema.java)
2. [`Create CORBA Schema`](https://docs.oracle.com/javase/tutorial/jndi/software/config/CreateCorbaSchema.java)

按照随附的 [`README文件`](https://docs.oracle.com/javase/tutorial/jndi/software/config/README-SCHEMA.TXT) 中的说明运行这些程序。

------

**注意：Windows Active Directory。**Active Directory 使用内部格式管理其架构。若要更新架构，可以按照Active Directory 的说明使用 Active Directory 管理控制台管理单元，`ADSIEdit`或`CreateJavaSchema`实用程序。

----

**步骤4：为此指引提供目录内容**

在此课程的示例中，显示的结果反映了如何使用配置文件设置 LDAP 目录（[`tutorial.ldif`](https://docs.oracle.com/javase/tutorial/jndi/software/config/tutorial.ldif) ）。如果您使用的是现有服务器或具有不同设置的服务器，则可能会看到不同的结果。在将配置文件（[`tutorial.ldif`](https://docs.oracle.com/javase/tutorial/jndi/software/config/tutorial.ldif) ）加载到目录服务器之前，必须遵循有关更新服务器架构的说明，或者您可以在 UNIX 系统上使用 *ldapadd* 或 *ldapmodify* 命令（如果可用）。

例如，您可以使用 ldapmodify（通过插入适当的主机名值，管理员DN（-D选项）和密码）：

```
ldapmodify -a -c -v -h hostname -p 389\
        -D "cn=Administrator, cn=users, dc=xxx, dc=xxx"\
        -w passwd -f tutorial.ldif
```

------

**安装注意：访问控制。**不同的目录服务器以不同方式处理访问控制。本教程中的一些示例执行目录的更新。此外，您安装教程的命名空间部分可能具有读取访问限制。因此，您需要采取特定于服务器的操作来使目录可读和/或可更新，以使这些示例起作用。对于 [Oracle Directory Server](http://www.oracle.com/technetwork/testcontent/index-085178.html) ，添加 [`sunds.aci.ldif`](https://docs.oracle.com/javase/tutorial/jndi/software/config/sunds.aci.ldif) 中建议的`aci`条目文件到 `dn: o=JNDITutorial` 条目，使整个目录可读和可更新。或者，您可以更改示例，以便它们对目录进行身份验证。有关如何执行此操作的详细信息，请参阅 [安全](https://docs.oracle.com/javase/tutorial/jndi/ldap/security.html) 课程。

**安装注意：名称空间设置。**  [`tutorial.ldif`](https://docs.oracle.com/javase/tutorial/jndi/software/config/tutorial.ldif) 文件中的条目使用尊贵名称（DN）“o=JNDITutorial”用于根命名上下文。如果您尚未将目录服务器配置为将“o=JNDITutorial”作为根命名上下文，则导入`tutorial.ldif`的尝试将失败。解决此问题的最简单方法是将现有根命名上下文的DN添加到`tutorial.ldif`文件中的每个“dn:”行。例如，如果您的服务器已经具有根命名上下文“dc=imc,dc=org”，那么您应该更改该行

```
dn: o=JNDITutorial
```

为

```
dn: o=JNDITutorial, dc=imc, dc=org
```

对文件中以“dn:”开头的每一行进行此更改。然后，在本教程的所有示例中，无论使用“o=JNDITutorial”，请使用“o=JNDITutorial,dc=imc,dc=org”。

**安装说明：文件格式。**根据您使用的操作系统平台，您可能需要编辑`tutorial.ldif`，以便它包含该平台的正确换行符。例如，如果您发现`tutorial.ldif`包含 Windows 样式的换行符（CRLF），并且您要将此文件导入到在 UNIX 平台上运行的目录服务器，则需要编辑该文件并将 CRLF 替换为 LF。此问题的一个症状是目录服务器拒绝`tutorial.ldif`中的所有条目。

**安装说明：Windows Active Directory。**

1. 根命名上下文不会是“o=jnditutorial”。它的形式为“dc=x,dc=y,dc=z”。您需要按照之前的**Namespace Setup**说明进行操作。

2. 使用 Active Directory 管理控制台管理单元`ADSIEdit`将“inetOrgPerson”和“groupOfUniqueNames”的对象类和相关属性添加到 Active Directory 架构。“groupOfUniqueNames”在 [RFC 2256](http://www.ietf.org/rfc/rfc2256.txt) 中定义，“inetOrgPerson”在 [RFC 2798](http://www.ietf.org/rfc/rfc2798.txt) 中定义。

3. 默认情况下，Active Directory 中不允许使用本教程使用的某些层次关系。要启用这些关系，请使用 Active Directory 管理控制台管理单元`ADSIEdit`添加它们。

   ````
   objectclass: organizationalUnit
   possible superiors: domainDNS
                       inetOrgPerson
                       organizaton
                       organizationalPerson
                       organizationalUnit
                       person
                       top
   
   objectclass: groupOfUniqueNames
   possible superiors: top
   
   objectclass: inetOrgPerson
   possible superiors: container
                       organizationalPerson
                       person
                       top
   ````

4. 从`tutorial.ldif`中的 Mark Twain 条目中删除两个“sn”属性中的一个。与 [RFC 2256](http://www.ietf.org/rfc/rfc2256.txt) 相反，Active Directory 将“sn”定义为单值属性。

5. 使用`dcifde`command-line实用程序加载修改后的`tutorial.ldif`文件。

      ```
   #ldif -i -v -k -f tutorial.ldif
   ```

6.  大多数示例假定已将目录设置为允许未经身份验证的读取和更新访问。您的 Active Directory 设置可能不允许您这样做。 请参阅**Access Control**安装说明。

7.  读取条目有时会产生比教程中显示的更多的属性，因为 Active Directory 通常会返回一些内部属性。

8.  创建条目可能需要指定其他特定于Active Directory的属性或使用其他对象类。


