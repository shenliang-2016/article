# Java Concurrency代码实例之八-CopyOnWriteArrayList

[![Alex Wang](https://pic4.zhimg.com/7b8e72c144e581881f769b179b98b309_xs.jpg)](https://www.zhihu.com/people/wang-du-du-43-1)

[Alex Wang](https://www.zhihu.com/people/wang-du-du-43-1)

高级工程师，Coder，Teamleader

15 人赞同了该文章

本文的读者应该是已经掌握了基本的Java多线程开发技巧，但不熟悉Java
Concurrency包的程序员。本文是本系列的第八篇文章，前七篇文章请看这里：

[Java Concurrency代码实例之一执行者与线程池](https://zhuanlan.zhihu.com/p/26724352)

[Java Concurrency代码实例之二并发队列](https://zhuanlan.zhihu.com/p/27148381)

[Java Concurrency代码实例之三原子变量](https://zhuanlan.zhihu.com/p/27338395)

[Java Concurrency代码实例之四-锁](https://zhuanlan.zhihu.com/p/27546231)

[Java Concurrency代码实例之五-同步工具](https://zhuanlan.zhihu.com/p/27829595)

[Java Concurrency代码实例之六-ConcurrentHashMap](https://zhuanlan.zhihu.com/p/28618718)

[Java Concurrency代码实例之七-ConcurrentSkipListMap](https://zhuanlan.zhihu.com/p/29451959)

## 1. 前言

按照用途与特性，Concurrency包中包含的工具被分为六类（外加一个工具类TimeUnit），即：

\1. 执行者与线程池

\2. 并发队列

\3. 同步工具

\4. 并发集合

\5. 锁

\6. 原子变量

本系列的前五篇文章分别介绍这六类中的一类。自第六篇起，一次仅介绍一个具体类。本文介绍的是并发集合中比较简单的一个类CopyOnWriteArrayList。从名称就可以看出来，它是ArrayList对应的并发类。此类的思想是，当仅有读操作时：进行无锁的访问，每当有写操作时，将内部数组拷贝一份，对拷贝的部分进行写操作，然后将其赋值回来。这种算法显然能够保证多线程安全，但是可知写操作会非常耗时，因此此类仅适合于读操作非常多，而写操作非常少的场景。与此类似的还有一个类CopyOnWriteArraySet。

## 2. 内部方法简介

## 2.1 内部属性和初始化

先看它的内部属性和一些初始化方法：

```java
/** The lock protecting all mutators */
transient final ReentrantLock lock = new ReentrantLock();

/** The array, accessed only via getArray/setArray. */
private volatile transient Object[] array;

/**
 * Gets the array.  Non-private so as to also be accessible
 * from CopyOnWriteArraySet class.
 */
final Object[] getArray() {
    return array;
}

/**
 * Sets the array.
 */
final void setArray(Object[] a) {
    array = a;
}

/**
 * Creates an empty list.
 */
public CopyOnWriteArrayList() {
    setArray(new Object[0]);
}
public CopyOnWriteArrayList(Collection<? extends E> c) {
    Object[] elements = c.toArray();
    // c.toArray might (incorrectly) not return Object[] (see 6260652)
    if (elements.getClass() != Object[].class)
        elements = Arrays.copyOf(elements, elements.length, Object[].class);
    setArray(elements);
}

/**
 * Creates a list holding a copy of the given array.
 *
 * @param toCopyIn the array (a copy of this array is used as the
 *        internal array)
 * @throws NullPointerException if the specified array is null
 */
public CopyOnWriteArrayList(E[] toCopyIn) {
    setArray(Arrays.copyOf(toCopyIn, toCopyIn.length, Object[].class));
}
```

从上面的代码可以看出：lock是一个用来保护写操作的锁，array是存储对象的原生数组，array是volatile和transient，这表明它具有多线程可见性，因此array的getter和setter方法不必使用synchronized修饰。

CopyOnWriteArrayList有三个构造函数，无参的构造函数仅仅new一个Object[0]数组赋值给array，其他两个都是将参数中的数组拷贝到array中。

## 2.2 各种拷贝方法

在CopyOnWriteArrayList的许多内部方法中，都使用了Arrays.copyOf()方法或者System.arraycopy()方法，而Arrays.copyOf()内部也调用了System.arraycopy()方法，因此有必要先介绍一下这两个方法。

Arrays类是操作原生数组的工具类，主要包括sort、search、equals、fill和copyOf等多种方法。CopyOnWriteArrayList中大量使用了copyOf方法，因为这种方法比使用数组元素一一赋值要性能高很多，各种copyOf方法的最终形式如下：

```java
public static <T,U> T[] copyOf(U[] original, int newLength, Class<? extends T[]> newType) {
    T[] copy = ((Object)newType == (Object)Object[].class)
        ? (T[]) new Object[newLength]
        : (T[]) Array.newInstance(newType.getComponentType(), newLength);
    System.arraycopy(original, 0, copy, 0,
                     Math.min(original.length, newLength));
    return copy;
}
```

该方法就是进行一个数组的类型转换，然后调用System.arraycopy()方法：

```java
public static native void arraycopy(Object src,  int  srcPos,
                                    Object dest, int destPos,
                                    int length);
```

System.arraycopy()是一个native方法，它是直接进行内存块之间的赋值，所以比一般的赋值语句要快很多，基本上是Java所能达到最快的数组赋值方法了，因此CopyOnWriteArrayList随处都可以看到使用System.arraycopy()进行赋值的语句，这是为了保证高效率。

## 2.3 get和indexOf方法

CopyOnWriteArrayList的get方法使用下标从数组中取出对应元素，由于array是使用volatile修饰的，且所有写入操作都会生成一个新的array，因此get方法不用加锁了，效率非常高。

indexOf方法从CopyOnWriteArrayList探测出某个对象的下标值，基于同样的理由，这个方法也是无锁的，但是它是靠一一比对来得到下标值的，因此它的时间消耗是O(n)的。

```java
/**
 * static version of indexOf, to allow repeated calls without
 * needing to re-acquire array each time.
 * @param o element to search for
 * @param elements the array
 * @param index first index to search
 * @param fence one past last index to search
 * @return index of element, or -1 if absent
 */
private static int indexOf(Object o, Object[] elements,
                           int index, int fence) {
    if (o == null) {
        for (int i = index; i < fence; i++)
            if (elements[i] == null)
                return i;
    } else {
        for (int i = index; i < fence; i++)
            if (o.equals(elements[i]))
                return i;
    }
    return -1;
}
```

contains方法也是靠调用indexOf方法来完成功能的。

## 2.4 add、set和remove方法

这三个方法都对数组进行了写操作，因此它们遵循了COW（Copy on Write）的原则，每写一个元素都要拷贝整个数组一次。

先看add方法：

```java
public void add(int index, E element) {
    final ReentrantLock lock = this.lock;
    lock.lock();
    try {
        Object[] elements = getArray();
        int len = elements.length;
        if (index > len || index < 0)
            throw new IndexOutOfBoundsException("Index: "+index+
                                                ", Size: "+len);
        Object[] newElements;
        int numMoved = len - index;
        if (numMoved == 0)
            newElements = Arrays.copyOf(elements, len + 1);
        else {
            newElements = new Object[len + 1];
            System.arraycopy(elements, 0, newElements, 0, index);
            System.arraycopy(elements, index, newElements, index + 1,
                             numMoved);
        }
        newElements[index] = element;
        setArray(newElements);
    } finally {
        lock.unlock();
    }
}
```

首先加锁，然后将数组分为两段，index之前的和之后的，对index所在的点进行赋值，然后分两次拷贝前后段数组到新的数组中，最后将新的数组赋值给array。

Set方法如出一辙，只不过set方法不会改变数组的长度，而且仅拷贝数组一次。

Remove方法是get方法的逆操作，也是加锁，并将数组分为两段，移除index所在的元素，然后分别将前后两段拷贝到新数组中，最后将新的数组赋值给array。

## 3. 效率比较

CopyOnWriteArrayList的思想非常简单，其内部方法的实现也非常简单，本章讨论一下它的用法和效率。

## 3.1 要使用拷贝而不是赋值来初始化

CopyOnWriteArrayList每add或者set一次，就要将整个数组拷贝一次，因此一定要使用拷贝整个原生数组的方法来初始化该类。例如：

```java
public class CopyOnWriteArrayListExam {
    private static final int TEST_NUM = 200000;
    public static void main(String[] args) {
        long start = System.currentTimeMillis();
        CopyOnWriteArrayList<Integer> list = new CopyOnWriteArrayList<>();
        for (int i = 0; i < TEST_NUM; i++) {
            list.add(i);
        }
        long end = System.currentTimeMillis();
        System.out.println("time span = "+(end-start));

        list.clear();
        start = System.currentTimeMillis();
        Integer[] integers = new Integer[TEST_NUM];
        for (int i = 0; i < TEST_NUM; i++) {
            integers[i]=i;
        }
        list = new CopyOnWriteArrayList<>(integers);
        end = System.currentTimeMillis();
        System.out.println("time span = "+(end-start));
    }
}
```

运行结果：

time span = 16162

time span = 0

## 3.2 与Collections.synchronizedList的比较

Collections.synchronizedList()方法可以将一个普通集合包装为一个多线程安全的集合，其实就是为集合的每个方法加上了锁。下面比较一下CopyOnWriteArrayList和Collections.synchronizedList在多个线程同时读取时的性能。代码如下：注意切换其中一行的注释就可以创建两种不同的集合：

```java
public class CopyOnWriteArrayListExam2 {
    private static final int TEST_NUM = 100000;
    public static void main(String[] args) throws InterruptedException {
        long start = System.currentTimeMillis();
        Integer[] integers = new Integer[TEST_NUM];
        for (int i = 0; i < TEST_NUM; i++) {
            integers[i] = i;
        }
        CopyOnWriteArrayList<Integer> list = new CopyOnWriteArrayList<>();
//        List<Integer> list = Collections.synchronizedList(new ArrayList<Integer>());
        list.addAll(Arrays.asList(integers));
        ExecutorService service = Executors.newCachedThreadPool();
        for (int i = 0; i < 100; i++) {
            service.execute(new Getter(list));
        }
        service.shutdown();
        service.awaitTermination(1, TimeUnit.DAYS);
        long end = System.currentTimeMillis();
        System.out.println("time span = " + (end - start));
    }

    private static class Getter implements Runnable {
        final List<Integer> list ;
        private static Random rand = new Random(System.currentTimeMillis());
        private Getter(List<Integer> list) {
            this.list = list;
        }

        @Override
        public void run() {
            for (int i = 0; i < TEST_NUM; i++) {
                list.get(rand.nextInt(TEST_NUM));
            }
        }
    }
}
```

100个线程同时随机读取一个包含10万个元素的队列，性能如下：

Collections.synchronizedList：

time span = 552

CopyOnWriteArrayList：

time span = 608

这说明，对于随机读取来说，这两种集合的性能差不多，没有数量级上的差异。

再来比较一下同时读取和写入的情况，代码被修改为90个线程读取，10个线程写入：

```java
public class CopyOnWriteArrayListExam3 {
    private static final int TEST_NUM = 100000;
    public static void main(String[] args) throws InterruptedException {
        long start = System.currentTimeMillis();
        Integer[] integers = new Integer[TEST_NUM];
        for (int i = 0; i < TEST_NUM; i++) {
            integers[i] = i;
        }
//        CopyOnWriteArrayList<Integer> list = new CopyOnWriteArrayList<>();
        List<Integer> list = Collections.synchronizedList(new ArrayList<Integer>());
        list.addAll(Arrays.asList(integers));
        ExecutorService service = Executors.newCachedThreadPool();
        for (int i = 0; i < 90; i++) {
            service.execute(new Getter(list));
        }
        for (int i = 0; i < 10; i++) {
            service.execute(new Putter(list));
        }
        service.shutdown();
        service.awaitTermination(1, TimeUnit.DAYS);
        long end = System.currentTimeMillis();
        System.out.println("time span = " + (end - start));
        System.out.println(list.size());
    }

    private static class Getter implements Runnable {
        final List<Integer> list ;
        private static Random rand = new Random(System.currentTimeMillis());
        private Getter(List<Integer> list) {
            this.list = list;
        }

        @Override
        public void run() {
            for (int i = 0; i < TEST_NUM; i++) {
                list.get(rand.nextInt(TEST_NUM));
            }
        }
    }

    private static class Putter implements Runnable {
        final List<Integer> list ;
        private static Random rand = new Random(System.currentTimeMillis());
        private Putter(List<Integer> list) {
            this.list = list;
        }

        @Override
        public void run() {
            for (int i = 0; i < TEST_NUM; i++) {
                list.add(rand.nextInt(TEST_NUM));
            }
        }
    }
}
```

性能如下：

Collections.synchronizedList：

time span = 637

CopyOnWriteArrayList：

time span = sorry，我没有耐心等到执行完毕。

这说明，在有写入线程的情况下，性能会非常非常的糟糕。

## 4. 小结

CopyOnWriteArrayList是ArrayList的并发类，它实现了“写时拷贝”的思想，每当要进行写入操作时，加锁并复制内部数组，完成写入后替换原来的内部数组。在并发读取时，CopyOnWriteArrayList不需要加锁，因此性能较高，事实上我们与Collections.synchronizedList进行了对比，其性能是相似的。而每当有写入线程时，CopyOnWriteArrayList的效率会变得极低，远远低于Collections.synchronizedList。因此在选择CopyOnWriteArrayList时，必须要慎重考虑应用场景。

发布于 2017-10-04