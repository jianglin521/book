## vuex
Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式

官网地址
[https://vuex.vuejs.org/zh-cn/api.html](https://vuex.vuejs.org/zh-cn/api.html)

## vuex原理
![](https://i.imgur.com/Z81hKSZ.png)

- dispatch可以是view视图中触发，也可以是程序业务逻辑来触发
- actions通过commit方法发出一个改变事件
- mutations中具体操作state的改变
- state的改变通过getter暴露给view，state改变后会立即通知用getter关联起来的view。
- 创建一个Vuex.Store的实例，用于Vue实例。

## 安装
`npm install vuex --save`

## 使用
在 src 下新建文件夹 vuex，进入 vuex 新建 store.js

然后去 main.js 加入
```js
	import store from './vuex/store'
```
再修改 Vue 实例如下
```js
	new Vue({
	  el: '#app',
	  router,
	  store,
	  render: h => h(App)
	})
```
我们去新建的 store.js
```js
	import Vue  from 'vue';
	import Vuex from 'vuex';
	
	Vue.use(Vuex)
	
	export default new Vuex.Store({
	  state: {
	    platform: ''
	  },
	  mutations: {
	    SET_APP(state, platform) {
	      state.platform = platform;
	    }
	  },
	  actions: {
	    setApp({commit}, platform) {
	      commit('SET_APP', platform);
	    }
	  },
	  getters: {
	    getApp: (state) => state.platform
	  }
	})
```