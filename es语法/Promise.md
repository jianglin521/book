---
title: Promise
date: 2018/4/1 13:49:22 
tags: es语法
categories: es语法
---

## Promise概念
所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

## Promise对象作用
有了Promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise对象提供统一的接口，使得控制异步操作更加容易。

## Promise基本用法
```js
	let p = new Promise(function(resolve, reject){
	    setTimeout(function(){
	        let num = Math.random()
	        if (num > 0.5) {
	            resolve(num)
	        }else{
	            reject(num)
	        }
	    }, 1000)
	})
	p.then(function(num){
	    console.log('大于0.5的数字：', num)
	},function(num){
	    console.log('小于等于0.5的数字', num)
	})
	// 运行第一次：小于等于0.5的数字 0.166162996031475
	// 运行第二次：大于0.5的数字： 0.6591451548308984
```

## Promise.all()
Promise.all能将多个Promise实例包装成一个Promise实例
```js
	let Promise1 = new Promise(function(resolve, reject){})
	let Promise2 = new Promise(function(resolve, reject){})
	let Promise3 = new Promise(function(resolve, reject){})
	
	let p = Promise.all([Promise1, Promise2, Promise3])
	
	p.then(funciton(){
	  // 三个都成功则成功  
	}, function(){
	  // 只要有失败，则失败 
	})
```


