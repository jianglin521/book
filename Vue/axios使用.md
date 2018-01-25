---
title: axios使用
date: 2018/1/25 21:12:10 
tags: vue
categories: vue
---

## axios使用
## 下载
`npm install axios --save-dev`

**官网地址**
[https://www.npmjs.com/package/axios](https://www.npmjs.com/package/axios)

## 使用
### 发送get请求
```js
	axios.get('/user?ID=12345')
	  .then( (response) => {
	    console.log(response);
	  })
	  .catch(error) => {
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