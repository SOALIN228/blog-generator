---
title: DOM
date: 2019-05-02 17:00:01
tags:
categories:
	- JavaScript
---

> DOM的原生API真是太难用了，我只想说一句jQuery真好用

<!--more-->

# Node

## 属性

### nodeType

`nodeType`属性返回一个整数值，表示节点的类型

- 元素节点（element）：1 (例如<p>、<div>)
- 文本节点（text）：3 (文字)

### nodeName

`nodeName`属性返回节点的名称

- 文档节点（document）：`#document`

- 元素节点（element）：大写的标签名
- 文本节点（text）：`#text`

### textContent

`textContent`属性返回当前节点和它的所有后代节点的文本内容

**与innerText的区别**

- textContent 会获取所有元素的内容，包括 <script> 和 <style> 元素，然而 innerText 不会
- `innerText` 受 CSS 样式的影响，并且不会返回隐藏元素的文本，而textContent会。

### nextSibling，

### previousSibling

**兄弟关系**

`Node.nextSibling`属性返回当前节点后面的第一个同级节点

`previousSibling`属性返回当前节点前面的第一个同级节点

**会获取到Text节点，即空格或回车**

### childNodes，

### firstChild，

### lastChild

**儿子关系**

`childNodes`属性返回一个伪数组，成员包括当前节点的所有子节点

`firstChild`属性返回当前节点的第一个子节点

`lastChild`属性返回当前节点的最后一个子节点

**会获取到Text节点，即空格或回车**

### parentNode

**父亲关系**

`parentNode`属性返回当前节点的父节点

**不会获取到Text节点，即空格或回车**



## 方法

### appendChild()

`appendChild()`方法接受一个节点对象作为参数，插入当前节点的最后

### hasChildNodes()

`hasChildNodes`方法返回一个布尔值，表示当前节点是否有子节点

### cloneNode()

`cloneNode`方法用于克隆一个节点。接收一个参数，表示是否采用深度克隆，为`true`则该节点的所有后代节点也都会被克隆,为`false`则只克隆该节点本身

### insertBefore()

`insertBefore`方法用于将某个节点插入父节点内部的指定位置

### removeChild()

`removeChild`方法接受一个子节点作为参数，用于从当前节点移除该子节点

### isEqualNode()，

### isSameNode()

`isEqualNode`方法返回一个布尔值，用于检查两个节点是否相等

`isSameNode`方法返回一个布尔值，表示两个节点是否为同一个节点

```javascript
var p1 = document.createElement('p');
var p2 = document.createElement('p');

p1.isEqualNode(p2) // true

p1.isSameNode(p2) // false
p1.isSameNode(p1) // true
```

### normalize()

`normalize`方法用于清理当前节点内部的所有文本节点

```javascript
var wrapper = document.createElement("div");

wrapper.appendChild(document.createTextNode("Part 1 "));
wrapper.appendChild(document.createTextNode("Part 2 "));

// (规范化之前),wrapper.childNodes.length === 2
// wrapper.childNodes[0].textContent === "Part 1 "
// wrapper.childNodes[1].textContent === "Part 2 "

wrapper.normalize();
// (规范化之后), wrapper.childNodes.length === 1
// wrapper.childNodes[0].textContent === "Part 1 Part 2"
```



# Document

## 属性

### 快捷属性

**document.documentElement**

指向 DOM 的 html节点

**document.scrollingElement**

`document.scrollingElement`属性返回文档的滚动元素

```javascript
// 页面滚动到浏览器顶部
document.scrollingElement.scrollTop = 0;
```



### 节点集合属性

**document.links**

`document.links`属性返回所有设定了`href`属性的`<a>`及`<area>`节点

**document.forms**

`document.forms`属性返回所有`<form>`表单节点

**document.images**

`document.images`属性返回页面所有`<img>`图片节点



### 文档信息属性

**document.location**

`Location`对象是浏览器提供的原生对象，提供 URL 相关的信息和操作方法

**document.referrer**

`document.referrer`属性返回一个字符串，表示当前文档的访问者来自哪里



## 方法

### document.querySelector()，

### document.querySelectorAll()

`document.querySelector`方法接受一个 CSS 选择器作为参数，返回匹配该选择器的元素节点。如果有多个节点满足匹配条件，则返回第一个匹配的节点

`document.querySelectorAll`方法，包含所有匹配给定选择器的节点

### document.getElementById()

`document.getElementById`方法返回匹配指定`id`属性的元素节点

