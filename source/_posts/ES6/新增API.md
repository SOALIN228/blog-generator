---
title: 新增API
date: 2019-09-03 06:48:49
tags:
categories:
	- ES6
---

> 新增加的API，有些很实用，解决了原因的bug，更加的方便

<!--more-->

### Object.assign

将所有可枚举属性的值从一个或多个源对象复制到目标对象

对象中的属性具有相同的键，则属性将被源对象中的属性覆盖，后面覆盖前面

```javascript
var a = {a1: 'a', a2: 2}
var b = {a1: 'b', b2: 2}
Object.assign(a, b)
var b = {a1: 'c', c2: 2}
Object.assign(a, b, c) // 复制多个
```

常用写法，拷贝到新的空对象上，完成浅拷贝

```javascript
var a = {a1: 'a', a2: 2, c:{c1: 2}}
var b =  Object.assign({}, a)
```

### Array.from

从一个伪数组对象中创建一个数组实例

```javascript
var a = { // 伪数组
  0: '000',
  1: '111',
  2: '222',
  length: 3
}

a = Array.prototype.slice.call(a, 0) // ES5转数组

a = Array.from(a) // ES6转数组
```

多种类型都可以转数组

```javascript
// String
Array.from('foo') // ["f", "o", "o"]

// Set
let s = new Set(['foo', window])
Array.from(s) // ["foo", window]

// Map
let m = new Map([[1, 2], [2, 4], [4, 8]])
Array.from(m) // [[1, 2], [2, 4], [4, 8]]
```

创建数组

```javascript
Array.apply(null, {length: 5}) // ES5创建一个5位数组

Array.from({length: 5}) // ES6创建一个5位数组

Array.from({length: 5}, (v, i) => i) // [0, 1, 2, 3, 4]

Array.from([1, 2, 3], x => x + x) // [2, 4, 6]

// 创建6个6的数组
function x(n, fill) { // ES5
  var array = Array.apply(null, {length: 5})
  return array.map(x => fill) // [6, 6, 6, 6, 6, 6]
}

function x(n, fill) { // ES5取巧方法，逼格高而已
  // ES5 创建一个多一位的数组，这样分隔符就会是你需要的，然后使用join替换分隔符,在转成数组即可
  // 注：数组内容是字符串 ["6", "6", "6", "6", "6", "6"] 
  return Array.apply(null, {length: n+1}).join(fill).split('')
}

function x(n, fill) { // ES6
  return Array.from({length: n}, x => fill) // [6, 6, 6, 6, 6, 6]
}

console.log(x(6, 6))
```

数组合并去重

```javascript
function combine(){ 
    let arr = [].concat.apply([], arguments) //没有去重复的新数组 
    return Array.from(new Set(arr))
} 

var m = [1, 2, 2], n = [2,3,3] 
console.log(combine(m,n)) // [1, 2, 3]
```

### Array.of

`Array.of()` 方法创建一个具有可变数量参数的新数组实例，而不考虑参数的数量或类型

```javascript
Array.of(7);       // [7] 
Array.of(1, 2, 3); // [1, 2, 3]
```

### Array.prototype.fill

用一个固定值填充一个数组中从起始索引到终止索引内的全部元素

第一个参数为填充值，第二个参数为起始位置，第三个参数为结束位置，后两个参数可以省略

```javascript
var array1 = [1, 2, 3, 4]

console.log(array1.fill(0, 2, 4)) // [1, 2, 0, 0]
console.log(array1.fill(0)) // [0, 0, 0, 0]
```

### Array.prototype.find

返回数组中满足提供的测试函数的第一个元素的值,filer是过滤所以会返回所以满足条件的

```javascript
var array1 = [5, 12, 8, 130, 44]

var found = array1.find(element => element > 10)

console.log(found)
```

### Array.prototype.keys()

 `keys()`方法返回一个包含数组中每个索引键的`Array Iterator`对象

```javascript
var array1 = ['a', 'b', 'c']
var iterator = array1.keys()
  
for (let key of iterator) {
  console.log(key) // 0 1 2
}
```

### Array.prototype.values()

 **values()** 方法返回一个新的 **Array Iterator** 对象，该对象包含数组每个索引的值

```javascript
const array1 = ['a', 'b', 'c']
const iterator = array1.values()

for (const value of iterator) {
  console.log(value) // "a" "b" "c"
}
```

### String.prototype.includes

`includes() ` 方法用来判断一个数组是否包含一个指定的值，如果包含则返回 true，否则返回false

```js
[1, 2, 3].includes(2)     // true
[1, 2, 3].includes(4)     // false
```

也可以使用`indexOf`,正则`search`和`match`来实现

### String.prototype.repeat

**repeat()** 构造并返回一个新字符串，该字符串包含指定数量的字符串的副本

```js
"abc".repeat(2)      // "abcabc"
```

### String.prototype.startsWith()

`startsWith()` 方法用来判断当前字符串是否以另外一个给定的子字符串开头，返回 `true` 或 `false`

```js
var str = "1234"

console.log(str.startsWith("123"))    // true
console.log(str.startsWith("234"))    // false

str.indexOf('1234') === 0 // 实现相同功能 true
```

### String.prototype.endsWith()

`endsWith()`方法用来判断当前字符串是否是以另外一个给定的子字符串结尾，返回 `true` 或 `false`

```js
var str = "1234"

console.log(str.endsWith("234"))    // true
console.log(str.endsWith("3"))      // false

str.lastIndexOf('4') === str.length-1   // 实现相同功能 true
str.lastIndexOf('34') === str.length-2  // true
```

### Number.EPSILON

**Number.EPSILON** 属性表示 1 与`Number`可表示的大于 1 的最小的浮点数之间的差值

```js
var i = 0
while(Math.abs(i - 1) < 0.00001) { // 计算机机是二级制，只能无限接近，不能等于
    i += 0.1
}
console.log("i is 1")


var i = 0
while(Math.abs(i - 1) < Number.EPSILON) {
    i += 0.1
}
console.log("i is 1")
```

### Number.isInteger()

**Number.isInteger()** 方法用来判断给定的参数是否为整数

```js
function isInt(n) { // 没有API之前
  return n === parseInt(n, 10)
}

Number.isInteger(0)        // true
Number.isInteger(1)        // true
```

### Number.isFinite()

**Number.isFinite()** 方法用来检测传入的参数是否是一个有穷数

```js
Number.isFinite(NaN);       // false
Number.isFinite(0);         // true
Number.isFinite(2e64);      // true
```

### Number.isNaN()

**Number.isNaN()** 方法确定传递的值是否为 `NaN`和其类型是 `Number`

```js
Number.isNaN(37) // false 参数是数字类型，且值为 NaN 的时候才会返回 true
Number.isNaN(NaN) // true

function myIsNaN(n) { // n != n 是NaN
  return n != n
}
```

