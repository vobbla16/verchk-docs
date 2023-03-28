---
title: Новые форматы вывода данных
type: docs
---

Вывод большинства данных представляет из себя "таблицу", которая может быть выведена во множестве форматов.

## Шаг 1. Имплементация абстрактного класса `OutputInterface`
Внутри `OutputInterface` уже содержится логика по добавлению "заголовков" и "столбцов", необходимо лишь реализовать абстрактную функцию `build()`.

Внутри класса содержится список заголовков `headersInt` и двумерный массив столбцов "таблицы" `linesInt`.

Пример реализации:
```kotlin
class CSVOutputImpl : OutputInterface() {
    override fun build(): String {
        val r = mutableListOf(headersInt.joinToString(","))
        r += linesInt.map { it.joinToString(",") }
        return r.joinToString("\n")
    }
}
```


## Шаг 2. Добавление своей реализации
После создания имплементации `OutputInterface`, необходимо добавить её в перечисление `Outputs`(находится в файле `output/Outputs.kt`).

Элемент перечисления состоит из 2х полей:
- короткого имени, по котором пользователь будет выбирать формат вывода
- ссылки на имплементацию `OutputInterface`

Пример:
```kotlin
enum class Outputs(
    val optionName: String,
    val outputClass: OutputClass
) {
    ConsTableOutput("console", ConsTableOutputImpl::class),
    CSVOutput("csv", CSVOutputImpl::class);
....
```
