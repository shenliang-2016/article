## 创建客户端程序

计算引擎是个相对简单的程序：它执行传递给它的任务。计算引擎的客户端更复杂一些。客户端需要调用计算引擎，同时还需要定义需要计算引擎执行的任务。

两个类构成了我们例子中的客户端。第一个类，`ComputePi` ，查找并调用一个 `Compute` 对象。第二个类，`Pi`，实现 `Task` 接口，定义由计算引擎完成的工作。`Pi` 类的工作是计算 ![the pi symbol](https://docs.oracle.com/javase/tutorial/figures/rmi/pi.gif) 的若干位小数值。

非远程的 [`Task`](https://docs.oracle.com/javase/tutorial/rmi/examples/compute/Task.java) 接口定义如下：

```java
package compute;

public interface Task<T> {
    T execute();
}
```

调用 `Compute` 对象的方法的代码必须获取对该对象的引用，创建一个 `Task` 对象，然后请求执行该任务。任务类 `Pi` 的定义将在后面展示。一个 `Pi` 对象是用一个参数构造的，结果是所需的精度。任务执行的结果是一个 `java.math.BigDecimal` 表示 ![pi符号](https://docs.oracle.com/javase/tutorial/figures/rmi/pi.gif)值，计算到指定的精度。

这里是 [`client.ComputePi`](https://docs.oracle.com/javase/tutorial/rmi/examples/client/ComputePi.java) 的源代码，主要的客户端类：

```java
package client;

import java.rmi.registry.LocateRegistry;
import java.rmi.registry.Registry;
import java.math.BigDecimal;
import compute.Compute;

public class ComputePi {
    public static void main(String args[]) {
        if (System.getSecurityManager() == null) {
            System.setSecurityManager(new SecurityManager());
        }
        try {
            String name = "Compute";
            Registry registry = LocateRegistry.getRegistry(args[0]);
            Compute comp = (Compute) registry.lookup(name);
            Pi task = new Pi(Integer.parseInt(args[1]));
            BigDecimal pi = comp.executeTask(task);
            System.out.println(pi);
        } catch (Exception e) {
            System.err.println("ComputePi exception:");
            e.printStackTrace();
        }
    }    
}
```

与 `ComputeEngine` 服务器一样，客户端首先安装安全管理器。此步骤是必需的，因为接收服务器远程对象的存根的过程可能需要从服务器下载类定义。要使 RMI 下载类，必须使用安全管理器。

在安装安全管理器之后，客户端构造一个名称，用于查找 `Compute` 远程对象，使用与 `ComputeEngine` 相同的名称来绑定其远程对象。此外，客户端使用 `LocateRegistry.getRegistry` API 来合成对服务器主机上的注册表的远程引用。第一个命令行参数 `args[0]` 的值是运行 `Compute` 对象的远程主机的名称。然后，客户端在注册表上调用 `lookup` 方法，以便在服务器主机的注册表中按名称查找远程对象。使用的 `LocateRegistry.getRegistry` 的特定重载，它有一个 `String` 参数，返回对命名主机和默认注册表端口 `1099` 的注册表的引用。您必须使用具有 `int` 参数的重载，如果注册表是在 `1099` 以外的端口上创建的。

接下来，客户端创建一个新的 `Pi` 对象，将第二个命令行参数 `args[1]` 的值传递给 `Pi` 构造函数，解析为整数。此参数指示计算中使用的小数位数。最后，客户端调用 `Compute` 远程对象的 `executeTask` 方法。传递给 `executeTask` 调用的对象返回一个类型为 `BigDecimal` 的对象，程序将该变量存储在变量 `result` 中。最后，程序打印结果。下图描述了 `ComputePi` 客户端，`rmiregistry` 和 `ComputeEngine` 之间的消息流。

![the flow of messages between the compute engine, the registry, and the client.](https://docs.oracle.com/javase/tutorial/figures/rmi/rmi-4.gif)

`Pi` 类实现 `Task` 接口，并将 ![pi符号](https://docs.oracle.com/javase/tutorial/figures/rmi/pi.gif)的值计算为指定小数位的值。对于此示例，实际算法并不重要。重要的是该算法的计算成本很高，这意味着您希望在有能力的服务器上执行该算法。

这里是 [`client.Pi`](https://docs.oracle.com/javase/tutorial/rmi/examples/client/Pi.java) 的源代码，该类实现了 `Task` 接口：

```java
package client;

import compute.Task;
import java.io.Serializable;
import java.math.BigDecimal;

public class Pi implements Task<BigDecimal>, Serializable {

    private static final long serialVersionUID = 227L;

    /** constants used in pi computation */
    private static final BigDecimal FOUR =
        BigDecimal.valueOf(4);

    /** rounding mode to use during pi computation */
    private static final int roundingMode = 
        BigDecimal.ROUND_HALF_EVEN;

    /** digits of precision after the decimal point */
    private final int digits;
    
    /**
     * Construct a task to calculate pi to the specified
     * precision.
     */
    public Pi(int digits) {
        this.digits = digits;
    }

    /**
     * Calculate pi.
     */
    public BigDecimal execute() {
        return computePi(digits);
    }

    /**
     * Compute the value of pi to the specified number of 
     * digits after the decimal point.  The value is 
     * computed using Machin's formula:
     *
     *          pi/4 = 4*arctan(1/5) - arctan(1/239)
     *
     * and a power series expansion of arctan(x) to 
     * sufficient precision.
     */
    public static BigDecimal computePi(int digits) {
        int scale = digits + 5;
        BigDecimal arctan1_5 = arctan(5, scale);
        BigDecimal arctan1_239 = arctan(239, scale);
        BigDecimal pi = arctan1_5.multiply(FOUR).subtract(
                                  arctan1_239).multiply(FOUR);
        return pi.setScale(digits, 
                           BigDecimal.ROUND_HALF_UP);
    }
    /**
     * Compute the value, in radians, of the arctangent of 
     * the inverse of the supplied integer to the specified
     * number of digits after the decimal point.  The value
     * is computed using the power series expansion for the
     * arc tangent:
     *
     * arctan(x) = x - (x^3)/3 + (x^5)/5 - (x^7)/7 + 
     *     (x^9)/9 ...
     */   
    public static BigDecimal arctan(int inverseX, 
                                    int scale) 
    {
        BigDecimal result, numer, term;
        BigDecimal invX = BigDecimal.valueOf(inverseX);
        BigDecimal invX2 = 
            BigDecimal.valueOf(inverseX * inverseX);

        numer = BigDecimal.ONE.divide(invX,
                                      scale, roundingMode);

        result = numer;
        int i = 1;
        do {
            numer = 
                numer.divide(invX2, scale, roundingMode);
            int denom = 2 * i + 1;
            term = 
                numer.divide(BigDecimal.valueOf(denom),
                             scale, roundingMode);
            if ((i % 2) != 0) {
                result = result.subtract(term);
            } else {
                result = result.add(term);
            }
            i++;
        } while (term.compareTo(BigDecimal.ZERO) != 0);
        return result;
    }
}
```

请注意，所有可序列化的类，无论是直接还是间接地实现 `Serializable` 接口，都必须声明一个名为 `serialVersionUID` 的 `private` `static` `final` 字段，以保证版本之间的序列化兼容性。如果没有发布该类的先前版本，则该字段的值可以是任何 `long` 值，类似于 `Pi` 使用的 `227L`，只要该值在将来的版本中一致使用即可。如果在没有明确的 `serialVersionUID` 声明的情况下发布了该类的先前版本，但与该版本的序列化兼容性很重要，则必须将先前版本的默认隐式计算值用于新版本的显式声明的值。可以针对先前版本运行 `serialver` 工具以确定它的默认计算值。

这个例子最有趣的特性是 `Compute` 实现对象永远不需要 `Pi` 类的定义，直到 `Pi` 对象作为 `executeTask` 方法的参数传入。此时，类的代码由 RMI 加载到 `Compute` 对象的 Java 虚拟机中，调用 `execute` 方法，并执行任务的代码。结果，在 `Pi` 任务的情况下是一个 `BigDecimal` 对象，被传递回客户端，在那里它用于打印计算结果。

提供的 `Task` 对象计算 `Pi` 的值这一事实与 `ComputeEngine` 对象无关。您还可以实现一项任务，例如，使用概率算法生成随机素数。该任务也是计算密集型的，因此是传递给 `ComputeEngine` 的一个很好的候选者，但它需要非常不同的代码。当 `Task` 对象传递给 `Compute` 对象时，也可以下载此代码。就像计算算法一样 ![pi符号](https://docs.oracle.com/javase/tutorial/figures/rmi/pi.gif)在需要时引入，生成随机素数的代码将在需要时引入。 `Compute` 对象只知道它接收的每个对象都实现了 `execute` 方法。`Compute`对象不知道，也不需要知道实现的作用。

