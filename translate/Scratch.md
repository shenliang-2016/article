# 线程池

当你需要限制你的应用中同时运行的线程数量的时候线程池就非常有用。启动一个新线程会带来一些性能损耗，同时每个线程都会分配一些内存用于线程栈等等。

将任务传递给线程池，可以避免为每个并发执行的任务都创建新的线程。只要线程池中还存在空闲的线程，就会将任务分配给空闲线程之一执行。内部机制上，任务会被插入一个阻塞队列，线程池中的线程会将任务从该队列中取出。当一个新的任务被插入队列，一个空闲线程将其从队列中取出并执行。线程池中其他的空闲线程将继续被阻塞等待任务出队。

线程池通常用于多线程服务器。每个通过网络到达服务器的连接都被包装成一个任务并被传递给一个线程池。线程池中的线程将并发处理这些连接上的请求。

Java 5 在 `java.util.concurrent` 包中内置了线程池，你不必实现自己的线程池。可以参考 [java.util.concurrent.ExecutorService](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html) 了解更多细节。了解实现背后的原理还是有用的。

下面是个简单的线程池实现。注意，这个实现使用了在 [Blocking Queues](http://tutorials.jenkov.com/java-concurrency/blocking-queues.html) 章节中介绍的 `BlockingQueue` 类。在实际的实现中，你可能需要使用 Java 内建阻塞队列之一。

```java
public class ThreadPool {

    private BlockingQueue taskQueue = null;
    private List<PoolThread> threads = new ArrayList<PoolThread>();
    private boolean isStopped = false;

    public ThreadPool(int noOfThreads, int maxNoOfTasks){
        taskQueue = new BlockingQueue(maxNoOfTasks);

        for(int i=0; i<noOfThreads; i++){
            threads.add(new PoolThread(taskQueue));
        }
        for(PoolThread thread : threads){
            thread.start();
        }
    }

    public synchronized void  execute(Runnable task) throws Exception{
        if(this.isStopped) throw
            new IllegalStateException("ThreadPool is stopped");

        this.taskQueue.enqueue(task);
    }

    public synchronized void stop(){
        this.isStopped = true;
        for(PoolThread thread : threads){
           thread.doStop();
        }
    }

}
public class PoolThread extends Thread {

    private BlockingQueue taskQueue = null;
    private boolean       isStopped = false;

    public PoolThread(BlockingQueue queue){
        taskQueue = queue;
    }

    public void run(){
        while(!isStopped()){
            try{
                Runnable runnable = (Runnable) taskQueue.dequeue();
                runnable.run();
            } catch(Exception e){
                //log or otherwise report exception,
                //but keep pool thread alive.
            }
        }
    }

    public synchronized void doStop(){
        isStopped = true;
        this.interrupt(); //break pool thread out of dequeue() call.
    }

    public synchronized boolean isStopped(){
        return isStopped;
    }
}
```

线程池实现包含两部分，`ThreadPool` 类是线程池的公开接口，`PoolThread` 类实现了实际执行任务的线程。

为了执行任务，使用一个 `Runnable` 实现作为参数调用方法 `ThreadPool.execute(Runnable r)` 。该 `Runnable` 在内部会被加入阻塞队列，等待被线程取出。

该 `Runnable` 将被一个空闲线程取出并执行。这个动作可以在 `PoolThread.run()` 方法中看到。任务执行完成之后 `PoolThread` 循环并尝试再次取出一个任务，直到停止。

调用 `ThreadPool.stop()` 以停止 `ThreadPool()`。内部在 `isStopped` 成员上记录了所调用的停止方法。然后，通过在每个线程上调用 `doStop()` 来停止池中的每个线程。注意，如果在调用 `stop()` 之后调用了 `execute()`，则 `execute()` 方法将抛出 `IllegalStateException`。

线程将在完成当前正在执行的所有任务后停止。注意 `PoolThread.doStop()` 中的 `this.interrupt()` 调用。这确保了在 `taskQueue.dequeue()` 调用内的 `wait()` 调用中阻塞的线程脱离了 `wait()` 调用，并使 `dequeue()` 方法调用带有 `InterruptedException` 抛出。此异常将在 `PoolThread.run()` 方法中被捕获并报告，然后检查 `isStopped` 变量。由于 `isStopped` 现在为真，因此 `PoolThread.run()` 将退出并且线程死亡。

