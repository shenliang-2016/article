#### 修改日期格式化符号

----

**版本提示：**本节使用`java.util`包中的日期和时间 APIs。`java.time` APIs，在 JDK 8 版本中可用，提供了一个全面的日期和时间模型，相对于`java.util`中的类有了巨大的改进。`java.time` APIs 在 [Date Time](https://docs.oracle.com/javase/tutorial/datetime/index.html) 中描述。[Legacy Date-Time Code](https://docs.oracle.com/javase/tutorial/datetime/iso/legacy.html) 页面内容可能也有一定参考价值。

----

`SimpleDateFormat`类的`format`方法返回一个由数字和符号组成的`String`。比如，在`String`“Friday, April 10,2009”中，“Friday”和"April"就是符号。如果`SimpleDateFormat`中包含的符号不符合你的需求，你可以使用 [`DateFormatSymbols`](https://docs.oracle.com/javase/8/docs/api/java/text/DateFormatSymbols.html) 修改这些符号。下表列出了`DateFormatSymbols`方法允许你修改这些符号：

| Setter Method      | Example of a Symbol the Method Modifies |
| ------------------ | --------------------------------------- |
| `setAmPmStrings`   | PM                                      |
| `setEras`          | AD                                      |
| `setMonths`        | December                                |
| `setShortMonths`   | Dec                                     |
| `setShortWeekdays` | Tue                                     |
| `setWeekdays`      | Tuesday                                 |
| `setZoneStrings`   | PST                                     |

以下示例调用`setShortWeekdays`将星期几的短名称从小写字符更改为大写字符。此示例的完整源代码位于  [`DateFormatSymbolsDemo`](https://docs.oracle.com/javase/tutorial/i18n/format/examples/DateFormatSymbolsDemo.java) 中。`setShortWeekdays`的数组参数中的第一个元素是空`String`。因此，数组下标是从 1 开始的。`SimpleDateFormat`构造函数接受修改后的`DateFormatSymbols`对象作为参数。这是源代码：

```java
Date today;
String result;
SimpleDateFormat formatter;
DateFormatSymbols symbols;
String[] defaultDays;
String[] modifiedDays;

symbols = new DateFormatSymbols( new Locale("en", "US"));
defaultDays = symbols.getShortWeekdays();

for (int i = 0; i < defaultDays.length; i++) {
    System.out.print(defaultDays[i] + " ");
}
System.out.println();

String[] capitalDays = {
    "", "SUN", "MON",
    "TUE", "WED", "THU",
    "FRI", "SAT"
};
symbols.setShortWeekdays(capitalDays);

modifiedDays = symbols.getShortWeekdays();
for (int i = 0; i < modifiedDays.length; i++) {
    System.out.print(modifiedDays[i] + " ");
}
System.out.println();
System.out.println();

formatter = new SimpleDateFormat("E", symbols);
today = new Date();
result = formatter.format(today);
System.out.println("Today's day of the week: " + result);

```

上面的代码产生如下输出：

```
 Sun Mon Tue Wed Thu Fri Sat 
 SUN MON TUE WED THU FRI SAT 

Today's day of the week: MON
```