---
title: New services for scan
type: docs
---

## Abstract class implementation
*To understand what the `Resource<T>` type is, see [this article]({{< relref "resource" >}})*

To add a new service for scanning, you must first implement the abstract class `TargetSystem`. It looks like this:
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

- The `targetName` field is the name used in the tool output
- The `cpe` field is the base CPE into which the version will be inserted and with which a request to the National Vulnerability Database API is created
- `check` method - must return `true` or `false` depending on whether the service is installed on the given URL
- `version` method - must return version in string representation suitable for substitution in CPE


## Adding your extension
After creating an implementation, you need to add it to the list of all extensions. To do this, you need to add a class reference to the list returned by the `getAllTargets()` function (it is located in the `getAllTargets.kt` file)

Example:
```kotlin
fun getAllTargets(): List<KClass<*>> {
    return listOf(
        ConfluenceTargetImpl::class,
        GrafanaTargetImpl::class
    )
}
```
