---
title: JavaScript数据类型
date: 2019-04-17 14:09:21
tags:
categories:
	- JavaScript
---

> JavaScript共有七种数据类型，让我们先来学习一下他的六种基础数据类型的知识吧，只有学好基础知识，在日后的开发工作中，才能做到游刃有余

<!--more-->

## 概述

JavaScript 的数据类型，共有七种, 对象是最复杂的数据类型，又可以分成三个子类型

- 数值（number）
- 字符串（string）
- Symbol（ES6）
- 布尔值（boolean）
- undefined
- null
- 对象（object）

  - 狭义的对象（object）
  - 数组（array）
  - 函数（function）



## typeof 运算符

用于判断数据类型

```javascript
typeof 123 // "number"
typeof '123' // "string"
typeof false // "boolean"
function f() {}
typeof f // "function"
typeof undefined // "undefined"
typeof null // "object"
```

没有声明的变量会返回 undefined， 所以可以 typeof 来判断一个变量是否声明



## null, undefined 和布尔值

#### null 和 undefined

`null`与`undefined`都可以表示“没有”，含义非常相似

`null`表示空值， `undefined`表示“未定义”

一般为声明的空对象手动赋值为`null`， 变量默认就是`undefined`，所以不用手动来添加

```javascript
// 变量声明了，但没有赋值
var i;
i // undefined

// 对象没有赋值的属性
var  o = new Object();
o.p // undefined
```

#### 布尔值

布尔值代表“真”和“假”两个状态。“真”用关键字`true`表示，“假”用关键字`false`表示

下面六个值被转为`false`(falsy)，其他值都视为`true`

- `undefined`
- `null`
- `false`
- `0`
- `NaN`
- `""`或`''`（空字符串）

#### 转换成布尔

取反两次就会变成Boolean

```javascript
!!1 // true
```



## 数值

#### NaN

`NaN` 是 JavaScript 的特殊值，表示“非数字”，它的数据类型依然属于 `number` 

#### parseInt()

用于将字符串转为整数,  头部空格会被自动去除

```javascript
parseInt('123', 10) // 123
```

#### parseFloat()

用于将一个字符串转为浮点数

```javascript
parseFloat('3.14') // 3.14
```

#### isNaN()

用来判断一个值是否为`NaN` 

**技巧**：由于`NaN` 是  `number` ， isNaN 可以帮助我们快速判断是不是一个数字



## 字符串

#### 转义

反斜杠（\）在字符串内有特殊含义，用来表示一些特殊字符，所以又称为转义符

- `\0` ：null
- `\b` ：后退键
- `\n` ：换行符
- `\t` ：制表符
- `\'` ：单引号
- `\"` ：双引号
- `\\` ：反斜杠

#### length

返回字符串的长度

```javascript
var s = 'hello'
s.length // 5
```

#### 多行字符串

用 `+` 连接

```javascript
var s = '123' +
		'456'
```

#### 类型转换为字符串

```javascript
var a = 1
a.toString() // '1'
```



## 对象

对象就是一组“键值对”（key-value）的集合，是一种无序的复合数据集合

#### 对象的引用

如果不同的变量名指向同一个对象，那么它们都是这个对象的引用，也就是说指向同一个内存地址。修改其中一个变量，会影响到其他所有变量

#### 属性的读取

读取对象的属性，有两种方法，一种是使用点运算符，还有一种是使用方括号运算符(**一定要加引号**)

```javascript
var obj = {
  p: 'Hello World'
}

obj.p // "Hello World"
obj['p'] // "Hello World"
```

#### 属性的赋值

```javascript
var obj = {}

obj.foo = 'Hello'
obj['bar'] = 'World'
```

#### 属性的查看

查看一个对象本身的所有属性，可以使用`Object.keys`方法

```javascript
var obj = {
  key1: 1,
  key2: 2
}

Object.keys(obj) // ['key1', 'key2']
```

#### 属性的删除

`delete`命令用于删除对象的属性，删除成功后返回`true`

```javascript
var obj = { p: 1 };
Object.keys(obj) // ["p"]

delete obj.p // true
obj.p // undefined
Object.keys(obj) // []
```

#### 属性是否存在

`in`运算符用于检查对象是否包含某个属性, 包含就返回`true`，否则返回`false`

```javascript
var obj = { p: 1 };
'p' in obj // true
```

使用对象的`hasOwnProperty`方法, 判断是否为对象自身的属性

```javascript
var obj = {};
if ('toString' in obj) {
  console.log(obj.hasOwnProperty('toString')) // false
}
```

#### 属性的遍历

`for...in`循环用来遍历一个对象的全部属性

```javascript
var obj = {a: 1, b: 2, c: 3};

for (var i in obj) {
  console.log('键名：', i); // a b c
  console.log('键值：', obj[i]); // 1 2 3
}
```



## 函数

#### 函数的声明

**function 命令**

```javascript
function print(s) {
  console.log(s);
}
```

**函数表达式**

```javascript
var print = function(s) {
  console.log(s);
};
```

#### 函数名的提升

JavaScript 引擎将函数名视同变量名，所以采用`function`命令声明函数时，整个函数会像变量声明一样，被提升到代码头部

