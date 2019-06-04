---
title: Promise
date: 2019-06-01 21:09:08
tags:
categories: 
	- ES6
---

> 可以解决回调地狱的问题，而且将方法规范，成功就调用 resolve 方法，失败就调用 reject 方法

<!--more-->

## 回调

**具名回调**

```javascript
function user(fn) {
    fn('user: soa')
}

function userLog(userInfo) {
    console.log(userInfo)
}

user(userLog)
```

**匿名回调**

```javascript
function user(fn) {
    fn('user: soa')
}

user(function (userInfo) {
    console.log(userInfo)
})
```



**缺点**：

1. 现在看着是不是很简单，但是如果**回调中**再次**调用回调**，然后**回调的回调中**再次**调用回调**，你是不是就崩溃了那
2. node.js 中根据第一个参数是不是空来判断调用的回调函数，jquery中成功调用 success，失败调用 error，回调方式不统一



## Promise

resolve：为成功调用

reject：为失败调用

then：第一个参数为成功执行的函数，第二个参数为失败执行的函数

```javascript
function getUserInfo() {
    return new Promise(function (resolve, reject) {
        resolve('name: soalin')
    })
}

function printUserInfo(userInfo) {
    return new Promise(function (resolve, reject) {
        console.log(userInfo)
        resolve()
    })
}

function getOtherUserInfo(userInfo) {
    return new Promise(function (resolve, reject) {
        resolve('name: orange')
    })
}

getUserInfo()
    .then(printUserInfo) // name: soalin
    .then(getOtherUserInfo)
    .then(printUserInfo)  // name: orange
```

成功调用 resolve， 失败调用 reject

```javascript
function getUserInfo(name) {
    return new Promise(function (resolve, reject) {
        if (name === 'soalin') {
            console.log('认识')
            resolve('soalin是个帅哥')
        } else {
            console.log('不认识')
            reject()
        }
    })
}

getUserInfo('soalin')
    .then(function(d) {
        console.log(d) // soalin是个帅哥
    }, function () {
        console.log('看来不认识soalin')
    })
```

在失败函数执行完后，可以继续调用 resolve 或 resolve，这样会可以控制 then 之后，调用那个方法

**注**： 如果在失败函数中不写 return new Promise 直接写方法，Promise会默认你已经处理了这个错误，会默认调用 then 之后的 resolve ，所以最好都用 return new Promise

```javascript
function getUserInfo(name) {
    return new Promise(function (resolve, reject) {
        if (name === 'soalin') {
            console.log('认识')
            resolve(['soalin', '是个帅哥'])
        } else {
            console.log('不认识')
            reject('不认识')
        }
        
    })
}

function printUserInfo(data) {
    console.log(1)
    return new Promise(function (resolve, reject) {
        console.log(data)
        resolve(data[0])
    })
}

function getParentInfo(name) {
    return new Promise(function (resolve, reject) {
        if (name === 'soalin') {
            resolve(['小明', '小红', '小花'])
        } else {
            reject()
        }
    })
}

function errorMessage(message) {
    return new Promise(function (resolve, reject) {
        console.log('失败的理由是：' + message)
        reject('还是没搞定')
    })
}

function errorAgainMessage(message) {
    return new Promise(function (resolve, reject) {
        console.log('失败的理由是：' + message)
        reject()
    })
}

getUserInfo('soalin1')
    .then(printUserInfo, errorMessage)
    .then(getParentInfo, errorAgainMessage)
    .then(printUserInfo)
```

**catch()** 一个语法糖，当出现错误时会执行

**finally()** 一个语法糖，如果成功的方法和失败的方法相同，可以将他们放到 finally() 中，因为 then() 和 catch() 最后都会执行

**all()** 返回一个 `Promise` 实例，每个实例都成功，all返回成功，只要一个失败，返回为失败，空也表示成功

**race()** 返回第一个执行的 `Promise` 实例，第一个是成功就是成功，第一个是失败就是失败, 但是内部都会执行