# 集合扩展工具

## 介绍

有时您需要编写自己的集合扩展。也许您希望在将元素添加到列表中时添加特殊的行为，或者想要编写实际上由数据库查询支持的 `Iterable`。Guava 提供了许多实用程序，可以使您和我们都更轻松地完成这些任务。（毕竟，我们自己就在从事扩展集合框架的工作。）

## 转发装饰器

对于各种集合接口，Guava 提供了 `Forwarding` 抽象类来简化 [装饰器模式](http://en.wikipedia.org/wiki/Decorator_pattern) 的使用。

`Forwarding` 类定义了一个抽象方法， `delegate()`，你应该覆盖这个方法并返回装饰之后的对象。其他的每个方法都直接委托给委托类：比如， `ForwardingList.get(int)` 被简单地实现为 `delegate().get(int)`。

通过将 `ForwardingXXX` 子类化并实现 `delegate()` 方法，您可以仅覆盖目标类中的选定方法，从而添加修饰的功能，而不必自己委派每个方法。

此外，许多方法都有一个 `standardMethod` 实现，可用于恢复预期的行为，并提供一些与（例如） 在 JDK 中扩展 `AbstractList` 或其他骨架类。

让我们举一个例子。假设您想装饰 `List`，以便它记录添加到其中的所有元素。当然，无论使用哪种方法添加元素 `add(int, E)`， `add(E)`， 或者 `addAll(Collection)` ，我们都希望记录元素。因此，我们必须覆盖所有这些方法。

```java
class AddLoggingList<E> extends ForwardingList<E> {
  final List<E> delegate; // backing list
  @Override protected List<E> delegate() {
    return delegate;
  }
  @Override public void add(int index, E elem) {
    log(index, elem);
    super.add(index, elem);
  }
  @Override public boolean add(E elem) {
    return standardAdd(elem); // implements in terms of add(int, E)
  }
  @Override public boolean addAll(Collection<? extends E> c) {
    return standardAddAll(c); // implements in terms of add
  }
}
```

请记住，默认情况下，所有方法都直接转发给委托，因此，覆盖 `ForwardingMap.put` 不会更改 `ForwardingMap.putAll` 的行为。小心重写必须更改其行为的每种方法，并确保修饰后的集合满足其约定。

通常，由抽象集合框架提供的大多数方法（如 `AbstractList` ）也作为 `standard` 实现在 `Forwarding` 装饰器中提供。

提供特殊视图的接口有时会提供这些视图的 `Standard` 实现。例如，`ForwardingMap` 提供了 `StandardKeySet`， `StandardValues`，和 `StandardEntrySet` 类，每一个类都尽可能将其方法委托给装饰后的 map，否则它们将剩下不能被委托的抽象方法。

| Interface       | Forwarding Decorator                                         |
| --------------- | ------------------------------------------------------------ |
| `Collection`    | [`ForwardingCollection`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingCollection.html) |
| `List`          | [`ForwardingList`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingList.html) |
| `Set`           | [`ForwardingSet`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingSet.html) |
| `SortedSet`     | [`ForwardingSortedSet`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingSortedSet.html) |
| `Map`           | [`ForwardingMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingMap.html) |
| `SortedMap`     | [`ForwardingSortedMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingSortedMap.html) |
| `ConcurrentMap` | [`ForwardingConcurrentMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingConcurrentMap.html) |
| `Map.Entry`     | [`ForwardingMapEntry`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingMapEntry.html) |
| `Queue`         | [`ForwardingQueue`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingQueue.html) |
| `Iterator`      | [`ForwardingIterator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingIterator.html) |
| `ListIterator`  | [`ForwardingListIterator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingListIterator.html) |
| `Multiset`      | [`ForwardingMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingMultiset.html) |
| `Multimap`      | [`ForwardingMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingMultimap.html) |
| `ListMultimap`  | [`ForwardingListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingListMultimap.html) |
| `SetMultimap`   | [`ForwardingSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ForwardingSetMultimap.html) |

## PeekingIterator

有时候，普通的 `Iterator` 接口不满足需求。

`Iterators` 支持方法 [`Iterators.peekingIterator(Iterator)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterators.html#peekingIterator-java.util.Iterator-)，包装了 `Iterator` 并返回 [`PeekingIterator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/PeekingIterator.html)，  `Iterator` 的子类，允许你 [`peek()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/PeekingIterator.html#peek--) 将会在下一次 `next()` 调用时被返回的元素。

*注意*：被 `Iterators.peekingIterator` 返回的 `PeekingIterator` 不支持在 `peek()` 之后的 `remove()` 调用。

举个例子：拷贝一个 `List` 的同时清除连续的重复元素。

```java
List<E> result = Lists.newArrayList();
PeekingIterator<E> iter = Iterators.peekingIterator(source.iterator());
while (iter.hasNext()) {
  E current = iter.next();
  while (iter.hasNext() && iter.peek().equals(current)) {
    // skip this duplicate element
    iter.next();
  }
  result.add(current);
}
```

实现这一目的的传统方法是保持前一个元素的引用，在适当的条件下回退，但是很容易出错。 `PeekingIterator` 相对来说更加直接和容易理解和使用。

## AbstractIterator

实现你自己的 `Iterator`？ [`AbstractIterator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/AbstractIterator.html) 可以帮助你。

举例说明。假设我们希望包装迭代器，用来跳过 null 值。

```java
public static Iterator<String> skipNulls(final Iterator<String> in) {
  return new AbstractIterator<String>() {
    protected String computeNext() {
      while (in.hasNext()) {
        String s = in.next();
        if (s != null) {
          return s;
        }
      }
      return endOfData();
    }
  };
}
```

实现一个方法， [`computeNext()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/AbstractIterator.html#computeNext--)，比较下一个值。当整个序列遍历完成，返回 `endOfData()` 以标记迭代结束。

*注意：*`AbstractIterator` 扩展了 `UnmodifiableIterator`，它禁止实现 `remove()`。如果您需要一个支持 `remove()` 的迭代器，则不应该扩展 `AbstractIterator`。

### AbstractSequentialIterator

某些迭代器通过其他方式表达最简单。 [`AbstractSequentialIterator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/AbstractSequentialIterator.html) 提哦功能了表达迭代的另外一种方法。

```java
Iterator<Integer> powersOfTwo = new AbstractSequentialIterator<Integer>(1) { // note the initial value!
  protected Integer computeNext(Integer previous) {
    return (previous == 1 << 30) ? null : previous * 2;
  }
};
```

在这里，我们实现了方法 [`computeNext(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/AbstractSequentialIterator.html#computeNext-T-)，它接受以前一个值作为参数。

请注意，如果迭代器应立即结束，则还必须传递一个初始值或 `null`。请注意，`computeNext` 假定 `null` 值表示迭代结束 —— `AbstractSequentialIterator` 不能用于实现可能返回 `null` 的迭代器。