#### name 属性

函数的`name`属性返回函数的名字

```javascript
function f1() {}
f1.name // "f1"

var f2 = function () {};
f2.name // "f2"

var f3 = function myName() {};
f3.name // 'myName'
```

#### length 属性

函数的`length`属性返回函数预期传入的参数个数

```javascript
function f(a, b) {}
f.length // 2
```

#### toString()

函数的`toString`方法返回一个字符串，内容是函数的源码

```javascript
function f() {
  a();
}

f.toString()
// function f() {
//  a();
// }
```

#### 函数本身的作用域

函数本身也是一个值，也有自己的作用域。它的作用域与变量一样，就是其声明时所在的作用域，与其运行时所在的作用域无关。

```javascript
var a = 1;
var x = function () {
  console.log(a);
};

function f() {
  var a = 2;
  x();
}

f() // 1
```

#### 参数传递方式

函数参数如果是原始类型的值（数值、字符串、布尔值），传递方式是传值传递（passes by value）。这意味着，在函数体内修改参数值，不会影响到函数外部

```javascript
var p = 2;

function f(p) {
  p = 3;
}
f(p);

p // 2
```

```javascript
var obj = { p: 1 };

function f(o) {
  o.p = 2;
}
f(obj);

obj.p // 2
```

注意，如果函数内部修改的，不是参数对象的某个属性，而是替换掉整个参数，这时不会影响到原始值

```javascript
var obj = [1, 2, 3];

function f(o) {
  o = [2, 3, 4];
}
f(obj);

obj // [1, 2, 3]
```

#### arguments 对象

`arguments`对象包含了函数运行时的所有参数，`arguments[0]`就是第一个参数，`arguments[1]`就是第二个参数，以此类推。

```javascript
var f = function (one) {
  console.log(arguments[0]);
  console.log(arguments[1]);
  console.log(arguments[2]);
}

f(1, 2, 3) // 1 // 2 // 3
```

虽然`arguments`很像数组，但它是一个对象

如果要让`arguments`对象使用数组方法，真正的解决方法是将`arguments`转为真正的数组

```javascript
var args = Array.prototype.slice.call(arguments);

// 或者
var args = [];
for (var i = 0; i < arguments.length; i++) {
  args.push(arguments[i]);
}
```

#### 闭包

函数外部无法读取函数内部声明的变量

但是`f2`可以读取`f1`的局部变量，那么只要把`f2`作为返回值，我们不就可以在`f1`外部读取它的内部变量了吗！

```javascript
function f1() {
  var n = 999;
  function f2() {
    console.log(n);
  }
  return f2;
}

var result = f1();
result(); // 999
```

闭包的最大用处有两个，一个是可以读取函数内部的变量，另一个就是让这些变量始终保持在内存中，即闭包可以使得它诞生环境一直存在

```javascript
function createIncrementor(start) {
  return function () {
    return start++;
  };
}

var inc = createIncrementor(5);

inc() // 5
inc() // 6
inc() // 7
```

闭包的另一个用处，是封装对象的私有属性和私有方法

```javascript
function Person(name) {
  var _age;
  function setAge(n) {
    _age = n;
  }
  function getAge() {
    return _age;
  }

  return {
    name: name,
    getAge: getAge,
    setAge: setAge
  };
}

var p1 = Person('张三');
p1.setAge(25);
p1.getAge() // 25
```

#### 立即调用的函数表达式

```javascript
(function(){ /* code */ }());
// 或者
(function(){ /* code */ })();
```

通常情况下，只对匿名函数使用这种“立即执行的函数表达式” 。它的目的有两个：一是不必为函数命名，避免了污染全局变量；二是 IIFE 内部形成了一个单独的作用域，可以封装一些外部无法读取的私有变量。

```javascript
(function () {
  /* code */
}());
```



## 数组

数组（array）是按次序排列的一组值。每个值的位置都有编号（从0开始），整个数组用方括号表示。

任何类型的数据，都可以放入数组

```javascript
var arr = [
  {a: 1},
  [1, 2, 3],
  function() {return true;}
];

arr[0] // Object {a: 1}
arr[1] // [1, 2, 3]
arr[2] // function (){return true;}
```

#### 数组的本质

数组属于一种特殊的对象

```javascript
var arr = ['a', 'b', 'c'];

Object.keys(arr)
// ["0", "1", "2"]
```

#### length 属性

数组的`length`属性，返回数组的成员数量

```javascript
['a', 'b', 'c'].length // 3
```

清空数组的一个有效方法，就是将`length`属性设为0

```javascript
var arr = [ 'a', 'b', 'c' ];

arr.length = 0;
arr // []
```

#### for...in 循环和数组的遍历

`for...in`循环可以遍历数组,但是`for...in`不仅会遍历数组所有的数字键，还会遍历非数字键,所以，不推荐使用`for...in`遍历数组

```javascript
var a = [1, 2, 3];

for (var i in a) {
  console.log(a[i]); // 1 2 3
}
```

```javascript
var a = [1, 2, 3];
a.foo = true;

for (var key in a) {
  console.log(key); // 0 1 2 foo
}
```