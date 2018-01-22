---
title: 前端css3
date: 2017-12-26 16:50:43
tags: css高级
categories: css高级
---

## css3
css3总的说来大概就是边框的一些特殊样式，比如圆角，还有就是渐变，动画。

## 圆角
在CSS3中border-radius属性被用于创建圆角（前提是有边框属性）：`border-radius:10px;`
如果你在 border-radius 属性中只指定一个值，那么将生成 4 个 圆角。
其也可以这样写：border-radius:1px 2px 3px 4px [可以给四个角同时设置]
也可以border-top/bottom-left/right-radius，给某个角给值。
其值也可以这样： 	` border-radius: 15px/50px;      border-radius: 50% ;`【椭圆效果】

## 阴影、背景
CSS3中的box-shadow属性被用来添加阴影:box-shadow : 3px 3px 3px yellow;[上右下左]

有了CSS3的border-image属性，你可以使用图像创建一个边框：

 -webkit-border-image : url(border.png) 30 30 round;
round : 图像平铺（重复）来填充该区域。

Stretch 这里，图像被拉伸以填充该区域。

background-size指定背景图像的大小。CSS3以前，背景图像大小由图像的实际大小决定。

background-size:80px 60px;
background-Origin属性指定了背景图像的位置区域。
content-box, padding-box,和 border-box区域内可以放置背景图像。

Eg:background-origin:border-box;

CSS3 允许你在元素,那个添加多个背景图像。
`background-image:url(img_flwr.gif),url(img_tree.gif);`
CSS3 background-clip 属性，类比background-origin[背景图片]
作用：指定绘图区的背景，也就是规定背景的真正作用区域。
语法：`background-clip: border-box|padding-box|content-box;`

## 渐变
CSS3 定义了两种类型的渐变（gradients）：
线性渐变（Linear Gradients）- 向下/向上/向左/向右/对角方向
径向渐变（Radial Gradients）- 由它们的中心定义
语法：
`background: -webkit-linear-gradient(red, pink); 从上到下`
`background: -webkit-linear-gradient(left, red , blue); 从左向右`
-moz代表firefox浏览器私有属性
-ms代表IE浏览器私有属性
-webkit代表chrome、safari（苹果浏览器）私有属性
-o代表opera（欧朋浏览器）的私有属性

`background: -webkit-linear-gradient(left top, red , blue);` 渐变呈对角线变化，从左上角开始。
渐变的方向上也可以做更多的控制，您可以定义一个角度，而不用预定义方向：
 `background: -webkit-linear-gradient(180deg, red, blue);`
也可以同时使用多个颜色节点：
`background: -webkit-linear-gradient(red, green, blue);`

CSS3 渐变也支持透明度（transparency），可用于创建减弱变淡的效果：
`background: -webkit-linear-gradient(left, rgba(255,0,0,0), rgba(255,0,0,1));``
我们使用 rgba() 函数来定义颜色结点。rgba() 函数中的最后一个参数可以是从 0 到 1 的值，它定义了颜色的透明度：0 表示完全透明，1 表示完全不透明。r代表红色，g代表绿色，b代表蓝色，a代表透明度。

重复的渐变：
`background: -webkit-repeating-linear-gradient(...);`
为了创建一个径向渐变，您也必须至少定义两种颜色结点。
`background: -webkit-radial-gradient(red 5%, green 15%, blue 60%); `
比例越大，”半径越大”，它的默认形状是椭圆。也可以自定义形状;
`background: -webkit-radial-gradient(circle, red, yellow, green);` 
CSS3的文本阴影:
`text-shadow: 5px 5px 5px #FF0000;`分别对应水平阴影，垂直阴影，模糊的距离，以及阴影的颜色.
CSS3文本的强制换行：
`p {word-wrap:break-word;}`

CSS3 @font-face 规则，自定义字体。
```css
<style> @font-face{font-family: myFirstFont;src: url('Sansation_Light.ttf')
    }div{font-family:myFirstFont;
}</style>
```
## CSS3 2D 转换：
您将了解2D变换方法：
translate()
rotate()
scale()
skew()
matrix()
rotate()方法，在一个给定度数顺时针旋转的元素。负值是允许的，这样是元素逆时针旋转。

