---
title: JavaScript标准库包装对象
date: 2019-05-01 20:01:44
tags:
categories:
	- JavaScript
---

> 包装对象也是标准库中的一部分，包装对象中最常用的是String对象，提供了很多用于的API

<!--more-->

# 包装对象

三种原始类型的值——数值、字符串、布尔值——在一定条件下，也会自动转为对象

所谓“包装对象”，指的是与数值、字符串、布尔值分别相对应的`Number`、`String`、`Boolean`三个原生对象。这三个原生对象可以把原始类型的值变成（包装成）对象

```javascript
var v1 = new Number(123); // 不加new就会生成原始类型而不是对象
var v2 = new String('abc');
var v3 = new Boolean(true);

typeof v1 // "object"
typeof v2 // "object"
typeof v3 // "object"

v1 === 123 // false
v2 === 'abc' // false
v3 === true // false
```



# Boolean 对象

`Boolean`对象是 JavaScript 的三个包装对象之一



## Boolean 函数的类型转换作用

5个falsy值

```javascript
Boolean(undefined) // false
Boolean(null) // false
Boolean(0) // false
Boolean('') // false
Boolean(NaN) // false
```

但是很少有人会这么用，下面才是常见的用法

```javascript
!!undefined // false
!!null // false
!!0 // false
!!'' // false
!!NaN // false
```



# Number 对象

`Number`对象是数值对应的包装对象，可以作为构造函数使用，也可以作为工具函数使用



## 静态属性

**了解即可(眼熟)**

- `Number.POSITIVE_INFINITY`：正的无限，指向`Infinity`
- `Number.NEGATIVE_INFINITY`：负的无限，指向`-Infinity`
- `Number.NaN`：表示非数值，指向`NaN`
- `Number.MIN_VALUE`：表示最小的正数（即最接近0的正数，在64位浮点数体系中为`5e-324`），相应的，最接近0的负数为`-Number.MIN_VALUE`
- `Number.MAX_SAFE_INTEGER`：表示能够精确表示的最大整数，即`9007199254740991`
- `Number.MIN_SAFE_INTEGER`：表示能够精确表示的最小整数，即`-9007199254740991`



## 实例方法

### Number.prototype.toString()

`toString`方法可以接受一个参数，表示输出的进制。如果省略这个参数，默认将数值先转为十进制

```javascript
(10).toString() // "10"

(10).toString(2) // "1010"
(10).toString(8) // "12"
(10).toString(16) // "a"
```



### Number.prototype.toFixed()

`toFixed()`方法先将一个数转为指定位数的小数，然后返回这个小数对应的字符串

```javascript
(10).toFixed(2) // "10.00"
```



### Number.prototype.toExponential()

`toExponential`方法用于将一个数转为科学计数法形式，参数是小数点后有效数字的位数，范围为0到20

```javascript
(10).toExponential()  // "1e+1"
(10).toExponential(1) // "1.0e+1"
(10).toExponential(2) // "1.00e+1"

(1234).toExponential()  // "1.234e+3"
(1234).toExponential(1) // "1.2e+3"
(1234).toExponential(2) // "1.23e+3"
```



### Number.prototype.toPrecision()



`toPrecision`方法用于将一个数转为指定位数的有效数字，参数为有效数字的位数，范围是1到21

```javascript
(12.34).toPrecision(1) // "1e+1"
(12.34).toPrecision(2) // "12"
(12.34).toPrecision(3) // "12.3"
(12.34).toPrecision(4) // "12.34"
(12.34).toPrecision(5) // "12.340"
```



# String 对象

`String`对象是 JavaScript 原生提供的三个包装对象之一，用来生成字符串对象(常用)



## 静态方法

### String.fromCharCode()

`String`对象提供的静态方法,参数是一个或多个数值，代表 Unicode 码点，返回值是这些码点组成的字符串

```javascript
String.fromCharCode() // ""
String.fromCharCode(97) // "a"
String.fromCharCode(104, 101, 108, 108, 111)
// "hello"
```



## 实例属性

### String.prototype.length

`length`属性返回字符串的长度

```javascript
'abc'.length // 3
```



## 实例方法

### String.prototype.charAt()

`charAt`方法返回指定位置的字符，参数是从`0`开始编号的位置

```javascript
var s = new String('abc');

s.charAt(1) // "b"
s.charAt(s.length - 1) // "c"
```



### String.prototype.charCodeAt()

`charCodeAt`方法返回字符串指定位置的 Unicode 码

```javascript
'abc'.charCodeAt(1) // 98
```



### String.prototype.concat()

`concat`方法用于连接两个字符串，返回一个新字符串，不改变原字符串

```javascript
var s1 = 'abc';
var s2 = 'def';

s1.concat(s2) // "abcdef"
```



### String.prototype.slice() 

`slice`方法用于从原字符串取出子字符串并返回，不改变原字符串。它的第一个参数是子字符串的开始位置，第二个参数是子字符串的结束位置（不含该位置）

```javascript
'JavaScript'.slice(0, 4) // "Java"
```

如果省略第二个参数，则表示子字符串一直到原字符串结束

