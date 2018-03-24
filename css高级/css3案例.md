---
title: css3案例
date: 2018/3/24 14:29:56 
tags: css高级
categories: css高级
---

## 开关按钮
用纯CSS写一个左右滑动的开关按钮
```css
	/*关闭状态*/
	<div class="dashDiv">
	   <span class="dashSpan"></span>
	</div>
	
	/*开通状态*/
	<div class="dashDivSelectd">
	   <span class="dashSpan"></span>
	</div>

	/*关闭状态*/
	.dashDiv{
	    float: right;
	    border-radius: 1.8667rem;
	    border: 0.03rem solid #cbcbcb;
	    background-color: #FFFFFF;
	    width: 1.26667rem;
	    height: 0.613333rem;
	    margin-top: 0.5rem;
	    margin-right: 0.4rem;
	    box-sizing: border-box;
	}
	.dashDiv .dashSpan{
	    border-radius: 50%;
	    border: 0.03rem solid #cbcbcb;
	    background-color: #FFFFFF;
	    float: left;
	    margin-left: 0.04rem;
	    margin-top: 0.019rem;
	    width: 0.506rem;
	    height: 0.506rem;
	    box-sizing: border-box;
	}
	/*开通状态*/
	.dashDivSelectd{
	    background-color: #4cd964;
	    transition: .5s;
	    border-radius: 1.8667rem;
	    border: 0.03rem solid #FFFFFF;
	    width: 1.26667rem;
	    height: 0.613333rem;
	    margin-top: 0.5rem;
	    margin-right: 0.4rem;
	    float: right;
	    box-sizing: border-box;
	
	}
	
	.dashDivSelectd .dashSpan{
	    border-radius: 50%;
	    border: 0.03rem solid #FFFFFF;
	    background-color: #FFFFFF;
	    float: right;
	    margin-right: 0.04rem;
	    margin-top: 0.019rem;
	    width: 0.506rem;
	    height: 0.506rem;
	    box-sizing: border-box;
	}
```






