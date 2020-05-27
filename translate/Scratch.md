# 同步器剖析

即使许多同步器（锁，信号量，阻塞队列等）在功能上有所不同，它们的内部设计通常也没有太大不同。换句话说，它们在内部由相同（或相似）的基本部分组成。在设计同步器时，了解这些基本部分会很有帮助。

**注意：**本文内容是 Jakob Jenkov，Toke Johansen 和 LarsBjørn 于 2004 年春季在哥本哈根 IT 大学开设的一个 M.Sc. 学生项目的部分内容。在这个项目中，我们问道格·李（Doug Lea）是否知道类似的工作。有趣的是，在 Java 5 并发实用程序的开发过程中，他独立于该项目也得出了类似的结论。我相信，Doug Lea 的工作在 ["Java Concurrency in Practice"](http://www.amazon.com/Java-Concurrency-Practice-Brian-Goetz/dp/0321349601/ref=pd_bbs_sr_1?ie=UTF8&s=books&qid=1215418711&sr=8-1) 一书中进行了描述。该书包含一章，标题为“同步器解剖”，其内容与本文相似，尽管不完全相同。

大部分(可能不是全部)同步器的目的都是守卫某些代码区域(临界区)以适应多线程并发访问。为了实现这一目标，同步器通常需要下面这几部分：

1. [状态](http://tutorials.jenkov.com/java-concurrency/anatomy-of-a-synchronizer.html#state)
2. [访问条件](http://tutorials.jenkov.com/java-concurrency/anatomy-of-a-synchronizer.html#accesscondition)
3. [状态变化](http://tutorials.jenkov.com/java-concurrency/anatomy-of-a-synchronizer.html#statechanges)
4. [通知策略](http://tutorials.jenkov.com/java-concurrency/anatomy-of-a-synchronizer.html#notificationstrategy)
5. [Test 和 Set 方法](http://tutorials.jenkov.com/java-concurrency/anatomy-of-a-synchronizer.html#testandset)
6. [Set 方法](http://tutorials.jenkov.com/java-concurrency/anatomy-of-a-synchronizer.html#set)

并不是所有同步器都包含以上所有部分，那些同步器可能不具有与此处所述完全相同的部分。通常，您总可以找到其中一个或多个部分。

