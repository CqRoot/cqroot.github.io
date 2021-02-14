---
title: Qt使用StyleSheet美化QPushButton
date: 2021-02-14 11:19:05
---

# Qt使用StyleSheet美化QPushButton

## 1 伪状态

QPushButton常用的伪状态有：default，hover，pressed，checked。

- default：正常状态
- hover：鼠标划过状态
- pressed：按钮被按下
- checked：按钮被选中

> 注意：如果仅在QPushButton上设置背景色，需要将border设置为某个值，否则背景可能不会显示。

## 2 分析

对于不可选中的按钮，我们常见的为default（默认）、hover（鼠标滑过）、pressed（按钮按下）三种状态。对于可选中的按钮，还要加一种checked（选中）状态。

对于按钮，我们主要可以设置的内容有前景色（字体颜色）、背景色、边框（圆角、颜色、粗细）。

## 3 编写StyleSheet

我绘制了三个QPushButton：button1，button2，button3。其中，button2可选中，button3准备使用qss绘制为圆角。

style sheet代码如下：

```css
QPushButton {
    background-color: #ffffff;
    border: 1px solid #dcdfe6;
    padding: 10px;
    border-radius: 5px;
}

QPushButton:hover {
    background-color: #ecf5ff;
    color: #409eff;
}

QPushButton:pressed, QPushButton:checked {
    border: 1px solid #3a8ee6;
    color: #409eff;
}

#button3 {
    border-radius: 20px;
}
```

## 4 效果

![效果图](/images/QnV4vCNY3rA9PpJ.gif)