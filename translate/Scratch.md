## 可迭代性

只要有可能，Guava 都会选择提供接受 `Iterable` 而不是 `Collection` 的实用程序。在 Google，遇到并非真正存储在主存储器中的所谓集合并不少见，它们是从数据库或另一个数据中心收集的，如果不实际获取所有元素，就无法支持 `size()` 之类操作。

因此，你希望看到的许多支持所有集合类型的操作都放在 [`Iterables`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html) 中。另外，大多数 `Iterables` 方法都有对应的版本在 [`Iterators`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterators.html) 中，以接受原始的迭代器。

`Iterables` 类中的绝大多数操作都是“惰性”的：它们仅在绝对必要时才进行后备迭代。本身返回 `Iterables` 的方法将返回延迟计算的视图，而不是在内存中显式构造一个集合。

从 Guava 12 开始，`Iterables` 由 [`FluentIterable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/FluentIterable.html)  类补充，包装了 `Iterable` 并为其中的许多操作提供了“流利”的语法。

以下是一些最常用的实用程序，尽管 [Guava 功能习语](https://github.com/google/guava/wiki/FunctionalExplained) 中讨论了 `Iterables` 中许多更“实用”的方法。