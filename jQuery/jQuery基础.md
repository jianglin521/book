---
title: jQuery基础
date: 2018/2/23 17:11:19 
tags: jQuery
categories: jQuery
---


## jQuery基础
## 效果 - 隐藏和显示
jQuery hide() 和 show()
通过 jQuery，您可以使用 hide() 和 show() 方法来隐藏和显示 HTML 元素：
```js
	$("#hide").click(function(){
	  $("p").hide();
	});
	
	$("#show").click(function(){
	  $("p").show();
	});
```