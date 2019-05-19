---
title: var、let和const
date: 2019-05-19 23:07:03
tags:
categories:
	- ES6
---

> ES6重新定义了JS，先了解下ES6最新的块作用域和const吧！

<!--more-->

## var

a = 1，如果当前没有a，声明一个全局 a，如果有 a，为 a 赋值，会造成含义不明

var a，会造成变量提升，会把定义放到最前面，在执行时赋值

var a, 可以被重复声明

如果只想暴露一个全局变量，非常复杂, 要使用立即执行函数和匿名函数，所以 let 应运而生

```javascript
(function () {
  var a = 1;
  window.soalin = function() {
      console.log(a)
  }
}())
```



## let

1. let作用域在最近的 {} 之间
2. 如果你在 let a 之前使用 a，会报错
3. 如果你重复 let a，那么报错



## const

1. const 作用域在最近的 {} 之间
2. 如果你在 const a 之前使用 a，会报错
3. 如果你重复 const a，那么报错
4. 只用一次赋值机会，且只能在声明时赋值

**注**：如果是对象指定的是指针指向的对象不可修改，对象的值可以修改

```javascript
function last() {
    const pi = 3.14;
    pi = 2; // 禁止修改
    const k = {
        a: 1
    }
    k.b = 2; // 可以添加
    k = { // 禁止指向其他对象
        s: 3
    }
    console.log(k);
}
```



## 实例

```html
<ul>
    <li>导航1</li>
    <li>导航2</li>
    <li>导航3</li>
    <li>导航4</li>
    <li>导航5</li>
    <li>导航6</li>
</ul>
```

不管点那个都是6，因为for已经执行完毕，且全局只有一个 i

```javascript
var liTags = document.querySelectorAll('li')

for (var i = 0; i < liTags.length; i++) {
  liTags[i].onclick = function () {
    console.log(i)
  }
}
```

如果想要使用 var 解决, 要使用匿名函数和立即执行函数来创建多个作用域

```javascript
var liTags = document.querySelectorAll('li')

for (var i = 0; i < liTags.length; i++) {
  (function (j) {
    liTags[j].onclick = function () {
      console.log(j)
    }
  })(i)
}
```

使用 let 就非常容易解决了, 因为 let 会创建多个 i， 一共会有7个 i， for上 1 个，for里 6 个

```js
var liTags = document.querySelectorAll('li')

for (let i = 0; i < liTags.length; i++) {
  // js会自动帮你创建一个 i，i 的值为for圆括号内 i 的值  
  liTags[i].onclick = function () {
    console.log(i)
  }
  // 将for里面 i 的值赋给外面for中 i 的值
}
```