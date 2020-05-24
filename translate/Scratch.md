# 死锁

## 线程死锁

死锁指的是当两个或者多个线程阻塞等待获取一些处于同一个死锁状态下的其他线程持有的锁的状态。当多个线程同时需要相同的锁，而获取这些锁的顺序有所不同时，就可能会发生死锁。

比如，如果线程 1 锁定 A，并尝试锁定 B，同时线程 2 已经锁定 B，并尝试锁定 A，死锁就产生了。线程 1 永远无法获得 B，同时线程 2 永远无法获得 A。另外，它们彼此也永远无法知道这种情况。它们将永远保持相互阻塞在对方已经锁定的对象上的状态。这种情况就是死锁。

这种情况如下所示：

```java
Thread 1  locks A, waits for B
Thread 2  locks B, waits for A
```

这里是个  `TreeNode`  类的例子，在不同实例上调用同步方法：

```java
public class TreeNode {
 
  TreeNode parent   = null;  
  List     children = new ArrayList();

  public synchronized void addChild(TreeNode child){
    if(!this.children.contains(child)) {
      this.children.add(child);
      child.setParentOnly(this);
    }
  }
  
  public synchronized void addChildOnly(TreeNode child){
    if(!this.children.contains(child){
      this.children.add(child);
    }
  }
  
  public synchronized void setParent(TreeNode parent){
    this.parent = parent;
    parent.addChildOnly(this);
  }

  public synchronized void setParentOnly(TreeNode parent){
    this.parent = parent;
  }
}
```

如果一个线程 (1) 调用 `parent.addChild(child)` 方法，同时另一个线程 (2) 调用 `child.setParent(parent)` 方法，在相同的父和子实例上，死锁就会发生。下面是解释这种情况的伪代码：

```java
Thread 1: parent.addChild(child); //locks parent
          --> child.setParentOnly(parent);

Thread 2: child.setParent(parent); //locks child
          --> parent.addChildOnly()
```

首先线程 1 调用 `parent.addChild(child)`。由于 `addChild()` 是同步方法，因此线程 1 有效地锁定了父对象以防止其他线程访问。

然后线程 2 调用 `child.setParent(parent)`。由于 `setParent()` 是同步的，线程 2 有效地锁定了子对象以防止其他线程访问。

现在，子对象和父对象都被两个不同的线程锁定。下一个线程 1 尝试调用 `child.setParentOnly()` 方法，但是子对象被线程 2 锁定，因此该方法调用只能阻塞。线程 2 还尝试调用 `parent.addChildOnly()`，但父对象被线程 1 锁定，导致线程 2 在该方法调用上阻塞。现在，两个线程都被阻塞，等待获取另一个线程持有的锁。

注意：这两个线程必须如上所述同时在同一个父实例和子实例上同时调用 `parent.addChild(child)` 和 `child.setParent(parent)`，以发生死锁。上面的代码可能会执行很长时间，直到突然陷入僵局。

线程确实需要“同时”获取锁。例如，如果线程 1 领先于线程 2，因此同时锁定了 A 和 B，那么在尝试锁定 B 时线程 2 将已经被阻塞。这样就不会发生死锁。由于线程调度通常是不可预测的，因此无法预测何时发生死锁。只能说死锁总是会发生的。

## 更复杂的死锁

死锁也可以包含多于两个线程，这就使得死锁很难检测。下面是四个线程死锁的例子：

```java
Thread 1  locks A, waits for B
Thread 2  locks B, waits for C
Thread 3  locks C, waits for D
Thread 4  locks D, waits for A
```

线程 1 等待线程 2，线程 2 等待线程 3，线程 3 等待线程 4，线程 4 等待线程 1。

## 数据库死锁

发生死锁的更为复杂的情况是数据库事务。数据库事务可能包含许多 SQL 更新请求。在事务期间更新记录时，该记录将被锁定以阻止其他事务的更新，直到第一个事务完成为止。因此，同一事务中的每个更新请求可能会锁定数据库中的某些记录。

如果需要同时更新同一记录的多个事务正在同时运行，则存在最终陷入僵局的风险。

比如：

```
Transaction 1, request 1, locks record 1 for update
Transaction 2, request 1, locks record 2 for update
Transaction 1, request 2, tries to lock record 2 for update.
Transaction 2, request 2, tries to lock record 1 for update.
```

由于锁是在不同的请求中获得的，并且无法提前知道给定事务所需的所有锁，因此很难检测或防止数据库事务中的死锁。

