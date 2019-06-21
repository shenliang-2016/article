#### 死锁

*死锁*描述了两个或多个线程永远被阻塞，等待彼此的情况。这是一个例子。

Alphonse 和 Gaston 是朋友，也很有礼貌的信徒。严格的礼貌规则是，当你向朋友鞠躬时，你必须保持鞠躬，直到你的朋友有机会还礼。不幸的是，这条规则没有考虑到两个朋友可能同时互相鞠躬的可能性。这个示例应用程序`Deadlock`模拟了这种可能性：

```java
public class Deadlock {
    static class Friend {
        private final String name;
        public Friend(String name) {
            this.name = name;
        }
        public String getName() {
            return this.name;
        }
        public synchronized void bow(Friend bower) {
            System.out.format("%s: %s"
                + "  has bowed to me!%n", 
                this.name, bower.getName());
            bower.bowBack(this);
        }
        public synchronized void bowBack(Friend bower) {
            System.out.format("%s: %s"
                + " has bowed back to me!%n",
                this.name, bower.getName());
        }
    }

    public static void main(String[] args) {
        final Friend alphonse =
            new Friend("Alphonse");
        final Friend gaston =
            new Friend("Gaston");
        new Thread(new Runnable() {
            public void run() { alphonse.bow(gaston); }
        }).start();
        new Thread(new Runnable() {
            public void run() { gaston.bow(alphonse); }
        }).start();
    }
}
```

当`Deadlock`运行时，两个线程在尝试调用`bowBack`时极有可能会阻塞。两个块都不会结束，因为每个线程都在等待另一个线程退出 `bow`。

#### 饥饿和活锁

与死锁相比，饥饿和活锁不是常见的问题，但仍然是并发软件的每个设计者都可能遇到的问题。

**饥饿**

*Starvation*描述了一种情况，即线程无法获得对共享资源的正常访问，并且无法继续运行。当“贪婪”线程使共享资源长时间不可用时，就会发生这种情况。例如，假设一个对象提供了一个通常需要很长时间才能返回的同步方法。如果一个线程经常调用此方法，则需要对同一对象进行频繁同步访问的其他线程就会经常被阻塞。

**活锁**

线程通常用于响应另一个线程的操作。如果另一个线程的操作也是对另一个线程的操作的响应，则可能导致活锁。与死锁一样，活锁线程无法继续运行。但是，线程没有被阻塞 - 他们只是太忙于相互回应以恢复工作。这相当于两个试图在走廊里互相通过的人：Alphonse向左移动让Gaston通过，而Gaston向右移动让Alphonse通过。看到他们仍然互相阻挡，Alphone向右移动，而Gaston向左移动。他们还在互相阻挡，所以......

