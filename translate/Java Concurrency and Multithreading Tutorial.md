# [Java并发和多线程教程]([http://tutorials.jenkov.com/java-concurrency/index.html](http://tutorials.jenkov.com/java-concurrency/index.html))

Java *并发性*是一个涵盖Java平台上的多线程，并发和并行性的术语。其中包括Java并发工具，问题和解决方案。该Java并发教程涵盖了多线程的核心概念，并发构造，并发问题，成本以及与Java中多线程相关的好处。

## 什么是多线程？

多线程意味着您在同一应用程序中具有多个*执行线程*。线程就像执行应用程序的独立CPU。因此，多线程应用程序就像具有多个CPU同时执行代码不同部分的应用程序。

线程不等于CPU。通常，单个CPU将在多个线程之间共享其执行时间，并在给定的时间量内在每个线程的执行之间进行切换。也可以让应用程序的线程由不同的CPU执行。

## 为什么要多线程？

为什么要在应用程序中使用多线程有几个原因。多线程的一些最常见原因是：

- 更好地利用单个CPU。
- 更好地利用多个CPU或CPU内核。
- 关于响应性的更好的用户体验。
- 关于公平的更好的用户体验。

我将在以下各节中详细解释每个原因。

### 更好地利用单个CPU

最常见的原因之一是能够更好地利用计算机中的资源。例如，如果一个线程正在等待对通过网络发送的请求的响应，则另一线程可以同时使用CPU来执行其他操作。此外，如果计算机具有多个CPU，或者CPU具有多个执行核心，则多线程还可以帮助您的应用程序利用这些额外的CPU核心。

### 更好地利用多个CPU或CPU内核

如果计算机包含多个CPU或CPU包含多个执行核心，则您需要为应用程序使用多个线程才能使用所有CPU或CPU核心。单个线程最多只能使用一个CPU，如上所述，有时甚至不能完全利用单个CPU。

### 关于响应能力的更好的用户体验

使用多线程的另一个原因是为了提供更好的用户体验。例如，如果您单击GUI中的按钮，并导致通过网络发送请求，那么哪个线程执行此请求就很重要。如果使用的线程也正在更新GUI，则在GUI线程等待请求响应时，用户可能会遇到GUI“挂起”的情况。取而代之的是，这样的请求可以由背景线程执行，因此GUI线程可以自由地同时响应其他用户请求。

### 关于公平的更好的用户体验

第四个原因是在用户之间更公平地共享计算机资源。例如，假设一台服务器接收来自客户端的请求，并且只有一个线程来执行这些请求。如果客户端发送的请求要花费很长时间才能处理，则所有其他客户端的请求都必须等待，直到一个请求完成。通过使每个客户端的请求都由其自己的线程执行，则没有一个任务可以完全垄断CPU。

## 多线程与多任务

过去，一台计算机只有一个CPU，并且一次只能执行一个程序。大多数小型计算机的功能实际上不足以同时执行多个程序，因此没有尝试过。公平地讲，许多大型机系统能够一次执行多个程序的时间比个人计算机长得多。

### 多任务

后来出现了多任务处理，这意味着计算机可以同时执行多个程序（AKA任务或进程）。但是，这并不是真正的“同时”。单个CPU在程序之间共享。操作系统将在运行的程序之间进行切换，并在切换之前执行每个程序一会儿。

随着多任务处理，软件开发人员面临着新的挑战。程序不再假定拥有所有可用的CPU时间，也不拥有所有的内存或任何其他计算机资源。一个“好公民”程序应释放不再使用的所有资源，以便其他程序可以使用它们。

### 多线程

后来出现了多线程，这意味着您可以在同一程序中拥有多个执行线程。可以将执行线程视为执行程序的CPU。当您有多个线程执行同一程序时，就像在同一程序中执行多个CPU。

## 多线程很难

