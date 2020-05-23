## ThreadLocal 值的懒设定

某些情况下你无法使用标准方法设定初始值。比如，也许你需要某些配置信息，而这些信息在你创建 `ThreadLocal` 时不可用。这种情况下，你可以推迟设定初始值。下面是示例：

```java
public class MyDateFormatter {

    private ThreadLocal<SimpleDateFormat> simpleDateFormatThreadLocal = new ThreadLocal<>();

    public String format(Date date) {
        SimpleDateFormat simpleDateFormat = getThreadLocalSimpleDateFormat();
        return simpleDateFormat.format(date);
    }
    
    
    private SimpleDateFormat getThreadLocalSimpleDateFormat() {
        SimpleDateFormat simpleDateFormat = simpleDateFormatThreadLocal.get();
        if(simpleDateFormat == null) {
            simpleDateFormat = new SimpleDateFormat("yyyy-MM-dd HH:mm:ss");
            simpleDateFormatThreadLocal.set(simpleDateFormat);
        }
        return simpleDateFormat;
    }
}
```

请注意，`format()` 方法如何调用 `getThreadLocalSimpleDateFormat()` 方法以获得 [Java SimpleDatFormat](http://tutorials.jenkov.com/java-internationalization/simpledateformat.html) 实例。如果尚未在 `ThreadLocal` 中设置 `SimpleDateFormat` 实例，则会创建一个新的 `SimpleDateFormat` 并在 `ThreadLocal` 变量中进行设置。一旦线程在 `ThreadLocal` 变量中设置了自己的 `SimpleDateFormat`，就将该 `SimpleDateFormat` 对象用于该线程，并且仅适用于该线程。每个线程都创建自己的 `SimpleDateFormat` 实例，因为它们看不到在 `ThreadLocal` 变量上设置的其他实例。

`SimpleDateFormat` 类本身不是线程安全的，因此多个线程不能同时使用它。为了解决此问题，例子中的 `MyDateFormatter` 类为每个线程创建了一个 `SimpleDateFormat` ，因而每个线程调用 `format()` 方法将使用各自的 `SimpleDateFormat` 实例。

## 将 ThreadLocal 与线程池或 ExecutorService 一起使用

如果你打算使用来自传递给 [Java Thread Pool](http://tutorials.jenkov.com/java-concurrency/thread-pools.html) 或者 [Java ExecutorService](http://tutorials.jenkov.com/java-util-concurrent/executorservice.html) 的任务内部的 `ThreadLocal` ，请注意，你无法得到任何保证哪个线程将会执行你的任务。不过，如果你所需要的仅仅是保证每个线程使用各自的某些对象的实例，这就不是问题。你可以放心地将 Java `ThreadLocal` 与线程池或者 `ExecutorService` 一起使用。

## 完整的 ThreadLocal 示例

下面是一个完整可运行的 Java `ThreadLocal` 示例：

```java
public class ThreadLocalExample {

    public static void main(String[] args) {
        MyRunnable sharedRunnableInstance = new MyRunnable();

        Thread thread1 = new Thread(sharedRunnableInstance);
        Thread thread2 = new Thread(sharedRunnableInstance);

        thread1.start();
        thread2.start();

        thread1.join(); //wait for thread 1 to terminate
        thread2.join(); //wait for thread 2 to terminate
    }

}
public class MyRunnable implements Runnable {

    private ThreadLocal<Integer> threadLocal = new ThreadLocal<Integer>();

    @Override
    public void run() {
        threadLocal.set( (int) (Math.random() * 100D) );

        try {
            Thread.sleep(2000);
        } catch (InterruptedException e) {
        }

        System.out.println(threadLocal.get());
    }
}
```

这个例子创建了一个 `MyRunnable` 实例，将其传递给两个不同线程。两个线程都执行 `run()` 方法，因此会设定不同的值到 `ThreadLocal` 实例上。如果对方法 `set()` 的调用被同步过了，而它此时又不是一个 `ThreadLocal` 对象，则第二个线程将会覆盖第一个线程设定的值。

不过，由于它是个 `ThreadLocal` 对象，则两个线程无法看到对方设定的值。因此，它们各自设定并得到不同的值。

## InheritableThreadLocal

`InheritableThreadLocal` 类是 `ThreadLocal` 的一个子类。不像每个线程在 `ThreadLocal` 内部都有各自的值，`InheritableThreadLocal` 允许一个线程和该线程所创建的所有子线程访问同一个值。