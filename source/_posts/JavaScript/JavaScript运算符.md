---
title: JavaScript运算符
date: 2019-04-18 22:11:42
tags:
categories:
	- JavaScript
---

> 熟练使用运算符，可以写出更优雅，更简洁的代码

<!--more-->

## 算术运算符

#### 减法运算符

string转化为数值

```javascript
'123' - 0 // 123 最便捷的转化成数值的方法
```

#### 加法运算符

数值转化为string

```javascript
1 + '' // '1'
```



## 布尔运算符

#### 取反运算符（!）

取反运算符是一个感叹号，用于将布尔值变为相反值，即`true`变成`false`，`false`变成`true`

```javascript
!true // false
!false // true
```

如果对一个值连续做两次取反运算，等于将其转为对应的布尔值

#### 且运算符（&&）

如果第一个运算子的布尔值为`true`，则返回第二个运算子的值

如果第一个运算子的布尔值为`false`，则直接返回第一个运算子的值，且不再对第二个运算子求值

取代`if`结构

```javascript
if (i) {
  doSomething();
}

// 等价于

i && doSomething();
```

#### 或运算符（||）

如果第一个运算子的布尔值为`true`，则返回第一个运算子的值，且不再对第二个运算子求值

如果第一个运算子的布尔值为`false`，则返回第二个运算子的值

短路规则对这个运算符也适用, 常用在如果第一个运算可能为null，则使用或运算添加一个' ',避免报错

```javascript
var x = 1;
true || (x = 2) // true
x // 1
```

#### 三元条件运算符

如果第一个表达式的布尔值为`true`，则返回第二个表达式的值，否则返回第三个表达式的值

```javascript
't' ? 'hello' : 'world' // "hello"
0 ? 'hello' : 'world' // "world"
```