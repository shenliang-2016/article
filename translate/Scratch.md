## Sets

[`Sets`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html) 工具类包含大量有用的方法。

### 集合论运算

我们提供了一系列标准的集合论运算，实现为参数集合的视图。这些方法返回 [`SetView`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.SetView.html)，可以被用于：

- 直接作为一个 `Set`，因为它实现了 `Set` 接口
- 使用  [`copyInto(Set)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.SetView.html#copyInto-S-) 将其复制进入另一个可变的集合
- 使用 [`immutableCopy()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.SetView.html#immutableCopy--) 创建一个不可变副本

| Method                                                       |
| ------------------------------------------------------------ |
| [`union(Set, Set)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#union-java.util.Set-java.util.Set-) |
| [`intersection(Set, Set)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#intersection-java.util.Set-java.util.Set-) |
| [`difference(Set, Set)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#difference-java.util.Set-java.util.Set-) |
| [`symmetricDifference(Set, Set)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#symmetricDifference-java.util.Set-java.util.Set-) |

比如：

```java
Set<String> wordsWithPrimeLength = ImmutableSet.of("one", "two", "three", "six", "seven", "eight");
Set<String> primes = ImmutableSet.of("two", "three", "five", "seven");

SetView<String> intersection = Sets.intersection(primes, wordsWithPrimeLength); // contains "two", "three", "seven"
// I can use intersection as a Set directly, but copying it can be more efficient if I use it a lot.
return intersection.immutableCopy();
```

### 其他 Set 工具

| Method                                                       | Description                                                | See Also                                                     |
| ------------------------------------------------------------ | ---------------------------------------------------------- | ------------------------------------------------------------ |
| [`cartesianProduct(List)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#cartesianProduct-java.util.List-) | 返回可以通过从每个集合中选择一个元素获得的每个可能的列表。 | [`cartesianProduct(Set...)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#cartesianProduct-java.util.Set...-) |
| [`powerSet(Set)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#powerSet-java.util.Set-) | 返回指定集合的子集。                                       |                                                              |

```java
Set<String> animals = ImmutableSet.of("gerbil", "hamster");
Set<String> fruits = ImmutableSet.of("apple", "orange", "banana");

Set<List<String>> product = Sets.cartesianProduct(animals, fruits);
// {{"gerbil", "apple"}, {"gerbil", "orange"}, {"gerbil", "banana"},
//  {"hamster", "apple"}, {"hamster", "orange"}, {"hamster", "banana"}}

Set<Set<String>> animalSets = Sets.powerSet(animals);
// {{}, {"gerbil"}, {"hamster"}, {"gerbil", "hamster"}}
```

### 静态工厂

`Sets` 提供了下列静态工厂方法：

| Implementation  | Factories                                                    |
| --------------- | ------------------------------------------------------------ |
| `HashSet`       | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newHashSet--), [with elements](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newHashSet-E...-), [from `Iterable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newHashSet-java.lang.Iterable-), [with expected size](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newHashSetWithExpectedSize-int-), [from `Iterator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newHashSet-java.util.Iterator-) |
| `LinkedHashSet` | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newLinkedHashSet--), [from `Iterable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newLinkedHashSet-java.lang.Iterable-), [with expected size](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newLinkedHashSetWithExpectedSize-int-) |
| `TreeSet`       | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newTreeSet--), [with `Comparator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newTreeSet-java.util.Comparator-), [from `Iterable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newTreeSet-java.lang.Iterable-) |