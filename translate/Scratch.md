## 隔离特定于语言的数据

必须根据最终用户的语言和区域的惯例来定制特定于语言环境的数据。用户界面显示的文本是区域设置特定数据的最明显示例。例如，在美国使用“Cancel”按钮的应用程序将在德国具有“Abbrechen”按钮。在其他国家/地区，此按钮将包含其他标签。显然你不想硬编码这个按钮标签。如果你能自动为给定的`Locale`获取正确的标签，那不是很好吗？幸运的是，只要您在`ResourceBundle`中隔离特定于语言环境的对象，就可以。

在本课程中，您将学习如何创建和访问`ResourceBundle`对象。如果您急于查看一些编码示例，请继续查看本课程的最后两节。然后，您可以回到前两个部分以获取有关`ResourceBundle`对象的一些概念性信息。

[关于 ResourceBundle 类](https://docs.oracle.com/javase/tutorial/i18n/resbundle/concept.html)

`ResourceBundle`对象包含特定于语言环境的对象。当您需要特定于语言环境的对象时，可以从`ResourceBundle`获取它，该`ResourceBundle`返回与最终用户的`Locale`匹配的对象。本节介绍`ResourceBundle`如何与`Locale`相关，并描述`ResourceBundle`子类。

[准备使用 ResourceBundle](https://docs.oracle.com/javase/tutorial/i18n/resbundle/prepare.html)

在创建`ResourceBundle`对象之前，您应该做一些计划。首先，确定程序中特定于语言环境的对象。然后将它们组织成类别并相应地将它们存储在不同的`ResourceBundle`对象中。

[用属性文件作为 ResourceBundle 的后备](https://docs.oracle.com/javase/tutorial/i18n/resbundle/propfile.html)

如果您的应用程序包含需要翻译成各种语言的`String`对象，则可以将这些`String`对象存储在`PropertyResourceBundle`中，该对象由一组属性文件备份。由于属性文件是简单的文本文件，因此翻译人员可以创建和维护这些文件。您不必更改源代码。在本节中，您将学习如何设置备份`PropertyResourceBundle`的属性文件。

[使用 ListResourceBundle](https://docs.oracle.com/javase/tutorial/i18n/resbundle/list.html)

`ListResourceBundle`类是`ResourceBundle`的子类，它使用列表管理特定于语言环境的对象。`ListResourceBundle`由类文件支持，这意味着每次需要支持其他语言环境时，您必须编写和编译新的源文件。但是，`ListResourceBundle`对象很有用，因为与属性文件不同，它们可以存储任何类型的特定于语言环境的对象。通过单步执行示例程序，本节演示了如何使用`ListResourceBundle`。

[自定义 Resource Bundle 加载](https://docs.oracle.com/javase/tutorial/i18n/resbundle/control.html)

本节介绍了改进`ResourceBundle.getBundle`工厂灵活性的新功能。`ResourceBundle.Control`类与用于加载资源包的工厂方法协作。这允许将资源包加载过程的每个步骤及其高速缓存控制视为单独的方法。

