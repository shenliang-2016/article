# Java Concurrency代码实例之六-ConcurrentHashMap

[![Alex Wang](https://pic4.zhimg.com/7b8e72c144e581881f769b179b98b309_xs.jpg)](https://www.zhihu.com/people/wang-du-du-43-1)

[Alex Wang](https://www.zhihu.com/people/wang-du-du-43-1)

高级工程师，Coder，Teamleader

60 人赞同了该文章

本文的读者应该是已经掌握了基本的Java多线程开发技巧，但不熟悉Java
Concurrency包的程序员。本文是本系列的第六篇文章，前五篇文章请看这里：

[Java Concurrency代码实例之一执行者与线程池](https://zhuanlan.zhihu.com/p/26724352)

[Java Concurrency代码实例之二并发队列](https://zhuanlan.zhihu.com/p/27148381)

[Java Concurrency代码实例之三原子变量](https://zhuanlan.zhihu.com/p/27338395)

[Java Concurrency代码实例之四-锁](https://zhuanlan.zhihu.com/p/27546231)

[Java Concurrency代码实例之五-同步工具](https://zhuanlan.zhihu.com/p/27829595)

## 1. 前言

按照用途与特性，Concurrency包中包含的工具被分为六类（外加一个工具类TimeUnit），即：

\1. 执行者与线程池

\2. 并发队列

\3. 同步工具

\4. 并发集合

\5. 锁

\6. 原子变量

由于前五篇文章一次介绍Concurrency包中的一整类特性，导致文章冗长，重点不突出，效果反而不好。因而自此以后，一篇仅介绍一个具体类。本文介绍的是并发集合中最常用的一个类ConcurrentHashMap。

## 2. 三大Map的区别

谈到ConcurrentHashMap，就不能不提它的前辈HashMap和Hashtable。

HashMap是Java中最常用的一个Map类了，它性能好、速度快，但不能保证线程安全，它可以使用null作为key或者value。

Hashtable是Java中最老的Map类，自JDK1.0版本就存在了，它是一个线程安全的Map类，其公有方法均使用synchronize关键字修饰，这表示在多线程操作时，每个线程在操作之前都会锁住整个map，待操作完成后才释放，这必然导致多线程时性能不佳。另外，Hashtable不能使用null作为key或者value。

ConcurrentHashMap是HashMap的并发类，它是线程安全的。与Hashtable相比，由于它大量使用了自旋等待、多segment等并发技术，使得并发操作时往往不需要锁住整个map，因此其多线程性能远超Hashtable。它也不能使用null作为key或者value。

## 3. HashMap原理概述

## 3.1 Hash函数与结构

HashMap是一个存储键值对<Key,Value>的集合，其内部的数据结构是一个原生数组，数组中的元素是单向链表的表头，每个链表中的数据元素是一个键值对。

键值对中的Key的hash值用来决定该键值对存储在数组中的位置，即数组的索引。所有相同hash值相同的键值对存储在一个单向链表中，如下图所示：



![img](https://pic1.zhimg.com/80/v2-ceb85c3165afa19c51c060b105348414_hd.png)



如上图所示，假设HashMap的hash函数就是Key % 10，则当一个键值对<106,Kx>被插入时，计算其hash值为6，则它应该被插入hash表的索引为6的单向链表的尾部。

这种结构的最大优点就是极大的降低了查询的时间开销。由于计算hash值是一个常量时间的消耗，与Map中存储的数值多少无关。而由于hash函数设计得比较好，以及后续将会提到的自动扩容和负载因子的影响，单向链表的长度会被控制在一个很小的长度，因此在HashMap中进行查询就是一个常量时间的开销，要远低于其他数据结构。

## 3.2 公有方法

HashMap中的公有方法是很少的，主要包括：

插入：put(K key, V value)和putAll(Map<? extends K, ? extends V> m)，分别用来插入一个键值对和一组键值对；

查询：containsKey(Object key)用来查询Map中是否包含key，containsValue(Object value)用来查询Map中是否包含value；

获取：get(Object key)，用来根据key获取value；

删除：remove(Object key)和clear()，分别用来删除一个键值对和清空Map；

长度：size()和isEmpty()。

## 3.3 三大集合与迭代子

除了以上方法以外，HashMap使用三大集合和三种迭代子来轮询其Key、Value和Entry对象，其使用方法如下所示：

```java
public class HashMapExam {
    public static void main(String[] args) {
        Map<Integer, String> map = new HashMap<>(16);
        for (int i = 0; i < 15; i++) {
            map.put(i, new String(new char[]{(char) ('A'+ i)}));
        }

        System.out.println("======keySet=======");
        Set<Integer> set = map.keySet();
        Iterator<Integer> iterator = set.iterator();
        while (iterator.hasNext()) {
            System.out.println(iterator.next());
        }

        System.out.println("======values=======");
        Collection<String> values = map.values();
        Iterator<String> stringIterator=values.iterator();
        while (stringIterator.hasNext()) {
            System.out.println(stringIterator.next());
        }

        System.out.println("======entrySet=======");
        for (Map.Entry<Integer, String> entry : map.entrySet()) {
            System.out.println(entry);
        }
    }
}
```



## 3.4 自动扩容

HashMap的hash表是一个原生数组Entry<K,V>[] table，这个原生数组的长度在HashMap创建时就被确定。程序员可以在构造函数中使用initialCapacity（初始容量，默认为16）和loadFactor（负载因子，默认为0.75）来指定HashMap的容量以及自动扩容的时机。

initialCapacity用来指定初始容量，HashMap的容量都是2的幂，若initialCapacity不是正好等于2的幂，则被向上取值为最近的一个2的幂值；loadFactor负载因子用来决定扩容的门槛值threshold，这个threshold就是容量与负载因子的乘积，当Map的size值大于threshold时，就会在put时检测是否进行扩容。当满足size大于threshold，且当前插入的Key在hash表中的相应位置已经有值（即该键值对要加入一个单向链表）时，Map会自动扩容为原来的2倍。

下面的例子展示了HashMap扩容的特性：

```java
public class HashMapExam2 {
    public static void main(String[] args) {
        Map<Integer, String> map = new HashMap<>(10);
        System.out.println("map initialize");
        showMap(map);
        for (int i = 0; i < 20; i++) {
            map.put(i, new String(new char[]{(char) ('A'+ i)}));
            System.out.println("put "+i);
            showMap(map);
        }
    }

    private static void showMap(Map<Integer, String> map) {
        try {
            Field f = HashMap.class.getDeclaredField("table");
            f.setAccessible(true);
            Map.Entry<Integer,String>[] table= (Map.Entry<Integer, String>[]) f.get(map);
            f = HashMap.class.getDeclaredField("threshold");
            f.setAccessible(true);
            int threshold = (int) f.get(map);
            System.out.println("map size = "+map.size()+",threshold = "+threshold+",length="+table.length);
        } catch (NoSuchFieldException e) {
            e.printStackTrace();
        } catch (IllegalAccessException e) {
            e.printStackTrace();
        }
    }

}
```



例子中使用反射获取了HashMap的Map.Entry<Integer,String>[] table和threshold变量。从运行结果可以看出，当Map为空时，table的长度为0；当put了一个元素时，table长度被初始化为16，而threshold为12；当put了17个元素时，table扩容为32，而threshold为24。

## 4. ConcurrentHashMap原理概述

此文章仅描述JDK1.7版本中的ConcurrentHashMap。与HashMap相比，虽然ConcurrentHashMap仅仅只增加了并发特性，但是其复杂度却极大的上升了。因为考虑到并发性能，它没有像Hashtable一样简单的给每个公有方法加上synchronize，而是利用了JUC包中提供的多种并发特性，在尽量保持性能的前提下实现了多线程安全。顺便说一句，《Java编程思想》的作者曾经提到，Hashtable类已经基本上可以废弃了，因为它能做的ConcurrentHashMap都能做，且性能更好。Hashtable类存在的意义可能就是用来面试吧。

## 4.1 ConcurrentHashMap与Hashtable之性能比较

为了验证以上的说法，写了一段代码来测试ConcurrentHashMap与Hashtable之性能比较：

```java
public class ConcurrentHashMapVsHashtable { private static int INPUT_NUMBER = 100000;

    public static void main(String[] args) throws InterruptedException {
//        Map<Integer, String> map = new Hashtable<>(12 * INPUT_NUMBER);
        Map<Integer, String> map = new ConcurrentHashMap<>(12 * INPUT_NUMBER);
        long begin = System.currentTimeMillis();
        ExecutorService service = Executors.newCachedThreadPool();
        for (int i = 0; i < 10; i++) {
            service.execute(new InputWorker(map, i));
        }
        service.shutdown();
        service.awaitTermination(1, TimeUnit.DAYS);
        long end = System.currentTimeMillis();
        System.out.println("span time = "+(end-begin)+", map size = "+map.size());
    }

    private static class InputWorker implements Runnable { private static Random rand = new Random(System.currentTimeMillis());
        private final Map<Integer,String> map;
        private final int flag;

        private InputWorker(Map<Integer, String> map, int begin) {
            this.map = map;
            this.flag = begin;
        }

        @Override public void run() {
            int input = 0;
            while (input < INPUT_NUMBER) {
                int x = rand.nextInt();
                if (!map.containsKey(x)) {
                    map.put(x, "Alex Wang" + x);
                    input++;
                }
            }
            System.out.println("InputWorker"+flag+" is over.");
        }
    }
}
```



这段代码中，生成10个子线程，每个线程向map中插入10万个键值对，然后计算耗时。ConcurrentHashMap平均耗时324ms，Hashtable平均耗时680ms，如此看来在我的普通PC机（i7，4核，16G内存）上，ConcurrentHashMap的耗时仅占Hashtable耗时的不到一半。

## 4.2 ConcurrentHashMap并发特性概述

本文仅描述JDK1.7中的ConcurrentHashMap。它采用多Segment（段）的结构来增加了并发性，如下图所示（为了便于描述，假设下图中的ConcurrentHashMap仅包含4个segment，每个segment的hash表初始容量为4）：

![img](https://pic2.zhimg.com/80/v2-f919c3afdcc95533e5697cb7d0fb6819_hd.png)



ConcurrentHashMap的并发思路就是将Map分为多个Segment，每个Segment含有一个类似HashMap中的hash表，每个hash表中的元素都是一个键值对Entry，此Entry可以组成一个单向链表。简单的说，ConcurrentHashMap是由多个hash表构成的双重hash表。

当要向图中插入数值时，分为三步：第一步计算key的hash值；第二步用此hash值的前n位（2的n次方即为segment的长度，注意segment的长度永远是2的n次方）截取后作为segment的索引；第三步找到该segment的hash表，用(tab.length-1)&hash作为hash表的索引，然后在此位置插入数值。

从图中查询数据时亦然，首先计算key的hash值，然后找到对应的segment，然后从segment的hash表中查到链表，再依次在链表中搜索相应的Entry。

## 4.3 Segment详解

## 4.3.1. Segment的索引与读取

ConcurrentHashMap类中包含三个与Segment相关的成员变量：

```java
/**
 * Mask value for indexing into segments. The upper bits of a
 * key's hash code are used to choose the segment.
 */ final int segmentMask;

/**
 * Shift value for indexing within segments.
 */ final int segmentShift;

/**
 * The segments, each of which is a specialized hash table.
 */ final Segment<K,V>[] segments;
```



其中segments是Segment的原生数组，此数组的长度可以在ConcurrentHashMap的构造函数中使用并发度参数指定，其默认值为DEFAULT_CONCURRENCY_LEVEL=16。segmentShift是用来计算segments数组索引的位移量，而segmentMask则是用来计算索引的掩码值。例如并发度为16时（即segments数组长度为16），segmentShift为32-4=28（因为2的4次幂为16），而segmentMask则为1111（二进制），索引的计算式如下：

```text
int j = (hash >>> segmentShift) & segmentMask;
```



考虑到并发环境下的性能和变量读写可见性，参考[https://tech.meituan.com/java-memory-reordering.html](https://link.zhihu.com/?target=https%3A//tech.meituan.com/java-memory-reordering.html)一文，在多线程并发访问一个共享变量时，为了保证逻辑的正确，可以采用以下方法：

\1. 加锁，性能最低，能保证原子性、可见性，防止指令重排；

\2. 使用volatile修饰，性能中等，能保证可见性，防止指令重排；

\3. 使用getObjectVolatile，性能最好，可防止指令重排；

因此ConcurrentHashMap选择了使用Unsafe（关于Unsafe的详细解释，请参考本系统的另一篇文章[Java Concurrency代码实例之三原子变量](https://zhuanlan.zhihu.com/p/27338395)）的getObjectVolatile来读取segments中的元素，相关代码如下：

```java
// Unsafe mechanics private static final sun.misc.Unsafe UNSAFE;
private static final long SBASE;
private static final int SSHIFT;
private static final long TBASE;
private static final int TSHIFT;
private static final long HASHSEED_OFFSET;
private static final long SEGSHIFT_OFFSET;
private static final long SEGMASK_OFFSET;
private static final long SEGMENTS_OFFSET;

static {
    int ss, ts;
    try {
        UNSAFE = sun.misc.Unsafe.getUnsafe();
        Class tc = HashEntry[].class;
        Class sc = Segment[].class;
        TBASE = UNSAFE.arrayBaseOffset(tc);
        SBASE = UNSAFE.arrayBaseOffset(sc);
        ts = UNSAFE.arrayIndexScale(tc);
        ss = UNSAFE.arrayIndexScale(sc);
        HASHSEED_OFFSET = UNSAFE.objectFieldOffset(
            ConcurrentHashMap.class.getDeclaredField("hashSeed"));
        SEGSHIFT_OFFSET = UNSAFE.objectFieldOffset(
            ConcurrentHashMap.class.getDeclaredField("segmentShift"));
        SEGMASK_OFFSET = UNSAFE.objectFieldOffset(
            ConcurrentHashMap.class.getDeclaredField("segmentMask"));
        SEGMENTS_OFFSET = UNSAFE.objectFieldOffset(
            ConcurrentHashMap.class.getDeclaredField("segments"));
    } catch (Exception e) {
        throw new Error(e);
    }
    if ((ss & (ss-1)) != 0 || (ts & (ts-1)) != 0)
        throw new Error("data type scale not a power of two");
    SSHIFT = 31 - Integer.numberOfLeadingZeros(ss);
    TSHIFT = 31 - Integer.numberOfLeadingZeros(ts);
}


private Segment<K,V> segmentForHash(int h) {
    long u = (((h >>> segmentShift) & segmentMask) << SSHIFT) + SBASE;
    return (Segment<K,V>) UNSAFE.getObjectVolatile(segments, u);
}
```

观察segmentForHash(int h)方法可知，首先使用(h >>> segmentShift) & segmentMask计算出该h对应的segments索引值（假设为x），然后使用索引值(x<<SSHIFT) + SBASE计算出segments中相应Segment的地址，最后使用UNSAFE.getObjectVolatile(segments,
u)取出相应的Segment，并保持volatile读的效果。

## 4.3.2. Segment的锁

Segment继承了ReentrantLock，因此它实际上是一把锁。在进行put、remove、replace、clear等需要改动内部内容的操作时，都要进行加锁操作，其代码一般是这样的：

```java
final V put(K key, int hash, V value, boolean onlyIfAbsent) {
    HashEntry<K,V> node = tryLock() ? null :
        scanAndLockForPut(key, hash, value);
    V oldValue;
    try {
//实际代码……
        }
    } finally {
        unlock();
    }
    return oldValue;
}
```



首先调用tryLock，如果加锁失败，则进入scanAndLockForPut(key, hash, value)方法，该方法实际上是先自旋等待其他线程解锁，直至指定的次数MAX_SCAN_RETRIES。若自旋过程中，其他线程释放了锁，导致本线程直接获得了锁，就避免了本线程进入等待锁的场景，提高了效率。若自旋一定次数后，仍未获取锁，则调用lock方法进入等待锁的场景。

采用这种自旋锁和独占锁结合的方法，在很多场景下能够提高Segment并发操作数据的效率。

## 4.4 HashEntry

如果说ConcurrentHashMap中的segments数组是第一层hash表，则每个Segment中的HashEntry数组（transient volatile
HashEntry<K,V>[] table）是第二层hash表。每个HashEntry有一个next属性，因此它们能够组成一个单向链表。HashEntry相关代码如下：

```java
static final class HashEntry<K,V> {
    final int hash;
    final K key;
    volatile V value;
    volatile HashEntry<K,V> next;

    HashEntry(int hash, K key, V value, HashEntry<K,V> next) {
        this.hash = hash;
        this.key = key;
        this.value = value;
        this.next = next;
    }

    /**
     * Sets next field with volatile write semantics.  (See above
     * about use of putOrderedObject.)
     */ final void setNext(HashEntry<K,V> n) {
        UNSAFE.putOrderedObject(this, nextOffset, n);
    }

    // Unsafe mechanics static final sun.misc.Unsafe UNSAFE;
    static final long nextOffset;
    static {
        try {
            UNSAFE = sun.misc.Unsafe.getUnsafe();
            Class k = HashEntry.class;
            nextOffset = UNSAFE.objectFieldOffset
                (k.getDeclaredField("next"));
        } catch (Exception e) {
            throw new Error(e);
        }
    }
}

/**
 * Gets the ith element of given table (if nonnull) with volatile
 * read semantics. Note: This is manually integrated into a few
 * performance-sensitive methods to reduce call overhead.
 */ @SuppressWarnings("unchecked")
static final <K,V> HashEntry<K,V> entryAt(HashEntry<K,V>[] tab, int i) {
    return (tab == null) ? null :
        (HashEntry<K,V>) UNSAFE.getObjectVolatile
        (tab, ((long)i << TSHIFT) + TBASE);
}

/**
 * Sets the ith element of given table, with volatile write
 * semantics. (See above about use of putOrderedObject.)
 */ static final <K,V> void setEntryAt(HashEntry<K,V>[] tab, int i,
                                   HashEntry<K,V> e) {
    UNSAFE.putOrderedObject(tab, ((long)i << TSHIFT) + TBASE, e);
}
```

与Segment类似，HashEntry使用UNSAFE.putOrderedObject来设置它的next成员变量，这样既可以提高性能，又能保持并发可见性。同时，entryAt方法和setEntryAt方法也使用了UNSAFE.getObjectVolatile和UNSAFE.putOrderedObject来读取和写入指定索引的HashEntry。

总之，Segment数组和HashEntry数组的读取写入一般都是使用UNSAFE。

## 4.5 get方法

从图中查询数据使用get方法，算法思路是首先查询key所在的segment，然后在segment的hash表中查询相应的HashEntry，最后在此单向链表中一一查询是否有符合key的值。

```java
public V get(Object key) {
    Segment<K,V> s; // manually integrate access methods to reduce overhead
    HashEntry<K,V>[] tab;
    int h = hash(key);
//找到segment的地址 long u = (((h >>> segmentShift) & segmentMask) << SSHIFT) + SBASE;
//取出segment，并找到其hashtable if ((s = (Segment<K,V>)UNSAFE.getObjectVolatile(segments, u)) != null &&
        (tab = s.table) != null) {
//遍历此链表，直到找到对应的值 for (HashEntry<K,V> e = (HashEntry<K,V>) UNSAFE.getObjectVolatile
                 (tab, ((long)(((tab.length - 1) & h)) << TSHIFT) + TBASE);
             e != null; e = e.next) {
            K k;
            if ((k = e.key) == key || (e.hash == h && key.equals(k)))
                return e.value;
        }
    }
    return null;
}
```



整个get方法不需要加锁，只需要计算两次hash值，然后遍历一个单向链表（此链表长度平均小于2），因此get性能很高。

containsKey方法与get非常类似。

## 4.6 put方法

put方法的第一步，计算segment数组的索引，并找到该segment，然后调用该segment的put方法。

```java
public V put(K key, V value) {
    Segment<K,V> s;
    if (value == null)
        throw new NullPointerException();
    int hash = hash(key);
//计算segment数组的索引，并找到该segment int j = (hash >>> segmentShift) & segmentMask;
    if ((s = (Segment<K,V>)UNSAFE.getObject          // nonvolatile; recheck
         (segments, (j << SSHIFT) + SBASE)) == null) //  in ensureSegment
        s = ensureSegment(j);
//调用该segment的put方法 return s.put(key, hash, value, false);
}
```



put方法第二步，在Segment的put方法中进行操作。

```java
final V put(K key, int hash, V value, boolean onlyIfAbsent) {
//调用tryLock()尝试加锁，若失败则调用scanAndLockForPut进行加锁，同时寻找key相应的节点node
    HashEntry<K,V> node = tryLock() ? null :
        scanAndLockForPut(key, hash, value);
//以下的代码都运行在加锁状态
    V oldValue;
    try {
        HashEntry<K,V>[] tab = table;
//计算hash表的索引值，并取出HashEntry int index = (tab.length - 1) & hash;
        HashEntry<K,V> first = entryAt(tab, index);
//遍历此链表 for (HashEntry<K,V> e = first;;) {
//如果链表不为空，在链表中寻找对应的node，找到后进行赋值，并退出循环 if (e != null) {
                K k;
                if ((k = e.key) == key ||
                    (e.hash == hash && key.equals(k))) {
                    oldValue = e.value;
                    if (!onlyIfAbsent) {
                        e.value = value;
                        ++modCount;
                    }
                    break;
                }
                e = e.next;
            }
//如果在链表中没有找到对应的node else {
//如果scanAndLockForPut方法中已经返回的对应的node，则将其插入first之前 if (node != null)
                    node.setNext(first);
                else //否则，new一个新的HashEntry
                    node = new HashEntry<K,V>(hash, key, value, first);
                int c = count + 1;
//测试是否需要自动扩容 if (c > threshold && tab.length < MAXIMUM_CAPACITY)
                    rehash(node);
                else //设置node到Hash表的index索引处
                    setEntryAt(tab, index, node);
                ++modCount;
                count = c;
                oldValue = null;
                break;
            }
        }
    } finally {
        unlock();
    }
    return oldValue;
}
```

在第二步中，如果当前线程tryLock失败，表明其他线程已经锁住了此Segment，因此会进入scanAndLockForPut，这个方法的主要目的是自旋等待，加锁和寻找对应的node：

```java
private HashEntry<K,V> scanAndLockForPut(K key, int hash, V value) {
//寻找对应的HashEntry
    HashEntry<K,V> first = entryForHash(this, hash);
    HashEntry<K,V> e = first;
    HashEntry<K,V> node = null;
    int retries = -1; // negative while locating node //若tryLock失败，表明还未获得锁，准备遍历此链表 while (!tryLock()) {
        HashEntry<K,V> f; // to recheck first below //如果node还未定位成功 if (retries < 0) {
            if (e == null) {
                if (node == null) // e为null且node也为null，则创建一个新的HashEntry
                    node = new HashEntry<K,V>(hash, key, value, null);
                retries = 0;
            }
//如果e不为null，e.key且等于key，表明找到了匹配的节点 else if (key.equals(e.key))
                retries = 0;
            else
                e = e.next;  //继续遍历
        }
// retries次数少于MAX_SCAN_RETRIES，自旋等待 else if (++retries > MAX_SCAN_RETRIES) {
            lock();
            break;
        }
//重新检查一遍链表 else if ((retries & 1) == 0 &&
                 (f = entryForHash(this, hash)) != first) {
            e = first = f; // re-traverse if entry changed
            retries = -1;
        }
    }
    return node;
}
```

注意，scanAndLockForPut主要是为了提高多线程竞争Segment锁的效率。其中用到了自旋锁，若一些线程在自旋过程中加锁成功，则避免了调用lock()等待的过程。当线程执行完scanAndLockForPut方法后，一定是加锁成功的。若线程没有找到匹配的node，则会新建一个node，该node可以在Segment的put方法中使用，这样降低了put方法在加锁状态中的代码量，提高了效率。若scanAndLockForPut的线程找到了匹配的node，反而会返回一个null，因为在put方法中还是要再找一次。

## 4.7 remove方法

remove方法用来删除key指定的值。

```java
public V remove(Object key) {
    int hash = hash(key);
    Segment<K,V> s = segmentForHash(hash);
    return s == null ? null : s.remove(key, hash, null);
}
首先找到对应的segment，然后调用Segment的remove方法。
final V remove(Object key, int hash, Object value) {
//和put方法一样，调用tryLock，失败则调用scanAndLock if (!tryLock())
        scanAndLock(key, hash);
//以下代码运行在加锁状态
    V oldValue = null;
    try {
//找到hash表中对应的HashEntry
        HashEntry<K,V>[] tab = table;
        int index = (tab.length - 1) & hash;
        HashEntry<K,V> e = entryAt(tab, index);
        HashEntry<K,V> pred = null;
//遍历链表 while (e != null) {
            K k;
            HashEntry<K,V> next = e.next;
            if ((k = e.key) == key ||
                (e.hash == hash && key.equals(k))) {
                V v = e.value;
//如果找到了对应的节点，则将其从链表中剔除 if (value == null || value == v || value.equals(v)) {
                    if (pred == null)
                        setEntryAt(tab, index, next);
                    else
                        pred.setNext(next);
                    ++modCount;
                    --count;
                    oldValue = v;
                }
                break;
            }
            pred = e;
            e = next;
        }
    } finally {
        unlock();
    }
    return oldValue;
}
```



remove方法相对简单，其scanAndLock是scanAndLockForPut的简化版本：

```java
private void scanAndLock(Object key, int hash) {
    // similar to but simpler than scanAndLockForPut
    HashEntry<K,V> first = entryForHash(this, hash);
    HashEntry<K,V> e = first;
    int retries = -1;
//遍历链表 while (!tryLock()) {
        HashEntry<K,V> f;
        if (retries < 0) {
//若e==null，或者找到匹配的节点，则不再继续找 if (e == null || key.equals(e.key))
                retries = 0;
            else
                e = e.next;
        }
//自旋等待加锁 else if (++retries > MAX_SCAN_RETRIES) {
            lock();
            break;
        }
//重复检测 else if ((retries & 1) == 0 &&
                 (f = entryForHash(this, hash)) != first) {
            e = first = f;
            retries = -1;
        }
    }
}
```



扫描链表，找到匹配的节点，同时自旋等待加锁。

## 4.8 replace方法

replace方法用来替换map中的匹配节点的value值。

```java
public V replace(K key, V value) {
    int hash = hash(key);
    if (value == null)
        throw new NullPointerException();
    Segment<K,V> s = segmentForHash(hash);
    return s == null ? null : s.replace(key, hash, value);
}
```



首先找到对应的Segment，然后调用其replace方法：

```java
final V replace(K key, int hash, V value) {
//tryLock，失败则调用scanAndLock if (!tryLock())
        scanAndLock(key, hash);
    V oldValue = null;
    try {
        HashEntry<K,V> e;
//遍历链表 for (e = entryForHash(this, hash); e != null; e = e.next) {
            K k;
//若找到匹配节点，则替换其value值 if ((k = e.key) == key ||
                (e.hash == hash && key.equals(k))) {
                oldValue = e.value;
                e.value = value;
                ++modCount;
                break;
            }
        }
    } finally {
        unlock();
    }
    return oldValue;
}
```



replace方法中也用到了scanAndLock方法。

## 4.9 size方法

size方法用来计算Map中有多少个节点，此方法的算法有些奇特，注意观察：

```java
public int size() {
    //运行多次来得到一个精确的值 //若多次失败，肯定是由于其他线程持续的修改hash表元素 //那么就必须加锁了 final Segment<K,V>[] segments = this.segments;
    int size;
    boolean overflow; // true if size overflows 32 bits long sum;         // sum of modCounts long last = 0L;   // previous sum int retries = -1; // first iteration isn't retry try {
        for (;;) {
//如果重试的次数大于某值，则把所有segment全部加锁 if (retries++ == RETRIES_BEFORE_LOCK) {
                for (int j = 0; j < segments.length; ++j)
                    ensureSegment(j).lock(); // force creation
            }
            sum = 0L;
            size = 0;
            overflow = false;
//遍历所有segment，计算一个总值sum for (int j = 0; j < segments.length; ++j) {
                Segment<K,V> seg = segmentAt(segments, j);
                if (seg != null) {
                    sum += seg.modCount;
                    int c = seg.count;
                    if (c < 0 || (size += c) < 0)
                        overflow = true;
                }
            }
//如果sum值与上次计算的值相等，则跳出循环 if (sum == last)
                break;
//将sum赋值给last
            last = sum;
        }
    } finally {
//若曾经加锁，则全部解锁 if (retries > RETRIES_BEFORE_LOCK) {
            for (int j = 0; j < segments.length; ++j)
                segmentAt(segments, j).unlock();
        }
    }
    return overflow ? Integer.MAX_VALUE : size;
}
```

size的算法思想是尽量不加锁，在无锁的状态下多次计算总值sum，如果连续两次的计算值相等，就可以认为此刻sum就是Map的size值。如果多次计算值都不相等，那么只能锁住所有segment再计算一次。

## 4.10 rehash

rehash方法用来对Segment的hash表进行自动扩容。它只会在Segment的put方法中被调用，每次将hash表扩容为原来的两倍。因为hash表的长度必然是2的幂，因此旧表中的元素对应的索引值在新表中只有两种可能。举个例子，设旧表长度为16，则元素的hash值需要与1111进行&运算来决定索引，设此索引值为WXYZ（这四个都是0或1）；新表的长度为32，则元素的hash值需要与11111进行&运算来决定索引，因此新表中该元素的索引值只会是0WXYZ或者1WXYZ。明白了这一点对理解rehash算法很重要。因为旧表中的很多元素可能都会维持原来的索引值0WXYZ不变，或者它们会形成一串索引值相同的子链表，这样在移动它们时效率就会很高。统计上来说，仅有六分之一的元素需要复制，其他元素仅仅移动就行。

另外，本算法中直接使用了数组下标的方法来获取数组元素，这是因为，除了本方法，其他方法都使用Unsafe的volatile读写。

```java
private void rehash(HashEntry<K,V> node) {
    HashEntry<K,V>[] oldTable = table;
    int oldCapacity = oldTable.length;
    int newCapacity = oldCapacity << 1;
    threshold = (int)(newCapacity * loadFactor);
//创建一个2倍长度的新hash表
    HashEntry<K,V>[] newTable =
        (HashEntry<K,V>[]) new HashEntry[newCapacity];
    int sizeMask = newCapacity - 1;
//遍历旧表 for (int i = 0; i < oldCapacity ; i++) {
        HashEntry<K,V> e = oldTable[i];
        if (e != null) {
            HashEntry<K,V> next = e.next;
//计算每个元素的新索引值idx int idx = e.hash & sizeMask;
            if (next == null)   //  若链表中只有一个节点，直接赋值给新表中的idx处
                newTable[idx] = e;
            else { // 新索引值相同的一串子链表可以复用
                HashEntry<K,V> lastRun = e;
                int lastIdx = idx;
//寻找最后一个与其他节点索引不同的节点lastRun，它后面带的一串子链表都与之相同 for (HashEntry<K,V> last = next;
                     last != null;
                     last = last.next) {
                    int k = last.hash & sizeMask;
                    if (k != lastIdx) {
                        lastIdx = k;
                        lastRun = last;
                    }
                }
//将子链表赋值到新表的lastIdx索引处
                newTable[lastIdx] = lastRun;
                // 将子链表之前的节点复制到新表中 for (HashEntry<K,V> p = e; p != lastRun; p = p.next) {
                    V v = p.value;
                    int h = p.hash;
                    int k = h & sizeMask;
                    HashEntry<K,V> n = newTable[k];
                    newTable[k] = new HashEntry<K,V>(h, p.key, v, n);
                }
            }
        }
    }
//加入参数中带入的node int nodeIndex = node.hash & sizeMask; // add the new node
    node.setNext(newTable[nodeIndex]);
    newTable[nodeIndex] = node;
    table = newTable;
}
```

rehash算法的难点主要是理解为什么rehash后，旧表中的每个链表中元素只能有两个去处，然后要理解子链表的操作。

## 4.11 三大集合与迭代子

关于ConcurrentHashMap的三大集合与迭代子，其用法与HashMap完全一致。其内部实现就是在多个Segment之间进行遍历，算法上没有什么难懂之处，因此直接使用即可。

## 5. ConcurrentHashMap特性小结

与HashMap、Hashtable这些类相比，ConcurrentHashMap最大的特点就是在获得线程安全性的同时，最大限度的提高了性能，其中使用了如下的设计和技巧：

一是采用多Segment结构，使得在不同Segment之间可以并发执行写操作，极大的提高了多线程写入效率；

二是使用了延迟加载技术，Map创建时仅创建一个Segment，其他Segment只有用到时再创建；

三是使用了Unsafe的putOrderedObject方法和getObjectVolatile方法来访问segments数组和table数组，既保持了一定的并发可见性，防止了因指令重排导致的错误，又比直接使用AtomicReferenceArrays（同时保持原子性和可见性）或volatile变量数组（况且volatile变量数组中的元素并不是volatile的）性能更高；

四是使用了自旋锁，在执行某些加锁操作前，自旋等待一段时间，并同时做一些预热操作（例如创建一些将会在后续加锁状态中用到的对象），若在自旋过程中加锁成功，则避免了进入加锁等待的耗时场景；

五是尽量避免加锁操作，将加锁代码的粒度最小化。例如get方法就完全是无锁的。在size方法中，也是尽量在无锁状态完成计算，多次失败后再加锁。

总之，ConcurrentHashMap使用起来与HashMap或Hashtable区别不大，但内部机制却值得仔细研究。

发布于 2017-08-19