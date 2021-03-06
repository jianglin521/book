---
title: Vue重要属性
date: 2017-12-24 10:05:43
tags: Vue
categories: Vue
---

## 计算属性
- 计算
	1. 在compute属性对象中定义计算属性的方法
	2. 在页面中使用{{方法名}}来显示计算的结果
- 监视
	1. 通过vm对象的$watch()来监视指定的属性
    2. 当属性变化时, 回调函数自动调用, 在函数内部进行计算
- 高级
	- 在compute属性里定义方法通过get/set方法实现对属性数据的显示和监视
	- get方法用来得到当前属性值
	- set方法用来监视当前属性值的变化
- 计算属性特点: 有缓存. 在页面中多次读取数据只调用一次get方法
```js	
	<script type="text/javascript" src="../js/vue.js"></script>
	<script type="text/javascript">
	  var vm = new Vue({
	    el: '#demo',
	    data: {
	      firstName: 'Kobe',
	      lastName: 'bryant',
	      fullName2: 'Kobe bryant'
	    },
	
	    computed: {
	
	      fullName: function () {
	        return this.firstName + " " + this.lastName
	      },
	
	      fullName3: {
	        get: function () {
	          return this.firstName + " " + this.lastName
	        },
	        set: function (value) {
	          var names = value.split(' ')
	          this.firstName = names[0]
	          this.lastName = names[1]
	        }
	      }
	    },
	
	    watch: {
	      lastName: function (newVal, oldVal) {
	        this.fullName2 = this.firstName + ' ' + newVal
	      }
	    }
	  })
	
	  vm.$watch('firstName', function (val) {
	    this.fullName2 = val + ' ' + this.lastName
	  })
	</script>
```

#### 绑定class和style属性
- 以变量的形式绑定class `:class="a"`
- 以对象的形式绑定class `:class="{ 'class-a': isA, 'class-b': isB }" ` isA和isB是布尔值型的data属性
- 以数组的形式绑定class `:class="[classA, classB]"` classA和classB是字符串值
- `:style="{color:'red', fontSize: fontSize + 'px'}" `
	- 属性名要使用驼峰命名
	- 属性值要求是字符串.也可以是data的属性

#### 过渡
- 利用Vue去操控css动画
- transition / animation
- 使用
	- <div v-show='a' v-if='a' transition='xxx'>
	- 定义CSS样式
		- .xxx-transition -- 指定transition或animation
		- .xxx-enter
		- .xxx-leave
	- 也可以使用动画回调钩子
		- Vue.transition('el指定的选择器对象', {配置回调函数})
		- beforeEnter:function(el){} //开始进入之前
		- enter:function(el){} //开始进入
		- afterEnter:function(el){} //进入完成后
		- enterCancelled:function(el){} 
		- beforeLeave:function(el){} //开始离开之前
		- leave:function(el){} //开始离开
		- afterLeave:function(el){} //离开完成之后
		- leaveCancelled:function(el){} 
