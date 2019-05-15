---
title: DOM事件
date: 2019-05-11 11:13:12
tags:
categories:
	- JavaScript
---

> 常用事件总结，嘿呀，真多啊！

<!--more-->

# EventTarget 接口

DOM 的事件操作（监听和触发），都定义在`EventTarget`接口

## addEventListener()

`addEventListener()`用于在当前节点或对象上，定义一个特定事件的监听函数

该方法接受三个参数。

- `type`：事件名称，大小写敏感。
- `listener`：监听函数。事件发生时，会调用该监听函数。
- `useCapture`：布尔值，表示监听函数是否在捕获阶段触发, 默认为`false`（监听函数只在冒泡阶段被触发）



## removeEventListener()

`removeEventListener`方法用来移除`addEventListener`方法添加的事件监听函数



# 事件模型

## 监听函数

浏览器的事件模型，就是通过监听函数对事件做出反应

JavaScript 有三种方法，可以为事件绑定监听函数

### HTML 的 on- 属性

一旦指定的事件发生，`on-`属性的值是原样传入 JavaScript 引擎执行。因此如果要执行函数，不要忘记加上一对圆括号

**缺点**：违反了 HTML 与 JavaScript 代码相分离的原则，不利于代码分工，别用

```html
<!-- 正确 -->
<body onload="doSomething()">

<!-- 错误 -->
<body onload="doSomething">
```



### 元素节点的事件属性

元素节点对象的事件属性，同样可以指定监听函数

**缺点**： 同一个事件只能定义一个监听函数，如果定义两次`onclick`属性，后一次定义会覆盖前一次，别用

```javascript
window.onload = doSomething;

div.onclick = function (event) {
  console.log('触发事件');
};
```



### addEventListener()

**优点**：同一个事件可以添加多个监听函数，能够指定在哪个阶段（捕获阶段还是冒泡阶段）触发监听函数，只用它

```javascript
div.addEventListener('click', function () {
    console.log(1)
}, false)

div.addEventListener('click', function () {
    console.log(2)
}, false)
```



# Event 对象

事件发生以后，会产生一个事件对象，作为参数传给监听函数。浏览器原生提供一个`Event`对象，所有的事件都是这个对象的实例，或者说继承了`Event.prototype`对象。

## 实例属性

### currentTarget，

### target

`currentTarget`属性返回事件正在执行的监听的那个节点。

`target`属性返回触发事件的那个节点

事件传播过程中，前者总是不变的，后者则是指向监听函数所在的那个节点对象,最好用 `currentTarget`



## 实例方法

### preventDefault()

`preventDefault`方法取消浏览器对当前事件的默认行为

利用这个方法，可以为文本输入框设置校验条件, 只能输入小写字母，否则输入事件的默认行为（写入文本框）将被取消，导致不能向文本框输入内容

```javascript
// <input type="text" id="my-input" />
var input = document.getElementById('my-input');
input.addEventListener('keypress', checkName, false);

function checkName(e) {
  if (e.charCode < 97 || e.charCode > 122) {
    e.preventDefault();
  }
}
```



### stopPropagation()

`stopPropagation`方法阻止事件在 DOM 中继续传播(阻止事件的冒泡和捕获)



### stopImmediatePropagation()

`stopImmediatePropagation`方法阻止同一个事件的其他监听函数被调用

```javascript
function l1(e){
  e.stopImmediatePropagation();
}

function l2(e){
  console.log('hello world'); // 不会输出
}

el.addEventListener('click', l1, false);
el.addEventListener('click', l2, false);
```



# 鼠标事件

## 鼠标事件的种类

- `click`：按下鼠标时触发
- `mousemove`：当鼠标在一个节点内部移动时触发
- `mouseenter`：鼠标进入一个节点时触发，进入子节点不会触发这个事件
- `mouseover`：鼠标进入一个节点时触发，进入子节点会再一次触发这个事件
- `mouseout`：鼠标离开一个节点时触发，离开父节点也会触发这个事件
- `mouseleave`：鼠标离开一个节点时触发，离开父节点不会触发这个事件



## 实例属性

### MouseEvent.clientX，

### MouseEvent.clientY

`clientX`属性返回鼠标位置相对于浏览器导航栏底部左上角(不会算上滚动条距离)的水平坐标，`clientY`属性返回垂直坐标

### MouseEvent.screenX，

### MouseEvent.screenY

`screenX`属性返回鼠标位置相对于**屏幕**左上角(浏览器顶部左上角)的水平坐标，`screenY`属性返回垂直坐标

### MouseEvent.offsetX，

### MouseEvent.offsetY

`offsetX`属性返回目标元素左侧`padding`边缘到鼠标位置的水平距离，`offsetY`属性返回目标元素上方`padding`边缘到鼠标位置的垂直距离

### MouseEvent.pageX，

### MouseEvent.pageY

`pageX`属性返回鼠标位置与文档(根节点html)左侧边缘的距离，`pageY`属性返回与文档上侧边缘的距离



# 键盘事件

## 键盘事件的种类

- `keydown`：按下键盘时触发
- `keypress`：按下有值的键时触发，即按下 Ctrl、Alt、Shift、Meta 这样无值的键，这个事件不会触发。对于有值的键，按下时先触发`keydown`事件，再触发这个事件
- `keyup`：松开键盘时触发该事件



## 实例属性

### KeyboardEvent.code

`code`属性返回一个字符串，表示当前按下的键的字符串形式

- 数字键0 - 9：返回`digital0` - `digital9`
- 字母键A - z：返回`KeyA` - `KeyZ`
- 功能键F1 - F12：返回 `F1` - `F12`

### KeyboardEvent.key

`key`属性返回一个字符串，表示按下的键名

按下 Ctrl + a，则返回`a`；按下 Shift + a，则返回大写的`A`

### KeyboardEvent.keyCode 

`key`属性返回一个数值，表示按下键名的ASCII



# 进度事件

- `error`：由于错误导致外部资源无法加载时触发
- `load`：外部资源加载成功时触发
- `timeout`：加载超时时触发



# 表单事件

### input 事件

`input`事件当`<input>`、`<select>`、`<textarea>`的值发生变化时触发*

**特点**: 会连续触发，每按下一次按键，就会触发一次`input`事件

### select 事件

`select`事件当在`<input>`、`<textarea>`里面选中文本时触发

### change 事件

`change`事件当`<input>`、`<select>`、`<textarea>`的值发生变化时触发

**特点**：不会连续触发，全部修改完成时才会触发

- 激活单选框（radio）或复选框（checkbox）时触发。
- 用户提交时触发。比如，从下列列表（select）完成选择，在日期或文件输入框完成选择。
- 当文本框或`<textarea>`元素的值发生改变，并且丧失焦点时触发

### invalid 事件

提交表单时，不满足校验条件，就会触发`invalid`事件

### reset 事件，submit 事件

这两个事件发生在表单对象`<form>`上，而不是发生在表单的成员上

`reset`事件当表单重置时触发

`submit`事件当表单数据向服务器提交时触发



# 窗口事件

### scroll 事件

`scroll`事件在文档或文档元素滚动时触发，主要出现在用户拖动滚动条

### resize 事件

`resize`事件在改变浏览器窗口大小时触发，主要发生在`window`对象上面



# 焦点事件

- `focus`：元素节点获得焦点后触发，该事件不会冒泡。
- `blur`：元素节点失去焦点后触发，该事件不会冒泡。