---
title: js数组
date: 2018/4/8 15:49:34 
tags: js
categories: js
---

## 数组常用方法
- push：向数组的末尾增加一项 返回值是数组的新长度
- unshift：向数组开头增加一项 返回值是数组的新长度
- pop:删除数组的末尾项 返回值是删除的数组项
- shift:删除数组开头项 返回被删除的开头项目
- splice：删除数组中的任意项 返回值是被删除的数组项
- slice:复制数组 返回值是复制到的新数组 写上数值之后 不包含被复制的最后一项

拼接：
- concat:把一个数组和另一个数组拼接在一起 返回拼接好的数组 
- join:把数组中的每一项 按照指定的分隔符拼接成字符串

排序：
- reverse:倒序数组 返回值倒序数组 原有数组改变
- sort:根据匿名函数进行冒泡排序 b-a倒序 a-b升序

兼容性不好：
- indexOf:返回获取项在数组中的索引
- lastIndexOf:返回获取项在数组中出现的最后一次索引
- forEach: 循环遍历数组 参数是一个匿名函数 默认返回为undefined
- map：循环遍历数组 参数是一个匿名函数

splice的拓展使用：
- 模拟push   ary.splice(ary.length,0,x)
- 模拟pop    ary.splice(ary.length-1,1)
- 模拟unshift   ary.splice(0,0,x)
- 模拟shift     ary.splice(0,1)
- splice(0) 从0开始删除到末尾==>全部删除的操作 ==>返回所有数组项 ==> 克隆数组

```js
    var ary = [1,2,3,4,5,6,7,8,9,0];
    var ary1=[1,5,7,4];
    var ary2=[2,3,4,5,7,3,4,5];
    var a=ary.splice(2,3,5);//删除数组中的任意项  可引申为push,unshift,pop,shift,slice最为常用
    var b=ary.splice(2,1);
    /*var a="test";
    var b=[123]; 供forEach测试使用*/
    var c=ary.push(1);//在数组的末尾增加一项
    var d=ary.unshift(3);//在数组的开头增加一项
    var e=ary.pop();//在数组的末尾删除一项
    var f=ary.shift();//在数组的开头删除一项
    var g=ary.slice(2,5);//复制数组
    var h=ary.concat(ary1,ary2).concat(1,2,2,2,2,[456654]); //如果没有参数 或者参数为（）空则为赋值数组
    var i=ary.join('+');//将数组中的每一项用指定的分隔符拼接成一个新的字符串
    var j=ary.reverse();//倒序排序  原有数组改变
    var k=ary1.sort(function(a,b){return b-a;});
    var l=ary2.indexOf(4);//返回获取项在数组中出现的索引
    var m=ary2.lastIndexOf(4);//返回获取项在数组中出现的最后一次索引
    var n=ary2.indexOf(9);//若获取项不存在则返回-1
    var o=ary.forEach(function(a,b){console.log(a,b)});
    var p=ary2.map(function(){});
```


