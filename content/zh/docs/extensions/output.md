---
title: 新的输出格式
type: docs
---

大多数数据的输出是一个 "表"，可以以各种格式输出。

## 步骤1. 实现抽象类 "OutputInterface"。
在`OutputInterface`中，已经包含了添加 "头 "和 "列 "的逻辑，只需要实现抽象函数`build()`。

该类包含一个`headersInt`标题列表和一个`linesInt`"表 "列的二维数组。

实施例子：
```kotlin
class CSVOutputImpl : OutputInterface() {
    override fun build(): String {
        val r = mutableListOf(headersInt.joinToString(","))
        r += linesInt.map { it.joinToString(",") }
        return r.joinToString("\n")
    }
}
```


## 第二步。添加你的实现
在创建了 "OutputInterface "实现后，你需要将其添加到 "Outputs "枚举中（位于 "output/Outputs.kt "文件）。

枚举元素由2个字段组成：
- 一个简短的名字，用户将通过它来选择输出格式
- 对 "OutputInterface "实现的引用

例子：
```kotlin
enum class Outputs(
    val optionName: String,
    val outputClass: OutputClass
) {
    ConsTableOutput("console", ConsTableOutputImpl::class),
    CSVOutput("csv", CSVOutputImpl::class);
....
```
