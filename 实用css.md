## 1.理解background-size ##
  如果使用px来定位的话，那么sprite图是以左上角(0 0) 为中心点的，如加上background-position：10px 20px;（那么图片的左边缘跟上边缘会往下移动20px,往左移动10px;我们平常使用的也是这种情况。)
  但使用百分比来定位的话，那图片就不是以左上角为中心点了。要想得到定位的百分比值（n m），我们需要 元素的宽高(w h), sprite图的宽高(k g),我们需要显示icon的坐标（x y），我们以向右向下移动端为正，向上向左为负。可以得到计算公式如下：
  `left： -n* k + n*w  =  -x
  top：  -m* g + m*h  =  -y`
  实现一段文字中单词的首字母大写
  ```css
    { text-transform: capitalize;}
   ```
##  2  CSS选择器 ##  
  元素选择器：``* 、E、 E#id、 E.class`
  关系选择器：`E、F、E>F、E+F、E~F`
  属性选择器：`E[att]、E[att="val"]、E[att~="val"]、E[att^="val"]、E[att$="val"]、E[att*="val"]、E[att|="val"]``
  伪类选择器：`E:link、E:visited、E:hover、E:active、E:focus、E:lang(fr)、E:not(s)、E:root、E:first-child、E:last-child`等
  伪对象选择器：`E:first-letter/E::first-letter、E:first-line/E::first-line、E:before/E::before、E:after/E::after、E::selection`
  （伪类和伪元素的根本区别：是否创造了新的元素（抽象））

###  2.2.1 权重 ###  
一个行内样式+1000，一个id+100，一个属性选择器/class类/伪类选择器+10，一个元素名/伪对象选择器+1。

###  2.2.2 rgba()和opacity的透明效果有什么不同？###  
a. `opacity`作用于元素，以及元素内的所有内容的透明度，`rgba()`只作用于元素的颜色或其背景色。
b. 设置rgba透明的元素的子元素不会继承透明效果


###  2.2.3 CSS中 link 和@import 的区别是什么？ ###  
a. link属于HTML标签，而@import是CSS提供的，且只能加载 CSS
b. 页面被加载时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载
c. import只在IE5以上才能识别，而link是HTML标签，无兼容问题
d. link方式的样式的权重高于@import的权重
e. 当使用 Javascript 控制 DOM 去改变样式的时候，只能使用 link 方式，因为 @import 眼里只有 CSS ，不是 DOM 可以控制

###  2.2.4请说说你对标签语义化的理解？ ###  
a. 去掉或者丢失样式的时候能够让页面呈现出清晰的结构
b. 有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；
c. 方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；
d. 便于团队开发和维护，语义化更具可读性，遵循W3C标准的团队都遵循这个标准，可以减少差异化。

###   2.2.5你知道多少种Doctype文档类型？ ###  
XHTML 1.0 规定了三种 XML 文档类型：Strict、Transitional 以及 Frameset。

###  2.2.6 截取图片clip介绍 ###  
clip:rect(30px 200px 200px 20px) 表示top right bottom left分别指最终剪裁可见区域的上边，右边，下边与左边。而所有的数值都表示位置，且是相对于原始元素的左上角而言的。

##  3.pc端的缩放：##  
(1).IE下：设置`zoom`:0.5的元素会以该元素的左上角为原点在直接被缩小一半；
(2). ff：使用`transform`:scale(0.5);
(3).webkit下可选择`zoom或scale`

##  4.流式布局 ##  
  指所有参与布局的div都用float:left，宽度都用百分比表示

##  5.闭合浮动的方法 ##  
  (1)在浮动元素末尾添加一个空的标签例如 `<div style=”clear:both”></div>`
  (2)使用 br标签和其自身的 html属性
  (3)设置父元素overflow值设置为hidden；在IE6中还需要触发 hasLayout,例如 zoom：1
     (原因：overflow除了visible，在auto, hidden或scroll时，会建立新的块级格式给他的子元素，从而达到清除浮动的目的)
  (4)父元素设置display:table
  (5)使用:after 伪元素
  ```css
    {content:".";display:block;height:0;clear:both;visibility:hidden;}
  ```
  如：
  ```css
  .clearfix:after{content:".";display:block; height:0; visibility:hidden; clear:both; }
  .clearfix { zoom:1; }
  ```

##  6.影响div层的顺序的因素： ##  
  除了将被定位的元素设置z-index外,元素设置了opacity，transforms,filters,css-regions,paged media等属性也会影响

##  7.负边距（margin取负值）：##  
  ①不脱离文档流（即没有使用定位或浮动）的元素，使用负值时，所有跟随元素都会上移；
  ②对浮动元素的影响：可以实现写在后面的元素移动到前面；
  ```html
    <div class="leftPart">left</div>
    <div class="rightPart">right</div>
  ```
  如：
  ```css
    .leftPart {float:left; margin-right:-100px;}
  ```
  说明：当leftPart和rightPart都浮动，如果负margin等于实际宽度，则元素会被完全覆盖。这是因为元素的完全宽度等于margin，padding，border，width相加而成，所以如果负margin等于余下三者的和，那元素的实际宽度也就变成了0px。

应用1：实现两列自适应等高
```html
<div class="wrap">
  <div class="leftPart">left</div>
  <div class="rightPart">right</div>
