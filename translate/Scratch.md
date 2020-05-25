# 死锁预防

某些情况下预防死锁是可能的。本节介绍三种死锁预防技术：

1. [锁排序](http://tutorials.jenkov.com/java-concurrency/deadlock-prevention.html#ordering)
2. [锁超时](http://tutorials.jenkov.com/java-concurrency/deadlock-prevention.html#timeout)
3. [死锁检测](http://tutorials.jenkov.com/java-concurrency/deadlock-prevention.html#detection)

## 锁排序

当多个线程需要一组相同的锁，而获取它们的顺序不同时就会发生死锁。

如果我们能够保证线程获取所有锁的顺序都完全一样，死锁就不会发生了。看看下面的例子：

```java
Thread 1:

  lock A 
  lock B


Thread 2:

   wait for A
   lock C (when A locked)


Thread 3:

   wait for A
   wait for B
   wait for C
```

如果一个线程，比如线程 3，需要一些锁。它必须以确定的顺序获取那些锁。也就是说，它不能在获取既定锁顺序中前面的锁之前获取任何一个后面的锁。

比如，线程 2 和线程 3 在意境锁定 A 之前都无法锁定 C。因为线程 1 持有锁 A，线程 2 和线程 3 首先必须等待锁 A 被释放。然后它们必须成功锁定 A，然后才能尝试锁定 B 或者 C。

锁排序是一种简单而有效的死锁避免机制。然而，它需要你在获取任何锁之前确知所有锁需要的锁，实际情况中这一点往往并不现实。