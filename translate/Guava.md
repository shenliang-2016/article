# Googel Guava User Guide

https://github.com/google/guava/wiki

## 介绍

Guava 项目包含若干个 Google 核心类库，这些类库用在 Java 项目中：集合，缓存，基本数据类型支持，并发类库，通用注解，字符串处理，I/O，等等。这些工具趋势都是 Google 的开发人员每天在生产服务开发中使用的。

不过通读 Javadoc 并不是学习如何使用一个类库的高效方法。这里我们尝试提供了一份更具可读性和趣味性的读物来解释一些最流行和最强大的 Guava 特性。

本 wiki 是一个进行中的项目，其中很多部分仍然在持续更新中。

- 基础工具：使得使用 Java 语言更具乐趣。
  - [使用和避免 null](https://github.com/google/guava/wiki/UsingAndAvoidingNullExplained): `null` 是模棱两可的，可能导致令人迷惑的错误，或者就是淡出的令人不爽。许多 Guava 的工具类拒绝接受 `null` 并对其执行快速失败，而不是默默接受。
  - [预定义条件](https://github.com/google/guava/wiki/PreconditionsExplained): 最简单的方式为你的方法测试预定义条件。
  - [通用 Object 方法](https://github.com/google/guava/wiki/CommonObjectUtilitiesExplained): 简化 `Object` 方法的实现，比如 `hashCode()` 和 `toString()`。
  - [排序](https://github.com/google/guava/wiki/OrderingExplained): Guava 强大的 "链式 `Comparator`" 类。
  - [Throwables](https://github.com/google/guava/wiki/ThrowablesExplained): 对异常和错误的处理和检查的简化。
- 集合：Guava 对 JDK 集合生态系统的扩展。这是 Guava 最成熟和流行的部分。
  - [不可变集合](https://github.com/google/guava/wiki/ImmutableCollectionsExplained)，用于防御性编程，常量集合，以及改善性能。
  - [新的集合类型](https://github.com/google/guava/wiki/NewCollectionTypesExplained)，用于 JDK 集合尚未覆盖的应用场景。主要包括：multisets, multimaps, tables, bidirectional maps, 等等。
  - [强大的集合工具类](https://github.com/google/guava/wiki/CollectionUtilitiesExplained)，用于 `java.util.Collections`  未提供的通用集合操作。
  - [扩展工具](https://github.com/google/guava/wiki/CollectionHelpersExplained): 编写 `Collection` decorator? 实现 `Iterator`? 我们可以使其更简单。
- Graphs：用于建模 [graph](https://en.wikipedia.org/wiki/Graph_(discrete_mathematics))-structured 数据的类库，也就是说，实体以及它们之间的关系。关键特性包括：
  - [Graph](https://github.com/google/guava/wiki/GraphsExplained#graph): 其中的边是没有 id 和其它信息的实体的图。
  - [ValueGraph](https://github.com/google/guava/wiki/GraphsExplained#valuegraph): 其中的边拥有不唯一的值的图。
  - [Network](https://github.com/google/guava/wiki/GraphsExplained#network): 其中的边是唯一对象的图。
  - 支持可变和不可变图，有向图和无向图，以及若干其它属性。
- [缓存](https://github.com/google/guava/wiki/CachesExplained): 本地缓存，保证正确的行为，同时支持各种不同的超时失效行为。
- [功能习语](https://github.com/google/guava/wiki/FunctionalExplained): 尽管很少见，Guava 的功能习语可以显著简化代码。
- 并发：强大而简单的抽象，使得编写并发代码变得简单。
  - [ListenableFuture](https://github.com/google/guava/wiki/ListenableFutureExplained): Futures, 携带当它们被完成时会被调用的回调。
  - [Service](https://github.com/google/guava/wiki/ServiceExplained): 启动和关闭相关操作，为您处理困难的状态逻辑。
- [Strings](https://github.com/google/guava/wiki/StringsExplained): 一些非常有用的字符串工具类：切分，连接，填充，等等。
- [Primitives](https://github.com/google/guava/wiki/PrimitivesExplained): 基本数据类型操作，比如 `int` 和 `char`，JDK 并未提供这些操作，包括某些类型的无符号变体。
- [Ranges](https://github.com/google/guava/wiki/RangesExplained): Guava 的强大 API 用于 `Comparable` 类型的范围操作，包括连续数据类型和离散数据类型。
- [I/O](https://github.com/google/guava/wiki/IOExplained): 简化的 I/O 操作，特别是针对 Java 5 中 6 的 I/O 流和文件操作。
- [Hashing](https://github.com/google/guava/wiki/HashingExplained): 比 `Object.hashCode()` 提供的更复杂哈希的工具，包括 Bloom 过滤器。
- [EventBus](https://github.com/google/guava/wiki/EventBusExplained): 组件之间的发布-订阅式通信，而无需组件之间进行显式注册。
- [Math](https://github.com/google/guava/wiki/MathExplained): JDK 未提供经过优化，经过全面测试的数学实用程序。
- [Reflection](https://github.com/google/guava/wiki/ReflectionExplained): 用于 Java 反射功能的 Guava 实用程序。
- 提示：使用 Guava 使您的应用程序按您希望的方式工作。
  - [哲学Philosophy](https://github.com/google/guava/wiki/PhilosophyExplained): Guava 是什么而不是什么，以及我们的目标。
  - [在构建中使用 Guava](https://github.com/google/guava/wiki/UseGuavaInYourBuild), 使用的构建系统包括 Maven, Gradle, 等等。
  - [使用 ProGuard](https://github.com/google/guava/wiki/UsingProGuardWithGuava) 避免将你不需要的 Guava 部分打包进入你的 JAR 中。
  - [Apache Commons equivalents](https://github.com/google/guava/wiki/ApacheCommonCollectionsEquivalents), 帮助您从使用 Apache Commons Collections 转换代码。
  - [兼容性](https://github.com/google/guava/wiki/Compatibility), Guava 不同版本之间的细节差异。
  - [Idea Graveyard](https://github.com/google/guava/wiki/IdeaGraveyard), 功能请求已被最终拒绝。
  - [Friends](https://github.com/google/guava/wiki/FriendsOfGuava), 我们喜欢并欣赏的开源项目。
  - [HowToContribute](https://github.com/google/guava/wiki/HowToContribute), 如何为 Guava 做贡献。

**注意：**要讨论此 wiki 的内容，请仅使用 Guava 讨论邮件列表。

## 基础工具

### 使用和避免 `null`

> *"Null sucks."* -[Doug Lea](http://en.wikipedia.org/wiki/Doug_Lea)
>
> *"I call it my billion-dollar mistake."* - [Sir C. A. R. Hoare](http://en.wikipedia.org/wiki/C._A._R._Hoare), on his invention of the null reference

不小心使用 `null` 会导致各种各样的错误。通过研究 Google 代码库，我们发现 95％ 的集合中不支持包含任何 `null` 值，而让它们快速失败而不是默默地接受 `null` 会对开发人员有所帮助。

另外，`null` 是令人不愉快的模棱两可。`null` 返回值应该是什么意思很不明确，例如，`Map.get(key)` 可以返回 `null`，要么是因为映射中的值为 `null`，要么就是该值不在映射中 。Null 可能意味着失败，可能意味着成功，几乎可以意味着任何事情。使用 `null` 以外的东西可以使您的意思更清楚。

也就是说，有时候 `null` 是正确正确的用法。就内存和速度而言，`null` 很节约资源，并且在对象数组中不可避免。但是在应用程序代码中，与库相反，它是混乱，棘手的怪异错误以及令人不快的歧义的主要来源—例如，当 `Map.get` 返回 `null` 时，可能意味着该值不存在，或者该值存在且为 `null`。最关键的是，`null` 完全不能表示 `null` 值的含义。

由于这些原因，只要有可用的 `null` 友好解决方案，Guava 的许多实用程序都被设计为在存在 `null` 的情况下快速失败，而不是允许使用 `null` 。另外，Guava 提供了许多便利，既可以在必要时简化使用 `null` 的工作，又可以帮助您避免使用 `null`。

#### 具体案例

如果您尝试在 `Set` 中使用 `null` 值或在 `Map` 中作为键，请不要使用；如果在查找操作期间显式使用特殊的 `null`，则更清楚（不足为奇）。

如果要在 Map 中使用 `null` 作为值，请忽略该条目；单独保存一组非空键（或空键）。将 `Map` 包含该键对应的项（值为空）的情况与 `Map` 没有该键对应的项的情况混合起来很容易。最好将这些键分开，并考虑与键关联的值为 `null` 时，它对您的应用程序意味着什么。

如果您在 `List` 中使用空值-如果列表稀疏，您可能宁愿使用 `Map<Integer, E>`？这实际上可能更有效，并且可能实际上可以更准确地满足您的应用程序需求。

考虑是否存在可以使用的自然“空对象”，有时候是如此。例如，如果它是一个枚举，请添加一个常量以表示您期望 `null` 表示的含义。例如，`java.math.RoundingMode` 具有一个 `UNNECESSARY` 值，以指示“不进行舍入，如果需要舍入则抛出异常”。

如果您确实需要 `null` 值，并且在使用 `null` 敌对的 `collection` 实现时遇到问题，请使用其他实现。例如，使用 `Collections.unmodifiableList(Lists.newArrayList())` 而不是 `ImmmableableList`。

#### Optional

程序员使用 `null` 的许多情况是为了表明某种缺席：也许在有值，无值或找不到值的地方。例如，如果未找到键值，则 `Map.get` 返回 `null`。

`Optional<T>` 是用非 `null` 值替换可为空的 `T` 引用的一种方法。一个 `Optional` 可能包含一个非空的 `T` 引用（在这种情况下，我们说该引用是“存在”），或者可能不包含任何内容（在这种情况下，我们说该引用是“不存在”），永远不表示“包含 null”。

```java
Optional<Integer> possible = Optional.of(5);
possible.isPresent(); // returns true
possible.get(); // returns 5
```

`Optional` 并不是与其他编程环境中任何现有 "option" 或 "maybe" 构造的直接类似物，尽管它可能具有某些相似之处。

我们在这里列出了一些最常见的 `Optional` 操作。

##### 创建 Optional

`Optional` 包含下表中的静态方法。

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`Optional.of(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#of-T-) | 创建一个包含给定的非空值，或者对 null 快速失败的 Optional 。 |
| [`Optional.absent()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#absent--) | 返回某类型的一个不存在的 Optional 。                         |
| [`Optional.fromNullable(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#fromNullable-T-) | 将给定的可能为 null 的引用转换为 Optional，将 non-null 视为存在，将 null 视为不存在。 |

##### 查询方法

这些都是基于特定 `Optional<T>` 值的非静态方法。

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`boolean isPresent()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#isPresent--) | 如果该 `Optional` 包含一个非空实例则返回 `true` 。           |
| [`T get()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#get--) | 返回包含的 `T` 实例，该实例必须存在； 否则，抛出 `IllegalStateException`。 |
| [`T or(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#or-T-) | 返回此`Optional` 中的当前值，如果没有，则返回指定的默认值。  |
| [`T orNull()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#orNull--) | 返回此 `Optional` 中的当前值，如果没有，则返回 `null` 。是 `fromNullable` 的逆运算。 |
| [`Set asSet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Optional.html#asSet--) | 如果有一个实例，则返回一个不可变的单例 `Set`，其中包含 `Optional` 中的实例，否则返回一个空的不可变集。 |

`Optional` 还提供了一些其它通用方法，查看文档了解有关细节。

##### 重点是什么？

除了给 `null` 一个 *name* 带来的可读性提高之外，`Optional` 的最大优点是它的防呆能力。如果您要完全编译程序，它会迫使您积极考虑不存在的情况，因为您必须主动展开 `Optional` 并解决该情况。Null 使得简单地忘记事情变得异常容易，尽管 FindBugs 有所帮助，但我们认为它几乎不能解决问题。

当您**返回**可能存在或可能不存在的值时，这一点尤其重要。您（和其他人）更有可能忘记 `other.method(a, b)` 可能返回空值，而您可能会忘记 `a` 在实现 `other.method` 时可能为 `null`。返回 `Optional` 使调用者无法忘记这种情况，因为调用者必须自己打开对象才能编译代码。

#### 便利方法

无论何时，如果你想要用某些默认值替换 `null` 值，使用 [`MoreObjects.firstNonNull(T, T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/MoreObjects.html#firstNonNull-T-T-)。正如方法名称所暗示的，如果两个输入参数都是 null，该方法将快速失败并抛出 `NullPointerException`。如果你正在使用 `Optional`，那么有个更好的替代品—比如， `first.or(second)`。

在 `Strings` 中提供了一些处理可能为 `null` 的 `String` 值的方法。具体来说，我们提供恰当的名称：

- [`emptyToNull(String)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Strings.html#emptyToNull-java.lang.String-)
- [`isNullOrEmpty(String)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Strings.html#isNullOrEmpty-java.lang.String-)
- [`nullToEmpty(String)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Strings.html#nullToEmpty-java.lang.String-)

我们想强调的是，这些方法主要用于与使 null 字符串和空字符串相等的令人讨厌的 API 进行接口。每次*您*编写将 null 字符串和空字符串放在一起的代码时，Guava 团队都会哭泣。（如果 null 字符串和空字符串在含义上是积极不同的，那会更好，但是将它们视为同一件事是一种令人不安的常见代码味道。）

### Preconditions

Guava 提供了大量的 precondition 检查工具。我们强烈推荐你静态导入它们。

每个方法都有三种变体：

1. 没有额外参数。所有抛出的异常都不携带错误信息。
2. 一个额外的 `Object` 参数。所有抛出的异常都携带错误信息 `object.toString()`。
3. 一个额外的 `String` 参数，以及任意数量的额外 `Object` 参数。此行为类似于 printf，但是为了 GWT 兼容性和执行效率，只允许 `%s` 占位符。
   - 注意：`checkNotNull`，`checkArgument` 和 `checkState` 具有大量重载，这些重载采用基本数据类型参数和 `Object` 参数的组合，而不是 varargs 数组—在绝大多数情况下这允许上述调用避免基本数据类型装箱和 varags 数组分配。

第三种变体的例子：

```
checkArgument(i >= 0, "Argument was %s but expected nonnegative", i);
checkArgument(i < j, "Expected i < j, but %s >= %s", i, j);
```

| Signature (not including extra args)                         | Description                                                  | Exception thrown on failure |
| ------------------------------------------------------------ | ------------------------------------------------------------ | --------------------------- |
| [`checkArgument(boolean)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkArgument-boolean-) | 检查布尔值是否为 `true`。用于验证方法的参数。                | `IllegalArgumentException`  |
| [`checkNotNull(T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkNotNull-T-) | 检查值是否不为 `null`。直接返回值，因此可以内联使用 `checkNotNull(value)`。 | `NullPointerException`      |
| [`checkState(boolean)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkState-boolean-) | 检查对象的某些状态，而不依赖于方法参数。 例如，`Iterator`可能会使用它来检查是否在调用 `remove` 之前调用了`next`。 | `IllegalStateException`     |
| [`checkElementIndex(int index, int size)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkElementIndex-int-int-) | 检查 `index` 是否为指定大小的列表，字符串或数组中的有效 *element* 索引。元素索引的范围可以从 0（含0）到 `size`（不含）。您不直接传递列表，字符串或数组；你只要通过它的大小。返回 `index`。 | `IndexOutOfBoundsException` |
| [`checkPositionIndex(int index, int size)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkPositionIndex-int-int-) | 检查`index`是否为指定大小的列表，字符串或数组中的有效“位置”索引。位置索引的范围可以从 0（含0）到 `size`（含）。 您不直接传递列表，字符串或数组；你只传递它的大小。返回`index`。 | `IndexOutOfBoundsException` |
| [`checkPositionIndexes(int start, int end, int size)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Preconditions.html#checkPositionIndexes-int-int-int-) | 检查 `[start, end)` 是具有指定大小的列表，字符串或数组的有效子范围。带有自己的错误消息。 | `IndexOutOfBoundsException` |

由于某些原因，我们更倾向于使用来自 Apache Commons 类库的工具来更新上面示例中的 preconditions 检查。主要原因：

- 静态导入后，Guave 方法清晰明了。 `checkNotNull` 可以清楚地说明正在执行的操作以及抛出的异常。
- `checkNotNull` 校验之后返回它的参数，允许跟构造方法调用放在一行的写法： `this.field = checkNotNull(field);`。
- 简单的， varargs "printf-style" 异常信息。(这个优点也是为何我们推荐继续使用 `checkNotNull` 在 [`Objects.requireNonNull`](http://docs.oracle.com/javase/7/docs/api/java/util/Objects.html#requireNonNull(java.lang.Object,java.lang.String)))

我们建议您将  preconditions  分成不同的行，这可以帮助您确定调试时哪个前提条件失败。此外，您还应该提供有用的错误消息，当每项检查单独执行时，此消息会更容易。

### 排序

#### 示例

```
assertTrue(byLengthOrdering.reverse().isOrdered(list));
```

#### 概述

[`Ordering`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html) 是 Guava 的 "fluent" `Comparator` 类，可以用于构建负责的比较器并将其应用于对象集合。

在其核心，`Ordering` 实例就只是一个特殊的 `Comparator` 实例。`Ordering` 仅仅包含需要依赖 `Comparator` 的方法(比如，`Collections.max`)，并使得它们成为可用的实例方法。为了提供额外的能力，`Ordering` 类提供了链式方法来调整和增强现有的比较器。

#### 创建

通用排序由静态方法提供：

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`natural()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#natural--) | 使用可比较类型的 *自然顺序* 。                               |
| [`usingToString()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#usingToString--) | 按对象的字符串表示形式，如 `toString()` 返回的那样，按字典顺序对其进行比较。 |

将预先存在的 `Comparator` 加入 `Ordering` 可以简单地通过使用 [`Ordering.from(Comparator)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#from-java.util.Comparator-) 实现。

但是创建自定义 `Ordering` 的更常见方法是完全跳过 `Comparator`，而直接扩展 `Ordering` 抽象类：

```java
Ordering<String> byLengthOrdering = new Ordering<String>() {
  public int compare(String left, String right) {
    return Ints.compare(left.length(), right.length());
  }
};
```

#### 链式

一个给定的 `Ordering` 可以被包装用于获取派生顺序。最常用的变体包括：

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`reverse()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#reverse--) | 返回逆序。                                                   |
| [`nullsFirst()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#nullsFirst--) | 返回一个将 nulls 排在 non-null 元素之前的 `Ordering` ，否则其行为与原始 `Ordering` 相同。参考 [`nullsLast()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#nullsLast--)。 |
| [`compound(Comparator)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#compound-java.util.Comparator-) | 返回一个使用指定的 `Comparator` 的 `Ordering` 来"打破僵局"。 |
| [`lexicographical()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#lexicographical--) | 返回一个 `Ordering`，按字典顺序对可迭代对象进行排序。        |
| [`onResultOf(Function)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#onResultOf-com.google.common.base.Function-) | 返回一个`Ordering`，该排序通过将函数应用到值上来排序，然后使用原始的`Ordering`来比较结果。 |

比如，你想要为下面这个类设计一个比较器：

```java
class Foo {
  @Nullable String sortedBy;
  int notSortedBy;
}
```

可以处理 null 值的 `sortedBy`。下面是建立在链式方法上的解决方案：

```java
Ordering<Foo> ordering = Ordering.natural().nullsFirst().onResultOf(new Function<Foo, String>() {
  public String apply(Foo foo) {
    return foo.sortedBy;
  }
});
```

阅读 `Ordering` 调用链时，请从右到左“反向”进行。上面的示例通过查找 `Foo` 实例的 `sortedBy` 字段值对它们进行排序，首先将所有空的 `sortedBy` 值移到顶部，然后通过自然字符串排序对其余值进行排序。之所以会出现这种反向顺序，是因为每个链接调用都将先前的 `Ordering` “包装”为新的 `Ordering` 。

（“反向”规则的例外：对于 `compound` 的调用链，从左到右读取。为避免混淆，请避免将 `compound` 调用与其他链接的调用混在一起。）

过长的链式调用可能很难理解。我们建议将链接限制为大约三个调用，如上例所示。即使这样，您也可能希望通过分离中间对象（例如 `Function` 实例）来简化代码：

```java
Ordering<Foo> ordering = Ordering.natural().nullsFirst().onResultOf(sortKeyFunction);
```

#### 应用

Guava 提供了许多方法来使用排序来操纵或检查值或集合。我们在这里列出了一些最受欢迎的。

| Method                                                       | Description                                                  | See also                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`greatestOf(Iterable iterable, int k)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#greatestOf-java.lang.Iterable-int-) | 按照此排序规则，从最大到最小的顺序返回指定可迭代对象的 `k` 个最大元素。不一定稳定。 | [`leastOf`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#leastOf-java.lang.Iterable-int-) |
| [`isOrdered(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#isOrdered-java.lang.Iterable-) | 测试特定的 `Iterable` 在该排序规则下是非递减顺序。           | [`isStrictlyOrdered`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#isStrictlyOrdered-java.lang.Iterable-) |
| [`sortedCopy(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#sortedCopy-java.lang.Iterable-) | 返回特定元素 `List` 的有序副本。                             | [`immutableSortedCopy`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#immutableSortedCopy-java.lang.Iterable-) |
| [`min(E, E)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#min-E-E-) | 根据此排序规则返回其两个参数中的最小值。如果值比较相等，则返回第一个参数。 | [`max(E, E)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#max-E-E-) |
| [`min(E, E, E, E...)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#min-E-E-E-E...-) | 根据此排序规则返回其参数的最小值。如果存在多个最小值，则返回第一个。 | [`max(E, E, E, E...)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#max-E-E-E-E...-) |
| [`min(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#min-java.lang.Iterable-) | 返回指定的 `Iterable` 的最小元素。如果 `Iterable` 为空，则抛出 `NoSuchElementException`。 | [`max(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#max-java.lang.Iterable-), [`min(Iterator)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#min-java.util.Iterator-), [`max(Iterator)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html#max-java.util.Iterator-) |

### 通用 Object 方法

#### equals

当你的对象字段可以是 `null`，实现 `Object.equals` 就非常痛苦，因为你不得不单独检查 `null`。使用 [`Objects.equal`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Objects.html#equal-java.lang.Object-java.lang.Object-) 允许你以 null 敏感的方式执行 `equals` 检查，而没有 `NullPointerException` 的风险。

```java
Objects.equal("a", "a"); // returns true
Objects.equal(null, "a"); // returns false
Objects.equal("a", null); // returns false
Objects.equal(null, null); // returns true
```

*注意*: 在 JDK 7 中新引入的 `Objects` 类提供了等效的 [`Objects.equals`](http://docs.oracle.com/javase/7/docs/api/java/util/Objects.html#equals(java.lang.Object, java.lang.Object)) 方法。

#### hashCode

哈希 `Object` 的所有字段应该更简单。Guava 的 [`Objects.hashCode(Object...)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Objects.html#hashCode-java.lang.Object...-) 为字段序列创建一个明智的，顺序敏感的哈希。使用 `Objects.hashCode(field1, field2, ..., fieldn)` 而不是手动构建哈希。

*注意*: 在 JDK 7 中新引入的 `Objects` 类提供了等效的 [`Objects.hash(Object...)`](http://docs.oracle.com/javase/7/docs/api/java/util/Objects.html#hash(java.lang.Object...))。

#### toString

一个设计良好的 `toString` 方法应该在调试中可能是无价之宝，虽然编写会很困难。使用 [`MoreObjects.toStringHelper()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/MoreObjects.html#toStringHelper-java.lang.Object-) 来简单地创建一个有用的 `toString`。一些简单的例子包括：

```java
   // Returns "ClassName{x=1}"
   MoreObjects.toStringHelper(this)
       .add("x", 1)
       .toString();

   // Returns "MyObject{x=1}"
   MoreObjects.toStringHelper("MyObject")
       .add("x", 1)
       .toString();
```

#### compare/compareTo

实现 `Comparator`，或者直接实现 `Comparable` 接口，都比较麻烦。考虑：

```java
class Person implements Comparable<Person> {
  private String lastName;
  private String firstName;
  private int zipCode;

  public int compareTo(Person other) {
    int cmp = lastName.compareTo(other.lastName);
    if (cmp != 0) {
      return cmp;
    }
    cmp = firstName.compareTo(other.firstName);
    if (cmp != 0) {
      return cmp;
    }
    return Integer.compare(zipCode, other.zipCode);
  }
}
```

这段代码很容易混乱，难以查找错误，而且冗长。我们应该能够做得更好。

因此，Guava 提供了 [`ComparisonChain`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ComparisonChain.html)。

`ComparisonChain` 执行一种 "懒" 比较：它只执行比较，直到找到非零结果，之后忽略后续的输入。

```java
   public int compareTo(Foo that) {
     return ComparisonChain.start()
         .compare(this.aString, that.aString)
         .compare(this.anInt, that.anInt)
         .compare(this.anEnum, that.anEnum, Ordering.natural().nullsLast())
         .result();
   }
```

这种链式习惯用法更具可读性，不容易出现偶然的拼写错误，并且足够聪明，无法做比必须的更多的工作。可以在 Guava 的“链式比较器” 类 [`Ordering`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Ordering.html ) 中找到其他比较实用程序，请参考 [此处](https://github.com/google/guava/wiki/OrderingExplained) 中的解释。

### Throwables

Guava 的 [`Throwables`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html) 工具能够显著简化异常处理。

#### 传播

有时候，当你捕获到异常，希望将它抛出给下一个 try/catch 块。这种场景通常出现在处理 `RuntimeException` or `Error` 实例的时候，这两类异常不强制 try/catch 块，当时会被现有的 try/catch 块意外捕获。

Guava 提供了若干工具来简化异常传播。比如：

```java
try {
  someMethodThatCouldThrowAnything();
} catch (IKnowWhatToDoWithThisException e) {
  handle(e);
} catch (Throwable t) {
  Throwables.propagateIfInstanceOf(t, IOException.class);
  Throwables.propagateIfInstanceOf(t, SQLException.class);
  throw Throwables.propagate(t);
}
```

每个方法都会抛出异常，但是抛出的结果 — 比如， `throw Throwables.propagate(t)` — 对向编译器证明将会抛出异常非常有用。

这里是 Guava 提供的异常传播方法的概述：

| Signature                                                    | Explanation                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`RuntimeException propagate(Throwable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#propagate-java.lang.Throwable-) | 如果是 `RuntimeException` 或 `Error`，则按原样传播可抛出对象，或者将其包装到 `RuntimeException` 中并抛出它。保证一定会抛出。返回类型为 `RuntimeException`，因此您可以如上所述编写`throw Throwables.propagate(t)`，Java 将意识到该行肯定会引发异常。 |
| [`void propagateIfInstanceOf(Throwable, Class) throws X`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#propagateIfInstanceOf-java.lang.Throwable-java.lang.Class-) | 原样传播可抛出对象，当且仅当它是一个  `X` 实例。             |
| [`void propagateIfPossible(Throwable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#propagateIfPossible-java.lang.Throwable-) | 原样抛出 `throwable` 仅当它是 `RuntimeException` 或者 `Error`。 |
| [`void propagateIfPossible(Throwable, Class) throws X`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#propagateIfPossible-java.lang.Throwable-java.lang.Class-) | 原样抛出 `throwable` 仅当它是 `RuntimeException`,  `Error`, 或者 `X`。 |

#### 使用 `Throwables.propagate`

##### 模拟 Java 7 多重捕获并重新抛出

通常，如果您想让异常在堆栈中传播，则根本不需要 `catch` 块。由于您不会从异常中恢复，因此您可能不应该记录该异常或采取其他措施。您可能需要执行一些清理操作，但是通常无论清理操作是否成功，都需要进行清理操作，因此它最终以 `finally` 块结尾。但是，带重新抛出的 `catch` 块有时会很有用：也许您必须在传播异常之前更新失败计数，或者可能只想有条件地传播异常。

仅处理一种异常时，捕获和重新抛出异常就很简单。当处理多种异常时，它变得凌乱：

```java
@Override public void run() {
  try {
    delegate.run();
  } catch (RuntimeException e) {
    failures.increment();
    throw e;
  } catch (Error e) {
    failures.increment();
    throw e;
  }
}
```

Java 7 使用 [multicatch](http://docs.oracle.com/javase/7/docs/technotes/guides/language/catch-multiple.html) 解决此问题：

```java
} catch (RuntimeException | Error e) {
  failures.increment();
  throw e;
}
```

非 Java 7 用户被卡住了。他们想编写如下代码，但是编译器不允许他们抛出 `Throwable` 类型的变量：

```java
} catch (Throwable t) {
  failures.increment();
  throw t;
}
```

解决的办法是用 `throw Throwables.propagate(t)` 代替 `throw t` 。在这种有限的情况下，`Throwables.propagate` 的行为与原始代码相同。但是，使用具有其他隐藏行为的 `Throwables.propagate` 编写代码很容易。 特别要注意的是，以上模式仅适用于 `RuntimeException` 和 `Error`。如果 `catch` 块可能捕获了受检查的异常，则您还需要对 `propagateIfInstanceOf` 进行一些调用以保留行为，因为 `Throwables.propagate` 不能直接传播受检查的异常。

总的来说，这种 `propagate` 的用法是一般的。在 Java 7 中是不必要的。在其他版本中，它可以节省少量重复，但是简单的 Extract Method 重构也可以。另外，使用 `propagate` [可以很容易地意外包装已检查的异常](https://github.com/google/guava/commit/287bc67cac97052b13cbbc0358aed8054b14bd4a)。

##### 没必要：将 "throws Throwable" 转化为 "throws Exception"

一些 API，特别是 Java 反射 API 和（作为结果的）JUnit，声明了抛出 `Throwable` 的方法。与这些 API 进行交互可能会很痛苦，因为即使是最通用的 API 通常也只会声明 `throws Exception`。`Throwables.propagate` 被一些调用者使用，这些调用者知道他们具有非 `Exception`，非 `Error` `Throwable` 的特性。这是一个声明执行 JUnit 测试的 `Callable` 的示例：

```java
public Void call() throws Exception {
  try {
    FooTest.super.runTest();
  } catch (Throwable t) {
    Throwables.propagateIfPossible(t, Exception.class);
    Throwables.propagate(t);
  }

  return null;
}
```

这里不需要 `propagate()`，因为第二行等效于 `throw new RuntimeException(t)`。（题外话：这个例子还提醒我，`propagateIfPossible` 可能会引起混淆，因为它不仅传播给定类型的参数，而且传播 `Errors` 和 `RuntimeExceptions`。）

这种模式（或类似的变体，如 `throw new RuntimeException(t)`）在 Google 的代码库中出现了约30次。 （搜索 `'propagateIfPossible[^;]* Exception.class[)];'`）。其中的大多数采用显式的 `throw new RuntimeException(t)` 方法。我们可能希望为 `Throwable` 到 `Exception` 的转换使用一个 `throwWrappingWeirdThrowable` 方法，但是考虑到两行选择，除非我们也废弃 `propagateIfPossible`，否则可能也不需要这个。

#### 有争议的 `Throwables.propagate`

##### 争议：将受检查异常转化为不受检查异常

原则上，未检查的异常表示错误，而检查的异常表示您无法控制的问题。实际上，甚至 JDK 有时也会 [gets](http://docs.oracle.com/javase/6/docs/api/java/lang/Object.html#clone()) [it](http://docs.oracle.com/javase/6/docs/api/java/lang/Integer.html#parseInt(java.lang.String)) [wrong](http://docs.oracle.com/javase/6/docs/api/java/net/URI.html#URI(java.lang.String)) （或至少对于某些方法，[没有适合所有人的答案](http://docs.oracle.com/javase/6/docs/api/java/net/URI.html#create(java.lang.String)) ）。

结果，调用者有时不得不在异常类型之间进行转换：

```java
try {
  return Integer.parseInt(userInput);
} catch (NumberFormatException e) {
  throw new InvalidInputException(e);
}
try {
  return publicInterfaceMethod.invoke();
} catch (IllegalAccessException e) {
  throw new AssertionError(e);
}
```

有时候，调用者使用 `Throwables.propagate`。这有什么缺陷？

主要的一点是代码的含义不太明显。`throw Throwables.propagate(ioException)` 有什么作用？ `throw new RuntimeException(ioException)` 有什么作用？两者的作用相同，但后者更直接。前者提出了一个问题：“这是做什么的？它不仅包装在 `RuntimeException` 中，是吗？如果是，为什么他们要编写一个方法包装器？”

诚然，这里的部分问题是“传播”是一个模糊的名称。（这是 [抛出未声明的异常的方法](http://www.eishay.com/2011/11/throw-undeclared-checked-exception-in.html) 吗？）也许 “wrapIfChecked” 会更好。即使调用了该方法，也不会对已知的已检查异常调用它。甚至还有其他缺点：也许有比普通的 `RuntimeException` 更合适的类型供您抛出——比如说 `IllegalArgumentException`。

当仅*可能*将异常作为检查异常时，有时我们还会看到`propagate`。结果比替代方法小一些，直接性也小一些：

```java
} catch (RuntimeException e) {
  throw e;
} catch (Exception e) {
  throw new RuntimeException(e);
}
} catch (Exception e) {
  throw Throwables.propagate(e);
}
```

但是，这里显然的问题是将已检查的异常转换为未检查的异常的一般做法。在某些情况下，这无疑是正确的事情，但更经常地，它是用来避免处理合法的已检查异常。这导致我们开始辩论有关检查异常是否总体上是一个坏主意。 我不想在这里讨论所有内容。可以说，`Throwables.propagate` 不是为了鼓励 Java 用户忽略 `IOException` 等而存在。

##### 争议：异常挖洞

但是，当您实现不允许抛出异常的方法时，该怎么办？有时，您需要将异常包装在未经检查的异常中。很好，但是同样，对于简单的包装，“传播”是不必要的。实际上，手动包装可能是更可取的：如果包装*每个*异常（而不是仅检查的异常），则可以在另一端包装所有异常，从而减少特殊情况。此外，您可能希望对包装使用自定义异常类型。

##### 争议：从别的线程重新抛出异常

```java
try {
  return future.get();
} catch (ExecutionException e) {
  throw Throwables.propagate(e.getCause());
}
```

这里有很多事情要考虑：

1. 原因可能是经过检查的异常。请参阅上面的“将检查的异常转换为未检查的异常”。但是，如果已知该任务不引发检查异常，该怎么办？（也许是 `Runnable` 的结果。）如上所述，您可以捕获异常并抛出 `AssertionError`。`Proagate` 的功能更多。特别是对于 `Future` ，请考虑 [`Futures.get`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/util/concurrent/Futures.html#getUnchecked-java.util.concurrent.Future-)。

2. 原因可能是非`Exception`，非`Error` ,  `Throwable`。（嗯，实际上不可能是一个，但是如果您尝试直接将其重新抛出，编译器将迫使您考虑这种可能性。）请参见上面的 “将 `throwable Throwable` 转换为 `throws Exception`”。

3. 原因可能是未经检查的异常或错误。如果是这样，它将直接被重新抛出。不幸的是，其堆栈跟踪将反映最初在其中创建异常的线程，而不是当前正在其中传播的线程。通常最好在异常链中包含两个线程的堆栈跟踪，如   `get` 抛出的 `ExecutionException` 一样。（这个问题实际上与 `propagate` 无关；它与任何在另一个线程中抛出异常的代码有关。）

#### 因果链

Guava 使研究异常的因果链更为简单，它提供了三种有用的方法，其签名是不言自明的：

- [`Throwable getRootCause(Throwable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#getRootCause-java.lang.Throwable-)
- [`List getCausalChain(Throwable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#getCausalChain-java.lang.Throwable-)
- [`String getStackTraceAsString(Throwable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#getStackTraceAsString-java.lang.Throwable-)

## 集合

### 不可变集合

#### 示例

```java
public static final ImmutableSet<String> COLOR_NAMES = ImmutableSet.of(
  "red",
  "orange",
  "yellow",
  "green",
  "blue",
  "purple");

class Foo {
  final ImmutableSet<Bar> bars;
  Foo(Set<Bar> bars) {
    this.bars = ImmutableSet.copyOf(bars); // defensive copy!
  }
}
```

#### 动机

不可变对象拥有很多优点，包括：

- 可以被不受信任的类库安全地使用。
- 线程安全：可以被多个线程使用而没有产生竞争条件的风险。
- 不需要支持修改，因而能够大量节省时间和空间。所有的不可变集合实现相比于它们的可变兄弟都要更加节省内存。([分析在此](https://github.com/DimitrisAndreou/memory-measurer/blob/master/ElementCostInDataStructures.txt))
- 可以作为常量使用，因为可以认为它始终都是固定的。

创建对象的不可变副本是一种良好的防御性编程技术。Guava 为每种标准 `Collection` 类型提供了简单易用的不可变版本，包括 Guava 自己的 `Collection` 变体。

JDK 提供了 `Collections.unmodifiableXXX` 方法，但是，这些方法在我们看来：

- 笨拙而冗长； 在您想制作防御性副本的任何地方都无法使用。
- 不安全：只有在没有人拥有对原始集合的引用的情况下，返回的集合才是真正不变的。
- 低效：数据结构仍然具有可变集合的所有开销，包括并发修改检查，哈希表中的额外空间等。

**当您不希望修改集合或希望集合保持不变时，最好将其防御性地复制到不可变的集合中。**

**重要提示:** 每个 Guava 不可变集合实现都*拒绝空值*。我们对 Google 的内部代码库进行了详尽的研究，表明大约 5％ 的场景允许在集合中使用 `null` 元素，而其他 95％ 的情况通过在 `null` 上快速失败来提供服务是最好的。如果需要使用空值，请考虑在允许空值的集合实现中使用 `Collections.unmodifiableList` 及其兄弟。可以在 [这里](https://github.com/google/guava/wiki/UsingAndAvoidingNullExplained) 找到更详细的建议。

#### 实现方法

有几种方法可以创建 `ImmutableXXX` 集合：

- 使用 `copyOf` 方法，比如， `ImmutableSet.copyOf(set)`
- 使用 `of` 方法，比如， `ImmutableSet.of("a", "b", "c")` 或者 `ImmutableMap.of("a", 1, "b", 2)`
- 使用 `Builder`，比如：

```java
public static final ImmutableSet<Color> GOOGLE_COLORS =
   ImmutableSet.<Color>builder()
       .addAll(WEBSAFE_COLORS)
       .add(new Color(0, 191, 255))
       .build();
```

除了有序集合， **在构建过程中就会生成元素顺序**，比如：

```java
ImmutableSet.of("a", "b", "c", "a", "d", "b")
```

将按照 "a", "b", "c", "d" 的顺序遍历其元素。

##### `copyOf` 比你想象中的要小

请记住，`ImmutableXXX.copyOf `会在安全的情况下尝试避免复制数据——确切的细节未指定，但实现通常是“智能”的。例如，

```java
ImmutableSet<String> foobar = ImmutableSet.of("foo", "bar", "baz");
thingamajig(foobar);

void thingamajig(Collection<String> collection) {
   ImmutableList<String> defensiveCopy = ImmutableList.copyOf(collection);
   ...
}
```

在这段代码中，`ImmutableList.copyOf(foobar)` 足够聪明，只返回 `foobar.asList()`，这是 `ImmutableSet` 的固定时间视图。

作为一种一般的启发式方法，`ImmutableXXX.copyOf(ImmutableCollection)` 尽量避免线性时间复制，如果

- 可以在恒定时间内使用基础数据结构。例如，`ImmutableSet.copyOf(ImmutableList)` 不能在固定时间内完成。

- 这不会导致内存泄漏——例如，如果您具有 `ImmutableList <String> hugeList`，并且您做了 `ImmutableList.copyOf(hugeList.subList(0, 10))`，则执行显式复制，因此为了避免意外保留不必要的 `hugeList` 中的引用。

- 它不会改变语义——因此，`ImmutableSet.copyOf(myImmutableSortedSet)` 将执行显式复制，因为 `ImmutableSet` 使用的 `hashCode()` 和 `equals` 具有与基于比较器的 `ImmutableSortedSet` de行为不同的语义 。

这有助于最大程度地降低良好的防御性编程风格的性能开销。

##### `asList`

所有不可变的集合都通过 `asList()` 提供 `ImmutableList` 视图，因此——例如——即使您将数据存储为 `ImmutableSortedSet`，也可以通过 `sortedSet.asList().get(k)` 获得第 `k` 个最小的元素。

返回的 `ImmutableList` 通常（并非总是但经常）是恒定开销的视图，而不是显式副本。就是说，它通常比普通的 `List` 要聪明——例如，它将使用后备集合的高效 `contains` 方法。

#### 细节

##### 在哪儿？

| Interface                                                    | JDK or Guava? | Immutable Version                                            |
| ------------------------------------------------------------ | ------------- | ------------------------------------------------------------ |
| `Collection`                                                 | JDK           | [`ImmutableCollection`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableCollection.html) |
| `List`                                                       | JDK           | [`ImmutableList`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableList.html) |
| `Set`                                                        | JDK           | [`ImmutableSet`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableSet.html) |
| `SortedSet`/`NavigableSet`                                   | JDK           | [`ImmutableSortedSet`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableSortedSet.html) |
| `Map`                                                        | JDK           | [`ImmutableMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableMap.html) |
| `SortedMap`                                                  | JDK           | [`ImmutableSortedMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableSortedMap.html) |
| [`Multiset`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#Multiset) | Guava         | [`ImmutableMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableMultiset.html) |
| `SortedMultiset`                                             | Guava         | [`ImmutableSortedMultiset`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/ImmutableSortedMultiset.html) |
| [`Multimap`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#Multimap) | Guava         | [`ImmutableMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableMultimap.html) |
| `ListMultimap`                                               | Guava         | [`ImmutableListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableListMultimap.html) |
| `SetMultimap`                                                | Guava         | [`ImmutableSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableSetMultimap.html) |
| [`BiMap`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#BiMap) | Guava         | [`ImmutableBiMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableBiMap.html) |
| [`ClassToInstanceMap`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#ClassToInstanceMap) | Guava         | [`ImmutableClassToInstanceMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableClassToInstanceMap.html) |
| [`Table`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#Table) | Guava         | [`ImmutableTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableTable.html) |

### 新的集合类型

Guava 引入了大量 JDK 中没有的新的集合类型，我们发现这些集合类型非常有用。所有这些都旨在与 JDK 集合框架愉快地共存，而不会在 JDK 集合抽象中产生麻烦。

通常，Guava 集合实现非常精确地遵循 JDK 接口协定。

#### Multiset

传统的 Java 习惯用法，例如，计算一个单词在文档中出现的次数是这样的：

```java
Map<String, Integer> counts = new HashMap<String, Integer>();
for (String word : words) {
  Integer count = counts.get(word);
  if (count == null) {
    counts.put(word, 1);
  } else {
    counts.put(word, count + 1);
  }
}
```

这很尴尬，容易出错，并且不支持收集各种有用的统计信息，例如单词总数。我们可以做得更好。

Guava 提供了一种新的集合类型 [`Multiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html) ，它支持添加多个相同元素。Wikipedia 在数学中将“多集”定义为"集合概念的一般化，在该概念中，成员可以多次出现在多集中，如在集中并且与元组相反，元素的顺序无关紧要： 多集 {a，a，b} 和 {a，b，a} 相等。”

有两种主要的查看方式：

- 类似于 `ArrayList<E>` 而没有顺序约束：顺序没有意义。
- 类似于 `Map<E, Integer>`，包含元素和出现次数。

Guava 的 `Multiset` API 综合了两种关于 `Multiset` 的看法，如下：

- 当为作为一个普通 `Collection` 时， `Multiset` 的行为更像是无序的 `ArrayList`：
  - 调用 `add(E)` 添加一个给定元素一次。
  - 多集的 `iterator()` 遍历每个元素的每次出现。
  - 多集的 `size()` 所有元素的所有出现次数的总和。
- 附加的查询操作，以及性能特性，类似于你希望从 `Map<E, Integer>` 那里得到的。
  - `count(Object)` 返回有关该元素的数量。对于 `HashMultiset`，时间复杂度 O(1)，对于 `TreeMultiset`，时间复杂度是 O(log n)。
  - `entrySet()` 返回一个 `Set<Multiset.Entry<E>>` ，其行为类似于 `Map` 的 `entrySet`。
  - `elementSet()` 返回一个 `Set<E>` 包含多集中的独特元素，类似于 `keySet()` 之于 `Map`。
  - `Multiset` 实现的内存假定为与其中独特元素数量为线性关系。

值得注意的是，`Multiset` 完全符合 `Collection` 接口的约定，在极少数情况下，JDK 本身具有先例除外——特别是，`TreeMultiset` 与 `TreeSet` 一样，使用比较替代 `Object.equals` 来判断相等。特别是， `Multiset.addAll(Collection)` 在每次出现时都会在 `Collection` 中添加每个元素一次，这比上面 `Map` 方法所需的 `for` 循环要方便得多。

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`count(E)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#count-java.lang.Object-) | 计算已添加到此多集的元素的出现次数。                         |
| [`elementSet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#elementSet--) | 以 `Set<E>` 的形式查看 `Multiset<E>` 的不同元素。            |
| [`entrySet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#entrySet--) | 与 `Map.entrySet()` 类似，返回 `Set<Multiset.Entry<E>>`，其中包含支持 `getElement()` 和 `getCount()` 的条目。 |
| [`add(E, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#add-java.lang.Object-int-) | 添加指定元素的指定出现次数。                                 |
| [`remove(E, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#remove-java.lang.Object-int--) | 删除指定元素的指定出现次数。                                 |
| [`setCount(E, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multiset.html#setCount-E-int-) | 将指定元素的出现次数设置为指定的非负值。                     |
| `size()`                                                     | 返回 `Multiset` 中所有元素的出现总数。                       |

##### Multiset 不是 Map

注意，尽管 `Multiset<E>` 可能是 `Multiset` 实现的一部分，但它不是 `Map<E, Integer>`。`Multiset` 是一种真正的 `Collection` 类型，它满足所有相关的契约义务。其他显着差异包括：

-  `Multiset<E>` 具有仅具有正计数的元素。没有元素可以具有负计数，并且计数为 0 的值被认为不在多集中。它们不会出现在 `elementSet()` 或 `entrySet()` 视图中。
-  `multiset.size()` 返回集合的大小，该大小等于所有元素的计数之和。对于不同元素的数量，使用 `elementSet().size()`。（因此，例如，`add(E)` 将`multiset.size()` 增加一。）
- `multiset.iterator()` 遍历每个元素的每次出现，因此，迭代的长度等于 `multiset.size()`。
- `Multiset<E>` 支持添加元素，删除元素，或者直接设定元素计数。 `setCount(elem, 0)` 等效与删除该元素的所有出现次数。
- `multiset.count(elem)` 对没有出现在多集中的元素永远返回 `0`。

##### 实现

Guava 提供了许多 `Multiset` 实现，大致上对应于 JDK map 实现。

| Map                 | Corresponding Multiset                                       | Supports `null` elements |
| ------------------- | ------------------------------------------------------------ | ------------------------ |
| `HashMap`           | [`HashMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/HashMultiset.html) | Yes                      |
| `TreeMap`           | [`TreeMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/TreeMultiset.html) | Yes                      |
| `LinkedHashMap`     | [`LinkedHashMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/LinkedHashMultiset.html) | Yes                      |
| `ConcurrentHashMap` | [`ConcurrentHashMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ConcurrentHashMultiset.html) | No                       |
| `ImmutableMap`      | [`ImmutableMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableMultiset.html) | No                       |

##### SortedMultiset

[`SortedMultiset`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/SortedMultiset.html) 是 `Multiset` 接口的一种变体，支持在指定范围内有效地提取子多集。例如，您可以使用 `latencies.subMultiset(0, BoundType.CLOSED, 100, BoundType.OPEN).size()` 来确定您的网站在 100ms 延迟内的点击次数，然后将其与 `latencies.size()` 进行比较确定整体比例。

`TreeMultiset` 实现 `SortedMultiset` 接口。在撰写本文时，仍在测试 `ImmutableSortedMultiset` 的 GWT 兼容性。

#### Multimap

每个有经验的 Java 开发者可能都体验过实现 `Map<K, List<V>>` 或者 `Map<K, Set<V>>`，然后处理该结构的某些尴尬之处。比如， `Map<K, Set<V>>` 是表示无标签有向图的典型方式。Guava 的 [`Multimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html) 框架使得处理一个键对应多个值的映射关系变得非常简单。 `Multimap` 就是处理一个键关联到任意多个值的关系的通用方法。

有两种方法可以从概念上考虑 Multimap：作为从单个键到单个值的映射的集合：

```
a -> 1
a -> 2
a -> 4
b -> 3
c -> 5
```

或者作为从单个键到值集合的映射：

```
a -> [1, 2, 4]
b -> [3]
c -> [5]
```

通常，最好从第一个视图的角度考虑 `Multimap` 接口，但可以通过 `asMap()` 视图以任何一种方式查看它，该视图返回一个 `Map<K, Collection<V>>`。最重要的是，不存在映射到空集合的键：键要么映射至至少一个值，要么根本不存在于 `Multimap` 中。

但是，您很少直接使用 `Multimap` 接口。 通常，您会使用 `ListMultimap` 或 `SetMultimap`，它们分别将键映射到 `List` 或 `Set`。

##### 构造

创建 `Multimap` 的最直接的方式是使用 [`MultimapBuilder`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MultimapBuilder.html)，允许你配置应该如何表示你的键和值。比如：

```java
// creates a ListMultimap with tree keys and array list values
ListMultimap<String, Integer> treeListMultimap =
    MultimapBuilder.treeKeys().arrayListValues().build();

// creates a SetMultimap with hash keys and enum set values
SetMultimap<Integer, MyEnum> hashEnumMultimap =
    MultimapBuilder.hashKeys().enumSetValues(MyEnum.class).build();
```

你也可以选择直接使用实现类上的 `create()` 方法，但是我们并不太建议使用 `MultimapBuilder`。

##### 修改

[`Multimap.get(key)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#get-K-) 返回与特定键关联的值视图，即使不存在。对于 `ListMultimap`，它返回一个 `List`，对于 `SetMultimap`，它返回一个 `Set`。

修改会写入底层的 `Multimap`。比如：

```java
Set<Person> aliceChildren = childrenMultimap.get(alice);
aliceChildren.clear();
aliceChildren.add(bob);
aliceChildren.add(carol);
```

其它更直接的修改 multimap 的方法包括：

| Signature                                                    | Description                                                  | Equivalent                                                   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`put(K, V)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#put-K-V-) | 添加一个键到值的关联。                                       | `multimap.get(key).add(value)`                               |
| [`putAll(K, Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#putAll-K-java.lang.Iterable-) | 依次添加键到每个值的关联。                                   | `Iterables.addAll(multimap.get(key), values)`                |
| [`remove(K, V)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#remove-java.lang.Object-java.lang.Object-) | 删除一个从 `key` 到 `value` 的关联，如果 multimap 改变则返回 `true` 。 | `multimap.get(key).remove(value)`                            |
| [`removeAll(K)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#removeAll-java.lang.Object-) | 删除并返回与指定键关联的所有值。返回的集合可能可以修改，也可以不可修改，但是对其进行修改不会影响 multimap。（返回适当的集合类型。） | `multimap.get(key).clear()`                                  |
| [`replaceValues(K, Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#replaceValues-K-java.lang.Iterable-) | 清除所有与 `key` 关联的值，并将 `key` 设置为与每个`values` 关联。返回先前与该键关联的值。 | `multimap.get(key).clear(); Iterables.addAll(multimap.get(key), values)` |

##### 视图

`Multimap` 还支持多种强大的视图。

- [`asMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#asMap--) 将任何 `Multimap<K, V>` 看作 `Map<K, Collection<V>>`。返回的 map 支持 `remove`，同时对返回的集合所作的修改是写穿透的，但是该 map 不支持 `put` 或者 `putAll`。关键是，你可以使用 `asMap().get(key)` 当你希望在不存在的键上使用 `null` 而不是一个新的、可写的空集合时。 (你可以并且应该将 `asMap.get(key)` 转化为合适的集合类型 —— `SetMultimap` 转化为 `Set`  , `ListMultimap` 转化为 `List`  —— 但是类型系统不允许 `ListMultimap` 在这里返回 `Map<K, List<V>>`。)
- [`entries`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#entries--) 将 `Collection<Map.Entry<K, V>>` 看作 `Multimap` 中的所有实体。 (对于 `SetMultimap`，就是一个 `Set`。)
- [`keySet`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#keySet--) 将 `Multimap` 中的各异键看作一个 `Set`。
- [`keys`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#keys--) 将 `Multimap` 中的键看作一个 `Multiset`，多重性等于与该键关联的值的数量。元素可以从 `Multiset` 中删除，但不能添加；更改将写穿透。
- [`values()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimap.html#values--) 将 `Multimap` 中的所有值看作一个 "扁平的" `Collection<V>`，全部作为一个集合。类似于 `Iterables.concat(multimap.asMap().values())`，但是返回一个完整的 `Collection` 。

##### Multimap 不是 Map

 `Multimap<K, V>` 不是 `Map<K, Collection<V>>`，尽管这样的 map 可能被用于 `Multimap` 实现。显著的差异包括：

- `Multimap.get(key)` 始终返回一个非 null，可能为空的集合。这并不意味着 multimap 会花费与该键关联的任何内存，而是返回的集合是一个视图，该视图允许您根据需要添加与键的关联。
- 如果您更喜欢类似 `Map` 的行为，即为不在 multimap 中的键返回 `null`，则使用 `asMap()` 视图来获取 `Map<K, Collection<V>>`。（或者，要从 `ListMultimap` 中获取 `Map<K,`**List**`<V>>` ，请使用静态 [`Multimaps.asMap()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#asMap-com.google.common.collect.ListMultimap-) 方法。`SetMultimap` 和 `SortedSetMultimap` 也存在类似的方法。）
- `Multimap.containsKey(key)` 当且仅当与指定键相关联的任何元素时为 true。特别是，如果键 `k` 先前与一个或多个从 multimap 移除的值相关联，则 `Multimap.containsKey(k)` 将返回 false。
- `Multimap.entries()` 返回 `Multimap` 中所有键的所有条目。如果需要所有键集合条目，请使用 `asMap().entrySet()`。
- `Multimap.size()` 返回整个 multimap 中的条目数，而不是不同键的数。使用 `Multimap.keySet().size()` 来获取不同键的数量。

##### 实现

`Multimap` 提供了各种实现。你可以在大部分可能使用 `Map<K, Collection<V>>` 的场景中使用它们。

| Implementation                                               | Keys behave like... | Values behave like.. |
| ------------------------------------------------------------ | ------------------- | -------------------- |
| [`ArrayListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ArrayListMultimap.html) | `HashMap`           | `ArrayList`          |
| [`HashMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/HashMultimap.html) | `HashMap`           | `HashSet`            |
| [`LinkedListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/LinkedListMultimap.html) `*` | `LinkedHashMap``*`  | `LinkedList``*`      |
| [`LinkedHashMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/LinkedHashMultimap.html)`**` | `LinkedHashMap`     | `LinkedHashSet`      |
| [`TreeMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/TreeMultimap.html) | `TreeMap`           | `TreeSet`            |
| [`ImmutableListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableListMultimap.html) | `ImmutableMap`      | `ImmutableList`      |
| [`ImmutableSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableSetMultimap.html) | `ImmutableMap`      | `ImmutableSet`       |

所有这些实现，除了不可变的版本，全都支持 null 键和值。

`*` `LinkedListMultimap.entries()` 保留不同键值之间的迭代顺序。 有关详细信息，请参见链接。

`**` `LinkedHashMultimap` 保留条目的插入顺序，键的插入顺序以及与任何一个键关联的一组值。

请注意，并非所有实现都实际上与列出的实现一起被实现为 `Map<K, Collection<V>>` ！（特别是，一些 `Multimap` 实现使用自定义哈希表来最大程度地减少开销。）

如果你需要更多的定制化，使用 [`Multimaps.newMultimap(Map, Supplier)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newMultimap-java.util.Map-com.google.common.base.Supplier-) 或者 [list](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newListMultimap-java.util.Map-com.google.common.base.Supplier-) 和 [set](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newSetMultimap-java.util.Map-com.google.common.base.Supplier-) 版本来使用自定义 collection, list, 或者 set 实现作为你的 multimap 的内部支撑。

#### BiMap

将值映射回键的传统方法是维护两个单独的映射，并使两个映射保持同步，但这容易出错，并且在映射中已经存在值时会造成极大的混乱。例如：

```java
Map<String, Integer> nameToId = Maps.newHashMap();
Map<Integer, String> idToName = Maps.newHashMap();

nameToId.put("Bob", 42);
idToName.put(42, "Bob");
// what happens if "Bob" or 42 are already present?
// weird bugs can arise if we forget to keep these in sync...
```

一个 [`BiMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/BiMap.html) 是这样的一个 `Map<K, V>` ：

- 允许你查看“反向”的 `BiMap<V, K>` 使用 [`inverse()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/BiMap.html#inverse--)
- 保证值是唯一的，使得 [`values()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/BiMap.html#values--) 是一个 `Set`

如果你试图将一个键映射到一个已经存在的值，`BiMap.put(key, value)` 将抛出 `IllegalArgumentException` 异常。如果你想要删除任何预先存在的具有特定值的实体，使用 [`BiMap.forcePut(key, value)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/BiMap.html#forcePut-java.lang.Object-java.lang.Object-) 。

```java
BiMap<String, Integer> userId = HashBiMap.create();
...

String userForId = userId.inverse().get(id);
```

##### 实现

| Key-Value Map Impl | Value-Key Map Impl | Corresponding `BiMap`                                        |
| ------------------ | ------------------ | ------------------------------------------------------------ |
| `HashMap`          | `HashMap`          | [`HashBiMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/HashBiMap.html) |
| `ImmutableMap`     | `ImmutableMap`     | [`ImmutableBiMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableBiMap.html) |
| `EnumMap`          | `EnumMap`          | [`EnumBiMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/EnumBiMap.html) |
| `EnumMap`          | `HashMap`          | [`EnumHashBiMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/EnumHashBiMap.html) |

*注意*： `BiMap` 工具，诸如 `synchronizedBiMap` 位于 [`Maps`](https://github.com/google/guava/wiki/CollectionUtilitiesExplained#Maps) 中。

#### Table

```java
Table<Vertex, Vertex, Double> weightedGraph = HashBasedTable.create();
weightedGraph.put(v1, v2, 4);
weightedGraph.put(v1, v3, 20);
weightedGraph.put(v2, v3, 5);

weightedGraph.row(v1); // returns a Map mapping v2 to 4, v3 to 20
weightedGraph.column(v3); // returns a Map mapping v1 to 20, v2 to 5
```

通常，当您尝试一次索引多个键时，您会遇到诸如 `Map<FirstName, Map<LastName, Person>>` 之类的东西，使用起来很丑陋且笨拙。Guava 提供了一种新的集合类型 [`Table`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html) ，它支持任何“行”类型和“列”类型的这种应用场景。`Table` 支持多种视图，可让您从任何角度使用数据，包括：

- [`rowMap()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#rowMap--)，将 `Table<R, C, V>` 视作 `Map<R, Map<C, V>>`。类似地， [`rowKeySet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#rowKeySet--) 返回 `Set<R>`。
- [`row(r)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#row-R-) 返回非空 `Map<C, V>`。写入 `Map` 将会直接写穿透到底层的 `Table`。
- 提供了类似的列方法： [`columnMap()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#columnMap--)， [`columnKeySet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#columnKeySet--)， 和 [`column(c)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#column-C-)。 (基于列的访问效率稍低于基于行的访问。)
- [`cellSet()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.html#cellSet--) 返回的视图将 `Table` 视作 [`Table.Cell`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Table.Cell.html) 集合。 `Cell` 类似于 `Map.Entry`，但是区分行键和列键。

提供了若干种 `Table` 实现，包括：

- [`HashBasedTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/HashBasedTable.html)，由 `HashMap<R, HashMap<C, V>>` 支撑实现。
- [`TreeBasedTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/TreeBasedTable.html)，由 `TreeMap<R, TreeMap<C, V>>` 支撑实现。
- [`ImmutableTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableTable.html)
- [`ArrayTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ArrayTable.html)，要求在构造时指定行和列的完整纬度，但是当表密集时，由二维数组支持，以提高速度和内存效率。`ArrayTable` 的工作方式与其他实现有所不同。有关详细信息，请查阅 Javadoc。

#### ClassToInstanceMap

有时候，你的 map 键不全都是相同的类型：它们本身是数据类型本身，你希望将它们映射到该类型的值。Guava 提供了 [`ClassToInstanceMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ClassToInstanceMap.html) 来实现这一目的。

除了扩展 `Map` 接口， `ClassToInstanceMap` 提供了方法 [`T getInstance(Class)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ClassToInstanceMap.html#getInstance-java.lang.Class-) 和 [`T putInstance(Class, T)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ClassToInstanceMap.html#putInstance-java.lang.Class-java.lang.Object-)，这样就消除了不愉快转型的需求，同时增强了类型安全性。

`ClassToInstanceMap` 拥有一个类型参数，典型地名为 `B`，表示 map 管理的类型的上界。比如：

```java
ClassToInstanceMap<Number> numberDefaults = MutableClassToInstanceMap.create();
numberDefaults.putInstance(Integer.class, Integer.valueOf(0));
```

从技术上讲，`ClassToInstanceMap<B>` 实现了 `Map<Class<? extends B>, B>` ，或换句话说，就是从 B 的子类到 B 的实例的映射。这会使 `ClassToInstanceMap` 中涉及的泛型类型引起混淆，但请记住，`B` 始终是 map 中的类型的上界，通常，`B` 只是 `Object`。

Guava 提供了名为 [`MutableClassToInstanceMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MutableClassToInstanceMap.html) 和 [`ImmutableClassToInstanceMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableClassToInstanceMap.html) 的非常有用的实现。

**重要**：类似于任何其它 `Map<Class, Object>`， `ClassToInstanceMap` 可以包含基本数据类型实体，基本数据类型以及它对应的包装类可以映射到不同的值。

#### RangeSet

`RangeSet` 描述了 *不连续的，非空的* 范围的一个集合。当添加一个范围到一个可变的 `RangeSet`，任何连接的范围都将合并，而空范围将被忽略。比如：

```java
   RangeSet<Integer> rangeSet = TreeRangeSet.create();
   rangeSet.add(Range.closed(1, 10)); // {[1, 10]}
   rangeSet.add(Range.closedOpen(11, 15)); // disconnected range: {[1, 10], [11, 15)}
   rangeSet.add(Range.closedOpen(15, 20)); // connected range; {[1, 10], [11, 20)}
   rangeSet.add(Range.openClosed(0, 0)); // empty range; {[1, 10], [11, 20)}
   rangeSet.remove(Range.open(5, 10)); // splits [1, 10]; {[1, 5], [10, 10], [11, 20)}
```

注意，如果要合并的范围类似 `Range.closed(1, 10)` 和 `Range.closedOpen(11, 15)`，你必须首先使用 [`Range.canonical(DiscreteDomain)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Range.html#canonical-com.google.common.collect.DiscreteDomain-) 对这些范围进行预处理，比如，使用 `DiscreteDomain.integers()`。

**注意**： `RangeSet` 在 GWT 下不支持，也不在 JDK 1.5 反向移植中， `RangeSet` 需要完整使用  JDK 1.6 中的 `NavigableMap` 特性。

##### 视图

`RangeSet` 实现支持相当宽泛的视图，包括：

- `complement()`：查看 `RangeSet` 的补集。 `complement` 也是一个 `RangeSet`，因为它也包含不连续的，非空的范围。
- `subRangeSet(Range<C>)`：返回 `RangeSet` 和指定 `Range` 的交集。这会产生传统有序集合的 `headSet`， `subSet`，以及  `tailSet` 视图。
- `asRanges()`：将 `RangeSet` 视作 `Set<Range<C>>` 因而可以通过迭代器遍历。
- `asSet(DiscreteDomain<C>)` (`ImmutableRangeSet` only)：以 `ImmutableSortedSet<C>` 的形式查看 `RangeSet<C>` ，查看范围内的元素，而不是范围本身。（如果 `DiscreteDomain` 和 `RangeSet` 都无上界或无下界，则不支持此操作。）

##### 查询

除了视图上的操作外，`RangeSet` 还直接支持多种查询操作，其中最主要的是：

- `contains(C)`：对 `RangeSet` 的最基本操作，查询 `RangeSet` 中的任何范围是否包含指定的元素。

- `rangeContaining(C)`：返回包围指定元素的 `Range` ，如果没有则返回 `null`。

- `encloses(Range<C>)`：很简单，测试 `RangeSet` 中的 `Range` 是否包含指定范围。

- `span()`：返回最小的 `Range`，该 `Range` 将 `RangeSet` 中的每个范围包围起来。

#### RangeMap

`RangeMap` 是一个集合类型，描述了从不相交的非空范围到值的映射。与 `RangeSet` 不同，`RangeMap` 从不“合并”相邻的映射，即使相邻的范围被映射到相同的值。例如：

```java
RangeMap<Integer, String> rangeMap = TreeRangeMap.create();
rangeMap.put(Range.closed(1, 10), "foo"); // {[1, 10] => "foo"}
rangeMap.put(Range.open(3, 6), "bar"); // {[1, 3] => "foo", (3, 6) => "bar", [6, 10] => "foo"}
rangeMap.put(Range.open(10, 20), "foo"); // {[1, 3] => "foo", (3, 6) => "bar", [6, 10] => "foo", (10, 20) => "foo"}
rangeMap.remove(Range.closed(5, 11)); // {[1, 3] => "foo", (3, 5) => "bar", (11, 20) => "foo"}
```

##### 视图

`RangeMap` 提供两种视图：

- `asMapOfRanges()`：将 `RangeMap` 视作 `Map<Range<K>, V>`。这可以被用于，比如，遍历 `RangeMap`。
- `subRangeMap(Range<K>)`：将 `RangeMap` 与特定 `Range` 的交集视作 `RangeMap`。这产生了传统的 `headMap`, `subMap`, 和 `tailMap` 操作。

### 集合工具类

有 JDK Collections 框架使用经验的程序员都了解和喜欢使用  [`java.util.Collections`](http://docs.oracle.com/javase/7/docs/api/java/util/Collections.html) 中的工具类。Guava 提供了更多的工具类，它们遵循这样的原则：静态方法适用于所有的集合。这部分内容也是 Guava 类库最流行和最成熟的部分。

与特定接口相对应的方法以相对直观的方式进行分组：

| Interface                                                    | JDK or Guava? | Corresponding Guava utility class                            |
| ------------------------------------------------------------ | ------------- | ------------------------------------------------------------ |
| `Collection`                                                 | JDK           | [`Collections2`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Collections2.html) |
| `List`                                                       | JDK           | [`Lists`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html) |
| `Set`                                                        | JDK           | [`Sets`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html) |
| `SortedSet`                                                  | JDK           | [`Sets`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html) |
| `Map`                                                        | JDK           | [`Maps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html) |
| `SortedMap`                                                  | JDK           | [`Maps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html) |
| `Queue`                                                      | JDK           | [`Queues`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Queues.html) |
| [`Multiset`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#Multiset) | Guava         | [`Multisets`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html) |
| [`Multimap`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#Multimap) | Guava         | [`Multimaps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html) |
| [`BiMap`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#BiMap) | Guava         | [`Maps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html) |
| [`Table`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#Table) | Guava         | [`Tables`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html) |

***正在寻找转换，过滤器之类的东西？ 这些东西在函数式习语下的函数式编程文章中。***

#### 静态构造器

JDK 7 之前，构造新的范型集合需要讨厌的冗长代码：

```java
List<TypeThatsTooLongForItsOwnGood> list = new ArrayList<TypeThatsTooLongForItsOwnGood>();
```

相信大家都会觉得这样不太好。Guava 提供了静态方法可以使用范型去推断表达式右边的类型：

```java
List<TypeThatsTooLongForItsOwnGood> list = Lists.newArrayList();
Map<KeyType, LongishValueType> map = Maps.newLinkedHashMap();
```

可以肯定的是，JDK 7 中的菱形运算符使此工作不再那么麻烦：

```java
List<TypeThatsTooLongForItsOwnGood> list = new ArrayList<>();
```

但是 Guava 远不止于此。使用工厂方法模式，我们可以非常方便地使用其起始元素初始化集合。

```java
Set<Type> copySet = Sets.newHashSet(elements);
List<String> theseElements = Lists.newArrayList("alpha", "beta", "gamma");
```

此外，借助命名工厂方法的功能（有效的 Java 元素1），我们可以提高将集合初始化为大小的可读性：

```java
List<Type> exactly100 = Lists.newArrayListWithCapacity(100);
List<Type> approx100 = Lists.newArrayListWithExpectedSize(100);
Set<Type> approx100Set = Sets.newHashSetWithExpectedSize(100);
```

下面列出了提供的精确静态工厂方法及其相应的实用程序类。

*注意*： Guava 引入的新集合类型不公开原始构造函数，也不在实用程序类中包含初始化程序。相反，它们直接公开静态工厂方法，例如：

```java
Multiset<String> multiset = HashMultiset.create();
```

#### 可迭代性

只要有可能，Guava 都会选择提供接受 `Iterable` 而不是 `Collection` 的实用程序。在 Google，遇到并非真正存储在主存储器中的所谓集合并不少见，它们是从数据库或另一个数据中心收集的，如果不实际获取所有元素，就无法支持 `size()` 之类操作。

因此，你希望看到的许多支持所有集合类型的操作都放在 [`Iterables`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html) 中。另外，大多数 `Iterables` 方法都有对应的版本在 [`Iterators`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterators.html) 中，以接受原始的迭代器。

`Iterables` 类中的绝大多数操作都是“惰性”的：它们仅在绝对必要时才进行后备迭代。本身返回 `Iterables` 的方法将返回延迟计算的视图，而不是在内存中显式构造一个集合。

从 Guava 12 开始，`Iterables` 由 [`FluentIterable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/FluentIterable.html)  类补充，包装了 `Iterable` 并为其中的许多操作提供了“流利”的语法。

以下是一些最常用的实用程序，尽管 [Guava 功能习语](https://github.com/google/guava/wiki/FunctionalExplained) 中讨论了 `Iterables` 中许多更“实用”的方法。

##### 通用

| Method                                                       | Description                                                  | See Also                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`concat(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#concat-java.lang.Iterable-) | 返回几个可迭代对象的串联的惰性视图。                         | [`concat(Iterable...)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#concat-java.lang.Iterable...-) |
| [`frequency(Iterable, Object)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#frequency-java.lang.Iterable-java.lang.Object-) | 返回对象的出现次数。                                         | Compare `Collections.frequency(Collection, Object)`; see [`Multiset`](https://github.com/google/guava/wiki/NewCollectionTypesExplained#Multiset) |
| [`partition(Iterable, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#partition-java.lang.Iterable-int-) | 返回可迭代的分区的不可修改的视图，该视图分为指定大小的块。   | [`Lists.partition(List, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#partition-java.util.List-int-), [`paddedPartition(Iterable, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#paddedPartition-java.lang.Iterable-int-) |
| [`getFirst(Iterable, T default)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#getFirst-java.lang.Iterable-T-) | 返回 iterable 的第一个元素，如果为空，则返回默认值。         | Compare `Iterable.iterator().next()`, [`FluentIterable.first()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/FluentIterable.html#first--) |
| [`getLast(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#getLast-java.lang.Iterable-) | 返回 iterable 的最后一个元素，如果为空则抛出 `NoSuchElementException` 快速失败。 | [`getLast(Iterable, T default)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#getLast-java.lang.Iterable-T-), [`FluentIterable.last()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/FluentIterable.html#last--) |
| [`elementsEqual(Iterable, Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#elementsEqual-java.lang.Iterable-java.lang.Iterable-) | 如果可迭代对象具有相同顺序的相同元素，则返回 `true`。        | Compare `List.equals(Object)`                                |
| [`unmodifiableIterable(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#unmodifiableIterable-java.lang.Iterable-) | 返回迭代的不可修改的视图。                                   | Compare `Collections.unmodifiableCollection(Collection)`     |
| [`limit(Iterable, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#limit-java.lang.Iterable-int-) | 返回一个`Iterable`，最多返回指定数量的元素。                 | [`FluentIterable.limit(int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/FluentIterable.html#limit-int-) |
| [`getOnlyElement(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#getOnlyElement-java.lang.Iterable-) | 返回 `Iterable` 中的唯一元素。如果 iterable 为空或具有多个元素，则快速失败。 | [`getOnlyElement(Iterable, T default)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#getOnlyElement-java.lang.Iterable-T-) |

```java
Iterable<Integer> concatenated = Iterables.concat(
  Ints.asList(1, 2, 3),
  Ints.asList(4, 5, 6));
// concatenated has elements 1, 2, 3, 4, 5, 6

String lastAdded = Iterables.getLast(myLinkedHashSet);

String theElement = Iterables.getOnlyElement(thisSetIsDefinitelyASingleton);
  // if this set isn't a singleton, something is wrong!
```

##### 类集合

通常，集合在其他集合上自然支持这些操作，但对可迭代对象不提供支持。

*当输入实际上是一个 Collection 时，这些操作中的每一个都会委托给相应的 Collection 接口方法。*例如，如果将 `Iterables.size` 传递给 `Collection`，它将调用 `Collection.size` 方法而不是通过迭代器遍历。

| Method                                                       | Analogous `Collection` method      | `FluentIterable` equivalent                                  |
| ------------------------------------------------------------ | ---------------------------------- | ------------------------------------------------------------ |
| [`addAll(Collection addTo, Iterable toAdd)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#addAll-java.util.Collection-java.lang.Iterable-) | `Collection.addAll(Collection)`    |                                                              |
| [`contains(Iterable, Object)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#contains-java.lang.Iterable-java.lang.Object-) | `Collection.contains(Object)`      | [`FluentIterable.contains(Object)`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#contains-java.lang.Object-) |
| [`removeAll(Iterable removeFrom, Collection toRemove)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#removeAll-java.lang.Iterable-java.util.Collection-) | `Collection.removeAll(Collection)` |                                                              |
| [`retainAll(Iterable removeFrom, Collection toRetain)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#retainAll-java.lang.Iterable-java.util.Collection-) | `Collection.retainAll(Collection)` |                                                              |
| [`size(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#size-java.lang.Iterable-) | `Collection.size()`                | [`FluentIterable.size()`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#size--) |
| [`toArray(Iterable, Class)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#toArray-java.lang.Iterable-java.lang.Class-) | `Collection.toArray(T[])`          | [`FluentIterable.toArray(Class)`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#toArray-java.lang.Class-) |
| [`isEmpty(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#isEmpty-java.lang.Iterable-) | `Collection.isEmpty()`             | [`FluentIterable.isEmpty()`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#isEmpty--) |
| [`get(Iterable, int)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#get-java.lang.Iterable-int-) | `List.get(int)`                    | [`FluentIterable.get(int)`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#get-int-) |
| [`toString(Iterable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Iterables.html#toString-java.lang.Iterable-) | `Collection.toString()`            | [`FluentIterable.toString()`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#toString--) |

##### 流利的可迭代性

除了上面和函数习语 [functional](https://github.com/google/guava/wiki/FunctionalExplained) 中介绍的方法外，`FluentIterable` 还有一些方便的方法可以复制到不可变的集合中：

| Result Type          | Method                                                       |
| -------------------- | ------------------------------------------------------------ |
| `ImmutableList`      | [`toImmutableList()`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#toImmutableList--) |
| `ImmutableSet`       | [`toImmutableSet()`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#toImmutableSet--) |
| `ImmutableSortedSet` | [`toImmutableSortedSet(Comparator)`](http://google.github.io/guava/releases/12.0/api/docs/com/google/common/collect/FluentIterable.html#toImmutableSortedSet-java.util.Comparator-) |

#### Lists

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

##### 静态工厂

`Lists` 提供了下列静态工厂方法：

| Implementation | Factories                                                    |
| -------------- | ------------------------------------------------------------ |
| `ArrayList`    | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newArrayList--), [with elements](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newArrayList-E...-), [from `Iterable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newArrayList-java.lang.Iterable-), [with exact capacity](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newArrayListWithCapacity-int-), [with expected size](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newArrayListWithExpectedSize-int-), [from `Iterator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newArrayList-java.util.Iterator-) |
| `LinkedList`   | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newLinkedList--), [from `Iterable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Lists.html#newLinkedList-java.lang.Iterable-) |

#### Sets

[`Sets`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html) 工具类包含大量有用的方法。

##### 集合论运算

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

##### 其他 Set 工具

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

##### 静态工厂

`Sets` 提供了下列静态工厂方法：

| Implementation  | Factories                                                    |
| --------------- | ------------------------------------------------------------ |
| `HashSet`       | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newHashSet--), [with elements](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newHashSet-E...-), [from `Iterable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newHashSet-java.lang.Iterable-), [with expected size](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newHashSetWithExpectedSize-int-), [from `Iterator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newHashSet-java.util.Iterator-) |
| `LinkedHashSet` | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newLinkedHashSet--), [from `Iterable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newLinkedHashSet-java.lang.Iterable-), [with expected size](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newLinkedHashSetWithExpectedSize-int-) |
| `TreeSet`       | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newTreeSet--), [with `Comparator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newTreeSet-java.util.Comparator-), [from `Iterable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Sets.html#newTreeSet-java.lang.Iterable-) |

#### Maps

[`Maps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html) 拥有许多很棒的工具值得单独介绍。

##### `uniqueIndex`

[`Maps.uniqueIndex(Iterable, Function)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#uniqueIndex-java.lang.Iterable-com.google.common.base.Function-) 解决了这样的常见情况：一堆对象每个都有一些独特的属性，并且希望能够基于该属性查找那些对象。

假设我们有一堆已知长度唯一的字符串，并且希望能够查找具有特定长度的字符串。

```java
ImmutableMap<Integer, String> stringsByIndex = Maps.uniqueIndex(strings, new Function<String, Integer> () {
    public Integer apply(String string) {
      return string.length();
    }
  });
```

如果字符串长度不是唯一的，参考下面的 `Multimaps.index` 。

##### `difference`

[`Maps.difference(Map, Map)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#difference-java.util.Map-java.util.Map-) 可让您比较两个 maps 之间的所有差异。它返回一个 `MapDifference` 对象，该对象将维恩图分解为：

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`entriesInCommon()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MapDifference.html#entriesInCommon--) | 同时存在于两个映射中的实体，具有同时匹配的键和值。           |
| [`entriesDiffering()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MapDifference.html#entriesDiffering--) | 具有相同键，但是值不同的实体。map 中的值是 [`MapDifference.ValueDifference`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MapDifference.ValueDifference.html) 类型，你可以看到左值和右值。 |
| [`entriesOnlyOnLeft()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MapDifference.html#entriesOnlyOnLeft--) | 返回那些键在左 map 中存在而右 map 中不存在的实体。           |
| [`entriesOnlyOnRight()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/MapDifference.html#entriesOnlyOnRight--) | 返回那些键在右 map 中存在而左 map 中不存在的实体。           |

```java
Map<String, Integer> left = ImmutableMap.of("a", 1, "b", 2, "c", 3);
Map<String, Integer> right = ImmutableMap.of("b", 2, "c", 4, "d", 5);
MapDifference<String, Integer> diff = Maps.difference(left, right);

diff.entriesInCommon(); // {"b" => 2}
diff.entriesDiffering(); // {"c" => (3, 4)}
diff.entriesOnlyOnLeft(); // {"a" => 1}
diff.entriesOnlyOnRight(); // {"d" => 5}
```

##### `BiMap` 工具

`BiMap` 上的 Guava 实用程序位于 `Maps` 类中，因为 `BiMap` 也是 `Map`。

| `BiMap` utility                                              | Corresponding `Map` utility        |
| ------------------------------------------------------------ | ---------------------------------- |
| [`synchronizedBiMap(BiMap)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#synchronizedBiMap-com.google.common.collect.BiMap-) | `Collections.synchronizedMap(Map)` |
| [`unmodifiableBiMap(BiMap)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#unmodifiableBiMap-com.google.common.collect.BiMap-) | `Collections.unmodifiableMap(Map)` |

##### 静态工厂

`Maps` 提供了下列静态工厂方法。

| Implementation    | Factories                                                    |
| ----------------- | ------------------------------------------------------------ |
| `HashMap`         | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newHashMap--), [from `Map`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newHashMap-java.util.Map-), [with expected size](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newHashMapWithExpectedSize-int-) |
| `LinkedHashMap`   | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newLinkedHashMap--), [from `Map`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newLinkedHashMap-java.util.Map-) |
| `TreeMap`         | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newTreeMap--), [from `Comparator`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newTreeMap-java.util.Comparator-), [from `SortedMap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newTreeMap-java.util.SortedMap-) |
| `EnumMap`         | [from `Class`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newEnumMap-java.lang.Class-), [from `Map`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newEnumMap-java.util.Map-) |
| `ConcurrentMap`   | [basic](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Maps.html#newConcurrentMap--) |
| `IdentityHashMap` | [basic](                                                     |

#### Multisets

标准 `Collection` 操作，比如 `containsAll`，忽略 multiset 中的元素数目，而只关心元素是否存在于 multiset 中。 [`Multisets`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html) 提供了提供许多操作，这些操作考虑了 multiset 中元素的多重性。

| Method                                                       | Explanation                                                  | Difference from `Collection` method                          |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`containsOccurrences(Multiset sup, Multiset sub)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#containsOccurrences-com.google.common.collect.Multiset-com.google.common.collect.Multiset-) | 返回 `true` 如果 `sub.count(o) <= super.count(o)` 对所有 `o`。 | `Collection.containsAll`  忽略数目，仅仅测试元素是否包含在其中。 |
| [`removeOccurrences(Multiset removeFrom, Multiset toRemove)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#removeOccurrences-com.google.common.collect.Multiset-com.google.common.collect.Multiset-) | 对于 `toRemove` 中元素的每次出现，从 `removeFrom` 中移除一个出现。 | `Collection.removeAll` 移除任何出现在 `toRemove` 中的元素的所有出现。 |
| [`retainOccurrences(Multiset removeFrom, Multiset toRetain)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#retainOccurrences-com.google.common.collect.Multiset-com.google.common.collect.Multiset-) | 保证 `removeFrom.count(o) <= toRetain.count(o)` 对所有的 `o`。 | `Collection.retainAll` 保留任何在 `toRetain` 中出现过的元素的所有出现。 |
| [`intersection(Multiset, Multiset)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#intersection-com.google.common.collect.Multiset-com.google.common.collect.Multiset-) | 返回两个多集相交的视图，替代 `retainOccurrences` 的一种非破坏性方法。 | 没有类似物。                                                 |

```java
Multiset<String> multiset1 = HashMultiset.create();
multiset1.add("a", 2);

Multiset<String> multiset2 = HashMultiset.create();
multiset2.add("a", 5);

multiset1.containsAll(multiset2); // returns true: all unique elements are contained,
  // even though multiset1.count("a") == 2 < multiset2.count("a") == 5
Multisets.containsOccurrences(multiset1, multiset2); // returns false

multiset2.removeOccurrences(multiset1); // multiset2 now contains 3 occurrences of "a"

multiset2.removeAll(multiset1); // removes all occurrences of "a" from multiset2, even though multiset1.count("a") == 2
multiset2.isEmpty(); // returns true
```

 `Multisets` 中的其他工具包括：

| Method                                                       | Description                                                  |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| [`copyHighestCountFirst(Multiset)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#copyHighestCountFirst-com.google.common.collect.Multiset-) | 返回 multiset 的不可变副本，该副本以递减的频率顺序遍历元素。 |
| [`unmodifiableMultiset(Multiset)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#unmodifiableMultiset-com.google.common.collect.Multiset-) | 返回 multiset 的不可变视图。                                 |
| [`unmodifiableSortedMultiset(SortedMultiset)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multisets.html#unmodifiableSortedMultiset-com.google.common.collect.SortedMultiset-) | 返回排序 multiset 的不可变视图。                             |

```java
Multiset<String> multiset = HashMultiset.create();
multiset.add("a", 3);
multiset.add("b", 5);
multiset.add("c", 1);

ImmutableMultiset<String> highestCountFirst = Multisets.copyHighestCountFirst(multiset);

// highestCountFirst, like its entrySet and elementSet, iterates over the elements in order {"b", "a", "c"}
```

#### Multimaps

[`Multimaps`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html) 提供了大量通用的操作值得单独介绍。

#####  `index`

 `Maps.uniqueIndex` 的堂兄， [`Multimaps.index(Iterable, Function)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#index-java.lang.Iterable-com.google.common.base.Function-) 可以帮助您查找具有某些共同特定属性（不一定是唯一属性）的所有对象。

假设我们要根据字符串的长度对字符串进行分组。

```java
ImmutableSet<String> digits = ImmutableSet.of(
    "zero", "one", "two", "three", "four",
    "five", "six", "seven", "eight", "nine");
Function<String, Integer> lengthFunction = new Function<String, Integer>() {
  public Integer apply(String string) {
    return string.length();
  }
};
ImmutableListMultimap<Integer, String> digitsByLength = Multimaps.index(digits, lengthFunction);
/*
 * digitsByLength maps:
 *  3 => {"one", "two", "six"}
 *  4 => {"zero", "four", "five", "nine"}
 *  5 => {"three", "seven", "eight"}
 */
```

##### `invertFrom`

由于 `Multimap` 能够将多个键映射到同一个值，也可以将一个键映射到多个值，它对倒置 `Multimap` 操作非常有用。Guava 提供了 [`invertFrom(Multimap toInvert, Multimap dest)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#invertFrom-com.google.common.collect.Multimap-M-) 来帮助你做到这一点，而没有为你选择一个实现。

*注意*：如果你正在使用 `ImmutableMultimap`，考虑使用 [`ImmutableMultimap.inverse()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableMultimap.html#inverse--) 替代。

```java
ArrayListMultimap<String, Integer> multimap = ArrayListMultimap.create();
multimap.putAll("b", Ints.asList(2, 4, 6));
multimap.putAll("a", Ints.asList(4, 2, 1));
multimap.putAll("c", Ints.asList(2, 5, 3));

TreeMultimap<Integer, String> inverse = Multimaps.invertFrom(multimap, TreeMultimap.<String, Integer> create());
// note that we choose the implementation, so if we use a TreeMultimap, we get results in order
/*
 * inverse maps:
 *  1 => {"a"}
 *  2 => {"a", "b", "c"}
 *  3 => {"c"}
 *  4 => {"a", "b"}
 *  5 => {"c"}
 *  6 => {"b"}
 */
```

##### `forMap`

需要在 `Map` 上使用 `Multimap` 方法？[`forMap(Map)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#forMap-java.util.Map-) 将 `Map` 视作 `SetMultimap`。这非常有用，比如，与 `Multimaps.invertFrom` 结合使用：

```java
Map<String, Integer> map = ImmutableMap.of("a", 1, "b", 1, "c", 2);
SetMultimap<String, Integer> multimap = Multimaps.forMap(map);
// multimap maps ["a" => {1}, "b" => {1}, "c" => {2}]
Multimap<Integer, String> inverse = Multimaps.invertFrom(multimap, HashMultimap.<Integer, String> create());
// inverse maps [1 => {"a", "b"}, 2 => {"c"}]
```

##### Wrappers

`Multimaps` 提供了传统的包装器方法，以及根据您选择的 `Map` 和 `Collection` 实现获取自定义 `Multimap` 实现的工具。

| Multimap type       | Unmodifiable                                                 | Synchronized                                                 | Custom                                                       |
| ------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| `Multimap`          | [`unmodifiableMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#unmodifiableMultimap-com.google.common.collect.Multimap-) | [`synchronizedMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#synchronizedMultimap-com.google.common.collect.Multimap-) | [`newMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newMultimap-java.util.Map-com.google.common.base.Supplier-) |
| `ListMultimap`      | [`unmodifiableListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#unmodifiableListMultimap-com.google.common.collect.ListMultimap-) | [`synchronizedListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#synchronizedListMultimap-com.google.common.collect.ListMultimap-) | [`newListMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newListMultimap-java.util.Map-com.google.common.base.Supplier-) |
| `SetMultimap`       | [`unmodifiableSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#unmodifiableSetMultimap-com.google.common.collect.SetMultimap-) | [`synchronizedSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#synchronizedSetMultimap-com.google.common.collect.SetMultimap-) | [`newSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newSetMultimap-java.util.Map-com.google.common.base.Supplier-) |
| `SortedSetMultimap` | [`unmodifiableSortedSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#unmodifiableSortedSetMultimap-com.google.common.collect.SortedSetMultimap-) | [`synchronizedSortedSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#synchronizedSortedSetMultimap-com.google.common.collect.SortedSetMultimap-) | [`newSortedSetMultimap`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Multimaps.html#newSortedSetMultimap-java.util.Map-com.google.common.base.Supplier-) |

自定义的 `Multimap` 实现可让您指定应在返回的 `Multimap` 中使用的特定实现。注意事项包括：

- multimap 假定对图和工厂返回的列表拥有完全所有权。这些对象不应手动更新，提供时应为空，并且不应使用软引用，弱引用或虚引用。

- **不保证**修改 `Multimap` 后 `Map` 的内容是什么样。

- 当任何并发操作更新 multimap 时，即使 multimap 和工厂生成的实例一样，multimap 也不是线程安全的。但是，并发读取操作将正常运行。如有必要，使用 `synchronized` 包装器解决此问题。

- 如果 map，工厂，工厂生成的列表以及 multimap 内容都可序列化，则 multimap 可序列化。

- `Multimap.get(key)` 返回的集合与 `Supplier` 返回的集合的类型不相同，尽管如果供应商返回 `RandomAccess` 列表，则 `Multimap.get(key)` 也将是随机访问。

注意，自定义的 `Multimap` 方法期望一个 `Supplier` 参数来生成新的集合。这是一个编写由 `ListMap` 映射到 `LinkedList` 的 `ListMultimap` 的示例。

```java
ListMultimap<String, Integer> myMultimap = Multimaps.newListMultimap(
  Maps.<String, Collection<Integer>>newTreeMap(),
  new Supplier<LinkedList<Integer>>() {
    public LinkedList<Integer> get() {
      return Lists.newLinkedList();
    }
  });
```

#### Tables

 [`Tables`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html) 类提供了一些有用的工具。

##### `customTable`

相比于 `Multimaps.newXXXMultimap(Map, Supplier)` 工具， [`Tables.newCustomTable(Map, Supplier)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html#newCustomTable-java.util.Map-com.google.common.base.Supplier-) 允许你指定一个 `Table` 实现，可以选择使用行或者列映射。

```java
// use LinkedHashMaps instead of HashMaps
Table<String, Character, Integer> table = Tables.newCustomTable(
  Maps.<String, Map<Character, Integer>>newLinkedHashMap(),
  new Supplier<Map<Character, Integer>> () {
    public Map<Character, Integer> get() {
      return Maps.newLinkedHashMap();
    }
  });
```

##### `transpose`

 [`transpose(Table)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html#transpose-com.google.common.collect.Table-) 方法允许你将 `Table<R, C, V>` 视作 `Table<C, R, V>`。

##### Wrappers

这些是您熟悉和喜爱的不可修改的包装器。不过，在大多数情况下，请考虑使用 [`ImmutableTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/ImmutableTable.html)。

- [`unmodifiableTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html#unmodifiableTable-com.google.common.collect.Table-)
- [`unmodifiableRowSortedTable`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/collect/Tables.html#unmodifiableRowSortedTable-com.google.common.collect.RowSortedTable-)

### 集合扩展工具

#### 介绍

有时您需要编写自己的集合扩展。也许您希望在将元素添加到列表中时添加特殊的行为，或者想要编写实际上由数据库查询支持的 `Iterable`。Guava 提供了许多实用程序，可以使您和我们都更轻松地完成这些任务。（毕竟，我们自己就在从事扩展集合框架的工作。）

#### 转发装饰器

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

#### PeekingIterator

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

#### AbstractIterator

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

#### AbstractSequentialIterator

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

## 缓存

### 示例

```java
LoadingCache<Key, Graph> graphs = CacheBuilder.newBuilder()
       .maximumSize(1000)
       .expireAfterWrite(10, TimeUnit.MINUTES)
       .removalListener(MY_LISTENER)
       .build(
           new CacheLoader<Key, Graph>() {
             @Override
             public Graph load(Key key) throws AnyException {
               return createExpensiveGraph(key);
             }
           });
```

### 适用性

缓存有非常广泛的应用场景。比如，你应该为那些计算或者查询代价高昂的数据使用缓存，或者你需要某个输入数据很多次的场景。

一个 `Cache` 类似于 `ConcurrentMap`，不过并不完全相同。基本的差异在于， `ConcurrentMap` 持久化所有添加进来的元素直到它们被显式删除。另一方面，通常将 `Cache` 配置为自动淘汰条目，以限制其内存占用量。在某些情况下， `LoadingCache` 会很有用，虽然它不淘汰条目，但是可以自动加载缓存。

通常，Guava 缓存工具可以适用与下列场景：

- 你希望使用一些内存空间来改善速度。
- 您希望多次查询某些键。
- 您的缓存将不需要存储超出 RAM 容量的数据。（Guava 缓存的作用范围局限于在应用程序的一次运行中。它们不将数据存储在文件中或外部服务器上。如果这不符合您的需求，请考虑使用 [Memcached](http://memcached.org/)。）

如果这些都适用于您的应用场景，那么 Guava 缓存实用程序将很适合您！

如上面的示例代码所示，使用 `CacheBuilder` 生成器模式可以获取 `Cache`，但是自定义缓存是有趣的部分。

*注意：* 如果不需要 `Cache` 的功能，则 `ConcurrentHashMap` 的内存使用效率更高——但是很难用任何旧的 `ConcurrentMap`来复制大多数 `Cache` 的功能。

### 填充

你需要问自己有关缓存的第一个问题是：是否有一些*合理的默认*函数来加载或计算与键关联的值？如果是这样，您应该使用 `CacheLoader`。如果不是这样，或者如果您需要覆盖默认值，但是仍然需要原子的 "get-if-absent-compute" 语义，则应该将 `Callable` 传递给 `get` 调用。可以使用 `Cache.put` 直接插入元素，但是首选自动加载缓存，因为这样可以更轻松地推断所有缓存内容的一致性。

#### 使用 CacheLoader

 `LoadingCache` 是一个通过附属的 [`CacheLoader`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheLoader.html) 构建的 `Cache`。创建一个 `CacheLoader` 通常与实现 `V load(K key) throws Exception` 方法一样。因此，比如，你可以使用下面的代码创建一个 `LoadingCache` ：

```java
LoadingCache<Key, Graph> graphs = CacheBuilder.newBuilder()
       .maximumSize(1000)
       .build(
           new CacheLoader<Key, Graph>() {
             public Graph load(Key key) throws AnyException {
               return createExpensiveGraph(key);
             }
           });

...
try {
  return graphs.get(key);
} catch (ExecutionException e) {
  throw new OtherException(e.getCause());
}
```

查询 `LoadingCache` 的规范方法是使用 [`get(K)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/LoadingCache.html#get-K-) 方法。这将返回一个已经缓存的值，或者使用缓存的 `CacheLoader` 原子地将新值加载到缓存中。由于 `CacheLoader` 可能会抛出 `Exception`，因此 `LoadingCache.get(K)` 会抛出 `ExecutionException`。（如果缓存加载器抛出 *unchecked* 异常，则`get(K)` 会引发包装了 `UncheckedExecutionException` 的异常。）您还可以选择使用 `getUnchecked(K)` 将所有异常包装在 `UncheckedExecutionException` 中， 但是如果底层的 `CacheLoader` 通常会抛出受检查异常，这可能会导致令人惊讶的行为。

```java
LoadingCache<Key, Graph> graphs = CacheBuilder.newBuilder()
       .expireAfterAccess(10, TimeUnit.MINUTES)
       .build(
           new CacheLoader<Key, Graph>() {
             public Graph load(Key key) { // no checked exception
               return createExpensiveGraph(key);
             }
           });

...
return graphs.getUnchecked(key);
```

可以使用 `getAll(Iterable<? extends K>)` 方法执行批量查找。默认情况下，`getAll` 将为缓存中不存在的每个键单独发出 `CacheLoader.load` 调用。如果批量检索比许多单个查询更有效，则可以覆盖 [`CacheLoader.loadAll`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheLoader.html#loadAll-java.lang.Iterable-) 来利用这一点。 `getAll(Iterable)` 的性能将相应提高。

请注意，您可以编写一个 `CacheLoader.loadAll` 实现，该实现加载未明确要求的键的值。例如，如果计算某个组中任何键的值给您该组中所有键的值，则 `loadAll` 可能会同时加载其余组。

#### 使用 Callable

所有 Guava 缓存（无论是否加载）均支持方法 [`get(K, Callable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#get-java.lang.Object-java.util.concurrent.Callable-) 。此方法返回与缓存中的键关联的值，或从指定的 `Callable` 中计算出该值并将其添加到缓存中。在加载完成之前，不会修改与此缓存关联的可观察状态。此方法为常规的“如果已缓存，则返回；否则创建，缓存并返回”模式提供了简单的替代方法。

```java
Cache<Key, Value> cache = CacheBuilder.newBuilder()
    .maximumSize(1000)
    .build(); // look Ma, no CacheLoader
...
try {
  // If the key wasn't in the "easy to compute" group, we need to
  // do things the hard way.
  cache.get(key, new Callable<Value>() {
    @Override
    public Value call() throws AnyException {
      return doThingsTheHardWay(key);
    }
  });
} catch (ExecutionException e) {
  throw new OtherException(e.getCause());
}
```

#### 直接插入

可以直接使用 [`cache.put(key, value)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#put-K-V-) 。这将覆盖高速缓存中指定键的任何先前条目。也可以使用  `Cache.asMap()` 视图公开的任何 `ConcurrentMap` 方法对缓存进行更改。注意，`asMap` 视图上的任何方法都不会导致条目自动加载到缓存中。此外，该视图上的原子操作在自动缓存加载范围之外运行，因此在使用 `CacheLoader` 或 `Callable` 加载值的缓存中，始终应优先选择 `Cache.get(K, Callable<V>)` 而不是 `Cache.asMap().putIfAbsent` 。

### 驱逐

冷酷的现实是，我们几乎*肯定*没有足够的内存来缓存我们可以缓存的所有内容。您必须决定：什么时候不值得保留缓存条目？Guava 提供三种基本的驱逐类型：基于大小的驱逐，基于时间的驱逐和基于引用的驱逐。

#### 基于大小的驱逐

如果你的缓存在达到某个大小之后就不应该继续增长，可以使用 [`CacheBuilder.maximumSize(long)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#maximumSize-long-)。缓存将会尝试驱逐最近最少使用的缓存数据实体。*警告*：缓存可能会在大小达到限制之前驱逐实体——通常是在缓存大小接近限制时。

另外，如果不同的缓存实体具有不同的“权重”——比如，如果你的缓存值具有不同的内存空间占用——你可以使用 [`CacheBuilder.weigher(Weigher)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#weigher-com.google.common.cache.Weigher-) 指定权重函数，同时使用 [`CacheBuilder.maximumWeight(long)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#maximumWeight-long-) 指定最大缓存权重。除了需要与 `maximumSize` 相同的限制外，请注意，权重是在条目创建时计算的，此后是静态的。

```java
LoadingCache<Key, Graph> graphs = CacheBuilder.newBuilder()
       .maximumWeight(100000)
       .weigher(new Weigher<Key, Graph>() {
          public int weigh(Key k, Graph g) {
            return g.vertices().size();
          }
        })
       .build(
           new CacheLoader<Key, Graph>() {
             public Graph load(Key key) { // no checked exception
               return createExpensiveGraph(key);
             }
           });
```

#### 基于时间的驱逐

`CacheBuilder` 提供了两种基于时间的驱逐方法：

- [`expireAfterAccess(long, TimeUnit)`](https://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#expireAfterAccess-long-java.util.concurrent.TimeUnit-) 仅在自从上次通过读取或写入访问条目以来经过指定的持续时间后，条目才到期。请注意，驱逐条目的顺序将类似于 [基于大小的驱逐](https://github.com/google/guava/wiki/CachesExplained#Size-based-Eviction)。
- [`expireAfterWrite(long, TimeUnit)`](https://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#expireAfterWrite-long-java.util.concurrent.TimeUnit-) 自创建条目以来经过指定的时间或该值的最新替换之后，使条目过期。如果经过一定时间后缓存的数据持续增长，则可能需要这样做。

定时到期是在写入过程中进行定期维护的，偶尔在读取过程中进行维护，如下所述。

##### 测试定时驱逐

测试定时驱逐并不一定会很痛苦...实际上也不需要花两秒钟来测试两秒钟的到期时间。使用 [Ticker](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Ticker.html) 接口和 [`CacheBuilder.ticker(Ticker)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#ticker-com.google.common.base.Ticker-) 方法来指定缓存构建器中的时间源，而不必等待系统时钟。

#### 基于引用的驱逐

Guava 允许你设置你的缓存以允许数据实体的垃圾收集，通过对键或者值使用的 [weak references](http://docs.oracle.com/javase/6/docs/api/java/lang/ref/WeakReference.html) ，或者对值使用的 [soft references](http://docs.oracle.com/javase/6/docs/api/java/lang/ref/SoftReference.html) 进行设置。

- [`CacheBuilder.weakKeys()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#weakKeys--) 使用弱引用存储键。这允许实体在没有其他引用（强引用或者软引用）指向其键时被垃圾收集。由于垃圾收集基于 id 相等规则，这就导致整个缓存多需要使用 id （`==`）相等来比较键，而不是使用 `equals()`。
- [`CacheBuilder.weakValues()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#weakValues--) 使用弱引用存储值。这允许实体在没有其他引用（强引用或者软引用）指向其值时被垃圾收集。由于垃圾收集基于 id 相等规则，这就导致整个缓存多需要使用 id （`==`）相等来比较值，而不是使用 `equals()`。
- [`CacheBuilder.softValues()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#softValues--) 将值包装进入软引用。软引用对象以全局最近最少使用规则进行垃圾收集，以响应内存需求。由于使用软引用可能会有些性能问题，我们通常推荐使用更加容易预测的 [maximum cache size](https://github.com/google/guava/wiki/CachesExplained#Size-based-Eviction) 替代。使用 `softValues()` 将导致值被通过 id (`==`) 相等比较，而不是使用 `equals()`。

### 显式删除

任何时刻，你都可以显式废除缓存实体，而不需要等待实体被驱逐。可以通过以下方法：

- 单个废除，使用 [`Cache.invalidate(key)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#invalidate-java.lang.Object-)
- 批量废除，使用 [`Cache.invalidateAll(keys)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#invalidateAll-java.lang.Iterable-)
- 全部废除，使用 [`Cache.invalidateAll()`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/Cache.html#invalidateAll--)

### 删除监听器

你可以为你的缓存指定删除监听器以在实体被删除时执行一些操作，通过 [`CacheBuilder.removalListener(RemovalListener)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/CacheBuilder.html#removalListener-com.google.common.cache.RemovalListener-)。 [`RemovalListener`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/RemovalListener.html) 传递了一个 [`RemovalNotification`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/RemovalNotification.html)，指定了 [`RemovalCause`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/RemovalCause.html)，键，和值。

注意， `RemovalListener` 抛出的所有异常都会被写入日志 (使用 `Logger`) 并被吞掉。

```java
CacheLoader<Key, DatabaseConnection> loader = new CacheLoader<Key, DatabaseConnection> () {
  public DatabaseConnection load(Key key) throws Exception {
    return openConnection(key);
  }
};
RemovalListener<Key, DatabaseConnection> removalListener = new RemovalListener<Key, DatabaseConnection>() {
  public void onRemoval(RemovalNotification<Key, DatabaseConnection> removal) {
    DatabaseConnection conn = removal.getValue();
    conn.close(); // tear down properly
  }
};

return CacheBuilder.newBuilder()
  .expireAfterWrite(2, TimeUnit.MINUTES)
  .removalListener(removalListener)
  .build(loader);
```

**警告**：默认情况下，删除侦听器操作是同步执行的，并且由于缓存维护通常是在常规缓存操作期间执行的，因此耗时的删除侦听器会降低正常的缓存功能！如果您有耗时的删除监听器，请使用 [`RemovalListeners.asynchronous(RemovalListener, Executor)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/cache/RemovalListeners.html#asynchronous-com.google.common.cache.RemovalListener-java.util.concurrent.Executor-) 来装饰 `RemovalListener` 以进行异步操作。

