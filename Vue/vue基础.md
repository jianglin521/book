---
title: vue基础
date: 2018/1/20 18:25:00 
tags: vue
categories: vue
---

## 起步 - Hello Vue
安装：`npm install vue --save`

指定vue管理内容区域，需要通过vue展示的内容都要放到找个元素中  通常我们也把它叫做边界 数据只在边界内部解析
`<div id="app">{{ msg }}</div>`

引入 vue.js
`<script src="vue.js"></script>`

使用 vue 
```js
	<script>
	  var vm = new Vue({
	    // el：提供一个在页面上已存在的 DOM 元素作为 Vue 实例的挂载目标
	    el: '#app',
	    // Vue 实例的数据对象，用于给 View 提供数据
	    data: {
	      msg: 'Hello Vue'
	    }
	  })
	</script>
```
## Vue实例
注意 1：先在data中声明数据，再使用数据
注意 2：可以通过 `vm.$data` 访问到data中的所有属性，或者 `vm.msg`
```js
	var vm = new Vue({
	  data: {
	    msg: '大家好，...'
	  }
	})
	
	vm.$data.msg === vm.msg // true
```
## 数据绑定
最常用的方式：Mustache(插值语法)，也就是 `{/{}}`语法
解释：`{/{}}`从数据对象data中获取数据
说明：数据对象的属性值发生了改变，插值处的内容都会更新
说明：`{/{}}`中只能出现JavaScript表达式 而不能解析js语句
注意：Mustache 语法不能作用在 HTML 元素的属性上
```js
	<h1>Hello, {{ msg }}.</h1>
	<p>{{ 1 + 2 }}</p>
	<p>{{ isOk ? 'yes': 'no' }}</p>
	
	<!-- ！！！错误示范！！！ -->
	<h1 title="{{ err }}"></h1>
```