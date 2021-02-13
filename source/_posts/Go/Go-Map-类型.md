---
title: Go Map 类型
date: 2021-02-13 19:36:10
---

# Go Map 类型

Map是一种无序的键值对的集合。通过哈希表实现。

## 定义Map

```go
// 声明一个Map，但没有分配空间。此时m等于nil
var m map[key_type]value_type

// 使用make()创建Map
var m map[key_type]value_type := make(map[key_type]value_type)
m                             := make(map[key_type]value_type)

// 声明一个Map并初始化
m := map[string]int {
    "item1": 1,
    "item2": 2,
}
```

key的type通常是数字、string（不可以是slice、map、function）

value的type可以是数字、string、map、struct。

## 判断Map中key是否存在

```go
_, ok := m["key"]
// ok为true则key存在，为false则key不存在
```

## 删除Map中的元素

使用`delete()`函数可以通过key来删除集合中的元素。如果key操作，删除该键值对；如果key不存在，不操作也不报错。

用法如下：

```go
delete(m, "key")
```

## 遍历Map中的内容

```go
for key, value := range m {
    fmt.Println(key, value)
}
```
