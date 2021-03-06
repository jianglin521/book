---
title: js数据类型
date: 2018/3/4 10:40:15 
tags: js
categories: js
---

## Javascript中的数据类型
## 基本数据类型
是对值的操作；放在栈内存里面，栈内存是js代码执行的环境，存放轻量级的数据

### 数值Number
- NaN属于Number数据类型，跟任何值都不相等，包括它自己
- isNaN()：判断是否是非有效数字；是非有效数字：true，是有效数字：false

### 字符串String
- 字符串和任何值相加

### 布尔Boolean

### Null

### undefined
- `null==undefined` 得到的是true
- `null===undefined` 得到的是false
- 产生undefined的情况
    1. 变量未定义
    2. 函数没有设置return的时候，用一个变量去接收其的返回值是undefined；即使设置了return，但是后面没有语句，那么获得的函数返回值也是undefined
    3. 对象身上的属性不存在的时候，获取的是undefined
    4. 如果定义了形参，但是没有传入实参，获取得也是undefined

### undefined+undefined=NaN

----------

## 引用数据类型
对地址的操作；开辟一个新的空间地址，存放在堆内存；对象以键值对的方式存储，数组是以字符串的方式存储；把空间地址赋值给一个变量名，指向当前的这个空间（堆内存）；堆内存里面存放的是js代码的字符串（也就是函数的定义阶段），执行js代码要到栈内存里面（也就是函数的调用阶段）

### 对象数据类型
- 数组[]
	- 字面量方式创建：var ary=[]
	- 对象实例创建：var ary=new Array()
- 对象{}
	- 两个基本的特征：属性（没有括号）和方法（有括号）；键值对展示对象的特性
	- var obj={}
	- var obj=new Object()
	- 遍历对象的方法：for(var a in obj){}
- 正则RegExp()
- 日期对象new Date()

### 函数数据类型
- 函数function
	- 最重要的是**封装**
	- 只定义函数，不调用函数（函数（）），函数不会执行
	- 定义阶段：
		1. 开辟一个新的空间地址，堆内存
		2.  把函数体内的所有`js`代码都作为**字符串**存储在这个堆内存里面
		3.  把这个堆内存的地址赋值给函数名
	- 调用阶段：
		1. 函数调用，会形成一个私有作用域
		2. 把以前的存储在堆内存里面的`js代码字符串`拿到栈内存作为`js代码`进行执行
	- 函数自带参数机制：arguments
		1. 可以获取到函数传入的实参，并且以`类数组`的形式展现或者打印；其是一个对象，有属性和方法
		2. arguments.callee：拿到的是当前函数本身，包括注释
		3. arguments.length：拿到的是实参的个数
		4. 解决参数个数不确定而无法传入的问题
		5. 形参是私有变量

----------

## 数据类型检测的方法
1. typeof：可以检测基本数据类型，但是对于对象数据类型，检测出来的都是object,无法知道具体属于哪种对象。
2. 对象 instanceof 类：比如ary instanceof Array判断这个实例对象是否属于某个类
3. 对象.constructor：比如ary.constructor可以打印出对象所属的类
4. Object.prototype.toString.call(ary)：出来的结果[object Array]

----------

## 数据类型的真假
- 除了假都是真
- 假false 6种
	- false
	- 空字符串''
	- 0
	- NaN
	- null
	- undefined

----------

## 数据类型的转换
- 字符串类型与数值类型之间的转换
	- 严格转换
		- Number()
	- 非严格转换
		- parseInt(传入要转化为整数的小数或者数字字符串)：只能转化为整数，不会进行四舍五入，向下取整，从前往后转
		- parseFloat(传入要转化的小数或者数字字符串)；可以保留小数
		- 返回的都是Number数据类型，转换失败得到NaN，也是Number数据类型

----------

## 隐式数据类型的比较
- []默认通过自身的toString()转成空字符串''，再通过Number('')转为0
- null默认隐式转换为0故：null+10=10
- 对象==对象  不相等，对地址的引用
- 对象==字符串 默认都转成字符串比较 特殊：""=={} 相等
- 对象==数值 默认转为数值比较 特殊：0==[]相等 0=={} 不相等
- 对象==布尔值 默认转为数值 特殊：false==[] 相等 ![]==[] 相等
- 数值==字符串 默认是转数值 特殊：0=="" 相等

