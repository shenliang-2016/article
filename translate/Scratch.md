#### `Joins`

`join`方法允许一个线程等待另一个线程的完成。如果`t`是其线程当前正在执行的`Thread`对象，

```java
t.join();
```

导致当前线程暂停执行，直到`t`的线程终止。`join`过载允许程序员指定等待时长。但是，与`sleep`一样，`join`依赖于操作系统进行计时，因此您不应该假设`join`将等待您指定的时间。

与`sleep`一样，`join`通过响应`InterruptedException`退出的方式来响应中断。

#### 线程的简单示例

以下示例汇总了本节的一些概念。`SimpleThreads`由两个线程组成。第一个是每个Java应用程序都有的主线程。主线程从`Runnable`对象`MessageLoop`创建一个新线程，并等待它完成。如果`MessageLoop`线程需要很长时间才能完成，主线程会中断它。

`MessageLoop`线程打印出一系列消息。如果在打印完所有消息之前中断，`MessageLoop`线程将打印一条消息并退出。

```java
public class SimpleThreads {

    // Display a message, preceded by
    // the name of the current thread
    static void threadMessage(String message) {
        String threadName =
            Thread.currentThread().getName();
        System.out.format("%s: %s%n",
                          threadName,
                          message);
    }

    private static class MessageLoop
        implements Runnable {
        public void run() {
            String importantInfo[] = {
                "Mares eat oats",
                "Does eat oats",
                "Little lambs eat ivy",
                "A kid will eat ivy too"
            };
            try {
                for (int i = 0;
                     i < importantInfo.length;
                     i++) {
                    // Pause for 4 seconds
                    Thread.sleep(4000);
                    // Print a message
                    threadMessage(importantInfo[i]);
                }
            } catch (InterruptedException e) {
                threadMessage("I wasn't done!");
            }
        }
    }

    public static void main(String args[])
        throws InterruptedException {

        // Delay, in milliseconds before
        // we interrupt MessageLoop
        // thread (default one hour).
        long patience = 1000 * 60 * 60;

        // If command line argument
        // present, gives patience
        // in seconds.
        if (args.length > 0) {
            try {
                patience = Long.parseLong(args[0]) * 1000;
            } catch (NumberFormatException e) {
                System.err.println("Argument must be an integer.");
                System.exit(1);
            }
        }

        threadMessage("Starting MessageLoop thread");
        long startTime = System.currentTimeMillis();
        Thread t = new Thread(new MessageLoop());
        t.start();

        threadMessage("Waiting for MessageLoop thread to finish");
        // loop until MessageLoop
        // thread exits
        while (t.isAlive()) {
            threadMessage("Still waiting...");
            // Wait maximum of 1 second
            // for MessageLoop thread
            // to finish.
            t.join(1000);
            if (((System.currentTimeMillis() - startTime) > patience)
                  && t.isAlive()) {
                threadMessage("Tired of waiting!");
                t.interrupt();
                // Shouldn't be long now
                // -- wait indefinitely
                t.join();
            }
        }
        threadMessage("Finally!");
    }
}
```

