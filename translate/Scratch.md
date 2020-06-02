# 使用 ForkJoinPool 的 Java Fork 和 Join 

 Java 7 添加了 `ForkJoinPool` 。 `ForkJoinPool` 类似于 [Java ExecutorService](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html) ，除了一个不同点。`ForkJoinPool` 使得将任务分解为若干个粒度更小的任务并同样提交给 `ForkJoinPool` 执行变的容易。只要可以拆分任务，任务就可以继续将其工作拆分为较小的子任务。听起来可能有点抽象，所以在此 fork 和 join 教程中，我将解释 `ForkJoinPool` 的工作方式以及拆分任务的工作方式。

## Fork 和 Join 解释

在介绍 `ForkJoinPool` 之前，我先解释一下普遍意义上的 fork 和 join 工作原理。

fork 和 join 原理包括两个步骤，这些步骤以递归方式执行。这两个步骤是 fork 步骤和 join 步骤。

### Fork

使用 fork 和 join 原理的任务可以将自身分解为多干个可以并发执行的子任务。如下图所示：

![](http://tutorials.jenkov.com/images/java-concurrency-utils/java-fork-and-join-1.png)

通过将任务分解为若干个子任务，每个子任务都可以在不同的 CPU 上，或者同一个 CPU 上不同线程中并行执行。

如果给定任务的工作足够大，则任务只能将自身拆分为子任务。将任务拆分为子任务会产生开销，因此对于少量工作，此开销可能会大于同时执行子任务所实现的加速。

何时适合将任务分解到子任务中的合理时限也称为阈值。不同的任务合理的阈值各不相同。这在很大程度上取决于所完成的工作。

### Join

当一个任务已经被分解为若干子任务，则该任务会等待所有子任务全部执行完成。

一旦所有的子任务都执行完成，任务将会将所有的子结果合并为一个结果。如下图所示：

![](http://tutorials.jenkov.com/images/java-concurrency-utils/java-fork-and-join-2.png)

当然，并非所有类型的任务都可能返回结果。如果任务未返回结果，则任务仅等待其子任务完成。这样就不会进行结果合并。

## ForkJoinPool

`ForkJoinPool` 是一种特殊的线程池，被设计为完美适配 fork-and-join 任务分解。 `ForkJoinPool` 位于 `java.util.concurrent` 包中，完整类名 `java.util.concurrent.ForkJoinPool`。

### 创建 ForkJoinPool

你可以使用构造器创建 `ForkJoinPool`。你可以将所有的并行度作为 `ForkJoinPool` 构造函数的参数，并行度表示要在传递给 `ForkJoinPool` 的任务同时使用多少个线程或 CPU。这是一个 `ForkJoinPool` 创建示例：

```java
ForkJoinPool forkJoinPool = new ForkJoinPool(4);
```

本示例创建一个并行度水平为 4 的 `ForkJoinPool` 。

### 向 ForkJoinPool 提交任务

您将任务提交给 `ForkJoinPool` 的方式类似于将任务提交给 `ExecutorService` 的方式。您可以提交两种类型的任务。一个不返回任何结果的任务（一个“action”），一个返回结果的任务（一个“task”）。这两种任务由 `RecursiveAction` 和 `RecursiveTask` 类表示。如何使用这两项任务以及如何提交这些任务将在以下各节中介绍。

## RecursiveAction

`RecursiveAction` 是一种不返回任何值的任务。它只是执行某些工作，比如，将数据写入磁盘然后退出。

`RecursiveAction` 可能仍然需要将它的工作分解为多哥分片，以便可以使用各自独立的线程或者 CPU 执行。

你可以通过实现子类来实现 `RecursiveAction` 。下面是 `RecursiveAction` 的例子：

```java
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.RecursiveAction;

public class MyRecursiveAction extends RecursiveAction {

    private long workLoad = 0;

    public MyRecursiveAction(long workLoad) {
        this.workLoad = workLoad;
    }

    @Override
    protected void compute() {

        //if work is above threshold, break tasks up into smaller tasks
        if(this.workLoad > 16) {
            System.out.println("Splitting workLoad : " + this.workLoad);

            List<MyRecursiveAction> subtasks =
                new ArrayList<MyRecursiveAction>();

            subtasks.addAll(createSubtasks());

            for(RecursiveAction subtask : subtasks){
                subtask.fork();
            }

        } else {
            System.out.println("Doing workLoad myself: " + this.workLoad);
        }
    }

    private List<MyRecursiveAction> createSubtasks() {
        List<MyRecursiveAction> subtasks =
            new ArrayList<MyRecursiveAction>();

        MyRecursiveAction subtask1 = new MyRecursiveAction(this.workLoad / 2);
        MyRecursiveAction subtask2 = new MyRecursiveAction(this.workLoad / 2);

        subtasks.add(subtask1);
        subtasks.add(subtask2);

        return subtasks;
    }

}
```

这个例子非常简化。`MyRecursiveAction` 只是将虚构的 `workLoad` 作为其构造函数的参数。如果 `workLoad` 高于某个阈值，则将工作拆分为多个子任务，这些子任务也调度执行（通过子任务的 `.fork()` 方法）。如果 `workLoad` 低于某个阈值，则该工作由 `MyRecursiveAction` 本身执行。

您可以像这样安排 `MyRecursiveAction` 执行：

```java
MyRecursiveAction myRecursiveAction = new MyRecursiveAction(24);

forkJoinPool.invoke(myRecursiveAction);
```

## RecursiveTask

 `RecursiveTask` 是一种返回结果的任务。它可以将任务分解为若干更小的任务，执行完成之后将所有小任务的结果合并为集合式结果。这种分解合并可能发生在多个层面。下面是一个 `RecursiveTask` 示例：

```java
import java.util.ArrayList;
import java.util.List;
import java.util.concurrent.RecursiveTask;
    
    
public class MyRecursiveTask extends RecursiveTask<Long> {

    private long workLoad = 0;

    public MyRecursiveTask(long workLoad) {
        this.workLoad = workLoad;
    }

    protected Long compute() {

        //if work is above threshold, break tasks up into smaller tasks
        if(this.workLoad > 16) {
            System.out.println("Splitting workLoad : " + this.workLoad);

            List<MyRecursiveTask> subtasks =
                new ArrayList<MyRecursiveTask>();
            subtasks.addAll(createSubtasks());

            for(MyRecursiveTask subtask : subtasks){
                subtask.fork();
            }

            long result = 0;
            for(MyRecursiveTask subtask : subtasks) {
                result += subtask.join();
            }
            return result;

        } else {
            System.out.println("Doing workLoad myself: " + this.workLoad);
            return workLoad * 3;
        }
    }

    private List<MyRecursiveTask> createSubtasks() {
        List<MyRecursiveTask> subtasks =
        new ArrayList<MyRecursiveTask>();

        MyRecursiveTask subtask1 = new MyRecursiveTask(this.workLoad / 2);
        MyRecursiveTask subtask2 = new MyRecursiveTask(this.workLoad / 2);

        subtasks.add(subtask1);
        subtasks.add(subtask2);

        return subtasks;
    }
}
```

这个例子类似于 `RecursiveAction` 示例，唯一不同是它返回一个结果。 `MyRecursiveTask` 扩展了 `RecursiveTask<Long>` ，这就意味着任务返回的结果是一个 `Long` 。

 `MyRecursiveTask` 示例也将任务分解为子任务，然后通过使用子任务的 `fork()` 方法调度执行。

另外，此示例然后通过调用每个子任务的 `join()` 方法接收每个子任务返回的结果。子任务结果将合并为更大的结果，然后将其返回。这种子任务结果的合并可能会针对多个递归级别进行递归发生。

您可以像这样调度 `RecursiveTask`：

```java
MyRecursiveTask myRecursiveTask = new MyRecursiveTask(128);

long mergedResult = forkJoinPool.invoke(myRecursiveTask);

System.out.println("mergedResult = " + mergedResult);    
```

注意如何通过调用 `ForkJoinPool.invoke()` 方法获取最终结果。

## ForkJoinPool 用户体验

似乎并不是每个人都对 Java 7 中的新 `ForkJoinPool` 感到同样满意。在搜索有关 `ForkJoinPool` 的经验和意见时，我遇到了以下批评：

[A Java Fork-Join Calamity](http://coopsoft.com/ar/CalamityArticle.html)

如果你打算在你的项目中使用 `ForkJoinPool` ，这就值得一读。

