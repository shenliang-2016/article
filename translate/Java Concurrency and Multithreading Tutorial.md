# Java并发和多线程教程

http://tutorials.jenkov.com/java-concurrency/index.html



Java *并发性*是一个涵盖Java平台上的多线程，并发和并行性的术语。其中包括Java并发工具，问题和解决方案。该Java并发教程涵盖了多线程的核心概念，并发构造，并发问题，成本以及与Java中多线程相关的好处。

## 什么是多线程？

多线程意味着您在同一应用程序中具有多个*执行线程*。线程就像执行应用程序的独立CPU。因此，多线程应用程序就像具有多个CPU同时执行代码不同部分的应用程序。

![](http://tutorials.jenkov.com/images/java-concurrency/introduction-1.png)

线程不等于CPU。通常，单个CPU将在多个线程之间共享其执行时间，并在给定的时间量内在每个线程的执行之间进行切换。也可以让应用程序的线程由不同的CPU执行。

![](http://tutorials.jenkov.com/images/java-concurrency/introduction-2.png)

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

![](http://tutorials.jenkov.com/images/java-concurrency/java-concurrency-tutorial-introduction-1.png)

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



# 并发模型

可以使用不同的*并发模型*来实现并发系统。一*并发模型*指定的系统协作线程如何完成他们给予的任务。不同的并发模型以不同的方式拆分任务，线程可以以不同的方式进行通信和协作。本并发模型教程将更深入地介绍撰写本文时（2015年至2019年）使用的最受欢迎的并发模型。

## 并发模型和分布式系统的相似性

本文中描述的并发模型类似于分布式系统中使用的不同体系结构。在并发系统中，不同的线程彼此通信。在分布式系统中，不同的进程相互通信（可能在不同的计算机上）。线程和进程本质上非常相似。这就是为什么不同的并发模型通常看起来与不同的分布式系统体系结构相似的原因。

当然，分布式系统还面临着额外的挑战，即网络可能会失败，或者远程计算机或进程出现故障等。但是，如果CPU发生故障，网卡发生故障，磁盘发生故障，则在大型服务器上运行的并发系统可能会遇到类似的问题。失败的可能性可能会更低，但理论上仍会发生。

由于并发模型与分布式系统体系结构相似，因此它们经常可以相互借鉴。例如，用于在工作者（线程）之间分配工作的模型通常类似于[分布式系统中](http://tutorials.jenkov.com/software-architecture/load-balancing.html)的[负载平衡](http://tutorials.jenkov.com/software-architecture/load-balancing.html)模型。错误处理技术（例如日志记录，故障转移，任务的幂等）也是如此。

## 共享状态与分离状态

并发模型的一个重要方面是，组件和线程是设计为在线程之间共享状态，还是要具有从未在线程之间共享的单独状态。

*共享状态*意味着系统中的不同线程将在它们之间共享某些状态。通过*状态*是指一些数据，通常是一个或多个对象或相似。当线程共享状态时，可能会出现[争用条件](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html) 和[死锁](http://tutorials.jenkov.com/java-concurrency/deadlock.html)等问题。当然，这取决于线程如何使用和访问共享对象。

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-0-1.png)

*分开的状态*意味着系统中的不同线程在它们之间不共享任何状态。万一不同的线程需要通信，它们可以通过在它们之间交换不可变对象或通过在它们之间发送对象（或数据）的副本来进行通信。因此，当没有两个线程写入同一对象（数据/状态）时，可以避免大多数常见的并发问题。

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-0-2.png)

使用单独的状态并发设计通常可以使代码的某些部分更易于实现和推理，因为您知道只有一个线程将写入给定对象。您不必担心并发访问该对象。但是，使用单独的状态并发性，您可能需要更全面地考虑应用程序设计。我觉得这是值得的。我个人更喜欢单独的状态并发设计。

## 并行工作者

第一个并发模型是我所说的*并行工作器*模型。传入的工作分配给不同的工作者。这是说明并行工作程序并发模型的图：

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-1.png)

在并行工作者并发模型中，委托者将传入的作业分配给不同的工作者。每个工作者完成全部工作。这些工作程序并行工作，在不同的线程中运行，并可能在不同的CPU上运行。

如果在汽车制造厂实施并行工作者模型，则每辆汽车将由一名工人生产。工人将获得要制造的汽车的规格，并会从头到尾制造所有东西。

并行工作程序并发模型是Java应用程序中最常用的并发模型（尽管正在改变）。[java.util.concurrent Java包](http://tutorials.jenkov.com/java-util-concurrent/index.html) 中的许多并发实用[程序](http://tutorials.jenkov.com/java-util-concurrent/index.html)都是设计用于此模型的。您还可以在Java Enterprise Edition应用程序服务器的设计中看到此模型的痕迹。

## 并行工作者的优势

并行工作程序并发模型的优点是易于理解。为了增加应用程序的并行化，您只需添加更多工作程序即可。

例如，如果您正在实施Web搜寻器，则可以使用不同数量的工作程序来搜寻一定数量的页面，并查看哪个数字提供了最短的总搜寻时间（意味着最高的性能）。由于Web爬网是一项IO密集型工作，您最终可能会为计算机中的每个CPU /内核使用几个线程。每个CPU一个线程太少了，因为它在等待数据下载时会处于许多空闲状态。

## 并行工作者的劣势

但是，并行工作程序并发模型具有一些隐藏在简单表面下的缺点。我将在以下各节中解释最明显的缺点。

### 共享状态会变得复杂

实际上，并行工作程序并发模型比上面说明的要复杂一些。共享工作者经常需要访问内存或共享数据库中的某种共享数据。下图显示了如何使并行工作者并发模型复杂化：

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-2.png)

这种共享状态中的某些处于诸如工作队列之类的通信机制中。但是这种共享状态中的一些是业务数据，数据缓存，与数据库的连接池等。

一旦共享状态潜入并行工作程序并发模型中，它就会开始变得复杂。线程需要以确保一个线程的更改对其他线程可见的方式访问共享数据（将其推送到主内存中，而不仅仅是停留在执行该线程的CPU的CPU缓存中）。线程需要避免[争用条件](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html)， [死锁](http://tutorials.jenkov.com/java-concurrency/deadlock.html)和许多其他共享状态并发问题。

此外，当线程在访问共享数据结构时互相等待时，并行化的一部分会丢失。许多并发数据结构正在阻塞，这意味着一个或一组有限的线程可以在任何给定时间访问它们。这可能导致对这些共享数据结构的争用。高竞争本质上将导致访问共享数据结构的部分代码的执行序列化。

现代[的非阻塞并发算法](http://tutorials.jenkov.com/java-concurrency/non-blocking-algorithms.html)可以减少争用并提高性能，但是很难实现非阻塞算法。

持久数据结构是另一种选择。永久数据结构在修改后始终保留其自身的先前版本。因此，如果多个线程指向相同的持久数据结构，并且一个线程对其进行了修改，则修改线程将获得对新结构的引用。所有其他线程保留对旧结构的引用，该旧结构仍保持不变，因此是一致的。Scala编程包含几个持久数据结构。

虽然持久性数据结构是对共享数据结构进行并发修改的理想解决方案，但持久性数据结构往往无法很好地执行。

例如，一个持久列表会将所有新元素添加到列表的开头，并返回对新添加元素的引用（该引用随后指向列表的其余部分）。所有其他线程仍保留对列表中先前第一个元素的引用，并且对这些线程而言，列表保持不变。他们看不到新添加的元素。

这样的持久列表被实现为链接列表。不幸的是，链表在现代硬件上的表现不佳。列表中的每个元素都是一个单独的对象，这些对象可以分布在整个计算机的内存中。现代CPU顺序访问数据的速度要快得多，因此在现代硬件上，从阵列顶部实现的列表中可以获得更高的性能。数组顺序存储数据。CPU高速缓存可以一次将更大的阵列块加载到高速缓存中，并让CPU在加载后直接访问CPU高速缓存中的数据。对于链表，将元素分散在整个RAM上，这实际上是不可能的。

### 无状态工作者

共享状态可以由系统中的其他线程修改。因此，工作者必须在需要时重新读取该状态，以确保该状态在最新副本上正常工作。无论共享状态是保留在内存中还是外部数据库中，都是如此。不在内部保持状态（但每次需要时都会重新读取*状态*）的工作者称为*无状态的*。

每次需要时重新读取数据都会变慢。特别是如果状态存储在外部数据库中。

### 作业排序是不确定的

并行工作程序模型的另一个缺点是作业执行顺序是不确定的。无法保证首先执行或最后执行哪些作业。作业A可以在作业B之前提供给工人，但作业B可以在作业A之前执行。

并行工作程序模型的不确定性使得很难在任何给定的时间点推断系统状态。这也使得很难（如果不是不可能的话）保证一项工作先于另一项工作发生。

## 流水线

第二种并发模型是我所说的*组装线*并发模型。我选择该名称只是为了适应早先的“并行工作者”隐喻。其他开发人员根据平台/社区使用其他名称（例如，反应系统或事件驱动的系统）。这是说明组装线并发模型的图：

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-3.png)

工作者的组织就像工厂中装配线的工人一样。每个工人仅完成全部工作的一部分。完成该部分后，工人会将工作转发给下一个工人。

每个工作程序都在自己的线程中运行，并且不与其他工作程序共享任何状态。有时也称为*无共享*并发模型。

使用组装线并发模型的系统通常设计为使用非阻塞IO。无阻塞IO意味着当工作者开始IO操作（例如，从网络连接读取文件或数据）时，工作者不会等待IO调用完成。IO操作很慢，因此等待IO操作完成会浪费CPU时间。同时，CPU可能正在做其他事情。IO操作完成后，IO操作的结果（例如，读取的数据或写入的数据的状态）将传递给另一个工作者。

使用非阻塞IO，IO操作将确定工作线程之间的边界。在必须启动IO操作之前，工作者将尽其所能。然后，它放弃了对工作的控制。IO操作完成后，装配线中的下一个工作者将继续工作，直到必须开始IO操作等为止。

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-4.png)

实际上，作业可能不会沿着一条装配线流动。由于大多数系统可以执行一项以上的工作，因此工作会根据需要完成的工作在工作者之间流动。实际上，可能同时存在多个不同的虚拟装配线。这是现实中流水线系统中的工作流的样子：

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-5.png)

甚至可以将作业转发给多个工作者进行并行处理。例如，可以将作业转发给作业执行者和作业记录器。此图说明了三个装配线如何通过将其作业转发给同一工作者（中间装配线中的最后一个工作者）来完成：

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-6.png)

流水线甚至比这还要复杂。

### 反应式，事件驱动系统

使用组装线并发模型的*系统*有时也称为*反应式系统*或 *事件驱动系统*。系统的工作者会对系统中发生的事件做出反应，这些事件是从外界接收到的，或者是其他工作者发出的。事件的示例可能是传入的HTTP请求，或者某个文件已完成加载到内存等。

在撰写本文时，有许多有趣的反应/事件驱动平台可用，将来还会有更多。一些更受欢迎的似乎是：

- [Vert.x](http://tutorials.jenkov.com/vert.x/index.html)
- Akka
- Node.JS（JavaScript）

我个人认为Vert.x非常有趣（特别是对于像我这样的Java / JVM恐龙）。

### 参与者与通道

参与者和通道是装配线（或反应/事件驱动）模型的两个类似示例。

在参与者模型中，每个工作者都称为*参与者*。参与者可以直接彼此发送消息。消息是异步发送和处理的。如前所述，可以使用Actor来实现一个或多个作业处理装配线。这是说明参与者模型的图：

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-7.png)

在通道模型中，工作者不直接相互通信。相反，他们在不同的通道上发布消息（事件）。然后，其他工作者可以在这些通道上收听消息，而发件人不知道谁在收听。这是说明通道模型的图：

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-8.png)

在撰写本文时，通道模型对我来说似乎更灵活。工作者不需要知道稍后在装配线中将处理什么工作的工人。它只需要知道将作业转发到哪个通道（或将消息发送到等等）。通道上的侦听器可以订阅和取消订阅，而不会影响工作者对通道的写入。这允许工作者之间的耦合稍松一些。

## 流水线优势

与并行工作者模型相比，组装线并发模型具有多个优点。在以下各节中，我将介绍最大的优点。

### 没有共享状态

工作者与其他工作者不共享任何状态的事实意味着无需考虑并发访问共享状态可能引起的所有并发问题，就可以实现他们。这使实施工作者变得容易得多。您将工作程序实现为好像是执行该工作的唯一线程-本质上是单线程实现。

