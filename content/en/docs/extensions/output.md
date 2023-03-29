---
title: New output formats
type: docs
---

The output of most data is a "table" that can be output in a variety of formats.

## Step 1. Implementing the abstract class `OutputInterface`
Inside `OutputInterface` the logic for adding "headers" and "columns" is already contained, it is only necessary to implement the abstract function `build()`.

The class contains a list of `headersInt` headers and a two-dimensional array of "table" columns `linesInt`.

Implementation example:
```kotlin
class CSVOutputImpl : OutputInterface() {
    override fun build(): String {
        val r = mutableListOf(headersInt.joinToString(","))
        r += linesInt.map { it.joinToString(",") }
        return r.joinToString("\n")
    }
}
```


## Step 2. Adding your implementation
After creating the `OutputInterface` implementation, you need to add it to the `Outputs` enum (located in the `output/Outputs.kt` file).

The enumeration element consists of 2 fields:
- a short name by which the user will select the output format
- references to `OutputInterface` implementation

Example:
```kotlin
enum class Outputs(
    val optionName: String,
    val outputClass: OutputClass
) {
    ConsTableOutput("console", ConsTableOutputImpl::class),
    CSVOutput("csv", CSVOutputImpl::class);
....
```
