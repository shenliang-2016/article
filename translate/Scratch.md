## 编译并运行示例

现在，计算引擎示例的代码已经完成，它需要被编译并运行。

[编译示例程序](https://docs.oracle.com/javase/tutorial/rmi/compiling.html)

本节中，你将学到编译组成计算引擎示例的服务器和客户端程序。

[运行示例代码](https://docs.oracle.com/javase/tutorial/rmi/running.html)

最后，你运行服务器和客户端程序计算 ![the pi symbol](https://docs.oracle.com/javase/tutorial/figures/rmi/pi.gif)值。

### 编译示例程序

在部署了计算引擎等服务的实际场景中，开发人员可能会创建一个 Java Archive（JAR）文件，其中包含用于实现服务器类的 `Compute` 和 `Task` 接口以及用于实现客户端程序的客户端程序。接下来，开发人员（可能是接口 JAR 文件的相同开发人员）将编写 `Compute` 接口的实现，并将该服务部署在客户端可用的机器上。客户端程序的开发人员可以使用 JAR 文件中包含的 `Compute` 和 `Task` 接口，并独立开发使用 `Compute` 服务的任务和客户端程序。

在本节中，您将学习如何设置 JAR 文件，服务器类和客户端类。您将看到客户端的 `Pi` 类将在运行时下载到服务器。此外，`Compute` 和 `Task` 接口将在运行时从服务器下载到注册表。

此示例将接口，远程对象实现和客户端代码分为三个包：

- `compute` – [`Compute`](https://docs.oracle.com/javase/tutorial/rmi/examples/compute/Compute.java) 和 [`Task`](https://docs.oracle.com/javase/tutorial/rmi/examples/compute/Task.java) 接口
- `engine` – [`ComputeEngine`](https://docs.oracle.com/javase/tutorial/rmi/examples/engine/ComputeEngine.java) 实现类
- `client` – [`ComputePi`](https://docs.oracle.com/javase/tutorial/rmi/examples/client/ComputePi.java) 客户端代码和 [`Pi`](https://docs.oracle.com/javase/tutorial/rmi/examples/client/Pi.java) 任务实现

首先，您需要构建接口 JAR 文件以提供给服务器和客户端开发人员。

**构建接口类的 JAR 文件**

首先，您需要在 `compute` 包中编译接口源文件，然后构建包含其类文件的 JAR 文件。假设用户 `waldo` 编写了这些接口并将源文件放在 Windows 上的目录 `c:\home\waldo\src\compute` 或 Solaris OS 或 Linux 上的目录 `/home/waldo/src/compute` 中。给定这些路径，您可以使用以下命令编译接口并创建 JAR 文件：

**Microsoft Windows**:

```shell
cd c:\home\waldo\src
javac compute\Compute.java compute\Task.java
jar cvf compute.jar compute\*.class
```

**Solaris OS or Linux**:

```shell
cd /home/waldo/src
javac compute/Compute.java compute/Task.java
jar cvf compute.jar compute/*.class
```

------

由于 `-v` 选项，`jar` 命令显示以下输出：

```
added manifest
adding: compute/Compute.class(in = 307) (out= 201)(deflated 34%)
adding: compute/Task.class(in = 217) (out= 149)(deflated 31%)
```

现在，您可以将 `compute.jar` 文件分发给服务器和客户端应用程序的开发人员，以便他们可以使用这些接口。

使用 `javac` 编译器构建服务器端或客户端类之后，如果其他 Java 虚拟机需要动态下载其中任何类，则必须确保将其类文件放在网络可访问的位置。在此示例中，对于 Solaris OS 或 Linux，此位置为`/home/user/public_html/classes`，因为许多 Web 服务器允许通过构造为 `http://host/~*user*/` 的 HTTP URL 访问用户的 `public_html` 目录。如果您的 Web 服务器不支持此约定，则可以在 Web 服务器的层次结构中使用其他位置，或者您可以使用文件 URL。文件 URL 在 Solaris OS 或 Linux 上采用 `file:/home/user/public_html/classes/`形式，在 Windows 上采用`file:/c:/home/user/public_html/classes/`形式。您也可以根据需要选择其他类型的 URL。

类文件的网络可访问性使 RMI 运行时能够在需要时下载代码。RMI 不是为代码下载定义自己的协议，而是使用 Java 平台支持的 URL 协议（例如 HTTP）来下载代码。请注意，使用完整的重量级 Web 服务器来提供这些类文件是不必要的。例如，可以在以下位置找到一个简单的 HTTP 服务器，该服务器提供使类可通过 HTTP 在 RMI 中下载所需的功能。
另请参见 [远程方法调用主页](http://www.oracle.com/technetwork/java/javase/tech/index-jsp-136424.html) 。

**构建服务器类**

`engine` 包只包含一个服务器端实现类，`ComputeEngine`，远程接口 `Compute` 的实现。

假设用户 `ann`，`ComputeEngine` 类的开发人员，已将 `ComputeEngine.java` 放在 Windows 上的目录 `c:\home\ann\src\engine` 或 Solaris OS 或 Linux 上的目录 `/home/ann/src/engine` 中。她正在为客户端部署类文件，以便在她的 `public_html` 目录的子目录中下载，在 Windows 上运行 `c:\home\ann\public_html\classes` 或在Solaris OS 或 Linux 上运行 `/home/ann/public_html/classes` 。这个位置可以通过一些 Web 服务器访问为 `http://host:port/~ann/classes/`。

`ComputeEngine` 类依赖于 `Compute` 和 `Task` 接口，它们包含在 `compute.jar`  JAR 文件中。因此，在构建服务器类时，需要在类路径中使用 `compute.jar` 文件。假设 `compute.jar` 文件位于 Windows 上的目录 `c:\home\ann\public_html\classes` 或 Solaris OS 或 Linux 上的目录 `/home/ann/public_html/classes`中。给定这些路径，您可以使用以下命令来构建服务器类：

**Microsoft Windows**:

```
cd c:\home\ann\src
javac -cp c:\home\ann\public_html\classes\compute.jar
    engine\ComputeEngine.java
```

**Solaris OS or Linux**:

```
cd /home/ann/src
javac -cp /home/ann/public_html/classes/compute.jar
    engine/ComputeEngine.java
```

`ComputeEngine` 的存根类实现了 `Compute` 接口，它指的是 `Task` 接口。因此，这两个接口的类定义需要是网络可访问的，以便存根被其他 Java 虚拟机（如注册表的 Java 虚拟机）接收。客户端 Java 虚拟机已经在其类路径中具有这些接口，因此实际上不需要下载它们的定义。 `public_html` 目录下的 `compute.jar` 文件可以用于此目的。

现在，计算引擎已准备好部署。您现在可以这样做，或者您可以等到构建客户端之后。

**构建客户端类**

`client` 包包含两个类，`ComputePi`，主客户端程序，以及 `Pi`，客户端实现 `Task` 接口。

假设用户 `jones`（客户端类的开发人员）已将 `ComputePi.java` 和 `Pi.java` 放在 Windows 上的目录 `c:\home\jones\src\client` 或 Solaris OS 或 Linux上的 `/home/jones/src/client` 目录。他正在为计算引擎部署类文件，以便在他的 `public_html` 目录的子目录中下载，在 Windows 上的 `c:\home\jones\public_html\classes` 或在 Solaris OS 或 Linux上的`/home/jones/public_html/classes` 下载。这个位置可以通过一些 Web 服务器访问为 `http://*host*:*port*/~jones/classes/`。

客户端类依赖于 `Compute` 和 `Task` 接口，它们包含在 `compute.jar`  JAR 文件中。因此，在构建客户端类时，需要在类路径中使用 `compute.jar` 文件。假设 `compute.jar` 文件位于 Windows 上的目录 `c:\home\jones\public_html\classes` 或 Solaris OS 或 Linux 上的目录 `/home/jones/public_html/classes` 中。给定这些路径，您可以使用以下命令来构建客户端类：

**Microsoft Windows**:

```
cd c:\home\jones\src
javac -cp c:\home\jones\public_html\classes\compute.jar
    client\ComputePi.java client\Pi.java
mkdir c:\home\jones\public_html\classes\client
cp client\Pi.class
    c:\home\jones\public_html\classes\client
```

**Solaris OS or Linux**:

```
cd /home/jones/src
javac -cp /home/jones/public_html/classes/compute.jar
    client/ComputePi.java client/Pi.java
mkdir /home/jones/public_html/classes/client
cp client/Pi.class
    /home/jones/public_html/classes/client
```

只需要将 `Pi` 类放在 `public_html\classes\client` 目录中，因为只需要 `Pi` 类可以下载到计算引擎的 Java 虚拟机。现在，您可以运行服务器，然后运行客户端。

### 运行示例程序

**一个安全提示**

服务器和客户端程序在安装了安全管理器的情况下运行。运行任一程序时，需要指定安全策略文件，以便为代码授予其运行所需的安全权限。这是一个例子 [policy file to use with the server program](https://docs.oracle.com/javase/tutorial/rmi/examples/server.policy)：

```
grant codeBase "file:/home/ann/src/" {
    permission java.security.AllPermission;
};
```

[policy file to use with the client program](https://docs.oracle.com/javase/tutorial/rmi/examples/client.policy) 的例子：

```
grant codeBase "file:/home/jones/src/" {
    permission java.security.AllPermission;
};
```

对于两个示例策略文件，所有权限都授予程序的本地类路径中的类，因为本地应用程序代码是受信任的，但是没有权限授予从其他位置下载的代码。因此，计算引擎服务器限制它执行的任务（其代码不可信并且可能是恶意的）执行任何需要安全权限的操作。示例客户端的 `Pi` 任务不需要任何权限来执行。

在此示例中，服务器程序的策略文件名为 `server.policy`，客户端程序的策略文件名为 `client.policy`。

**启动服务器**

在启动计算引擎之前，您需要启动 RMI 注册表。RMI 注册表是一个简单的服务器端引导程序命名工具，它使远程客户端能够获取对初始远程对象的引用。它可以使用 `rmiregistry` 命令启动。在执行 `rmiregistry` 之前，必须确保运行 `rmiregistry` 的 shell 或窗口没有设置 `CLASSPATH` 环境变量或者有一个不包含任何您希望下载到客户端的远程对象的类路径的 `CLASSPATH` 环境变量。

要在服务器上启动注册表，请执行 `rmiregistry` 命令。 此命令不产生输出，通常在后台运行。对于此示例，注册表在主机 `mycomputer` 上启动。

**Microsoft Windows** (使用 `javaw` 如果 `start` 不可用):

```
start rmiregistry
```

**Solaris OS or Linux**:

```
rmiregistry &
```

默认情况下，注册表在端口1099上运行。要在其他端口上启动注册表，请在命令行上指定端口号。不要忘记取消设置 `CLASSPATH` 环境变量。

**Microsoft Windows**:

```
start rmiregistry 2001
```

**Solaris OS or Linux**:

```
rmiregistry 2001 &
```

注册表启动后，您可以启动服务器。您需要确保 `compute.jar` 文件和远程对象实现类都在您的类路径中。启动计算引擎时，需要使用 `java.rmi.server.codebase` 属性指定服务器的类可通过网络访问。在这个例子中，可供下载的服务器端类是 `Compute` 和 `Task` 接口，可以在用户 `ann` 的 `public_html\classes` 目录的 `compute.jar` 文件中找到。计算引擎服务器在主机 `mycomputer` 上启动，该主机是启动注册表的主机。

**Microsoft Windows**:

```
java -cp c:\home\ann\src;c:\home\ann\public_html\classes\compute.jar
     -Djava.rmi.server.codebase=file:/c:/home/ann/public_html/classes/compute.jar
     -Djava.rmi.server.hostname=mycomputer.example.com
     -Djava.security.policy=server.policy
        engine.ComputeEngine
```

**Solaris OS or Linux**:

```
java -cp /home/ann/src:/home/ann/public_html/classes/compute.jar
     -Djava.rmi.server.codebase=http://mycomputer/~ann/classes/compute.jar
     -Djava.rmi.server.hostname=mycomputer.example.com
     -Djava.security.policy=server.policy
        engine.ComputeEngine
```

上面的 `java` 命令定义了以下系统属性：

 - `java.rmi.server.codebase` 属性指定位置，即代码库 URL，从中可以下载*来自*此服务器的类的定义。如果代码库指定了目录层次结构（而不是 JAR 文件），则必须在代码库 URL 的末尾包含尾部斜杠。
 - `java.rmi.server.hostname` 属性指定要放入在此 Java 虚拟机中导出的远程对象的存根中的主机名或地址。此值是客户端在尝试传递远程方法调用时使用的主机名或地址。默认情况下，RMI 实现使用服务器的IP地址，如 `java.net.InetAddress.getLocalHost`  API所示。但是，有时，此地址不适用于所有客户端，并且完全限定的主机名将更有效。要确保 RMI 使用可从所有潜在客户端路由的服务器的主机名（或IP地址），请设置 `java.rmi.server.hostname` 属性。
 - `java.security.policy` 属性用于指定包含您要授予的权限的策略文件。

**启动客户端**

注册表和计算引擎运行后，您可以启动客户端，指定以下内容：

 - 客户端使用 `java.rmi.server.codebase` 属性为其类（`Pi`类）提供服务的位置
 - `java.security.policy` 属性，用于指定包含您要授予各种代码的权限的安全策略文件
 - 作为命令行参数，服务器的主机名（以便客户端知道 `Compute` 远程对象的位置）以及 ![the pi symbol](https://docs.oracle.com/javase/tutorial/figures/rmi/pi.gif) 计算中使用的小数位数。

在另一台主机（例如名为 `mysecondcomputer` 的主机）上启动客户端，如下所示：

------

**Microsoft Windows**:

```
java -cp c:\home\jones\src;c:\home\jones\public_html\classes\compute.jar
     -Djava.rmi.server.codebase=file:/c:/home/jones/public_html/classes/
     -Djava.security.policy=client.policy
        client.ComputePi mycomputer.example.com 45
```

**Solaris OS or Linux**:

```
java -cp /home/jones/src:/home/jones/public_html/classes/compute.jar
     -Djava.rmi.server.codebase=http://mysecondcomputer/~jones/classes/
     -Djava.security.policy=client.policy
        client.ComputePi mycomputer.example.com 45
```

请注意，类路径是在命令行上设置的，以便解释器可以找到客户端类和包含接口的 JAR 文件。另请注意，指定目录层次结构的 `java.rmi.server.codebase` 属性的值以尾部斜杠结尾。

启动客户端后，将显示以下输出：

```
3.141592653589793238462643383279502884197169399
```

下图说明了 `rmiregistry`，`ComputeEngine` 服务器和 `ComputePi` 客户端在程序执行期间获取类的位置。

![the registry, the compute engine, and the client obtaining classes during program execution](https://docs.oracle.com/javase/tutorial/figures/rmi/rmi-5.gif)

当 `ComputeEngine` 服务器在注册表中绑定其远程对象引用时，注册表会下载存根类依赖的 `Compute` 和 `Task` 接口。这些类是从 `ComputeEngine` 服务器的 Web 服务器或文件系统下载的，具体取决于启动服务器时使用的代码库 URL 的类型。

因为 `ComputePi` 客户端在其类路径中同时具有 `Compute` 和 `Task` 接口，所以它从类路径加载它们的定义，而不是从服务器的代码库加载它们的定义。

最后，当 `Pi` 对象在 `executeTask` 远程调用中传递给 `ComputeEngine` 对象时，`Pi` 类被加载到 `ComputeEngine` 服务器的 Java 虚拟机中。服务器从客户端的 Web 服务器或文件系统加载 `Pi` 类，具体取决于启动客户端时使用的代码库 URL 的类型。

