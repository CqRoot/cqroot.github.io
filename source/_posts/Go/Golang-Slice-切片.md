---
title: Golang Slice 切片
date: 2021-02-13 15:25:22
---

# Golang Slice 切片

Slice（切片）可以理解为不固定长度的数组。它的类型和操作比数组更加灵活。切片是数组的一个引用。

## 结构组成

`src/runtime/slice.go`中slice的结构如下：

```go
type slice struct {
	array unsafe.Pointer
	len   int
	cap   int
}
```

其中有三个元素：

- `array`指向一个数组的指针。
- `len`是切片的可见元素的个数。使用`len()`函数可以获取切边的长度。
- `cap`表示切片指向的内存空间的最大容量（对应元素的个数，而不是字节数）。使用`cap()`函数可以获取切片的容量。

访问切片中元素时，如果访问的元素超过切片长度程序会报错。

向切片追加元素时，如果切片总元素数超过切片容量，切片会自动扩容。

数组的长度和容量是一样的。

## 定义切片

```go
// 声明一个切片，但没有分配空间。此时s等于nil
var s []type

// 使用make()创建切片，指定了切片的length（capacity为可选参数）
var s []type = make([]type, length)
s           := make([]type, length)
s           := make([]type, length, capacity)

// 声明一个切片并初始化
s := []int{1, 2, 3}

// 从数组arr初始化切片
s := arr[:]
s := arr[2:4]

// 从切片s初始化切片
s2 := s[2:4]
```

## 向切片追加元素

向切片追加元素使用内置的`append()`函数。如果追加后总元素数超过切片的容量，切片会自动扩容。

用法如下：

```go
s = append(s, 1)                 // 向切片s追加一个元素
s = append(s, 1, 2)              // 向切片s追加两个元素
s = append(s, []int{1, 2, 3}...) // 追加一个切片，切片需要使用...运算符
s = append([]int{1, 2, 3}, s...) // 向切片前面追加元素
```

切片后使用`...`运算符会把切片打散作为参数传递。

需要注意的是，在切片容量不足的情况下，append的操作会导致重新分配内存和数据复制。

> https://golang.org/ref/spec#Appending_and_copying_slices

## 遍历切片元素

使用内置的`range()`函数可以遍历切片元素。用法如下：

```go
for _, item := range(s) {
	fmt.Println(item)
}
```