### document.getElementsByTagName()

`document.getElementsByTagName`方法搜索 HTML 标签名，返回符合条件的元素

### document.createElement()

`document.createElement`方法用来生成元素节点，并返回该节点

```javascript
var newDiv = document.createElement('div');
```

### document.createTextNode()

`document.createTextNode`方法用来生成文本节点（`Text`实例），并返回该节点

```javascript
var newDiv = document.createElement('div');
var newContent = document.createTextNode('Hello');
newDiv.appendChild(newContent);
```

### document.createDocumentFragment()

`document.createDocumentFragment`方法生成一个空的文档片段对象，用来生成一段较复杂的 DOM 结构，然后再插入当前文档。因为`DocumentFragment`不属于当前文档，对它的任何改动，都不会引发网页的重新渲染，减少对DOM的操作

```javascript
var docfrag = document.createDocumentFragment();

[1, 2, 3, 4].forEach(function (e) {
  var li = document.createElement('li');
  li.textContent = e;
  docfrag.appendChild(li);
});

var element  = document.getElementById('ul');
element.appendChild(docfrag);
```

### document.addEventListener()

```javascript
// 添加事件监听函数
document.addEventListener('click', listener, false);
```



# Element

## 实例属性 

### id

`id`属性返回指定元素的`id`属性，该属性可读写

### tagName

`tagName`属性返回指定元素的大写标签名

### className，

### classList

`className`属性用来**读写**当前元素节点的`class`属性

`classList`属性返回一个类似数组的对象，当前元素节点的每个`class`就是这个对象的一个成员

```javascript
// HTML 代码 <div class="one two three" id="myDiv"></div>
var div = document.getElementById('myDiv');

div.className // "one two three"

div.classList
// {
//   0: "one"
//   1: "two"
//   2: "three"
//   length: 3
// }
```

`classList`对象有下列方法

- `add()`：增加一个 class
- `remove()`：移除一个 class
- `contains()`：检查当前元素是否包含某个 class
- `toggle()`：将某个 class 移入或移出当前元素
- `item()`：返回指定索引位置的 class

### innerHTML

`innerHTML`属性返回一个字符串，等同于该元素包含的所有 HTML 代码

为了安全考虑，如果插入的是文本，最好用`textContent`属性代替`innerHTML`

### scrollHeight，

### scrollWidth

`scrollHeight`属性返回一个整数值，表示当前元素的总高度

```javascript
// 返回网页的总高度
document.documentElement.scrollHeight
document.body.scrollHeight
```

### offsetLeft，

### offsetTop

`Element.offsetLeft`返回当前元素左上角相对于网页的距离



## 实例方法

### getBoundingClientRect()

`getBoundingClientRect`方法返回一个对象，提供当前元素节点的大小、位置等信息，基本上就是 CSS 盒状模型的所有信息

- `left`：元素左上角相对于视口的横坐标
- `right`：元素右边界相对于视口的横坐标
- `top`：元素顶部相对于视口的纵坐标
- `bottom`：元素底部相对于视口的纵坐标

如果想得到绝对位置，可以将`left`属性加上`window.scrollX`，`top`属性加上`window.scrollY`

### focus()，

### blur()

`focus`方法用于将当前页面的焦点，转移到指定元素上

`blur`方法用于将焦点从当前元素移除



# 属性的操作

## 元素的标准属性

HTML 元素的标准属性（即在标准中定义的属性），会自动成为元素节点对象的属性

如：`a`元素标签的属性`id`和`href`，自动成为节点对象的属性

注： class属性改为`className`



## 属性操作的标准方法

### Element.getAttribute()

`getAttribute`方法返回当前元素节点的指定属性

```javascript
// <div id="div1" align="left">
div1.getAttribute('align') // "left"
```

### Element.setAttribute()

`Element.setAttribute`方法用于为当前元素节点新增属性

```javascript
// <button>Hello World</button>
var b = document.querySelector('button');
b.setAttribute('name', 'myButton');
```

### Element.hasAttribute()

`Element.hasAttribute`方法返回一个布尔值，表示当前元素节点是否包含指定属性

```javascript
var d = document.getElementById('div1');

if (d.hasAttribute('align')) {
  d.setAttribute('align', 'center');
}
```

### Element.removeAttribute()

`Element.removeAttribute`方法移除指定属性

```javascript
// <div id="div1" align="left" width="200px">
div1.removeAttribute('align');
// <div id="div1" width="200px">
```

## dataset 属性