---
title: DOM2.0
date: 2018/1/7 16:02:27 
tags: js高级
categories: js高级
---

## DOM2.0
## DOM规范
DOM是独立于平台和语言的接口，任何语言可以实现DOM规范. 该接口为程序和脚本提供了对文档的内容、结构和样式的动态获取和更新的功能。
DOM0：不是W3C规范。
DOM1：开始是W3C规范。专注于HTML文档和XML文档。
DOM2：对DOM1增加了样式表对象模型(DOM2)
DOM3：对DOM2增加了内容模型 (DTD 、Schemas) 和文档验证。

## DOM 添加
- document.createElement() 创建新的元素节点
	- 返回值指向新建节点的引用指针,是一个元素节点. 
	- nodeType 属性值等于 1
	- 新元素节点不会自动添加到文档里. 只在JS上下文中
- document.createTextNode() 创建新的文本节点
	- 返回值指向新建文本节点引用指针,是一个文本节点
	- nodeType 属性等于 3
- document.createAttribute() 创建新的属性节点
- appendChild() 为元素节点添加子节点到最后一位
	- 返回值是一个指向新增子节点的引用指针
- insertBefore() 插入节点
	- 第一个参数: 要插入的子节点
	- 第二个参数: 要添加新的节点前的子节点
- cloneNode() 复制子节点. 第二个参数传true深度克隆

## DOM 删除
- removeChild() 从给定元素里删除一个子节点
	- 返回值是一个指向已被删除的子节点的引用指针
- removeAttribute() 删除属性节点的值
	
## DOM 修改
- innerHTML. 获取设置html文本
- innerText. 获取设置文本
- setAttribute() 设置属性节点的值
	- 第一个参数: 属性名
	- 第二个参数: 修改的值
- replaceChild() 替换节点
	- 第一个参数: 要插入的子节点
	- 第二个参数: 被替换的节点

## DOM 查询
- getElementById 通过元素ID获取
- getElementsByTagName 通过标签名获取一组元素
- querySelector("选择器") 获取一个元素
- querySelectorAll("选择器") 获取多个元素
- getAttribute() 获取属性节点的值
- parentNode 属性可返回某节点的父节点
- childNodes 属性返回包含被选节点的子节点的 NodeList
- children 获取指定节点的所有子节点(无空白文档)
- firstChild 获取第一个子节点 (nodeValue属性来获取文本值)
- lastChild 获取最后一个子节点 (nodeValue属性来获取文本值)
- previousSibling 属性可返回某节点之前紧跟的节点
- nextSibling 属性可返回某个元素之后紧跟的节点（处于同一树层级中）

## DOM0事件
- DOM0事件绑定: xxx.onclick = fn;
	- 默认冒泡
	- 一个元素上只能绑定一个同类事件,如果继续绑定的话,第二个事件函数会覆盖第一个
- DOM0事件解绑: xxx.onclick = null;
	- 最后一次注册事件设置成null


## DOM2事件
- IE绑定事件: xxx.attachEvent(事件名称，事件函数);
	1. 没有捕获. 默认冒泡
	2. 事件名称有on
	3. 事件执行的顺序:IE8以下为倒序. IE8及以上为正序
	4. this指向window
- 标准绑定事件: xxx.addEventListener(事件名称，事件函数，是否捕获);
	1. 第三个参数设置是否捕获:默认false:冒泡; true：捕获
	2. 事件名称没有on
	3. 事件执行的顺序是正序
	4. this触发该事件的对象 
	5. 一个元素上可以绑定多个同类事件,它们都会被执行
- DOM2解绑: removeEventListener("事件名称", "事件回调", "捕获/冒泡")

## 兼容浏览器DOM2绑定方法 (同步this)
```js
	function bind(obj, evname, fn) {
		if (obj.addEventListener) {//除ie低版本外都可以进入
			obj.addEventListener(evname, fn, false);
		} else {
			obj.attachEvent('on' + evname, function() {
				fn.call(obj);
			});
		}
	}

	bind(document, 'click', fn1);
```

