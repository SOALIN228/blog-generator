---
title: float布局
date: 2019-04-29 22:04:45
tags:
categories:
	- CSS
---

> 页面最常用布局之一，使用float布局即可以实现常见的页面的页面效果，也不会因为副作用而产生意外的BUG，兼容IE就用它

<!--more-->

## 概述

布局分两种，兼容IE和高级浏览器

兼容IE用float，高级浏览器用flex

## float布局

1. 父元素清除浮动

2. 子元素设置浮动和百分比

3. 功能分离，不要给子元素加margent等属性，做布局的只做布局，在子元素内部创建新元素做属性操作
4. 宽度和高度尽量少用
5. 建一个中间件div来设置 `-margin` 控制两端多余的 `margin`

注：ie8伪元素只支持一对冒号真傻逼，不兼容ie8写两对

```css
.header {
  background-color: #ddd;
  min-width: 680px;
}

.logo {
  width: 100px;
  height: 36px;
  line-height: 36px;
  float: left;
  background-color: #333;
  color: white;
  text-align: center;
}

.nav-fr {
  float: right;
}

.clearfix:after {
  content: '';
  display: block;
  clear: both;
}

.nav {
  line-height: 24px;
  padding: 6px 0;
}

.navItem {
  float: left;
  margin-left: 20px;
}

.banner {
  width: 800px;
  height: 300px;
  background-color: #888;
  margin-left: auto;
  margin-right: auto;
  margin-top: 10px;
}

.pictures {
  width: 800px;
  margin: 0 auto;
}

.pictures > .middle {
  margin: 0 -4px;
}

.picture {
  width: 194px;
  height: 194px;
  background-color: #ddd;
  margin: 4px;
  float: left;
}

.art {
  width: 800px;
  margin: 0 auto;
}

.art > .sider {
  float: left;
  width: 33.3%;
}

.sider-child {
  margin-right: 20px;
  height: 300px;
  background-color: #eee;
}

.art > .main {
  float: left;
  width: 66.6%;
  height: 300px;
  background-color: #eee;
}
```

```html
<div class="header clearfix">
  <div class="logo">logo</div>
  <div class="nav-fr">
    <div class="nav clearfix">
      <div class="navItem">导航1</div>
      <div class="navItem">导航2</div>
      <div class="navItem">导航3</div>
      <div class="navItem">导航4</div>
      <div class="navItem">导航5</div>
    </div>
  </div>
</div>
  
<div class="banner"></div>
  
<div class="pictures clearfix">
  <div class="middle">
    <div class="picture"></div>
    <div class="picture"></div>
    <div class="picture"></div>
    <div class="picture"></div>
    <div class="picture"></div>
    <div class="picture"></div>
    <div class="picture"></div>
    <!-- <div class="picture"></div> -->
  </div>
</div>
  
<div class="art clearfix">
  <div class="sider">
    <div class="sider-child"></div>
  </div>
  <div class="main"></div>
</div>
```