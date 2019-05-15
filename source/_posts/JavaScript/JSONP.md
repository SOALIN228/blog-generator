---
title: JSONP
date: 2019-05-14 22:55:05
tags:
categories:
	- JavaScript
---

> JSONP的本质就是使用script标签发送一个get请求带上一个callback函数，然后移除script标签，后台收到请求后执行前端传过去的函数

<!--more-->

## 实现一个简易JSONP

**需求**： 点击按钮，钱数减1

### 手写一个 JSONP

```html
<title>首页</title>
<link rel="stylesheet" href="/style.css">
<h5>您的账户余额是 <span id="amount">$$$amount$$$</span></h5>
<button id="button">付款</button>
<script>
    button.addEventListener('click', function (e) {
      let script = document.createElement('script')
      let functionName = 'soa' + parseInt(Math.random()*10000, 10)
      window[functionName] = function (result) {
          if (result === 'success') { // 后台返回成功
              amount.innerText = amount.innerText - 1
          } else {
              // 后台返回失败
          }
      }
      script.src = 'http://xxx.com:8080/pay？callback=' + functionName
      document.body.appendChild(script)
      script.onload = function (e) {
        alert('success')
        e.currentTarget.remove() // 移除script
        delete window[functionName] // 移除window方法
      }
      script.onerror = function (e) {
        alert('fail')
        e.currentTarget.remove()
        delete window[functionName]
      }
    })
</script>
```

### 使用 jQuery 的 JSONP

```html
<title>首页</title>
<link rel="stylesheet" href="/style.css">
<h5>您的账户余额是 <span id="amount">$$$amount$$$</span></h5>
<button id="button">付款</button>
<script src="https://cdn.bootcss.com/jquery/3.4.1/jquery.min.js"></script>
<script>
    button.addEventListener('click', function (e) {
        $.ajax({
            url: "http://xxx.com:8080/pay",
            dataType: "jsonp",
            success: function (response) {
                if (response === 'success') {
                    amount.innerText = amount.innerText - 1
                }
            }
        })
    })
</script>
```

### 后台简易逻辑

```javascript
if (path === '/pay') {
    var amount = fs.readFileSync('./db', 'utf8') // 读取数据库数据
    var newAmount = amount - 1
    fs.writeFileSync('./db', newAmount) // 数据写入数据库
    response.setHeader("Content-Type", "application/javascript")
	response.statusCode = 200
    response.write(`${query.callbackName}.call(undefined, 'success')`) // 调用前端传递传递的参数，将数据返回给前端
    response.end() 
}
```



## JSONP的理解

### JSONP 的实现步骤

请求方: xxx.com 的前端程序员(浏览器)

响应方: yyy.com 的后端程序员(服务器)

1. 请求方创建 script, src 指向响应方, 同时传一个查询参数`?callbackName=xxx`
2. 响应方根据查询参数 callbackName, 构造形如`xxx.call(undefined, "你想要的数据")`这样的响应
3. 浏览器收到响应, 就会执行 `xxx.call(undefined, "你要的数据")`
4. 那么请求方就知道了他要的数据



### JSONP的约定

1. callbackName -> callback
2. xxx -> 用随机数xxx()



### JSONP 格式

在 JSONP 的实现步骤中, 第三步的`你要的数据`必须是 JSONP 格式, 它是从后端传给前端的数据

P 表示padding, 指 JSONP 的边界(花括号)

JSON 表示数据格式为 json(json数据一定要有双引号)

```json
{ // 边界
  "zzz": 'success', // json数据
  "left": ${newAount}
}
```