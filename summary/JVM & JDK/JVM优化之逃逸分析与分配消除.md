## JVM优化之逃逸分析与分配消除

Published: 11 Jul 2019 Category: [JVM](http://it.deepinmind.com/categories.html#JVM-ref)

在Java Magazine的前几期文章中，我们介绍了[just-in- time (JIT) 编译技术](https://bitbucket.org/javamagazine/magdownloads/downloads/2012-05-IntroToJIT-Evans&Lawrey-articleOnly.pdf)的一些理论基础，以及如何使用Java Microbenching Harness（JMH）和开源工具[JITWatch](http://www.javamagazine.mozaicreader.com/MarApr2015#&pageSet=33&page=0)来进行可视化分析，以便搞清楚HotSpot VM的内部机制。在这期文章中，我们将要深入介绍一下逃逸分析（escape analysis）技术，这是JVM最有意思的优化手段之一。逃逸分析是JVM的一项自动分析变量作用域的技术，它可以用来实现某些特殊的优化，后续我们也会分析下这些优化。在开始之前，你只需要掌握一些HotSpot JVM的基本工作原理就可以了。

要了解逃逸分析背后的基本原理，我们先来看下这段有问题的C代码——当然这个是没法用Java来写的：

```
int * get_the_int() {
    int i = 42;
    return &i; 
}
```

这段C代码在栈上创建了一个int类型的变量，然后把它的指针作为函数的返回值返回了。这样做是有问题的，因为当get*the*int()函数返回的时候，int所在的栈帧就已经被销毁了，后面你再去访问这个地址的话，就不知道里面存储的到底是什么了。

Java平台设计的一个主要目标就是要消除这种类型的bug。从设计上，JVM就不具备这种低级的“根据位置索引来读内存”的能力。这类操作对应的Java字节码是putfield和getfield。

来看下这段Java代码：

```
public class Rect {
    private int w;
    private int h;
    public Rect(int w, int h) {
        this.w = w;
        this.h = h; 
    }

    public int area() {
        return w * h;
    }

    public boolean sameArea(Rect other) {
        return this.area() == other.area();
    }

    public static void main(final String[] args) {
        java.util.Random rand = new java.util.Random();
        int sameArea = 0;
        for (int i = 0; i < 100_000_000; i++) {
            Rect r1 = new Rect(rand.nextInt(5), rand.nextInt(5));
            Rect r2 = new Rect(rand.nextInt(5), rand.nextInt(5));

            if (r1.sameArea(r2)) {
                sameArea++;
            } 
        }

        System.out.println("Same area: " + sameArea);
    }
}
```

这段代码创建了一亿对随机大小的矩形，并去计算有多少对是大小一样的。每次迭代都会创建一对新的矩形。你可能会认为main方法里会创建2亿个Rect对象：一亿个r1，一亿个r2。

不过，如果某个对象只是在方法内部创建并使用的话——也就是说，它不会传递到另一个方法中或者作为返回值返回——那么运行时程序就还能做得更聪明一些。你可以说这个对象是没有逃逸出去的，因此运行时（其实就是JIT编译器）做的这个分析又叫做逃逸分析。

如果一个对象没有逃逸出去，那也就是说JVM可以针对这个对象做一些类似“栈自动分配”的事情。在这个例子当中，这个对象不会从堆上分配空间，因此它也不需要垃圾回收器来回收。一旦使用这个“栈分配（stack-allocated）”对象的方法返回了，这个对象所占用的内存也就自动被释放掉了。

事实上，HotSpot VM的C2编译器做的事情要比栈分配要复杂得多。我们现在就来看一下。

在HotSpot VM的源码中，可以看到逃逸分析系统是如何对对象的使用进行分类的：

```
typedef enum {
  NoEscape = 1,    // An object does not escape method or thread and it is
                    // not passed to call. It could be replaced with scalar.

  ArgEscape = 2,  // An object does not escape method or thread but it is
                   // passed as argument to call or referenced by argument
                   // and it does not escape during call.
  GlobalEscape = 3 // An object escapes the method or thread.
}
```

第一类说明这个对象可以用标量来代替。这种分配消除技术叫标量替换（scalar replacement）。这意味着这个对象会被拆解成它的构成字段，这就相当于分配对象的操作变成了在方法内部创建多个局部变量。完成这个之后，另一项HotSpot VM的JIT技术会参与进来，它会将这些字段（事实上已经是局部变量了）存储到CPU的寄存器中（如果有必要就存储在栈上）。

Java平台的主要挑战是执行模型非常复杂。在上述例子中，如果只看源代码，你会认为r1对象是不会逃逸出main方法外的，但r2会作为参数传给r1的sameArea方法，因此它逃逸出了main方法外。

根据上面的分类，乍一看的话r1应该归类为NoEscape，而r2应该归为ArgEscape；不过这个结论是错误的，原因有几点。

第一，回想一下，Java中的方法调用最终会通过编译器替换为字节码invoke。它会把调用目标（也就是接收对象，注：即要调用的对象）和入参填充到栈中，然后查找到这个方法，再分发给它（也就是执行这个方法）。

这意味着接收对象也被传入了调用的方法中（它就是调用的方法里的this对象）。因此接收对象也逃逸出了当前域；在这个例子中，这意味着如果逃逸分析分析完这段Java代码，r1和r2都会归类为ArgEscape。

如果就只是这样的话，那么分配消除的使用场景就很有限了。所幸的是，HotSpot VM能做得更好。我们来仔细看一下它的字节码，看看能发现什么。

sameArea()方法很小（只有17个字节的字节码），在本例中也会被频繁调用，因此它是方法内联（method inlined）的一个理想对象。

```
public boolean sameArea(Rect);
  Code:
       0: aload_0
       1: invokevirtual #4    // Method area:()I
       4: aload_1
       5: invokevirtual #4    // Method area:()I
       8: if_icmpne     15
      11: iconst_1
      12: goto          16
      15: iconst_0
      16: ireturn
```

这个方法又调用了两次area()方法（这个也是可以内联的）:

```
public int area();
  Code:
     0: aload_0
     1: getfield      #2    // Field w:I
     4: aload_0
     5: getfield      #3    // Field h:I
     8: imul
     9: ireturn
```

通过JITWatch或者PrintCompilation可以看到，area()方法的调用的确被内联进了调用方sameArea()方法里，而sameArea()又被内联到了main()方法的循环体中。JITWatch为内联方法提供了一个很方便的图形化展示（如图一所示）。

![图一](https://deepinmind.oss-cn-beijing.aliyuncs.com/2018-03-EscapeAnalysis-Evans-Figure1.png)

请记住Java HotSpot VM的JIT编译器的优化顺序也是很重要的。方法内联是最早的优化，也被称为网关优化（gateway optimization），因为它首先把相关联的代码都聚合在了一起，为其它优化打开了大门。

现在sameArea()方法和area()方法都被内联进来了，方法域的问题不复存在，所有的变量都只在main方法的作用域内了。也就是说逃逸分析不会再把r1和r2视作ArgEscape类型：方法内联之后，它们现在都被归类为NoEscape。

这个结果看起来可能有悖常理，不过你需要记住的是JIT编译器并不是通过原始代码来进行优化的。如果不知道这点，就搞不清楚哪些情况能够进行逃逸分析。

前面的例子中，这些对象的分配都不会在堆上进行了，会把它们的字段拆解成独立的值。寄存器分配器通常会把拆解出来的字段直接放到寄存器中，不过如果没有足够可用的寄存器，那剩下的字段会被存储到栈上。这种情况被称为栈溢出（stack spill，注：和stack overflow不同）。

在逃逸分析开启和关闭的模式下分别运行这个程序，再观察下GC的活动，你就能看到密集循环中堆分配消除的巨大威力。

在现代JVM中逃逸分析是默认开启的，得通过JVM参数-XX:-DoEscapeAnalysis来关掉它。

下面是开启了逃逸分析之后的GC日志（一些细节删除了）：

```
java -XX:+PrintGCDetails Rect
Same area: 18073993
Heap
 PSYoungGen      total 95744K, used 13462K
  eden space 82432K, 16% used
  from space 13312K, 0% used
  to   space 13312K, 0% used
 ParOldGen       total 218624K, used 0K
  object space 218624K, 0% used
 Metaspace       used 2664K, capacity 4490K, committed 4864K, reserved 1056768K
  class space    used 286K, capacity 386K, committed 512K, reserved 1048576K
```

从日志中可以看到根本没有发生GC事件——只是在进程退出时往日志里记录了下堆的摘要信息。如果再看下关闭逃逸分析后的运行日志，情况就截然不同了：

```
java -XX:+PrintGCDetails -XX:-DoEscapeAnalysis Rect
[GC (Allocation Failure) [PSYoungGen: 82432K->480K(95744K)] 82432K->488K(314368K),
0.0008348 secs] [Times: user=0.01 sys=0.00, real=0.00 secs]
[GC (Allocation Failure) [PSYoungGen: 82912K->464K(95744K)] 82920K->480K(314368K),
0.0007404 secs] [Times: user=0.00 sys=0.00, real=0.01 secs]
[Many minor GC collections]
[GC (Allocation Failure) [PSYoungGen: 56352K->0K(55808K)] 56720K->368K(274432K),
0.0004405 secs] [Times: user=0.00 sys=0.01, real=0.00 secs]
[GC (Allocation Failure) [PSYoungGen: 55296K->0K(54784K)] 55664K->368K(273408K),
0.0004537 secs] [Times: user=0.00 sys=0.00, real=0.00 secs]
Same area: 18080278
Heap
 PSYoungGen      total 54784K, used 46674K
  eden space 54272K, 86% used
  from space 512K, 0% used
  to   space 512K, 0% used
 ParOldGen       total 218624K, used 368K
  object space 218624K, 0% used
 Metaspace       used 2665K, capacity 4490K, committed 4864K, reserved 1056768K
  class space    used 286K, capacity 386K, committed 512K, reserved 1048576K
```

这里可以很清楚地看到，由于Eden区空间满了，导致了内存分配失败、需要进行垃圾回收，因此触发了GC事件。

### 结论

逃逸分析是Java HotSpot VM引入的一项非常有用的升级。这项功能仍在开发阶段时，实际测试中它带来的性能提升就有3%到6%。

对于那些对平台特性的实现过程和原理感兴趣的开发人员来说，逃逸分析有个很有意思的特点：这项特性依赖于其它优化（自动内联），不然用处不大。

JVM底层的实现和源代码可以在HotSpot VM的源码opto/escape.hpp中找到。它是1999年11月由Jong-Deok Choi，Manish Gupta，Mauricio Serrano，Vugranam C. Sreedhar和Sam Midkif在[ACM SIGPLAN](https://www.sigplan.org/)的OOPSLA（面向对象编程，系统，语言和应用程序）会议中提出的“Escape Analysis for Java”算法的一个变种实现。

除了分配消除，Java HotSpot VM中还有几项优化技术也是基于类似的作用域分析的技术来实现的。这些优化主要用于Java为每个对象提供的内部锁上。下期文章我们会来讨论下这些优化技术。

[英文原文链接](http://www.javamagazine.mozaicreader.com/MayJune2018/Default/74/0/3978350)