</div>
```
```css
/*.leftPart,.rightPart{border:1px solid black;float: left;}
   .leftPart{width:100%;margin-right:-202px;background: red;}
   .rightPart{width: 200px;background: green;}*/
.wrap{overflow: hidden;}
.leftPart,.rightPart{float:left;height:auto;margin-bottom:-1000px;padding-bottom:1000px;}
 .leftPart{width:100%;margin-right:-200px;background: red;}
 .rightPart{width: 200px;background: green;height:auto;}
 ```
(测试：有些问题)
应用2：左右两栏固定，中间自适应
```html
<div class="content">content</div>
<div class="leftPart">left</div>
<div class="rightPart">right</div>
``
Css:
```css
   .content,.leftPart,.rightPart{float: left;height:200px;}
   .leftPart,.rightPart{width: 200px;}
   .leftPart{margin-left:-100%;background: red;}
   .rightPart{margin-left:-200px;background: green;}
   .content{background:#D4DBED;width: 100%;}
```
应用3:列表相关
去除ul最右边的li的右边距：
如：
```html
<div class="test">
  <ul class="testUl">
    <li>list1</li>
    <li>list2</li>
    <li>list3</li>
    <li>list4</li>
    <li>list5</li>
    <li>list6</li>
  </ul>
</div>
```
```css
.test{width:320px;height:400px;background:#4FC964;}
.testUl{
    margin:0;padding:0;
    list-style-type: none;
    margin-right: -10px;
    zoom:1;
 }
.testUl li{
  float: left;width:100px;background: yellow;
  margin-bottom:10px;
  margin-right: 10px;
}
```
去除ul最后一个的li的底部边框
```html
<div class="test">
  <ul class="testUl">
    <li>list1</li>
    <li>list2</li>
    <li>list3</li>
    <li>list4</li>
    <li>list5</li>
    <li>list6</li>
  </ul>
</div>
```
Css:
```css
  .test{width:320px;height:600px;background:#4FC964;border: 1px solid black;}
  .testUl{list-style: none;margin:0;padding:0;}
  .testUlli{border-bottom: 1px solid black;height:100px;margin-bottom:-1px;}
```
应用4：多列等高
```html
<div id="wrap">
  <div id="left">
      style="height:50px"
  </div>
  <div id="center">
      style="height:50px"
  </div>
  <div id="right">
      style="height:50px"
  </div>
</div>
```
```css
    #wrap{
      overflow:hidden;
      width:580px;
    }
    #left,#center,#right{
      margin-bottom:-200px;
      padding-bottom:200px;
    }
    #left{
      float:left;
      width:140px;
      background:#777;
      height:100px;
    }
    #center {
      float:left;
      width:300px;
      background:#888;height:30px;
    }
    #right {
      float:right;
      width:140px;
      background:#999;height:50px;
    }
```    
增加元素的宽度
左右负边距还能增加元素的宽度，能实现的前提是：该元素没有设定width属性(当然width:auto)是可以的

应用5：负边距+定位：水平垂直居中
使用绝对定位将div定位到body的中心，然后使用负margin（content宽高的一半），将div的中心拉回到body的中心，已到达水平垂直居中的效果。
```css
  #test{
    width:200px;
    height:200px;
    background:#F60;
    position:absolute;
    left:50%;
    top:50%;
    margin-left:-100px;
    margin-top:-100px;
  }
```
## 7.多列等高及CSS实现自适应布局： ##
### 7.1多列等高 ###
<!--原理就是给每一列添加相对应用的容器，并进行相互嵌套,适用于流体布局和多列，但不适用于带边框的 -->
```html
<div class="container">
  <div class="rightWrap">
    <div class="contentWrap">
      <div class="leftWrap">
      <div class="left">left<br/><br/><br/></div>
      <div class="content">content<br/></div>
      <div class="right">right</div>
      </div>
    </div>
   </div>
</div>
```
```css
.container{width:960px;overflow:hidden;}
.rightWrap,.contentWrap,.leftWrap,.right,.content,.left{
        position: relative; float: left;
 }
.rightWrap,.contentWrap,.leftWrap{width: 100%;}

   .rightWrap{background:#DFE4F4;overflow: hidden;}
   .contentWrap{background:#ECDE8C;right:320px;}
   .leftWrap{background:#4CB849;right:420px;}

   .right,.content,.left{overflow: hidden; left:740px;}
   .right{width: 320px;}
   .content{width:420px;}
   .left{width:220px;}
```

### 7.2 三栏布局：左右固定，中间自适应 ###
```css
 /*方法一*/
.main{position: absolute;left: 200px;right: 200px;}
.left,.right{width: 200px;}
.left{float: left;}
.right{float: right;}

    /*方法二*/
   .wrap{padding:0 300px 0 200px;}
   .main{float: left;width: 100%;}
   .left,.right{position: relative;_display:inline;}
   .left{float:left;width: 200px;margin-left: -100%;right:200px;_right:-300px;}
   .right{float:right;width: 300px;margin-right: -300px;}
```
```html
<div class="wrap">
<div class="main">
       main-中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>
	</div>
	<div class="left">
		 left-中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>
	中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>
	中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>
	</div>
	<div class="right">
		 right-中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>
	中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>
	中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>中间自适应部分<br>
	</div>
</div>
```

