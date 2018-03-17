---
title: axios使用
date: 2018/3/17 17:54:21 
tags: Vue
categories: Vue
---

## axios官网
`npm install axios --save`

**官网地址**
[https://www.npmjs.com/package/axios](https://www.npmjs.com/package/axios)

## 使用
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