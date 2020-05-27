## 乐观锁和 CAS

如果你确实需要超过一个线程同时写入同一个共享变量，volatile 变量就不够了。你需要某种对变量的独占式访问。下面是使用 [Java 同步块](http://tutorials.jenkov.com/java-concurrency/synchronized.html) 实现的这种独占式访问的例子：

```java
public class SynchronizedCounter {
    long count = 0;

    public void inc() {
        synchronized(this) {
            count++;
        }
    }

    public long count() {
        synchronized(this) {
            return this.count;
        }
    }
}
```

注意，`inc()` 和 `count()` 方法都包含一个同步块。这就是我们想要避免的——同步块和 `wait()` - `notify()` 调用。

我们可以使用一种 Java 的原子变量替换两个同步块。这种场景下使用 `AtomicLong` 。下面是上面的计数器类的修改版本：

```java
import java.util.concurrent.atomic.AtomicLong;

public class AtomicCounter {
    private AtomicLong count = new AtomicLong(0);

    public void inc() {
        boolean updated = false;
        while(!updated){
            long prevCount = this.count.get();
            updated = this.count.compareAndSet(prevCount, prevCount + 1);
        }
    }

    public long count() {
        return this.count.get();
    }
}
```

这个版本跟前面一个版本一样都是线程安全的。有趣的是其中的 `inc()` 方法实现。这里的 `inc()` 方法不再包含同步块，而是包含下面几行：

```java
boolean updated = false;
while(!updated){
    long prevCount = this.count.get();
    updated = this.count.compareAndSet(prevCount, prevCount + 1);
}
```

这几行布施原子操作。也就是说，两个不同线程可以调用 `inc()` 方法并执行 `long prevCount = this.count.get()` 语句，从而都获取到计数器的上一个计数值。因此，上面的代码不包含任何竞争条件。

秘密在于 `while` 循环中的第二行代码。`compareAndSet()` 方法调用是一个原子操作。它将 `AtomicLong` 的内部值与期望值进行比较，如果两个值相等，则为 `AtomicLong` 的内部值设置新值。`compareAndSet()` 方法通常是由 CPU 中的 CAS 结构直接支持。因此没有同步的必要，也没有线程阻塞的必要。这就节省了线程阻塞的开销。

假设 `AtomicLong` 的内部值是 20。两个线程读取该值，都尝试调用 `compareAndSet(20, 20+1)`。由于 `compareAndSet()` 是原子操作，线程将会依次执行该方法(每次一个线程)。

第一个线程会将期望值 20（计数器的先前值）与 `AtomicLong` 的内部值进行比较。由于两个值相等，因此会将 `AtomicLong` 内部值更新为 21（20 +1）。`updated` 变量将被设置为 `true`，而 `while` 循环将停止。

现在第二个线程调用 `compareAndSet(20, 20+1)`。由于 `AtomicLong` 的内部值不再为 20，因此该调用将失败。 `AtomicLong` 的内部值不会设置为 21。`updated` 变量将设置为 `false`，并且线程将在 `while` 循环中再旋转一圈。这次它将读取值 21 并尝试将其更新为 22。如果在此期间没有其他线程调用 `inc()`，则第二次迭代将成功将 `AtomicLong` 更新为 22。

### 为什么叫做乐观锁？

上一节中的代码称为“乐观锁”。乐观锁不同于传统锁，传统锁有时也称为悲观锁。传统锁使用同步块或某种锁来阻止对共享内存的访问。同步块或锁可能导致线程被挂起。

乐观锁允许所有线程创建共享内存的副本而没有任何阻塞。然后，线程可以对其副本进行修改，并尝试将其修改后的版本写回到共享内存中。如果没有其他线程对共享内存进行任何修改，则比较和交换操作将允许线程将其更改写入共享内存。如果另一个线程已经更改了共享内存，则该线程将必须获取新副本，进行更改，然后尝试再次将它们写入共享内存。

之所以称为乐观锁，是因为线程在乐观的假设（即没有其他线程会同时对共享内存进行更改）下获得要更改的数据的副本并进行更改。当这种乐观假设成立时，线程就可以设法在不加锁的情况下更新共享内存。如果这个假设是错误的，那么就浪费了工作，但是仍然没有使用锁定。

乐观锁通常在共享内存争用较低或中等的情况下效果最佳。如果共享内存上的内容过多，线程将浪费大量的 CPU 周期来复制和修改共享内存，以至于无法将更改写回到共享内存中。但是，如果共享内存上有很多内容，则无论如何都应考虑重新设计代码以减少争用。

### 乐观锁是非阻塞的

我在这里展示的乐观锁机制是非阻塞的。如果某个线程获取了共享内存的副本并在尝试对其进行修改时（无论出于何种原因）被阻止，并不会阻止其他线程访问共享内存。

在传统的加锁/解锁范例中，当线程锁定锁时，该锁将对所有其他线程保持锁定状态，直到拥有该锁的线程再次将其解锁。如果锁定该锁的线程在其他地方被阻塞，则该锁定将保持锁定状态很长时间——甚至是无限期的。