###  7.3左边固定，右边自适应 ##  
```css
  /*方法一*/
html{height: auto;}
    .container{border:1px solid red;}
    .wrapper{position: relative;display: inline-block;border-left: 200px solid #d4c376;vertical-align: bottom;}
    .sidebar{position: relative;float: left;width: 200px;margin-left: -200px;}
    .main{float: left;}
    .main,.sidebar{min-height: 200px;height: auto!important;height: 200px;}
```
```html
<div class="container">
	<div class="wrapper">
		<div class="sidebar">Left Sidebar</div>
		<div class="main">
		  Main Content<br/> Main ContentMain Content Main Content<br/>
		  Main Content<br/>Main Content<br/> Main Content<br/> Main Content<br/>
		  Main Content<br/> Main Content<br/> Main Content<br/> Main Content<br/>
		  Main Content<br/> Main Content<br/> Main Content<br/> Main Content<br/>
		</div>
	</div>
</div>
```
    /*方法二*/
  ```css
.container{overflow: hidden;}
.left{float: left;margin-bottom: -99999px;padding-bottom:99999px;width: 200px;background:#ccc;}
.content{margin-left: 200px;margin-bottom: -99999px;padding-bottom:99999px;background-color: #eee;}
.left,.content{min-height: 200px;height:auto!important;height: 200px;}
```
```html
<div class="container">
	<div class="left aside">Left aside</div>
	<div class="content seticon">  Main Content<br/> Main Content<br/> Main Content<br/> Main Content<br/>
		  Main Content<br/> Main Content<br/> Main Content<br/> Main Content<br/>
		  Main Content<br/> Main Content<br/> Main Content<br/> Main Content<br/>
		  Main Content<br/> Main Content<br/> Main Content<br/> Main Content<br/>
		  Main Content<br/> Main Content<br/> Main Content<br/> Main Contentlast<br/>
	</div>
</div>
```
##   7.4上下固定，中间自适应 ##  
```css
.headerWrap,.footerWrap,.contentWrap{position: absolute;width:100%;}
.headerWrap,.footerWrap{height:100px;line-height:100px;background-color:#669801;}
.headerWrap{top:0;left: 0;}
.contentWrap{background-color:#F6D96B;overflow: auto;top:100px;bottom: 100px;}
.footerWrap{bottom:0;left: 0;}
```
```html
<div class="headerWrap">这是头部</div>
	<div class="contentWrap">
	the中间自适应部分<br>
	中间自适应部分<br>
	    last中间自适应部分<br>
</div>
<div class="footerWrap">这是底部部分。</div>
```

##  8.自适应和响应式网页设计 ##  
自适应布局:指的是可以自动识别屏幕宽度，并做出相应调整的网页设计，等于使用固定分割点来进行布局。
响应式网页设计：指的是页面的布局（流动网格、灵活的图像及媒体查询）

##  9．css实现垂直居中： ##  
注：ie7及ie7以下无法识别display:table
(1)固定高度的层相对于浏览器窗体垂直居中的四种方法：
```css
    *{margin:0;padding: 0;}

    /*fun1 start*/
    .wrapper{display: table;height:300px;width: 100%;}
    .cell{display: table-cell;vertical-align: middle;border:1px solid black;}
    /*fun1 end*/

    /*fun2 start(推荐)*/
    .content2{position:absolute;top:50%;height:200px;margin-top:-100px;border:1px solid black;}
    /*fun2 end*/

   /*fun3 start*/
html,body{height:100%;}
   .floatEmpty {float:left; height:50%; margin-bottom:-100px;position:relative;}
   .content3{clear:both; height:200px; position:relative;border:1px solid black;margin:0 auto;background-color:#FFCC66;width:80;}
   /*fun3 end*/

  /*fun4 start*/
  .content4{position:absolute;top:0;bottom:0;left:0;right:0;margin:auto;height:240px;width:80%;border:1px solid black;}
  /*fun4 end*/
```

