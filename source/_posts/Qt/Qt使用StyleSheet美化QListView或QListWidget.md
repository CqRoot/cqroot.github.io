---
title: Qt使用StyleSheet美化QListView或QListWidget
date: 2021-02-14 11:29:13
---

# Qt使用StyleSheet美化QListView或QListWidget

## 1 子控件与伪状态

QListWidget是QListView的子类，对这两个控件的美化是基本一样的。

对列表框的美化，分为对它本身的美化和对它的子控件item的美化。

对列表框的美化，主要就是保持背景色与item一致，以及其他一些通用的属性。

对item的美化，主要为default，hover，selected三个状态的配置。

## 2 分析

对QListView和QListWidget使用`outline: none`可以不显示item切换焦点的虚线。

如果需要对item添加边框，只显示下边框就好了（都设置边框的话前一个item的下边框会和后一个item的上边框叠在一起，边框显得很粗）。

对于选中状态后列表左侧显示小长条，有两种实现方法，这里直接设置了左边框来实现。对于一些情况控件设置左边框无效的情况下，也可以通过渐变背景色来实现。

## 3 编写StyleSheet

准备了两个QListWidget：listWidget、listWidget_2。其中，listWidget使用亮配色，绘制边框；listWidget_2使用暗配色，不绘制边框。

```css
QListView {
    outline: none;
}

#listWidget::item {
    background-color: #ffffff;
    color: #000000;
    border: transparent;
    border-bottom: 1px solid #dbdbdb;
    padding: 8px;
}

#listWidget::item:hover {
    background-color: #f5f5f5;
}

#listWidget::item:selected {
    border-left: 5px solid #777777;
}

#listWidget_2::item {
    background-color: #393d49;
    color: #ffffff;
    border: transparent;
    padding: 8px;
}

#listWidget_2::item:hover {
    background-color: #4e5465;
}

#listWidget_2::item:selected {
    border-left: 5px solid #009688;
}
```

## 效果

![效果图](/images/QkVK7SFcgehwvps.gif)