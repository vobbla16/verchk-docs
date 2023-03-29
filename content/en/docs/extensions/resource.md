---
title: Resource class
---

The sealed class `Resource<out T>` is used to pass 2 states:
- `Resource.Success<T>(val data: T)` - data was received successfully; stores data of type `T`
- `Resource.Error(val message: String)` - data acquisition failed; stores the error message
