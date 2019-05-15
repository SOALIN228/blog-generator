---
title: BFC&IFC
date: 2019-05-12 21:47:18
tags:
categories:
	- CSS
---

> BFC很少用主要是面试用，因为BFC可以解决的，使用flex布局都可以解决而且会更好

<!--more-->

# BFC

## BFC的功能

**爸爸管儿子**

用BFC包住浮动元素

**注意**： 

虽然和清除浮动效果一样，但不是清除浮动

儿子的子元素不归爸爸管，孙子归儿子管

BFC中兄弟元素的竖直margin会合并

**兄弟之间划清界限**

```html
<div class="gege"></div>
<div class="didi"></div>
```

```css
.gege {
  width: 30px;
  height: 600px;
  border: 3px solid red;
  float: left;
}

.didi {
  height: 600px;
  border: 5px solid green;
  overflow: hidden; // 触发bfc
}
```

触发bfc会将didi从做左面拉回来，即哥哥和弟弟分开，不缠在一起



## 如何触发BFC

- 为父元素设置浮动
- 为父元素设置绝对定位
- 为父元素设置inline-blocks或table-cells
- 为父元素设置overflow不为visible
- 为父元素设置display:flow-root



## 总结

不要解释什么是BFC，举例子说明什么是BFC

BFC可以解决的,可以使用其他来代替

除了面试不要用BFC，因为BFC会有副作用，可能产生意外bug



# IFC

## font-size

指的是一个看不见的框的高度，文字在这个框中，相当于印刷术的版子，版子中文字距离上下的高度由设计师决定，不同的字体距离不同



## line-height

指的是实际占地面积，不论line-height是否大于font-size所占框的高度，font-size所占的框都会在line-height中居中显示，默认为设计师指定

**问：**

子元素设置line-height为100px，为什么父元素高度不为100px，因为字体按照基线进行对齐，所以不同字体的基线位置不同，按照基线对齐后，有些字体的高度会超过100px(相当于上移或下移)，所以父元素包裹所有子元素就会高度变高一些(1px或3px不同字体不同)



## vertical-align

指定字体的对齐方式，默认基线对齐，基本不用



**解决实际问题：**

在div中插入img，图片下方有空隙，因为图片会和一个先不见的x以基线的形式对齐，这样下方便会出现空隙

使用vertical-align:middle、top、bottom都可以解决