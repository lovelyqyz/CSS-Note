## 1.transition（转换）
   含义：“CSS的transition允许CSS的属性值在一定的时间区间内平滑地过渡。
   触发动作：这种效果可以在鼠标单击、获得焦点、被点击或对元素任何改变中触发，并圆滑地以动画效果改变CSS的属性值。”
```css
transition: <property> <duration> <animation type> <delay>
```
参考链接：[http://www.php100.com/html/webkaifa/DIV_CSS/2012/1029/11403.html](http://www.php100.com/html/webkaifa/DIV_CSS/2012/1029/11403.html)

##  2.兼容各个浏览器的transform写法 ##
```css
  //Mozilla内核浏览器：firefox3.5+
  -moz-transform: rotate | scale | skew | translate ;
 //Webkit内核浏览器：Safari and Chrome
  -webkit-transform: rotate | scale | skew | translate ;
 //Opera
  -o-transform: rotate | scale | skew | translate ;
 //IE9
  -ms-transform: rotate | scale | skew | translate ;
 //W3C标准
  transform: rotate | scale | skew | translate ;
```
## 3. display:inline-block ##
(1)解决display：`inline-block`造成的间距空白问题
采用纯css解决方法：在父元素中设置font-size:0,用来兼容chrome，而使用letter-space:-N px来兼容safari:
```css
.finally-solve {
  /*根据不同字体字号或许需要做一定的调整*/
  letter-spacing: -4px;
  word-spacing: -4px;
  font-size: 0;
}
.finally-solve li {
  font-size: 16px;
  letter-spacing: normal;
  word-spacing: normal;
  display:inline-block;
  *display: inline;
  zoom:1;
}
```
方法二：
```css
html{-webkit-text-size-adjust:none;}
.parentElme{font-size:0;*word-spacing:-1px; /*修复IE6、7中始终存在的 1px 空隙*/}
.elem{font-size:12px;letter-spacing:normal;word-spacing:normal;}
```
(2)使用ext-align:justify实现列表两端对齐
   好处：无需计算每个列表元素之间的margin间距，更不用去修改父容器的宽度；
  最常见的列表标签-ul, li标签举例，要实现li列表的两端对齐，直接用CSS代码如下：
  ```css
  ul{text-align:justify;}
  li{display:inline-block;}
  ```

a.还需注意的就是列表元素首尾标签留空（或换行），不能够上一个标签组的结束标签与下一个标签组的其实标签连在一起，列表元素不能处在font-size:0的环境下
   ![image](https://github.com/lovelyqyz/CSS-Note/blob/master/images/标签留空.png)

b. 最后一行排列不满的问题：列表（或文字）要两端对齐的前提就是内容必须超过一行，所以解决方法就是在列表（或文字段）的最后创建一个高度为0的宽度100%的透明的inline-block的标签层就可以了
```css
.justify_fix{display:inline-block; width:100%; height:0; overflow:hidden;}
```
如下html
```html
<span class="justify_fix"></span>
```

c.实现最后一行左对齐：
原理与上面的两端对齐一致。就是复制几个列表元素的外层标签，等宽，但高度为0，里面就是个&nbsp;(不可缺)，复制的个数一般就是每行元素的列表个数啦
```html
<span class="list left_fix">&nbsp;</span>
```
```css
.left_fix{height:0; padding:0; overflow:hidden;}
```
参照网址：[http://www.zhangxinxu.com/wordpress/2011/03/displayinline-blocktext-alignjustify%E4%B8%8B%E5%88%97%E8%A1%A8%E7%9A%84%E4%B8%A4%E7%AB%AF%E5%AF%B9%E9%BD%90%E5%B8%83%E5%B1%80/](http://www.zhangxinxu.com/wordpress/2011/03/displayinline-blocktext-alignjustify%E4%B8%8B%E5%88%97%E8%A1%A8%E7%9A%84%E4%B8%A4%E7%AB%AF%E5%AF%B9%E9%BD%90%E5%B8%83%E5%B1%80/)

##  4.font-weight的数值设置 ##
 取值: `normal | bold | bolder | lighter | 100 | 200 | 300 | 400 | 500 | 600 | 700 | 800 | 900 | inherit
 （其中normal = 400 ; bold = 500）`

##  5.移动端样式控制适配 ##
```css
@media screen and (min-width: 320px) {html{font-size:50px;}}
@media screen and (min-width: 360px) {html{font-size:56.25px;}}
@media screen and (min-width: 375px) {html{font-size:58.59375px;}}
@media screen and (min-width: 400px) {html{font-size:62.5px;}}
@media screen and (min-width: 414px) {html{font-size:64.6875px;}}
@media screen and (min-width: 440px) {html{font-size:68.75px;}}
@media screen and (min-width: 480px) {html{font-size:75px;}}
@media screen and (min-width: 520px) {html{font-size:81.25px;}}
@media screen and (min-width: 560px) {html{font-size:87.5px;}}
@media screen and (min-width: 600px) {html{font-size:93.75px;}}
@media screen and (min-width: 640px) {html{font-size:100px;}}
@media screen and (min-width: 680px) {html{font-size:106.25px;}}
@media screen and (min-width: 720px) {html{font-size:112.5px;}}
@media screen and (min-width: 760px) {html{font-size:118.75px;}}
@media screen and (min-width: 800px) {html{font-size:125px;}}
@media screen and (min-width: 960px) {html{font-size:150px;}}
```
##  6.实现图片懒加载 ##
 一般加载分为：预加载和懒加载（包括滚动加载）
（1）将页面中的img标签src指向一张小图片或者src为空，然后定义`data-src`（这个属性可以自定义命名，我才用data-src）属性指向真实的图片，当真正需要加载显示时再将src设置   为data-src的值；
 分析：当img没有设置src的值时，浏览器是不会发出图片加载请求的；
```JavaScript
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
        if(obj.complete){

          //判断是否存在于缓存中
           that.loadImgNumbers++;
           callback(parseInt(that.loadImgNumbers/that.imgNumbers)*100);
           return;
        }
        obj.onload = function(){
           obj.onload = null;
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
##  7.去掉input选中后默认的边框 ##
```css
 input:focus{border:0;outline:none;}
```

##  8.滚动条隐藏 ##
```css
::-webkit-scrollbar{
    width:0;
    height:0;
}
```
上面的样式只对pc端的chrome浏览器起作用，对移动端的浏览器无效。

##  9.理解line-height ##
（1）若一个标签没有定义height属性（包括百分比高度），那么其最终的高度一定是line-height起作用；
（2）行高的表示方法有：px/em，或normal（浏览器的normal值在1~1.2之间），或百分值，或数值，或inherit继承；
     注：150%和1.5在值上是一样的，但它们在继承性上存在差别，百分比会先计算line-height的值，然后以px的单位继承下去；而1.5则是先继承1.5这个值，遍历到对应的标签再计算line-height的像素值；
（3）实现根据文字大小自动调整间距的方法：使用数值，如1.5；
（4）line-height和height可以互换，都可以撑开一个高度，区别在于height会使标签haslayout,而line-height则不会。

##  10.有滚动条时div高度设置 ##
  设计一个div宽高是整个屏幕，页面一般都是可滚动的，所以高度一般是可变的；如下方法可以实现：
  基本原理：div继承的是父元素body的高度,body是继承html的高度，html是继承的浏览器屏幕的高度
  ```css
  html{height:100%;}
  body{height:100%;padding:0;margin:0;}
  .main{background-color: red;width:100%;height:100%;}
```
##  11.强制使用双核浏览器提供webkit内核渲染 ##
```css
	<meta name="renderer" content="webkit" />
```
##  12. 移动端使用rem导致加载时出现抖动问题 ##
   解决方法：在body之前放置下面这行js，而不是在body中或是之后；
```javascript
 <script>
    document.documentElement.style.fontSize = document.documentElement.clientWidth /6.4 + 'px';
</scrip>
```
