---
title: parted 分区工具
date: 2021-02-10 23:31:38
tags: [linux,storage]
categories:
  - storage
---

# parted - 分区工具

## 查看块设备分区信息

```bash
parted -l
```

## 设置分区表类型

```bash
parted -s /dev/sdX mklabel gpt
```

其中，`gpt`是`LABEL-TYPE`，其值还可以为`msdos`（mbr）。

## 分区

### 新建分区

```bash
parted -s /dev/sdX mkpart PART-TYPE [FS-TYPE] START END
```

* `PART-TYPE` 是分区类型，可选：`primary` `extended` `logical`
* `FS-TYPE` 是文件系统类型。mkpart并不会实际创建文件系统，FS-TYPE参数仅是让parted设置一个 1-byte 编码，让启动管理器可以提前知道分区中有什么格式的数据。
* `START` 是分区的起始位置，可以带单位，例如1M。一般写1。
* `END` 是设备的结束位置。可以带单位，也可以用百分比。例如100%表示到设备的末尾。

示例：

```bash
parted -s /dev/sdb mkpart primary 1 100%
```