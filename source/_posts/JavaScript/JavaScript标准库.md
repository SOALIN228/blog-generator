---
title: JavaScript标准库
date: 2019-04-30 11:04:39
tags:
categories:
	- JavaScript
---

> 学习标准库中的方法，就是一个字真多啊，啊！学习一时累，一直学习一直类，嘿(皮)！

<!--more-->
# Object 对象

JavaScript 的所有其他对象都继承自`Object`对象，即那些对象都是`Object`的实例

`Object`对象的原生方法分成两类：`Object`本身的方法与`Object`的实例方法

所谓“本身的方法”就是直接定义在`Object`对象的方法

所谓实例方法就是定义在`Object`原型对象`Object.prototype`上的方法。它可以被`Object`实例直接使用



## 构造函数

`Object`构造函数的首要用途，是直接通过它来生成新对象

```javascript
var obj1 = new Object();

var obj2 = {} // 与上面写法等价，是简便的写法
```

> `Number`、`String`、`Boolean` 不加new生成基本类型，加new生成对象，`Object`、`Array` 、`Function`加不加new都一样



## 静态方法

### Object.keys()

`Object.keys`方法用来遍历对象的属性

```javascript
var obj = {
  p1: 123,
  p2: 456
};

Object.keys(obj) // ["p1", "p2"]
```



## 实例方法

### Object.prototype.valueOf()

`valueOf`方法的作用是返回一个对象的“值”，默认情况下返回对象本身

```javascript
var obj = new Object();
obj.valueOf() === obj // true
```

### Object.prototype.toString()

`toString`方法的作用是返回一个对象的字符串形式，默认情况下返回类型字符串

```javascript
var o1 = new Object();
o1.toString() // "[object Object]"
```

### toString() 的应用：判断数据类型

`Object.prototype.toString`方法返回对象的类型字符串，因此可以用来判断一个值的类型

```javascript
var obj = {};
obj.toString() // "[object Object]"
```

`Object.prototype.toString`可以看出一个值到底是什么类型

```javascript
Object.prototype.toString.call(2) // "[object Number]"
Object.prototype.toString.call('') // "[object String]"
Object.prototype.toString.call(true) // "[object Boolean]"
Object.prototype.toString.call(undefined) // "[object Undefined]"
Object.prototype.toString.call(null) // "[object Null]"
Object.prototype.toString.call(Math) // "[object Math]"
Object.prototype.toString.call({}) // "[object Object]"
Object.prototype.toString.call([]) // "[object Array]"
```

### Object.prototype.hasOwnProperty() 

`Object.prototype.hasOwnProperty`方法接受一个字符串作为参数，返回一个布尔值，表示该实例对象自身是否具有该属性

```javascript
var obj = {
  p: 123
};

obj.hasOwnProperty('p') // true
obj.hasOwnProperty('toString') // false
```



# Array 对象

## 构造函数

`Array`是 JavaScript 的原生对象，同时也是一个构造函数，可以用它生成新的数组

```javascript
var arr = new Array(2);
arr.length // 2
arr // [ empty x 2 ]
```

不建议使用它生成新数组，因为只传一个参数代表数组长度，多个参数代表多个值，不一致性，所以直接使用数组字面量是更好的做法

```javascript
// bad
var arr = new Array(1, 2);

// good
var arr = [1, 2];
```




## 静态方法

### Array.isArray()

`Array.isArray`方法返回一个布尔值，表示参数是否为数组。它可以弥补`typeof`运算符的不足

```javascript
var arr = [1, 2, 3];

typeof arr // "object"
Array.isArray(arr) // true
```



## 实例方法

### valueOf()，toString()

`valueOf`方法是一个所有对象都拥有的方法，表示对该对象求值。数组的`valueOf`方法返回数组本身

```javascript
var arr = [1, 2, 3];
arr.valueOf() // [1, 2, 3]
```

`toString`方法也是对象的通用方法，数组的`toString`方法返回数组的字符串形式

