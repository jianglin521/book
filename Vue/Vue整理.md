---
title: Vue整理
date: 2018/1/27 18:24:59 
tags: Vue
categories: Vue
---

## vue整理
## 起步 - Hello Vue
**安装**：`npm isntall --save`

指定vue管理内容区域，需要通过vue展示的内容都要放到找个元素中 通常我们也把它叫做边界 数据只在边界内部解析
`<div id="app">{{ msg }}</div>`

 引入 vue.js 
`<script src="vue.js"></script>`

## 使用 vue
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
**注意 1**：先在data中声明数据，再使用数据
**注意 2**：可以通过 vm.$data 访问到data中的所有属性，或者 vm.msg
```js
	var vm = new Vue({
	data: {
	msg: '大家好，...'
	}
	})
	vm.$data.msg === vm.msg // true
```

## 数据绑定
最常用的方式：Mustache(插值语法)，也就是` {/{}}` 语法
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

## 双向数据绑定
双向数据绑定：将DOM与Vue实例的data数据绑定到一起，彼此之间相互影响
- 数据的改变会引起DOM的改变
- DOM的改变也会引起数据的变化

原理：Object.defineProperty中的get和set方法
- getter和setter：访问器
- 作用：指定读取或设置对象属性值的时候，执行的操作
```js
	/* defineProperty语法 介绍 */
	var obj = {}
	Object.defineProperty(obj, 'msg', {
	// 设置 obj.msg = "1" 时set方法会被系统调用 参数分别是设置后和设置前的值
	set: function (newVal, oldVal) { },
	// 读取 obj.msg 时get方法会被系统调用
	get: function ( newVal, oldVal ) {}
	})
```

## Vue双向绑定的极简实现
```js
	<!-- 示例 -->
	<input type="text" id="txt" />
	<span id="sp"></span>

	<script>
	var txt = document.getElementById('txt'),
	sp = document.getElementById('sp'),
	obj = {}
	
	// 给对象obj添加msg属性，并设置setter访问器
	Object.defineProperty(obj, 'msg', {
	// 设置 obj.msg 当obj.msg反生改变时set方法将会被调用 
	set: function (newVal) {
	// 当obj.msg被赋值时 同时设置给 input/span
	txt.value = newVal
	sp.innerText = newVal
	}
	})
	
	// 监听文本框的改变 当文本框输入内容时 改变obj.msg
	txt.addEventListener('keyup', function (event) {
	obj.msg = event.target.value
	})
	</script>
```

## 动态添加数据的注意点
**注意**：只有data中的数据才是响应式的，动态添加进来的数据默认为非响应式

可以通过以下方式实现动态添加数据的响应式
- Vue.set(object, key, value) 适用于添加单个属性
- Object.assign() 适用于添加多个属性
```js
	var vm = new Vue({
	data: {
	stu: {
	name: 'jack',
	age: 19
	}
	}
	})
	
	/* Vue.set */
	Vue.set(vm.stu, 'gender', 'male')

	/* Object.assign 将参数中的所有对象属性和值 合并到第一个参数 并返回合并后的对象*/
	vm.stu = Object.assign({}, vm.stu, { gender: 'female', height: 180 })
```

## 异步DOM更新
说明：Vue 异步执行 DOM 更新，监视所有数据改变，一次性更新DOM
优势：可以去除重复数据，对于避免不必要的计算和 避免重复 DOM 操作上，非常重要
如果需要那到更新后dom中的数据 则需要通过 Vue.nextTick(callback)：在DOM更新后，执行某个操作（属于DOM操作）

- 实例调用vm.$nextTick(function () {})
```js
	methods: {
	fn() {
	this.msg = 'change'
	this.$nextTick(function () {
	console.log('$nextTick中打印：', this.$el.children[0].innerText);
	})
	console.log('直接打印：', this.$el.children[0].innerText);
	}
	}
```

## 指令
解释：指令 (Directives) 是带有 v- 前缀的特殊属性
作用：当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM

### v-text
解释：更新DOM对象的 textContent
`<h1 v-text="msg"></h1>`
### v-html
解释：更新DOM对象的 innerHTML
`<h1 v-html="msg"></h1>`
### v-bind
作用：当表达式的值改变时，将其产生的连带影响，响应式地作用于 DOM
语法：v-bind:title="msg"
简写：:title="msg"
```js
	<!-- 完整语法 -->
	<a v-bind:href="url"></a>
	<!-- 缩写 -->
	<a :href="url"></a>
```