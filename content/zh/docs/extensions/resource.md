---
title: 资源类
---

密封类`Resource<out T>`用于传递2种状态：
- `Resource.Success<T>(val data: T)` - 数据被成功接收；存储`T`类型的数据。
- `Resource.Error(val message: String)` - 数据获取失败；存储错误信息

