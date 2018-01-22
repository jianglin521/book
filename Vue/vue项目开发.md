---
title: vue项目开发
date: 2018/1/21 21:45:16 
tags: vue
categories: vue
---

## vue安装
### 全局安装 vue-cli
`npm install --global vue-cli`

### 创建一个基于 webpack 模板的新项目
 `vue init webpack my-project`


## 安装stylus
`npm install stylus stylus-loader --save-dev`

**stylus编写样式**
```js
<style lang="stylus" rel="stylesheet/stylus">

</style>
```

## 安装mockjs
`npm install mockjs --save-dev`
**mockjs官网**：http://mockjs.com/

### 简单使用
mockServer.js内容
```js
	import Mock from 'mockjs'
	let data = Mock.mock({
	  'goods|50': [{
	    'id|+1': 1,
	    //出生年月
	    'date': '@date("yyyy-MM-dd")',
	  }],
	})
	// 映射几个接口
	Mock.mock('/api/goods', {
	  code: 0,
	  data: data.goods
	})	
	//只需要让当前文件被执行一次即可
```
在main.js中添加
`import './mock/mockServer'`

## 编码测试与打包发布项目
### 编码测试
`npm run dev`
访问: http://localhost:8080
编码, 自动编译打包(HMR), 查看效果

### 打包发布
`npm run build`
`npm install -g pushstate-server`
`pushstate-server dist`
访问: http://localhost:9000
