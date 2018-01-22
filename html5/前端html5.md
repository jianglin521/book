---
title: 前端html5
date: 2017-12-26 17:07:19 
tags: html5
categories: html5
---

## Html5
Html5新加了一些语义元素，画布，拖放，web存储（localstarge，sessionstrage）等
## 1. 语义化标签
HTML5 定了 8 个新的 HTML 语义（semantic） 元素。所有这些元素都是 块级 元素。
为了能让旧版本的浏览器正确显示这些元素，你可以设置 CSS 的 display 属性值为 block:

## 2.你可以为 HTML 添加新的元素。
```css
	fuck{
		Font-family：simhei;
		Color:pink
	}
```
本例中，JavaScript 语句 document.createElement("myHero") 是为了为 IE 浏览器添加新的元素。Internet Explorer 8 及更早 IE 版本的浏览器不支持以上的方式。幸运的是， Sjoerd Visscher 创建了 "HTML5 Enabling JavaScript", " shiv":以上代码是一个注释，作用是在 IE 浏览器的版本小于 IE9 时将读取 html5.js 文件，并解析它。
## 3.HTML5 `<canvas> `
HTML5 `<canvas> `元素用于图形的绘制，通过脚本 (通常是JavaScript)来完成.
`<canvas>` 标签只是图形容器，您必须使用脚本来绘制图形。Ie8以及以前不支持、
```js
	<script>
		var c=document.getElementById("myCanvas");
		var ctx=c.getContext("2d");
		ctx.fillStyle="#FF0000";
		ctx.fillRect(0,0,150,75);
	</script>
```
getContext() 方法返回一个用于在画布上绘图的环境。
设置fillStyle属性可以是CSS颜色，渐变，或图案。fillStyle 默认设置是#000000（黑色）。
fillRect(x,y,width,height) 方法定义了矩形当前的填充方式。
canvas 是一个二维网格。canvas 的左上角坐标为 (0,0)
在Canvas上画线，我们将使用以下两种方法：
moveTo(x,y) 定义线条开始坐标
lineTo(x,y) 定义线条结束坐标
然后使用 stroke() 方法来绘制线条:
在canvas中绘制圆形, 我们将使用以下方法: arc(x,y,r,start,stop)
ctx.arc(95,50,20,0,2*Math.PI);
参数分别为，圆心的横坐标，纵坐标，半径，起始角（以弧度记），结束角（以弧度记）
使用 canvas 绘制文本，重要的属性和方法如下：
font - 定义字体
fillText(text,x,y) - 在 canvas 上绘制实心的文本
strokeText(text,x,y) - 在 canvas 上绘制空心的文本
渐变可以填充在矩形, 圆形, 线条, 文本等等, 各种形状可以自己定义不同的颜色。
以下有两种不同的方式来设置Canvas渐变：
createLinearGradient(x,y,x1,y1) - 创建线条渐变
createRadialGradient(x,y,r,x1,y1,r1) - 创建一个径向/圆渐变

var c=document.getElementById("myCanvas");
var ctx=c.getContext("2d");// Create gradientvar grd=ctx.createLinearGradient(0,0,200,0);
grd.addColorStop(0,"red");
grd.addColorStop(1,"white");// Fill with gradientctx.fillStyle=grd;
ctx.fillRect(10,10,150,80);
将图片画在画布上：

var c=document.getElementById("myCanvas");var ctx=c.getContext("2d");var img=document.getElementById("scream");
ctx.drawImage(img,10,10);
SVG 指可伸缩矢量图形 (Scalable Vector Graphics)SVG 图像在放大或改变尺寸的情况下其图形质量不会有损失

Canvas 与 SVG 的比较：
SVG 是一种使用 XML 描述 2D 图形的语言。Canvas 通过 JavaScript 来绘制 2D 图形。
Svg支持事件处理器，canvas不支持事件处理器
在 SVG 中，每个被绘制的图形均被视为对象，而canvas能够以 .png 或 .jpg 格式保存结果图像
如果 SVG 对象的属性发生变化，那么浏览器能够自动重现图形。

Html5的拖放功能、

## HTML5 - 使用地理定位
请使用 getCurrentPosition() 方法来获得用户的位置。

##Html5新的input类型：
color
date
datetime
datetime-local
email
month
number
range
search
tel
time
url
Week

