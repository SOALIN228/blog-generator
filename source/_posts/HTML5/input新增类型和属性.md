---
title: input新增类型和属性
date: 2019-04-15 22:36:11
categories: 
	- HTML5
---

> HTML5中input增加了很多类型和属性，使用这些属性不仅在移动端可以方便我们开发，在pc端也可以方便我们对表单的验证

<!--more-->

 ## 新增类型

  在移动端类型不同，调出的键盘不同，在pc端可以配合`:valid` 和 `:invalid`做表单验证

  -  `<input type='email'>` 
  -  `<input type='url'>` 
  -  `<input type='tel'>`
  -  `<input type='number'>` 
  -  `<input type='search'>`




  ## 新增属性

  - autocomplete=“on”

    保存输入过的记录，`on/off`控制开关，也可以在input上选择关闭

  - autofocus="autofocus"

    页面加载时自动获得焦点

  - multiple="multiple"

    选择多个文件

  - placeholder="您好，请在这里输入您的用户名！"

    输入默认提示值

  - required="required"

    输入不能为空
