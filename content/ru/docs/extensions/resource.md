---
title: Класс `Resource`
---

Запечатанный класс `Resource<out T>` используется для передачи 2 состояний:
- `Resource.Success<T>(val data: T)` - получение данных прошло успешно; хранит данные типа `T`
- `Resource.Error(val message: String)` - получение данных завершилось неудачей; хранит сообщение об ошибке