```javascript
var arr = [1, 2, 3];
arr.toString() // "1,2,3"

var arr = [1, 2, 3, [4, 5, 6]];
arr.toString() // "1,2,3,4,5,6"
```

### push()，pop()

`push`方法用于在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组

```javascript
var arr = [];

arr.push(1) // 1
arr.push('a') // 2
arr.push(true, {}) // 4
arr // [1, 'a', true, {}]
```

`pop`方法用于删除数组的最后一个元素，并返回该元素。注意，该方法会改变原数组

```javascript
var arr = ['a', 'b', 'c'];

arr.pop() // 'c'
arr // ['a', 'b']
```

### shift()，unshift()

`shift()`方法用于删除数组的第一个元素，并返回该元素。注意，该方法会改变原数组

```javascript
var a = ['a', 'b', 'c'];

a.shift() // 'a'
a // ['b', 'c']
```

`unshift()`方法用于在数组的第一个位置添加元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组

```javascript
var a = ['a', 'b', 'c'];

a.unshift('x'); // 4
a // ['x', 'a', 'b', 'c']
```

`unshift()`方法可以接受多个参数，这些参数都会添加到目标数组头部

```javascript
var arr = [ 'c', 'd' ];
arr.unshift('a', 'b') // 4
arr // [ 'a', 'b', 'c', 'd' ]
```

### join()

`join()`方法以指定参数作为分隔符，将所有数组成员连接为一个字符串返回。如果不提供参数，默认用逗号分隔。

```javascript
var a = [1, 2, 3, 4];

a.join(' ') // '1 2 3 4'
a.join(' | ') // "1 | 2 | 3 | 4"
a.join() // "1,2,3,4"
```

### concat()

`concat`方法用于多个数组的合并。它将新数组的成员，添加到原数组成员的后部，然后返回一个新数组，原数组不变

```javascript
['hello'].concat(['world'], ['!'])
// ["hello", "world", "!"]

[1, 2, 3].concat(4, 5, 6)
// [1, 2, 3, 4, 5, 6]
```

如果数组成员包括对象，`concat`方法返回当前数组的一个浅拷贝。所谓“浅拷贝”，指的是新数组拷贝的是对象的引用

```javascript
var obj = { a: 1 };
var oldArray = [obj];

var newArray = oldArray.concat();

obj.a = 2;
newArray[0].a // 2
```

### reverse()

`reverse`方法用于颠倒排列数组元素，返回改变后的数组。注意，该方法将改变原数组

```javascript
var a = ['a', 'b', 'c'];

a.reverse() // ["c", "b", "a"]
a // ["c", "b", "a"]
```

### slice()

`slice`方法用于提取目标数组的一部分，返回一个新数组，原数组不变

```javascript
arr.slice(start, end);
```

它的第一个参数为起始位置（从0开始），第二个参数为终止位置（但该位置的元素本身不包括在内）。如果省略第二个参数，则一直返回到原数组的最后一个成员

```javascript
var a = ['a', 'b', 'c'];

a.slice(0) // ["a", "b", "c"]
a.slice(1) // ["b", "c"]
a.slice(1, 2) // ["b"]
a.slice(2, 6) // ["c"]
a.slice() // ["a", "b", "c"]
```

如果`slice`方法的参数是负数，则表示倒数计算的位置

```javascript
var a = ['a', 'b', 'c'];
a.slice(-2) // ["b", "c"]
a.slice(-2, -1) // ["b"]
```

`slice`方法的一个重要应用，是将类似数组的对象转为真正的数组

```javascript
Array.prototype.slice.call({ 0: 'a', 1: 'b', length: 2 })
// ['a', 'b']

Array.prototype.slice.call(document.querySelectorAll("div"));
Array.prototype.slice.call(arguments);
```

上面代码的参数都不是数组，但是通过`call`方法，在它们上面调用`slice`方法，就可以把它们转为真正的数组

### splice()

`splice`方法用于删除原数组的一部分成员，并可以在删除的位置添加新的数组成员，返回值是被删除的元素。注意，该方法会改变原数组