### 有状态的工作者

由于工作者知道没有其他线程修改其数据，因此工作者可以是有状态的。有状态的意思是他们可以将需要操作的数据保留在内存中，仅将更改写回最终的外部存储系统。因此，有状态工作者通常比无状态工作者更快。

### 更好的硬件整合

单线程代码的优势在于，它通常与底层硬件的工作方式更好地相符。首先，当您可以假定代码在单线程模式下执行时，通常可以创建更多优化的数据结构和算法。

其次，如上所述，单线程有状态工作者可以在内存中缓存数据。当数据缓存在内存中时，也更有可能将此数据也缓存在执行线程的CPU的CPU缓存中。这样可以更快地访问缓存的数据。

当以自然受益于底层硬件工作方式的方式编写代码时， 我将其称为*硬件一致性*。一些开发商称这种*机械同情*。我更喜欢“硬件一致性”一词，因为计算机几乎没有机械零件，并且在这种情况下，“同情”一词被用作“更好地匹配”的隐喻，我相信“符合”一词可以很好地传达。无论如何，这是挑剔的。使用您喜欢的任何术语。

### 可以进行工作排序

可以根据组装线并发模型以保证作业排序的方式实现并发系统。作业排序使在任何给定时间点推断系统状态变得更加容易。此外，您可以将所有传入的作业写入日志。然后，在系统的任何部分出现故障的情况下，可以使用此日志从头开始重建系统状态。作业以特定顺序写入日志，并且该顺序成为保证的作业顺序。这是这样的设计的外观：

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-models-8.png)

实施保证的工作订单不一定很容易，但是通常是可能的。如果可以的话，它可以极大地简化备份，还原数据，复制数据等任务，因为所有这些都可以通过日志文件来完成。

## 组装线的缺点

组装流水线并发模型的主要缺点是，作业的执行通常分散在多个工作者中，因此也分散在项目中的多个类中。因此，很难确切地知道给定作业正在执行什么代码。

编写代码也可能会更困难。辅助代码有时被编写为回调处理程序。具有许多嵌套回调处理程序的代码可能会导致某些开发人员称之为*回调地狱*。回调地狱只是意味着很难跟踪所有回调中代码的实际作用，以及确保每个回调都可以访问所需的数据。

使用并行工作程序并发模型，这往往会更容易。您可以打开工作程序代码，并从头到尾阅读几乎执行的代码。当然，并行工作程序代码也可以分布在许多不同的类上，但是执行顺序通常更容易从代码中读取。

## 函数式并行

函数式并行是第三种并发模型，最近（2015年）被广泛讨论。

函数并行性的基本思想是使用函数调用实现程序。功能可以看作是相互发送消息的“代理”或“角色”，就像在组装线并发模型（AKA反应或事件驱动系统）中一样。当一个函数调用另一个函数时，这类似于发送消息。

传递给函数的所有参数都将被复制，因此接收函数之外的任何实体都无法操纵数据。该复制对于避免共享数据出现争用情况至关重要。这使得函数执行类似于原子操作。每个函数调用都可以独立于任何其他函数调用执行。

当每个函数调用可以独立执行时，每个函数调用可以在单独的CPU上执行。这就是说，功能上实现的算法可以在多个CPU上并行执行。