```html
<!DOCTYPE html>
<html>
<head>
<meta charset="utf-8">
<title>垂直居中</title>
</head>
<body>
<!-- fun1 -->
<!--<div class="wrapper">
	<div class="cell">
	<div class="content">Content</div>
	</div>
</div> -->

<!-- fun2 -->
<!--<div class="content2">content</div> -->

<!-- fun3 -->
<div class="floatEmpty"></div>
<div class="content3">the third content.</div>

<!-- fun4 -->
<!--<div class="content4">content4 is here!</div> -->

</body>
</html>
```
(2)多行文字高度不确定在层中的垂直居中方式
```css
	   /*水平居中*/
     /*  .center{display: inline-block;_display:inline-block;border:2px solid black;}
     .center a{float: left;border:1px solid #fff;padding:5px;}
     .container{text-align: center;} */

 /*高度不确定的垂直水平居中(兼容ie7及ie7以下)*/
    #vc { display:table;overflow:hidden; background-color:#C2300B; width:500px; height:200px;  margin-left:50px; *position:relative; }
    #vci { vertical-align:middle; display:table-cell; text-align:center; *position:absolute; *top:50%; *left:50%; }
    #content { color:#fff; border:1px solid #fff; display:inline-block; *position:relative; *top:-50%; *left:-50%; }
```
```html
<body>
<div class="container">
	<div class="center">
		<a href="#">1</a><a href="#">2</a><a href="#">3</a>
	</div>
</div>

<!--方式一：高度不确定的垂直水平居中开始 -->
<div id="vc">
  <div id="vci">
    <div id="content">
      <p>我们垂直居中了，我们水平居中了</p>
      <p>我们垂直居中了，我们水平居中了</p>
      <p>我们垂直居中了，我们水平居中了</p>
    </div>
  </div>
</div>
<!--方式一结束 -->
</body>
```
（3）高度不确定的图片进行垂直居中：
方式一：将外部容器设置成display:table，img标签外部再嵌套一个span标签，设置span的为
```css
  display:table-cell，vertical-align: middle
```
如：
```css
body {height:100%; }
#box{width:500px;height:400px; display:table; text-align:center; border:1px solid #d3d3d3;background:#fff; }
#box span{ display:table-cell; vertical-align:middle; }
#box img{ border:1px solid #ccc; }
```
<!--[if lte IE 7]>
<style type="text/css">
#box{ position:relative; overflow:hidden; }
#box span{ position:absolute; left:50%;top:50%; }
#box img{ position:relative; left:-50%;top:-50%; }
</style>
<![endif]-->
```html
<body>
	<div id="box">
	<span><img src="images/demo_zl.png" alt="" /></span>
	</div>
</body>
```
方式二：外层容器设置`line-height=height`,img设置为`display:inline-block;vertical-align: middle`（推荐兼容ie7及以下）;
如：
```css
     .imgWrap{height:200px;width: 600px;line-height: 200px;border:1px solid black; text-align: center; }
     .imgWrap img{display: inline-block;vertical-align: middle;*margin-top:expression((200 - this.height )/2);}
```
```html
<body>
<div class="imgWrap">
	<img src="./images/tmp.jpg">
</div>
</body>
```
##  10.JavaScript控制垂直居中 ##  
如何控制滚动条滚动时div始终垂直居中方法（前提：弹出框的大小要小于可视窗体的大小）：
```javaScript
  Var elemHeight=$(elemId).height();
  Var elemWidth=$(elemId).width();
  Var leftPos=($(window).clientwidth()-elemWidth)/2;
  Var topPos =($(window).clientHeight()-elemHeight)/2+ $(document).scrollTop();
  $(elemId).css({left:leftPos,top:topPos});
```
11.-webkit-text-size-adjust
为了解决chrome不支持小于12px： html{-webkit-text-size-adjust:none;}
不足:设置为none之后，缩放屏幕时，字体不会更改。同时该属性只对chrome27以下有效。

##  11.弹出灰色遮罩层： ##  
```css
.grayShadowBg{
	 position:fixed;left:0;top:0; z-index:100;
   background:#636363;
   filter:alpha(opacity=50);  
    -moz-opacity:0.5;  
    -khtml-opacity: 0.5;  
  opacity: 0.5;  
  width: 100%;
  height: 100%;
}
```

遮罩层上的居中内容层：
```css
.popDgMain{position: absolute;z-index:101;width:530px;height:326px;left:0;top:0;}
```
（始终相对于可视屏幕居中：
```javaScript
JS:
/* 弹出遮罩层的窗体相对屏幕居中*/
function setPopupDgPosition($mainContentElem){
//$mainContentElem为$(‘. popDgMain’)
  var screenWidth = $(window).width(),
  screenHeight = $(window).height();
  var scrolltop = $(document).scrollTop();
  var objLeft = (screenWidth - $mainContentElem.width()) / 2;
  var objTop = (screenHeight - $mainContentElem.height()) / 2 + scrolltop;
  $mainContentElem.css({
      left: objLeft + 'px',
      top: objTop + 'px'
    });
}
```
##  12.弹出层对话框的关闭按钮样式 ##  
```css
Css:
.clostBtn{display: inline-block;float: right;margin:10px;
  height: 20px;width: 20px;
  background: url(./img.png) center center no-repeat; background-position: 0 -20px;
 }
a.clostBtn:hover{background: url(./img.png) center center no-repeat;background-position: 0 0; }
```
```html
html:
<a href="javascript:void(0)" class="closeBtn"></a>
图片： (图1：img.png)  （图2：hclose.png） (图：closeBtn.png)
```

##  13.鼠标滑轮滚动事件 ##  
FF：DOMMouseScroll滚动值获取：event.detail
非FF：onmousewheel 滚动值获取：event.wheelDelta

##  14. tab设置tr导致边框缺失问题： ##  
受到overflow的影响或可加上table:border:1px solid white;进行解决

