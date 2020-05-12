### Lists

除了静态构造器方法和函数式编程方法， [`Lists`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html) 在 `List` 对象上提供了很多有用的工具方法。

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`partition(List, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#partition-java.util.List-int-) | 返回基础列表的视图，该视图分为指定大小的块。                 |
| [`reverse(List)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#reverse-java.util.List-) | 返回指定列表的反向视图。注意：如果列表不可变，考虑 [`ImmutableList.reverse()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableList.html#reverse--) 替代。 |

```java
List<Integer> countUp = Ints.asList(1, 2, 3, 4, 5);
List<Integer> countDown = Lists.reverse(theList); // {5, 4, 3, 2, 1}

List<List<Integer>> parts = Lists.partition(countUp, 2); // {{1, 2}, {3, 4}, {5}}
```

### 静态工厂

`Lists` 提供了下列静态工厂方法：

| Implementation | Factories                                                    |
| -------------- | ------------------------------------------------------------ |
| `ArrayList`    | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newArrayList--), [with elements](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newArrayList-E...-), [from `Iterable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newArrayList-java.lang.Iterable-), [with exact capacity](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newArrayListWithCapacity-int-), [with expected size](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newArrayListWithExpectedSize-int-), [from `Iterator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newArrayList-java.util.Iterator-) |
| `LinkedList`   | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newLinkedList--), [from `Iterable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newLinkedList-java.lang.Iterable-) |