多线程是提高某些类型程序性能的好方法。但是，多线程处理比多任务处理更具挑战性。这些线程在同一程序中执行，因此同时在读取和写入相同的内存。这可能会导致在单线程程序中看不到的错误。在单个CPU机器上可能看不到其中一些错误，因为两个线程从未真正“同时”执行。但是，现代计算机配备了多核CPU，甚至还配备了多个CPU。这意味着可以由单独的内核或CPU同时执行单独的线程。

如果一个线程在另一个线程写入内存位置时读取了一个内存位置，那么第一个线程最终将读取什么值？旧值？第二个线程写的值？还是两者之间混合的值？或者，如果两个线程正在同时写入同一内存位置，那么完成后将剩下什么值？由第一个线程写的值？第二个线程写的值？还是两个值的混合编写？

没有适当的预防措施，任何这些结果都是可能的。该行为甚至是不可预测的。结果可能会不时改变。因此，作为开发人员，重要的是要知道如何采取正确的预防措施-意味着学习控制线程如何访问共享资源（如内存，文件，数据库等）。这是本Java并发性教程解决的主题之一。

## Java中的多线程和并发

Java是最早使开发人员可以使用多线程的语言之一。Java从一开始就具有多线程功能。因此，Java开发人员经常会遇到上述问题。这就是我在Java并发上编写此线索的原因。谨此提醒自己，以及可能从中受益的其他Java开发人员。

本教程主要关注Java中的多线程，但是多线程中发生的某些问题类似于多任务和分布式系统中发生的问题。因此，对多任务和分布式系统的引用也可能出现在此线索中。因此，单词“并发”而不是“多线程”。

## 并发模型

第一个Java *并发模型*假定在同一应用程序中执行的多个线程也将共享对象。这种类型的并发模型通常称为“共享状态并发模型”。许多并发语言构造和实用程序都旨在支持此并发模型。

但是，自从编写第一本Java并发书籍以来，甚至自Java 5并发实用工具发布以来，并发体系结构和设计领域已经发生了很多事情。

共享状态并发模型导致许多并发问题，这些问题很难优雅地解决。因此，被称为“无共享”或“分离状态”的替代并发模型已经普及。在单独的状态并发模型中，线程不共享任何对象或数据。这避免了共享状态并发模型的许多并发访问问题。

出现了新的异步“独立状态”平台和工具包，例如Netty，Vert.x和Play / Akka和Qbit。新的非阻塞并发算法已经发布，并且新的非阻塞工具（例如LMax Disrupter）已添加到我们的工具箱中。Java 7中的Fork and Join框架和Java 8中的collection stream API引入了新的函数式编程并行性。

通过所有这些新开发，现在是时候更新本Java Concurrency教程了。因此，本教程再次**进行中**。只要有时间编写新教程，它们就会发布。



## Java并发学习指南

如果您不熟悉Java并发，建议您遵循以下学习计划。您也可以在此页面左侧的菜单中找到所有主题的链接。

通用并发和多线程理论：

