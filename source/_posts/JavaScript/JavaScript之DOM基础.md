---
title: JavaScript之DOM基础
date: 2019-04-18 22:11:42
tags:
categories:
	- JavaScript
---

> 很多时候我们使用js对页面的操作，都是通多操作DOM，来操作页面，使页面展现出我们想要的效果

<!--more-->

## 选取DOM元素的方法

| 方法         | 语法                     | 说明                                                         |
| ------------ | ------------------------ | ------------------------------------------------------------ |
| 通过ID       | getElementById()         | 返回带有指定ID的元素                                         |
| 通过标签名   | getElementsByTagName()   | 返回带有指定标签名的所有元素集合，类数组对象                 |
| 通过name属性 | getElementsByName()      | 返回指定name属性值的所有元素集合，类数组对象                 |
| 通过CSS类    | getElementsByClassName() | 返回指定class名称的所有元素集合，类数组对象                  |
| 上述都可     | querySelector()          | 返回选择器或选择器组匹配的第一个元素,如果找不到，则返回`null` |
| 上述都可     | querySelectorAll()       | 返回一个 `NodeList` 表示元素的列表                           |


## style

```javascript
// 获取id为box的元素
var box=document.getElementById("box");

// 设置元素的属性时减号连接的复合形式时必需要转换为驼峰形式
box.style.color='#f00';
box.style.fontWeight="bold";
```



## innerHTML

```javascript
*.innerHTML // 获取标签内容
*.innerHTML+='程序' // 设置标签内容
```



## className

```javascript
*.className // 获取标签class属性
*.className="current" // 设置标签class属性
```



## classList

**length**

获取元素类名的个数

```javascript
document.getElementById('box').classList.length
```

**item**

获取元素的类名

```javascript
document.getElementById('box').classList.item(0)
```

**add**

为元素添加指定类名

```javascript
document.getElementById('box').classList.add('green')
```

**remove**

移除元素上指定类名

```javascript
document.getElementById('box').classList.remove('red')
```

**contains**

检测元素是否含有指定类名

```javascript
document.getElementById('box').classList.contains('red')
```

**toggle**

如果不存在指定类名就添加，存在就删除

```javascript
document.getElementById('box').onclick = function() {
  this.classList.toggle('red')
}
```



## 总结

获取到元素的dom后

自身的属性如id，align，type等可以直接通过 `.属性名` 来操作

class属性用 `.className` 来操作

getAttribute() 可以获得所有属性

setAttribute() 可以设置所有属性

removeAttribute() 移除指定属性

```html
<p id="text" class="text" align="center" data-type="title">文本</p>
<input type="text" name="user" value="user" id="user" validate="true">
<script>
    var p=document.getElementById("text");
    var user=document.getElementById("user");
    console.log(p.getAttribute("class"));  //p.className
    console.log(user.getAttribute("validate"));
    // 给p设置一个data-color的属性
    p.setAttribute("data-color","red");
    // 给input设置一个isRead的属性
    user.setAttribute("isRead","false");
    // 删除p上的align属性
    p.removeAttribute("align");
</script>
```