## HTML5 新的表单元素：
```
<datalist>
<keygen>
<output>
```
Select和datalist的区别：
select：5个值里面选择1个；
datalist：你可以在文本框里填值，也可以在下面5个值里选1个。
```html
<input list="browser" name="browser">

<datalist id="browser">
    <option value="Internet Explorer"></option>
    <option value="Firefox">
    <option value="Chrome">
    <option value="Opera">
    <option value="Safari">
</datalist>
<input type="submit">
```
`<keygen> `元素的作用是提供一种验证用户的可靠方法。
`<keygen>`标签规定用于表单的密钥对生成器字段。
当提交表单时，会生成两个键，一个是私钥，一个公钥。
`<output>` 元素用于不同类型的输出，比如计算或脚本输出：
```html
<form oninput="x.value=parseInt(a.value)+parseInt(b.value)">0
    <input type="range" id="a" value="50">100
    +<input type="number" id="b" value="50">
    =<output name="x" for="a b"></output>
</form>
```
属性 值 描述
for element_id 定义输出域相关的一个或多个元素。
form form_id 定义输入字段所属的一个或多个表单。
name name 定义对象的唯一名称。（表单提交时使用）

P.S：别忘了给range和number设置value属性。

`<form>`新属性：

autocomplete
novalidate

`<input>`新属性：

autocomplete
autofocus
form
formaction
formenctype
formmethod
formnovalidate
formtarget
height and width
list
min and max
multiple
pattern (regexp)
placeholder
required
step
①. autocomplete 属性规定 form 或 input 域应该拥有自动完成功能。
当用户在自动完成域中开始输入时，浏览器应该在该域中显示填写的选项。有on（开）,off（关）。
②．novalidate 属性规定在提交表单时不验证 form 或 input 域输入元素的合法性。
③．autofocus 属性是一个 boolean 属性.autofocus 属性规定在页面加载时，域自动地获得焦点，就是进去就可以直接输入。
④．form 属性规定输入域所属的一个或多个表单。Eg:
```html
<form action="demo-form.php" id="form1">
First name: <input type="text" name="fname">

<input type="submit" value="Submit">
</form>
```
Last name: `<input type="text" name="lname" form="form1">`
"Last name" 字段没有在form表单之内，但它也是form表单的一部分。
⑤The formaction 属性用于描述表单提交的URL地址.
⑥formenctype 属性描述了表单提交到服务器的数据编码 (只对form表单中 method="post" 表单)
⑦formmethod 属性定义了表单提交的方式。
⑧novalidate属性描述了 `<input>` 元素在表单提交时无需被验证。
⑨formtarget 属性指定一个名称或一个关键字来指明表单提交数据接收后的展示。
`<input type="submit" formtarget="_blank" value="提交到一个新的页面上">`
10.height 和 width 属性规定用于 image 类型的 `<input> `标签的图像高度和宽度。
`<input type="image" src="05.jpg">`这种形式写在表单里，可以实现点击图片提交表单。
11.list 属性规定输入域的 datalist。datalist 是输入域的选项列表。结合datalist标签使用。
12.min、max 和 step 属性用于为包含数字或日期的 input 类型规定限定（约束）。
13.

   multiple 属性是一个 boolean 属性.  multiple 属性规定`<input>` 元素中可选择多个值。例如同时选择多个文件上传。
14.pattern 属性描述了一个正则表达式用于验证` <input>` 元素的值。
15.placeholder 属性提供一种提示（hint），描述输入域所期待的值
16.required 属性规定必须在提交之前填写输入域（不能为空）。

17.step 属性为输入域规定合法的数字间隔。
如果 step="3"，则合法的数是 -3,0,3,6 等

## 语义元素：
一个语义元素能够清楚的描述其意义给浏览器和开发者。
无语义 元素实例: `<div> `和 `<span>` - 无需考虑内容.
语义元素实例: `<form>, <table>, and <img>` - 清楚的定义了它的内容.
HTML5中新的语义元素：
许多现有网站都包含以下HTML代码：` <div id="nav">, <div class="header">, 或者 <div id="footer">,` 来指明导航链接, 头部, 以及尾部.

