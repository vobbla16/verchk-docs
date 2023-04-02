---
title: 扫描的新服务
type: docs
---

## 抽象类的实现
*要了解什么是`Resource<T>`类型，请参见[本文]({{< relref "resource" >}})*。

要添加一个新的扫描服务，你必须首先实现抽象类`TargetSystem`。它看起来像这样：
```kotlin
abstract class TargetSystem (
    /**
     * URL to analyze
     */
    val url: String
) {
    /**
     * Target name
     */
    abstract val targetName: String

    /**
     * NVD CPE name
     */
    abstract val cpe: String

    /**
     * Check is the url matches this target
     * @return is url matches target
     */
    abstract suspend fun check(): Resource<Boolean>

    /**
     * Get target's version
     * @return target's version presented as String
     */
    abstract suspend fun version(): Resource<String>
}
```

- `targetName`字段是工具输出中使用的名称。
- `cpe`字段是基本CPE，该版本将被插入其中，用它来创建对国家漏洞数据库API的请求。
- `check`方法 - 必须返回`true`或`false`，取决于服务是否安装在指定的URL上。
- `version`方法 - 必须返回适合在CPE中替换的字符串表示的版本。


## 添加你的扩展
在创建一个实现后，你需要将其添加到所有扩展的列表中。要做到这一点，你需要在`getAllTargets()`函数返回的列表中添加一个类引用（它位于`getAllTargets.kt`文件中）

例子：
```kotlin
fun getAllTargets(): List<KClass<*>> {
    return listOf(
        ConfluenceTargetImpl::class,
        GrafanaTargetImpl::class
    )
}
```