使用Java 7，我们获得了`java.util.concurrent`包含[ForkAndJoinPool](http://tutorials.jenkov.com/java-util-concurrent/java-fork-and-join-forkjoinpool.html)的软件包，该软件包 可以帮助您实现类似于功能并行性的东西。使用Java 8，我们获得了并行[流](http://tutorials.jenkov.com/java-collections/streams.html) ，可以帮助您并行化大型集合的迭代。请记住，有些开发人员对此表示批评`ForkAndJoinPool`（您可以在本`ForkAndJoinPool`教程中找到批评的链接）。

关于函数并行性的难点是知道要并行调用哪些函数。跨CPU协调函数调用会带来开销。一个功能完成的工作单元必须具有一定的大小，才能负担此开销。如果函数调用很小，则尝试并行化它们实际上可能比单线程，单CPU执行慢。

根据我的理解（一点也不完美），您可以使用反应性，事件驱动的模型来实现算法，并实现类似于功能并行性的工作分解。使用均匀驱动的模型，您可以更好地控制要并行化的对象和数量（在我看来）。

另外，只有在该任务当前是程序唯一执行的任务时，才有意义地将任务分配给多个CPU，并产生开销。但是，如果系统正在同时执行多个其他任务（例如，Web服务器，数据库服务器和许多其他系统都在执行），则尝试并行化单个任务毫无意义。无论如何，计算机中的其他CPU都将忙于其他任务，因此没有理由尝试以较慢的，功能上并行的任务来打扰它们。组装流水线（反应式）并发模型可能会更好，因为它具有较少的开销（以单线程模式顺序执行），并且与底层硬件的工作方式更好地兼容。

## 哪种并发模型最好？

那么，哪种并发模型更好？

通常，答案是这取决于系统应该执行的操作。如果您的工作自然是并行的，独立的并且不需要共享状态，则可以使用并行工作器模型来实现系统。

但是，许多工作并非自然而然地平行和独立。对于这些类型的系统，我相信组装线并发模型的优点要大于缺点，比并行工作器模型要有更多的优点。

您甚至不必自己编写所有组装线基础结构的代码。像[Vert.x](http://tutorials.jenkov.com/vert.x/index.html)这样的现代平台 已经为您实现了很多功能。我个人将为下一个项目探索在Vert.x等平台上运行的设计。我觉得Java EE不再具有优势。



# 同线程

同线程是一种并发模型，其中单线程系统可扩展到N个单线程系统。结果是N个单线程系统并行运行。

同一个线程的系统不是纯粹的单线程系统，因为它包含多个线程。但是——每个线程都像单线程系统一样运行。因此，术语“ *同线程”*而不是“单线程”。

## 为什么选择单线程系统？

您可能想知道为什么今天有人设计单线程系统。单线程系统之所以受欢迎，是因为其并发模型比多线程系统简单得多。单线程系统不与其他线程共享任何状态（对象/数据）。这使单线程可以使用非并行数据结构，并更好地利用CPU和CPU缓存。

不幸的是，单线程系统不能完全利用现代CPU。现代CPU通常会多带2、4、6、8个内核。每个内核都充当一个单独的CPU。单线程系统只能使用其中一个内核，如下所示：

![](http://tutorials.jenkov.com/images/java-concurrency/same-threading-0.png)

## 同线程：单线程横向扩展

为了利用CPU中的所有内核，可以扩展单线程系统以利用整个计算机。

### 每个CPU一个线程

同线程系统通常在计算机中每个CPU运行1个线程。如果计算机包含4个CPU或具有4个内核的CPU，则通常会运行4个相同线程系统的实例（4个单线程系统）。下图显示了此原理：

![](http://tutorials.jenkov.com/images/java-concurrency/same-threading-0-1.png)

## 没有共享状态

同一个线程的系统看起来类似于传统的多线程系统，因为同一个线程的系统内部有多个线程在运行。但是有细微的差别。

同一线程系统与传统的多线程系统之间的区别在于，同一线程系统中的线程不共享状态。没有线程并行访问的共享内存。没有线程共享数据的并发数据结构等。此处说明了这种差异：

![](http://tutorials.jenkov.com/images/java-concurrency/same-threading-4.png)

缺少共享状态是导致每个线程在单线程系统下的行为。但是，由于同一个线程的系统可以包含多个线程——它实际上不是“单线程系统”。由于缺乏更好的名称，我发现将这样的系统称为*同线程*系统而不是“具有单线程设计的多线程系统” 更为精确。同线程更容易说，也更容易理解。

从本质上讲，相同线程意味着数据处理停留在同一线程内，并且同一线程系统中没有线程可以同时共享数据。有时，这也被称为 *没有共享状态*并发或*单独的状态*并发。

## 负荷分配

显然，同一个线程的系统需要在运行的单线程实例之间共享工作负载。如果只有一个线程可以完成任何工作，则该系统实际上将是单线程的。

究竟如何在不同线程上分配负载取决于系统的设计。我将在以下各节中介绍一些内容。

### 单线程微服务

如果您的系统包含多个微服务，则每个微服务都可以以单线程模式运行。当您将多个单线程微服务部署到同一台计算机上时，每个微服务都可以在单个CPU上运行单个线程。

微服务本质上不共享任何数据，因此微服务是同线程系统的一个很好的用例。

### 分片数据服务

如果您的系统确实确实需要共享数据，或者至少需要共享一个数据库，则可以对数据库进行分片。分片意味着将数据分为多个数据库。通常对数据进行划分，以使彼此相关的所有数据一起位于同一数据库中。例如，属于某个“所有者”实体的所有数据将被插入到同一数据库中。但是，分片不在本教程的讨论范围之内，因此您必须搜索有关该主题的教程。

## 线程通讯

如果同一线程系统中的线程需要通信，则可以通过消息传递进行通信。如果线程A要向线程B发送消息，则线程A可以通过生成消息（字节序列）来发送消息。然后，线程B可以复制该消息（字节序列）并读取它。通过复制消息，线程B确保线程A在读取消息时无法修改消息。复制后，线程A无法访问消息副本。

通过消息传递进行的线程通信如下所示：

![](http://tutorials.jenkov.com/images/java-concurrency/same-threading-5.png)

线程通信可以通过队列，管道，Unix套接字，TCP套接字等进行。无论您的系统适合什么。

## 更简单的并发模型

在同一线程系统中在自己线程中运行的每个系统都可以实现为单线程。这意味着内部并发模型变得比线程共享状态简单得多。您不必担心并发数据结构以及此类数据结构可能导致的所有并发问题。

## 插图

以下是单线程，多线程和同线程系统的图示，因此您可以更轻松地了解它们之间的区别。

第一个插图显示了一个单线程系统。

![](http://tutorials.jenkov.com/images/java-concurrency/same-threading-1.png)

第二个图显示了一个多线程系统，其中线程共享数据。

![](http://tutorials.jenkov.com/images/java-concurrency/same-threading-2.png)

第三幅图显示了一个具有2个线程且具有单独数据的同线程系统，它们通过相互传递消息进行通信。

![](http://tutorials.jenkov.com/images/java-concurrency/same-threading-3.png)

## Java线程操作

Thread Ops for Java 是一个开源工具包，旨在帮助您更轻松地实现单独的状态相同的线程系统。线程操作包含用于启动和停止单个线程以及通过单个线程实现某种程度的并发性的工具。如果您对使用相同线程的应用程序设计感兴趣，那么让 Thread Ops 看起来可能很有趣。您可以在我的 [Java线程操作教程中](http://tutorials.jenkov.com/thread-ops-java/index.html) 阅读有关线程操作的更多信息。



# 并发与并行

术语“ *并发性”*和“ *并行性”*通常与多线程程序有关。但是并发和并行性到底是什么意思，这两个术语有何不同？

我花了一些时间才终于了解并发和并行性之间的区别。因此，我决定在此Java并发教程中添加有关并发与并行性的文本。

## 并发

*并发*意味着应用程序同时（并发）在一项以上的任务上取得进展。好吧，如果计算机只有一个CPU，则应用程序可能无法 *在同一时间*同时完成一项以上的任务，而是在应用程序中一次要处理多个任务。在开始下一项任务之前，它并没有完全完成一项任务。而是，CPU在不同任务之间切换，直到任务完成为止。

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-vs-parallelism-1.png)

即使并发应用程序内部仅运行一个线程，也可以使用它。顺便说一下，这是我们（Nanosai）[Thread Ops](http://tutorials.jenkov.com/thread-ops-java/index.html)工具箱的目标之一。

## 并行性

并行是指应用程序将其任务分解为较小的子任务，这些子任务可以并行处理，例如，在同一时间在多个CPU上。

![](http://tutorials.jenkov.com/images/java-concurrency/concurrency-vs-parallelism-2.png)

为了实现真正的并行性，您的应用程序必须运行多个线程，或者至少能够调度要在其他线程，进程，CPU，图形卡等中执行的任务。

## 并发与并行的细节

如您所见，并发与应用程序如何处理其执行的多个任务有关。应用程序可以一次（顺序）处理一个任务，也可以同时（同时）处理多个任务。

另一方面，并行性与应用程序如何处理每个单独的任务有关。应用程序可以从头到尾顺序处理任务，或者将任务拆分为可以并行完成的子任务。

如您所见，应用程序可以是并发的，但不能并行。这意味着它可以同时处理多个任务，但是线程一次只能执行一个任务。在并行线程/ CPU中没有并行执行的任务。

应用程序也可以是并行的，但不能是并行的。这意味着该应用程序一次只能处理一个任务，并且该任务被分解为可以并行处理的子任务。但是，每个任务（+子任务）在拆分下一个任务并并行执行之前已完成。

此外，应用程序既不能是并发的，也不能是并行的。这意味着它一次只能处理一个任务，并且该任务永远不会分解为子任务以并行执行。

最后，应用程序也可以是并发和并行的，因为它既可以同时处理多个任务，又可以将每个任务分解为多个子任务以并行执行。但是，在这种情况下，并发性和并行性的某些好处可能会丢失，因为计算机中的CPU已经足够合理地仅使用并发性或并行性。结合使用它可能只会导致很小的性能提升，甚至导致性能下降。在盲目采用并发并行模型之前，请确保进行分析和衡量。



# 创建和启动Java线程

一个*Java的* *线程*就像是可以执行Java代码的虚拟CPU —— 你的Java应用程序中。启动Java应用程序时，其`main()`方法由*主线程*执行—— *主线程*是由Java VM创建以运行您的应用程序的特殊线程。在应用程序内部，您可以创建和启动更多线程，这些线程可以与主线程并行执行应用程序代码的某些部分。

Java线程是与任何其他Java对象一样的对象。线程是class的实例`java.lang.Thread`，或者此类的子类的实例。除了作为对象之外，java线程还可以执行代码。在本Java线程教程中，我将解释如何创建和启动线程。

## 创建和启动线程

用Java创建线程是这样完成的：

```java
Thread thread = new Thread();
```

要启动Java线程，您将调用其 `start()` 方法，如下所示：

```java
thread.start();
```

本示例未指定任何代码来执行线程。因此，线程在启动后将立即停止。

有两种方法可以指定线程应执行的代码。第一种是创建Thread的子类并覆盖该`run()`方法。第二种方法是将实现的对象`Runnable` （`java.lang.Runnable`）传递给 `Thread`构造函数。下面介绍这两种方法。

## 线程子类

指定线程运行什么代码的第一种方法是创建Thread的子类并重写该`run()`方法。该`run()`方法是调用`start()`后线程执行的操作。这是创建Java `Thread`子类的示例：

```java
  public class MyThread extends Thread {

    public void run(){
       System.out.println("MyThread running");
    }
  }
```

要创建并启动上述线程，您可以执行以下操作：

```java
  MyThread myThread = new MyThread();
  myTread.start();
```

`start()`线程启动后 ，调用将立即返回。它不会等到`run()`方法完成。该`run()`方法将像由其他CPU执行一样执行。该`run()`方法执行时，将打印出文本“ MyThread running”。

您也可以创建一个匿名子类，`Thread`如下所示：

```java
  Thread thread = new Thread(){
    public void run(){
      System.out.println("Thread Running");
    }
  }

  thread.start();
```

一旦`run()`新线程执行了该方法，此示例将打印出文本“ Thread running” 。

## Runnable 接口的实现

指定线程应运行什么代码的第二种方法是通过创建实现`java.lang.Runnable`接口的类。实现`Runnable`接口的Java对象可以由Java `Thread` 执行。本教程的稍后部分将介绍如何完成此操作。

`Runnable` 接口是Java平台随附的标准[Java接口](http://tutorials.jenkov.com/java/interfaces.html)。`Runnable`接口只有一个方法`run()`。`Runnable`接口基本上是这样的：

```java
public interface Runnable() {

    public void run();

}
```

`run()`方法的实现中必须包括线程在执行时应该执行的操作。有三种实现`Runnable`接口的方法：

1. 创建一个实现该`Runnable`接口的Java类。
2. 创建一个实现该`Runnable`接口的匿名类。
3. 创建一个实现`Runnable`接口的Java Lambda 。

以下各节将说明所有这三个选项。

### Java类实现 Runnable

实现Java `Runnable`接口的第一种方法是创建自己的实现该`Runnable`接口的Java类。这是实现`Runnable`接口的自定义Java类的示例：

```java
  public class MyRunnable implements Runnable {

    public void run(){
       System.out.println("MyRunnable running");
    }
  }
```

此`Runnable`实现的全部作用是打印出文本 `MyRunnable running`。打印完该文本后，`run()`方法退出，并且运行`run()`方法的线程将停止。

### Runnable 的匿名实现

您还可以创建`Runnable`的匿名实现。这是实现`Runnable`接口的匿名Java类的示例：

```java
Runnable myRunnable =
    new Runnable(){
        public void run(){
            System.out.println("Runnable running");
        }
    }
```

除了是一个匿名类之外，该示例与使用自定义类实现`Runnable`接口的示例非常相似。

### Java Lambda 实现 Runnable

实现`Runnable`接口的第三种方法是通过创建`Runnable`接口的 [Java Lambda](http://tutorials.jenkov.com/java/lambda-expressions.html)实现。这是可能的，因为`Runnable`接口仅具有单个未实现的方法，因此实际上（尽管可能是无意地）是 [函数式Java接口](http://tutorials.jenkov.com/java-functional-programming/functional-interfaces.html)。

这是实现`Runnable`接口的Java lambda表达式的示例：

```java
Runnable runnable =
        () -> { System.out.println("Lambda Runnable running"); };
```

### 用 Runnable 启动线程

要让`run()`方法由线程执行，请将实现`Runnable`接口的类，匿名类或lambda表达式的实例传递进入`Thread`的构造函数。如下所示：

```java
Runnable runnable = new MyRunnable(); // or an anonymous class, or lambda...

Thread thread = new Thread(runnable);
thread.start();
```

当线程启动时，它将调用`MyRunnable`实例的`run()`方法，而不是执行自己的`run()`方法。上面的示例将打印出文本“ MyRunnable running”。

## 选择子类还是 Runnable？

对于这两种方法中哪一种最好没有任何标准，两种方法均有效。不过，就我个人而言，我更喜欢实现`Runnable`，并将实现它的实例传递给`Thread`实例。当`Runnable`由[线程池](http://tutorials.jenkov.com/java-concurrency/creating-and-starting-threads.html)执行时，很容易将`Runnable` 实例排队，直到池中的线程空闲为止。`Thread`子类很难做到这一点。

有时您可能必须同时实现`Runnable`以及`Thread`子类。例如，如果创建的`Thread`子类可以执行多个`Runnable`。实现线程池时通常是这种情况。

## 常见陷阱：调用 run() 而不是 start()

创建和启动线程时，常见的错误是调用 `Thread` 的 `run()` 而不是 `start()`方法，如下所示：

```java
  Thread newThread = new Thread(MyRunnable());
  newThread.run();  //should be start();
```

刚开始您可能不会注意到任何事情，因为`Runnable`的`run()`方法按预期执行。但是，它不会由您刚刚创建的新线程执行。而是由创建线程的线程执行`run()`方法。换句话说，该线程执行了以上两行代码。要使新创建的线程 `newThread` 调用 `MyRunnable` 实例的 `run()`方法，必须调用 `newThread.start()` 方法。 

## 线程名称

创建Java线程时，可以为其命名。该名称可以帮助您区分不同的线程。例如，如果有多个线程写入， `System.out`可以很方便地查看哪个线程写入了文本。这是一个例子：

```java
   Thread thread = new Thread("New Thread") {
      public void run(){
        System.out.println("run by: " + getName());
      }
   };


   thread.start();
   System.out.println(thread.getName());
```

注意作为参数传递给`Thread`构造函数的字符串“ New Thread” 。此字符串是线程的名称。可以通过`Thread`的`getName()`方法获取名称。您也可以`Thread`在使用`Runnable`实现时将名称传递给。看起来是这样的：

```
   MyRunnable runnable = new MyRunnable();
   Thread thread = new Thread(runnable, "New Thread");

   thread.start();
   System.out.println(thread.getName());
```

但是请注意，由于`MyRunnable`类不是 `Thread`的子类，因此它无权访问执行它的线程的`getName()`方法。

## Thread.currentThread()

`Thread.currentThread()`方法返回对执行`currentThread()`的`Thread`实例的引用。这样，您可以访问`Thread`表示的执行给定代码块的线程的Java 对象。这是一个使用方法`Thread.currentThread()`的例子：

```
Thread thread = Thread.currentThread();
```

一旦有了对`Thread`对象的引用，就可以在其上调用方法。例如，您可以获取当前正在执行代码的线程的名称，如下所示：

```
String threadName = Thread.currentThread().getName();
```

## Java线程示例

这是一个小例子。首先，它打印出执行`main()`方法的线程的名称。该线程由JVM分配。然后启动10个线程，并给它们一个全名（`"" + i`）。然后，每个线程将其名称打印出来，然后停止执行。

```java
public class ThreadExample {

  public static void main(String[] args){
    System.out.println(Thread.currentThread().getName());
    for(int i=0; i<10; i++){
      new Thread("" + i){
        public void run(){
          System.out.println("Thread: " + getName() + " running");
        }
      }.start();
    }
  }
}
```

请注意，即使线程按顺序启动（1、2、3等），它们也可能不会顺序执行，这意味着线程1可能不是第一个将其名称写入`System.out`的线程。这是因为线程原则上是并行执行的，而不是顺序执行的。JVM和/或操作系统确定线程的执行顺序。此顺序不必与开始时的顺序相同。

## 暂停线程

线程可以通过调用 static 方法`Thread.sleep()`来暂停自身。`sleep()` 需要数毫秒作为参数。`sleep()`方法将尝试在恢复执行之前休眠该毫秒数。线程`sleep()`不是100％精确的，但还是很不错的。这是通过调用`Thread.sleep()`将Java线程暂停的示例：

```java
try {
    Thread.sleep(10L * 1000L);
} catch (InterruptedException e) {
    e.printStackTrace();
}
```

执行上述Java代码的线程将休眠大约10秒钟（10.000毫秒）。

## 停止线程

停止Java线程需要一些线程实现代码的准备。Java `Thread`类包含一个`stop()`方法，但已弃用。原始`stop()` 方法无法保证线程在什么状态下停止。这意味着，线程在执行过程中可以访问的所有Java对象将处于未知状态。如果您的应用程序中的其他线程也可以访问相同的对象，则您的应用程序可能会意外失败并且无法预期。

不必调用该`stop()`方法，您必须实现线程代码，以便可以将其停止。这是一个实现的类示例，`Runnable`其中包含一个称为的额外方法`doStop()`，该方法向`Runnable`发出停止信号。`Runnable`会检查这个信号，并当它准备好后停止。

```java
public class MyRunnable implements Runnable {

    private boolean doStop = false;

    public synchronized void doStop() {
        this.doStop = true;
    }

    private synchronized boolean keepRunning() {
        return this.doStop == false;
    }

    @Override
    public void run() {
        while(keepRunning()) {
            // keep doing what this thread should do.
            System.out.println("Running");

            try {
                Thread.sleep(3L * 1000L);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }

        }
    }
}
```

注意`doStop()`和`keepRunning()`方法。`doStop()`旨在被从另一个不同于执行调用`MyRunnable`的`run()` 方法的线程中调用。`keepRunning()`方法由执行 `MyRunnable`的`run()`方法的线程内部调用。只要`doStop()`尚未调用，该`keepRunning()`方法就会返回`true`——意味着执行`run()`方法的线程将继续运行。

这是一个启动执行上述`MyRunnable` 类的实例的Java线程，并在延迟后再次停止的示例：

```java
public class MyRunnableMain {

    public static void main(String[] args) {
        MyRunnable myRunnable = new MyRunnable();

        Thread thread = new Thread(myRunnable);

        thread.start();

        try {
            Thread.sleep(10L * 1000L);
        } catch (InterruptedException e) {
            e.printStackTrace();
        }

        myRunnable.doStop();
    }
}
```

本示例首先创建一个`MyRunnable`实例，然后将该实例传递给线程并启动该线程。然后执行该`main()`方法的线程（主线程）休眠10秒钟，然后调用`MyRunnable`实例的`doStop()`方法。这将导致执行该`MyRunnable`方法的线程停止，因为`keepRunning()`将在`doStop()`调用之后返回`true`。

请记住，如果您的`Runnable`实现不仅需要 `run()`方法（例如还需要 `stop()`或`pause()`方法），那么您将无法再使用Java lambda表达式创建`Runnable`实现。Java lambda只能实现一个方法。相反，您必须使用自定义类或扩展`Runnable`的自定义接口，该接口具有额外的方法，并且由匿名类实现。

# 竞争条件和临界区

竞争条件是可能发生在临界区内的特殊条件。所谓临界区是指由多个线程执行的代码段，多个线程的不同执行顺序会产生临界区并发执行的不同结果。

当多线程执行临界区的结果何时会有所不同取决于线程的执行顺序时，我们就说该临界区包含竞争条件。术语竞争条件来自这样的比喻：多个线程正在竞争通过临界区，这种竞争的结果影响了临界区执行的结果。

听起来好像有点复杂，所以接下来我会分别详细介绍它们。

## 临界区

在同一应用程序中运行多个线程本身不会导致问题。当多个线程访问相同的资源时，就会出现问题。例如，相同的内存（变量，数组或对象），系统（数据库，Web服务等）或文件。

实际上，仅当一个或多个线程写入这些资源时才会出现问题。只要资源不变，让多个线程读取相同的资源是安全的。

这是临界区的Java代码示例，如果同时由多个线程执行，则该示例可能会失败：

```java
  public class Counter {

     protected long count = 0;

     public void add(long value){
         this.count = this.count + value;
     }
  }
```

设想两个线程，A 和 B，正在执行同一个 `Counter` 类实例上的 `add` 方法。没有任何办法可以确知操作系统如何调度两个线程。`add()` 方法中的代码并不会作为一个原子指令被 JVM 执行。它会作为一系列更小的指令被执行，类似于：

1.从内存中读取 `this.count` 到寄存器中。
2.增加值到寄存器。
3.将寄存器写回内存。

观察当 A 和 B 像下面这样交错执行时会发生什么：

```
       this.count = 0;

   A:  Reads this.count into a register (0)
   B:  Reads this.count into a register (0)
   B:  Adds value 2 to register
   B:  Writes register value (2) back to memory. this.count now equals 2
   A:  Adds value 3 to register
   A:  Writes register value (3) back to memory. this.count now equals 3
```

这两个线程想将值 2 和 3 加到计数器上。因此，两个线程完成执行后，该值应为5。但是，由于两个线程的执行是交错的，因此结果最终会有所不同。

在上面列出的执行序列示例中，两个线程都从内存中读取值 0。然后，将各自的值 2 和 3 加到该值上，并将结果写回到内存中。`this.count`中剩下的值将是最后一个线程写入的值，而不是 5。在上述情况下，它是线程 A 的结果，但也可能是线程 B 的结果。

## 临界区中的竞争条件

前面示例中 `add()` 方法中的代码包含一个临界区。当多个线程执行此临界区时，就会出现竞争条件。

更正式地讲，两个线程争用同一资源的情况（竞争资源的顺序很重要）被称为竞争条件。导致竞争条件的代码段称为临界区。

## 预防竞争条件

为了防止出现竞争条件，您必须确保临界区作为原子指令执行。这意味着一旦一个线程执行了它，其他线程就无法执行它，直到第一个线程离开了临界区。

可以通过对临界区进行适当的线程同步来避免竞争条件。可以使用 [Java代码的同步块](http://tutorials.jenkov.com/java-concurrency/synchronized.html) 实现线程同步。线程同步也可以使用其他同步结构（例如 [locks](http://tutorials.jenkov.com/java-concurrency/locks.html) 或原子变量，例如 [java.util.concurrent.atomic.AtomicInteger](http://tutorials.jenkov.com/java-util-concurrent/atomicinteger.html)。

## 临界区吞吐量

对于多个较小的临界区，将整个临界区作为一个同步代码块是可行的。但是，对于较大的临界区，将其拆分为多个较小的临界区，以允许多个线程并发执行每个较小的临界区，可能是有好处的。这样做可以降低对共享资源的争用，因而提升整个临界区的吞吐量。

下面的简单的代码示例展示了这一点：

```java
public class TwoSums {
    
    private int sum1 = 0;
    private int sum2 = 0;
    
    public void add(int val1, int val2){
        synchronized(this){
            this.sum1 += val1;   
            this.sum2 += val2;
        }
    }
}
```

注意 `add()` 方法如何将值添加到两个不同的 `sum` 成员变量。为了防止竞争条件，求和是在Java同步块内执行的。 使用此实现，同一时刻只有一个线程可以执行求和。

然而，由于两个 sum 变量实际上是相互独立的，你可以将求和逻辑拆分为两个同步块，如下所示：

```java
public class TwoSums {
    
    private int sum1 = 0;
    private int sum2 = 0;

    private Integer sum1Lock = new Integer(1);
    private Integer sum2Lock = new Integer(2);

    public void add(int val1, int val2){
        synchronized(this.sum1Lock){
            this.sum1 += val1;   
        }
        synchronized(this.sum2Lock){
            this.sum2 += val2;
        }
    }
}
```

现在，两个线程可以同时执行`add()`方法。第一个同步块内的一个线程，第二个同步块内的另一个线程。两个同步块在不同的对象上同步，因此两个不同的线程可以独立执行两个块。这样，线程将更少地等待彼此来执行`add()`方法。

当然，这个例子很简单。在现实生活中共享的资源中，临界区的分解可能要复杂得多，并且需要对执行顺序的可能性进行更多分析。

# 线程安全和共享资源

可以安全地被多个线程同时调用的代码称为线程安全的。如果一段代码是线程安全的，那么肯定不包含 [竞争条件](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html)。竞争条件只有在多个线程更新共享资源时才会出现。因此，了解 java 线程执行过程中共享了什么资源是至关重要的。

## 局部变量

局部变量存储在每个线程自己的栈中。这就意味着局部变量绝对不会在线程之间共享。同时还意味着所有局部基本数据类型的变量都是线程安全的。下面是线程安全的基本数据类型的局部变量的例子：

```java
public void someMethod(){

  long threadSafeInt = 0;

  threadSafeInt++;
}
```

## 局部对象引用

对象的局部引用有点不同。这些引用本身并不是共享的。被引用的对象也不是存储在线程自己的局部栈中。所有的对象都存储在共享堆中。

如果一个被局部创建的对象从来没有从创建它的方法中逃逸，它就是线程安全的。事实上，你也可以将它传递给别的方法或者对象，只要这些目标方法或者对象都没有将该对象开放给其他线程使用。

下面是线程安全的局部对象的示例：

```java
public void someMethod(){

  LocalObject localObject = new LocalObject();

  localObject.callMethod();
  method2(localObject);
}

public void method2(LocalObject localObject){
  localObject.setValue("value");
}
```

例子中的 `LocalObject` 实例不会从方法返回，也不会被传递给任何可以从 `someMethod()` 方法外部访问的其他对象。每个执行  `someMethod()`  方法的线程将创建自己的 `LocalObject` 实例并分配给 `localObject` 引用。因此，这里 `localObject` 的使用是线程安全的。

事实上，整个 `someMethod()` 方法都是线程安全的。即使 `LocalObject` 实例被作为参数传递给同一个类或者别的类中其他方法，对它的使用也都是线程安全的。

唯一的例外，如果使用  `LocalObject` 作为参数调用一个方法，以允许从其他线程中访问的方式存储  `LocalObject`  实例。

## 对象成员变量

对象成员变量(域)和对象一起存储在堆中。因此，如果两个线程调用同一个对象实例上的一个方法，该方法会修改对象成员变量，该方法就不是线程安全的。下面是此类方法的例子：

```java
public class NotThreadSafe{
    StringBuilder builder = new StringBuilder();

    public add(String text){
        this.builder.append(text);
    }
}
```

如果两个线程同时调用同一个非线程安全的实例上的 `add()` 方法，将导致竞争条件。比如：

```java
NotThreadSafe sharedInstance = new NotThreadSafe();

new Thread(new MyRunnable(sharedInstance)).start();
new Thread(new MyRunnable(sharedInstance)).start();

public class MyRunnable implements Runnable{
  NotThreadSafe instance = null;

  public MyRunnable(NotThreadSafe instance){
    this.instance = instance;
  }

  public void run(){
    this.instance.add("some text");
  }
}
```

注意，两个 `MyRunnable` 实例如何共享同一个 `NotThreadSafe` 实例。因此，当它们同时调用  `NotThreadSafe`  实例上的 `add()` 方法时，将会导致竞争条件。

然而，如果两个线程同时调用不同实例上的 `add()` 方法时，当然就不会导致竞争条件。下面是这个版本的例子：

```java
new Thread(new MyRunnable(new NotThreadSafe())).start();
new Thread(new MyRunnable(new NotThreadSafe())).start();
```

现在，两个线程都有自己的 `NotThreadSafe` 实例，因而它们调用 `add()` 方法时就不会有任何相互影响。代码不再包含竞争条件。因此，即使是非线程安全的对象，也可以被以不会导致竞争条件的方式使用。

## 线程控制逃逸规则

可以使用线程控制逃逸规则来判断你的代码是否访问了某些线程安全的特定资源：

```
If a resource is created, used and disposed within
the control of the same thread,
and never escapes the control of this thread,
the use of that resource is thread safe.
```

资源可以是任何共享资源，比如对象、数组、文件数据库连接或者网络套接字等等。在 Java 中你并不会显式销毁对象，因此，这里的"销毁"意味着对象的引用丢失或者置空。

即使对象的使用是线程安全的，如果对象指向共享资源，比如文件或者数据库，你的应用作为一个整体可能仍然是非线程安全的。比如，如果线程 1 和线程 2 分别创建它们自己的数据库连接，连接 1 和连接 2 ，每个连接本身的使用是线程安全的。但是对这些连接指向的数据库的使用就未必是线程安全的。比如，如果两个线程都执行入戏逻辑：

```
check if record X exists
if not, insert record X
```

如果两个线程同时执行，同时它们检查的记录 X 恰好又是同一条数据，这就有两个线程都插入成功的风险。过程如下：

```
Thread 1 checks if record X exists. Result = no
Thread 2 checks if record X exists. Result = no
Thread 1 inserts record X
Thread 2 inserts record X
```

在文件或其他共享资源上运行的线程也可能发生这种情况。因此，区分由线程控制的对象是资源还是仅引用资源（就像数据库连接一样）是很重要的。

# 线程安全和不可变性

[竞争条件](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html) 只有在多个线程同时访问相同的资源，而其中一个或者多个线程写入该资源时才会发生。如果多个线程都只是读取资源，则竞争条件就不会发生。

可以确保线程共享的对象永远不会被任何线程修改的办法是使用不可变的共享对象，这样也就可以实现线程安全。如下面例子所示：

```java
public class ImmutableValue{

  private int value = 0;

  public ImmutableValue(int value){
    this.value = value;
  }

  public int getValue(){
    return this.value;
  }
}
```

注意如何在构造函数中传递 `ImmutableValue` 实例的值。还请注意，没有 setter 方法。一旦创建了 `ImmutableValue` 实例，您将无法更改其值，这是一成不变的。但是，您可以使用 `getValue()` 方法读取它。

如果您需要在 `ImmutableValue` 实例上执行操作，可以通过返回一个新实例并返回该操作产生的值来执行此操作。这是增加操作的示例：

```java
public class ImmutableValue{

  private int value = 0;

  public ImmutableValue(int value){
    this.value = value;
  }

  public int getValue(){
    return this.value;
  }

  
      public ImmutableValue add(int valueToAdd){
      return new ImmutableValue(this.value + valueToAdd);
      }
  
}
```

注意 `add()` 方法返回一个新的 `ImmutableValue` 实例，携带加法操作的结果，而不是将原来的值加上参数值。

## 引用不是线程安全的！

记住这一点非常重要：即使对象是不可变的，因而是线程安全的，指向该对象的引用却可能是非线程安全的。考虑下面的例子：

```java
public class Calculator{
  private ImmutableValue currentValue = null;

  public ImmutableValue getValue(){
    return currentValue;
  }

  public void setValue(ImmutableValue newValue){
    this.currentValue = newValue;
  }

  public void add(int newValue){
    this.currentValue = this.currentValue.add(newValue);
  }
}
```

`Calculator` 类包含对 `ImmutableValue` 实例的引用。注意，如何通过 `setValue()` 和 `add()` 方法都可以更改该引用。因此，即使 `Calculator` 类在内部使用不可变对象，它本身也不是不可变的，因此不是线程安全的。换句话说：`ImmutableValue` 类是线程安全的，但**使用**不是。尝试通过不变性实现线程安全时，请牢记这一点。

为了使 `Calculator` 类线程安全，您可以声明 `getValue()`，`setValue()` 和 `add()` 方法为 `synchronized`。这样就可以了。

# Java 内存模型

Java 内存模型指定了 Java 虚拟机如何使用计算机的内存(RAM)。Java 虚拟机可以看作是整个计算机的模型，因而自然包含一个内存模型——也就是所谓的 Java 内存模型。

如果想要设计具有精确行为的并发程序，理解 Java 内存模型是非常重要的。Java 内存模型指定了不同的线程在何时以何种方法可以看到由其他线程写入共享变量的值，以及在必要时如何同步访问共享变量。

最初的 Java 内存模型性能不好，因而在 Java 1.5 中进行了改进。改进后的 Java 内存模型在 Java 1.8 中仍然使用。

## 内部 Java 内存模型

JVM 内部使用的 Java 内存模型将内存划分为线程栈和堆。下图展示了 Java 内存模型的逻辑表达形式：

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-1.png)

Java 虚拟机中运行的每个线程都拥有自己的线程栈。线程栈包含线程已经调用的方法直到当前执行到的代码位置的信息。我将这种信息称为"调用栈"。随着线程执行代码，调用栈不断变化。

线程栈还包含正在执行的每个方法（调用栈上的所有方法）的所有局部变量。线程只能访问自己的线程栈。由线程创建的局部变量对除了创建它的线程之外的所有线程都是不可见的。即使两个线程正在执行完全相同的代码，两个线程仍然会在各自的线程栈中创建代码中的局部变量。因此，每个线程都拥有每个局部变量的自身版本。

所有的基本数据类型 ( `boolean`, `byte`, `short`, `char`, `int`, `long`, `float`, `double`) 的局部变量都完全存储在线程栈上，因而对其他线程不可见。线程可以将一个基本数据类型的变量传递给另一个线程，但是并不能共享自己的基本数据类型的局部变量。

堆包含你的 Java 应用中创建的所有对象，不关心创建对象的线程。包括基本数据类型的对象版本 (比如， `Byte`, `Integer`, `Long` 等等)。对象被创建并分配给局部变量，或者作为另一个对象的成员变量被创建，都没关系，这些对象都存储在堆中。

下图展示了存储在线程栈中的调用栈和局部变量，以及存储在堆中的对象：

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-2.png)

局部变量也可能是基本数据类型，这种情况下完全存储在线程栈中。

局部变量也可以是对象的引用。这种情况下该引用(局部变量)存储在线程栈上，但是对象本身存储在堆上。

一个对象可能包含方法，而这些方法可能包含局部变量。即使这些方法所属的对象存储在堆中，这些局部变量也存储在线程栈中。

对象的成员变量与对象本身一起存储在堆中。当成员变量是原始类型时，以及它是对对象的引用时，都是如此。静态类变量也与类定义一起存储在堆中。

引用对象的所有线程都可以访问堆上的对象。当线程可以访问对象时，它也可以访问该对象的成员变量。如果两个线程同时在同一个对象上调用方法，则它们都将有权访问该对象的成员变量，但是每个线程将拥有自己的局部变量副本。

下图展示了上述要点：

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-3.png)

两个线程具有一组局部变量。局部变量之一（`Local Variable 2`）指向堆上的共享对象（对象3）。这两个线程分别具有对同一对象的不同引用。它们的引用是局部变量，因此存储在每个线程的线程栈中（在每个线程上）。但是，两个不同的引用指向堆上的同一对象。

请注意，共享对象（对象3）如何引用对象2和对象4作为成员变量（如从对象3到对象2和对象4的箭头所示）。通过对象3中的这些成员变量引用，两个线程可以访问对象2和对象4。

该图还显示了一个局部变量，该局部变量指向堆上的两个不同对象。在这种情况下，引用指向两个不同的对象（对象1和对象5），而不是同一对象。理论上，如果两个线程都引用了两个对象，则两个线程都可以访问对象1和对象5。但是在上图中，每个线程仅具有对两个对象之一的引用。

那么，什么样的 Java 代码能够产生上面的内存分布图？如下的代码即可：

```java
public class MyRunnable implements Runnable() {

    public void run() {
        methodOne();
    }

    public void methodOne() {
        int localVariable1 = 45;

        MySharedObject localVariable2 =
            MySharedObject.sharedInstance;

        //... do more with local variables.

        methodTwo();
    }

    public void methodTwo() {
        Integer localVariable1 = new Integer(99);

        //... do more with local variable.
    }
}
public class MySharedObject {

    //static variable pointing to instance of MySharedObject

    public static final MySharedObject sharedInstance =
        new MySharedObject();


    //member variables pointing to two objects on the heap

    public Integer object2 = new Integer(22);
    public Integer object4 = new Integer(44);

    public long member1 = 12345;
    public long member1 = 67890;
}
```

如果两个线程都正在执行 `run()` 方法，则前面的图将会产生。`run()` 方法调用 `methodOne()` ，而 `methodOne()` 调用 `methodTwo()`。

`methodOne()` 声明一个基本数据类型的局部变量 ( `int` 类型的`localVariable1` ) 和一个对象引用类型的局部变量 (`localVariable2`)。

每个执行 `methodOne()` 的线程都将在各自的线程栈上创建自己的 `localVariable1` 和 `localVariable2` 的副本。 `localVariable1` 变量将是彻底相互独立的，各自存活在自己的线程栈中。一个线程无法看到别的线程对它自己的 `localVariable1` 的副本所作的修改。

每个执行 `methodOne()` 的线程也会创建自己的 `localVariable2` 副本。但是，`localVariable2` 的两个不同副本最终都指向堆上的同一对象。该代码将 `localVariable2` 设置为指向静态变量引用的对象。静态变量只有一个副本，并且此副本存储在堆中。因此，`localVariable2` 的两个副本最终都指向静态变量指向的 `MySharedObject` 的同一实例。`MySharedObject` 实例也存储在堆中。它对应于上图中的对象3。

注意 `MySharedObject` 类也包含两个成员变量。成员变量本身与对象一起存储在堆中。这两个成员变量指向另外两个 `Integer` 对象。这些 `Integer` 对象对应于上图中的对象2和对象4。

还要注意 `methodTwo()` 如何创建一个名为 `localVariable1` 的局部变量。该局部变量是对 `Integer` 对象的对象引用。 该方法将 `localVariable1` 引用设置为指向新的 `Integer` 实例。执行 `methodTwo()` 的每个线程的 `localVariable1` 引用将存储在一个副本中。实例化的两个 `Integer` 对象将存储在堆中，但是由于该方法每次执行时都会创建一个新的 `Integer` 对象，因此执行此方法的两个线程将创建单独的 `Integer` 实例。在 `methodTwo()` 内部创建的 `Integer` 对象对应于上图中的对象1和对象5。

还要注意类型为 `long` 的 `MySharedObject` 类中的两个成员变量，这是原始类型。由于这些变量是成员变量，因此它们仍与对象一起存储在堆中。仅局部变量存储在线程堆栈上。

## 硬件内存架构

现代硬件内存体系结构与内部 Java 内存模型有所不同。同样重要的是，还要了解硬件内存架构，并了解 Java 内存模型如何与之协同工作。本节描述了常见的硬件内存体系结构，下一节将描述 Java 内存模型如何与之协同工作。

下面是最简化的现代计算机硬件架构示意图：

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-4.png)

现代计算机通常其中装有2个或更多CPU。其中一些CPU也可能具有多个内核。关键是，在具有2个或更多CPU的现代计算机上，可能同时运行多个线程。每个CPU都可以在任何给定时间运行一个线程。这意味着，如果Java应用程序是多线程的，则每个CPU可能在Java应用程序中同时（并发）运行一个线程。

每个CPU包含一组寄存器，这些寄存器本质上是CPU内存。 CPU在这些寄存器上执行操作的速度比对主存储器中的变量执行操作的速度快得多。这是因为CPU可以比访问主存储器更快地访问这些寄存器。

每个CPU可能还具有一个CPU高速缓存存储层。实际上，大多数现代CPU都具有一定大小的缓存层。 CPU可以比其主存储器更快地访问其高速缓存，但是通常不如它可以访问其内部寄存器的速度快。因此，CPU高速缓存内存介于内部寄存器和主内存的速度之间。某些CPU可能具有多个高速缓存层（第1级和第2级），但是了解Java内存模型如何与内存交互并不重要。重要的是要知道CPU可以具有某种高速缓存层。

计算机还包含一个主存储区（RAM）。所有CPU都可以访问主存储器。主存储区通常比CPU的缓存大得多。

通常，当CPU需要访问主存储器时，它将部分主存储器读入其CPU缓存中。它甚至可以将缓存的一部分读入其内部寄存器，然后对其执行操作。当CPU需要将结果写回主存储器时，它将把值从其内部寄存器刷新到高速缓存，并在某个时候将值刷新回主存储器。

当CPU需要将其他内容存储在高速缓存中时，通常会将高速缓存中存储的值刷新回主存储器。 CPU高速缓存可以一次将数据写入其部分内存，并一次刷新其部分内存。它不必每次更新都读取/写入完整的缓存。通常，缓存在称为“缓存行”的较小存储块中更新。可以将一个或多个高速缓存行读入高速缓存存储器，并且可以将一个或多个高速缓存行再次刷新回主存储器。

## 在 Java 内存模型和硬件内存架构之间架起桥梁

如前所述，Java 内存模型和硬件内存架构是不同的。硬件内存架构并不区分线程栈和堆。从硬件层面看，线程栈和堆都在主内存中。部分线程栈和堆有时候可以出现在 CPU 缓存或者 CPU 寄存器中。下图展示了这种分布情况：

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-5.png)

当对象和变量可以被存储在各种不同的计算机存储区域中时，可能会发生某些问题。主要的两类问题：

-线程对共享变量的修改（写入）的可见性。
-在读取，校验以及写入共享变量时的竞争条件。

接下来分别解释这两类问题。

### 共享对象的可见性

如果两个线程正在共享一个对象，如果没有正确使用 `volatile` 声明或者同步，那么一个线程对共享对象的修改将可能不会被另一个线程看到。

设想共享对象最初存储在主内存中。一个运行在 CPU 上的线程将该共享对象读取到它的 CPU 缓存中。然后对该对象进行了修改。由于 CPU 此时并没有将缓存中的对象写回主内存，所以共享对象的修改之后的版本对运行在其他 CPU 上的线程是不可见的。这样每个线程都各自拥有自己的共享对象副本，每个副本存储在不同的 CPU 缓存中。

下图描述了上述情形。运行在左侧 CPU 上的线程将共享对象拷贝到它的 CPU 缓存中，然后修改其 `count` 变量为2。这个修改对运行在右侧 CPU 上的线程是不可见的，因为对 `count` 的修改尚未被会写到主内存。

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-6.png)

解决此类问题的办法是使用 [Java 的 volatile 关键字](http://tutorials.jenkov.com/java-concurrency/volatile.html)。 `volatile` 关键字能够确保给定的变量直接从主内存中读取，当修改时始终会直接写回主内存。

### 竞争条件

如果两个或者多个线程共享一个对象，其中若干线程修改该共享对象的变量，就可能会发生 [竞争条件](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html) 。

设想这样的情形，如果线程 A 将共享对象中的变量 `count` 读取到它的 CPU 缓存中。运行在另一个 CPU 上的线程 B 也将该变量读取到自己所在 CPU 的缓存中。现在线程 A 对 `count` 加1，线程 B 也对 `count` 加1。现在 `count` 已经被增加过两次，每个 CPU 缓存一次。

如果这两次增加操作顺序发生，变量 `count` 将会增加两次，初始值增加2并写回主内存。

然而，两次增加并发发生，而没有正确地同步。无论哪个线程将它修改过的 `count` 版本写回主内存，最终的结果只会比初始值增加1，两次增加操作无效。

下图展示了上述发生竞争条件的情形：

![](http://tutorials.jenkov.com/images/java-concurrency/java-memory-model-7.png)

解决此类问题的办法是使用 [Java synchronized 块](http://tutorials.jenkov.com/java-concurrency/synchronized.html)。同步块保证在任何给定时间点只有一个线程可以进入给定的代码临界区。同步块同时保证所有在同步块内部访问的变量都将直接从主内存读取。同时，当线程退出同步块时，所有被修改过的变量都会立即被写回主内存，无论变量有没有声明为 `volatile` 。

# Java 同步块

Java 同步块将一个方法或者代码块标记为同步的。Java 同步块同一时刻只能被一个线程执行(取决于你如何使用)。因此，Java 同步块可以被用于避免 [竞争条件](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html)。本文详细介绍了 Java *synchronized* 关键字的工作原理。

## Java 并发工具类

 `synchronized` 机制是 Java 用于多线程同步访问共享对象的第一种机制。 `synchronized` 机制目前看来并不是非常好用。因此 Java 5 添加了整套的 [concurrency utility classes](http://tutorials.jenkov.com/java-util-concurrent/index.html) 来帮助开发者实现相较与 `synchronized` 更精细的并发控制。

## Java synchronized 关键字

Java 同步块使用 `synchronized` 关键字标记。Java 同步块被同步在某些对象上。所有同步在相同对象上的所有同步块在同一时刻只允许一个线程在它们内部执行。所有其他试图进入同步块的线程都会被阻塞，直到同步块内的线程退出同步块。

 `synchronized` 可以用来标记四种不同类型的代码块：

1.实例方法
2.静态方法
3.实例方法内部的代码块
4.静态方法内部的代码块

这些代码块被同步在不同对象上。你需要何种同步块需要具体情况具体分析。接下来我们详细介绍每种类型的同步块。

## 同步实例方法

这是一个同步的实例方法：

```java
public class MyCounter {

  private int count = 0;

  public synchronized void add(int value){
      this.count += value;
  }
}
```

注意 `synchronized` 关键字使用在 `add()` 方法声明中。这就告诉 Java 该方法是同步的。

Java 中的同步实例方法被同步在拥有该方法的实例(对象)上。因此，每个实例拥有的同步方法都同步在不同的对象上：拥有该方法的实例。

每个实例上只有一个线程能够在一个同步实例方法内部执行。如果存在多个实例，则同一时刻一个线程只能在每个实例的一个同步实例方法内部执行。每个实例一个线程。

这一点对于同一个对象(实例)中的所有同步实例方法也是使用的。因此，下面例子中，只有一个线程能够在两个同步方法之一内部执行。一个实例只有一个线程：

```java
public class MyCounter {

  private int count = 0;

  public synchronized void add(int value){
      this.count += value;
  }
  public synchronized void subtract(int value){
      this.count -= value;
  }

}
```

## 同步静态方法

类似于实例方法，静态方法也可以使用 `synchronized` 关键字标记为同步的。下面是 Java 同步静态方法的例子：

```java
public static MyStaticCounter{

  private static int count = 0;

  public static synchronized void add(int value){
      count += value;
  }

}
```

这里的 `synchronized` 关键字也是告诉 Java  `add()` 方法是同步的。

同步静态方法是同步在静态方法所在的类的类对象上。由于每个类只会有唯一一个类对象存在于 JVM 中，只会有一个线程能够在同一个类的一个同步静态方法中执行。

如果一个类包含多个同步静态方法，同一时刻只能有一个线程执行这些方法中任何一个。请看下面的例子：

```java
public static MyStaticCounter{

  private static int count = 0;

  public static synchronized void add(int value){
    count += value;
  }

  public static synchronized void subtract(int value){
    count -= value;
  }
}
```

在任何给定时间点只有一个线程可以在 `add()` 和 `subtract()` 其中之一内部执行。如果线程 A 正在执行 `add()`，则线程 B 既不能执行 `add()` 也不能执行 `subtract()` ，直到线程 A 退出 `add()`。

如果静态同步方法位于不同类中，则一个线程可以在每个类的静态同步方法内部执行。每个类一个线程，无论它调用的是哪个静态同步方法。

## 实例方法中的同步块

你并不是必须同步整个方法，有时候仅仅同步方法的一部分逻辑更加合理。Java 的方法内部同步块允许你做到这一点。

下面是一个非同步 Java 方法内部的同步代码块的示例：

```java
  public void add(int value){

    synchronized(this){
       this.count += value;   
    }
  }
```

这个例子使用 Java 同步块结构来将一个代码块标记为同步的。该代码块将类似于同步方法那样被执行。

注意，Java 同步块结构如何选择同步使用的对象。上面例子中使用了 `this` ，也就是 `add` 方法在其上被调用的那个实例。被同步结构选取放在括号中的对象被称为监视器对象。代码块被称为被同步在监视器对象上。一个同步实例方法使用它所属的对象作为监视器对象。

只有一个线程可以在同步于同一个监视器对象的 Java 同步代码块内部运行。

下面两个例子都是同步在它们被调用于其上的实例上。它们在同步方面是等效的：

```java
  public class MyClass {
  
    public synchronized void log1(String msg1, String msg2){
       log.writeln(msg1);
       log.writeln(msg2);
    }

  
    public void log2(String msg1, String msg2){
       synchronized(this){
          log.writeln(msg1);
          log.writeln(msg2);
       }
    }
  }
```

因此，只有一个线程能够执行在例子中的两个同步块之一内部。

如果第二个同步块被同步在一个不同于 `this` 的对象上，则一个线程就可以在同一时刻执行在每个方法内部。

## 静态方法中的同步块

同步块也可以被用在静态方法内部。这里是与前面静态方法示例相同的例子。这些方法都同步在它们所属的类的类对象上：

```java
  public class MyClass {

    public static synchronized void log1(String msg1, String msg2){
       log.writeln(msg1);
       log.writeln(msg2);
    }

  
    public static void log2(String msg1, String msg2){
       synchronized(MyClass.class){
          log.writeln(msg1);
          log.writeln(msg2);  
       }
    }
  }
```

同一时刻只有一个线程能够执行在这两个方法之一内部。

如果第二个同步块被同步在 `MyClass.class` 之外的对象上，则同一时刻一个线程可以执行在每个方法内部。

## Lambda 表达式中的同步块

在 [Java Lambda Expression](http://tutorials.jenkov.com/java/lambda-expressions.html) 和匿名类内部使用同步块也是可能的。

这是一个内部包含同步块的 Java lambda 表达式。注意，该同步块同步在包含该 lambda 表达式的类的类对象上。如果有必要，它也可以同步在其他对象上。不过使用类对象很适合这个例子：

```java
import java.util.function.Consumer;

public class SynchronizedExample {

  public static void main(String[] args) {

    Consumer<String> func = (String param) -> {

      synchronized(SynchronizedExample.class) {

        System.out.println(
            Thread.currentThread().getName() +
                    " step 1: " + param);

        try {
          Thread.sleep( (long) (Math.random() * 1000));
        } catch (InterruptedException e) {
          e.printStackTrace();
        }

        System.out.println(
            Thread.currentThread().getName() +
                    " step 2: " + param);
      }

    };


    Thread thread1 = new Thread(() -> {
        func.accept("Parameter");
    }, "Thread 1");

    Thread thread2 = new Thread(() -> {
        func.accept("Parameter");
    }, "Thread 2");

    thread1.start();
    thread2.start();
  }
}
```

## Java 同步示例

这个例子启动两个线程，它们都会调用同一个计数器实例上的 `add` 方法。此时只有一个线程能够调用同一个实例上的 `add` 方法，因为该方法被同步在它所属的实例上。

```java
  public class Example {

    public static void main(String[] args){
      Counter counter = new Counter();
      Thread  threadA = new CounterThread(counter);
      Thread  threadB = new CounterThread(counter);

      threadA.start();
      threadB.start();
    }
  }
```

下面是例子中用到的类， `Counter` 和 `CounterThread`。

```java
  public class Counter{
     
     long count = 0;
    
     public synchronized void add(long value){
       this.count += value;
     }
  }
  public class CounterThread extends Thread{

     protected Counter counter = null;

     public CounterThread(Counter counter){
        this.counter = counter;
     }

     public void run() {
	for(int i=0; i<10; i++){
           counter.add(i);
        }
     }
  }
```

两个线程被创建。同一个 `Counter` 实例通过构造器被传递给它们。`Counter.add()` 方法被同步到该实例上，因为 `add` 方法是实例方法，而且被标记为同步的。由于此时只有一个线程可以调用 `add()` 方法。另外一个线程将等待直到第一个线程退出 `add()` 方法，然后才能执行该方法。

如果两个线程引用了各自独立的 `Counter` 实例，它们同时调用 `add()` 方法就没有任何问题。调用将会指向不同的对象，因此方法调用也可以在不同的对象（拥有该方法的对象）上同步。方法的调用不会被阻塞。大概是下面这样：

```java
public class Example {

  public static void main(String[] args){
    Counter counterA = new Counter();
    Counter counterB = new Counter();
    Thread  threadA = new CounterThread(counterA);
    Thread  threadB = new CounterThread(counterB);

    threadA.start();
    threadB.start();
  }
}
```

注意，两个线程，线程 A 和线程 B，不再引用相同的 `Counter` 实例。`counterA` 和 `counterB` 上的 `add()` 方法在各自的对象实例上同步。调用 `counterA` 上的 `add()` 当然不会阻塞对 `counterB` 上的 `add()` 的调用。

## 同步和数据可见性

除了使用 `synchronized` 关键字(或者 [Java volatile](http://tutorials.jenkov.com/java-concurrency/volatile.html) 关键字)，无法保证当一个线程修改与其他线程共享的变量的值时，其他的线程能够看到这个修改的值。对于由线程读取到 CPU 寄存器中的变量何时会被"提交"到主内存中，没有任何保证。同样，别的线程何时根据主内存对自己的 CPU 寄存器中的变量进行"刷新"，也没有任何保证。

`synchronized` 关键字改变了这一切。当一个线程进入同步块，它将刷行所有它可见的变量的值。当一个线程退出同步块时，该线程可见的所有变量的变化都会被提交到主内存。类似于 [volatile keyword](http://tutorials.jenkov.com/java-concurrency/volatile.html) 的行为。

## 同步和指令重排序

Java 编译器和 Java 虚拟机被允许对你的代码进行指令重排序以使得它们执行更快，通常是通过允许重排序之后的指令被 CPU 并行执行。

对那些同时被多个线程执行的代码进行指令重排序可能会导致问题。比如，如果一个发生在同步块内部的变量写入被重排序到了同步块之外。

为了解决这种问题，Java `synchronized` 关键字对同步块之前、内部以及之后的指令重排序设置了一些限制。类似于 [volatile 关键字](http://tutorials.jenkov.com/java-concurrency/volatile.html) 设置的限制。

最终结果是，您可以确保您的代码正确运行——不会发生指令重新排序，最终导致该代码的行为不同于您编写的代码所期望的行为。

## 在什么对象上同步

如前所述，同步块必须同步在某些对象上。你可以选择几乎任何对象以同步于其上，但是建议不要在 `String` 对象上同步，或者任何其他基本数据类型的包装对象。因为编译器可能对此进行优化，导致代码中你以为使用的是不同的实例的地方，可能实际上使用的是相同的实例。分析下面的例子：

```java
synchronized("Hey") {
   //do something in here.
}
```

如果你有多个同步块都同步在字面值"Hey"上，编译器可能在背后实际上使用同一个 `String` 对象。结果是，这些同步块就同步在同一个对象上。这可能不是你期望的行为。

使用基本数据类型包装对象时的情况类似。如下面的例子：

```java
synchronized(Integer.valueOf(1)) {
   //do something in here.
}
```

如果你调用 `Integer.valueOf(1)` 很多次，它可能实际上为相同的输入参数值返回同一个包装对象实例。这就意味着，如果你将多个同步块同步在相同的基本数据类型包装对象上，你可能就会面临所有同步块都同步在同一个对象上的风险。这也不是你期望的行为。

为了确保安全，在 `this` 上同步——或者在 `new Object()` 上同步。使用那些不会被编译器、JVM 或者 Java 类库内部缓存或者复用的对象。

## 同步块的局限性和替代方案

Java 中的同步块具有一些局限性。比如，一个同步块同一时刻只允许一个线程进入。然而，如果两个线程都只是想要读取共享值，而并不会修改它呢？允许同时读取可能是安全的。作为同步块的替代方案，你可以使用一种名为 [Read / Write Lock](http://tutorials.jenkov.com/java-concurrency/read-write-locks.html) 的技术来保护你的代码，这是一种比同步块更加先进的锁语义。Java 实际上已经内置了一个你可以直接使用的 [ReadWriteLock](http://tutorials.jenkov.com/java-util-concurrent/readwritelock.html) 类。

如果你希望若干个线程进入同步块，而不仅仅是一个，该怎么办？你可以使用 [Semaphore](http://tutorials.jenkov.com/java-concurrency/semaphore.html) 实现这种行为。Java 内置了你可以直接使用的 [Java Semaphore](http://tutorials.jenkov.com/java-util-concurrent/semaphore.html) 类。

同步块并不能保证等待进入同步块的线程最终会以何种顺序进入同步块。如果你想要保证这些等待线程能够按照它们最初请求进入同步块的顺序依次进入同步块，该怎么办？你需要实现自己的 [Fairness](http://tutorials.jenkov.com/java-concurrency/starvation-and-fairness.html) 。

如果你希望一个线程写入共享变量的同时，别的线程还可以同时读取该变量，该如何做？可能你只需要使用 [volatile variable](http://tutorials.jenkov.com/java-concurrency/volatile.html) 而不需要任何同步逻辑。

## 同步块的性能损耗

与进入和退出 Java 中的同步块相关的性能开销很小。随着 Jave 的发展，性能开销下降了，但是仍然要付出很小的代价。

如果您在一个紧密的循环内多次进入和退出同步块，则通常要担心进入和退出同步块的性能开销。

另外，请尽量不要使同步块大于必需的块。换句话说，仅同步真正需要同步的操作——避免阻止其他线程执行不必同步的操作。同步块中只有绝对必要的指令。应该尽可能增加代码的并行性。

## 同步块的可重入

一旦线程已经进入同步块，则称该线程"持有了同步块同步于其上的监视器对象的锁"。如果该线程调用另外的方法，后者又反向调用同步块内部的前者方法，则持有锁的线程可以再次进入该同步块。它不会被阻塞，因为该线程本身正持有锁。除非别的线程持有了锁。分析下面的例子：

```java
public class MyClass {
    
  List<String> elements = new ArrayList<String>();
    
  public void count() {
    if(elements.size() == 0) {
        return 0;
    }
    synchronized(this) {
       elements.remove();
       return 1 + count();  
    }
  }
    
}
```

不必在意上述计算列表元素的方法根本没有任何意义。只需关注 `count()` 方法内的同步块内部如何递归调用 `count()` 方法即可。因此，线程调用 `count()` 最终可能会多次进入同一同步块。这是允许的。

注意：如果你不谨慎设计你的代码，允许一个线程进入多个同步块可能会导致 [嵌套监视器锁定](http://tutorials.jenkov.com/java-concurrency/nested-monitor-lockout.html)。

## 集群设置中的同步块

请记住，同步块仅阻止同一 Java VM 中的线程进入该代码块。如果在集群中的多个 Java VM 上运行相同的 Java 应用程序，则每个 Java VM 中的一个线程可能同时进入该同步块。

如果需要跨集群中所有 Java VM 进行同步，则将需要使用其他同步机制，而不仅仅是同步块。

# Java Volatile 关键字

Java `volatile` 关键字用于将 Java 变量标记为"被存储在主内存中"。更精确的含义，每次都从计算机的主内存中读取 `volatile` 变量，而不是从 CPU 缓存中。同时，每次对 `volatile` 变量的写入都会直接写入主内存，而不仅仅写入 CPU 缓存。

实际上，Java 5 以来，`volatile` 关键字不仅仅提供了从主内存读写 `volatile` 变量的保证，接下来将详细介绍其他功能。

## 变量可见性问题

Java `volatile` 关键字保证对共享变量的修改在线程之间的可见性。听起来可能有点抽象，让我们来解释一下。

早多线程应用中，多个线程操作非 `volatile` 变量，为了提高性能，每个线程都会从主内存将变量拷贝到自己的 CPU 缓存中。如果你的计算机有多个 CPU，每个线程可能都运行在不同的 CPU 上。这就意味着，每个线程都会将变量拷贝到各自不同的 CPU 缓存中。如下图所示：

![](http://tutorials.jenkov.com/images/java-concurrency/java-volatile-1.png)

使用非 `volatile` 变量，无法保证 JVM 何时会从主内存读取数据到 CPU 缓存中，何时将 CPU 缓存中的数据写回主内存。下面我将介绍这种情况可能导致的若干问题。

设想这种情况，两个或者更多线程需要访问一个包含计数器变量的共享对象，声明如下：

```java
public class SharedObject {

    public int counter = 0;

}
```

同时假想，只有线程 1 增加 `counter` 变量，不过线程 1 和线程 2 可能不时读取 `counter` 变量。

如果 `counter` 变量没有声明为 `volatile` ，就无法保证该变量的值会被从 CPU 缓存写回主内存。这就意味着，CPU 缓存中的 `counter` 变量的值可能与主内存中的不同。如下所示：

![](http://tutorials.jenkov.com/images/java-concurrency/java-volatile-2.png)

这种由于其他线程没有将变量的缓存写回主内存而导致的线程无法看到变量的最新值的问题，被称为"可见性"问题。一个线程的更新结果对别的线程不可见。

## Java volatile 可见性保证

Java `volatile` 关键字尝试解决可见性问题。通过声明 `counter` 变量为 `volatile` ，所有 `counter` 变量的写入都会被立即写回主内存。同时，所有 `counter` 变量的读取都会直接来自主内存。

声明 `volatile` 变量 `counter` 如下：

```java
public class SharedObject {

    public volatile int counter = 0;

}
```

声明变量为 `volatile` 提供了该变量的写入对其他线程的可见性保证。

上面给出的场景中，一个线程(T1)修改 `counter` ，另一个线程(T2)读取 `counter` 而不修改它，声明 `counter` 为 `volatile` 足以保证 T2 对 `counter` 变量写入的可见性。

但是，如果 T1 和 T2 都在增加 `counter` 变量，那么声明 `counter` 变量 `volatile` 将是不够的。接下来解释。

### 完整 volatile 可见性保证

实际上，Java `volatile` 的可见性保证不仅局限于 `volatile` 变量本身。完整的可见性保证如下：

-如果线程 A 写入一个 `volatile` 变量，然后线程 B 随后读取相同的 `volatile` 变量，那么在写入 `volatile` 变量之前，线程 A 可见的所有变量，在线程 B 读取 `volatile` 变量之后也将对其可见。
-如果线程 A 读取了 `volatile` 变量，那么读取 `volatile` 变量时线程 A 可见的所有所有变量也将从主内存中重新读取。

代码示例：

```java
public class MyClass {
    private int years;
    private int months
    private volatile int days;


    public void update(int years, int months, int days){
        this.years  = years;
        this.months = months;
        this.days   = days;
    }
}
```

`udpate()` 方法写入三个变量，其中只有 `days` 是 `volatile` 的。

完整的 `volatile` 可见性保证的含义是，当一个值被写入 `days`，所有对线程可见的变量也都会被写入主内存。也就是说，当一个值被写入 `days`， `years` 和 `months` 的值也会同时被写入主内存。

当读取 `years`， `months` 和 `days` 时，可以这样做：

```java
public class MyClass {
    private int years;
    private int months
    private volatile int days;

    public int totalDays() {
        int total = this.days;
        total += months * 30;
        total += years * 365;
        return total;
    }

    public void update(int years, int months, int days){
        this.years  = years;
        this.months = months;
        this.days   = days;
    }
}
```

注意，`totalDays()` 方法是通过将 `days` 的值读入 `total` 变量开始的。当读取 `days` 的值时， `months` 和 `years` 的值也被从主存储器读入。因此，可以保证按照上述读取顺序看到 `days`，`months` 和 `years` 的最新值。

## 指令重排序挑战

为了提高程序性能，JVM 和 CPU 可以对指令进行重排序，同时保持指令的语义不变。比如，下面的指令：

```java
int a = 1;
int b = 2;

a++;
b++;
```

这些指令可以被如下重新排序，而不会丢失程序的语义：

```java
int a = 1;
a++;

int b = 2;
b++;
```

不过，当存在 `volatile` 变量时，指令重排序就会带来一些挑战。让我们来重新审视前面使用过的 `MyClass` 例子：

```java
public class MyClass {
    private int years;
    private int months
    private volatile int days;


    public void update(int years, int months, int days){
        this.years  = years;
        this.months = months;
        this.days   = days;
    }
}
```

一旦 `update()` 方法将一个值写入 `days`，新的写入 `years` 和 `months` 的值也会被同时写入主内存。但是，当 JVM 对指令进行进行重排序之后：

```java
public void update(int years, int months, int days){
    this.days   = days;
    this.months = months;
    this.years  = years;
}
```

`months`  和 `years` 的值在 `days` 变量值变化的时候仍然会被写入主内存，但是此时写入动作发生在对 `months` 和 `years` 赋新值之前。因此，新的值就没有正确地对其他线程可见。也就是重排序之后的指令语义发生了变化。

Java 对此问题有一套解决方案，接下来介绍。

## Java volatile Happens-Before 保证

为了应对指令重排序挑战，Java `volatile` 关键字在可见性保证基础上，又提供了 "happens-before" 保证。该保证含义如下：

-对其他变量的读取和写入不能被重排序为发生在写入 `volatile` 变量之后，如果该读取和写入本来发生在写入 `volatile` 之前。`volatile` 变量写入操作之前的读写操作保证会发生在 `volatile` 变量写入之前。注意，本来发生在 `volatile` 变量写入操作之后的对其他变量的读取操作还是有可能会被重排序到发生在 `volatile` 变量写入操作之前。而非相反。也就是说，经过指令重排序，后面的移动到前面允许，前面移动到后面不允许。

-对其他变量的读取和写入不能被重排序为发生在读取 `volatile` 变量之前，如果该读取和写入本来发生在读取 `volatile` 之后。注意，本来发生在 `volatile` 变量读取操作之前的对其他变量的读取操作还是有可能会被重排序到发生在 `volatile` 变量读取操作之后。而非相反。也就是说，经过指令重排序，前面的移动到后面允许，后面的移动到前面不允许。

上述 "happens-before" 保证假定 `volatile` 关键字的可见性保证正在发挥作用。

## volatile 并不总是足够

即使 `volatle` 关键字保证直接从主内存读取所有的 `volatile` 变量，所有对 `volatile` 变量的写入都直接写入主内存，仍然存在某些情况，仅仅将变量声明为 `volatile` 是不够的。

在上文中解释的情况下，只有一个线程 1 对共享变量 `counter` 进行写入，将该变量声明为 `volatile` 就足以保证线程 2 始终都能看到最新写入的值。

事实上，如果写入变量的新值不依赖于变量的先前值，多个线程甚至能够同时写入共享的 `volatile` 变量，仍然能够保证主内存中存储正确的值。换句话说，如果一个写入共享 `volatile` 变量的线程不需要事先读取该变量的值就能确定它的下一个值就可以。

一旦线程需要事先读取 `volatile` 变量的值，然后基于该值产生该变量的新值，则声明为 `volatile` 变量就不再足够保证正确的可见性。`volatile` 变量读取和新值写入操作之间短暂的时间差，制造出一个 [race condition](http://tutorials.jenkov.com/java-concurrency/race-conditions-and-critical-sections.html) ，其中多个线程可能读取到该 `volatile` 变量的相同的值，产生变量的新值，而在将变量值写回主内存时——覆盖其他线程写入的值。

多个线程同时增加同一个计数器的场景正好就是 `volatile` 变量不足够的例子。下面一节进一步解释这种情况。

设想如果线程 1 读取一个值为 0 的共享 `counter` 变量到它的 CPU 缓存中，对其值加 1 而并没有将修改之后的值写入主内存。线程 2 接下来从主内存读取同一个 `counter` 变量，其值仍为 0 ，到它的 CPU 缓存中。然后线程 2 也对其值加 1 ，也没有将修改后的值写入主内存。如下图所示：

![](http://tutorials.jenkov.com/images/java-concurrency/java-volatile-3.png)

现在，线程 1 和线程 2 实际上不同步。共享的 `counter` 变量的实际值应该为 2 ，但是每个线程在其 CPU 缓存中的变量值为 1 ，而在主内存中该值仍然为 0 。真是一团糟！即使线程最终将共享 `counter` 变量的值写回到主存中，该值也将是错误的。

## volatile 何时足够？

如前所述，如果两个线程都在读取和写入共享变量，那么仅使用 `volatile` 关键字是不够的。在这种情况下，您需要使用 [synchronized](http://tutorials.jenkov.com/java-concurrency/synchronized.html)，以确保变量的读写是原子性的。读取或写入 `volatile` 变量不会阻止线程读取或写入。为此，您必须在临界区周围使用 `synchronized` 关键字。

作为 `synchronized` 块的替代方法，您还可以使用在 [`java.util.concurrent`包](http://tutorials.jenkov.com/java-util-concurrent/index.html) 中找到的许多原子数据类型之一。例如，[`AtomicLong`](http://tutorials.jenkov.com/java-util-concurrent/atomiclong.html) 或 [`AtomicReference`](http://tutorials.jenkov.com/java-util-concurrent/atomicreference.html) 或其他之一。

如果只有一个线程读取和写入 `volatile` 变量的值，而其他线程仅读取该变量，则保证读取线程可以看到写入 `volatile` 变量的最新值。如果不使变量 `volatile` ，则将无法保证。

关键字 `volatile` 可以在 32 位和 64 位变量上工作。

## volatile 性能分析

读取和写入 `volatile` 变量会使该变量被读取或写入主存储器。与访问 CPU 缓存相比，读写主存储器的开销更大。访问 `volatile` 变量还可以防止指令重新排序，这是正常的性能增强技术。因此，仅在确实需要增强变量的可见性时才应使用 `volatile` 变量。

# Java ThreadLocal

 *Java* *ThreadLocal* 类使得你可以创建只允许同一个线程读写的变量。因此，即使两个线程执行相同的代码，同时该代码拥有同一个 `ThreadLocal` 变量的引用，这两个线程还是无法看到彼此的 `ThreadLocal` 变量。因此，Java   ThreadLocal 类提供了一种简单的方式保证代码的 [线程安全](http://tutorials.jenkov.com/java-concurrency/thread-safety.html) 。

## 创建 ThreadLocal

你可以像创建任何其他 Java 对象那样创建 `ThreadLocal` 实例——通过 `new` 操作符。示例如下：

```java
private ThreadLocal threadLocal = new ThreadLocal();
```

每个线程只需要这样做一次。现在多个线程可以读取和设置该 `ThreadLocal` 中的值，同时每个线程都只能看到它自己设置的值。

## 设置 ThreadLocal 值

一旦 `ThreadLocal` 被创建出来你就可以设置需要存储在其中的值，使用它的 `set()` 方法。

```java
threadLocal.set("A thread local value");
```

## 获取 ThreadLocal 值

你可以读取存储在 `ThreadLocal` 中的值，使用它的 `get()` 方法。如下所示：

```java
String threadLocalValue = (String) threadLocal.get();
```

## 删除 ThreadLocal 值

删除设置在 ThreadLocal 变量中的值是可能的。你可以调用 `ThreadLocal` 的 `remove()` 方法。如下所示：

```java
threadLocal.remove();
```

## 范型 ThreadLocal

你可以使用范型类型创建 `ThreadLocal`。使用范型类型时，只有范型类型对象可以被设置为 `ThreadLocal` 值。另外，你必须对 `get()` 方法返回的值进行类型转换。如下面例子所示：

```java
private ThreadLocal<String> myThreadLocal = new ThreadLocal<String>();
```

现在你只能在 `ThreadLocal` 实例中存储字符串。另外，你不需要对获取自 `ThreadLocal` 的值进行类型转换：

```java
myThreadLocal.set("Hello ThreadLocal");

String threadLocalValue = myThreadLocal.get();
```

## ThreadLocal 初始值

可以为 Java `ThreadLocal` 设置一个初始值，该值将在首次调用 `get()` 时使用——在以新值调用 `set()` 之前。您可以通过两种方式为 `ThreadLocal` 指定初始值：

-创建 `ThreadLocal` 子类并覆写 `initialValue()` 方法。
-使用 `Supplier` 接口的实现创建 `ThreadLocal` 。

接下来详细介绍两种方法。

### 覆写 initialValue()

第一种为 Java `ThreadLocal` 变量指定初始值的方法是创建一个 `ThreadLocal` 子类并覆盖 `initialValue()` 方法。最简单的创建 `ThreadLocal` 子类的方法就是简单地创建一个匿名子类，就在你创建该 `ThreadLocal` 变量的位置。下面是创建一个 `ThreadLocal` 的匿名子类并覆盖 `initialValue()` 方法的例子：

```java
private ThreadLocal myThreadLocal = new ThreadLocal<String>() {
    @Override protected String initialValue() {
        return String.valueOf(System.currentTimeMillis());
    }
};    
```

注意，不同的线程会看到不同的初始值。每个线程将创建自己的初始值。只有当你从 `initialValue()` 方法返回同一个对象时，所有线程才能看到相同的对象。然而，使用 `ThreadLocal` 的根本目的就是避免不同的线程看到相同的变量对象实例。

### 提供 Supplier 实现

第二种为 Java `ThreadLocal` 变量指定初始值的方法是使用静态工厂方法 `withInitial(Supplier)` 传递一个 `Supplier` 接口实现作为参数。该 `Supplier` 实现提供 `ThreadLocal` 的初始值。示例如下：

```
ThreadLocal<String> threadLocal = ThreadLocal.withInitial(new Supplier<String>() {
    @Override
    public String get() {
        return String.valueOf(System.currentTimeMillis());
    }
});
```

由于 `Supplier` 是一个 [函数式接口](http://tutorials.jenkov.com/java-functional-programming/functional-interfaces.html) ，它可以使用 [Java Lambda Expression](http://tutorials.jenkov.com/java/lambda-expressions.html) 实现。下面示例展示了如何使用 lambda 表达式提供 `Supplier` 实现给 `withInitial()` ：

```java
ThreadLocal threadLocal = ThreadLocal.withInitial(
        () -> { return String.valueOf(System.currentTimeMillis()); } );
```

如你所见，这样会简短一些。不过还能继续变短，使用最紧凑语法的 lambada 表达式：

```java
ThreadLocal threadLocal3 = ThreadLocal.withInitial(
        () -> String.valueOf(System.currentTimeMillis()) );
```

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

# Thread 信号

线程信号的目的是允许线程彼此之间发送信号。同时，线程信号使得线程可以等待来自其他线程的信号。比如，线程 B 可能等待来自线程 A 的信号，该信号表明数据已经准备好被处理。

## 通过共享对象发送信号

线程之间发送信号的简单方式是将信号值设置到某些共享对象变量中。线程 A 可以在同步块内部将布尔类型的成员变量 `hasDataToProcess` 为 `true` ，线程 B 可以读取该成员变量，同样也是在同步块中。下面的示例展示了一个可以承载一个信号的对象，同时提供了相应的设置和检查方法：

```java
public class MySignal{

  protected boolean hasDataToProcess = false;

  public synchronized boolean hasDataToProcess(){
    return this.hasDataToProcess;
  }

  public synchronized void setHasDataToProcess(boolean hasData){
    this.hasDataToProcess = hasData;  
  }

}
```

线程 A 和 B 必须拥有一个共享的 `MySignal` 示例的引用来承载信号。如果两个线程拥有的是不同对象实例的引用，将无法检测到彼此的信号。需要处理的数据可以存储在与 `MySignal` 实例分开的共享缓冲区内。

## 忙等

需要处理数据的线程 B 正在等待数据准备好被处理。换句话说，它正在等待来自线程 A 的表示 `hasDataToProcess()` 返回 `true` 的信号。这是在线程 B 等待该信号期间运行的循环：

```java
protected MySignal sharedSignal = ...

...

while(!sharedSignal.hasDataToProcess()){
  //do nothing... busy waiting
}
```

注意，该循环将会一直运行直到 `hasDataToProcess()` 返回 `true`。这被称为忙等。线程在等待期间是繁忙的。

## wait(), notify() 和 notifyAll()

忙等策略无法有效利用运行等待线程的计算机的 CPU 资源，除非平均等待时间非常短。相反，如果等待线程可以休眠或者不活动直到接收到所等待的信号，无疑更加聪明。

Java 拥有一种内置的等待机制允许线程在等待信号时变成不活动状态。`java.lang.Object` 类定义了三个方法，`wait()`，`notify()`，以及 `notifyAll()` 来做到这一点。

在任何对象上调用 `wait()` 的线程会变成不活动状态，直到另外的线程在该对象上调用 `notify()` 方法。为了调用这两个方法，调用者线程必须首先获得该对象的锁。换句话说，调用者线程必须在同步块内部调用着两个方法。下面是示例：

```java
public class MonitorObject{
}

public class MyWaitNotify{

  MonitorObject myMonitorObject = new MonitorObject();

  public void doWait(){
    synchronized(myMonitorObject){
      try{
        myMonitorObject.wait();
      } catch(InterruptedException e){...}
    }
  }

  public void doNotify(){
    synchronized(myMonitorObject){
      myMonitorObject.notify();
    }
  }
}
```

等待线程将调用 `doWait()`，唤醒线程将调用 `doNotify()`。当一个线程在一个对象上调用 `notify()`，在该对象上等待的线程之一就会被唤醒并允许执行。而 `notifyAll()` 方法则会给定对象上等待的所有线程。

如你所见，等待线程和唤醒线程都在同步块内部调用 `wait()` 和 `notify()` 方法。这是强制性的。线程不能在尚未获取到对象锁的情况下在该对象上调用 `wait()`，`notify()` 以及 `notifyAll()` 方法。如果强行这么做，将会抛出 `IllegalMonitorStateException` 。

但是，这怎么可能呢？只要等待线程在同步块中执行，它就不会持有对监视器对象（`myMonitorObject`）的锁吗？等待线程是否不会阻止通知线程从 `doNotify()` 中进入同步块？答案是不会。线程调用 `wait()` 后，它将释放它持有的监视器对象的锁。这也允许其他线程调用 `wait()` 或 `notify()`，因为必须从同步块内部调用这些方法。

一旦线程被唤醒，在调用 `notify()` 的线程退出同步块之前，被唤醒的线程都无法退出 `wait()` 调用。换句话说，被调用的线程在它能够退出 `wait()` 调用之前必须重新获得监视器对象的锁，因为该 `wait()` 调用包含在同步块中。如果多个线程通过 `notifyAll()` 被唤醒，则同一时刻只有其中一个线程能够退出 `wait()` 方法，因为在退出 `wait()` 调用之前，每个线程都必须依次获取监视器对象上的锁。

## 丢失的信号

万一调用时没有线程在等待，方法 `notify()` 和 `notifyAll()` 不会将方法调用保存到它们中。然后，通知信号就丢失了。因此，如果线程在发出信号的线程调用 `wait()` 之前调用 `notify()` ，则等待的线程将丢失该信号。这可能是问题，也可能不是问题，但是在某些情况下，这可能会导致等待线程永远等待，永远不会醒来，因为错过了唤醒信号。

为了避免信号丢失，它们应该被存储在信号类内部。在 `MyWaitNotify` 示例中，唤醒信号应该存储在 `MyWaitNotify` 实例的一个成员变量中。下面是示例：

```java
public class MyWaitNotify2{

  MonitorObject myMonitorObject = new MonitorObject();
  boolean wasSignalled = false;

  public void doWait(){
    synchronized(myMonitorObject){
      if(!wasSignalled){
        try{
          myMonitorObject.wait();
         } catch(InterruptedException e){...}
      }
      //clear signal and continue running.
      wasSignalled = false;
    }
  }

  public void doNotify(){
    synchronized(myMonitorObject){
      wasSignalled = true;
      myMonitorObject.notify();
    }
  }
}
```

注意，在调用 `notify()` 之前，`doNotify()` 方法现在如何将 `wasSignalled` 变量设置为 `true`。另外，请注意 `doWait()` 方法现在如何在调用 `wait()` 之前检查 `wasSignalled` 变量。实际上，如果在先前的 `doWait()` 调用与本次调用之间未接收到任何信号，则仅调用 `wait()`。

## 虚假唤醒

由于无法解释的原因，即使未调用 `notify()` 和 `notifyAll()` ，线程也有可能被唤醒。这就是所谓的虚假唤醒。没有任何原因的唤醒。

如果在 `MyWaitNofity2` 类的 `doWait()` 方法中发生了虚假唤醒，则等待线程可能会继续处理而没有收到适当的信号！这可能会在您的应用程序中引起严重的问题。

为了防止虚假唤醒，请在 `while` 循环内而不是 `if` 语句内检查 `signal` 成员变量。这样的 `while` 循环也称为自旋锁。唤醒的线程一直旋转，直到旋转锁（`while` 循环）中的条件变为 `false` 为止。这是 `MyWaitNotify2` 的修改版本，展示了此内容：

```java
public class MyWaitNotify3{

  MonitorObject myMonitorObject = new MonitorObject();
  boolean wasSignalled = false;

  public void doWait(){
    synchronized(myMonitorObject){
      while(!wasSignalled){
        try{
          myMonitorObject.wait();
         } catch(InterruptedException e){...}
      }
      //clear signal and continue running.
      wasSignalled = false;
    }
  }

  public void doNotify(){
    synchronized(myMonitorObject){
      wasSignalled = true;
      myMonitorObject.notify();
    }
  }
}
```

请注意，`wait()` 调用现在如何嵌套在 `while` 循环而不是 `if` 语句内。如果等待线程在没有收到信号的情况下唤醒，则 `wasSignalled` 成员仍然为 `false`，而 `while` 循环将再次执行，从而使唤醒的线程返回等待状态。