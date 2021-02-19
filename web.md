## HTML

#### 1.Doctype

\<!Doctype>位于整个文档最前面，告诉浏览器的解析器，用什么文档类型规范解析这个文档

 严格模式的排版和 JS 运作模式是 以该浏览器支持的最高标准运行。在混杂模式中，页面以宽松的向后兼容的方式显示。模拟老式浏览器的行为以防止站点无法工作。
DOCTYPE不存在或格式不正确会导致文档以混杂模式呈现。 

#### 2.浏览器内核

1. Trident内核代表产品Internet Explorer，又称其为IE内核。Trident（又称为MSHTML），是微软开发的一种排版引擎。使用Trident渲染引擎的浏览器包括：IE、傲游、世界之窗浏览器、Avant、腾讯TT、Netscape 8、NetCaptor、Sleipnir、GOSURF、GreenBrowser和KKman等。
2. Gecko内核代表作品Mozilla FirefoxGecko是一套开放源代码的、以C++编写的网页排版引擎。Gecko是最流行的排版引擎之一，仅次于Trident。使用它的最著名浏览器有Firefox、Netscape6至9。
3. WebKit内核代表作品Safari、Chromewebkit 是一个开源项目，包含了来自KDE项目和苹果公司的一些组件，主要用于Mac OS系统，它的特点在于源码结构清晰、渲染速度极快。缺点是对网页代码的兼容性不高，导致一些编写不标准的网页无法正常显示。主要代表作品有Safari和Google的浏览器Chrome。
4. Presto内核代表作品OperaPresto是由Opera Software开发的浏览器排版引擎，供Opera 7.0及以上使用。它取代了旧版Opera 4至6版本使用的Elektra排版引擎，包括加入动态功能，例如网页或其部分可随着DOM及Script语法的事件而重新排版。

#### 3.html5新内核

画板：canvas

音频控件：video,audio

语义化控件：nav,section,footer,header

表单控件:calendar,date,time,email,url,search

存储技术：localStroage,sessionStroage

新的技术：webworker,websocket,Geolocation

#### 4.web标准和w3c标准

标签闭合，标签小写，不乱嵌套，使用外链形势的css和js,结构层，表现层，行为层分离

#### 5.iframe的缺点

1.会阻塞页面的onload事件2.搜索引擎不能解决iframe页面，不利于seo

#### 6.canvas和svg的区别

svg有单独的节点，放大不会有锯齿，矢量图

canvas绘制出来的图片是一个画布，放大会有锯齿

#### 7.输入网址到出现页面发生了什么

1.域名解析

2.TCP三次握手

3.建立TCP连接后发起http请求

4.服务器端相应http请求，浏览器得到html代码

5.浏览器解析html代码，并请求html代码中的资源

6.浏览器对页面进行渲染呈现给用户

#### 8.前端性能优化：

1.请求数量：合并脚本和样式,css sprites,拆分初始化负载，划分主域

2.请求带宽：开启Gzip，精简Javascript,移除重复脚本，图像优化

3.缓存利用：使用CDN,s使用外部JS和css,添加expires,减少DNS查找，配置ETAG,使ajax可缓存

4.页面结构：css放在顶部，js放在尾部

5.代码校验：避免css表达式，避免重定向。

#### 9.减少页面加载时间

尽量减少http请求数量；服务器开启gzip压缩；css样式的定义放置在文件头部....

#### 10.优雅降级、渐进增强

优雅降级：先完成所有功能，再根据低版本浏览器做兼容

渐进增强：先根据低版本的浏览器进行基本的功能建筑，然后再根据高版本浏览器丰富交互，

#### 11.web应用从服务器主动推送Data到客户端的方式

1.html5 websocket

2.webSocket 通过flash

3.xhr长时间连接

4.script标签的长时间连接（可跨域）

#### 12.JS请求后的缓存处理地方

1.浏览器端存储

2.浏览器端文件缓存

3.http缓存304

4.服务器端文件类型缓存

5.表现层和Dom缓存

## CSS

#### 1.display:none和visibilty:hidden的区别

display:none隐藏但是也会取消布局中的空间

visbility:none隐藏但是保留空间

#### 2.link和@import区别

link是html的标签，引入的css被同时加载，引入的权重较重

@import是css提供的标签，引入的文件在页面加载完毕后被加载，引入的权重较轻，IE5+才能识别

#### 3.css权重优先顺序：

```js
 !important > 行内样式 > ID > 类、伪类、属性 > 标签名 > 继承 > 通配符 
```

| 选择器         | 权重 |
| -------------- | ---- |
| 通配符         | 0    |
| 标签           | 1    |
| 类、伪类，属性 | 10   |
| ID             | 100  |
| 行内样式       | 1000 |
|！important      |1/0(无穷大)|

#### 4.calc()、 @support、@media各自含义和用法

@support 判断是否支持某个css属性，满足的话和不满足的都可以使用不同样式。

calc() 用于动态计算长度值

