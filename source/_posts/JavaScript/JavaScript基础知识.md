---
title: JavaScript基础知识
date: 2019-04-17 14:09:21
tags:
categories:
	- JavaScript
---

> 使用JavaScript可以让我们做出很多酷炫的效果，现在让我们先来学习一下基础知识吧，只有学好基础知识，在日后的开发工作中，才能做到游刃有余

<!--more-->

## 逻辑与 &&

**说明**：在有一个操作数不是布尔值的情况下，遵循以下规则

1. 如果第一个操作数隐式类型转换后为true，则返回第二个操作数
2. 如果第一个操作数隐式类型转换后为false，则返回第一个操作数
3. 如果有一个操作数是null，则返回null
4. 如果有一个操作数是NaN，则返回NaN
5. 如果有一个操作数是undefined，则返回undefined

## 逻辑或 ||

**说明**：在有一个操作数不是布尔值的情况下，遵循以下规则

1. 如果第一个操作数隐式类型转换后为true，则返回第一个操作数
2. 如果第一个操作数隐式类型转换后为false，则返回第二个操作数
3. 如果有两个操作数是null，则返回null
4. 如果有两个操作数是NaN，则返回NaN
5. 如果有两个操作数是undefined，则返回undefined

## isNaN

使用isNaN可以帮助我们快速判断是不是一个数字，但是如果传入对象为空格或空字符串也会出问题，所以最好就是先判断一下类型是否为'number'

## arguments

**说明**：接受方法传递过来的所有参数

```javascript
function getAvg() {
  var sum=0.0, len=arguments.length, i;
  for (i = 0; i < len; i++) {
    sum += arguments[i];
  }
  return sum / len;
}
```

## Array数组对象



|   方法    | 描述                                                         |
| :-------: | ------------------------------------------------------------ |
|  push()   | 向数组的末尾添加元素，并返回新的长度                         |
| unshift() | 向数组的开头添加元素，并返回新的长度                         |
|   pop()   | 删除最后一个元素，并返回该元素的值                           |
|  shift()  | 从数组中**删除**第一个元素，并返回该元素的值                 |
|  join()   | 数组通过指定的分隔符进行分隔。默认是逗号                     |
|   map()   | 创建一个新数组，其结果是该数组中调用处理函数后返回的结果     |
| reverse() | 将数组中元素的位置颠倒,并返回该数组。该方法会改变原数组      |
|  sort()   | 对数组的元素进行排序，并返回数组                             |
| concat()  | 合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组 |
|  slice()  | 返回一个新的数组对象，这一对象是一个由 begin和 end决定的原数组 |
| splice()  | 通过删除或替换现有元素或者原地添加新的元素来修改数组,并以数组形式返回被修改的内容。此方法会改变原数组 |
| indexOf() | 返回查询元素在数组中的位置，没有找到该元素返回-1             |

`join`

```javascript
var elements = ['Fire', 'Wind', 'Rain'];

console.log(elements.join()); //"Fire,Wind,Rain"
```

`map` 

```javascript
var data = [1, 2, 3, 4];

var map1 = data.map(function (item) {
  return item + 2;
}); 

console.log(map1);// [3, 4, 5, 6]
```

`concat` 

```javascript
var alpha = ['a', 'b', 'c'];
var numeric = [1, 2, 3];

alpha.concat(numeric); // ['a', 'b', 'c', 1, 2, 3]
```

`sort`默认是将数组中的内容转换成字符串进行比较，所以要用匿名函数

```javascript
var arr = [9, 88, 12, 15, -2];
// 升序排列
arr.sort(function(a, b) {return a-b});
// 降序排列
arr.sort(function(a, b) {return b-a});
```

`splice` 可以操作数组的插入，删除，替换，返回操作的元素

```javascript
var arr = ["a", "b", "c", "d", "e"];

// 删除第2个元素后的一个元素
var delArr = arr.splice(2, 1); // "c"
console.log(arr); // "a", "b", "d", "e"

// 在第三个元素后插入
var insertArr = arr.splice(3, 0, "x", "y"); // []
console.log(arr); // "a", "b", "c", "x", "y", "d", "e"

// 替换第一个元素后的两个元素
var insertArr = arr.splice(1, 2, "x", "y"); // "b", "c"
console.log(arr); // "a", "x", "y", "d", "e"
```

## String

|        方法        |                       描述                       |
| :----------------: | :----------------------------------------------: |
|      charAt()      |            返回字符串中指定位置的字符            |
|     indexOf()      |     判断子字符串第一次在父字符串中出现的位置     |
|   lastIndexOf()    |                     从后开始                     |
| slice(start，end)  |                 返回一个新字符串                 |
| substr(start, len) | 返回一个字符串中从指定位置开始到指定字符数的字符 |
|      split()       |         以分隔符转换为数组，和join()相反         |
|       trim()       |             删除字符串两端的空白字符             |
|     replace()      |                返回被替换的字符串                |
|   toUpperCase()    |              返回转换为大写的字符串              |
|   toLowerCase()    |              返回转换为小写的字符串              |



## Math

|   方法   |        描述         |
| :------: | :-----------------: |
|  ceil()  |      向上取整       |
| floor()  |      向下取整       |
| round()  |    四舍五入取整     |
| random() | 产生0-1之间的随机数 |

产生`n-m`之间的随机整数的公式

```javascript
random = Math.floor(Math.random() * (m - n + 1) + n);
```

## Date

|     方法      |         描述         |
| :-----------: | :------------------: |
| getFullYear() |       返回年份       |
|  getMonth()   | 返回月份，值为`0-11` |
|   getDate()   |       返回天数       |
|   getDay()    | 返回星期，值为`0-6`  |
|   getTime()   |      返回毫秒值      |

可以通过	`new Date(year+1, month+1, day+1)`获得距离当前时间`1年+1月+1天的时间`