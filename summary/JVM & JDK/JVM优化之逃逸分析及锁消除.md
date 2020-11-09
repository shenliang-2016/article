## JVM优化之逃逸分析及锁消除

Published: 09 Jul 2019 Category: [JVM](http://it.deepinmind.com/categories.html#JVM-ref)

逃逸分析——我们在上一篇文章中所介绍的由编译器完成的一项的分析技术——使得删除锁的优化成为了可能。如果它能确认某个加锁的对象不会逃逸出局部作用域，就可以进行锁删除。这意味着这个对象同时只可能被一个线程访问，因此也就没有必要防止其它线程对它进行访问了。这样的话这个锁就是可以删除的。这个便叫做锁消除，本文是JVM实现机制的系列文章，这也正是今天要讲的主题。

众所周知，java.lang.StringBuffer是一个使用同步方法的线程安全的类，它可以用来很好地诠释锁消除。StringBuffer是Java1.0的时候开始引入的，可以用来高效地拼接不可变的字符串对象。它对所有append方法都进行了同步操作，以确保当多个线程同时写入同一个StringBuffer对象的时候也能够保证构造中的字符串可以安全地创建出来。

很多程序其实并不需要这层线程安全保障，因此在Java 5中又引入了一个非同步的java.lang.StringBuilder类来作为它的备选。这两个类都继承了包私有（注：简单来说就是没有修饰符的类）的java.lang.AbstractStringBuilder类，它们的append方法的实现也非常类似。

不同之处就在于StringBuffer的同步操作：

```
@Override
public synchronized StringBuffer append(String str) {
    toStringCache = null;
    super.append(str);

    return this;
}
```

和StringBuilder作一下对比：

```
@Override
public StringBuilder append(String str) {
    super.append(str);
    return this;
}
```

调用StringBuffer的append方法的线程，必须得获取到这个对象的内部锁（也叫监视器锁）才能进入到方法内部，在退出方法前也必须要释放掉这个锁。而StringBuilder就不需要进行这个操作，因此它的执行性能比StringBuffer的要高——至少乍看上去是这样的。

不过在HotSpot虚拟机引入了逃逸分析之后，在调用像StringBuffer这样的对象的同步方法时，就能够自动地把锁消除掉了。这只会出现在方法域内部所创建的对象上，只有这样才能保证不会发生逃逸。

Java的性能测试一般都会用到Java Microbenchmark Harness（JMH）。我们就用JMH来测试一下，当现代的JVM能够确认StringBuffer对象只能被一个线程访问时，它是如何通过消除StringBuffer上的锁来缩小性能上的差距的。

```
@State(Scope.Thread)
@BenchmarkMode(Mode.Throughput)
@OutputTimeUnit(TimeUnit.SECONDS)
public class StringBufferLockElision {
    private static final String[] pieces =
        new String[]{"a", "b", "c", "d", "e"};

    @Benchmark
    public String concatWithStringBuffer() {
        final StringBuffer buffer = new StringBuffer();
        for (String piece : pieces) {
            buffer.append(piece);
        }
        return buffer.toString();
    }

    @Benchmark
    public String concatWithStringBuilder() {
        StringBuilder builder = new StringBuilder();
        for (String piece : pieces) {
            builder.append(piece);
        }
        return builder.toString();
    }
}
```



锁消除是一项非常有效的优化，在Java 8中它是默认开启的，不过你也可以通过-XX:-DoEscapeAnalysis这个VM参数来关掉它，这样可以看下优化的效果。开启（默认）了逃逸分析后，StringBuffer和StringBuilder的性能基本上是一样的。（结果报告统计的是每秒执行的操作数。分数越高说明性能越好。）

```text
concatWithStringBuffer  16280252.994 ± 17K  ops/s
concatWithStringBuilder 16479504.748 ± 34K  ops/s
concatWithStringBuffer  12385164.076 ± 58K  ops/s
concatWithStringBuilder 14570548.284 ± 55K  ops/s
```

如上所示，关掉了逃逸分析后，StringBuffer的代码要慢15%左右——而这个差别主要就是由于调用append()方法时的加锁操作导致的。

### 锁粗化（Lock Coarsening）

HotSpot虚拟机还有一些额外的锁优化的技术，虽然从技术上讲它们并不属于逃逸分析子系统中的一部分，但也是通过分析作用域来提高内部锁的性能。当连续获取同一个对象的锁时，HotSpot虚拟机会去检查多个锁区域是否能合并成一个更大的锁区域。这种聚合被称作锁粗化，它能够减少加锁和解锁的消耗。

当HotSpot JVM发现需要加锁时，它会尝试往前查找同一个对象的解锁操作。如果能匹配上，它会考虑是否要将两个锁区域作合并，并删除一组解锁/加锁操作。

我们来看一个程序，它会连续获取同一个对象的监视器锁：

```
public class CoarsenedLocks {
    public static void main(String[] args) {
        new CoarsenedLocks();
    }

    private java.util.Random random = new java.util.Random();

    private static final Object lock = new Object();

    public CoarsenedLocks()
    {
        long sum = 0;

        for (int i = 0; i < 1_000_000; i++) {
            synchronized (lock) {
                sum += random.nextInt();
            }
            synchronized (lock) {
                sum -= random.nextInt();
            }     
        }
        System.out.println(sum);
    }
}
```

它的字节码如下，看起来非常的冗长：

```
public optjava.CoarsenedLocks();
    descriptor: ()V
    flags: ACC_PUBLIC
    Code:
      stack=5, locals=5, args_size=1
         0: aload_0
         1: invokespecial #3
         4: aload_0
         5: lconst_0
         6: putfield     #4
         // Method java/lang/Object."<init>":()V
         // Field sum:J
         // int 1000000
         9: iconst_0
         10: istore_1
         11: iload_1
         12: ldc          #5
         14: if_icmpge     73
         17: aload_0
         18: dup
         19: astore_2
         20: monitorenter
         21: aload_0
         22: dup
         23: getfield      #4       // Field sum:J
         26: lconst_1
         27: ladd
         28: putfield      #4         // Field sum:J
         31: aload_2
         32: monitorexit
         33: goto          41
         36: astore_3
         37: aload_2
         38: monitorexit
         39: aload_3
         40: athrow
         41: aload_0
         42: dup
         43: astore_2
         44: monitorenter
         45: aload_0
         46: dup
         47: getfield      #4         // Field sum:J
         50: lconst_1
         51: lsub
         52: putfield      #4         // Field sum:J
         55: aload_2
         56: monitorexit
         57: goto          67
         60: astore        4
         62: aload_2
         63: monitorexit
         64: aload            4
         66: athrow
         67: iinc         1,1
         70: goto         11       
            // Field java/lang/System.out:Ljava/io/PrintStream;
         73: getstatic     #6
         76: aload_0
         77: getfield      #4       // Field sum:J       
            // Method java/io/PrintStream.println:(J)V
         80: invokevirtual #7
         83: return
```

[代码最后的注释对应着后面的输出结果行。——Ed.]

先来回顾一下，操作内部锁对应的字节码是monitorenter和monitorexit。

字节码中的每一条monitorenter指令都会对应着两条monitorexit指令，它们分别对应着不同的执行路径。原因是第一条monitorexit指令会在正常退出锁区域时释放监视器锁，而第二条指令则是在异常退出时进行释放。

这段字节码看起来可能很奇怪，因为在源程序中同步块中只有一个int变量的自增操作而已。代码中并没有抛异常，不过它的确有可能会异常退出锁区域。（如果线程捕获到InterruptedException异常就可能会这样，比如调用了执行线程的stop()方法。因此，需要有第二条执行路径来确保监视器锁一定能被释放掉，即使是抛了非受检异常（unchecked exception）也是如此。从JVM规范中可以了解到更多相关知识。）锁粗化是默认开启的，不过也可以通过启动参数-XX:-EliminateLocks来关掉它。

### 嵌套锁

同步块可能会一个嵌套一个，进而两个块使用同一个对象的监视器锁来进行同步也是很有可能的。这种情况我们称之为嵌套锁，HotSpot虚拟机是可以识别出来并删除掉内部块中的锁的。当一个线程进入外部块时就已经获取到锁了，因此当它尝试进入内部块时，肯定也仍持有这个锁，所以这个时候删除锁是可行的。

在写作本文的时候，Java 8中的嵌套锁删除只有在锁被声明为static final或者锁的是this对象时才可能发生。

下面是一个碰到嵌套同步块时删除内部锁的例子：

```
public class NestedLocks {
    public static void main(String[] args) {
        new NestedLocks();
    }

    private java.util.Random random = new java.util.Random();

    private static final Object lock = new Object();

    public NestedLocks()
    {
        long sum = 0;

        for (int i = 0; i < 1_000_000; i++) {
            synchronized (lock) {
                sum += random.nextInt();

                synchronized (lock) {
                    sum -= random.nextInt();
                }

            } 
        }

        System.out.println(sum);
    }
}
```

HotSpot虚拟机会删除掉内部的嵌套锁，因此这段代码最终会变成这样：

```
for (int i = 0; i < 1_000_000; i++) {
    synchronized(lock) {
        sum += random.nextInt();

        sum -= random.nextInt();
    }
}
```

嵌套锁优化是默认开启的，不过也可以通过启动参数-XX:-EliminateNestedLocks来关掉它。

### 数组及逃逸分析

非堆上分配的空间要么存储在栈上，要么就在CPU寄存器中，这些都是相对稀缺的资源，因此逃逸分析和其它优化一样，（在实现上）肯定会面临妥协。HotSpot JVM上的一个默认限制是大于64个元素的数组不会进行逃逸分析优化。这个大小可以通过启动参数-XX:EliminateAllocationArraySizeLimit=n来进行控制，n是数组的大小。

假设有段热点代码，它会去分配一个临时数组用于从缓存中读取数据。如果逃逸分析发现这个数组的作用域没有逃逸出方法体外，便不会在堆上分配内存。不过如果数组大小超过64的话（哪怕并不是全都用到）便仍会存储到堆里。这样数组的逃逸分析优化便不会起作用，也仍会从堆内分配内存。

在下面的JMH基准测试中，test方法会分别新建大小为63、64、65的非逃逸数组。（大小为63的数组之所以也参与测试，是为了证明64的数组比65的快并不是因为内存对齐的缘故。）

每轮测试都只使用到了数组的前两个元素，也就是a[0]和a[1]。需要注意的是，逃逸分析只受限于数组长度的大小，和实际使用到多少个元素是没有关系的。

```
@State(Scope.Thread)
@BenchmarkMode(Mode.Throughput)
@OutputTimeUnit(TimeUnit.SECONDS)
public class EscapeTestArraySize {
    private java.util.Random random = new java.util.Random();

    @Benchmark
    public long arraySize63() {
        int[] a = new int[63];
        a[0] = random.nextInt();
        a[1] = random.nextInt();
        return a[0] + a[1];
    }

    @Benchmark
    public long arraySize64() {
        int[] a = new int[64];
        a[0] = random.nextInt();
        a[1] = random.nextInt();


        return a[0] + a[1];
    }

    @Benchmark
    public long arraySize65() {
        int[] a = new int[65];
        a[0] = random.nextInt();
        a[1] = random.nextInt();
        return a[0] + a[1];
    }
}
```



从结果来看，一旦数组分配不能受益于逃逸分析的优化时，性能便会出现大幅下降。（这里的分数也是对应的每秒的操作数，分越高性能越好。）

```text
EscapeTestArraySize.arraySize63  49824186.696 ±  9K  ops/s
EscapeTestArraySize.arraySize64  49815447.849 ±  2K  ops/s
EscapeTestArraySize.arraySize65  21115003.388 ± 34K  ops/s
```

如果你需要在热点代码中分配更大的数组，可以通过配置让虚拟机对大数组进行优化。把元素上限调整成65，然后再跑一下基准测试便会发现性能也对齐了。

命令行：

> java -XX:EliminateAllocationArraySizeLimit=65 -jar target/benchmarks.jar

的执行结果是：

```text
EscapeTestArraySize.arraySize63  49814492.787 ± 2K  ops/s
EscapeTestArraySize.arraySize64  49815595.566 ± 6K  ops/s
EscapeTestArraySize.arraySize65  49818143.279 ± 2K  ops/s
```

可以看到结果是一样的。

### 结论

本文及上一篇关于逃逸分析的文章给大家展示了HotSpot JVM所蕴藏的一些魔力。同时大家也能看到这些优化背后的复杂度。Java的每一次大的版本发布都会往JVM中增加一些新的特性。

事实上，Oracle也在研究下一代的编译技术。它便是[Graal](https://github.com/oracle/graal)，这是一款可插拔、可扩展的、Java实现的just-in-time (JIT)编译器。它是Metropolis项目的重要组成部分，这个项目的目标是尽可能多地使用Java语言来构建JVM的运行时程序。

正如[JEP 317](http://openjdk.java.net/jeps/317)中所提到的，Graal编译器是Java 10的一项实验性的新功能。它的主要目标是让开发人员和专业平台的负责人能够自己去编写专属的、满足自身特殊需求的JIT编译器。对于新的优化技术的设计和原型完成来说，Graal是一个非常合适的平台。

本文及上一篇文章所提到的作用域分析的方法可以用来实现很多优化技术。首先便是分配消除（allocation elimination，也就是标量替换，注：指的是把对象分解成int等基础类型，在栈和寄存器中分配空间，这样就可以不在堆上分配内存，也不需要GC进行回收了），还有我们讨论到的这些锁相关的技术。这些只是HotSpot JVM中成熟的C2编译器的所提供的JIT编译技术中的一些例子。后续的文章还会陆续介绍HotSpot JVM中用来提升代码性能的一些其它的技术。

[英文原文链接](http://www.javamagazine.mozaicreader.com/MayJune2018/Default/74/0/3978350)