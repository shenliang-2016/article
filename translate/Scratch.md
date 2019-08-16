#### 获取和设定字段值

给定一个类的实例，可以使用反射来设置该类中的字段值。这通常仅在特殊情况下才能使用，比如当不可能以通常方式设置值时。由于此类访问通常违反了该类的设计意图，因此应谨慎使用。

[`Book`](https://docs.oracle.com/javase/tutorial/reflect/member/example/Book.java) 类说明了如何设置`long`，`array`和`enum`类型字段的值。获取和设置其他基本数据类型的方法在[`Field`](https://docs.oracle.com/javase/8/docs/api/java/lang/reflect/Field.html#method_summary) 中描述。

```java
import java.lang.reflect.Field;
import java.util.Arrays;
import static java.lang.System.out;

enum Tweedle { DEE, DUM }

public class Book {
    public long chapters = 0;
    public String[] characters = { "Alice", "White Rabbit" };
    public Tweedle twin = Tweedle.DEE;

    public static void main(String... args) {
	Book book = new Book();
	String fmt = "%6S:  %-12s = %s%n";

	try {
	    Class<?> c = book.getClass();

	    Field chap = c.getDeclaredField("chapters");
	    out.format(fmt, "before", "chapters", book.chapters);
  	    chap.setLong(book, 12);
	    out.format(fmt, "after", "chapters", chap.getLong(book));

	    Field chars = c.getDeclaredField("characters");
	    out.format(fmt, "before", "characters",
		       Arrays.asList(book.characters));
	    String[] newChars = { "Queen", "King" };
	    chars.set(book, newChars);
	    out.format(fmt, "after", "characters",
		       Arrays.asList(book.characters));

	    Field t = c.getDeclaredField("twin");
	    out.format(fmt, "before", "twin", book.twin);
	    t.set(book, Tweedle.DUM);
	    out.format(fmt, "after", "twin", t.get(book));

        // production code should handle these exceptions more gracefully
	} catch (NoSuchFieldException x) {
	    x.printStackTrace();
	} catch (IllegalAccessException x) {
	    x.printStackTrace();
	}
    }
}
```

输出如下：

$ *java Book*

```
BEFORE:  chapters     = 0
 AFTER:  chapters     = 12
BEFORE:  characters   = [Alice, White Rabbit]
 AFTER:  characters   = [Queen, King]
BEFORE:  twin         = DEE
 AFTER:  twin         = DUM
```

------

注意：

通过反射设置字段值会产生一定的性能开销，因为必须进行很多额外操作，例如验证访问权限。从运行时的角度来看，效果是相同的，并且操作是原子的，就像在类代码中直接更改了值一样。

使用反射可能会导致某些运行时优化丢失。例如，以下代码很可能由Java虚拟机优化：

```java
int x = 1;
x = 2;
x = 3;
```

使用 `Field.set*()` 的等效代码就可能不会被虚拟机优化。

----