@media 查询，你可以针对不同的媒体类型定义不同的样式， 可以针对不同的屏幕尺寸设置不同的样式，特别是如果你需要设置设计响应式的页面，@media 是非常有用的

#### 5.样式顺序

**上右下走**

#### 6.rem em vh px各个意义

**rem**:相对于根元素的html，通常的给html设置一个字体大小

**em:**子元素的em是根据父元素的字体大小来决定的，元素的width/margin/padding/height是相对于该元素的字体大小。

**vh:** 视窗的宽度和高度，相对于屏幕高度和宽度的1%.

**px:** 相对于显示器屏幕分辨率

#### 7.三角形画法：

```css
.triangle{
    width:0;
    height:0;
    border-width:100px;
    border-style:solid;
    border-color:transparent #0099CC transparent transparent;
    transform:rotate(-90deg)
}
```

#### 8.清除浮动的几种方式

1.添加一个新的div,使用clear:both

2.父类div定义伪类:after和zoom

3.父级div定义overflow:hidden

4.父级div也浮动，并且定义宽度

5.结尾处加`<br>` 

```css
.clearfix:after{visibility:hidden;display:block;font-size:0;content:" ";clear:both;height:0}
.clearfix{display:inline-table}
.clearfix{height:1%}
.clearfix{display:block;*zoom:1}
```

#### 9.css3新特性

1.新增css选择器

2.border-radius

3.多列布局

4.阴影和反射

5.text=-shadow

6.线性渐变

7.transform

8.动画效果



## Javascript

#### 1.闭包

为了设计私有的方法和变量。优点是可以避免全局变量的污染，缺点是闭包会常驻内存，增加内存使用量，容易造成内存泄露。

 当一个函数的返回值是另外一个函数，而返回的那个函数如果调用了其父函数内部的其它变量，如果返回的这个函数在外部被执行，就产生了闭包。 

> 闭包的三个特性：
>
> 1.函数嵌套函数
>
> 2.函数内部可以引用外部的参数和变量
>
> 3.参数和变量不会被垃圾回收机制回收

```js
function add(){
    var count=0;    //函数全局作用域 标记为flag2
    return function(){
        count+=1;   //函数的内部作用域
        alert(count);
    }
}
var s = add()
s();//输出1
s();//输出2
```



#### 2.Cookie

**限定性**：每个特定的域名最多生成20个cookie

>  1.IE6或更低版本最多20个cookie
> 2.IE7和之后的版本最后可以有50个cookie。
> 3.Firefox最多50个cookie
> 4.chrome和Safari没有做硬性限制 

IE和Opera会清理最近少用的cookie，firefox会随机清理Cookie,最大为4096

**优点：** 极高的扩展性和可用性

**缺点：** 1.ta的限定性2.安全性，可能被人拦截

#### 3.浏览器本地存储

webStorage:

**sessionStorage**: 本地存储会话中的数据，只能在会话中使用，会话销毁数据也会随之销毁

**localStorage**:用于持久化的本地存储，除非主动删除数据，否则数据不会过期

webStorage相比于cookie存储量更大，cookie会在每一个新页面请求的时候都会被发送过去，还需要指定作用域，不可以跨域使用，并且需要自己封装setCookie,getCookie;但是webStorage拥有自己的setItem,getItem等方法。ie7以下不支持web Storage,但是可以使用userData.

#### 4.防抖、节流

**防抖**：触发事件后再n秒内函数只能执行一次，如果在n秒内又触发了事件，则会重新计算函数执行事件

 当持续触发事件时，一定时间段内没有再触发事件，事件处理函数才会执行一次，如果设定的时间到来之前，又一次触发了事件，就重新开始延时。如下图，持续触发scroll事件时，并不执行handle函数，当1000毫秒内没有触发scroll事件时，才会延时触发scroll事件。 

 将几次操作合并为一此操作进行。原理是维护一个计时器，规定在delay时间后触发函数，但是在delay时间内再次触发的话，就会取消之前的计时器而重新设置。这样一来，只有最后一次操作能被触发。 

```js
//非立即执行：
function debounce(func,wait){
    let timeout;
    return function(){
        let context = this;
        let args = arguments;
        if(timeout)clearTimeout(timeout);
        timeout = setTimeout(()=>{
            func.apply(context.args)
        },wait)
    }
}
//立即执行：
function debounce(func,wait){
    let timeout;
    return function(){
        let context = this;
        let args = arguments;
        if(timeout)clearTimeout(timeout);
        let callNow = !timeout;
        timeout = setTimeout(()=>{
            timeout = null;
        },wait)
        if(callNow)func.apply(context,args)
    }
}
```

**节流：**所谓节流，就是指连续触发事件但是在n秒内中执行一次函数。

 持续触发scroll事件时，并不立即执行handle函数，每隔1000毫秒才会执行一次handle函数。 

 使得一定时间内只触发一次函数。原理是通过判断是否到达一定时间来触发函数 

