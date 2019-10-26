# Java Concurrency代码实例之四-锁

[![Alex Wang](https://pic4.zhimg.com/7b8e72c144e581881f769b179b98b309_xs.jpg)](https://www.zhihu.com/people/wang-du-du-43-1)

[Alex Wang](https://www.zhihu.com/people/wang-du-du-43-1)

高级工程师，Coder，Teamleader

47 人赞同了该文章

本文的读者应该是已经掌握了基本的Java多线程开发技巧，但不熟悉Java Concurrency包的程序员。本文是本系列的第四篇文章，前三篇文章请看这里：
[Java Concurrency代码实例之一执行者与线程池 - 知乎专栏](https://zhuanlan.zhihu.com/p/26724352)
[Java Concurrency代码实例之二并发队列 - 知乎专栏](https://zhuanlan.zhihu.com/p/27148381)
[Java Concurrency代码实例之三原子变量 - 知乎专栏](https://zhuanlan.zhihu.com/p/27338395)

# 1. 前言

按照用途与特性，Concurrency包中包含的工具被分为六类（外加一个工具类TimeUnit），即：
1. 执行者与线程池
2. 并发队列
3. 同步工具
4. 并发集合
5. 锁
6. 原子变量
本文介绍的是其中的锁，与synchronize关键字不同，并发包中的锁，其阻塞机制是调用Unsafe类提供的park和unpark方法，结合CAS原子语句，实现了比synchronize更加高效灵活的各种锁。

# 2. Unsafe类的park和unpark

在前文（[Java Concurrency代码实例之三原子变量 - 知乎专栏](https://zhuanlan.zhihu.com/p/27338395)）中曾经详细介绍过Unsafe类的指针和CAS操作，这里再介绍一下它的park和unpark操作。

```text
public native void park(boolean var1, long var2);
public native void unpark(Object var1);
```

park方法用来阻塞一个线程，第一个参数用来指示后面的参数是绝对时间还是相对时间，true表示绝对时间，false表示从此刻开始后的相对时间。调用park的线程就阻塞在此处。
upark用来释放某个线程的阻塞，线程用参数var1表示。例子如下：

```text
public class UnsafeParkExam {
    public static void main(String[] args) throws NoSuchFieldException, IllegalAccessException {
        Field f = Unsafe.class.getDeclaredField("theUnsafe");
        f.setAccessible(true);
        Unsafe unsafe = (Unsafe) f.get(null);
        Thread t1 = new Thread() {
            @Override
            public void run() {
                Thread.currentThread().setName("t1");
                System.out.println(Thread.currentThread().getName() + " before park");
                //park 100 seconds
                unsafe.park(false, TimeUnit.NANOSECONDS.convert(100, TimeUnit.SECONDS));
                System.out.println(Thread.currentThread().getName() + " after park");
            }
        };
        Thread t2 = new Thread() {
            @Override
            public void run() {
                try {
                    Thread.currentThread().setName("t2");
                    TimeUnit.SECONDS.sleep(1);
                    System.out.println(Thread.currentThread().getName() + " unpark t1");
                    unsafe.unpark(t1);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }

            }
        };
        Thread t3 = new Thread() {
            @Override
            public void run() {
                Thread.currentThread().setName("t3");
                System.out.println(Thread.currentThread().getName() + " park 5 seconds");
                //park 5 seconds
                unsafe.park(true, System.currentTimeMillis() + TimeUnit.MILLISECONDS.convert(5,TimeUnit.SECONDS));
                System.out.println(Thread.currentThread().getName() + " after park");
            }
        };
        t1.start();
        t2.start();
        t3.start();
        try {
            t1.join();
            t2.join();
            t3.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

# 3. LockSupport

直接使用Unsafe还是有诸多不便之处，因此lock包提供了一个辅助类LockSupport来封装了park和unpark，例子如下：

```text
public class LockSupportExam {
    public static void main(String[] args) {
        Thread t1 = new Thread() {
            @Override
            public void run() {
                Thread.currentThread().setName("t1");
                System.out.println(Thread.currentThread().getName() + " before park");
                //park 100 seconds
                LockSupport.parkNanos(TimeUnit.NANOSECONDS.convert(100, TimeUnit.SECONDS));
                System.out.println(Thread.currentThread().getName() + " after park");
            }
        };
        Thread t2 = new Thread() {
            @Override
            public void run() {
                try {
                    Thread.currentThread().setName("t2");
                    TimeUnit.SECONDS.sleep(1);
                    System.out.println(Thread.currentThread().getName() + " unpark t1");
                    LockSupport.unpark(t1);
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }

            }
        };
        Thread t3 = new Thread() {
            @Override
            public void run() {
                Thread.currentThread().setName("t3");
                System.out.println(Thread.currentThread().getName() + " park 5 seconds");
                //park 5 seconds
                LockSupport.parkUntil(System.currentTimeMillis() + TimeUnit.MILLISECONDS.convert(5,TimeUnit.SECONDS));
                System.out.println(Thread.currentThread().getName() + " after park");
            }
        };
        t1.start();
        t2.start();
        t3.start();
        try {
            t1.join();
            t2.join();
            t3.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

从例子中可以看出，使用LockSupport要比直接只用Unsafe更加便捷。除此之外，LockSupport还可以用来给线程设置一个Blocker对象，便于调试和检测线程，其原理是使用Unsafe的putObject方法直接设置Thread对象的parkBlocker属性，并在合适的时候读取这个Blocker对象，例子如下：

```text
public class LockSupportBlockerExam {
    public static void main(String[] args) {
        Thread t3 = new Thread() {
            @Override
            public void run() {
                Thread.currentThread().setName("t3");
                System.out.println(Thread.currentThread().getName() + " park 5 seconds");
                //park 5 seconds, set blocker
                Object blocker = new String("Alex Wang");
                LockSupport.parkUntil(blocker, System.currentTimeMillis() + TimeUnit.MILLISECONDS.convert(5, TimeUnit.SECONDS));
                System.out.println(Thread.currentThread().getName() + " after park");
            }
        };
        t3.start();

        try {
            Object t3_blocker = null;
            while (t3_blocker == null) {
                t3_blocker = LockSupport.getBlocker(t3);
                TimeUnit.MILLISECONDS.sleep(10);
            }
            System.out.println("t3 blocker is :" + t3_blocker);
            t3.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
    }
}
```

# 4. 锁的核心AQS同步器

毫不夸张的说，各种锁ReentrantLock、ReentrantReadWriteLock以及各种同步器诸如Semaphore、CountDownLatch等等，其核心都是AbstractQueuedSynchronizer（AQS同步器）。要了解AQS的原理，仅仅看代码和JDK文档是不够的，其原理在这一篇论文（[http://gee.cs.oswego.edu/dl/papers/aqs.pdf](https://link.zhihu.com/?target=http%3A//gee.cs.oswego.edu/dl/papers/aqs.pdf)）中详细阐述了，强烈建议仔细阅读此论文。

## 4.1 使用AQS写一个排它锁

由于AQS非常复杂，从源代码入手很难看懂，最好的学习方法是看它是如何被使用的。这里有一个非常简单的例子SimpleLock，实现了一个最简单的排它锁。当有线程获得锁时，其他线程只能等待；当这个线程释放锁时，另一个线程可以竞争获取锁。

```text
public class SimpleLock {
    private static class Sync extends AbstractQueuedSynchronizer {
        @Override
        protected boolean tryAcquire(int ignore) {
            return compareAndSetState(0, 1);
        }

        @Override
        protected boolean tryRelease(int ignore) {
            setState(0);
            return true;
        }

        protected Sync() {
            super();
        }
    }

    private final Sync sync = new Sync();

    public void lock() {
        sync.acquire(1);
    }

    public void unlock() {
        sync.release(1);
    }

    private static class MyThread extends Thread {
        private final String name;
        private final SimpleLock lock;

        private MyThread(String name, SimpleLock lock) {
            this.name = name;
            this.lock = lock;
        }

        @Override
        public void run() {
            try {
                lock.lock();
                System.out.println(name + " get the lock");
                TimeUnit.SECONDS.sleep(2);
            } catch (InterruptedException e) {
                e.printStackTrace();
            } finally {
                lock.unlock();
                System.out.println(name + " release the lock");
            }
        }
    }

    public static void main(String[] args) {
        final SimpleLock mutex = new SimpleLock();
        MyThread t1 = new MyThread("t1", mutex);
        MyThread t2 = new MyThread("t2", mutex);
        MyThread t3 = new MyThread("t3", mutex);
        t1.start();
        t2.start();
        t3.start();
        try {
            t1.join();
            t2.join();
            t3.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("main thread exit!");
    }
}
```

运行结果表明，通过简单的几行代码，就实行了一个锁的所有功能。
根据JUC（Java Util Concurrency）作者的建议，AQS的使用方法要遵循上面这个模式。一是使用一个内部类Sync来继承AQS，并实现AQS的相关方法，一般是tryAcquire和tryRelease（排它锁），或者tryAcquireShared和tryReleaseShared（共享锁）；二是在内部使用一个代理模式来实现锁的功能，这样做的好处是可以让暴露出的同步、互斥方法名由程序员自行决定，例如各种锁可以使用lock、unlock，Semaphore可以使用acquire和release，CountDownLatch可以使用await和countDown。

## 4.2 AQS基本原理

要实现一个同步器，需要三个条件：
\1. 一个同步状态值，并可以原子化的操作这个状态值。显然，我们可以使用上一篇讲到的CAS方法来操作状态值；
\2. 阻塞线程和解除阻塞线程的机制，可以用LockSupport来实现；
\3. 维持一个阻塞线程的队列，并在队列的每个节点中存储线程的状态等信息。
AQS同时满足了这三个条件，首先，它提供了如下的状态值，以及相应的操作方法：

```text
private volatile int state;

protected final int getState() {
    return state;
}

protected final void setState(int newState) {
    state = newState;
}

protected final boolean compareAndSetState(int expect, int update) {
    // See below for intrinsics setup to support this
    return unsafe.compareAndSwapInt(this, stateOffset, expect, update);
}
```

state是一个volatile int类型，除了getter和setter方法外，还提供了一个CAS方法，提供原子化的比较更新操作。一般来说，AQS认为state为0时，同步器处于释放状态，多个线程此刻可以竞争获取同步器；state不等于0时，同步器处于已获取状态，后续线程需进入队列，等待同步器（可重入的同步器允许获取同步器的线程再次进入同步器，并使用state进行计数）。当然，很多情况下，程序员也可自己定义state的值的含义，特别是在实现读写锁时，需要将state一分为二的用。
其次，LockSupport提供了阻塞和解除阻塞的功能。因此，所有同步器的阻塞操作其实都是基于LockSupport的，也就是基于Unsafe的park和unpark方法的。
第三，AQS内部提供了一个Node类型，它是用来形成“线程等待队列”的节点类型，以及一个由Node类型组成的队列。此队列的原理留待后续章节细说。

## 4.3 继承AQS时需要重写的方法

从上面的例子中可以看出，通过继承时重写了两个方法tryAcquire和tryRelease，就可以实现一个具体的同步器。通过研究AQS的原理可以得知，它将一些复杂的操作封装在自己内部，留待继承者重写的方法仅有以下5个（除去构造函数）：
\1. tryAcquire

```text
protected boolean tryAcquire(int arg) {
    throw new UnsupportedOperationException();
}
```

此方法是用来在多个线程竞争同步器时调用，作为AQS中acquire方法的第一个部分。若tryAcquire返回true，表明此线程获取了同步器；否则表明此线程没有获取同步器，而要进入队列等待同步器。在重写此方法时，仅需获取state的值，并通过CAS设置state的值，若成功则说明本线程竞争成功，否则说明线程竞争失败。
\2. tryRelease

```text
protected boolean tryRelease(int arg) {
    throw new UnsupportedOperationException();
}
```

此方法是用来释放同步器时调用，作为AQS中release方法的第一个部分。若tryRelease返回true，则表明当前线程可以正常释放同步器；否则不做其他操作。在重写此方法时，需要获取state的值，进行状态判断，然后依据具体情况将其设置为另一个值（一般设置为0）即可。
\3. tryAcquireShared

```text
protected int tryAcquireShared(int arg) {
    throw new UnsupportedOperationException();
}
```

此方法与tryAcquire非常类似，不同的是它被用来实现共享锁时调用。由于共享锁允许多个线程同时获取同步器，而且在释放时也可以同时释放多个线程。因此在重写tryAcquireShared时要特别注意state的定义和读写方法。
\4. tryReleaseShared

```text
protected boolean tryReleaseShared(int arg) {
    throw new UnsupportedOperationException();
}
```

此方法与tryRelease类似，不同的是它也被用来实现共享锁时调用。由于共享锁的特性，重写此方法时也要注意state的定义和读写方法。
\5. isHeldExclusively

```text
protected boolean isHeldExclusively() {
    throw new UnsupportedOperationException();
}
```

此方法在需要实现排它锁的Condition时重写。

## 4.4 排它锁的原理与流程

前面我们已经提供了一个最简单的排它锁SimpleLock，然而它的实现细节没有讲，下面我用两个图来说明，第一个图是lock的流程框架：

![img](https://pic4.zhimg.com/80/v2-93282e02335e3221f6e4584f3223db67_hd.png)

AQS已经把排它锁的加锁框架全部搭建好了，程序员只需要重写tryAcquire方法即可完成整个的功能。在看流程图的时候，要设想多个线程同时进入这个流程的样子。

第二个图是unlock的流程框架：

![img](https://pic1.zhimg.com/80/v2-031b2c930b5cbf41c0a6a9d293de83a8_hd.png)

同样，AQS已经把解锁的框架全部搭建好了，程序员只需重写tryRelease方法即可实现排它锁的解锁。值得注意的是，排它锁被解锁后，仅有一个被阻塞的线程能够获得锁，其他线程依然在队列中等待。



## 4.5 初试共享锁

AQS不仅提供了排它锁，同时也提供了共享锁的框架。对于排它锁和共享锁，并没有明确的定义，此处根据本人自己的理解，给出一个定义。排它锁，即在一个时刻只有一个线程可以获取的锁，其他线程的加锁方法会被阻塞，直至拥有锁的线程释放该锁为止。共享锁，即在一个时刻允许多个线程同时获取的锁。根据场景的不同，可以构建多种不同类型的共享锁，有的共享锁允许定量的（n个）线程拥有锁，此外的线程在加锁时依然会被阻塞，每当一个线程释放一次锁，则后续的一个线程可以竞争获取该锁（例如Semaphore）；有的共享锁会阻塞所有的线程，但一旦执行某种释放操作，则所有被阻塞的线程会被同时唤醒（例如CountDownLatch）；有的共享锁需要与一个排它锁配合，实现对文件读写的各种同步（ReentrantReadWriteLock）。这些具体的同步器会在后续的章节或文章中介绍。
根据SimpleLock，我们再试着实现一个最简单的共享锁SimpleSharedLock，代码如下：

```text
public class SimpleSharedLock {
    private static class Sync extends AbstractQueuedSynchronizer {
        @Override
        protected int tryAcquireShared(int arg) {
            return compareAndSetState(0, 1) ? 1 : -1;
        }

        @Override
        protected boolean tryReleaseShared(int arg) {
            setState(0);
            return true;
        }

        protected Sync() {
            super();
        }
    }

    private final Sync sync = new Sync();

    public void lock() {
        sync.acquireShared(1);
    }

    public void unlock() {
        sync.releaseShared(1);
    }

    private static class MyThread extends Thread {
        private final String name;
        private final SimpleSharedLock lock;

        private MyThread(String name, SimpleSharedLock lock) {
            this.name = name;
            this.lock = lock;
        }

        @Override
        public void run() {
            try {
                lock.lock();
                System.out.println(name + " get the lock");
                TimeUnit.SECONDS.sleep(2);
            } catch (InterruptedException e) {
                e.printStackTrace();
            } finally {
                lock.unlock();
                System.out.println(name + " release the lock");
            }
        }
    }

    public static void main(String[] args) {
        final SimpleSharedLock lock = new SimpleSharedLock();
        MyThread t1 = new MyThread("t1", lock);
        MyThread t2 = new MyThread("t2", lock);
        MyThread t3 = new MyThread("t3", lock);
        t1.start();
        t2.start();
        t3.start();
        try {
            t1.join();
            t2.join();
            t3.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("main thread exit!");
    }
}
```

运行此段代码后发现很奇怪，虽然我们重写了tryAcquireShared和tryReleaseShared方法，但是SimpleSharedLock依然像一个排它锁，线程既不能同时拥有锁，也不能在释放时同时获取锁。这是因为我们对共享锁的流程以及AQS中state的含义依然不清楚的原因。

## 4.6 共享锁的原理与流程

首先明白一点：tryAcquireShared方法与tryAcquire方法不同，它返回的不是布尔值，而是整形。返回值为正表明该线程获取了锁，为负表明此线程获取锁失败，应该被阻塞，为0表明该锁尚未被获取。共享锁的加锁流程如下：

![img](https://pic2.zhimg.com/80/v2-3d91010766834062aab2aa163debba71_hd.png)

与排它锁的lock流程相比，共享锁的流程多了几步，即从setHeadAndPropagate，doReleaseShared和unparkSuccessor。这几步是在当前节点已经被唤醒后，将解锁状态向后传递的过程。本线程将唤醒下一个阻塞的共享线程（被共享锁阻塞的线程），然后此共享线程再唤醒下一个共享线程，这样直至所有共享线程都被唤醒。

共享锁的解锁流程如下：

![img](https://pic1.zhimg.com/80/v2-d1d73511fb75e305c85e1d2b54f5d3a0_hd.png)

我们会发现解锁流程并不复杂，且使用的doReleaseShared方法在加锁流程中已经使用过了。

现在我们再来回答，为什么在SimpleSharedLock中，解锁方法没有同时唤醒所有线程？原因就在于，重写的tryAcquireShared方法没有在加锁框架中发挥应有的作用，它在被唤醒后的第一次调用中（也就是在setHeadAndPropagate之前的那一次调用中）重新将state设置为1，也就是锁被获取了。因此下一个被唤醒的线程没有能够通过tryAcquireShared的检测从而重新被阻塞。若要弄清所有细节，你必须阅读AQS的源代码。

至此我们明白了，对state的查询和操作是设计一种共享锁的关键。



## 4.7 一次唤醒所有阻塞线程的共享锁

假设有这样一种共享锁，它天生就阻塞所有调用lock的线程，但一旦有其他线程调用unlock，则唤醒所有线程，那么应该这样设计：

```text
public class SimpleSharedLock2 {
    private static class Sync extends AbstractQueuedSynchronizer {
        @Override
        protected int tryAcquireShared(int arg) {
            return getState() == 0 ? 1 : -1;
        }

        @Override
        protected boolean tryReleaseShared(int arg) {
            for (; ; ) {
                if (compareAndSetState(1, 0)) {
                    return true;
                }
            }
        }

        protected Sync() {
            setState(1);
        }
    }

    private final Sync sync = new Sync();

    public void lock() {
        sync.acquireShared(1);
    }

    public void unlock() {
        sync.releaseShared(1);
    }

    private static class MyThread extends Thread {
        private final String name;
        private final SimpleSharedLock2 lock;

        private MyThread(String name, SimpleSharedLock2 lock) {
            this.name = name;
            this.lock = lock;
        }

        @Override
        public void run() {
            try {
                System.out.println(name + " begin to get lock");
                lock.lock();
                System.out.println(name + " get the lock");
                TimeUnit.SECONDS.sleep(2);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        final SimpleSharedLock2 lock = new SimpleSharedLock2();
        MyThread t1 = new MyThread("t1", lock);
        MyThread t2 = new MyThread("t2", lock);
        MyThread t3 = new MyThread("t3", lock);
        t1.start();
        t2.start();
        t3.start();
        try {
            TimeUnit.SECONDS.sleep(5);
            System.out.println("main thread invoke unlock ");
            lock.unlock();
            t1.join();
            t2.join();
            t3.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("main thread exit!");
    }
}
```

运行此代码，我们会发现，这种共享锁果然符合设计。但是，它是一种一次性的锁，用完之后，由于tryReleaseShared不能将state的值重新设置为其他值，因此以后该锁就失效了。这个锁其实就是简化版的CountDownLatch，我会在后续文章中详细介绍它的使用。

## 4.8 拥有多个许可证的共享锁

SimpleSharedLock2能够一次释放多个阻塞线程，现在我们设计一种共享锁，它允许n个线程同时获取锁，就仿佛该锁有n个许可证，每个许可证允许一个线程获取锁。释放时，每个线程会还回一个许可证让后续的线程竞争。

```text
public class SimpleSharedLock3 {
    private static class Sync extends AbstractQueuedSynchronizer {
        final int getPermits() {
            return getState();
        }

        @Override
        protected int tryAcquireShared(int arg) {
            for (; ; ) {
                int available = getState();
                int remaining = available - arg;
                if (remaining < 0 ||
                        compareAndSetState(available, remaining))
                    return remaining;
            }
        }

        @Override
        protected boolean tryReleaseShared(int arg) {
            for (; ; ) {
                int available = getState();
                int remaining = available + arg;
                if (compareAndSetState(available, remaining)) {
                    return true;
                }
            }
        }

        protected Sync(int permits) {
            setState(permits);
        }
    }

    public SimpleSharedLock3(int permits) {
        sync = new Sync(permits);
    }

    private final Sync sync;

    public void lock() {
        sync.acquireShared(1);
    }

    public void unlock() {
        sync.releaseShared(1);
    }

    public int getPermits() {
        return sync.getPermits();
    }

    private static class MyThread extends Thread {
        private final String name;
        private final SimpleSharedLock3 lock;

        private MyThread(String name, SimpleSharedLock3 lock) {
            this.name = name;
            this.lock = lock;
        }

        @Override
        public void run() {
            try {
                lock.lock();
                System.out.println(name + " get the lock, permits = " + lock.getPermits());
                TimeUnit.SECONDS.sleep(2);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
    }

    public static void main(String[] args) {
        //给予此锁2个许可
        final SimpleSharedLock3 lock = new SimpleSharedLock3(2);
        MyThread t1 = new MyThread("t1", lock);
        MyThread t2 = new MyThread("t2", lock);
        MyThread t3 = new MyThread("t3", lock);
        t1.start();
        t2.start();
        t3.start();
        try {
            TimeUnit.SECONDS.sleep(5);
            lock.unlock();
            System.out.println("main thread invoke unlock, permits = " + lock.getPermits());
            t1.join();
            t2.join();
            t3.join();
        } catch (InterruptedException e) {
            e.printStackTrace();
        }
        System.out.println("main thread exit!");
    }
}
```

运行结果表明，这种锁符合设计，它其实就是一个简化版的Semaphore。

# 5. 可重入锁ReentrantLock

了解了AQS的原理之后，再来看RentrantLock就非常简单了。从实现原理上来说，它与我们之前设计的SimpleLock很类似。但是作为Java Concurrency包中使用最频繁的锁，它还有可重入性、可中断性、公平策略和Condition等特性。RentrantLock是一个排它锁，因此当一个线程获取锁之后，其他线程只能阻塞。但是若拥有锁的线程重复调用lock方法，依然可以重复进入锁。被RentrantLock阻塞的线程可以被中断，并抛出一个InterruptedException异常。

## 5.1 RentrantLock

与synchronize关键字相比，ReentrantLock更加灵活，唯一的不足是使用时必须使用try-finally模式来进行加解锁，下面是使用它的一个简单代码：

```text
public class ReentrantLockExam {
    public static void main(String[] args) {
        final ReentrantLock lock = new ReentrantLock();
        ExecutorService service = Executors.newCachedThreadPool();
        for (int i = 0; i < 2; i++) {
            service.execute(new Runnable() {
                @Override
                public void run() {
                    try {
                        System.out.println(Thread.currentThread() + " ready to get lock");
                        lock.lock();
                        System.out.println(Thread.currentThread()+" get the lock");
                        for (int j = 0; j < 5; j++) {
                            System.out.println(Thread.currentThread()+" is running, number = "+j);
                            TimeUnit.MILLISECONDS.sleep(500);
                        }
                    } catch (InterruptedException e) {
                        e.printStackTrace();
                    } finally {
                        lock.unlock();
                        System.out.println(Thread.currentThread()+" unlock");
                    }
                }
            });
        }
        service.shutdown();
    }
}
```

代码中，两个线程竞争一把RentrantLock锁，得到锁的线程持续运行，直至解锁后，另一个线程才等得到锁并运行。若我们将lock方法连续调用两次，程序依然能够正常运行；将unlock方法也连续调用两次，线程也能够正常解锁。每lock一次，拥有该锁的线程的计数增加1，每unlock一次，计数减少1，当AQS的state为0时，所有线程可以竞争锁。

## 5.2 Condition

Condition是与RentrantLock配合使用，来实现synchronize中的wait、notify功能的一个接口，其具体实现类为AQS中的ConditionObject。配合使用的方法如下所示（此示例来自JDK文档，本文做了扩充）：

```text
public class ConditionExam {
    public static void main(String[] args) {
        ExecutorService service = Executors.newCachedThreadPool();
        final BoundedBuffer buffer = new BoundedBuffer();
        service.execute(new Runnable() {
            @Override
            public void run() {
                try {
                    for (int i = 0; i < 1000; i++) {
                        String str = "string" + i;
                        buffer.put(str);
                        System.out.println(Thread.currentThread() + " put " + str);
                        TimeUnit.MILLISECONDS.sleep(50);
                    }
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
        service.execute(new Runnable() {
            @Override
            public void run() {
                try {
                    for (int i = 0; i < 1000; i++) {
                        String str = (String) buffer.take();
                        System.out.println(Thread.currentThread() + " take " + str);
                        TimeUnit.MILLISECONDS.sleep(50);
                    }
                } catch (InterruptedException e) {
                    e.printStackTrace();
                }
            }
        });
        service.shutdown();
    }

    private static class BoundedBuffer {
        final Lock lock = new ReentrantLock();
        final Condition notFull = lock.newCondition();
        final Condition notEmpty = lock.newCondition();

        final Object[] items = new Object[100];
        int putptr, takeptr, count;

        public void put(Object x) throws InterruptedException {
            lock.lock();
            try {
                while (count == items.length)
                    notFull.await();
                items[putptr] = x;
                if (++putptr == items.length) putptr = 0;
                ++count;
                notEmpty.signal();
            } finally {
                lock.unlock();
            }
        }

        public Object take() throws InterruptedException {
            lock.lock();
            try {
                while (count == 0)
                    notEmpty.await();
                Object x = items[takeptr];
                if (++takeptr == items.length) takeptr = 0;
                --count;
                notFull.signal();
                return x;
            } finally {
                lock.unlock();
            }
        }
    }
}
```

在上面的代码中，使用一个ReentrantLock以及它的两个Condition实现了对一个原生数组的安全并发访问，其中notFull条件用来控制数组不会溢出，notEmpty条件控制数组不会为空时还被取出元素。

# 6. 读写锁ReentrantWriteReadLock

读写锁ReentrantWriteReadLock的用法比较难以理解，因此用一个大家都熟悉的场景来说明。假设一个班级有一块黑板（共享资源），有多个老师都需要在黑板上书写。老师在写之前，先要获取写锁（writeLock），在写的时候其他的老师和学生都不能在黑板上写或者读，老师写完之后，释放写锁。学生在读黑板之前，先要获取读锁（readLock），多个学生可以同时获取读锁，因此多个学生可以同时读取黑板上的内容，在读的时候其他老师不能在黑板上写，学生读完之后，释放读锁。直至所有学生都释放完读锁，才能够由老师获取写锁。例子代码如下：

```text
public class ReentrantReadWriteLockExam {
    public static Random rand = new Random(System.currentTimeMillis());

    public static void main(String[] args) {
        ReentrantReadWriteLock lock = new ReentrantReadWriteLock();
        StringBuilder blackboard = new StringBuilder(100);

        ExecutorService service= Executors.newCachedThreadPool();
        service.execute(new Teacher(lock, "Chinese Teacher", blackboard));
        service.execute(new Teacher(lock, "English Teacher", blackboard));
        service.execute(new Student(lock,"Wang",blackboard));
        service.execute(new Student(lock,"Li",blackboard));
        service.execute(new Student(lock,"Zhang",blackboard));
        service.shutdown();
    }

    private static class Teacher extends Thread {
        final private ReentrantReadWriteLock lock;
        final private String name;
        final private StringBuilder blackboard;
        private AtomicInteger id = new AtomicInteger(0);

        private Teacher(ReentrantReadWriteLock lock, String name, StringBuilder blackboard) {
            this.lock = lock;
            this.name = name;
            this.blackboard = blackboard;
        }

        @Override
        public void run() {
            for (int i = 0; i < 1000; i++) {
                try {
                    lock.writeLock().lock();
                    System.out.println(name + " get write lock");
                    blackboard.delete(0, 99).append(name + " has written on the blackboard, number = " + id.getAndIncrement());
                    System.out.println(name + " write content:" + blackboard);
                    TimeUnit.MILLISECONDS.sleep(rand.nextInt(500));
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } finally {
                    lock.writeLock().unlock();
                    System.out.println(name + " release write lock");
                }
            }
        }
    }

    private static class Student extends Thread {
        final private ReentrantReadWriteLock lock;
        final private String name;
        final private StringBuilder blackboard;

        private Student(ReentrantReadWriteLock lock, String name, StringBuilder blackboard) {
            this.lock = lock;
            this.name = name;
            this.blackboard = blackboard;
        }

        @Override
        public void run() {
            for (int i = 0; i < 1000; i++) {
                try {
                    lock.readLock().lock();
                    System.out.println(name + " get read lock");
                    System.out.println(name + " read the blackboard:" + blackboard);
                    TimeUnit.MILLISECONDS.sleep(rand.nextInt(500));
                } catch (InterruptedException e) {
                    e.printStackTrace();
                } finally {
                    lock.readLock().unlock();
                    System.out.println(name+" release the read lock");
                }
            }
        }
    }
}
```

总结规则如下：
1.写锁是排它锁，一旦被获取，其他竞争写锁的线程被阻塞，其他竞争读锁的线程也被阻塞；
2.写锁被释放后，其他的线程可以竞争写锁或者读锁；
3.读锁是共享锁，它可以同时被多个线程获取，但是读锁和写锁是不能同时被不同的线程获取的；
4.所有的读锁被释放后，其他的线程可以竞争写锁。

# 7. 小结

为了提供区别于synchronize关键的阻塞机制，Java提供了锁包。锁包的核心类是AQS，它提供了排它锁和共享锁的流程框架，通过继承此类，可以构造出各种类型的同步器。可重入锁ReentrantLock是使用最广泛的排它锁，除了拥有可重入特性外，它还提供了Condition用来模拟Object的wait和notify操作。读写锁ReentrantWriteReadLock提供了对共享资源的读写保护，可以被方便的用于各类共享资源的访问控制。

编辑于 2017-06-24