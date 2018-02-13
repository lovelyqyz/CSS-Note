## Bootstrap ##
Api: [http://v3.bootcss.com/css/](http://v3.bootcss.com/css/)
1.css
  （1）布局容器：.container和.container-fluid（100%宽度）,两者不可互相嵌套；

  （2） col-xs-*(适用于pc端和用移动)、.col-sm-*（适用于平板设备），.col-md-*，.col-ld-*(大屏)，创建基本的栅格类，如：
  ```html
  <div class="row">
  		<div class="col-md-4">the 4</div>
  		<div class="col-md-8">the 8</div>
  	</div>
  ```
  `xs (phones), sm (tablets), md (desktops), and lg (larger desktops)``

  (3)列数>12，应该另起一行进行排列，但由于别的行高不同，导致类似浮动的效果，可采用.clearfix，如：
  ```html
     <divclass="clearfix visible-xs-block"></div>
     ```
  (4)重置偏移，后推或前拉某个列，采用如`col-md-offset-2`

  (5)改变列的顺序：`.col-md-push-*` 和 `.col-md-pull-* `

  （6）p默认字体大小：14px,行高： 1.428；
     `<pclass="lead">...</p>`可让段落突出显示；
      内嵌文本:`<mark>、<del>、<s>、<ins>、<u>、<small>、<strong>、<em>、<b>、<i>`
    （含义：高亮、被删除的文本、无用文本、插入文本、带下划线的文本、小号文本（父类字体大小的85%）、着重、斜体（<b>用于高亮单词或短语，不带任何着重的意味；<i>标签主要用于发言、技术词汇等））；

  (7)文本对齐方式：text-left、text-justify、text-nowrap等
    改变大小写：`text-lowercase、text-uppercase、text-capitalize`
    缩略语（当鼠标悬停在缩写和缩写词上时就会显示完整内容）：<abbrtitle="attribute">attr</abbr>

  (8)地址`<address></address>`在每行结尾添加<br>可以保留需要的样式。

  （9）情境文本颜色：`text-muted，text-primary，text-success，text-info，text-warning，text-danger`，对应的情境背景色，只需将上面的text改为bg.

  (10)快速浮动：pull-left、pull-right（不能用于导航条组件中，用.navbar-left 或 .navbar-right）

  （11）内容块居中：center-block，清除浮动：.clearfix；显示/隐藏：.show/.hide/.invisible

  （12）列表
    无序列表：<ul><li></li></ul>
    有序列表：<ol><li></li></ol>
    无样式列表：<ul class="list-unstyled"><li></li></ul>
    内嵌列表：<ul class="list-inline"><li></li></ul>
    描述列表：
    ```html
    <dl class="dl-horizontal">
      <dt></dt>
      <dd></dd>
    </dl>
  ```
  （13）表单
  ```html
      <div class="form-group">
  	    <label for="exampleInputEmail">Email</label>
  	    <input type="text" id="exampleInputEmail" class="form-control" placeholder="Email">
  	  </div>
      ```
  a.所有设置了`form-control`的input，textarea和select都将默认设置宽度属性为width：100%；

  b. 内联表单：form-inline类，只适用于视口至少在768px宽度时，若小于这个宽度就会使表单折叠；
    一定要为每个输入控件设置label 标签，可以使用sr-only类将其隐藏;
   form-horizonta;
   bootstrap对表单控件的校验状态，如`error、warning和success`状态，都定义了样式，使用时，添加`.has-warning、has-error或 has-success类`到这些控件的父元素即可；
    针对校验状态为输入框添加额外的图标，只需设置相应的`.has-feedback`类并添加正确的图标即可；

  c.下拉列表（select）
    显示多选项：multiple

  d.按钮
   类型：btn-default,btn- primary,btn- success,btn-info,btn-warning,btn-danger,btn-link
   尺寸：btn-lg,btn-sm,btn-xs
   激活状态：添加active类
   禁用状态：disabled

## 2. 组件 ##
（1）下拉菜单
（2）按钮组：按钮式下拉菜单、单按钮下拉菜单、分列式按钮下拉菜单、向上弹出式菜单、
（3）输入框组合：通过在文本输入框input前面、后面或是两边加上文字或按钮，可以实现对表单控件的扩展。为input-group添加input-group-addon或input-group-btn类
 (4)导航：依赖nav类，
（5）导航条
 (6)分页
（7）标签
（8）徽章：给链接、导航等元素嵌套<span class="badge">，可以醒目地展示新的或未读的信息条目；
（9）巨幕：能延伸至整个浏览器视口来展示网站上的关键内容；
（10）缩略图
（11）警告框
（12）进度条
（13）面板

## 3.js插件 ##
（1）事件：bootstrap事件分为不定式（表示在事件开始前被触发），可以使用e.preventDefault( )触发和过去式（在动作执行完毕后发触发）

(2).  让IE浏览器运行在最新的渲染模式下：
  ```html
       <meta http-equiv="X-UA-Compatible" content="IE=edge">
    ```
     让浏览器默认采用高速模式渲染页面：
     ```html
     <mata name="renderer" content="webkit">
     ```
  (3).针对不同屏幕大小的样式设置
    ```css
    /* 小屏幕（平板，大于等于768px） */
    @media (min-width: @screen-sm-min){

    }
    /* 中屏幕（桌面浏览器，大于等于992px） */
    @media(min-width: @screen-md-min){

    }
    /* 大屏幕(大于等于1200px) */
    @media(min-width: @screen-lg-min){

    }
  ```

## css预处理器 ##
     css预处理器：一种语言为css增加一些编程特性，进行web页面样式设计，再编译成css文件，以供项目使用。
### 1.Less ###
    混合（minix）：可将一个定义好的class A引入到class B中，即实现class B继承class A中的所有属性。也可带参数调用，如函数一样。
    安装：npm install -g less
    编译：lessc style.less > style.css

### 2.Sass ###
2.1	less、sass与Stylus 的对比
Sass 和 Less都是标准的CSS语法，默认Sass使用.sass扩展名，而Less使用.less扩展名。Less是基于JavaScript的，在客户端处理的；Sass是基于Ruby的，在服务端处理。
（1）语法：sass与stylus都支持老语法（即不包括花括号和分号方式），如：
`  h1
  color: #0982C1`
（2）变量：sass变量是以$开头（如：`$mainColor: #0982c1;`）；而Less是使用@开头（如：`@mainColor: #0982c1;`）；
        Stylus 对变量名没有任何限定，你可以是 $ 开始，也可以是任意的字符，而且与变量值之间可以用冒号、空格隔开，在 Stylus 的变量名不要用 @ 开头。
（3）嵌套：三者都支持嵌套，如：
```css
  section {
    margin: 10px;
   nav {
    height: 25px;

    a {
      color: #0982C1;
      &amp;:hover {
        text-decoration: underline;
       }
    }
  }
  ```
（4）混入（Mixin）：
  Mixins 有点像是函数或者是宏，当你某段 CSS 经常需要在多个元素中使用时，你可以为这些共用的 CSS 定义一个 Mixin，然后你只需要在需要引用这些 CSS 地方调用该 Mixin 即可；如
  `Sass的混入`：
  ```css
  @mixin error($borderWidth: 2px) {
    border: $borderWidth solid#F00;
    color: #F00;
  }

  .generic-error {
    padding: 20px;
    margin: 4px;
    @ include error(); /* Applies styles from mixin error */
  }
  .login-error {
    left: 12px;
    position: absolute;
    top: 20px;
    @ include error(5px); /* Applies styles from mixin error with argument $borderWidth equal to 5px*/
  }
     ```
  `Less的混入：`
  ```css
  .error(@borderWidth: 2px) {
    border: @borderWidth solid#F00;
    color: #F00;
  }  
  .generic-error {
    padding: 20px;
    margin: 4px;
    .error(); /* Applies styles from mixin error */
  }
  .login-error {
    left: 12px;
    position: absolute;
    top: 20px;
    .error(5px); /* Applies styles from mixin error with argument @borderWidth equal to 5px */
  }
  ```
`Stylus的混入：`
  ```css
  error(borderWidth= 2px) {
    border: borderWidth solid#F00;
    color: #F00;
  }
  .generic-error {
    padding: 20px;
    margin: 4px;
    error(); /* Applies styles from mixin error */
  }
  .login-error {
    left: 12px;
    position: absolute;
    top: 20px;
    error(5px); /* Applies styles from mixin error with argument borderWidth equal to 5px */
  }
```
（5）继承：当我们需要为多个元素定义相同样式的时候，我们可以考虑使用继承的做法。
  ①在sass和stylus里可以如下写：
  ```css
  .block{
    margin: 10px5px;
    padding: 2px;
  }
  p {
    @extend .block; /* Inherit styles from '.block' */
    border: 1pxsolid#EEE;
  }
  ul, ol {
    @extend .block; /* Inherit styles from '.block' */
    color: #333;
    text-transform: uppercase;
  }
  ```
  ②Less类似于混入方式,如：
  ```css
  .block{
    margin: 10px5px;
    padding: 2px;
  }

  p {
    .block; /* Inherit styles from '.block' */
    border: 1pxsolid#EEE;
  }
  ul, ol {
    .block; /* Inherit styles from '.block' */
    color: #333;
    text-transform: uppercase;
  }
```
（6）导入：
    css文件的导入，会出现多次http请求，但css预编译器导入只是语义上包含多个文件，最终结果是一个单一css文件.如：@ import"reset.css";
（7）函数：
  一般会内置一些颜色处理函数来对颜色值进行处理
  
  二、less 与 sass 的区别
  less在如下情形下不能进行覆盖，
  ```css
   .average(@x, @y){
  	@average:((@x + @y)/2);
   }
   div{
	  .average(10px, 20px);
   	padding:@average;

  	.average(15px, 25px);  
     	padding:@average;  //average覆盖不了
    }
  ```
