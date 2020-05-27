# 阻塞队列

阻塞队列是一个队列，当您尝试从队列中出队并且队列为空时，或者尝试将项目入队并且队列已满时，操作将被阻塞。尝试从空队列中出队的线程将被阻止，直到其他线程将一项插入队列中为止。尝试使一个项目进入满队列的线程被阻塞，直到某个其他线程在队列中腾出空间为止，方法是使一个或多个项目出队或完全清除队列。

下图展示了两个线程通过一个阻塞队列进行协作的场景：

| ![A BlockingQueue with one thread putting into it, and another thread taking from it.](http://tutorials.jenkov.com/images/java-concurrency-utils/blocking-queue.png) |
| ------------------------------------------------------------ |
| **一个阻塞队列，一个线程将元素放入其中，另一个线程从队列中取出元素。** |

Java 5 的 `java.util.concurrent` 包中已经提供了阻塞队列实现。尽管 Java 5 提供了一种阻塞队列实现，理解它们背后的原理还是很有用的。

## 阻塞队列实现

阻塞队列的实现类似于 [Bounded Semaphore](http://tutorials.jenkov.com/java-concurrency/semaphores.html#bounded)。下面是一个简单的阻塞队列实现：

```java
public class BlockingQueue {

  private List queue = new LinkedList();
  private int  limit = 10;

  public BlockingQueue(int limit){
    this.limit = limit;
  }


  public synchronized void enqueue(Object item)
  throws InterruptedException  {
    while(this.queue.size() == this.limit) {
      wait();
    }
    this.queue.add(item);
    if(this.queue.size() == 1) {
      notifyAll();
    }
  }


  public synchronized Object dequeue()
  throws InterruptedException{
    while(this.queue.size() == 0){
      wait();
    }
    if(this.queue.size() == this.limit){
      notifyAll();
    }

    return this.queue.remove(0);
  }

}
    
```

注意，如果队列大小等于大小限制（ 0 或上限），那么仅从 `enqueue()` 和 `dequeue()` 调用 `notifyAll()`。如果在调用 `enqueue()` 或 `dequeue()` 时队列大小不等于上限，则没有线程等待入队或出队。