-webkit-transform:rotate(30deg); /* Safari and Chrome */ 注意是-webkit-transform :是冒号
translate()方法，根据左(X轴)和顶部(Y轴)位置给定的参数，从当前元素位置移动:

-webkit-transform:translate(50px,100px)
scale()方法，该元素增加或减少的大小，取决于宽度（X轴）和高度（Y轴）的参数

-webkit-transform:scale(1,2); 也就是宽度和高度呈对应的倍数增加。
skew()方法，该元素会根据横向（X轴）和垂直（Y轴）线参数给定角度：

skew(30deg,20deg)是绕X轴和Y轴周围20度30度的元素。
matrix 方法有六个参数，包含旋转，缩放，移动（平移）和倾斜功能。
rty 描述 CSS
transform 适用于2D或3D转换的元素 3
transform-origin 允许您更改转化元素位置 3
函数 描述
matrix(n,n,n,n,n,n) 定义 2D 转换，使用六个值的矩阵。
translate(x,y) 定义 2D 转换，沿着 X 和 Y 轴移动元素。
translateX(n) 定义 2D 转换，沿着 X 轴移动元素。
translateY(n) 定义 2D 转换，沿着 Y 轴移动元素。
scale(x,y) 定义 2D 缩放转换，改变元素的宽度和高度。
scaleX(n) 定义 2D 缩放转换，改变元素的宽度。
scaleY(n) 定义 2D 缩放转换，改变元素的高度。
rotate(angle) 定义 2D 旋转，在参数中规定角度。
skew(x-angle,y-angle) 定义 2D 倾斜转换，沿着 X 和 Y 轴。
skewX(angle) 定义 2D 倾斜转换，沿着 X 轴。
skewY(angle) 定义 2D 倾斜转换，沿着 Y 轴。

## CSS3 3D 转换:
rotateX()
rotateY()
-webkit-transform:rotateX/Y(120deg); / Safari and Chrome /

## CSS3 过渡 : transition 属性.
CSS3 过渡是元素从一种样式逐渐改变为另一种的效果。
要实现这一点，必须规定两项内容：
指定要添加效果的CSS属性
指定效果的持续时间
Eg : -webkit-transition: -webkit-transform 3s;
-webkit-transition-delay 规定过渡效果何时开始。默认是 0。

## CSS3 动画
当在@keyframe创建动画，把它绑定到一个选择器，否则动画不会有任何效果。
指定至少这两个CSS3的动画属性绑定向一个选择器：
规定动画的名称
规定动画的时长
```css
	<style>
		div{
		width:100px;
		height:100px;
		background:red;
		-webkit-animation:myfirst 5s; / Safari and Chrome /
		}
		@-webkit-keyframes myfirst / Safari and Chrome /
		{
		from {background:red;}
		to {background:yellow;}
		}
	</style>
```
也可以这样写：
```css
	@-webkit-keyframes myfirst / Safari and Chrome /
	{
	0% {background:red;}
	25% {background:yellow;}
	50% {background:blue;}
	100% {background:green;}
	}
```
其中不仅仅跟background属性，可以跟一系列属性。

属性 描述 CSS
@keyframes 规定动画。 3
animation 所有动画属性的简写属性，除了 animation-play-state 属性。 3
animation-name 规定 @keyframes 动画的名称。 3
animation-duration 规定动画完成一个周期所花费的秒或毫秒。默认是 0。 3
animation-timing-function 规定动画的速度曲线。默认是 "ease"。 3
animation-delay 规定动画何时开始。默认是 0。 3
animation-iteration-count 规定动画被播放的次数。默认是 1。 3
animation-direction 规定动画是否在下一周期逆向地播放。默认是 "normal"。 3
animation-play-state 规定动画是否正在运行或暂停。默认是 "running"。 3
通过 CSS3多列，您能够创建多个列来对文本进行布局 - 就像报纸那样！
在本章中，您将学习如下多列属性：
column-count
column-gap
column-rule

div{
-webkit-column-count:3; /* Safari and Chrome */    将文章划为3列
-webkit-column-gap:40px; /* Safari and Chrome */    每列间的距离为40px
-webkit-column-rule:3px outset #ff00ff; /* Safari and Chrome */  设置列之间
的宽度，样式和颜色
} 