- [多线程的好处](http://tutorials.jenkov.com/java-concurrency/benefits.html)
- [多线程成本](http://tutorials.jenkov.com/java-concurrency/costs.html)
- [并发模型](http://tutorials.jenkov.com/java-concurrency/concurrency-models.html)
- [同线程](http://tutorials.jenkov.com/java-concurrency/same-threading.html)
- [并发与并行](http://tutorials.jenkov.com/java-concurrency/concurrency-vs-parallelism.html)

Java并发基础知识：

- [创建和启动Java线程](http://tutorials.jenkov.com/java-concurrency/creating-and-starting-threads.html)
- [比赛条件和关键部分](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html)
- [线程安全和共享资源](http://tutorials.jenkov.com/java-concurrency/thread-safety.html)
- [线程安全性和不变性](http://tutorials.jenkov.com/java-concurrency/thread-safety-and-immutability.html)
- [Java内存模型](http://tutorials.jenkov.com/java-concurrency/java-memory-model.html)
- [Java同步块](http://tutorials.jenkov.com/java-concurrency/synchronized.html)
- [Java易失关键字](http://tutorials.jenkov.com/java-concurrency/volatile.html)
- [Java ThreadLocal](http://tutorials.jenkov.com/java-concurrency/threadlocal.html)
- [Java线程信令](http://tutorials.jenkov.com/java-concurrency/thread-signaling.html)

Java并发性的典型问题：

- [僵局](http://tutorials.jenkov.com/java-concurrency/deadlock.html)
- [防止死锁](http://tutorials.jenkov.com/java-concurrency/deadlock-prevention.html)
- [饥饿与公平](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html)
- [嵌套监视器锁定](http://tutorials.jenkov.com/java-concurrency/nested-monitor-lockout.html)
- [滑倒条件](http://tutorials.jenkov.com/java-concurrency/slipped-conditions.html)

Java并发构造可帮助解决上述问题：

- [Java锁](http://tutorials.jenkov.com/java-concurrency/locks.html)
- [Java中的读/写锁](http://tutorials.jenkov.com/java-concurrency/read-write-locks.html)
- [重入锁定](http://tutorials.jenkov.com/java-concurrency/reentrance-lockout.html)
- [信号量](http://tutorials.jenkov.com/java-concurrency/semaphores.html)
- [阻塞队列](http://tutorials.jenkov.com/java-concurrency/blocking-queues.html)
- [线程池](http://tutorials.jenkov.com/java-concurrency/thread-pools.html)
- [比较和交换](http://tutorials.jenkov.com/java-concurrency/compare-and-swap.html)

Java并发实用程序（java.util.concurrent）：

- [Java并发实用程序-java.util.concurrent](http://tutorials.jenkov.com/java-util-concurrent/index.html)

进一步的主题：

- [同步器的解剖](http://tutorials.jenkov.com/java-concurrency/anatomy-of-a-synchronizer.html)
- [非阻塞算法](http://tutorials.jenkov.com/java-concurrency/non-blocking-algorithms.html)
- [阿姆达尔定律](http://tutorials.jenkov.com/java-concurrency/amdahls-law.html)
- [参考文献](http://tutorials.jenkov.com/java-concurrency/references.html)

# 多线程的好处

多线程的最大好处是：

- 更高的CPU利用率。
- 在某些情况下，程序设计更简单。
- 响应速度更快的程序。
- 在不同任务之间更公平地分配CPU资源。

## 更好的CPU使用率

想象一个应用程序从本地文件系统读取和处理文件。假设从磁盘读取af文件需要5秒钟，而处理则需要2秒钟。然后处理两个文件

```
  5秒钟读取文件A
  2秒处理文件A
  5秒钟读取文件B
  2秒处理文件B
-----------------------
 总共14秒
```

从磁盘读取文件时，大部分的CPU时间都花在等待磁盘读取数据上。在这段时间内，CPU几乎处于空闲状态。它可能正在做其他事情。通过更改操作顺序，可以更好地利用CPU。查看以下顺序：

```
  5秒钟读取文件A
  5秒读取文件B + 2秒处理文件A
  2秒处理文件B
-----------------------
 总共12秒
```

CPU等待读取第一个文件。然后，它开始读取第二个文件。当计算机的IO组件读取第二个文件时，CPU处理第一个文件。请记住，在等待从磁盘读取文件时，CPU大部分处于空闲状态。

通常，CPU在等待IO时可以做其他事情。不必是磁盘IO。它也可以是网络IO，也可以是来自计算机用户的输入。网络和磁盘IO通常比CPU和内存IO慢很多。

## 程序设计更简单

如果要在单线程应用程序中手动编写上述读取和处理的顺序，则必须跟踪每个文件的读取和处理状态。相反，您可以启动两个线程，每个线程仅读取和处理一个文件。这些等待线程将在等待磁盘读取其文件时被阻止。在等待时，其他线程可以使用CPU处理已读取的文件部分。结果是磁盘始终保持忙碌状态，将各种文件读入内存。这样可以更好地利用磁盘和CPU。编程也更容易，因为每个线程只需要跟踪一个文件即可。

## 更多响应程序

将单线程应用程序转换为多线程应用程序的另一个共同目标是实现响应速度更快的应用程序。想象一个服务器应用程序在某个端口上侦听传入的请求。收到请求后，它将处理该请求，然后返回监听。服务器循环如下所示：

```
  而（服务器处于活动状态）{
    听请求
    处理要求
  }
```

如果请求需要很长时间才能处理，则在此期间内没有新客户端可以将请求发送到服务器。只有在服务器正在侦听时，才能接收请求。

另一种设计是侦听线程将请求传递给工作线程，然后立即返回侦听。工作线程将处理该请求，并将回复发送给客户端。该设计如下所示：

```
  而（服务器处于活动状态）{
    听请求
    手动请求工人线程
  }
```

这样，服务器线程将尽快恢复监听。因此，更多的客户端可以将请求发送到服务器。服务器变得更加敏感。

桌面应用程序也是如此。如果单击启动长任务的按钮，并且执行任务的线程是更新窗口，按钮等的线程，则任务执行时应用程序将显示为无响应。而是可以将任务移交给工作线程。当工作线程忙于任务时，窗口线程可以自由响应其他用户请求。当工作线程完成时，它向窗口线程发出信号。然后，窗口线程可以使用任务结果更新应用程序窗口。具有工作线程设计的程序将对用户响应更快。

## 更公平地分配CPU资源

假设有一个服务器正在接收来自客户端的请求。然后想象一下，其中一个客户端发送了一个处理时间很长的请求，例如10秒。如果服务器使用单个线程处理所有任务，则处理缓慢的请求之后的所有请求将被迫等待，直到处理完完整的请求为止。

通过在多个线程之间划分CPU时间并在线程之间进行切换，CPU可以在多个请求之间更公平地共享其执行时间。这样，即使其中一个请求较慢，也可以与较慢的请求同时执行处理速度更快的其他请求。当然，这意味着执行慢速请求的速度甚至会更慢，因为它不会仅将CPU分配给处理它。但是，其他请求将不得不等待更短的时间来处理，因为它们不必等待缓慢的任务完成才可以处理它们。如果只有慢请求要处理，则仍可以将CPU单独分配给慢任务。

# 多线程成本

从单线程应用程序到多线程应用程序不仅会带来好处。它也有一些费用。不要仅仅因为可以就启用多线程应用程序。您应该有一个好主意，即这样做所带来的收益大于成本。如有疑问，请尝试评估应用程序的性能或响应能力，而不仅仅是猜测。

## 更复杂的设计

尽管多线程应用程序的某些部分比单线程应用程序简单，但其他部分则更复杂。由多个线程访问共享数据执行的代码需要特别注意。线程交互远非总是那么简单。错误线程同步引起的错误很难检测，重现和修复。

## 上下文切换开销

当CPU从执行一个线程切换到执行另一个线程时，CPU需要保存当前线程的本地数据，程序指针等，并加载要执行的下一个线程的本地数据，程序指针等。此开关称为“上下文开关”。CPU从在一个线程的上下文中执行切换为在另一个线程的上下文中执行。

上下文切换并不便宜。您不想在线程之间进行不必要的切换。

您可以在Wikipedia上阅读有关上下文切换的更多信息：

[http://en.wikipedia.org/wiki/Context_switch](http://en.wikipedia.org/wiki/Context_switch)

## 资源消耗增加

线程需要计算机中的一些资源才能运行。除了CPU时间外，线程还需要一些内存来保留其本地堆栈。它还可能会占用操作系统中管理线程所需的一些资源。尝试创建一个程序，该程序创建的100个线程除了等待外什么也不做，并查看应用程序在运行时需要占用多少内存。

