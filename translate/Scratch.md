## 非阻塞算法模板

下面是一个代码模板，旨在使您了解如何实现非阻塞算法。该模板基于本教程前面给出的描述。

注意：我不是非阻塞算法专家，所以下面的模板可能有一些错误。不要在我的模板上建立自己的非阻塞算法实现。该模板仅用于使您了解非阻塞算法的代码外观。如果要实现自己的非阻塞算法，请首先研究一些实际的，有效的非阻塞算法实现，以了解有关如何在实践中实现它们的更多信息。

````java
import java.util.concurrent.atomic.AtomicBoolean;
import java.util.concurrent.atomic.AtomicStampedReference;

public class NonblockingTemplate {

    public static class IntendedModification {
        public AtomicBoolean completed =
                new AtomicBoolean(false);
    }

    private AtomicStampedReference<IntendedModification>
        ongoingMod =
            new AtomicStampedReference<IntendedModification>(null, 0);

    //declare the state of the data structure here.


    public void modify() {
        while(!attemptModifyASR());
    }

    public boolean attemptModifyASR(){

        boolean modified = false;
    
        IntendedModification currentlyOngoingMod =
        ongoingMod.getReference();
        int stamp = ongoingMod.getStamp();
    
        if(currentlyOngoingMod == null){
            //copy data structure state - for use
            //in intended modification
        
            //prepare intended modification
            IntendedModification newMod =
            new IntendedModification();
        
            boolean modSubmitted = 
                ongoingMod.compareAndSet(null, newMod, stamp, stamp + 1);
        
            if(modSubmitted){
            
                //complete modification via a series of compare-and-swap operations.
                //note: other threads may assist in completing the compare-and-swap
                // operations, so some CAS may fail
            
                modified = true;
            }
    
        } else {
            //attempt to complete ongoing modification, so the data structure is freed up
            //to allow access from this thread.
        
            modified = false;
        }
    
        return modified;
    }
}
````

## 非阻塞算法难以实现

非阻塞算法很难正确设计和实现。在尝试实现自己的非阻塞算法之前，请查看是否没有人已经开发出可以满足您需求的非阻塞算法。

Java 已经提供了一些非阻塞实现（例如 `ConcurrentLinkedQueue`），并且很可能在将来的 Java 版本中获得更多的非阻塞算法实现。

除了 Java 的内置非阻塞数据结构之外，您还可以使用一些开源的非阻塞数据结构。例如，LMAX Disrupter（类似队列的数据结构）和来自 Cliff Click 的非阻塞 HashMap。请参阅我的 [Java并发参考页面](http://tutorials.jenkov.com/java-concurrency/references.html) 以获取更多资源的链接。

## 非阻塞算法的好处

与阻塞算法相比，非阻塞算法有几个好处。本节将描述这些好处。

### 选择

非阻塞算法的第一个好处是，在无法执行请求的操作时，请求线程可以选择做什么，而不仅仅是被阻塞。有时线程无法执行任何操作。在这种情况下，它可以选择阻塞或等待，从而将 CPU 释放给其他任务。但是至少可以给请求线程一个选择。

在单个 CPU 系统上，挂起无法执行所需动作的线程，然后让其他可以执行其工作的线程在 CPU 上运行也许是有意义的。但是即使在单个 CPU 系统上，阻塞算法也可能导致[死锁](http://tutorials.jenkov.com/java-concurrency/deadlock.html)，[饥饿](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) 和其他并发问题。

### 无死锁

非阻塞算法的第二个好处是，一个线程的挂起不会导致其他线程的挂起。这意味着不会发生死锁。不能阻止两个线程互相等待释放它们想要的锁。由于在无法执行请求的操作时不会阻塞线程，因此无法导致彼此之间的等待。非阻塞算法可能仍会导致活锁，在此情况下，两个线程会继续尝试某些操作，但始终被告知这是不可能的（因为另一个线程的操作）。

### 没有线程挂起

挂起和重新激活线程的成本很高。是的，随着操作系统和线程库变得更加高效，挂起和重新激活的成本已随着时间的推移而下降。但是，线程挂起和重新激活仍然需要付出高昂的代价。

每当线程被阻塞时，它就会被挂起，从而导致线程挂起和重新激活的开销。由于线程不会被非阻塞算法挂起，因此不会发生这种开销。这意味着 CPU 可能会花费更多时间执行实际的业务逻辑，而不是进行上下文切换。

在多 CPU 系统上，阻塞算法可能会对整体性能产生更大的影响。可以阻止 CPU A 上运行的线程等待 CPU B 上运行的线程。这降低了应用程序能够实现的并行度。当然，CPU A 可以安排另一个线程运行，但是挂起和激活线程（上下文切换）非常昂贵。需要挂起的线程越少越好。

### 减少线程延迟

在这种语境下，延迟意味着在请求的操作成为可能与线程实际执行操作之间的时间。由于线程未在非阻塞算法中挂起，因此它们不必支付昂贵且缓慢的重新激活开销。这意味着当请求的操作变为可能时，线程可以更快地响应，从而减少其响应延迟。

非阻塞算法通常通过忙于等待直到请求的动作变为可能而获得较低的延迟。当然，在非阻塞数据结构上具有高线程争用的系统中，CPU 可能会在这些繁忙的等待期间消耗大量周期。这是要记住的事情。如果您的数据结构具有高线程争用，则非阻塞算法可能不是最好的。但是，通常有很多方法可以重新设计应用程序以减少线程争用。