```js
//时间戳版
function throttle(func,wait){
    let previous = 0;
    return function(){
        let now = Date.now();
        let context = this;
        let args = arguments;
        if(now-previous > wait){
            func.apply(context,args)
            previous = now;
        }
    }
}
//定时器版
function throttle(func, wait) {
    let timeout;
    return function() {
        let context = this;
        let args = arguments;
        if (!timeout) {
            timeout = setTimeout(() => {
                timeout = null;
                func.apply(context, args)
            }, wait)
        }

    }
}
```

#### 5.跨域

只要有**域名、协议、端口**有一个任何一个不同，都是跨域。

解决办法：

```js
jsonp
iframe
window.name
window.postMessage
服务器设置代理页面
```



#### 6.变量取名

 变量命名必须以字母、下划线”_”或者”$”为开头。其他字符可以是字母、_、美元符号或数字。 

#### 7.浏览器内核

渲染内核：主要负责网页的html，xml,整理信息结合css渲染页面，计算显示方式

js内核：解析和执行js来达到网页的动态交互效果

#### 8.this的理解

this指向函数的直接调用者，如果有new关键字，this指向new出来的对象。在事件中,this指向触发这个时间的对象。

#### 9.null和undefined

undefined表示不存在这个值。

null:变量被定义复制可，但为空，没有任何属性和值。在验证null时，一定要使用===

#### 10.Promise

promise保存异步操作。Promise对象有两个特点：1.对象的状态不受外界硬性，有三种状态pending、Resolved、Rejected

2.一旦状态改变就不会再变

#### 12.JS检查一个变量是String类型

```js
typeof(obj) == 'string'
typeof obj == 'string'
obj.constructor === String
```

#### 13.声明提前

将使用var定义的变量声明提升到对应作用域的最顶部，赋值部分位置不变

如果使用声明的方式定义的函数，将整个函数都提升到作用域的最顶部

如果是表达式的方式定义的函数，只提示声明，不提升赋值

## vue

#### 1.MVVM:

Model:数据模型，可以在Model中定义数据修改和操作的业务逻辑。

View代表UI组件，负责将数据模型转换成UI展现出来。

viewModel:监听模型数据的改变和控制视图行为，处理用户交互，连接Model和View.

#### 2.vue的生命周期

beforeCreate:在数据观测和初始化事件还未开始时

created:完成数据观测、属性和方法的运算，初始化事件，$el属性还没有完全显示出来。

beforeMount:在挂载开始之前被调用，相关的render首次被调用，编译模板并将data里面的数据和模板生成html,准备挂载到html上

mounted:挂载完成，也就是模块中的html渲染到了html页面，只会执行一次

beforeUpdate: 在数据更新之前被调用，发生在虚拟DOM重新渲染和打补丁之前，可以在该钩子中进一步地更改状态，不会触发附加地重渲染过程 

updated: 在由于数据更改导致地虚拟DOM重新渲染和打补丁只会调用，调用时，组件DOM已经更新，所以可以执行依赖于DOM的操作 

beforeDestory:在销毁之前

destoryed:Vue实例销毁

#### 3.v-show和v-if的区别，keep-alive和v-show的区别

v-show是css的display控制显示和隐藏,v-if的组件是真正的渲染和销毁。频繁切换用v-show，否则用v-if

keep-alive是一个内置组件，包裹动态组件的时候，会缓存不活动的组件实例，而不会销毁他们，他只是个抽象组件，不会渲染出节点。

keep-alive是在vue框架层级进行的JS对象渲染,可以使被包含的组件保留状态，或避免重新渲染 。

简单的用v-show,tab切换一般用keep-alive

#### 4.v-for要用key

key是vue中vnode的唯一标记，通过key，diff操作更准确

#### 5.Vue组件的通讯 

https://www.cnblogs.com/queenya/p/13572754.html

父子组件通讯：使用属性和触发事件,props,$emit,this.$emit调用父组件的事件

组件之间没有关系或层级较深：使用自定义事件，event是Vue实例,vue本身就具有自定义事件的能力。 调用自定义事件： event.$emit('xxx', 变量名)；绑定自定义事件：event.$on('xxx', 函数名字)。在beforeDestroy 要做的一件事是及时解绑自定义事件，及时销毁，否则可能造成内存泄漏，写法：event.$off('xxx', 函数名). 

vuex通讯

#### 6.组件渲染和更新

初次渲染过程：1.解析模板为render函数。2.触发响应式，监听data属性getter,setter.3.执行render函数，生成vnode,patch(elem,vnode)

更新过程：1.修改data,触发setter.2.重新执行render函数，生成newVNode.3.patch(vnode,newVnode)

异步渲染：1.回顾$nextTick2.汇总data的修改3.减少DOM操作次数

#### 7.v-modal的使用

v-modal用于表单数据的双向绑定,具体做了两个操作：

(1)v-bind绑定一个value属性.(2)v-on指令给当前元素绑定input事件

#### 8.computed和watch的使用环境

computed:是属性，可以像data中的数据一样使用，当一个属性受多个属性影响就需要用到computed;

watch:类似当一条数据影响到多条数据的时候就使用watch