##  15.pc端网页使用字体分析： ##  
（1）推荐常用的英文字体是：`arial`。 视觉设计的专业人士可能会认为在Windows中使用`tahoma`、在Mac中使用`helvetica`更好，比如淘宝的默认字体样式是font: 12px/1 Tahoma, Helvetica, Arial, "5b8b4f53", sans-serif;（注：“5b8b4f53”是宋体的意思，这是unicode的编码方式，不用 SimSun, 是因为 Firefox 的某些版本和 Opera 不支持 SimSun 的写法。使用宋体时，字号常用是12px和14px;12px/1表示默认的行高是默认字体的1倍，即行高是12*1=12px）
中文最好用`unicode`表示，比如使用宋体是`{font-family:\5b8b\4f53;}`，使用微软雅黑是`{font-family:\5fae\8f6f\96c5\9ed1;}`，这样的好处是避免编码问题，同时能得到所有的主流浏览器的支持。使用正确的字体种类写法，避免使用引号，这样可以缩小CSS的大小。
`微软雅黑   Microsoft YaHei   \5FAE\8F6F\96C5\9ED1`
常用的行高：`1.2,1:1.5和1:2` </br>
（2） 2.1Mac & Windows公有可用英文及数字字体有：`Arial, Arial Black, Comic Sans MS, Courier New, Georgia, Impact Times New Roman, Trebuchet MS,Verdana`
Windows下可用中文字体有`宋体（中易宋体），新宋体，仿宋体，黑体，楷体，微软雅黑`（部分系统适用，Vista以上系统，xp系统没有）。
Mac下可用中文字体有宋体`（华文宋体），仿宋体（华文仿宋），黑体（华文黑体），华文细黑，华文楷体`。（Mac默认下Safari使用`华文宋体`，chrome默认使用`华文黑体`）
（说明：windows下中文字体效果与Mac下字体没有共同字体，故效果差异蛮大的。）

2.2. 对于微软雅黑，以操作系统计算，覆盖率仅为不到30%，未安装该字体的用户可使用宋体或黑体替代，有必要的话可考虑指定替代字体。

2.3. 在Mac中，未针对Mac做Mac字体设置的话，网页字体会按一定规则转成Mac下的字体。

2.4. 正文`12px`字体建议使用宋体。`12-17px`宋体比微软雅黑要清晰