```javascript
arr.splice(start, count, addElement1, addElement2, ...);
```

`splice`的第一个参数是删除的起始位置（从0开始），第二个参数是被删除的元素个数。如果后面还有更多的参数，则表示这些就是要被插入数组的新元素

```javascript
var a = ['a', 'b', 'c', 'd', 'e', 'f'];
a.splice(4, 2) // ["e", "f"]
a // ["a", "b", "c", "d"]

var a = ['a', 'b', 'c', 'd', 'e', 'f'];
a.splice(4, 2, 1, 2) // ["e", "f"]
a // ["a", "b", "c", "d", 1, 2]
```

起始位置如果是负数，就表示从倒数位置开始删除

```javascript
var a = ['a', 'b', 'c', 'd', 'e', 'f'];
a.splice(-4, 2) // ["c", "d"]
```

如果只是单纯地插入元素，`splice`方法的第二个参数可以设为`0`

```javascript
var a = [1, 1, 1];

a.splice(1, 0, 2) // []
a // [1, 2, 1, 1]
```

如果只提供第一个参数，等同于将原数组在指定位置拆分成两个数组

```javascript
var a = [1, 2, 3, 4];
a.splice(2) // [3, 4]
a // [1, 2]
```

### sort()

`sort`方法对数组成员进行排序，默认是按照字典顺序排序。排序后，原数组将被改变

```javascript
['d', 'c', 'b', 'a'].sort()
// ['a', 'b', 'c', 'd']

[4, 3, 2, 1].sort()
// [1, 2, 3, 4]

[11, 101].sort()
// [101, 11]
```

如果想让`sort`方法按照自定义方式排序，可以传入一个函数作为参数

```javascript
[10111, 1101, 111].sort(function (a, b) {
  return a - b;
})
// [111, 1101, 10111]
```

`sort`的参数函数本身接受两个参数，表示进行比较的两个数组成员。如果该函数的返回值大于`0`，表示第一个成员排在第二个成员后面；其他情况下，都是第一个元素排在第二个元素前面。

```javascript
[
  { name: "张三", age: 30 },
  { name: "李四", age: 24 },
  { name: "王五", age: 28  }
].sort(function (o1, o2) {
  return o1.age - o2.age;
})
// [
//   { name: "李四", age: 24 },
//   { name: "王五", age: 28  },
//   { name: "张三", age: 30 }
// ]
```

### map()

`map`方法将数组的所有成员依次传入参数函数，然后把每一次的执行结果组成一个新数组返回,原数组没有变化

```javascript
var numbers = [1, 2, 3];

numbers.map(function (n) {
  return n + 1;
});
// [2, 3, 4]

numbers
// [1, 2, 3]
```

`map`方法接受一个函数作为参数。该函数调用时，`map`方法向它传入三个参数：当前成员、当前位置和数组本身

```javascript
[1, 2, 3].map(function(elem, index, arr) {
  return elem * index;
});
// [0, 2, 6]
```

`map`方法还可以接受第二个参数，用来绑定回调函数内部的`this`变量

```javascript
var arr = ['a', 'b', 'c'];

[1, 2].map(function (e) {
  return this[e];
}, arr)
// ['b', 'c']
```

### forEach()

`forEach`方法与`map`方法很相似，但是，`forEach`方法不返回值，只用来操作数据。这就是说，如果数组遍历的目的是为了得到返回值，那么使用`map`方法，否则使用`forEach`方法。

`forEach`的用法与`map`方法一致，参数是一个函数，该函数同样接受三个参数：当前值、当前位置、整个数组

```javascript
function log(element, index, array) {
  console.log('[' + index + '] = ' + element);
}

[2, 5, 9].forEach(log);
// [0] = 2
// [1] = 5
// [2] = 9
```

`forEach`方法也可以接受第二个参数，绑定参数函数的`this`变量

```javascript
var out = [];

[1, 2, 3].forEach(function(elem) {
  this.push(elem * elem);
}, out);

out // [1, 4, 9]
```