## 取消冒泡
- DOM0: event.cancelBubble = true;
- DOM2: event.stopPropagation();

## 获取视口宽度
document.documentElement.clientWidth (文档的根节点)

## clientWidth & offsetWidth
- clientWidth = 内容区Width + paading. 可视区域. 可以渲染背景的区域 
- offsetWidth = 内容区Width + padding + border. 根节点的border-box

## 怪异盒模型
- 怪异盒模型 = 内容区 + padding + border
- clientWidth =  width - border
- offsetWidth =  width

## scrollTop & scrollLeft
- 页面上元素滚动的距离
- document.documentElement.scrollTop || document.body.scrollTop;
- document.documentElement.scrollLeft || document.body.scrollLeft;

## scrollHeight & scrollWidth
- 如果没有子元素溢出, scrollHeight或者scrollWidth获得就是自己的尺寸
- 如果子元素溢出, 父元素的scrollHeight或者scrollWidth就是子元素的height和width
- scrollHeight & scrollWidth 可以获得子元素真实的大小

## parentNode
返回指定节点的父节点

### parentNode面试题

    <div>1 <a href="javascript:;">删除</a> </div>
    <div>2 <a href="javascript:;">删除</a> </div>
    <div>3 <a href="javascript:;">删除</a> </div>
    <div>4 <a href="javascript:;">删除</a> </div>
    <div>5 <a href="javascript:;">删除</a> </div>

    var all = document.getElementsByTagName('a');

    //循环遍历加监听
    for (var i = 0; i < all.length; i++) {

      (function (i) {
      	  all[i].onclick = function () {
      	  	  all[i].parentNode.style.display = "none";
      	  }
      })(i)
    }

	//this方法
	for (let i = 0; i < all.length; i++) {

      	  all[i].onclick = function () {
      	  	  this.parentNode.style.display = "none";
      	  }
    }

## offsetParent 规则
- 返回一个指向最近的包含该元素的定位元素
- 前提: html和body之间的margin被重置为0
	- 本身定位不是fixed
		- 如果有定位父级 ==> 定位父级
 	    - 如果没有定位父级 ==> body
	- 本身定位是fixed
 	    - ==> offsetParent:null (谷歌.苹果.ie7以上)
        - ==> offsetParent:body (火狐)


## offsetTop & offsetLeft
- offsetTop返回当前元素相对于其 offsetParent 元素的padding顶部的距离。
- offsetLeft返回当前元素相对于其 offsetParent 元素的padding左边界的距离。
- 规则
	- 本身定位不是 fixed ==> offsetParent
	- 本身定位是 fixed ==> 视口
	
## getBoundingClientRect()
- 返回元素的大小及其相对于视口的位置
- 相对坐标: (参照视口)
	- left 和 top 是元素左上角距离视口的坐标
	- right 和 bottom 是元素右上角距离视口的坐标
- 绝对坐标: (有滚动条时. 参照初始包含块)
	- left不会变化. top用来确定元素离视口的坐标
	- right不会变化. bottom用来确定元素离视口的坐标


## 检测低版本IE方法
```js
    function isIe(v) {
    	var b = document.createElement("b");
    	b.innerHTML = "<!--[if IE "+ v +"]><i></i><![endif]-->";
        return b.getElementsByTagName("i").length == 1;
    }
```

## PC端拖拽方案
- 实现原理:
	1. 获得元素开始位置
	2. 获得鼠标移动距离
	3. 鼠标移动距离加上元素开始位置
