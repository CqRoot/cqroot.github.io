---
title: Go Slice 切片类型
date: 2021-02-13 15:25:22
---

# Go Slice 切片类型

Slice（切片）可以理解为不固定长度的数组。它的类型和操作比数组更加灵活。Slice是数组的一个引用。

## 结构组成

`src/runtime/slice.go`中Slice的结构如下：

```go
type slice struct {
	array unsafe.Pointer
	len   int
	cap   int
}
```

其中有三个元素：

- `array`指向一个数组的指针。
- `len`是Slice的可见元素的个数。使用`len()`函数可以获取切边的长度。
- `cap`表示Slice指向的内存空间的最大容量（对应元素的个数，而不是字节数）。使用`cap()`函数可以获取Slice的容量。

访问Slice中元素时，如果访问的元素超过Slice长度程序会报错。

向Slice追加元素时，如果Slice总元素数超过Slice容量，Slice会自动扩容。

数组的长度和容量是一样的。

## 定义Slice

```go
// 声明一个Slice，但没有分配空间。此时s等于nil
var s []type

// 使用make()创建Slice，指定了Slice的length（capacity为可选参数）
var s []type = make([]type, length)
s           := make([]type, length)
s           := make([]type, length, capacity)

// 声明一个Slice并初始化
s := []int{1, 2, 3}

// 从数组arr初始化Slice
s := arr[:]
s := arr[2:4]

// 从Slice s初始化Slice
s2 := s[2:4]
```

## 向Slice追加元素

向Slice追加元素使用内置的`append()`函数。如果追加后总元素数超过Slice的容量，Slice会自动扩容。

用法如下：

```go
s = append(s, 1)                 // 向Slice s追加一个元素
s = append(s, 1, 2)              // 向Slice s追加两个元素
s = append(s, []int{1, 2, 3}...) // 追加一个Slice，Slice需要使用...运算符
s = append([]int{1, 2, 3}, s...) // 向Slice前面追加元素
```

Slice后使用`...`运算符会把Slice打散作为参数传递。

需要注意的是，在Slice容量不足的情况下，append的操作会导致重新分配内存和数据复制。

> https://golang.org/ref/spec#Appending_and_copying_slices

## 遍历Slice元素

使用内置的`range()`函数可以遍历Slice元素。用法如下：

```go
for _, item := range(s) {
	fmt.Println(item)
}
```

