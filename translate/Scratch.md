## Lock Timeout

另一个防止死锁的机制是对锁尝试进行超时，这意味着试图获取锁的线程只会尝试这么长时间然后就会放弃。如果线程在给定的超时时间内未成功获取所有必要的锁，它将阻塞，释放所有已获取的锁，等待随机的时间，然后重试。等待的随机时间使尝试进行相同锁定的其他线程有机会获得锁，从而使应用程序可以继续运行而不会死锁。

下面的例子是两个线程以不同顺序尝试获取相同的两个锁，线程会阻塞并重试：

```java
Thread 1 locks A
Thread 2 locks B

Thread 1 attempts to lock B but is blocked
Thread 2 attempts to lock A but is blocked

Thread 1's lock attempt on B times out
Thread 1 backs up and releases A as well
Thread 1 waits randomly (e.g. 257 millis) before retrying.

Thread 2's lock attempt on A times out
Thread 2 backs up and releases B as well
Thread 2 waits randomly (e.g. 43 millis) before retrying.
```

上面的例子中，线程 2 将在线程 1 之前尝试获取锁 200 毫秒，并将因此可能成功获取两个锁。线程 1 随后将等待已经在尝试获取锁 A 的线程。当线程 2 执行结束，线程 1 也将可以获取两个锁(除非线程 2 或者其他线程在此期间再次获取了锁)。

要记住的一个问题是，仅仅是锁定超时，并不一定意味着线程已死锁。这也可能仅意味着持有锁的线程（导致另一个线程超时）需要很长时间才能完成其任务。

此外，如果有足够的线程争用同一资源，即使超时和阻塞，它们仍然会一次又一次地冒险尝试。在重试之前，有 2 个线程在 0 到 500 毫秒之间等待，可能不会发生这种情况，但是有 10 或 20 个线程时，情况就不同了。这种情况下，两个线程在重试之前（或者足够接近以引起问题）等待相同时长的可能性要高得多。

锁超时机制的问题在于，无法为 Java 中的同步块设置超时时间。您将必须创建一个自定义锁类或使用 `java.util.concurrency` 包中的 Java 5 并发构造之一。编写自定义锁并不困难，但这不在本文讨论范围之内。Java 并发教程中的后续文本将涵盖自定义锁。