- 实现步骤:
	1. 元素开启绝对定位并且初始化元素和鼠标的位置 {x:0, y:0}
	2. 在鼠标按钮按下时(onmousedown)
	3. 基于offsetParent 获得元素开始位置 (offsetLeft/Top)
	4. 基于视口 获得鼠标开始位置 (clientX/Y)
	5. 在元素身上全局捕获 (兼容IE8) setCapture
	6. 鼠标移动时 (onmousemove). 该方法要在onmousedown里实现
	7. 初始化鼠标实时位置. 并获取(clientX/Y)
	8. 获得鼠标移动距离: 鼠标实时位置 - 鼠标开始位置
	9. 获得元素拖拽的位置: 元素开始位置 + 鼠标移动距离
	10. 在鼠标按钮抬起时 (onmouseup) 解绑dom0 事件
	11. 在onmouseup里document身上释放全局捕获 (releaseCapture)
	
### 拖拽实例
```js
    var box = document.getElementById('box');

    //初始化元素的位置
    var elementStart = {x:0, y:0};
    //初始化鼠标的位置
    var mouseStart = {x:0, y:0};

    //在鼠标按钮按下时获得初始位置 (移动端: 手指滑动的距离)
    test.onmousedown = function (e) {
    	  var e = e ||event;

      //1.基于offsetParent  获得元素开始的位置
      elementStart.x = test.offsetLeft;
      elementStart.y = test.offsetTop;

    	//2.基于视口 获得鼠标一开始的位置
      mouseStart.x = e.clientX;
      mouseStart.y = e.clientY;

      //全局捕获(兼容IE8)
      if(test.setCapture){
        test.setCapture;
      }

      //鼠标被移动时
      document.onmousemove = function (e) {
        var e = e ||event;
        //3.鼠标实时的位置
        var mouseMove = {x:0, y:0};
        mouseMove.x = e.clientX;
        mouseMove.y = e.clientY;

        //4.鼠标移动的距离
        var dis = {x:0, y:0};
        dis.x = mouseMove.x - mouseStart.x;
        dis.y = mouseMove.y - mouseStart.y;

        //5. 元素开始的位置加上鼠标移动的距离
        test.style.left = elementStart.x + dis.x +"px";
        test.style.top = elementStart.y + dis.y +"px";
      };

      //鼠标按钮抬起时
      document.onmouseup = function () {
        //dom0解绑事件
        document.onmousemove = document.onmouseup = null;
        //释放全局
        if(document.releaseCapture){
          document.releaseCapture
        }
      }
	 //处理主流浏览器 取消默认行为
      return false
    }
```

### PC端拖拽模版
```js
    //在鼠标点击时
    elem.onmousedown = function (e) {
      var e = e || event;

      //全局捕获(兼容IE8) 最好放在onmousedown里
      if(elem.setCapture){
        elem.setCapture;
      }

      //鼠标移动时
      document.onmousemove = function (e) {
        var e = e || event;
      };

      //鼠标抬起时取消事件
      document.onmouseup = function () {
          document.onmousemove = document.onmouseup = null;

          //释放全局
          if(document.releaseCapture){
            document.releaseCapture
          }
      }
		 return false
    }
```

## 扇形导航
- 样式布局
	1. 有三个结构: 最外层包裹元素. 菜单元素. 主home键元素
	2. 给三个结构设置固定宽高值并开启绝对定位 (到底部: bottom&right)
	3. 为菜单图片设置绝对定位叠加到一起. left&top为0 设置圆角
	4. home键元素添加背景图并且设置圆角.z-index提升层级
