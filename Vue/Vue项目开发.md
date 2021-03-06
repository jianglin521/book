---
title: Vue项目开发
date: 2018/1/27 18:12:08 
tags: Vue
categories: Vue
---

## vue安装
### 全局安装 vue-cli
`npm install --global vue-cli`

### 创建一个基于 webpack 模板的新项目
 `vue init webpack my-project`

## stylus安装
`npm install stylus stylus-loader --save-dev`

**stylus编写样式**
```js
<style lang="stylus" rel="stylesheet/stylus">

</style>
```

## 安装mockjs
`npm install mockjs --save-dev`

**官方网站** [http://mockjs.com/](http://mockjs.com/)

### 简单使用
mockServer.js内容
```js
	//引入mockjs
	import Mock from 'mockjs'
	//创建数据
	let data = Mock.mock({
	  'goods|100': [{
	    'id|+1': 1,
	    //出生年月
	    'date': '@date("yyyy-MM-dd")',
	    // 邮箱
	    'email': '@email',
	    // 汉字姓名
	    'name': '@cname()',
	    // 地址
	    'address': '@province' + '@city' + '@county',
	    // 手机号
	    'phone': /^1[385][1-9]\d{8}/
	  }]
	})
	//console.log(JSON.stringify(data, null, 4))
	
	// 映射几个接口
	Mock.mock('/api/goods', {
	  code: 0,
	  data: data.goods
	})
	
	//只需要让当前文件被执行一次即可
```
### 模拟数据
```js
	Mock.mock(template)
	Mock.mock(rurl,function(options))
	Mock.mock(rurl,rtype,template)
	Mock.mock(rurl,rtype,function(options))
```
- template表示数据模板，可以是{'data|1-10':[{}]}也可以是’@EMAIL’
- rurl表示要拦截的地址，可以使普通的url如http://c.cn，也可以是url正则表达式/\.json/
- rtype表示需要拦截的 Ajax 请求类型。例如 GET、POST、PUT、DELETE 等。
- funtion(options)表示用于生成响应数据的函数。
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
