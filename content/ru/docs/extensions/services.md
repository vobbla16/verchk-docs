---
title: Новые сервисы для сканирования
type: docs
---

## Имплементация абстрактного класса
*Для понимания, чем является тип `Resource<T>`, ознакомьтесь с [этой статьёй]({{< relref "resource" >}})*

Для добавления нового сервиса для сканирования необходимо в первую очередь реализовать абстрактный класс `TargetSystem`. Он выглядит так:
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

- Поле `targetName` - имя, используемое в выводе инструмента
- Поле `cpe` - базовое CPE, в которое будет вставляться версия, и с которым создаваться запрос к API National Vulnerability Database
- Метод `check` - должен возвражать `true` или `false` в зависимости от того, установлен ли на данном URL сервис
- Метод `version` - должен возвращать версию в строковом представлении, подходящем для подстановки в CPE


## Добавление Вашего расширения
После создания имплементации, необходимо добавить её в список всех расширений. Для этого необходимо добавить ссылку на класс в список, возвращаемый функцией `getAllTargets()`(она находится в файле `getAllTargets.kt`)

Пример:
```kotlin
fun getAllTargets(): List<KClass<*>> {
    return listOf(
        ConfluenceTargetImpl::class,
        GrafanaTargetImpl::class
    )
}
```