- 实现思路
	1. 点击home键按钮旋转. 预定义flag为true. 当点击时判断, flag是true,则transform旋转负的xx角度. 否则就是0度. 每次调用完置空flag
	2. 给home元素样式里添加过渡时间
	3. 根据半径和图片到home键之间的角度求出图片所在的坐标
	4. 需要传入 定义的半径长度和角度
	5. 通过Math.sin()方法求出对边x的坐标. 参数: 弧度
		- 角度转弧度公式 =  角度 * π / 180
		- 得出sin结果乘以半径长度得到对边坐标
	6. 通过Math.cos()方法求出邻边y的坐标. 参数: 弧度
		- 得出cos结果乘以半径长度得到邻边坐标
	7. 该方法return出一个对象  {x:x,y:y}
	8. 当flag为true时, 循环遍历出所有图片并显示
	9. 显示方式: 过渡 + 旋转
	10. 图片坐标通过之前定义的方法获得
	11. 当flag为false时, 循环遍历出所有图片并隐藏
	12. 循环遍历所有图片,在点击时给图片添加动画样式
	13. 过渡 + 缩放旋转 + 透明
	14. 定义 transitionend 的事件监听. 过渡完成后恢复样式并解绑
### 代码实现
```js
	<div id="wrap">
       <div id="menu">
         <img src="img/clos.png" alt="">
         <img src="img/full.png" alt="">
         <img src="img/open.png" alt="">
         <img src="img/prev.png" alt="">
         <img src="img/refresh.png" alt="">
       </div>
       <div id="home"></div>
    </div>

	* {
      margin: 0;
      padding: 0;
    }

    #wrap{
      position: absolute;
      bottom:20px;
      right: 20px;
      width: 50px;
      height: 50px;
    }
    #menu{
      position: absolute;
      width: 50px;
      height: 50px;
    }

    #wrap img{
      /*1. 让图标叠到一起*/
      position: absolute;
      left:0;
      top: 0;
      /*去除边角*/
      margin: 4px;
      border-radius: 99%;
    }

    #home{
      height: 50px;
      width: 50px;
      background: url("img/home.png") no-repeat;
      /*去除边角*/
      border-radius: 99%;
      /*2. 看到home键 提高层级*/
      position: relative;
      z-index: 99;

      transition: 1s;
    }




    var home = document.getElementById('home');
    var imgs = document.getElementById('menu').getElementsByTagName('img');

    //1. 实现home按钮旋转 (第一下逆时针)
    var flag = true;
    var c = -120;
    home.onclick = function () {
        if (flag){
          this.style.transform = "rotate(-1440deg)";

          //2. 遍历得到每一个图片. 让图片去指定位置
          for (var i = 0; i < imgs.length; i++) {
            imgs[i].style.transition = ".5s " + (i*0.1)+"s";
            imgs[i].style.transform = "scale(1) rotate(-720deg)";
            imgs[i].style.left = getPoint(c,(90/(imgs.length-1)) * i).x +"px";
            imgs[i].style.top = getPoint(c,(90/(imgs.length-1)) * i).y +"px";
          }
        }else{
          this.style.transform = "rotate(0)";

          for (var i = 0; i < imgs.length; i++) {
            imgs[i].style.transition = ".5s " + ((imgs.length - 1 - i)*0.2)+"s";
            imgs[i].style.transform = "scale(1) rotate(0)";
            imgs[i].style.left = 0;
            imgs[i].style.top = 0;
          }
        }
      flag = !flag
    };

    //完善小图标
    for (var i = 0; i < imgs.length; i++) {
      imgs[i].onclick = function () {
          this.style.transition = ".5s";
      	  this.style.transform = "scale(2) rotate(-720deg)";
          this.style.opacity = 0.1;

        this.addEventListener("transitionend",fn)
      };
    }

    //完成后解绑 transitionend
    function fn() {
      this.style.transition = ".2s";
      this.style.transform = "scale(1) rotate(-720deg)";
      this.style.opacity = 1;

      this.removeEventListener("transitionend",fn)
    }


    //根据第三条边和角度 求出元素的坐标
    function getPoint(c,deg) {
        //x 对边 b 底边 c 直角边
        //角度转弧度: 角度 * π / 180
    	  var x = Math.round(Math.sin(deg*Math.PI/180) * c);
        var y = Math.round(Math.cos(deg*Math.PI/180) * c);
        return {x:x,y:y};
    }
```

![](http://i.imgur.com/ZuOg4Zz.png)