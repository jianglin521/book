---
title: axios使用
date: 2018/4/1 14:20:48 
tags: axios
categories: axios
---

## axios官网
`npm install axios --save`

**官网地址**
[https://www.npmjs.com/package/axios](https://www.npmjs.com/package/axios)

## 使用
### 全局axios默认值
```js
	axios.defaults.headers.common['Content-Type'] = 'application/json;charset=UTF-8'
```
### 添加自定义token
```js
	//请求添加token
	axios.interceptors.request.use(config => {
	  let token = store.state.token;
	  if (token) {  // 判断是否存在token，如果存在的话，则每个http header都加上token
	    config.headers.Authorization = token;
	    //console.log('interceptors config=',config)
	  }
	  return config
	}, error => {
	  return Promise.reject(error)
	})
```
### 发送get请求
```js
	// 向具有给定ID的用户发出请求
	axios.get('/user?ID=12345')
	  .then( (response) => {
	    console.log(response);
	  })
	  .catch((error) => {
	    console.log(error);
	  });
	 
	// 上述请求也可以如下完成
	axios.get('/user', {
	    params: {
	      ID: 12345
	    }
	  })
	  .then((response) => {
	    console.log(response);
	  })
	  .catch( (error)=> {
	    console.log(error);
	  });
```
### 发送post请求
```js
	axios.post('/user', {
	    firstName: 'Fred',
	    lastName: 'Flintstone'
	  })
	  .then((response) => {
	    console.log(response);
	  })
	  .catch( (error) => {
	    console.log(error);
	  });
```
### 执行多个并发请求
```js
	function getUserAccount() {
	  return axios.get('/user/12345');
	}
	 
	function getUserPermissions() {
	  return axios.get('/user/12345/permissions');
	}
	 
	axios.all([getUserAccount(), getUserPermissions()])
	  .then(axios.spread(function (acct, perms) {
	    // 这两个请求现在都已完成
	  }));
```