---
title:  Vue组件通信
date: 2018/2/1 20:42:47 
tags: Vue
categories: Vue
---

## 父组件数据传递给子组件
父组件
```js
	<parent>
	    <child :child-msg="msg"></child>//这里必须要用 - 代替驼峰
	</parent>
	
	data(){
	    return {
	        msg: [1,2,3]
	    };
	}
```
子组件
```js
	props: {
	    childMsg: Array //这样可以指定传入的类型，如果类型不对，会警告
	}
```

## 子组件与父组件通信
父组件
```js
	<div>
	    <child @upup="change" ></child> //监听子组件触发的upup事件,然后调用change方法
	</div>
	
	methods: {
	    change(msg) {
	        this.msg = msg;
	    }
	}
```
子组件:
```js
	<div @click="up"></div>
	
	methods: {
	    up() {
	        this.$emit('upup','hehe'); //主动触发upup方法，'hehe'为向父组件传递的数据
	    }
	}
```