---
title: flex布局
date: 2019-05-05 22:00:28
tags:
categories:
	- CSS
---

> flex布局现代前端必会技能之一，还不赶紧学住？

<!--more-->

## 一、flex 布局是什么？

1. flex与方向无关
2. flex空间自动分配，自动对齐
3. 适用于简单线性布局

注意：flex布局，子元素的 `float` 、`clear` 和 `vertical-align` 属性将失效。

## 二、基本概念

![img](/blogImg/flex.png)

`container` 默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做`main start`，结束位置叫做`main end`；交叉轴的开始位置叫做`cross start`，结束位置叫做`cross end`。

`item` 默认沿主轴排列。单个项目占据的主轴空间叫做`main size`，占据的交叉轴空间叫做`cross size`。

## 三、container的属性

### 3.1 flex-direction

`flex-direction` 属性决定主轴的方向（即项目的排列方向）。

- `row`（默认值）：主轴为水平方向，起点在左端。
- `row-reverse`：主轴为水平方向，起点在右端。
- `column`：主轴为垂直方向，起点在上沿。
- `column-reverse`：主轴为垂直方向，起点在下沿。

### 3.2 flex-wrap

`flex-wrap`属性定义，如果一条轴线排不下，如何换行。

- `nowrap`（默认）：不换行。
- `wrap`：换行，第一行在上方。
- `wrap-reverse`：换行，第一行在下方。

### 3.3 flex-flow

`flex-flow`属性是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`。

### 3.4 justify-content

`justify-content` 属性定义了项目在**主轴**上的对齐方式。

- `flex-start`（默认值）：左对齐
- `flex-end`：右对齐
- `center`： 居中
- `space-between`：两端对齐，项目之间的间隔都相等。
- `space-around`：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

### 3.5 align-items

`align-items` 属性定义项目在**交叉轴**上如何对齐。父容器要有高度或子容器内容高度不同，才可以进行对齐。

- `flex-start`：交叉轴的起点对齐。
- `flex-end`：交叉轴的终点对齐。
- `center`：交叉轴的中点对齐。
- `baseline`: 项目的第一行文字的基线对齐。
- `stretch`（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

### 3.6 align-content

`align-content` 属性定义了多根轴线(多行)的对齐方式。如果项目只有一根轴线，该属性不起作用。

- `flex-start`：与交叉轴的起点对齐。
- `flex-end`：与交叉轴的终点对齐。
- `center`：与交叉轴的中点对齐。
- `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
- `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- `stretch`（默认值）：轴线占满整个交叉轴。

## 四、item的属性

### 4.1 order

`order` 属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

### 4.2 flex-grow

`flex-grow` 属性定义项目的放大比例，默认为 `0` ，即如果存在剩余空间，也不放大。

如果所有 `item` 的 `flex-grow` 属性都为1，则它们将等分剩余空间（如果有的话）。

按照 `flex-grow` 属性设置的值，成比例分配剩余空间。

### 4.3 flex-shrink

`flex-shrink` 属性定义了项目的缩小比例，默认为1，即如果空间不足，该 `item` 将缩小。

如果一个项目的 `flex-shrink`属性为0，则不缩小。

按照 `flex-grow` 属性设置的值，成比例缩小。

### 4.4 flex-basis

`flex-basis` 属性定义了在分配多余空间之前，`item` 占据的主轴空间（main size）的大小。

多余空间 = 伸缩容器的空间 - `flex-basis` 设置的空间 - 内容空间

设置 `flex-basis` 为0表示内容所占空间为0，平分父元素空间

### 4.5 flex

`flex` 属性是 `flex-grow` , `flex-shrink` 和 `flex-basis` 的简写，默认值为`0 1 auto`。后两个属性可选

flex:1 `flex-grow: 1;flex-shrink: 0;flex-basis: 0;`

flex:2 `flex-grow: 2;flex-shrink: 0;flex-basis: 0;`

### 4.6 align-self

`align-self` 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖 `align-items` 属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。