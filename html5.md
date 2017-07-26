1.废除的标签

（1）能使用css代替的元素

 big、basefont、center、font、s、strike、tt、u

 s、strike可以使用del代替；tt可以使用font-family代替；

 (2)不再使用frame框架

 (3)只有部分浏览器支持的元素

  applet、marquee、bgsound、blink

  applet可由embed元素或object元素代替；bgsound可由embed元素或object元素代替；不过sound元素可由audio元素代替；marquee可由JavaScript编程代替；

2.新增属性

(1)与表单相关
  autofocus属性、placeholder、指定form属性、required属性、input元素新增了autocomplete、min、max、multiple、pattern和step;fileset增加了disabled;novalidate属性;

(2)与链接相关的属性
   a、area添加了media属性；<br/>
   area添加了hreflang属性与rel属性；<br/>
   link元素属性新增sizes;<br/>
   base元素添加了target<br/>

(3)其他属性

ol新增reversed;media增加charset;<br/>
menu新增type和label；<br/>
style元素添加scoped属性；<br/>
script增加async属性；<br/>
html元素新增manifest;<br/>
为iframe元素新增3个属性sandbox、seamless、srcdoc<br/>

结构元素：header、footer
页面交互元素：details、menu、command和meter

3.网络通信API
  otherwindow.postMessage(message,tragetOrigin);跨域页面之间获取数据

 后台线程处理，worker没有访问document对象的权限
  ```javascript
    var worker = nre Worker("numberAdd.js");
    worker.postMessage();

    worker.addEventListener("message",function(event){
      alert(event.data);
    },false);
  ```
  4.离线缓存
  manifest文件

  5.拖放操作

  元素设置draggable为true,dataTransfer对象；
