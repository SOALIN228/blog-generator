---
title: MVC与双向绑定与单向绑定
date: 2019-06-13 22:47:04
tags:
categories: 
	- JavaScript
---

> 彻底了解 MVC 的发展过程，以及框架带给我们的好处

<!--more-->

## MVC

通过前人的总结，发现代码基本可以分为三类：

1. 专门操作远程数据的代码（数据库打交道）
2. 专门呈现页面元素的代码（视图、显示）
3. 专门控制逻辑的代码（点击按钮后做什么）

前端发现后端代码经常分为三类(上面三类)，经过不断的完善最终形成了MVC的思想

1. M 专门负责处理数据
2. V 专门负责表现(视图)
3. C 专门负责逻辑

MVC 是 WEB 开发中经典的设计模式，也就是写代码的套路



## 使用 MVC 改写混乱的代码

**改写前的代码**：

<https://jsbin.com/noraye/8/edit?html,js,output>

**使用 MVC 改写后的代码**：

https://jsbin.com/yuwopuf/3/edit?js,output

**改进的几点**:

1. 将混乱的代码变得有条理，有组织
2. model 只负责存储数据、请求数据、更新数据
3. view 只负责渲染 HTML
4. controller 负责调度 model 和 view（view 数据改变后调用 model 更新，model 更新数据后重新渲染 view）



bindEvents() 中有几个注意点，分别是**事件委托**和 **this 绑定**

```javascript
// ...
events: [
	{ type: 'click', selector: '#increaseByOne', fnName: 'add' },
	{ type: 'click', selector: '#decreaseByOne', fnName: 'minus' },
	{ type: 'click', selector: '#square', fnName: 'square' },
	{ type: 'click', selector: '#cube', fnName: 'cube' },
],
bindEvents() {
	this.events.map((event)=>{
		$(this.view.el).on(event.type, event.selector, this[event.fnName].bind(this))
	})
},
add(){
	let newData = {number: this.model.data.number + 1}
	this.updateModel(newData)
},
// ...
```



## 使用模板代码

虽然 MVC 的代码很好，但是你们发现每个页面都需要写 model 、view 、controller ，那么为什么不用面向对象的思想来将通用的代码封装成一个类那

**使用模板封装的代码**：

https://jsbin.com/sodojac/5/edit?js,output

在 constructor 中，调用 init 方法使用 apply 传递所以参数，使用 Object.assign(this, rest) 将方法复制到Controller 这个对象上

```javascript
class Controller {
  constructor({view, model, events, init, ...rest }) {
    this.view = view 
    this.model = model
    this.events = events
    Object.assign(this, rest)
    this.bindEvents()
    this.view.render(this.model.data)
    init.apply(this, arguments)
  }
  bindEvents() {
    this.events.map((e) => {
      this.view.$el.on(e.type, e.el, this[e.fn].bind(this))
    })
  }
}
```



## 细节优化

虽然我们的代码已经比较完美了，但是还可以继续优化

1. 使用发布/订阅模式在 controller 初始化时订阅(监听数据的变化)，在数据改变时进行发布(触发被监听的事件)
2. 模板渲染的变化太大，每次更新全部的数据，导致用户输入的数据被清空
   - 将用户输入的数据记录，记在 JS 的 data 里，每次重现渲染后填入记录的数据(数据绑定)
   - 只更新发生变化的部分(虚拟DOM)

**优化了第一部分的代码**：

<https://jsbin.com/sodojac/10/edit?js,output>

第二部分就要使用框架来进行优化了



## 双向绑定

Vue 是法语中的 View，目的就是为了代替 View

**双向绑定**：用户输入的数据和 Vue 中的data绑定，用户输入改变，data 中数据随之改变，反之也是如此,

原理是通过 `Object.defineProperty` 把这些属性全部转为 `getter/setter`



Vue 中的 data 使用**双向绑定**记录下用户输入的数据，这样数据就不会丢失，而且 Vue **只更新变化的部分**

**代码：**

<https://jsbin.com/vixoku/4/edit?js,output>



Vue 可以将方法写在 **methods** 中，直接在 DOM 中使用 **v-on** 调用，这样 controller 显得很多余

**代码：**

https://jsbin.com/ruzikax/2/edit?js,output



model 中的 data 也可以写在 Vue 的 data 中

**代码：**

https://jsbin.com/cuhurit/5/edit?js,output



全部改完后你就会发现这已经不是 MVC 而是 MVVM 了



## 单向绑定

双向绑定存在一个问题，如果两个组件修改同一个对象上的不同属性，那么由于双向绑定，两个组件上的数据会不一致，解决办法就是将共同的数据写在父组件中，子组件改变后通知事件管理器，事件管理器告知父元素来修改数据，这样只要改一个地方，所有地方都会改变，这就是单向绑定



## 结论

**单向绑定**其实就是一个半自动的双向绑定，只是中间有几个环节，因为双向绑定有些时候无法解决我们遇到的问题，所以还不如由我们来控制中间过程

**双向绑定**是一个全自动的双向绑定，我们追求的目标

与用户数据打交道最好用单向绑定，与 UI 数据打交道用双向绑定



### 要点

**单向绑定**

- 了解如何是实现单项绑定
- 了解虚拟 DOM

**双向绑定**

- 了解双向绑定原理 `Object.defineProperty`，会使用 set 监听不存在的属性
- Proxy 会自动检查，如果发现不存在的属性，会帮你添加到对象上，这样就不用手动调用 set 了