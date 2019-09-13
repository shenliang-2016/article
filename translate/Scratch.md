### Java 应用设置

为了在你的应用中使用 JNDI，你需要配置它的编译和执行环境。

**导入 JNDI 类**

下面是 JNDI 包：

- [`javax.naming`](https://docs.oracle.com/javase/8/docs/api/javax/naming/package-summary.html)
- [`javax.naming.directory`](https://docs.oracle.com/javase/8/docs/api/javax/naming/directory/package-summary.html)
- [`javax.naming.event`](https://docs.oracle.com/javase/8/docs/api/javax/naming/event/package-summary.html)
- [`javax.naming.ldap`](https://docs.oracle.com/javase/8/docs/api/javax/naming/ldap/package-summary.html)
- [`javax.naming.spi`](https://docs.oracle.com/javase/8/docs/api/javax/naming/spi/package-summary.html)

此课程中的示例使用前两个包中的类和接口。您需要将这两个包导入您的程序或导入您使用的各个类和接口。以下两行从两个包`javax.naming`和`javax.naming.directory`导入所有类和接口。

```java
import javax.naming.*;
import javax.naming.directory.*;
```

**编译环境**

要编译使用 JNDI 的程序，您需要访问 JNDI 类。[Java SE 6](https://docs.oracle.com/javase/tutorial/jndi/software/package.html) 已经包含了 JNDI 类，因此如果您正在使用它，则无需采取进一步的操作。

**执行环境**

要运行使用 JNDI 的程序，您需要访问程序使用的任何服务提供程序的 JNDI 类和类。[Java Runtime Environment（JRE）6](https://docs.oracle.com/javase/tutorial/jndi/software/package.html) 已经包含用于 LDAP，COS 命名，RMI 注册的服务提供程序、 JNDI 类和DNS。

如果您正在使用其他服务提供程序，则需要在 *JAVA_HOME*`/jre/lib/ext` 目录中下载并安装其存档文件，其中*JAVA_HOME* 是包含 JRE 的目录。[JNDI页面](http://www.oracle.com/technetwork/java/jndi/index.html#download) 列出了一些服务提供者。您可以下载这些提供者或使用其他供应商的提供者。

