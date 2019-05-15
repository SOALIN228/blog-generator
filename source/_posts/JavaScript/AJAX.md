---
title: AJAX
date: 2019-05-15 22:58:28
tags:
categories:
	- JavaScript
---

> 从0开始掌握AJAX从原生到JQuery，一站式解惑

<!--more-->

# XMLHttpRequest 对象

## 实例属性

### readyState

`readyState`返回一个整数，表示实例对象的当前状态。该属性只读

- 4，表示请求完毕

### onreadystatechange

`onreadystatechange`属性指向一个监听函数（实例的`readyState`属性变化），就会执行

### response

`response`属性表示服务器返回的数据体

### responseType

`responseType`属性是一个字符串，告诉服务器返回数据的类型

如果将这个属性设为`json`，浏览器就会自动对返回数据调用`JSON.parse()`方法。从`xhr.response`属性得到的不是字符串，而是一个 JSON 对象。

### responseText

`responseText`属性返回从服务器接收到的字符串

### responseXML

`responseXML`属性返回从服务器接收到的 HTML 或 XML 文档对象

### status

- 200, OK，访问正常
- 403, Forbidden，禁止访问(跨域)
- 404, Not Found，未找到指定网址
- 500, Internal Server Error，服务器发生错误

### timeout

`timeout`属性返回一个整数，表示多少毫秒后，如果请求仍然没有得到结果，就会自动终止。如果该属性等于0，就表示没有时间限制

### withCredentials

`withCredentials`属性是一个布尔值，表示跨域请求时，用户信息（比如 Cookie 和认证的 HTTP 头信息）是否会包含在请求之中，默认为`false`

如果需要跨域 AJAX 请求发送 Cookie，需要`withCredentials`属性设为`true`

为了让这个属性生效，服务器必须显式返回`Access-Control-Allow-Credentials`这个头信息

```xml
Access-Control-Allow-Credentials: true
```



## 实例方法

### open()

`open()`方法用于指定 HTTP 请求的参数

- `method`：表示 HTTP 动词方法，比如`GET`、`POST`、`PUT`、`DELETE`、`HEAD`等。
- `url`: 表示请求发送目标 URL。
- `async`: 布尔值，表示请求是否为异步，默认为`true`。

### send()

`send()`方法用于实际发出 HTTP 请求，GET请求的话可以不写参数，POST请求将参数写在send中传递

```javascript
var formData = new FormData(); // 发送表单

formData.append('username', '张三');
formData.append('email', 'zhangsan@example.com');
formData.append('birthDate', 1940);

var xhr = new XMLHttpRequest();
xhr.open('POST', '/register');
xhr.send(formData);
```

### setRequestHeader() 

`setRequestHeader()`方法用于设置浏览器发送的 HTTP 请求的头信息。该方法必须在`open()`之后、`send()`之前调用

### getResponseHeader()

`getResponseHeader()`方法返回 HTTP 头信息指定字段的值，如果还没有收到服务器回应或者指定字段不存在，返回`null`

### getAllResponseHeaders()

`getAllResponseHeaders()`方法返回一个字符串，表示服务器发来的所有 HTTP 头信息



### 设置和获取 header 

header 第三部分为回车

```xml
1. js设置 header
第一部分 request.open('post', '/xxx')
第二部分 request.setHeader('content-type', 'x-www-from-urlencoded')
第四部分 request.send('a=1&b=2')
2. js获取 header
第一部分 request.status / request.statusText
第二部分 request.getResponseHeader() / request.getAllResponseHeaders()
第四部分 request.responseText
```



# JSON

JS 是一门语言，JSON 是另一门语言，JSON 这门语言抄袭了 JS这门语言

JSON 没有 function 和 undefined ，别的都抄了

JSON 字符串必须加双引号

|        JS        |       JSON        |
| :--------------: | :---------------: |
|       null       |       null        |
|    ['a','b']     |     ["a","b"]     |
| {name: 'soalin'} | {"name":"soalin"} |

## stringify()

`JSON.stringify`方法用于将一个js值转为 JSON 字符串

```javascript
SON.stringify('abc') // ""abc""
JSON.stringify([]) // "[]"
JSON.stringify({}) // "{}"
JSON.stringify({ name: "张三" }) // '{"name":"张三"}'
```

## parse()

`JSON.parse`方法用于将 JSON 字符串转换成对应的js值

```javascript
JSON.parse('{}') // {}
JSON.parse('[1, 5, "false"]') // [1, 5, "false"]
```



# AJAX

**ajax返回的是字符串** **ajax返回的是字符串** **ajax返回的是字符串**

Jesse James Garrett 讲如下技术取名叫做 AJAX：异步的 JavaScript 和 XML

AJAX 技术包括以下四步:

1. 创建 AJAX 对象(XMLHttpRequest), 使用 XMLHttpRequest 发请求
2. 服务器返回 XML 格式的字符串
3. JS 解析 XML，并更新局部页面

## 原生

```javascript
let request = new XMLHttpRequest()
request.open('GET', '/xxx') // 配置requset
requset.send() // 发送
request.onreadystatechange = () => {
    if (request.readyState === 4) { // 请求响应完毕
        if (request.status >= 200 && request.status < 300) { // 请求成功
            let string = request.responseText // 获取返回的json字符串
            let object = window.JSON.parse(string) // 将json字符串转换成js对象
            } else if (request.status >= 400 && request.status < 500) {
                console.log('请求失败')
            }
    }
}
```

## 自己封装一个AJAX

```javascript
window.jQuery = function (nodeOrSelector) {
  let nodes = {}
  return nodes
}

window.$ = window.jQuery

window.jQuery.ajax = function ({ method, url, body }) {

  return new Promise(function (resolve, reject) {
    let request = new XMLHttpRequest()
    request.open(method, url)

    request.onreadystatechange = () => {
      if (request.readyState === 4) {
        if (request.status >= 200 && request.status < 300) {
          resolve.call(undefined, request.responseText)
        } else if (request.status >= 400 && request.status < 500) {
          reject.call(undefined, request)
        }
      }
    }

    request.send(body)
  })
}

myButton.addEventListener('click', function () {
  $.ajax({
    method: 'post',
    url: '/xxx',
    body: 'a=1&b=2'
  }).then(
    (text) => {
      console.log(text)
    },
    (request) => {
      console.log(request)
    })
})
```

## jQuery 的 AJAX

支持使用 promise 

```javascript
myButton.addEventListener('click', (e) => {
  $.ajax({
    url: '/xxx',
    method: 'post'
  }).then((responseText) => {
    console.log(responseText)
    return '请求成功了'
  }, () => {
    console.log('请求失败了')
  }).then((responseText) => {
    // 上一次的处理结果
    console.log(responseText)
  })
})
```



# 同源策略

同源政策的目的，是为了保证用户信息的安全，防止恶意的网站窃取数据

只有 协议+端口+域名 **一模一样**才允许发 AJAX 请求



# CORS 通信

CORS 是一个 W3C 标准，它允许浏览器向跨域的服务器，发出`XMLHttpRequest`请求，从而克服了 AJAX 只能同源使用的限制

在接口中设置Access-Control-Allow-Origin， 这样`http://xxx.com:8080`就可以访问这个接口了

```javascript
response.setRequestHeader('Access-Control-Allow-Origin', 'http://xxx.com:8080')
```