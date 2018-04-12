---
title: js异步
date: 2018/4/1 13:49:22 
tags: es语法
categories: es语法
---

## Promise概念
所谓Promise，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理。

### Promise对象作用
有了Promise对象，就可以将异步操作以同步操作的流程表达出来，避免了层层嵌套的回调函数。此外，Promise对象提供统一的接口，使得控制异步操作更加容易。

### Promise基本用法
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

### Promise.all()
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
----------

## async/await
异步是JavaScript的一大难点之一，因此js的异步解决方案也是多种多样的。从最早的回调函数，到Promise对象，到Generator函数，再到现在的async/await。很多人都认为async/await是异步操作的终极解决方案

async/await 这名字取得就很语义化，async声明一个异步function，await用于等待异步function执行完成。并且语法规定，await只能出现在async函数中。

```js
	function test1() {
	    return 'test'
	}
	function testAsync(n) {
	    return new Promise((resolve, reject) => {
	        setTimeout(() => {
	            resolve(n)
	        }, 1000)
	    })
	}
	
	async function test() {
	    const result1 = await test1()    
	    console.log(result1)
	    const result2 = await testAsync(999)
	    console.log(result2)
	}
	
	test()
	
	console.log('同步代码')
```
上述代码首先打出了"同步代码"，随后又立即打出"test"，并在一秒后打出了"999"。
我们可以得出以下结论：

- await会阻塞它所在的异步函数的后面代码的执行(因为它需要等到testAsync函数的结果才会往下执行)，但是不会阻塞异步函数之外的代码的执行(因为先打印的"同步代码")，其实它内部的阻塞都被封装到一个Promise对象中异步执行，我想可能是因为这样await才必须在async函数中吧。
- 如果await等到的不是Promise对象的话会将它转成立即resolve的Promise对象，并将该值作为await表达式的结果(打印完"同步代码"之后立即打出"test")；如果是的话就等着Promise对象resolve()，然后将resolve的结果作为await表达式的结果(一秒后打印"999")。

在async函数中，这样的代码看起来就像是同步代码，await等待到结果才执行后面的语句，但是却不会阻塞async函数之外的代码的执行。


