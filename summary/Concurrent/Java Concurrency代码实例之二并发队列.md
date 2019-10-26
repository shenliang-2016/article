# Java Concurrency代码实例之二并发队列

[![Alex Wang](https://pic4.zhimg.com/7b8e72c144e581881f769b179b98b309_xs.jpg)](https://www.zhihu.com/people/wang-du-du-43-1)

[Alex Wang](https://www.zhihu.com/people/wang-du-du-43-1)

高级工程师，Coder，Teamleader

60 人赞同了该文章

**本文的读者应该是已经掌握了基本的Java多线程开发技巧，但不熟悉Java Concurrency包的程序员。本文是本系列的第二篇文章，第一篇文章请看这里：
[Java Concurrency代码实例之一执行者与线程池 - 知乎专栏](https://zhuanlan.zhihu.com/p/26724352)**

# 1. 前言

按照用途与特性，Concurrency包中包含的工具被分为六类（外加一个工具类TimeUnit），即：
1. 执行者与线程池
2. 并发队列
3. 同步工具
4. 并发集合
5. 锁
6. 原子变量
本文介绍的就是第二类并发队列，具体包括五类，即Blockingqueue阻塞队列、BlockingDeque阻塞双向队列、TransferQueue传输队列、ConcurrentLinkedQueue并发链接队列和ConcurrentLinkedDeque并发链接双向队列。

# 2. BlockingQueue阻塞队列

BlockingQueue是一系列阻塞队列类的父接口，阻塞队列的共同特性是当存取条件不满足时，阻塞在操作处，因此常常被用于生产者和消费者场景中。

## 2.1 四组操作方法

BlockingQueue继承自Queue接口，因此也继承了Queue的两组操作方法，即add、remove、element和offer、poll、peek。
第一组方法在遇到异常时（例如add时队列已满，或者remove时队列已空）会抛出异常；
第二组方法在遇到异常时会返回特殊值，例如offer时队列已满返回false，poll时队列已空会返回null。
除此之外，BlockingQueue还提供了两组新的操作方法，第三组即put、take（它没有提供像element、peek类似的仅仅读取的方法）。put在队列已满时阻塞，直到队列中空出位置，然后将元素加入队列；take在队列已空时阻塞，直到队列中重新有了元素，然后从队列头取出元素并返回。
第四组方法，为了提供timeout特性，BlockingQueue提供了offer和poll的timeout形式，即offer(e, time, unit)和poll(time, unit)，它们会在特殊情况时阻塞直到条件满足或者超时。

## 2.2 生产者和消费者例子

在介绍具体的阻塞类之前，先来看看阻塞队列最常应用的场景，即生产者和消费者例子。一般而言，有n个生产者，各自生产产品，并放入队列。同时有m个消费者，各自从队列中取出产品消费。当队列已满时（队列可以在初始化时设置Capacity容量），生产者会在放入队列时阻塞；当队列空时，消费者会在取出产品时阻塞。代码如下：

```text
public class BlockingQueueExam {
    public static void main(String[] args) throws InterruptedException {
        BlockingQueue<String> blockingQueue = new LinkedBlockingQueue<>(3);
        ExecutorService service = Executors.newCachedThreadPool();
        for (int i = 0; i < 5; i++) {
            service.submit(new Producer("Producer" + i, blockingQueue));
        }
        for (int i = 0; i < 5; i++) {
            service.submit(new Consumer("Consumer" + i, blockingQueue));
        }
        service.shutdown();
    }
}

class Producer implements Runnable {
    private final String name;
    private final BlockingQueue<String> blockingQueue;
    private static Random rand = new Random(47);
    private static AtomicInteger productID = new AtomicInteger(0);

    Producer(String name, BlockingQueue<String> blockingQueue) {
        this.name = name;
        this.blockingQueue = blockingQueue;
    }

    @Override
    public void run() {
        try {
            for (int i = 0; i < 10; i++) {
                SECONDS.sleep(rand.nextInt(5));
                String str = "Product" + productID.getAndIncrement();
                blockingQueue.add(str);
                //注意，这里得到的size()有可能是错误的
                System.out.println(name + " product " + str + ", queue size = " + blockingQueue.size());
            }
            System.out.println(name + " is over");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}

class Consumer implements Runnable {
    private final String name;
    private final BlockingQueue<String> blockingQueue;
    private static Random rand = new Random(47);

    Consumer(String name, BlockingQueue<String> blockingQueue) {
        this.name = name;
        this.blockingQueue = blockingQueue;
    }

    @Override
    public void run() {
        try {
            for (int i = 0; i < 10; i++) {
                SECONDS.sleep(rand.nextInt(5));
                String str = blockingQueue.take();
                //注意，这里得到的size()有可能是错误的
                System.out.println(name + " consume " + str + ", queue size = " + blockingQueue.size());
            }
            System.out.println(name + " is over");
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

以上代码中的阻塞队列是LinkedBlockingQueue，初始化容量为3。生产者5个，每个生产者间隔随机时间后生产一个产品put放入队列，每个生产者生产10个产品；消费者也是5个，每个消费者间隔随机时间后take取出一个产品进行消费，每个消费者消费10个产品。可以看到，当队列满时，所有生产者被阻塞；当队列空时，所有消费者被阻塞。代码中还用到了AtomicInteger原子整数，用来确保产品的编号不会混乱，此类留到后续文章中介绍。

## 2.3 LinkedBlockingQueue和ArrayedBlockingQueue

前面已经介绍过，BlockingQueue是所有阻塞队列的父接口，具体的实现类有LinkedBlockingQueue、ArrayedBlockingQueue、SynchronousQueue、PriorityBlockingQueue和DelayQueue。
LinkedBlockingQueue和ArrayedBlockingQueue的共同点在于，它们都是一个FIFO（先入先出）队列，列头元素就是最老的元素，列尾元素就是最新的元素。元素总是从列尾插入队列，从列头取出队列。
它们的不同之处在于，LinkedBlockingQueue的内部实现是一个链表，而ArrayedBlockingQueue的内部实现是一个原生数组。正如其他Java集合一样，链表形式的队列，其存取效率要比数组形式的队列高。但是在一些并发程序中，数组形式的队列由于具有一定的可预测性，因此可以在某些场景中获得更好的效率。
另一个不同点在于，ArrayedBlockingQueue支持“公平”策略。若在构造函数中指定了“公平”策略为true，则阻塞在插入或取出方法的所有线程也会按照FIFO进行排队，这样可以有效避免一些线程被“饿死”。
BlockingQueue queue = new ArrayBlockingQueue<>(3, true);
总体而言，LinkedBlockingQueue是阻塞队列的最经典实现，在不需要“公平”策略时，基本上使用它就够了。

## 2.4 SynchronousQueue同步队列

SynchronousQueue是一个比较特殊的阻塞队列，它具有以下几个特点：
1. 一个调用插入方法的线程必须等待另一个线程调用取出方法；
2. 队列没有容量Capacity（或者说容量为0），事实上队列中并不存储元素，它只是提供两个线程进行信息交换的场所；
3. 由于以上原因，队列在很多场合表现的像一个空队列。不能对元素进行迭代，不能peek元素，poll会返回null；
4. 队列中不允许存入null元素。
5. SynchronousQueue如同ArrayedBlockingQueue一样，支持“公平”策略，在构造函数中可以传入false或true表示是否支持该策略。
下面是一个例子，5个Producer产生产品，存入队列；5个Consumer从队列中取出产品，进行消费。

```text
public class SynchronizeQueueExam {
    public static void main(String[] args) {
        SynchronousQueue<String> queue = new SynchronousQueue<>(false);
        ExecutorService service = Executors.newCachedThreadPool();
        for (int i = 0; i < 5; i++) {
            service.submit(new Producer(queue, "Producer" + i));
        }
        for (int i = 0; i < 5; i++) {
            service.submit(new Consumer(queue, "Consumer" + i));
        }
        service.shutdown();
    }

    static class Producer implements Runnable {
        private final SynchronousQueue<String> queue;
        private final String name;
        private static Random rand = new Random(47);
        private static AtomicInteger productID = new AtomicInteger(0);

        Producer(SynchronousQueue<String> queue, String name) {
            this.queue = queue;
            this.name = name;
        }

        @Override
        public void run() {
            try {
                for (int i = 0; i < 5; i++) {
                    TimeUnit.SECONDS.sleep(rand.nextInt(5));
                    String str = "Product" + productID.incrementAndGet();
                    queue.put(str);
                    System.out.println(name + " put " + str);
                }
                System.out.println(name + " is over.");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }


    static class Consumer implements Runnable {
        private final SynchronousQueue<String> queue;
        private final String name;

        Consumer(SynchronousQueue<String> queue, String name) {
            this.queue = queue;
            this.name = name;
        }

        @Override
        public void run() {
            try {
                for (int i = 0; i < 5; i++) {
                    String str = queue.take();
                    System.out.println(name + " take " + str);
                }
                System.out.println(name + " is over.");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

同步队列在线程池的构造中用到过。我们在本系列的第一篇文章中介绍过几类线程池的构造函数，复习一下。
**单线程池**：newSingleThreadExecutor()方法创建，五个参数分别是ThreadPoolExecutor(1, 1, 0L, TimeUnit.MILLISECONDS, new LinkedBlockingQueue())。含义是池中保持一个线程，最多也只有一个线程，也就是说这个线程池是顺序执行任务的，多余的任务就在队列中排队。
**固定线程池**：newFixedThreadPool(nThreads)方法创建，五个参数分别是ThreadPoolExecutor(nThreads, nThreads, 0L, TimeUnit.MILLISECONDS, new LinkedBlockingQueue())。含义是池中保持nThreads个线程，最多也只有nThreads个线程，多余的任务也在队列中排队。
**缓存线程池**：newCachedThreadPool()创建，五个参数分别是ThreadPoolExecutor(0, Integer.MAX_VALUE, 60L, TimeUnit.SECONDS, new SynchronousQueue())。含义是池中不保持固定数量的线程，随需创建，最多可以创建Integer.MAX_VALUE个线程（说一句，这个数量已经大大超过目前任何操作系统允许的线程数了），空闲的线程最多保持60秒，多余的任务在SynchronousQueue中等待。
为什么单线程池和固定线程池使用的任务阻塞队列是LinkedBlockingQueue()，而缓存线程池使用的是SynchronousQueue()呢？
因为单线程池和固定线程池中，线程数量是有限的，因此提交的任务需要在LinkedBlockingQueue队列中等待空余的线程；而缓存线程池中，线程数量几乎无限（上限为Integer.MAX_VALUE），因此提交的任务只需要在SynchronousQueue队列中同步移交给空余线程即可。

## 2.5 PriorityBlockingQueue优先级阻塞队列

优先级队列PriorityQueue有以下几个特点：
1. 队列中的元素总是按照“自然顺序”进行排序，或者根据构造函数中给定的Comparator进行排序；
2. 队列中不允许存在null，也不允许存在不能排序的元素；
3. 对于排序值相同的元素，其序列是不保证的，当然你可以自己扩展这个功能；
4. 队列容量是没有上限的，但是如果插入的元素超过负载，有可能会引起OutOfMemory异常；
5. 使用迭代子iterator()对队列进行轮询，其顺序不能保证；
那么PriorityBlockingQueue除了以上特点外，还有另外的特点：
6. 它还具有BlockingQueue的put和take方法，但是由于队列容量没有上线，所以put方法是不会被阻塞的，但是take方法是会被阻塞的；
7. 可以给定初始容量，这个容量会按照一定的算法自动扩充。
下面是一个PriorityBlockingQueue的例子，例子中定义了一个按照字符串倒序排列的队列。5个生产者不断产生随机字符串放入队列，5个消费者不断从队列中取出随机字符串，可以看到若队列为空，取出的线程会等待；也可以看到同一个线程取出的字符串基本上是倒序的（因为不同线程同时存取元素，因此取出的字符串打印到屏幕上往往不是倒序的了）：

```text
public class PriorityBlockingQueueExam {
    public static void main(String[] args) {
        //创建一个初始容量为3，排序为字符串排序相反的队列
        PriorityBlockingQueue<String> queue = new PriorityBlockingQueue<String>(3, new Comparator<String>() {
            @Override
            public int compare(String o1, String o2) {
                if (o1.compareTo(o2) < 0) {
                    return 1;
                } else if (o1.compareTo(o2) > 0) {
                    return -1;
                } else {
                    return 0;
                }
            }
        });

        ExecutorService service = Executors.newCachedThreadPool();
        for (int i = 0; i < 5; i++) {
            service.submit(new Producer("Producer" + i, queue));
        }
        for (int i = 0; i < 5; i++) {
            service.submit(new Consumer("Consumer" + i, queue));
        }
        service.shutdown();
    }

    static class Producer implements Runnable {
        private final String name;
        private final PriorityBlockingQueue<String> queue;
        private static Random rand = new Random(System.currentTimeMillis());

        Producer(String name, PriorityBlockingQueue<String> queue) {
            this.name = name;
            this.queue = queue;
        }

        @Override
        public void run() {
            for (int i = 0; i < 10; i++) {
                String str = "Product" + rand.nextInt(1000);
                queue.put(str);
                System.out.println("->" + name + " put " + str);
                try {
                    TimeUnit.SECONDS.sleep(rand.nextInt(5));
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
            System.out.println(name + " is over");
        }
    }


    static class Consumer implements Runnable {
        private final String name;
        private final PriorityBlockingQueue<String> queue;
        private static Random rand = new Random(System.currentTimeMillis());

        Consumer(String name, PriorityBlockingQueue<String> queue) {
            this.name = name;
            this.queue = queue;
        }

        @Override
        public void run() {
            try {
                for (int i = 0; i < 10; i++) {
                    String str = queue.take();
                    System.out.println("<-" + name + " take " + str);
                    TimeUnit.SECONDS.sleep(rand.nextInt(5));
                }
                System.out.println(name + " is over");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

总之，在需要使用优先级队列，且还有阻塞需求时，就可以使用PriorityBlockingQueue了。

## 2.6 DelayQueue

DelayQueue是一个延时优先级阻塞队列。队列中只能存入Delayed接口实现的对象，Delayed接口如下所示：

```text
public interface Delayed extends Comparable<Delayed> {
    long getDelay(TimeUnit unit);
}
Comparable接口如下所示：
public interface Comparable<T> {
        public int compareTo(T o);
}
```

因此DelayQueue中存入的对象要同时实现getDelay和compareTo两个方法。getDelay方法是用来检测队列中的元素是否到期；compareTo方法是用来给队列中的元素进行排序。DelayQueue持有一个PriorityBlockingQueue，每个Delayed对象实际上都放入了这个队列，并按照compareTo方法进行排序。当队列中对象的getDelay方法返回的值小于等于0（即对象已经超时）时，才可以将对象从队列中取出。若使用take方法，则方法会一直阻塞，直到队列头部的对象超时被取出；若使用poll方法，则当没有超时对象时，直接返回null。
总结来说，有如下几个特点：
1. 队列中的对象都是Delayed对象，它实现了getDelay和compareTo两个方法；
2. 队列中的对象按照优先级（按照compareTo）进行了排序，队列头部是最先超时的对象；
3. take方法会在没有超时对象时一直阻塞，直到有对象超时；poll方法会在没有超时对象时返回null。
4. 队列中不允许存储null，且iterator方法返回的值不能确保按顺序排列。
下面是一个列子，特别需要注意getDelay和compareTo方法的实现：

```text
public class DelayQueueExam {
    public static void main(String[] args) throws InterruptedException {
        DelayQueue<DelayElement> queue = new DelayQueue<>();
        for (int i = 0; i < 10; i++) {
            queue.put(new DelayElement(1000 * i, "DelayElement" + i));
        }
        while (!queue.isEmpty()) {
            DelayElement delayElement = queue.take();
            System.out.println(delayElement.getName());
        }
    }

    static class DelayElement implements Delayed {
        private final long delay;
        private long expired;
        private final String name;

        DelayElement(int delay, String name) {
            this.delay = delay;
            this.name = name;
            expired = System.currentTimeMillis() + delay;
        }

        public String getName() {
            return name;
        }

        @Override
        public long getDelay(TimeUnit unit) {
            return unit.convert(expired - System.currentTimeMillis(), TimeUnit.MILLISECONDS);
        }

        @Override
        public int compareTo(Delayed o) {
            long d = (getDelay(TimeUnit.MILLISECONDS) - o.getDelay(TimeUnit.MILLISECONDS));
            return (d == 0) ? 0 : ((d < 0) ? -1 : 1);
        }
    }
}
```

DelayQueue通过PriorityQueue，使得超时的对象最先被处理，将take对象的操作阻塞住，避免了遍历方式的轮询，提高了性能。在很多需要回收超时对象的场景都能用上。

# 3. BlockingDeque阻塞双向队列

BlockingDeque中各种特性上都非常类似于BlockingQueue，事实上它也继承自BlockingQueue，它们的不同点主要在于BlockingDeque可以同时从队列头部和尾部增删元素。
因此，总结一下BlockingDeque的四组增删元素的方法：
第一组，抛异常的方法，包括addFirst(e)，addLast(e)，removeFirst()，removeLast()，getFirst()和getLast()；
第二组，返回特殊值的方法，包括offerFirst(e) ，offerLast(e) ，pollFirst()，pollLast()，peekFirst()和peekLast()；
第三组，阻塞的方法，包括putFirst(e)，putLast(e)，takeFirst()和takeLast()；
第四组，超时的方法，包括offerFirst(e, time, unit)，offerLast(e, time, unit)，pollFirst(time, unit)和pollLast(time, unit)。
BlockingDeque目前只有一个实现类LinkedBlockingDeque，其用法与LinkedBlockingQueue非常类似，这里就不给出实例了。

# 4. TransferQueue传输队列

TransferQueue继承自BlockingQueue，之所以将它独立成章，是因为它是一个非常重要的队列，且提供了一些阻塞队列所不具有的特性。
简单来说，TransferQueue提供了一个场所，生产者线程使用transfer方法传入一些对象并阻塞，直至这些对象被消费者线程全部取出。前面介绍的SynchronousQueue很像一个容量为0的TransferQueue。
下面是一个例子，一个生产者使用transfer方法传输10个字符串，两个消费者线程则各取出5个字符串，可以看到生产者在transfer时会一直阻塞直到所有字符串被取出：

```text
public class TransferQueueExam {
    public static void main(String[] args) {
        TransferQueue<String> queue = new LinkedTransferQueue<>();
        ExecutorService service = Executors.newCachedThreadPool();
        service.submit(new Producer("Producer1", queue));
        service.submit(new Consumer("Consumer1", queue));
        service.submit(new Consumer("Consumer2", queue));
        service.shutdown();
    }

    static class Producer implements Runnable {
        private final String name;
        private final TransferQueue<String> queue;

        Producer(String name, TransferQueue<String> queue) {
            this.name = name;
            this.queue = queue;
        }
        @Override
        public void run() {
            System.out.println("begin transfer objects");

            try {
                for (int i = 0; i < 10; i++) {
                    queue.transfer("Product" + i);
                    System.out.println(name + " transfer "+"Product"+i);
                }
                System.out.println("after transformation");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(name + " is over");
        }
    }

    static class Consumer implements Runnable {
        private final String name;
        private final TransferQueue<String> queue;
        private static Random rand = new Random(System.currentTimeMillis());

        Consumer(String name, TransferQueue<String> queue) {
            this.name = name;
            this.queue = queue;
        }

        @Override
        public void run() {
            try {
                for (int i = 0; i < 5; i++) {
                    String str = queue.take();
                    System.out.println(name + " take " + str);
                    TimeUnit.SECONDS.sleep(rand.nextInt(5));
                }
                System.out.println(name + " is over");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

上面的代码中只使用了transfer方法，TransferQueue共包括以下方法：
1. transfer(E e)，若当前存在一个正在等待获取的消费者线程，即立刻移交之；否则会将元素e插入到队列尾部，并进入阻塞状态，直到有消费者线程取走该元素。
2. tryTransfer(E e)，若当前存在一个正在等待获取的消费者线程（使用take()或者poll()函数），即立刻移交之； 否则返回false，并且不进入队列，这是一个非阻塞的操作。
3. tryTransfer(E e, long timeout, TimeUnit unit) 若当前存在一个正在等待获取的消费者线程，即立刻移交之；否则会将元素e插入到队列尾部，并且等待被消费者线程获取消费掉，若在指定的时间内元素e无法被消费者线程获取，则返回false，同时该元素被移除。
4. hasWaitingConsumer() 判断是否存在消费者线程。
5. getWaitingConsumerCount() 获取所有等待获取元素的消费线程数量。
再来看两个生产者和两个消费者的例子：

```text
public class TransferQueueExam2 {
    public static void main(String[] args) {
        TransferQueue<String> queue = new LinkedTransferQueue<>();
        ExecutorService service = Executors.newCachedThreadPool();
        service.submit(new Producer("Producer1", queue));
        service.submit(new Producer("Producer2", queue));
        service.submit(new Consumer("Consumer1", queue));
        service.submit(new Consumer("Consumer2", queue));
        service.shutdown();
    }

    static class Producer implements Runnable {
        private final String name;
        private final TransferQueue<String> queue;

        Producer(String name, TransferQueue<String> queue) {
            this.name = name;
            this.queue = queue;
        }

        @Override
        public void run() {
            System.out.println(name + " begin transfer objects");

            try {
                for (int i = 0; i < 5; i++) {
                    queue.transfer(name + "_Product" + i);
                    System.out.println(name + " transfer " + name + "_Product" + i);
                }
                System.out.println(name + " after transformation");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println(name + " is over");
        }
    }

    static class Consumer implements Runnable {
        private final String name;
        private final TransferQueue<String> queue;
        private static Random rand = new Random(System.currentTimeMillis());

        Consumer(String name, TransferQueue<String> queue) {
            this.name = name;
            this.queue = queue;
        }

        @Override
        public void run() {
            try {
                for (int i = 0; i < 5; i++) {
                    String str = queue.take();
                    System.out.println(name + " take " + str);
                    TimeUnit.SECONDS.sleep(rand.nextInt(5));
                }
                System.out.println(name + " is over");
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }
}
```

它的作者Doug Lea 这样评价它：TransferQueue是一个聪明的队列，它是ConcurrentLinkedQueue, SynchronousQueue (在公平模式下), 无界的LinkedBlockingQueues等的超集。
所以，在合适的场景中，请尽量使用TransferQueue，目前它只有一个实现类LinkedTransferQueue。

# 5. ConcurrentLinkedQueue并发链接队列

## 5.1 并发与并行

写到此处时，应该认真梳理一下关于多线程编程中的一些名词了，具体包括多线程（MultiThread）、并发（Concurrency）和并行（Parrellism）。多线程的概念应该是比较清晰的，是指计算机和编程语言都提供线程的概念，多个线程可以同时在一台计算机中运行。
而并发和并行则是两个非常容易混淆的概念，第一种区分方法是以程序在计算机中的执行方式来区分。我称之为“并发执行”和“并行执行”的区分：
并发执行是指多个线程（例如n个）在一台计算机中宏观上“同时”运行，它们有可能是一个CPU轮换的处理n个线程，也有可能是m个CPU以各种调度策略来轮换处理n个线程；
并行执行是指多个线程（n个）在一台计算机的多个CPU（m个，m>=n）上微观上同时运行，并行执行时操作系统不需要调度这n个线程，每个线程都独享一个CPU持续运行直至结束。
第二种区分方法则是“并发编程”和“并行编程”的区别：
并发编程可以理解为多线程编程，并发编程的代码必定以“并发执行”的方式运行；
并行编程则是一种更加特殊的编程方法，它需要使用特殊的编程语言（例如Cilk语言），或者特殊的编程框架（例如Parallel Java 2 Library）。另外，我在本系列的第一篇中提到的Fork-Join框架也是一种并行编程框架。

## 5.2 并发的基础

理解了并发的概念，我们再来看首次遇到的带有并发字眼（Concurrent）的类ConcurrentLinkedQueue，并发链接队列。
目前看来，可以这么认为，在java.util.concurrency包内，凡是带有Concurrent字眼的类，都是以CAS为基础的非阻塞工具类。例如ConcurrentLinkedQueue、ConcurrentLinkedDeque、ConcurrentHashMap、ConcurrentSkipListMap、ConcurrentSkipListSet。
好了，那么什么是CAS呢？CAS即CompareAndSwap“比较并交换”，具体的细节将会在后续的关于原子变量（Atomic）章节中介绍。简而言之，当代的很多CPU提供了一种CAS指令，由于指令运行不会被打断，因此依赖这种指令就可以设计出一种不需要锁的非阻塞并发算法，依赖这种算法，就可以设计出各种并发类。
期望提前看到CAS和ConcurrentLinkedQueue具体设计细节的可以看这一篇文章：非阻塞算法在并发容器中的实现

## 5.3 各类队列的例子

下面的例子中，我们使用参数控制，分别测试了四种队列在多个线程同时存储变量时的表现：

```text
public class ConcurrentLinkedQueueExam {
    private static final int TEST_INT = 10000000;

    public static void main(String[] args) throws InterruptedException {
        long start = System.currentTimeMillis();
        Queue<Integer> queue = null;
        if (args.length < 1) {
            System.out.println("Usage: input 1~4 ");
            System.exit(1);
        }
        int param = Integer.parseInt(args[0]);
        switch (param) {
            case 1:
                queue = new LinkedList<>();
                break;
            case 2:
                queue = new LinkedBlockingQueue<>();
                break;
            case 3:
                queue = new ArrayBlockingQueue<Integer>(TEST_INT * 5);
                break;
            case 4:
                queue = new ConcurrentLinkedQueue<>();
                break;
            default:
                System.out.println("Usage: input 1~4 ");
                System.exit(2);
        }
        System.out.println("Using " + queue.getClass().getSimpleName());

        ExecutorService service = Executors.newCachedThreadPool();
        for (int i = 0; i < 5; i++) {
            service.submit(new Putter(queue, "Putter" + i));
        }
        TimeUnit.SECONDS.sleep(2);
        for (int i = 0; i < 5; i++) {
            service.submit(new Getter(queue, "Getter" + i));
        }
        service.shutdown();
        service.awaitTermination(1, TimeUnit.DAYS);
        long end = System.currentTimeMillis();
        System.out.println("Time span = " + (end - start));
        System.out.println("queue size = " + queue.size());
    }

    static class Putter implements Runnable {
        private final Queue<Integer> queue;
        private final String name;

        Putter(Queue<Integer> queue, String name) {
            this.queue = queue;
            this.name = name;
        }


        @Override
        public void run() {
            for (int i = 0; i < TEST_INT; i++) {
                queue.offer(1);
            }
            System.out.println(name + " is over");
        }
    }

    static class Getter implements Runnable {
        private final Queue<Integer> queue;
        private final String name;

        Getter(Queue<Integer> queue, String name) {
            this.queue = queue;
            this.name = name;
        }

        @Override
        public void run() {
            int i = 0;
            while (i < TEST_INT) {
                synchronized (Getter.class) {
                    if (!queue.isEmpty()) {
                        queue.poll();
                        i++;
                    }
                }
            }
            System.out.println(name + " is over");
        }
    }
}
```

输入1，结果如下：

```text
Using LinkedList
…
Time span = 16613
queue size = 10296577
```

输入2，结果如下：

```text
Using LinkedBlockingQueue
…
Time span = 16847
queue size = 0
```

输入3，结果如下：

```text
Using ArrayBlockingQueue
…
Time span = 6815
queue size = 0
```

输入4，结果如下：

```text
Using ConcurrentLinkedQueue
…
Time span = 22802
queue size = 0
```

分析运行的结果，有如下结论：
第一，非并发类例如LinkedList在多线程环境下运行是会出错的，结果的最后一行输出了队列的size值，只有它的size值不等于0，这说明在多线程运行时许多poll操作并没有弹出元素，甚至很多offer操作也没有能够正确插入元素。其他三种并发类都能够在多线程环境下正确运行；
第二，并发类也不是完全不需要注意加锁，例如这一段代码：

```text
while (i < TEST_INT) {
    synchronized (Getter.class) {
        if (!queue.isEmpty()) {
            queue.poll();
            i++;
        }
    }
}
```

如果不加锁，那么isEmpty和poll之间有可能被其他线程打断，造成结果的不确定性。
第三，本例中LinkedBlockingQueue和ArrayBlockingQueue并没有因为生产-消费关系阻塞，因为容量设置得足够大。它们的元素插入和弹出操作是加锁的，而ConcurrentLinkedQueue的元素插入和弹出操作是不加锁的，而观察性能其实并没有数量级上的差异（有待进一步测试）。
第四，ArrayBlockingQueue性能明显好于LinkedBlockingQueue，甚至也好于ConcurrentLinkedQueue，这是因为它的内部存储结构是原生数组，而其他两个是链表，需要new一个Node。同时，链表也会造成更多的GC。

# 6. ConcurrentLinkedDeque并发链接双向队列

ConcurrentLinkedDeque与ConcurrentLinkedQueue非常类似，不同之处仅在于它是一个双向队列。

# 7. 小结

Java的并发队列，具体包括BlockingQueue阻塞队列、BlockingDeque阻塞双向队列、TransferQueue传输队列、ConcurrentLinkedQueue并发链接队列和ConcurrentLinkedDeque并发链接双向队列。BlockingQueue和BlockingDeque的内部使用锁来保护元素的插入弹出操作，同时它们还提供了生产者-消费者场景的阻塞方法；TransferQueue被用来在多个线程之间优雅的传递对象；ConcurrentLinkedQueue和ConcurrentLinkedDeque依靠CAS指令，来实现非阻塞的并发算法。

发布于 2017-05-27