`<section>` 标签定义文档中的节（section、区段）。比如章节、页眉、页脚或文档中的其他部分。
`<article> `标签定义独立的内容。.
`<nav>` 标签定义导航链接的部分。
`<aside>` 标签定义页面主区域内容之外的内容（比如侧边栏）。
`<header>`元素描述了文档的头部区域
`<footer>` 元素描述了文档的底部区域.
`<figure>`标签规定独立的流内容（图像、图表、照片、代码等等）。
`<figcaption>` 标签定义` <figure>` 元素的标题.
为了让这些块及元素在所有版本的浏览器中生效，你需要在样式表文件中设置一下属性 (以下样式代码可以让旧版本浏览器支持本章介绍的块级元素):
```css
header, section, footer, aside, nav, article, figure
{ 
display: block; 
}
```
HTML5 Shiv解决ie旧版本不支持h5新元素。浏览器小于IE9版本时会加载html5shiv.js文件. 你必须将其放置于<head> 元素中。让CSS 样式应用在未知元素上只需执行 document.createElement(elementName) 即可实现。html5shiv就是根据这个原理创建的。如下：
```js
	<!--[ifltIE9]>
	<script
	type="text/javascript"
	src="scripts/html5shiv.js"></script>
	<![endif]-->
```
## HTML5 Web 存储
早些时候,本地存储使用的是cookies。但是Web 存储需要更加的安全与快速. 
localStorage - 没有时间限制的数据存储
sessionStorage - 针对一个 session 的数据存储
```js
    if(typeof(Storage)!=="undefined") {  
 	 if (localStorage.clickcount) {    
   		 localStorage.clickcount=Number(localStorage.clickcount)+1;
    	} else{   
    		localStorage.clickcount=1;
   	}
```
关键词：localStorage.clickcount

## HTML5 应用程序缓存
1. 离线浏览 用户可在应用离线时使用它们
2. 速度 已缓存资源加载得更快
3. 减少服务器负载 浏览器将只从服务器下载更新过或更改过的资源。
```html
	 <!DOCTYPE HTML>
	 <html manifest="demo.appcache">
	 ...
	 </html>
 ```
manifest 文件需要配置正确的 MIME-type，即 "text/cache-manifest"。必须在 web 服务器上进行配置。manifest 文件是简单的文本文件，它告知浏览器被缓存的内容（以及不缓存的内容）。
manifest 文件可分为三个部分：
CACHE MANIFEST - 在此标题下列出的文件将在首次下载后进行缓存
NETWORK - 在此标题下列出的文件需要与服务器的连接，且不会被缓存
FALLBACK - 在此标题下列出的文件规定当页面无法访问时的回退页面（比如 404 页面）

## HTML5 Web Workers
web worker 是运行在后台的 JavaScript，不会影响页面的性能。
当在 HTML 页面中执行脚本时，页面的状态是不可响应的，直到脚本已完成。
web worker 是运行在后台的 JavaScript，独立于其他脚本，不会影响页面的性能。您可以继续做任何愿意做的事情：点击、选取内容等等，而此时 web worker 在后台运行。

首先，检测浏览器是否支持web worker。
```js
if(typeof(Worker)!=="undefined"){
      ......
}
```
 首先创建 web worker 文件，也就是外部的js文件 
 var i=0;
 postMessage(i);
 创建 Web Worker 对象
 w=new Worker("demo_workers.js");
当我们创建 web worker 对象后，它会继续监听消息（即使在外部脚本完成之后）直到其被终止为止。

w.terminate(); terminate【终止】

具体实例：
```js
	 if(typeof(Worker)!=="undefined"){      
		 var w=new Worker("client.js");
	       w.onmessage=function(ev){
	           alert(ev.data)
	       }
	   }
```
 关键：postMessage()   onmessage;
 
HTML5 服务器发送事件(Server-Sent Events):
Server-Sent 事件指的是网页自动获取来自服务器的更新。 单向消息传递.
客户端代码：
```js
	<!DOCTYPE html>
	<html>
	    <meta http-equiv="content-type" content="text/html charset=utf-8">
	    <body>
	    <h1>获得服务器更新</h1>
	    <div id="result"></div>
	    <script>
	    if(typeof(EventSource)!=="undefined"){  
	    		var source=new EventSource("test.php");
	  		source.onmessage=function(event)    {   
	  			document.getElementById("result").innerHTML+=event.data+ "<br />";
	    		};
	  }else{  
	  document.getElementById("result").innerHTML="Sorry, your browser does not support server-sent events...";
	  }
	  </script>
	  </body>
	</html>
```
服务器代码：
```js
	<?phpheader('Content-Type: text/event-stream');
	header('Cache-Control: no-cache');echo "data: This is server info! \n\n";
	flush();?>
```
关键字：EventSource对象 flush()。