### filter()

`filter`方法用于过滤数组成员，满足条件的成员组成一个新数组返回

```javascript
[1, 2, 3, 4, 5].filter(function (elem) {
  return (elem > 3);
})
// [4, 5]
```

`filter`方法的参数函数可以接受三个参数：当前成员，当前位置和整个数组

```javascript
[1, 2, 3, 4, 5].filter(function (elem, index, arr) {
  return index % 2 === 0;
});
// [1, 3, 5]
```

`filter`方法还可以接受第二个参数，用来绑定参数函数内部的`this`变量

```javascript
var obj = { MAX: 3 };
var myFilter = function (item) {
  if (item > this.MAX) return true;
};

var arr = [2, 8, 3, 4, 1, 3, 2, 9];
arr.filter(myFilter, obj) // [8, 4, 9]
```

### reduce()，reduceRight()

`reduce`方法和`reduceRight`方法依次处理数组的每个成员，最终累计为一个值。它们的差别是，`reduce`是从左到右处理，`reduceRight`则是从右到左，其他完全一样

```javascript
[1, 2, 3, 4, 5].reduce(function (a, b) {
  console.log(a, b);
  return a + b;
})
// 1 2
// 3 3
// 6 4
// 10 5
//最后结果：15
```

`reduce`方法和`reduceRight`方法的第一个参数都是一个函数。该函数接受以下四个参数

1. 累积变量，默认为数组的第一个成员
2. 当前变量，默认为数组的第二个成员
3. 当前位置（从0开始）
4. 原数组

这四个参数之中，只有前两个是必须的，后两个则是可选的

如果要对累积变量指定初值，可以把它放在`reduce`方法和`reduceRight`方法的第二个参数

```javascript
[1, 2, 3, 4, 5].reduce(function (a, b) {
  return a + b;
}, 10);
// 25
```

下面是一个`reduceRight`方法的例子

```javascript
function subtract(prev, cur) {
  return prev - cur;
}

[3, 2, 1].reduce(subtract) // 0
[3, 2, 1].reduceRight(subtract) // -4
```

由于这两个方法会遍历数组，所以实际上还可以用来做一些遍历相关的操作。比如，找出字符长度最长的数组成员。

```javascript
function findLongest(entries) {
  return entries.reduce(function (longest, entry) {
    return entry.length > longest.length ? entry : longest;
  }, '');
}

findLongest(['aaa', 'bb', 'c']) // "aaa"
```

### indexOf()，lastIndexOf()

`indexOf`方法返回给定元素在数组中第一次出现的位置，如果没有出现则返回`-1`

```javascript
var a = ['a', 'b', 'c'];

a.indexOf('b') // 1
a.indexOf('y') // -1
```

`indexOf`方法还可以接受第二个参数，表示搜索的开始位置

```javascript
['a', 'b', 'c'].indexOf('a', 1) // -1
```

`lastIndexOf`方法返回给定元素在数组中最后一次出现的位置，如果没有出现则返回`-1`

```javascript
var a = [2, 5, 9, 2];
a.lastIndexOf(2) // 3
a.lastIndexOf(7) // -1
```

### 链式使用

上面这些数组方法之中，有不少返回的还是数组，所以可以链式使用

```javascript
var users = [
  {name: 'tom', email: 'tom@example.com'},
  {name: 'peter', email: 'peter@example.com'}
];

users
.map(function (user) {
  return user.email;
})
.filter(function (email) {
  return /^t/.test(email);
})
.forEach(function (email) {
  console.log(email);
});
// "tom@example.com"
```



## 理解

### JS中数组的本质

人类理解：数组就是数据的有序集合
JS理解：数据就是原型链中有 Array.prototype 的对象

### 伪数组

1. 有 0,1,2,3,4,5...n,length 这些 key 的对象
2. 原型链中没有 Array.prototype, 这样的对象就是伪数组
   -  arguments 对象
   -  document.querySelectAll('div') 返回的对象