# Java Concurrency代码实例之一执行者与线程池

[![Alex Wang](https://pic4.zhimg.com/7b8e72c144e581881f769b179b98b309_xs.jpg)](https://www.zhihu.com/people/wang-du-du-43-1)

[Alex Wang](https://www.zhihu.com/people/wang-du-du-43-1)

高级工程师，Coder，Teamleader

128 人赞同了该文章

本文的读者应该是已经掌握了基本的Java多线程开发技巧，但不熟悉Java Concurrency包的程序员。
Concurrency包中提供的工具众多，用法各异，熟练掌握后大有裨益。本文对包中的各种工具类从概念和用法上进行了分类，并给出了具体的样例代码。

# 1. 前言

在JDK1.4之前，Java多线程工具仅有Runnable、Thread、Timer以及synchronize关键字等寥寥无几的几个工具。随着多核处理器的普遍应用，Java并发的作用越来越重要，因此自JDK1.5后，Java参考了操作系统以及其他编程语言的并发理念，发明了许多的概念、方法和算法，并提供了相关的工具。这些工具极大的提高了Java并发编程的可靠性、安全性和性能，成为Java程序员必须掌握的利器之一。

# 2. Concurrency包的分类

按照用途与特性，Concurrency包中包含的工具被分为六类（外加一个工具类TimeUnit），即：
1. 执行者与线程池
2. 并发队列
3. 同步工具
4. 并发集合
5. 锁
6. 原子变量
本文介绍的就是第一类，执行者与线程池。

![img](https://pic1.zhimg.com/80/v2-e11a5c34827a48bb00035a7937978df0_hd.png)



# 3. 执行者Executor的由来

在介绍具体的工具之前，先讲讲设计者的思路。在Java1.4之前，已经提供了Runnable接口、Thread类、Timer类和synchronize关键字，它们已经足以完成各种各样的多线程编程任务，为什么还要提供执行者这样的概念呢？这是因为Java的设计者想把线程的创建、执行和调度分离。在Concurrency包出现之前，线程的创建基本上靠new一个Thread对象，执行靠start()方法，而线程的调度则完全依赖程序员在具体代码中自己写出来。
而Concurrency包出现之后，线程的创建还是依靠Thread、Runnable和Callable（新加入）对象的实例化；而线程的执行则靠Executor、ExecutorService的对象执行execute()方法或submit()方法；线程的调度则被固化为几个具体的线程池类，如ThreadPoolExecutor、ScheduledThreadPoolExecutor、ExecutorCompletionService等等。这样表面上增加了复杂度，而实际上成功将线程的创建、执行和调度的业务逻辑分离，使程序员能够将精力集中在线程中业务逻辑的编写，大大提高了编码效率，降低了出错的概率，而且大大提高了性能。

# 4. 工具介绍

## 4.1 线程执行者

这个功能主要由三个接口和类提供，分别是：
Executor：执行者接口，所有执行者的父类；
ExecutorService：执行者服务接口，具体的执行者类都继承自此接口；
Executors：执行者工具类，大部分执行者的实例以及线程池都由它的工厂方法创建。
先看一个例子：

```text
public class ExecutorExam {
    public static void main(String[] args) {
        ExecutorService service = Executors.newCachedThreadPool();
        service.execute(new Task("task1"));
        service.execute(new Task("task2"));
        service.execute(new Task("task3"));
        service.shutdown();
    }
}

class Task implements Runnable {
    private final String name;

    Task(String name) {
        this.name = name;
    }

    @Override
    public void run() {
        try {
            for (int i = 0; i < 5; i++) {
                TimeUnit.SECONDS.sleep(1);
                System.out.println(name + "-[" + i + "]");
            }
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

Executors工具类的newCachedThreadPool方法创建了一个执行者的对象，该对象是ExecutorService的实现类（后面我们会知道它是一个ThreadPoolExecutor对象）。Task是Runnable接口的实现类，代码中new出了三个Task对象，它们被提交给ExecutorService的execute方法作为参数，即三个线程被ExecutorService执行了，其调度机制隐含在执行者的具体类中。最后ExecutorService调用shutdown方法，阻止继续提交其他线程，并等待执行中的线程结束。
通过这种方式，线程的创建、执行和调度被分离了，程序员可以将精力集中在线程的内部业务中。

## 4.2 得到异步执行的结果

在Java1.4之前，如果要得到一个线程运行后产生的值，没有一套现成的机制，程序员可以通过Thread类的成员变量、程序的全局变量等方式来得到一个线程运行后产生的某个值。但是这样的话，你必须不断探测线程是否已经成功结束，或者运用同步技术来等待线程执行完成，再去获取异步执行的结果。
在Java Concurrency中，得到异步结果有了一套固定的机制，即通过Callable接口、Future接口和ExecutorService的submit方法来得到异步执行的结果，相关工具的介绍如下：
Callable：泛型接口，与Runnable接口类似，它的实例可以被另一个线程执行，内部有一个call方法，返回一个泛型变量V；
Future：泛型接口，代表依次异步执行的结果值，调用其get方法可以得到一次异步执行的结果，如果运算未完成，则阻塞直到完成；调用其cancel方法可以取消一次异步执行；
CompletionService：一种执行者，可将submit的多个任务的结果按照完成的先后顺序存入一个内部队列，然后可以使用take方法从队列中依次取出结果并移除，如果调用take时计算未完成则会阻塞。
先看一个简单的例子，得到一个异步执行的整形值：

```text
public class CallableExam {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        ExecutorService service = Executors.newCachedThreadPool();
        Future<Integer> future = service.submit(new Callable<Integer>() {
            @Override
            public Integer call() throws Exception {
                System.out.println("Callable is running");
                TimeUnit.SECONDS.sleep(2);
                return 47;
            }
        });
        service.shutdown();
        System.out.println("future.get = " + future.get());
    }
}
```

接下来是一个使用CompletionService的例子，创建5个线程计算一些值，执行完成后使用CompletionService依次取出结果并打印：

```text
public class CompletionServiceExam {
    public static void main(String[] args) throws InterruptedException, ExecutionException {
        ExecutorService service = Executors.newCachedThreadPool();
        CompletionService<Integer> completionService = new ExecutorCompletionService<>(service);
        for (int i = 0; i < 5; i++) {
            completionService.submit(new TaskInteger(i));
        }
        service.shutdown();
        //will block
        for (int i = 0; i < 5; i++) {
            Future<Integer> future = completionService.take();
            System.out.println(future.get());
        }

    }
}

class TaskInteger implements Callable<Integer> {
    private final int sum;

    TaskInteger(int sum)  {
        this.sum = sum;
    }

    @Override
    public Integer call() throws Exception {
        TimeUnit.SECONDS.sleep(sum);
        return sum * sum;
    }
}
```

需要注意的是CompletionService的创建方法，它的构造函数需要一个ExecutorService的对象作为参数。

## 4.3 重复执行和延期执行

在Java1.4之前，一般使用Timer来重复或者延期执行任务。Java Concurrency为了使之与Executor理念协调，引入了ScheduledExecutorService来完成同样的工作。
ScheduledExecutorService：另一种执行者，可以将提交的任务延期执行，也可以将提交的任务反复执行。
ScheduledFuture：与Future接口类似，代表一个被调度执行的异步任务的返回值。
下面的例子中ScheduledExecutorService的实例scheduler调度了两个任务，第一个任务使用scheduleAtFixedRate()方法每隔一秒重复打印“beep”，第二个任务使用schedule()方法在10秒后延迟执行，它的作用是取消第一个任务，代码如下：

```text
public class ScheduledExecutorServiceExam {
    public static void main(String[] args) {
        ScheduledExecutorService scheduler = new ScheduledThreadPoolExecutor(2);
        ScheduledFuture<?> scheduledFuture = scheduler.scheduleAtFixedRate(new Runnable() {
            @Override
            public void run() {
                System.out.println("beep");
            }
        }, 1, 1, TimeUnit.SECONDS);

        scheduler.schedule(new Runnable() {
            @Override
            public void run() {
                System.out.println("cancel beep");
                scheduledFuture.cancel(true);
                scheduler.shutdown();
            }
        }, 10, TimeUnit.SECONDS);
    }
}
```

## 4.4 TimeUnit

上面的例子中用到了TimeUnit，因此这里就先介绍一下。TimeUnit是Java Concurrency包引入的新式的表达时间间隔或延迟的单位。在JDK1.5后面引入的新类中，都使用TimeUnit作为时间的表达方式。例如：

```text
lock.tryLock(50L, TimeUnit.MILLISECONDS)
public ScheduledFuture<?> schedule(Runnable command,                                       long delay, TimeUnit unit);
```

还有，使用最多的，替代Thread.sleep的这种用法：

```text
TimeUnit.SECONDS.sleep(5);
TimeUnit有以下6个时间单位：
NANOSECONDS：纳秒，1000纳秒为一微秒
MICROSECONDS：微秒，1000微秒为一毫秒
MILLISECONDS：毫秒，1000毫秒为一秒
SECONDS：秒，60秒为1分钟
MINUTES：分钟，60分钟为1小时
HOURS：小时，24小时为1天
DAYS：天
```

原来Java的时间单位默认为毫秒，引入TimeUnit后增加了纳秒和微秒，精度更高了，同时引入了很多转换方法，便于使用。

## 4.5 线程池

在前面的章节中我们已经多次使用了ExecutorService接口的对象，它的具体实现类主要有两个，分别是ThreadPoolExecutor和ScheduledExecutorService，它们都是某种线程池。
在JDK1.8中，按照线程池的创建方法来看，应该有五种线程池，它们的创建方法如下所示：

```text
ExecutorService singleThreadPool = Executors.newSingleThreadExecutor();
ExecutorService fixedThreadPool = Executors.newFixedThreadPool(5);
ExecutorService cachedThreadPool = Executors.newCachedThreadPool();
ScheduledExecutorService singleThreadScheduledPool = Executors.newSingleThreadScheduledExecutor();
ScheduledExecutorService scheduledPool = Executors.newScheduledThreadPool(5);
```

而进一步查看源代码，这些方法最终都调用了ThreadPoolExecutor和ScheduledExecutorService的构造函数。而ScheduledExecutorService继承自ThreadPoolExecutor，因此最终所有线程池的构造函数都调用了ThreadPoolExecutor的如下构造函数：

```text
public ThreadPoolExecutor(int corePoolSize,
                          int maximumPoolSize,
                          long keepAliveTime,
                          TimeUnit unit,
                          BlockingQueue<Runnable> workQueue) 
```

**请大家注意这五个参数（重点）**：
第一个参数corePoolSize，指明了线程池中应该保持的线程数量，即使线程处于空闲状态，除非设置了allowCoreThreadTimeOut这个参数；
第二个参数maximumPoolSize，线程池中允许的最大线程数，线程池中的线程一旦到达这个数，后续任务就会等待池中的线程空闲，而不会去创建新的线程了；
第三个参数keepAliveTime，当池中线程数量大于corePoolSize时，多出的线程在空闲时能够生存的最大时间，若一个线程空闲超过这个时间，它就会被终止并从池中删除；
第四个参数unit，指示第三个参数的时间单位；
第五个参数workQueue，存储待执行任务的阻塞队列，这些任务必须是Runnable的对象（如果是Callable对象，会在submit内部转换为Runnable对象）。
弄明白以上概念后，再来看这五种线程池：
**单线程池**：newSingleThreadExecutor()方法创建，五个参数分别是ThreadPoolExecutor(1, 1, 0L, TimeUnit.MILLISECONDS, new LinkedBlockingQueue())。含义是池中保持一个线程，最多也只有一个线程，也就是说这个线程池是顺序执行任务的，多余的任务就在队列中排队。
**固定线程池**：newFixedThreadPool(nThreads)方法创建，五个参数分别是ThreadPoolExecutor(nThreads, nThreads, 0L, TimeUnit.MILLISECONDS, new LinkedBlockingQueue())。含义是池中保持nThreads个线程，最多也只有nThreads个线程，多余的任务也在队列中排队。
**缓存线程池**：newCachedThreadPool()创建，五个参数分别是ThreadPoolExecutor(0, Integer.MAX_VALUE, 60L, TimeUnit.SECONDS, new SynchronousQueue())。含义是池中不保持固定数量的线程，随需创建，最多可以创建Integer.MAX_VALUE个线程（说一句，这个数量已经大大超过目前任何操作系统允许的线程数了），空闲的线程最多保持60秒，多余的任务在SynchronousQueue（所有阻塞、并发队列在后续文章中具体介绍）中等待。
**单线程调度线程池**：newSingleThreadScheduledExecutor()创建，五个参数分别是 (1, Integer.MAX_VALUE, 0, NANOSECONDS, new DelayedWorkQueue())。含义是池中保持1个线程，多余的任务在DelayedWorkQueue中等待。
**固定调度线程池**：newScheduledThreadPool(n)创建，五个参数分别是 (n, Integer.MAX_VALUE, 0, NANOSECONDS, new DelayedWorkQueue())。含义是池中保持n个线程，多余的任务在DelayedWorkQueue中等待。
先看第一个例子，测试单线程池、固定线程池和缓存线程池（注意增加和取消注释）：

```text
public class ThreadPoolExam {
    public static void main(String[] args) {
        //first test for singleThreadPool
        ExecutorService pool = Executors.newSingleThreadExecutor();
        //second test for fixedThreadPool
//        ExecutorService pool = Executors.newFixedThreadPool(2);
        //third test for cachedThreadPool
//        ExecutorService pool = Executors.newCachedThreadPool();
        for (int i = 0; i < 5; i++) {
            pool.execute(new TaskInPool(i));
        }
        pool.shutdown();
    }
}

class TaskInPool implements Runnable {
private final int id;

    TaskInPool(int id) {
        this.id = id;
    }

    @Override
    public void run() {
        try {
            for (int i = 0; i < 5; i++) {
                System.out.println("TaskInPool-["+id+"] is running phase-"+i);
                TimeUnit.SECONDS.sleep(1);
            }
            System.out.println("TaskInPool-["+id+"] is over");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

从运行结果可以看出，单线程池中的线程是顺序执行的。固定线程池（参数为2）中，永远最多只有两个线程并发执行。缓存线程池中，所有线程都并发执行。
第二个例子，测试单线程调度线程池和固定调度线程池。

```text
public class ScheduledThreadPoolExam {
    public static void main(String[] args) {
        //first test for singleThreadScheduledPool
        ScheduledExecutorService scheduledPool = Executors.newSingleThreadScheduledExecutor();
        //second test for scheduledThreadPool
//        ScheduledExecutorService scheduledPool = Executors.newScheduledThreadPool(2);
        for (int i = 0; i < 5; i++) {
            scheduledPool.schedule(new TaskInScheduledPool(i), 0, TimeUnit.SECONDS);
        }
        scheduledPool.shutdown();
    }
}

class TaskInScheduledPool implements Runnable {
    private final int id;

    TaskInScheduledPool(int id) {
        this.id = id;
    }

    @Override
    public void run() {
        try {
            for (int i = 0; i < 5; i++) {
                System.out.println("TaskInScheduledPool-["+id+"] is running phase-"+i);
                TimeUnit.SECONDS.sleep(1);
            }
            System.out.println("TaskInScheduledPool-["+id+"] is over");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

从运行结果可以看出，单线程调度线程池和单线程池类似，而固定调度线程池和固定线程池类似。
总结：如果没有特殊要求，使用缓存线程池总是合适的；如果只能运行固定数量的线程，就使用固定线程池；如果只能运行一个线程，就使用单线程池。如果要运行调度任务，则按需使用调度线程池或单线程调度线程池。如果有其他特殊要求，则可以直接使用ThreadPoolExecutor类的构造函数来创建线程池，并自己给定那五个参数。

# 5. Fork-Join框架

在JDK1.7引入了一种新的并行编程模式“fork-join”，它是实现了“分而治之”思想的Java并发编程框架。网上关于此框架的各种介绍很多，本文从框架特点出发，通过几个例子来进行实用性的介绍。

## 5.1 fork-join框架的特点

fork-join框架对新手来说很难理解，因此我先从它的特点说起，它有几个特点：
1.它对问题的解决思路是分而治之，先将一个问题fork（分为）几个子问题，然后子问题又分为孙子问题，直至细分为一个容易计算的问题，然后再将结果依次join(结合)为最终的答案。是不是感觉和云计算中的Map-reduce计算模型很像？思路是一样的，只不过fork-join运行在一个JVM中的多个线程内，而map-reduce运行在分布式计算节点上。
2.在运行线程时，它使用“work-steal”（任务偷取）算法。一般来说，fork-join会启动多个线程（由参数指定，若不指定则默认为CPU核心数量），每个线程负责一个任务队列，并依次从队列头部获得任务并执行。当某个线程空闲时，它会从其他线程的任务队列尾部偷取一个任务来执行，这样就保证了线程的运行效率达到最高。
3.它面向的问题域是可以大量并行执行的计算任务，例如计算某个大型数组中每个元素的平方（当然这个有些无趣），其计算对象最好是一些独立的元素，不会被其他线程访问，也没有同步、互斥要求，更不要涉及IO或者无限循环。当然此框架也可以执行普通的并发编程任务，但是这时就失去了性能优势。
4.细分的计算任务有一个粗略的优化标准，即可以在100~10000条指令中执行完毕。
了解以上思路后，来看看fork-join框架提供的几个工具类：
ForkJoinPool：支持fork-join框架的线程池，所有ForkJoinTask任务都必须在其中运行，线程池主要使用invoke()、invokeAll()等方法来执行任务，当然也可以使用原有的execute()和submit()方法；
ForkJoinTask：支持fork-join框架的任务抽象类，它是Future接口，它代表一个支持fork()和join()方法的任务；
RecursiveAction：ForkJoinTask的两个具体子类之一，代表没有返回值的ForkJoinTask任务；
RecursiveTask：ForkJoinTask的两个具体子类之一，代表有返回值的ForkJoinTask任务。

## 5.2 RecursiveAction

先来看一个使用RecursiveAction的例子，这段代码的目的是计算一个大型数组中每个元素x的一个公式的值，这个公式是sin(x)+cos(x)+tan(x)：

```text
public class RecursiveActionExam {
    private final static int NUMBER = 10000000;

    public static void main(String[] args) {
        double[] array = new double[NUMBER];
        for (int i = 0; i < NUMBER; i++) {
            array[i] = i;
        }
        long startTime = System.currentTimeMillis();
        System.out.println(Runtime.getRuntime().availableProcessors());
        ForkJoinPool forkJoinPool = new ForkJoinPool();
        forkJoinPool.invoke(new ComputeTask(array, 0, array.length));
        long endTime = System.currentTimeMillis();
        System.out.println("Time span = " + (endTime - startTime));
    }
}

class ComputeTask extends RecursiveAction {
    final double[] array;
    final int lo, hi;

    ComputeTask(double[] array, int lo, int hi) {
        this.array = array;
        this.lo = lo;
        this.hi = hi;
    }

    protected void compute() {
        if (hi - lo < 2) {
            for (int i = lo; i < hi; ++i)
                array[i] = Math.sin(array[i]) + Math.cos(array[i]) + Math.tan(array[i]);
        } else {
            int mid = (lo + hi) >>> 1;
            invokeAll(new ComputeTask(array, lo, mid),
                    new ComputeTask(array, mid, hi));
        }
    }
}
```

代码还是比较简单的，首先创建一个ForkJoinPool，然后new一个ComputeTask对象丢到线程池中运行。ComputeTask继承自RecursiveAction，实现了其compute()方法。这个方法中，当上界和下界的差小于一个值（这里是2）时，直接计算；否则创建两个子任务，并丢到线程池中。最值得注意的是compute()方法，这个方法里面体现了“分而治之”的思想，对程序员来说，叫递归思想更加合适。只不过普通的递归是在单线程中完成的，而这里的递归则把递归任务通过invokeAll()方法丢进了线程池中，让线程池来调度执行。运行结果是Time span = 3798。
再看看单线程的情况：

```text
public class RecursiveSequenceExam {
    private final static int NUMBER = 10000000;

    public static void main(String[] args) {
        double[] array = new double[NUMBER];
        for (int i = 0; i < NUMBER; i++) {
            array[i] = i;
        }

        long startTime = System.currentTimeMillis();
        for (int i = 0; i < NUMBER; i++) {
            array[i] = Math.sin(array[i]) + Math.cos(array[i]) + Math.tan(array[i]);
        }
        long endTime = System.currentTimeMillis();
        System.out.println("Time span = " + (endTime - startTime));
    }
}
```

运行结果是Time span = 9354。
由于我的CPU是4核的，再看看4线程的情况：

```text
public class Recusive4ThreadExam {
    private final static int NUMBER = 10000000;

    public static void main(String[] args) throws InterruptedException {
        double[] array = new double[NUMBER];
        for (int i = 0; i < NUMBER; i++) {
            array[i] = i;
        }

        long startTime = System.currentTimeMillis();
        ExecutorService service = Executors.newFixedThreadPool(4);
        service.execute(new ArrayTask(array, 0, NUMBER / 4));
        service.execute(new ArrayTask(array, NUMBER / 4, NUMBER / 2));
        service.execute(new ArrayTask(array, NUMBER / 2, NUMBER*3 / 4));
        service.execute(new ArrayTask(array, NUMBER*3 / 4, NUMBER ));
        service.shutdown();
        service.awaitTermination(1,TimeUnit.DAYS);
        long endTime = System.currentTimeMillis();
        System.out.println("Time span = " + (endTime - startTime));

    }
}

class ArrayTask implements Runnable {
    final double[] array;
    final int lo, hi;

    ArrayTask(double[] array, int lo, int hi) {
        this.array = array;
        this.lo = lo;
        this.hi = hi;
    }

    @Override
    public void run() {
        for (int i = lo; i < hi; ++i)
            array[i] = Math.sin(array[i]) + Math.cos(array[i]) + Math.tan(array[i]);
    }
}
```

运行结果是Time span = 4064。可以看出由于fork-join框架采用了任务偷取算法，比普通4线程快了一点点。

## 5.3 RecursiveTask

下面来看一个更有意义的场景，寻找一个大型数组的最小值，这里我使用RecursiveTask（其实使用RecursiveAction也行，在它内部用一个成员变量保存结果即可）。代码如下：

```text
public class RecursiveFindMax {
    private static Random rand = new Random(47);
    private static final int NUMBER = 1000000;

    public static void main(String[] args) {
        double[] array = new double[NUMBER];
        for (int i = 0; i < NUMBER; i++) {
            array[i] = rand.nextDouble();
        }

        ForkJoinPool pool = new ForkJoinPool();
        TaskFindMax task = new TaskFindMax(0, array.length - 1, array);
        pool.invoke(task);
        System.out.println("MaxValue = " + task.join());
    }
}

class TaskFindMax extends RecursiveTask<Double> {
    private final int lo;
    private final int hi;
    private final double[] array;
    //you can change THRESHOLD to get better efficiency
    private final static int THRESHOLD = 10;

    TaskFindMax(int lo, int hi, double[] array) {
        this.lo = lo;
        this.hi = hi;
        this.array = array;
    }

    @Override
    protected Double compute() {
        if ((hi - lo) < THRESHOLD) {
            double max = array[lo];
            for (int i = lo; i < hi; i++) {
                max = Math.max(max, array[i + 1]);
            }
            return max;
        } else {
            int mid = (lo + hi) >>> 1;
            TaskFindMax lhs = new TaskFindMax(lo, mid, array);
            TaskFindMax rhs = new TaskFindMax(mid, hi, array);
            invokeAll(lhs, rhs);
            return Math.max(lhs.join(), rhs.join());
        }
    }
}
```

pool.invoke(task)将一个最初的任务扔进了线程池执行，这个任务将会执行它的compute()方法。在此方法中，若满足某个条件（例如数组上界和下界只差小于阈值THRESHOLD）则直接在这一段数组中查找最大值；若不满足条件，则找出中值mid，然后new出两个子任务lhs(left hand side)和rhs(right hand side)，并调用invokeAll(lhs, rhs)将这两个子任务都扔进线程池执行。任务的join()方法会得到返回值，若任务尚未执行完毕则会在此阻塞。
通过这种编程模式，很好的将递归思想用到了多线程领域。值得注意的是，通过调整THRESHOLD可以增加或减少任务的个数，从而极大的影响线程的执行。在很多情况下，使用fork-join框架并不会比普通的多线程效率更高，甚至比单线程运行效率更低。因此，必须找到适合的场景，然后进行多次调优，才能获得性能的改进。

# 6. 小结

本来准备在一篇文章中将Concurrency包中所有内容都介绍完，刚刚写了一个开头就知道自己过于自大了，因此本系统将分为六篇文章。
执行者与线程池的引入是因为Concurrency包的设计者想将线程的创建、执行和调度分离，从而使得用户能够更加专注于业务逻辑；Callable接口和Future接口使得异步执行结果的获取更加简单；ScheduledExecutorService取代Timer成为了线程重复和延迟执行的新标准；TimeUnit类的引入简化了时间段的表达工作；包中提供的五种线程池可以极大的满足程序员的各种需求，极端情况下还可以利用ThreadPoolExecutor类自己定制线程池。最后，从JDK1.7后引入的Fork-Join框架将“分而治之”的递归思想实现到线程池中，并应用“work-steal”算法实现了任务执行效率的提升。

编辑于 2017-05-04