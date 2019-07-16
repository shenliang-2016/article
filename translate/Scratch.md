### 定制化 Resource Bundle 加载

在本课程的前面部分，您学习了如何创建和访问`ResourceBundle`类的对象。本节将扩展您的知识并解释如何从`ResourceBundle.Control`类功能中获益。

创建`ResourceBundle.Control`以指定如何查找和实例化资源包。它定义了一组回调方法，这些方法在资源包加载过程中由`ResourceBundle.getBundle`工厂方法调用。

与前面描述的`ResourceBundle.getBundle`方法不同，此`ResourceBundle.getBundle`方法使用指定的基本名称，默认语言环境和指定的控件定义资源包。

```java
public static final ResourceBundle getBundle(
    String baseName,
    ResourceBundle.Control cont
    // ...
```

指定的控件提供资源包加载过程的信息。

以下示例程序`RBControl.java`说明了如何为中文语言环境定义自己的搜索路径。

**1. 创建 `properties` 文件**

如前所述，您可以从类或属性文件加载资源。 这些文件包含以下语言环境的说明：

- `RBControl.properties` – 全局
- `RBControl_zh.properties` – 只用于语言：简体中文
- `RBControl_zh_cn.properties` – 只用于区域：中国
- `RBControl_zh_hk.properties` – 只用于区域：香港
- `RBControl_zh_tw.properties` – 台湾

在此示例中，应用程序为香港地区创建新的区域设置。

**2. 创建 `ResourceBundle` 实例**

与上一节中的示例一样，此应用程序通过调用`getBundle`方法创建`ResourceBundle`实例：

```java
private static void test(Locale locale) {
    ResourceBundle rb = ResourceBundle.getBundle(
                            "RBControl",
                            locale,
                            new ResourceBundle.Control() {
                                    // ...
                            }
                        );
```

`getBundle`方法使用`RBControl`前缀搜索属性文件。但是，此方法包含`Control`参数，该参数驱动搜索`Chineese`区域设置的过程。

**3. 调用 `getCandidateLocales` 方法**

`getCandidateLocales`方法返回`Locales`对象的列表，作为基本名称和语言环境的候选语言环境。

```java
new ResourceBundle.Control() {
    @Override
    public List<Locale> getCandidateLocales(
                            String baseName,
                            Locale locale) {
                // ...                                        
    }
}
```

默认实现返回`Locale`对象的列表，如下所示：`Locale(language, country)` 。

但是，重写此方法以实现以下特定行为：

```java
if (baseName == null)
    throw new NullPointerException();

if (locale.equals(new Locale("zh", "HK"))) {
    return Arrays.asList(
               locale,
               Locale.TAIWAN,
               // no Locale.CHINESE here
               Locale.ROOT);
} else if (locale.equals(Locale.TAIWAN)) {
    return Arrays.asList(
               locale,
               // no Locale.CHINESE here
               Locale.ROOT);
}
```

请注意，候选语言环境序列的最后一个元素必须是根区域设置。

**4. 调用 `test` 类**

为下面4个不同的区域调用`test`类：

```java
public static void main(String[] args) {
    test(Locale.CHINA);
    test(new Locale("zh", "HK"));
    test(Locale.TAIWAN);
    test(Locale.CANADA);
}
```

**5. 运行示例程序**

你将看到程序输出如下：

```
locale: zh_CN
        region: China
        language: Simplified Chinese
locale: zh_HK
        region: Hong Kong
        language: Traditional Chinese
locale: zh_TW
        region: Taiwan
        language: Traditional Chinese
locale: en_CA
        region: global
        language: English
```

请注意，新创建的分配了香港地区，因为它是在相应的属性文件中指定的。繁体中文被指定为台湾语言。

在`RBControl`示例中没有使用`ResourceBundle.Control`类的另外两个有趣的方法，但它们值得提及。`getTimeToLive`方法用于确定资源包在缓存中可以存在多长时间。如果缓存中资源包的时间限制已过期，则调用`needsReload`方法以确定是否需要重新加载资源包。