##  16.hack注释的写法：##  
如
`<!--[if lte IE 7]>
<style type="text/css">?
#box{
position:relative;
overflow:hidden;
}
</style>
<![endif]-->`
##  16.放链接到指定图片的固定位置上，不随窗体的移动而变化 ##  
常应用于banner区btn的点击：
如：
```css
    .imgWrap{position:relative;left:50%;top:0;margin-left:-960px;width:1920px;height:380px;background:url('./images/car_banner.jpg') center center  no-repeat;min-width:1200px;
    }
   .imgWrap .btnA{
      position: absolute;z-index:2;top:75%;left:56%;display: inline-block;width: 124px;height: 34px;line-height: 34px;border-radius:2px;background-color:#FF9924;font-size: 18px;text-align: center;color: white;text-decoration: none;cursor: pointer;
    }
   .imgWrap .btnA:hover{background-color: #FF8A05;}
```
```html
<body>
<div class="imgWrap">
<a class="btnA" href="#">立即投保</a>
</div>
</body>
```
 ![image](https://github.com/lovelyqyz/CSS-Note/blob/master/images/practicalCss-clickArea.png)
图1
（说明：min-width不能被ie6识别，在ie7中若设置了position：absolute，没有设置z-index的话，默认会放置在最底层，所以为了避免出现效果与预期不符，要设置z-index）
##  17.关于`display：inline-block，min-height,min-width`的兼容问题： ##  
（1）inline-block的使用
```css
  display:inline-block; /* 现代浏览器 +IE6、7 inline 元素 */
  *display:inline; /* IE6、7 block 元素(设置宽度和高度无效) */
  *zoom:1;  /*触发ie6的hasLayout*/
```
分析：在ie6，7下的块元素`display:inline-block`会失效，需要通过`*display:inline;*zoom:1`做hack处理
（2）`vertical-align`的适用范围：用于行内元素和表格元素,不适用于块元素（注：常见的行内元素：img,span,a）
(3)`min-height`和`min-width`的使用
设置最小高度：min-height可兼容到ie7，兼容id6可以使用_height；
设置最小宽度：直接设置min-width无效，因为元容器的默认高度是填充的内容的高度，而默认宽度是继承父容器的宽度，当然前提是block,所以需要添加display：inline-block
Css如下：
```html
  <div style="border:5px solid #f00;min-height:120px;_height:120px;width:300px;padding:12px;">
     最小高度最小高度最小高度最
</div>
<div style="display:inline-block;*display:inline;zoom:1; min-width:120px;border:5px solid #f00; padding:12px;">
     最小宽度
</div>
  ```
##   18.a属性title与img属性alt ##  
    Alt属性值：告诉搜索引擎蜘蛛该图片表达的内容,本意是替换的意思，即图片不存在的或者因为其他原因没有显示的时候，网页会显示ALT的内容。
    Title是提供非本质的额外信息，只是对链接的一个补充提示作用，鼠标移上去会显示title的内容。如果链接文字不完整，可以加上。
（1）兼容问题：当使用title来显示提示性文字时，若提示性文字过长，在Firefox下会出现内容截断，不能显示完全，而ie,chrome下显示正常；
解决方法：手动强制换行：
```html
<a href="javascript:void(0)"
title="123,344,566,123,344,566,123,344,566,123,344,566,123,
&#13;344,566,123,344,566,123,344,566,123,344,5688,">
	 123,344,566……
</a>
```
使用js控制：
```javascript
$('#linkA').attr('title','123,344,566,123,344,566,123,344,566,123,\n566,123,344,566,123,344,566');
```
js判断是否是ff浏览器内核：
```javascript
//取得浏览器的userAgent字符串
    var userAgent = navigator.userAgent;
    if (userAgent.indexOf("Firefox") > -1) {
      //是ff内核
    }
```
##  19.css实现具有3D效果的按钮 ##  
只要将它的左上部边框设为浅色，右下部边框设为深色即可。
```css
　　div#button {
　　　　background: #888;
　　　　border: 1px solid;
　　　　border-color: #999 #777 #777 #999;　}
```
##  20.页面的加载过程 ##  
（参考网址：[http://kb.cnblogs.com/page/129756/](http://kb.cnblogs.com/page/129756/)
渲染引擎在取得内容后的基本流程：解析html以构建dom树(将标签转换为dom节点)
构建render树（attachment）布局(回流)render树（layout或reflow） ->绘制render树

##  21.视觉滚动差 ##  
如：
```css
 .box{
  position:relative;
  height:939px; /* 此为元素背景图像实际高度 X 元素*/
  margin:0 auto;
  background-repeat:no-repeat;
  background-position:center center;
  background-attachment:scroll; /* 使背景图像相对于窗体固定 */
  background-size:cover; /* 取值auto | cover | contain */
  overflow:hidden;
  text-align:center;
}  
.box-1{background-image:url(scrollImg/p1.jpg);}
.box-2{background-image:url(scrollImg/p2.jpg);}
.box-3{background-image:url(scrollImg/p3.jpg);}
```
```html
<body>
	<div class="box box-1">区域1</div>
	<div class="box box-2">区域2</div>
	<div class="box box-3">区域3</div>
</body>
```
##  22.浏览器问题 ##  
(1)chrome下记住密码之后，form表单下的input会默认有淡黄色背景，所以为input设置背景图片，容易被覆盖。
92)设置ie默认的文档模式：
```html
  <meta http-equiv="X-UA-Compatible"content="IE=EmulateIE8" >
```
(3)关于CSS样式中加padding的文本框在chrome里面高度显示不正确问题
如：定义了`line-height:20px; height:20px; padding:2px 5px;` 在IE下显示正常，但chrome下的input高度仍是20px，而不是24px
解决：
方法1：页首的声明只写了一个<!DOCTYPE>，把它改为html5的标准声明格式<!DOCTYPE HTML>
方法2：在css里面添加了一个新的样式：`box-sizing:content-box;`

相关网址：
1.移动端h5字体及间距：[http://www.cnblogs.com/shouce/p/5074851.html](http://www.cnblogs.com/shouce/p/5074851.html)

##  23.移动端App相关技巧及遗留问题 ##  
1.iOS人机交互规范中提到手指最合适的触控区域至少需要44 point
2.默认操作：（1）两个指头可放大图片；（2）长按出现对话框；（3）阅读中向左滑是在向后翻页

###  23.1 bug ###
1.IOS下弹出层遮罩透明度问题
```html
<div class="descrDgWrap">
<div class="fullShadow"></div>
<div class="descrDgDetail">
  <p>测试数据</p>
</div>
</div>
```
```css
CSS:
.descrDgWrap.fullShadow{position: fixed;z-index:1;top:0;left:0;width:100%;height:100%;background-color:#A3A3A3; filter:alpha(opacity=40); -moz-opacity:0.4;   -khtml-opacity:0.4; opacity:0.4; }
.descrDgWrap.descrDgDetail{position:absolute;z-index:2;left:0;top:0;width:96%;background-color: white;margin:0 auto;border-radius:6px;}
.descrDgWrapp{padding:20px;line-height:22px;}
```
```javascript
Js:
var $surwayDg=$('.descrDgDetail');
var screenWidth = $(window).width(),
    screenHeight = $(window).height(); //当前浏览器窗口的宽高
var scrolltop = $(document).scrollTop(); //获取当前窗口距离页面顶部高度
var objLeft = (screenWidth - $surwayDg.width()) / 2;
var objTop = (screenHeight - $surwayDg.height()) / 2 + scrolltop; $surwayDg.css({ left: objLeft + 'px', top: objTop + 'px' });
```
问题：descrDgDetail这层应该是浮在最上层，且背景为纯白色，如果scrolltop不为0时，在ios系统下这个层有些灰，但scrolltop=0时显示正常，初步判断是受到fullShadow这层opacity的影响？
解决方法：在.descrDgDetail外面再添加一层div,设置样式为`{display:fixed;}`

### 23.2 技巧 ###
1.如何自定义移动端控件默认样式，但同时保持原生的touch、focus等事件
      方法：将自定义样式覆盖在控件上，原来控件设置为opacity：0；

23.3 注意事项
1.头部导航高度固定为44px，字体大小可选择18px

2.移动端button状态
（按钮有三态Normal（正常）、Pressed/Highlighted（按下）、Disabled（不可点击））
 ![image](https://github.com/lovelyqyz/CSS-Note/blob/master/images/practicalCss-btnstatus.png)
   图2

2.1点击a链接出现阴影遮罩
方法一：
```html
html：
<a href="javascript:void(0)" class="clickLink">点击按钮</a>
```
```css
css:
a{position: relative;display: block;background-color: #04BE02;border-radius:4px;text-align: center;border:none;text-decoration: none;}
 .pressShadow{position: absolute;top:0;left:0;background-color: #000000;filter:alpha(opacity=20);  -moz-opacity:0.2;  -khtml-opacity: 0.2;  opacity: 0.2;}
a,.pressShadow{height: 30px;line-height: 30px;width:100px;color: white;}
```
```javascript
js:
$('a').on("touchstart", function(){
    $(this).after("<div class='pressShadow'></div>");
}).on("touchend", function(){
    $(this).siblings('.pressShadow').remove();
})
```
方法二：
```html
html:
<a href="javascript:void(0)">点击按钮</a>
```
```css
css:
a{position: absolute;background-color: #04BE02;border-radius:4px;text-align: center; border:none;text-decoration: none;height: 30px;line-height: 30px;
   width:100px;color: white;
}
a.shadowClick:after{content:'';height:30px;width:100px;
    position: absolute;top:0;left:0;background-color: #000000;
    filter:alpha(opacity=20);-moz-opacity:0.2;-khtml-opacity:0.2;
    opacity: 0.2;
}
```
```javascript
js:
$('a').on("touchstart", function(){
/*  var  cStyle=document.createElement('style');       cStyle.innerText="a:after{content:'';height:30px;width:30px;width:100px;
color:white;border:1px solid red;position:absolute;top:0;left:0;
background-color: #000000;filter:alpha(opacity=20);  -moz-opacity:0.2; -khtml-opacity: 0.2;opacity: 0.2;
border:1px solid red;}";
document.body.appendChild(cStyle);
*/
   $(this).addClass('shadowClick');
}).on("touchend", function(){
   $(this).removeClass('shadowClick');
});
```

### 24.图片加载问题 ###
```javascript
    /*图片懒加载*/
  function loadingImg(){
     function Load(){}
     Load.prototype.loadImg = function(imgUrlArray,callback){
       this.imgUrlArray = imgUrlArray;
       this.imgNumbers = imgUrlArray.length;
       this.loadImgNumbers = 0;
       var that = this;
       for(var i = 0; i<imgUrlArray.length; i++){
        var obj = new Image();
        obj.src = imgUrlArray[i];
        obj.onload = function(){
           that.loadImgNumbers++;
           callback(parseInt(that.loadImgNumbers/that.imgNumbers)*100);
        }
       }
     }
     var loader = new Load();
     loader.loadImgs([

        // 将所有需要加载的图片地址写于此处
        "http://domain/site/dist/img/XX.png",
        "http://domain/site/dist/img/XX.png",
        "http://domain/site/dist/img/XX.png",
        "http://domain/site/dist/img/XX.png",
        "http://domain/site/dist/img/XX.png",
        "http://domain/site/dist/img/XX.png",
        "http://domain/site/dist/img/XX.png"
       ],function(percent){

          // 假设显示百分比的元素为 $(".percent")
          $(".percent").text(percent+'%');

          // 加载结束后，隐藏相应的 loading 或遮罩
          if(percent==100) {
              $(".mask").css('display','none');
          }
      });
}
loadingImg();
```
###  25.css的关系选择器 ###
 `X + Y` ：紧邻的兄弟元素
 `X > Y` ：子元素
 `X ~ Y` ：兄弟元素
（IE7+、ff、chrome兼容）


###  26.隐藏图片的请求情况 ###  
1.display：none的图片或背景的请求情况
 1下面是普通隐藏的img标签（有请求: file:///F:/test-example/req-img/images/3.jpg）

  <img src=" ./images/3.jpg" class="hide">
 2、下面是被隐藏的img标签（有请求: file:///F:/test-example/req-img/images/3.jpg）
   <div class="img2 hide">
    <div class="img2-inner"><img src=" ./images/3.jpg "></div>
   </div>
 3、下面是背景设在隐藏的div（有请求: file:///F:/test-example/req-img/images/3.jpg）

   <div class="bg1 hide"><!-- 这个div设有背景 --></div>
4、下面是背景设在隐藏div的子元素（没有请求: file:///F:/test-example/req-img/images/3.jpg）
   <div class="bg2 hide">
     <div class="bg2-inner"><!-- 这个div设有背景 --></div>
   </div>
 5、下面是背景设在隐藏div的子元素的子元素（没有请求file:///F:/test-example/req-img/images/3.jpg）
   <div class="bg3 hide">
     <div class="bg3-inner">
        <div class="bg3-inners"><!-- 这个div设有背景 --></div>
      </div>
    </div>

## 前端冷知识##

### js部分 ###
    1.浏览器地址栏可直接执行js代码：
      如：`javascript:alert('hello');`
    2.把浏览器当做编辑器
      地址栏上输入：`data:text/html,<html contenteditable>`
    3.将页面变为可编辑状态
      console面板下执行如下代码：`document.body.contentEditable = 'true'`
    4.页面拥有id的元素会创建全局变量
      如：`<div id="sample"></div>`
      可以直接：console.log(sample);
    5.加载CDN文件时，可省掉HTTP标识
     CDN即从专门的服务器加载一些通用的JS和CSS文件
    6.整数操作
  `  |0 `和` ~~`将浮点数转换为整型且效率方面要比同类的parseInt,Math.round()要快;
    如：`console.log((10/3)|0);
         console.log(~~(10/3));`
     结果都是 3
    7.不声明第三个变量的值交换
    ` var a = 1, b = 2; a = [b,b=a][0];     `
    8.数字型调用toString()
      1.toString()会报错，应改为1..toString()或(1).toString()
    9.禁止别人通过iframe加载你的页面
    `  if (window.location != window.parent.location)   window.parent.location = window.location;`

## css部分 ##
  1.鼠标消失
  ```css
    *{
      cursor: none!important;
    }
  ```
  2.文字模糊效果
    ```css
  p {
    color: transparent;
    text-shadow: #111 0 0 5px;
  }
  ```
  3.垂直居中
  IE9以上的浏览器支持
    ```css
  .center-horizontal {
     position: relative;
     left: 50%;
     transform: translateX(-50%);
  }
  ```
  4.多重边框
  采用box-shadow来实现，
    ```css
  div {
    box-shadow: 0 0 0 6px rgba(0, 0, 0, 0.2), 0 0 0 12px rgba(0, 0, 0, 0.2), 0 0 0 18px rgba(0, 0, 0, 0.2), 0 0 0 24px rgba(0, 0, 0, 0.2);
    height: 200px;
    margin: 50px auto;
    width: 400px
  }
  ```
  5.创建长宽等比固定的元素
  ```html
  <div style="width:100%;position:relative;padding-botton:20%;">
      <div style="position:absolute;left:0;top:0;right:0;bottom:0;background-color:yellow">
           this content will have a constant aspect ratio that varies based on the width.
      </div>
    </div>
```

6.BFC
 含义：Block  Formatting Context ,块级格式化上下文，
 作用：自适应两栏布局、清除内部浮动、防止垂直margin重叠(放在两个BFC里面)
 产生：根元素、float元素不为none、position为absolute或fixed, display为inline-block、table-cell、table-caption、flex、inline-flex、overflow不为visible;

 7.animation和transition的区别
   同：都是随着时间改变的元素值
   异：transition需要触发一个事件（hover或click事件等）才会随着时间改变其css属性；
       animation在不需要触发任何事件的情况下也可以显示地随着时间变化

8.标准模型和怪异模型
  怪异模型：box-sizing:border-box; (content)
  标准模型：box-sizing:content-box; (content + border + padding)

9、写出5大浏览器的内核
`*Trident: IE、Maxthon(遨游)、腾讯 、Theworld世界之窗、360浏览器
*Gecko：： Mozilla Firefox 是开源的
*Webkit : Safari、Chrome ， 是一个开源项目。
*Presto : Opera ，Presto是由Opera Software开发的浏览器排版引擎。它也是世界上公认的渲染速度最快的引擎。
*Blink  ：由Google和Opera Software开发的浏览器排版引擎，2013年4月发布。`

10.浮动后的元素的display的值
  无论是左浮动还是右浮动后都可以设置宽和高，display的值是block

11.等比例缩放区块
`padding-bottom`取值为百分比形式时，百分比的基数是其所在元素的父元素的`宽度`而不是`高度`（与padding-left和padding-right一样）;
 示例：实现窗体宽度缩放时，让宽度自适应的同时，保持高度与宽度的比例不变，实现方法：利用padding-bottom，如元素宽度为20%，让元素的高度始终是其宽度的一半，则padding-bottom:10%;
 ```css
 .productsWrap span{
   display: inline-block;
   width: 20%;height: 0;padding-bottom: 10%;
   background-color: #B4B8E4;
   text-align: center;
   color: white;
}
 ```
 ```html
 <div class="productsWrap">
   <span>block part</span>
   <span>block part</span>
   <span>block part</span>
   <span>block part</span>
</div>
 ```
 12. contenteditable属性
  兼容各个浏览器，作用是让元素可编辑状态;
 ```html
 <div contenteditable="true">可以编辑里面的内容</div>
 ```

 13.Javascript的垃圾回收机制及原理
  使用计数垃圾收集、循环引用

14.实现品字布局
```css
*{margin:0;padding: 0;}
 .pinWrap .headWrap{margin:0 auto;background-color: #505080;}
 .pinWrap .headWrap, .pinWrap .left, .pinWrap .right{width: 100px;height: 100px;}
 .pinWrap .left, .pinWrap .right{display: inline-block;}
 .pinWrap .left{margin-left: -200px;background-color: #7272A7;}
 .pinWrap .right{margin-left: 50%;background-color: #B4B8E4}
```

```html
<div class="pinWrap">
  <div class="headWrap"></div>
  <div class="bottWrap">
     <p class="right"></p>
     <p class="left"></p>
  </div>
</div>
<!-- pinWrap end -->
```
