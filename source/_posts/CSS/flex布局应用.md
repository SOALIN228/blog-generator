---
title: flex布局应用
date: 2019-05-06 22:22:12
tags:
categories:
	- CSS
---

> flex 的一些工作中常用的实例

<!--more-->

### 手机页面布局



```css
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

ul {
  list-style: none;
}

.container {
  height: 100vh;
  display: flex;
  flex-direction: column;
}

header {
  height: 100px;
  background-color: #ddd;
}


main {
  flex-grow: 1;
  overflow: auto;
}

footer > ul {
  height: 100px;
  background-color: #ddd;
  display: flex;
}

footer > ul > li {
  background-color: red;
  width: 25%;
  height: 100%;
  border: 1px solid black;
}
```

```html
<div class="container">
  <header>header</header>
  <main>
    
  </main>
  <footer>
    <ul>
      <li></li>
      <li></li>
      <li></li>
      <li></li>
    </ul>
  </footer>
</div>
```



### 产品布局



```css
*{
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

ul {
  list-style: none;
}

ul {
  display: flex;
  flex-wrap: wrap;
  width: 350px;
  margin: auto;
  border: 1px solid black;
  justify-content: space-between;
}

li {
  width: 100px;
  height: 100px;
  background-color: #ddd;
  border: 1px solid red;
  margin: 10px 0;
}
```

```html
<ul>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
  <li></li>
</ul>
```



### pc布局



**常用布局**

```css
header {
  height: 50px;
  background-color: #ddd;
}

footer {
  height: 50px;
  background-color: #ddd;
}

.content {
  display: flex;
}

.content > aside {
  width: 120px;
  background-color: #444;
  /* order: 1; */
}

.content > main {
  height: 400px;
  flex: 1;
  background-color: red;
  /* order: 2; */
}

.content > nav {
  width: 100px;
  background-color: green;
  /* order: 3; */
}
```

```html
<header></header>
<div class="content">
  <aside></aside>
  <main></main>
  <nav></nav>
</div>
<footer></footer>
```



**双飞翼布局**

在常用布局的基础上，通过 `flex` 的 `order` 就可以快速实现

```html
<header></header>
<div class="content">
  <main></main>
  <aside></aside>
  <nav></nav>
</div>
<footer></footer>
```



### 绝对居中



```css
.parent {
  height: 400px;
  background-color: #ddd;
  display: flex;
  justify-content: center;
  align-items: center;
}
```

```html
<div class="parent">
  <div class="child">
    哈哈哈
  </div>
</div>
```