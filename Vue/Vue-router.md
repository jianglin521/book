---
title: Vue-router
date: 2018/3/20 21:45:45 
tags: Vue
categories: Vue
---

## 全局路由守卫
main.js添加
```js
	// 全局路由守卫
	router.beforeEach((to,from,next) => {
	  if(to.matched.some( m => m.meta.auth)){
	    // 本地存储
	    if (window.sessionStorage.getItem("token")) {
	     let token = JSON.parse(window.sessionStorage.getItem("token")) ;
	     store.state.token = token.authorization
	      //console.log(store.state.token);
	    }
	    // 对路由进行验证
	    if(store.state.token !== '') { // 已经登陆
	      next()  // 正常跳转到你设置好的页面
	    }else{
	      // 未登录则跳转到登陆界面，query:{ Rurl: to.fullPath}表示把当前路由信息传递过去方便登录后跳转回来；
	      next({path:'/login',query:{ Rurl: to.fullPath} })
	    }
	  }else{
	    next()
	  }
	})	
```
router/index.js添加
```js
	meta:{auth:true}
```
