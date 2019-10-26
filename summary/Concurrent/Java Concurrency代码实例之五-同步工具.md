# Java Concurrency代码实例之五-同步工具

[![Alex Wang](https://pic4.zhimg.com/7b8e72c144e581881f769b179b98b309_xs.jpg)](https://www.zhihu.com/people/wang-du-du-43-1)

[Alex Wang](https://www.zhihu.com/people/wang-du-du-43-1)

高级工程师，Coder，Teamleader

26 人赞同了该文章

本文的读者应该是已经掌握了基本的Java多线程开发技巧，但不熟悉Java Concurrency包的程序员。本文是本系列的第五篇文章，前四篇文章请看这里：

https://zhuanlan.zhihu.com/p/26724352

https://zhuanlan.zhihu.com/p/27148381

https://zhuanlan.zhihu.com/p/27338395

https://zhuanlan.zhihu.com/p/27546231

## 1. 前言

按照用途与特性，Concurrency包中包含的工具被分为六类（外加一个工具类TimeUnit），即： 1. 执行者与线程池 2. 并发队列 3. 同步工具 4. 并发集合 5. 锁 6. 原子变量 本文介绍的是其中的同步工具，这些同步工具均以上一篇文章(https://zhuanlan.zhihu.com/p/27546231)中讲到的AQS（AbstractQueuedSynchronizer）以及锁为基础，构造了各种各样适用于各个场景的同步器，提供了灵活多变的同步性。在JDK1.7中，同步工具主要包括CountDownLatch（一次性栅栏）、Semaphore（信号量）、CyclicBarrier（循环同步栅栏）、Exchanger（线程间交换器）和Phaser。下面的篇幅中，将依次讲述每种同步工具的概念、用法和原理。

## 2. CountDownLatch一次性栅栏

## 2.1 概念与用法

CountDownLatch是一个用来同步多个线程的并发工具，n个线程启动后，分别调用CountDownLatch的await方法来等待其m个条件满足（m在初始化时指定）；每当有条件满足时，当前线程调用CountDownLatch的countDown方法，使得其m值减1；直至m值为0时，所有等待的线程被唤醒，继续执行。注意，CountDownLatch是一次性的，当条件满足后，它不能再回到初始状态，也不能阻止后续线程了。若要循环的阻塞多个线程，则考虑使用CyclicBarrier。 例如5匹马参加赛马比赛，需等待3个裁判到位后才能启动，代码如下：

```java
public class CountDownLatchExam {
    public static void main(String[] args) {
        CountDownLatch latch = new CountDownLatch(3);
        ExecutorService service = Executors.newCachedThreadPool();
        for (int i = 0; i < 5; i++) {
            service.submit(new Horse("horse" + i, latch));
        }
        for (int i = 0; i < 3; i++) {
            service.submit(new Judge("judge" + i, latch));
        }
        service.shutdown();
    }


    private static class Horse implements Runnable {
        private final String name;
        private final CountDownLatch latch;

        Horse(String name, CountDownLatch latch) {
            this.name = name;
            this.latch = latch;
        }

        @Override
        public void run() {
            try {
                System.out.println(name + " is ready,wait for all judges.");
                latch.await();
                System.out.println(name + " is running.");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    private static class Judge implements Runnable {
        private final String name;
        private final CountDownLatch latch;
        private static Random random = new Random(System.currentTimeMillis());

        Judge(String name, CountDownLatch latch) {
            this.name = name;
            this.latch = latch;
        }

        @Override
        public void run() {
            try {
                TimeUnit.SECONDS.sleep(random.nextInt(5));
                System.out.println(name + " is ready.");
                latch.countDown();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

## 2.2 原理

CountDownLatch的原理在上一篇的4.7节“一次唤醒所有阻塞线程的共享锁”中已经详细阐述了。简要复述一下，CountDownLatch使用AQS的子类Sync作为内部的同步器，并由Sync复写了AQS的tryAcquireShared和tryReleaseShared方法。它将AQS中的state当做需要满足的条件个数，生成了一个共享锁。每当调用await方法时，内部调用了tryAcquireShared方法，由于state>0，因此调用的线程会阻塞在共享锁的循环框架中。每当调用countDown方法时，内部调用了releaseShared方法，而此方法将会把state的值减1，当state的值为0时，tryAcquireShared中的循环将会唤醒所有等待线程，使之继续运行。由于tryAcquireShared方法中没有修改state值，因此CountDownLatch只能一次性使用，不能循环使用。 若需知道更多细节，请直接阅读CountDownLatch和AQS的源代码。提醒一句，CountDownLatch的源代码是所有AQS的应用中最简单的，应当从它读起。

## 3. Semaphore信号量

## 3.1 概念与用法

Semaphore信号量，在多个任务争夺几个有限的共享资源时使用。调用acquire方法获取一个许可，成功获取的线程继续执行，否则就阻塞；调用release方法释放一个许可。每当有空余的许可时，阻塞的线程和其他线程可竞争许可。 下面的例子中，10辆车竞争3个许可证，有了许可证的车就可以入内访问资源，访问完成后释放许可证：

```java
public class SemaphoreExam {
    public static void main(String[] args) {
        Semaphore semaphore = new Semaphore(3);
        ExecutorService service = Executors.newCachedThreadPool();
        // 10 cars wait for 3 semaphore
        for (int i = 0; i < 10; i++) {
            service.submit(new Car("Car" + i, semaphore));
        }

        service.shutdown();
    }
    private static class Car implements Runnable {
        private final String name;
        private final Semaphore semaphore;
        private static Random random = new Random(System.currentTimeMillis());

        Car(String name, Semaphore semaphore) {
            this.name = name;
            this.semaphore = semaphore;
        }

        @Override
        public void run() {
            try {
                System.out.println(name + " is waiting for a permit");
                semaphore.acquire();
                System.out.println(name+" get a permit to access, available permits:"+semaphore.availablePermits());
                TimeUnit.SECONDS.sleep(random.nextInt(5));
                System.out.println(name + " release a permit, available permits:"+semaphore.availablePermits());
                semaphore.release();
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

注意，运行时semaphore.availablePermits()方法会返回当前空余的许可证数量。但由于线程获取许可证的速度往往快于IO的速度，因此很多时刻看到这个数字都是0。

## 3.2 原理

Semaphore的原理在上一篇的4.8节“拥有多个许可证的共享锁”中已经详细阐述了。简要复述一下，Semaphore使用AQS的子类Sync作为内部的同步器，并由Sync复写了AQS的tryAcquireShared和tryReleaseShared方法。它将AQS中的state当做许可证的个数，生成了一个共享锁。state的值在Semaphore的构造函数中指定，必须大于0。每当调用acquire方法时，内部调用了tryAcquireShared方法，此方法检测state的值是否>0，若是则将state减1，并继续运行，否则线程就阻塞在共享锁的循环框架中。每当调用release方法时，内部调用了releaseShared方法，而此方法将会把state的值加1，当state的值大于0时，tryAcquireShared中的循环将会唤醒所有等待线程，使之继续运行，重新竞争许可证。 若需知道更多细节，请直接阅读Semaphore和AQS的源代码。

## 4. CyclicBarrier循环同步栅栏

## 4.1 概念与用法

CyclicBarrier可用来在某些栅栏点处同步多个线程，且可以多次使用，每次在栅栏点同步后，还可以激发一个事件。例如三个旅游者（线程）各自出发，依次到达三个城市，必须每个人都到达某个城市后（栅栏点），才能再次出发去向下一个城市，当他们每同步一次时，激发一个事件，输出一段文字。代码如下：

```java
public class CyclicBarrierExam {
    public static void main(String[] args) {
        CyclicBarrier barrier = new CyclicBarrier(3, new Runnable() {
            @Override
            public void run() {
                System.out.println("======== all threads have arrived at the checkpoint ===========");
            }
        });
        ExecutorService service = Executors.newFixedThreadPool(3);
        service.submit(new Traveler("Traveler1", barrier));
        service.submit(new Traveler("Traveler2", barrier));
        service.submit(new Traveler("Traveler3", barrier));
        service.shutdown();
    }
    private static class Traveler implements Runnable {
        private final String name;
        private final CyclicBarrier barrier;
        private static Random rand = new Random(47);

        Traveler(String name, CyclicBarrier barrier) {
            this.name = name;
            this.barrier = barrier;
        }

        @Override
        public void run() {
            try {
                TimeUnit.SECONDS.sleep(rand.nextInt(5));
                System.out.println(name + " arrived at Beijing.");
                barrier.await();
                TimeUnit.SECONDS.sleep(rand.nextInt(5));
                System.out.println(name + " arrived at Shanghai.");
                barrier.await();
                TimeUnit.SECONDS.sleep(rand.nextInt(5));
                System.out.println(name + " arrived at Guangzhou.");
                barrier.await();
            } catch (InterruptedException e) {
                e.printStackTrace();
            } catch (BrokenBarrierException e) {
                e.printStackTrace();
            }

        }
    }
}
```



## 4.2 原理

CyclicBarrier是依赖一个可重入锁ReentrantLock和它的一个Condition实现的，在构造时，CyclicBarrier得到了一个parties数值，它代表参与的线程数量，以及一个Runnable的实例，它代表被激发的事件。每当有线程调用await时，parties减1。若此时parties大于0，线程就在Condition处阻塞，若parties等于0，则此Condition会调用signalAll释放所有等待线程，并触发事件，同时将parties复原。因此所有的线程又进入下一轮循环。 CyclicBarrier代码非常简单，复杂之处在于它还要处理线程中断、超时等情况。

## 5. Exchange线程间变量交换

## 5.1 概念与用法

Exchange专门用于成对的线程间同步的交换一个同类型的变量，这种交换是线程安全且高效的。直接来看一个例子：

```java
public class ExchangerExam {
    public static void main(String[] args) {
        Exchanger<String> exchanger = new Exchanger<>();
        ExecutorService service = Executors.newCachedThreadPool();
        service.submit(new StringHolder("LeftHand", "LeftValue", exchanger));
        service.submit(new StringHolder("RightHand", "RightValue", exchanger));
        service.shutdown();
    }

    private static class StringHolder implements Runnable {
        private final String name;
        private final String val;
        private final Exchanger<String> exchanger;
        private static Random rand = new Random(System.currentTimeMillis());

        StringHolder(String name, String val, Exchanger<String> exchanger) {
            this.name = name;
            this.val = val;
            this.exchanger = exchanger;
        }

        @Override
        public void run() {
            try {
                System.out.println(name + " hold the val:" + val);
                TimeUnit.SECONDS.sleep(rand.nextInt(5));
                String str = exchanger.exchange(val);
                System.out.println(name + " get the val:" + str);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

可以看到，代码中两个线程同步的交换了一个String。先执行exchange方法的线程会阻塞直到后一个线程也执行了exchange方法，然后同步的完成数据的交换。再看一个例子：

```java
public class ExchangerExam2 {
    public static void main(String[] args) throws InterruptedException {
        Exchanger<String> exchanger = new Exchanger<>();
        ExecutorService service = Executors.newCachedThreadPool();
        long start = System.currentTimeMillis();
        service.submit(new StringHolder("LeftHand", "LeftValue", exchanger));
        service.submit(new StringHolder("RightHand", "RightValue", exchanger));
        service.shutdown();
        service.awaitTermination(1, TimeUnit.DAYS);
        long end = System.currentTimeMillis();
        System.out.println("time span is " + (end - start) + " milliseconds");
    }


    private static class StringHolder implements Runnable {
        private final String name;
        private final String val;
        private final Exchanger<String> exchanger;
        private static Random rand = new Random(System.currentTimeMillis());

        StringHolder(String name, String val, Exchanger<String> exchanger) {
            this.name = name;
            this.val = val;
            this.exchanger = exchanger;
        }

        @Override
        public void run() {
            try {
                for (int i = 0; i < 10000; i++) {
//                    System.out.println(name + "-" + i + ": hold the val:" + val + i);
//                    TimeUnit.NANOSECONDS.sleep(rand.nextInt(5));
                    String str = exchanger.exchange(val + i);
//                    System.out.println(name + "-" + i + ": get the val:" + str);
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

代码中，两个线程交换了10000组数据，用时仅41ms，这说明Exchanger的同步效率是非常高的。 再看一段代码：

```java
public class ExchangerExam3 {
    public static void main(String[] args) {
        Exchanger<String> exchanger = new Exchanger<>();
        ExecutorService service = Executors.newCachedThreadPool();
        service.submit(new StringHolder("North", "NorthValue", exchanger));
        service.submit(new StringHolder("East", "EastValue", exchanger));
        service.submit(new StringHolder("West", "WestValue", exchanger));
        service.submit(new StringHolder("South", "SouthValue", exchanger));
        service.shutdown();
    }

    private static class StringHolder implements Runnable {
        private final String name;
        private final String val;
        private final Exchanger<String> exchanger;
        private static Random rand = new Random(System.currentTimeMillis());

        StringHolder(String name, String val, Exchanger<String> exchanger) {
            this.name = name;
            this.val = val;
            this.exchanger = exchanger;
        }

        @Override
        public void run() {
            try {
                for (int i = 0; i < 10000; i++) {
                    System.out.println(name + "-" + i + ": hold the val:" + val + i);
                    TimeUnit.NANOSECONDS.sleep(rand.nextInt(5));
                    String str = exchanger.exchange(val + i);
                    System.out.println(name + "-" + i + ": get the val:" + str);
                }
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```



这段代码在运行时有很大的概率会死锁，原因就是Exchanger是用来在“成对”的线程之间交换数据的，像上面这样在四个线程之间交换数据，Exchanger很有可能将多个线程互相阻塞在其Slot中，造成死锁。

## 5.2 原理

Exchanger这个类初看非常简单，其公开的接口仅有一个无参构造函数，两个重载的泛型exchange方法：

```java
public V exchange(V x) throws InterruptedException
public V exchange(V x, long timeout, TimeUnit unit) throws InterruptedException, TimeoutException
```



第一个方法用来持续阻塞的交换数据；第二个方法用来在一个时间范围内交换数据，若超时则抛出TimeoutException后返回，同时唤醒另一个阻塞线程。 Exchanger的基本原理是维持一个槽（Slot），这个Slot中存储一个Node的引用，这个Node中保存了一个用来交换的Item和一个用来获取对象的洞Hole。如果一个来“占有”的线程看见Slot为null，则调用CAS方法（CAS方法在前面的文章中已经详细介绍了https://zhuanlan.zhihu.com/p/27338395）使一个Node对象占据这个Slot，并等待另一个线程前来交换。如果第二个来“填充”的线程看见Slot不为null，则调用CAS方法将其设置为null，同时使用CAS与Hole交换Item，然后唤醒等待的线程。注意所有的CAS操作都有可能失败，因此CAS必须是循环调用的。 看看JDK1.7中Exchanger的数据结构相关源代码：

```java
// AtomicReference中存储的是Hole对象
private static final class Node extends AtomicReference<Object> {
    /** 用来交换的对象. */
    public final Object item;

    /** The Thread waiting to be signalled; null until waiting. */
    public volatile Thread waiter;

    /**
     * Creates node with given item and empty hole.
     * @param item the item
     */
    public Node(Object item) {
        this.item = item;
    }
}
//Slot中存储的是Node
private static final class Slot extends AtomicReference<Object> {
    //这一行是为了防止伪共享而加入的缓冲行，与具体算法无关
long q0, q1, q2, q3, q4, q5, q6, q7, q8, q9, qa, qb, qc, qd, qe;
}
//一个Slot数组，数组中有32个Slot，只在必要时才创建
private volatile Slot[] arena = new Slot[CAPACITY];
```



下面是进行交换操作的核心算法：

```java
private Object doExchange(Object item, boolean timed, long nanos) {
    Node me = new Node(item);               // 创建一个Node，预备在“占用”时使用
    int index = hashIndex();                   // 当前Slot的哈希值
    int fails = 0;                            // CAS失败次数

    for (;;) {
        Object y;                          // 当前Slot中的内容
        Slot slot = arena[index];              //得到当前的Slot
        if (slot == null)                     // 延迟加载slots
            createSlot(index);                // 创建Slot并重入循环
        else if ((y = slot.get()) != null &&  // 如果Hole不为null，准备“填充”
                 slot.compareAndSet(y, null)) {
            Node you = (Node)y;               // 从这里开始交换数据
            if (you.compareAndSet(null, item)) {
                LockSupport.unpark(you.waiter);  //唤醒等待线程
                return you.item;                //“填充”线程从这里返回值
            }                                // 上面条件不满足，重入循环
        }
        else if (y == null &&                 // 如果Hole为null，准备“占有”
                 slot.compareAndSet(null, me)) {
            if (index == 0)                   // 在slot 0上等待交换
                return timed ?
                    awaitNanos(me, slot, nanos) :
                    await(me, slot);
            Object v = spinWait(me, slot);    // Slot位置不为0时，自旋等待交换
            if (v != CANCEL)
                return v;                 //“占有”线程从这里返回值
            me = new Node(item);              // 抛弃被取消的Node，创建新Node
            int m = max.get();
            if (m > (index >>>= 1))           // index右移1位，相当于arena中slot向右1位
                max.compareAndSet(m, m - 1);  // 缩表
        }
        else if (++fails > 1) {               // 在第一个Slot上运行两次失败
            int m = max.get();
            if (fails > 3 && m < FULL && max.compareAndSet(m, m + 1))
                index = m + 1;                // 第三次失败时index增加
            else if (--index < 0)
                index = m;                    // 当index小于0时，赋值为m
        }
    }
}
```

上述代码比前面介绍的基本原理稍微复杂了一些。主要是以下几点，首先Slot是放在一个数组arena中的，这些Slot是延迟加载的；第二，参数中有延时的参数，在超时的时候有其他的处理代码；第三，在等待时首先采用自旋，超过一定次数后再进入park；第四，引入了一个max值，它代表Slot的索引index的范围，最小为0，最大为FULL，这个值的相关代码如下：

```java
private final AtomicInteger max = new AtomicInteger();
//其中CAPACITY=32，NCPU是CPU的核心数量
private static final int FULL = Math.max(0, Math.min(CAPACITY, NCPU / 2) - 1);
```



由此可见，max值与CPU的核心数量相关，因此在多核CPU（例如目前主流服务器的CPU经常是32或者64核）上，所能使用的Slot数量多；而在PC上（CPU一般为4核），max最大是1，只能使用两个Slot。这样就最大限度的保证了Exchanger的性能。具体如下图所示：



![img](https://pic4.zhimg.com/80/v2-33061d7251faa3c7747c4b8ade323203_hd.png)



最后，要彻底弄清楚Exchanger，最好的方法是去看源代码。

## 6. Phaser灵活可重用同步栅栏

## 6.1 概念与用法

Phaser是一个灵活的可重用的同步栅栏，它的不同用法可以代替CountDownLatch和CyclicBarrier，但是比它们更加灵活。它引入了注册、注销、同步、到达、等待、结束、分层、监视等概念，可以让程序员构造出各种灵活多变的同步器。当然，理解和使用的复杂度也更高了。

## 6.1.1. 注册与注销

我们知道，在CyclicBarrier中，参与同步的“线程数”被称之为parties，在其构造函数中作为参数指定，一旦指定，则不可更改。在Phaser中，parties则是一个可以更改的数字，各个线程可以通过注册方法（register、bulkRegister）来增加parties的值；也可以通过arriveAndDeregister()来减少parties的值。注意，线程调用这些方法时仅仅在内部修改了parties的值，在Phaser的内部并没有一个登记本登记了哪个线程已经注册，因此不能查询某个线程的注册状态。

## 6.1.2. 同步、等待与到达

与CyclicBarrier类似，Phaser的主要用法也是用于一组线程在某些阶段处等待全部的线程到达。这种等待可以是一次性的，也可以是重复的，由于Phaser的注册机制，每次参与等待的线程数量也是可变的。每次等待的阶段都有一个阶段号phase number，这个phase number从0开始，每当完成一次线程同步， phase number就加1，直至Integer.MAX_VALUE，然后又从0开始。通过phase number，可以灵活的控制每次同步完成时触发的事件（该事件通过重载onAdvance(int, int)方法实现）。 当一个线程调用arrive时，表示它到达了一个阶段，并立即返回该phase number，如果Phaser已经终止，则返回一个负数。线程也可以调用arriveAndDeregister方法，表示到达且注销自己； 当一个线程调用awaitAdvance(int phase)时，表示它要等待本阶段其他线程到达，参数就是arrive返回的那个phase number。当然为了方便，可以直接调用arriveAndAwaitAdvance表示awaitAdvance(arrive())的效果。 当所有线程（满足注册数）都达到一个阶段时，所有等待的线程被解除阻塞，然后由最后到达的线程触发并执行onAdvance方法，然后所有线程继续执行。

## 6.1.3. 模拟CountDownLatch

用Phaser模拟CountDownLatch非常简单，主线程创建Phaser时，将注册数设置为1，每个子线程自己注册自己，这样n个线程就有了n+1个注册数。每个子线程在阶段处调用arriveAndAwaitAdvance等待同步，等所有子线程都到达后到达的注册数就是n；然后主线程注销自己，则满足了到达条件，所有子线程继续执行。

```java
public class PhaserExam1 {
    public static void main(String[] args) {
        //初始化时parties设置为1
        Phaser phaser = new Phaser(1);
        ExecutorService service = Executors.newCachedThreadPool();
        service.execute(new MyTask(phaser));
        service.execute(new MyTask(phaser));
        service.execute(new MyTask(phaser));
        service.shutdown();
        try {
            System.out.println("main thread sleep for 5 seconds.");
            TimeUnit.SECONDS.sleep(5);
            System.out.println("In main thread, registered parties:" + phaser.getRegisteredParties());
            System.out.println("In main thread, arrived parties:" + phaser.getArrivedParties());
            //到达并deregister，此时parties会减少至3，从而释放所有线程
            phaser.arriveAndDeregister();
            System.out.println("main thread releases all waiting threads.");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }

    private static class MyTask implements Runnable {
        final Phaser phaser;

        private MyTask(Phaser phaser) {
            this.phaser = phaser;
        }

        @Override
        public void run() {
            //每个线程register，意味着parties加1
            phaser.register();
            System.out.println(Thread.currentThread() + " is waiting for synchronization, registered parties:" + phaser.getRegisteredParties());
            //等待所有parties到达
            phaser.arriveAndAwaitAdvance();
            System.out.println(Thread.currentThread() + " is arrived, arrived parties:" + phaser.getArrivedParties());
        }
    }
}
```



当然，还有很多方法可以模拟CountDownLatch。JDK中就提供了一种，可以仔细看JDK的注释。

## 6.1.4. 模拟CyclicBarrier

模拟CyclicBarrier就要复杂一点，为了解释如何触发同步事件，需要继承Phaser并重写onArrive方法。

```java
public class PhaserExam2 {
    public static void main(String[] args) {
        //循环的次数
        final int iterations = 3;
        Phaser phaser = new Phaser(){
            @Override
            protected boolean onAdvance(int phase, int registeredParties) {
                //当phase number大于等于指定值，或者注册的parties数量等于0时，Phaser终止
                System.out.println("============== all threads arrive at phase :"+getPhase()+" ==============");
                return phase >= (iterations - 1) || registeredParties == 0;
            }
        };
        ExecutorService service = Executors.newCachedThreadPool();
        service.execute(new CyclicTask(phaser));
        service.execute(new CyclicTask(phaser));
        service.execute(new CyclicTask(phaser));
        service.shutdown();
    }

    private static class CyclicTask implements Runnable {
        static Random rand = new Random(System.currentTimeMillis());
        final Phaser phaser;
        private CyclicTask(Phaser phaser) {
            this.phaser = phaser;
        }
        @Override
        public void run() {
            phaser.register();
            try {
                do {
                    System.out.println(Thread.currentThread() + " is begin, doing some work.");
                    TimeUnit.SECONDS.sleep(rand.nextInt(5));
                    phaser.arriveAndAwaitAdvance();
                    System.out.println(Thread.currentThread() + " is over.");
                } while (!phaser.isTerminated());
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```



值得注意的一点是，可以使用isTerminated检测Phaser的终止条件。当然，模拟CyclicBarrier的方法也不止这一种，JDK的注释中就有另外一种，可供仔细研究。

## 6.1.5. 终止

如上所述，Phaser可以进入终止Termination状态，这个状态可以用isTerminated方法来检测。当进入Termination状态时，所有等待同步的线程都会立即退出，并返回一个负数。进入Termination状态有两种方法，一是onAdvance返回true；第二种则是调用forceTermination方法。一般来说，当注册的parties数量减少至0时，onAdvance就会返回true，从而进入Termination状态。下面是一段强制终止的代码。

```java
public class PhaserTermination {
    public static void main(String[] args) throws InterruptedException {
        Phaser phaser = new Phaser(1){
            @Override
            protected boolean onAdvance(int phase, int registeredParties) {
                System.out.println("Termination state");
                return super.onAdvance(phase, registeredParties);
            }
        };
        ExecutorService service= Executors.newCachedThreadPool();
        service.execute(new NeverEnd(phaser));
        service.execute(new NeverEnd(phaser));
        service.execute(new NeverEnd(phaser));
        service.shutdown();
        System.out.println("main thread wait 5 seconds");
        TimeUnit.SECONDS.sleep(5);
        System.out.println("main thread terminate the phaser");
        phaser.forceTermination();
    }

    private static class NeverEnd implements Runnable {
        final Phaser phaser;

        private NeverEnd(Phaser phaser) {
            this.phaser = phaser;
        }

        @Override
        public void run() {
                phaser.register();
                System.out.println(Thread.currentThread()+" is running , it's never end.");
                System.out.println(Thread.currentThread()+" is end, return value = "+ phaser.arriveAndAwaitAdvance());
        }
    }
}
```



## 6.1.6. 分层

原则上来说，一个Phaser可以支持Integer.MAX_VALUE个parties，但是考虑到性能问题，目前Jdk1.7中仅支持65535个parties。一个Phaser如果有大量的parties，那么线程竞争的开销会很大，导致性能降低，因此Phaser支持分层，由一个父Phaser自动控制多个子Phaser。在一个分层的Phaser体系中，子Phaser中parties的注册与注销会自动被父Phaser管理。当一个子Phaser的parties降低到0时，它自动从父Phaser中注销，当一个子Phaser的parties上升到大于0时，它自动在Phaser中注册。 下面看一个例子，这个例子是从JDK的说明文档中修改过来的：

```java
public class PhaserTiers {
    final static int TASKS_PER_PHASER = 4;
    public static void main(String[] args) {
        Phaser phaser = new Phaser(){
            @Override
            protected boolean onAdvance(int phase, int registeredParties) {
                System.out.println("================== all threads is arrived ===================");
                return super.onAdvance(phase, registeredParties);
            }
        };
        Task[] tasks = new Task[12];
        build(tasks,0,12,phaser);
    }

    static void build(Task[] tasks, int lo, int hi, Phaser ph) {
        if (hi - lo > TASKS_PER_PHASER) {
            for (int i = lo; i < hi; i += TASKS_PER_PHASER) {
                int j = Math.min(i + TASKS_PER_PHASER, hi);
                build(tasks, i, j, new Phaser(ph));
            }
        } else {
            for (int i = lo; i < hi; ++i){
                tasks[i] = new Task(ph);
                tasks[i].start();
            }
        }
    }

    private static class Task extends Thread {
        private static Random rand = new Random(System.currentTimeMillis());
        final Phaser phaser;

        private Task(Phaser phaser) {
            this.phaser = phaser;
        }

        @Override
        public void run() {
            phaser.register();
            System.out.println(Thread.currentThread()+" is working.");
            try {
                TimeUnit.SECONDS.sleep(rand.nextInt(5)+1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            phaser.arriveAndAwaitAdvance();
        }
    }
}
```



例子中，共创建了12个线程，每4个线程注册到一个子Phaser中，一共有3个子Phaser。这3个子Phaser全部注册到一个根Phaser中，最后达到了12个线程在根Phaser中同步的效果。为了看得更加清晰，我扩展了Phaser类，代码如下：

```java
public class PhaserTiers2 {
    final static int TASKS_PER_PHASER = 4;

    public static void main(String[] args) {
        MyPhaser phaser = new MyPhaser("rootPhaser");

        Task[] tasks = new Task[12];
        build(tasks, 0, 12, phaser);
    }

    private static class MyPhaser extends Phaser {
        final private String name;

        public String getName() {
            return name;
        }

        public MyPhaser(String name) {
            this.name = name;
        }

        public MyPhaser(Phaser ph, String name) {
            super(ph);
            this.name = name;
        }

        @Override
        protected boolean onAdvance(int phase, int registeredParties) {
            System.out.println("================== all threads is arrived ===================");
            return super.onAdvance(phase, registeredParties);
        }
    }

    static void build(Task[] tasks, int lo, int hi, MyPhaser ph) {
        if (hi - lo > TASKS_PER_PHASER) {
            for (int i = lo; i < hi; i += TASKS_PER_PHASER) {
                int j = Math.min(i + TASKS_PER_PHASER, hi);
                build(tasks, i, j, new MyPhaser(ph, "SonPhaser" + i / TASKS_PER_PHASER));
            }
        } else {
            for (int i = lo; i < hi; ++i) {
                tasks[i] = new Task(ph);
                tasks[i].start();
            }
        }
    }

    private static class Task extends Thread {
        private static Random rand = new Random(System.currentTimeMillis());
        final MyPhaser phaser;

        private Task(MyPhaser phaser) {
            this.phaser = phaser;
        }

        @Override
        public void run() {
            phaser.register();
            System.out.println(Thread.currentThread() + " is working, it has registered in " + phaser.getName());
            try {
                TimeUnit.SECONDS.sleep(rand.nextInt(5)+1);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            phaser.arriveAndAwaitAdvance();
        }
    }
}
```



从以上代码的运行结果中可以清楚的看出，根Phaser管理着4个子Phaser，每个子Phaser中注册了4个线程，最终这12个线程如同注册在同一个Phaser中一样进行同步。

## 6.1.7. 监视

Phaser提供了多种方法来监视其各项状态。getRegisteredParties返回注册的parties数量，getArrivedParties返回当前阶段已经到达的parites数量，getUnarrivedParties返回当前阶段中尚未到达的parties数量，getPhase返回当前的phase number。

## 6.2 原理

从上面的概念和用法也可以看出来，Phaser是一个较为复杂的同步类，但它仅仅用到了TimeUnit、AtomicReference、LockSupport和Unsafe这四个辅助类而已。Phaser类的实现要点主要包括以下几点： 第一，所有的状态存储于一个volatile long state中，这个变量被分为四段使用，0~15字节表示当前阶段没有到达的线程数量unarrived；16~31字节表示parties；32~62字节表示phase；最后的一个字节表示Phaser的终止状态。Phaser中包含各种方法来线程安全的读写这些值，主要是使用Unsafe类中的CAS方法（详情见本系列的第三篇文章https://zhuanlan.zhihu.com/p/27338395）。 第二，定义了一个QNode类来表示Phaser的等待队列。这个QNode实现了ForkJoinPool.ManagedBlocker接口，因此可以直接在ForkJoinPool线程池中使用。即使不使用ForkJoinPool线程池，也可以直接使用QNode达到检查和阻塞线程的效果。ForkJoinPool.ManagedBlocker接口有两个方法，其中block方法可能会阻塞线程，若它返回true，则表示不需要阻塞线程了；isReleasable检查线程是否需要阻塞，如果它返回true，表示不需要阻塞。QNode类清晰明了，一望可知。 第三，Phaser中定义了两个等待队列，AtomicReference evenQ和AtomicReference oddQ。这是为了在同时增加和释放线程时，避免更大的冲突。evenQ用于偶数阶段，oddQ用于奇数阶段。 第四，Phaser的所有构造函数，最终调用如下的函数：

```java
public Phaser(Phaser parent, int parties) {
//如果parties大于65535，则抛出异常
    if (parties >>> PARTIES_SHIFT != 0)
        throw new IllegalArgumentException("Illegal number of parties");
    int phase = 0;
    this.parent = parent;
//如果parent不为null，则将root设置为parent的root
    if (parent != null) {
        final Phaser root = parent.root;
        this.root = root;
        this.evenQ = root.evenQ;
        this.oddQ = root.oddQ;
//如果初始化时parties不为0，则执行内部的注册方法
        if (parties != 0)
            phase = parent.doRegister(1);
    }
//如果parent为null，则创建两个QNode队列
    else {
        this.root = this;
        this.evenQ = new AtomicReference<QNode>();
        this.oddQ = new AtomicReference<QNode>();
    }
//拼出state字段
    this.state = (parties == 0) ? (long)EMPTY :
        ((long)phase << PHASE_SHIFT) |
        ((long)parties << PARTIES_SHIFT) |
        ((long)parties);
}
```



第五，内部的注册方法，主要是修改state的值：

```java
private int doRegister(int registrations) {
    // 拼出adjustment，这个变量包含unarrived和parties，分别是0~15和16~32字节
long adj = ((long)registrations << PARTIES_SHIFT) | registrations;
    final Phaser parent = this.parent;
    int phase;
    for (;;) {
        long s = state;
//counts是unarrived和parties拼出的一个int值
        int counts = (int)s;
//计算出parties和unarrived值
        int parties = counts >>> PARTIES_SHIFT;
        int unarrived = counts & UNARRIVED_MASK;
//如果注册值加上parites值超过范围，抛出异常
        if (registrations > MAX_PARTIES - parties)
            throw new IllegalStateException(badRegister(s));
//如果phase值<0，直接跳出循环
        else if ((phase = (int)(s >>> PHASE_SHIFT)) < 0)
            break;
        else if (counts != EMPTY) {             // 如果不是第一次注册
            if (parent == null || reconcileState() == s) {
                if (unarrived == 0)             // 等待advance
                    root.internalAwaitAdvance(phase, null); //执行内部的advance操作，有可能会等待
//反复执行CAS操作，将s设置为s+adj，修改相应的unarrived和parties，直至成功后跳出循环
                else if (UNSAFE.compareAndSwapLong(this, stateOffset,
                                                   s, s + adj))
                    break;
            }
        }
        else if (parent == null) {              // 第一次root的注册
//拼出下一个state，包含phase、parties和unarrived
            long next = ((long)phase << PHASE_SHIFT) | adj;
//反复执行CAS操作，将s设置为拼出的next，直至成功后跳出循环
            if (UNSAFE.compareAndSwapLong(this, stateOffset, s, next))
                break;
        }
        else {
            synchronized (this) {               // 第一个子Phaser的注册
                if (state == s) {               // 再次检查是否正确加锁
                    parent.doRegister(1);      //调用parent的注册方法
                    do {                        //设置当前的phase
                        phase = (int)(root.state >>> PHASE_SHIFT);
                        // assert phase < 0 || (int)state == EMPTY;
                    }
//反复使用CAS将state设置为phase和adj拼出的值，直至成功
 while (!UNSAFE.compareAndSwapLong
                             (this, stateOffset, state,
                              ((long)phase << PHASE_SHIFT) | adj));
                    break;
                }
            }
        }
    }
    return phase;
}
```



第六，内部的arrive方法，这个方法比较简单，主要是将unarrived数字减去1，然后检查是否当前阶段所有线程都已经到达，如果都到达则phase加1。

```java
private int doArrive(boolean deregister) {
//arrive后是否执行注销，据此设置adj（调整量）的值
    int adj = deregister ? ONE_ARRIVAL|ONE_PARTY : ONE_ARRIVAL;
    final Phaser root = this.root;
    for (;;) {
//根据是否为root设置s的值
        long s = (root == this) ? state : reconcileState();
//计算phase、counts、unarrived等变量的值
        int phase = (int)(s >>> PHASE_SHIFT);
        int counts = (int)s;
        int unarrived = (counts & UNARRIVED_MASK) - 1;
//phase值<0，直接退出
        if (phase < 0)
            return phase;
//检查异常状态
        else if (counts == EMPTY || unarrived < 0) {
            if (root == this || reconcileState() == s)
                throw new IllegalStateException(badArrive(s));
        }
//执行CAS操作，将state减去adj
        else if (UNSAFE.compareAndSwapLong(this, stateOffset, s, s-=adj)) {
//如果所有线程都已经到达，说明本阶段结束，要进入下一个阶段
            if (unarrived == 0) {
                long n = s & PARTIES_MASK;  // 下一个阶段的基础值
                int nextUnarrived = (int)n >>> PARTIES_SHIFT;
//若this不是root，则执行parent的doArrive操作
                if (root != this)
                    return parent.doArrive(nextUnarrived == 0);
//执行onAdvance操作，注意用户重写后的操作就在此处执行
                if (onAdvance(phase, nextUnarrived))
                    n |= TERMINATION_BIT;
                else if (nextUnarrived == 0)
                    n |= EMPTY;
                else
                    n |= nextUnarrived;
                n |= (long)((phase + 1) & MAX_PHASE) << PHASE_SHIFT;
//拼出n后，使用CAS来将s改写为n
                UNSAFE.compareAndSwapLong(this, stateOffset, s, n);
//将当前阶段的等待线程全部释放
                releaseWaiters(phase);
            }
            return phase;
        }
    }
}
```



第七，内部的awaitAdvance方法，用来让线程等待所有其他线程到达本阶段：

```java
private int internalAwaitAdvance(int phase, QNode node) {
//将上一个阶段的等待线程全部释放（如果有的话）
    releaseWaiters(phase-1);          
    boolean queued = false;           // true说明node已经进入等待队列
    int lastUnarrived = 0;            // to increase spins upon change
//自旋等待次数，单核CPU为1，多核CPU为256
    int spins = SPINS_PER_ARRIVAL;
    long s;
    int p;
//若p等于phase值时，进入循环
    while ((p = (int)((s = state) >>> PHASE_SHIFT)) == phase) {
        if (node == null) {           // 非中断模式时，自旋等待
            int unarrived = (int)s & UNARRIVED_MASK;
//如果未到达的线程数和上次未到达的线程数满足某条件时，自旋等待次数翻倍
            if (unarrived != lastUnarrived &&
                (lastUnarrived = unarrived) < NCPU)
                spins += SPINS_PER_ARRIVAL;
            boolean interrupted = Thread.interrupted();
//自旋等待，直至中断或者自旋次数已满（自旋等待是为了提高性能，避免频繁的操作队列）
            if (interrupted || --spins < 0) { 
//自旋等待完成后线程还未等到advance，则创建node，准备进入队列
                node = new QNode(this, phase, false, false, 0L);
                node.wasInterrupted = interrupted;
            }
        }
        else if (node.isReleasable()) // 线程等待完成或者中断
            break;
        else if (!queued) {           // 如果node未进入队列，则加入队列
            AtomicReference<QNode> head = (phase & 1) == 0 ? evenQ : oddQ;
            QNode q = node.next = head.get();
//使用CAS方法将node加入队列头部
            if ((q == null || q.phase == phase) &&
                (int)(state >>> PHASE_SHIFT) == phase) 
                queued = head.compareAndSet(q, node);
        }
        else {
            try {
//当node加入队列后，使用managedBlock方法来控制node进行等待，直至isReleasable返回true或者线程中断
                ForkJoinPool.managedBlock(node);
            } catch (InterruptedException ie) {
                node.wasInterrupted = true;
            }
        }
    }
//循环退出后，处理node的一些属性
    if (node != null) {
        if (node.thread != null)
            node.thread = null;       // avoid need for unpark()
        if (node.wasInterrupted && !node.interruptible)
            Thread.currentThread().interrupt();
        if (p == phase && (p = (int)(state >>> PHASE_SHIFT)) == phase)
            return abortWait(phase); // possibly clean up on abort
    }
//释放本阶段的所有等待线程
    releaseWaiters(phase);
    return p;
}
```



## 7. 小结

本文按照从易到难的顺序，介绍了JDK1.7中的5个同步工具，它们依次是CountDownLatch（一次性栅栏）、Semaphore（信号量）、CyclicBarrier（循环同步栅栏）、Exchanger（线程间交换器）和Phaser（灵活可重用同步栅栏）。与其他文章不同的是，本文不仅介绍了这些工具的用法，还简要的介绍了其实现原理。并发库中的源代码显得比较复杂，尤其是需要考虑到多线程重入的场景，更是增加了理解的难度。因此，多看代码，多多进行并发调试，尤为重要。

编辑于 2017-07-11