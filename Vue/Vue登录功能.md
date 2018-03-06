---
title:  Vue登录功能
date: 2018/3/4 11:19:58 
tags: Vue
categories: Vue
---

## vue登录功能
链接地址 [http://www.mamicode.com/info-detail-1909572.html](http://www.mamicode.com/info-detail-1909572.html)
通过判断该用户是否登录过，如果没有登录则跳转到login登录路由，如果登录则正常跳转。

### 首先在用户登录前后分别给出一个状态来标识此用户是否登录（建议用vuex）
```js
	import Vue from 'vue'
	import Vuex from 'vuex'
	
	Vue.use(Vuex);
	
	var state = {
	    isLogin:0,    //初始时候给一个  isLogin=0  表示用户未登录
	};
	
	const mutations = {
	    changeLogin(state,data){
	        state.isLogin = data;
	    }
	};
```
###  在用户登录时改变登录状态
```js
  this.$store.commit('changeLogin','100')     //登录后改变登录状态 isLogin = 100 ；
```

### 重点来了
在你的路由入口加上导航钩子，具体什么意思看代码

#### 设置需要校验的路由
```js
  { path: '/admin', 
    component: Admin,
    meta:{auth:true}  // 设置当前路由需要校验   不需要校验的路由就不用写了；不要问为什么，自己去看官网
   }   
```
#### 路由跳转并校验
```js
	router.beforeEach((to,from,next) => {
	    if(to.matched.some( m => m.meta.auth)){
	        // 对路由进行验证
	        if(store.state.isLogin==‘100‘) { // 已经登陆
	            next()     // 正常跳转到你设置好的页面
	        }else{
	            // 未登录则跳转到登陆界面，query:{ Rurl: to.fullPath}表示把当前路由信息传递过去方便登录后跳转回来；
	　　 　　　　next({path:'/login',query:{ Rurl: to.fullPath} })
	 　　　　　} 
	　　　　}else{ 
	　　　　　　next() 
	　　} 
	})
```