```javascript
'JavaScript'.slice(4) // "Script"
```

如果参数是负值，表示从结尾开始倒数计算的位置

```javascript
'JavaScript'.slice(-6) // "Script"
'JavaScript'.slice(0, -6) // "Java"
'JavaScript'.slice(-2, -1) // "p"
```



### String.prototype.substring()

`substring`方法用于从原字符串取出子字符串并返回，不改变原字符串，它的第一个参数表示子字符串的开始位置，第二个位置表示结束位置（返回结果不含该位置）

```javascript
'JavaScript'.substring(0, 4) // "Java"
```

如果省略第二个参数，则表示子字符串一直到原字符串的结束

```javascript
'JavaScript'.substring(4) // "Script"
```

如果第一个参数大于第二个参数，`substring`方法会自动更换两个参数的位置

如果参数是负数，`substring`方法会自动将负数转为0

```javascript
'JavaScript'.substring(-3) // "JavaScript"
'JavaScript'.substring(4, -3) // "Java"
```



### String.prototype.substr()

`substr`方法用于从原字符串取出子字符串并返回，不改变原字符串，第一个参数是子字符串的开始位置（从0开始计算），第二个参数是子字符串的长度

```javascript
'JavaScript'.substr(4, 6) // "Script"
```

如果省略第二个参数，则表示子字符串一直到原字符串的结束

如果第一个参数是负数，表示倒数计算的字符位置。如果第二个参数是负数，将被自动转为0



### String.prototype.indexOf()，

### String.prototype.lastIndexOf()

`indexOf`方法用于确定一个字符串在另一个字符串中第一次出现的位置，返回结果是匹配开始的位置。返回`-1`表示不匹配

```javascript
'hello world'.indexOf('o') // 4
'JavaScript'.indexOf('script') // -1
```

`indexOf`方法还可以接受第二个参数，表示从该位置开始向后匹配

```javascript
'hello world'.indexOf('o', 6) // 7
```

`lastIndexOf`方法的用法跟`indexOf`方法一致，主要的区别是`lastIndexOf`从尾部开始匹配，`indexOf`则是从头部开始匹配

```javascript
'hello world'.lastIndexOf('o') // 7
```



### String.prototype.trim()

`trim`方法用于去除字符串两端的空格，包括制表符（`\t`、`\v`）、换行符（`\n`）和回车符（`\r`），返回一个新字符串，不改变原字符串

```javascript
'  hello world  '.trim() // "hello world"
```



### String.prototype.toLowerCase()，

### String.prototype.toUpperCase()

`toLowerCase`方法用于将一个字符串全部转为小写，`toUpperCase`则是全部转为大写。它们都返回一个新字符串，不改变原字符串

```javascript
'Hello World'.toLowerCase() // "hello world"

'Hello World'.toUpperCase() // "HELLO WORLD"
```



### String.prototype.match()

`match`方法用于确定原字符串是否匹配某个子字符串，返回一个数组，成员为匹配的第一个字符串。如果没有找到匹配，则返回`null`

```javascript
'cat, bat, sat, fat'.match('at') // ["at"]
'cat, bat, sat, fat'.match('xt') // null
```

返回的数组还有`index`属性和`input`属性，分别表示匹配字符串开始的位置和原始字符串

```javascript
var matches = 'cat, bat, sat, fat'.match('at');
matches.index // 1
matches.input // "cat, bat, sat, fat"
```



### String.prototype.search()，

### String.prototype.replace()

`search`方法的用法基本等同于`match`，但是返回值为匹配的第一个位置。如果没有找到匹配，则返回`-1`

```javascript
'cat, bat, sat, fat'.search('at') // 1
```

`replace`方法用于替换匹配的子字符串，一般情况下只替换第一个匹配

```javascript
'aaa'.replace('a', 'b') // "baa"
```



### String.prototype.split()

`split`方法按照给定规则分割字符串，返回一个由分割出来的子字符串组成的数组

```javascript
'a|b|c'.split('|') // ["a", "b", "c"]
```

如果分割规则为空字符串，则返回数组的成员是原字符串的每一个字符

```javascript
'a|b|c'.split('') // ["a", "|", "b", "|", "c"]
```

如果省略参数，则返回数组的唯一成员就是原字符串

```javascript
'a|b|c'.split() // ["a|b|c"]
```

`split`方法还可以接受第二个参数，限定返回数组的最大成员数

```javascript
'a|b|c'.split('|', 0) // []
'a|b|c'.split('|', 1) // ["a"]
'a|b|c'.split('|', 2) // ["a", "b"]
'a|b|c'.split('|', 3) // ["a", "b", "c"]
'a|b|c'.split('|', 4) // ["a", "b", "c"]
```



### String.prototype.localeCompare()

`localeCompare`方法用于比较两个字符串。它返回一个整数，如果小于0，表示第一个字符串小于第二个字符串；如果等于0，表示两者相等；如果大于0，表示第一个字符串大于第二个字符串

```javascript
'apple'.localeCompare('banana') // -1
'apple'.localeCompare('apple') // 0
```