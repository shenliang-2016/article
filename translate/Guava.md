# Googel Guava User Guide

https://github.com/google/guava/wiki

Joshua O'Madadhain edited this page on 25 Oct 2016 · [5 revisions](https://github.com/google/guava/wiki/Home/_history)

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

Catching and rethrowing an exception is straightforward when dealing with only one kind of exception. Where it gets messy is when dealing with multiple kinds of exceptions:

```
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

Java 7 solves this problem with [multicatch](http://docs.oracle.com/javase/7/docs/technotes/guides/language/catch-multiple.html):

```
} catch (RuntimeException | Error e) {
  failures.increment();
  throw e;
}
```

Non-Java 7 users are stuck. They'd like to write code like the following, but the compiler won't permit them to throw a variable of type `Throwable`:

```
} catch (Throwable t) {
  failures.increment();
  throw t;
}
```

The solution is to replace `throw t` with `throw Throwables.propagate(t)`. In this limited circumstance, `Throwables.propagate` behaves identically to the original code. However, it's easy to write code with `Throwables.propagate` that has other, hidden behavior. In particular, note that the above pattern works only with `RuntimeException` and `Error`. If the `catch` block may catch checked exceptions, you'll also need some calls to `propagateIfInstanceOf` in order to preserve behavior, as `Throwables.propagate` can't directly propagate a checked exception.

Overall, this use of `propagate` is so-so. It's unnecessary under Java 7. Under other versions, it saves a small amount of duplication, but so could a simple Extract Method refactoring. Additionally, use of `propagate` [makes it easy to accidentally wrap checked exceptions](https://github.com/google/guava/commit/287bc67cac97052b13cbbc0358aed8054b14bd4a).

##### Unnecessary: Converting from "throws Throwable" to "throws Exception"

A few APIs, notably the Java reflection API and (as a result) JUnit, declare methods that throw `Throwable`. Interacting with these APIs can be a pain, as even the most general-purpose APIs typically only declare `throws Exception`. `Throwables.propagate` is used by some callers who know they have a non-`Exception`, non-`Error` `Throwable`. Here's an example of declaring a `Callable` that executes a JUnit test:

```
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

There's no need for `propagate()` here, as the second line is equivalent to `throw new RuntimeException(t)`. (Digression: This example also reminds me that `propagateIfPossible` is potentially confusing, since it propagates not just arguments of the given type but also `Errors` and `RuntimeExceptions`.)

This pattern (or similar variants like `throw new RuntimeException(t)`) shows up ~30 times in Google's codebase. (Search for `'propagateIfPossible[^;]* Exception.class[)];'`.) A slight majority of them take the explicit `throw new RuntimeException(t)` approach. It's possible that we would want a `throwWrappingWeirdThrowable` method for `Throwable`-to-`Exception` conversions, but given the two-line alternative, there's probably not much need unless we were to also deprecate `propagateIfPossible`.

#### Controversial uses for `Throwables.propagate`

##### Controversial: Converting checked exceptions to unchecked exceptions

In principle, unchecked exceptions indicate bugs, and checked exceptions indicate problems outside your control. In practice, even the JDK sometimes [gets](http://docs.oracle.com/javase/6/docs/api/java/lang/Object.html#clone()) [it](http://docs.oracle.com/javase/6/docs/api/java/lang/Integer.html#parseInt(java.lang.String)) [wrong](http://docs.oracle.com/javase/6/docs/api/java/net/URI.html#URI(java.lang.String)) (or at least, for some methods, [no answer is right for everyone](http://docs.oracle.com/javase/6/docs/api/java/net/URI.html#create(java.lang.String))).

As a result, callers occasionally have to translate between exception types:

```
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

Sometimes, those callers use `Throwables.propagate`. What are the disadvantages?

The main one is that the meaning of the code is less obvious. What does `throw Throwables.propagate(ioException)` do? What does `throw new RuntimeException(ioException)` do? The two do the same thing, but the latter is more straightforward. The former raises questions: "What does this do? It isn't just wrapping in `RuntimeException`, is it? If it were, why would they write a method wrapper?"

Part of the problem here, admittedly, is that "propagate" is a vague name. (Is it [a way of throwing undeclared exceptions](http://www.eishay.com/2011/11/throw-undeclared-checked-exception-in.html)?) Perhaps "wrapIfChecked" would have worked better. Even if the method were called that, though, there would be no advantage to calling it on a known checked exception. There may even be additional downsides: Perhaps there's a more suitable type than a plain `RuntimeException` for you to throw -- say, `IllegalArgumentException`.

We sometimes also see `propagate` used when the exception only *might* be a checked exception. The result is slightly smaller and slightly less straightforward than the alternative:

```
} catch (RuntimeException e) {
  throw e;
} catch (Exception e) {
  throw new RuntimeException(e);
}
} catch (Exception e) {
  throw Throwables.propagate(e);
}
```

However, the elephant in the room here is the general practice of converting checked exceptions to unchecked exceptions. It is unquestionably the right thing in some cases, but more frequently it's used to avoid dealing with a legitimate checked exception. This leads us to the debate over whether checked exceptions are bad idea in general. I don't wish to go into all that here. Suffice it to say that `Throwables.propagate` does not exist for the purpose of encouraging Java users to ignore `IOException` and the like.

##### Controversial: Exception tunneling

But what about when you're implementing a method that isn't allowed to throw exceptions? Sometimes you need to wrap your exception in an unchecked exception. This is fine, but again, `propagate` is unnecessary for simple wrapping. In fact, manual wrapping may be preferable: If you wrap *every* exception (instead of just checked exceptions), then you can unwrap every exception on the other end, making for fewer special cases. Additionally, you may wish to use a custom exception type for the wrapping.

##### Controversial: Rethrowing exceptions from other threads

```
try {
  return future.get();
} catch (ExecutionException e) {
  throw Throwables.propagate(e.getCause());
}
```

There are multiple things to consider here:

1. The cause may be a checked exception. See "Converting checked exceptions to unchecked exceptions" above. But what if the task is known not to throw a checked exception? (Maybe it's the result of a `Runnable`.) As discussed above, you can catch the exception and throw `AssertionError`; `propagate` has little more to offer. For `Future` in particular, also consider [`Futures.get`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/util/concurrent/Futures.html#getUnchecked-java.util.concurrent.Future-).
2. The cause may be a non-`Exception`, non-`Error` `Throwable`. (Well, it's unlikely to actually be one, but the compiler would force you to consider the possibility if you tried to rethrow it directly.) See "Converting from `throws Throwable` to `throws Exception`" above.
3. The cause may be an unchecked exception or error. If so, it will be rethrown directly. Unfortunately, its stack trace will reflect the thread in which the exception was originally created, not the thread in which it is currently propagating. It's typically best to have include both threads' stack traces available in the exception chain, as in the `ExecutionException` thrown by `get`. (This problem isn't really about `propagate`; it's about any code that rethrows an exception in a different thread.)

#### Causal Chain

Guava makes it somewhat simpler to study the causal chain of an exception, providing three useful methods whose signatures are self-explanatory:

- [`Throwable getRootCause(Throwable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#getRootCause-java.lang.Throwable-)
- [`List getCausalChain(Throwable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#getCausalChain-java.lang.Throwable-)
- [`String getStackTraceAsString(Throwable)`](http://google.github.io/guava/releases/snapshot/api/docs/com/google/common/base/Throwables.html#getStackTraceAsString-java.lang.Throwable-)