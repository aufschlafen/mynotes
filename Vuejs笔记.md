---
typora-root-url: ./
---

## Vuejs笔记

##### 1.认识

vue是一个渐进性框架，可以将vue嵌入应用中

![1569288544325](C:\Users\wxj123\AppData\Roaming\Typora\typora-user-images\1569288544325.png)

##### 2.实例

```javascript
html:<div id="id">{{message}}</div>
var x = new Vue({
    el:'#id', //挂载在那个元素
    data:{
        message:'你好'
    }
})
```

v-for:

官方推荐使用v-for时候，给对应的元素或组件添加上:key属性

```vue
<li v-for="item in movies">{{item}}</li>
```

计数器：(按钮交互事件)

```vue
>h2>{{counter}}</h2>
<button v-on:click="counter++">+</button>
<button v-on:click="counter--">-</button>

var app = new Vue({
			el:'#app',
			data:{
				message:'get!',
				movies:['aaaa','bbbb','cccc','dddd'],
				counter:0
			},
			method:{//方法 
			add:function(){},
			sub:function(){}
}
		})
```

**methods在Vue对象中定义方法**

**@click用于监听某个元素的点击事件，并且需要指定当发生点击是，执行的方法**

------

### Vue的MVVM(Modal ViewModal View)

![1569372995574](C:\Users\wxj123\AppData\Roaming\Typora\typora-user-images\1569372995574.png)

##### 创建Vue的option属性

el: String|HTMLElement

data:Object|Function

methods:{key:string|Function}              //在类里面的叫方法(function),在外面直接定义的叫方法(methods)

------

#### Vue的生命周期函数

```javascript
call:function(){}//生命周期函数
```

![img](http://www.ailbk.com/uploads/allimg/180928/1-1P92R11500602.jpg)

------

#### Vue的Templates

Mustache语法 ：{{}}

```javascript
<li v-for="(m,index) in movies">{{index}}-{{m}}</li>
```



指令：v-once  指定不可以更改(const)

​	  v-html:  表示以html格式展示这个数据

​	 v-text: 以文本方式展示出来 （会覆盖标签里的原有文本）

​	  v-pre: 不进行编译，依原有方式展示出来

​	 v-cloak:防止未编译之前，div有一个属性是v-cloak,在vue解析之后，div没有一个属性v-cloak,可以根据v-cloak写出是否显示的样式

**关于属性的指令**

v-bind:  动态的改变属性 如：

```javascript
<img v-bind:src="">
<img v-bind:href="aHref">
<img :src="">   (语法糖的写法)
<h2 v-bind:class="{key:value,key2:value2}"> // 动态绑定class类名 （对象语法）

<h2 v-bind:class="{类1：boolean,类2“boolean}">{{message}}</h2> //通过boolean来控制类名是否增加

例子：
<body>
		<div id="app">
			<h1>{{message}}</h1>
			<h2 v-bind:class="{red:isActive}">{{message}}</h2>
			<button v-on:click="btnClick"> click me</button>
		</div>
		
		<script src="vue.js"></script>
		<script>
			const app = new Vue({
				el:'#app',
				data:{
					message:'hello',
					isActive:true
				},
				methods:{
					btnClick:function(){
						this.isActive = !this.isActive;
					}
				}
			})
		</script>
	</body>

```



```javascript
methods:getClasses:function(){
    return {active:this.isActive}
}//Vue的内容
<h2 v-bind:class="getClasses()">{{message}}</h2> 
```

##### 数组语法

```javascript
<h2 :class="[active,line]">{{message}}</h2> 
methods:{
    getClasses:function(){
        return [this.active.this.line]
    }
}
```

???根据v-for出来的按钮，来改变相应的class属性

-----

v-bind 动态改变样式

```html
<h2 :style="{key(属性):value(属性)}"></h2>
<h2 :style="{font-size:"50px"}"></h2>		//注意加引号

<h2 :style="{font-size:	finalSize}">{{message}}</h2>
<h2 :style="[baseStyle]">{{message}}</h2>
data:{
finalSize:'100px',
baseStyle:{backgroundColor:'red','fontSize':20px}
}

```

-----

### 计算属性  computed

computed:只会计算一次,会缓存

```javascript
<h1>{{totalprice}}</h1>
computed:{
    totalPrice:function(){
        let result = 0;
        for(let i =0;i<this.books.length;i++){
            result += this.books[i].price;
        }
        return result;
        //或
        for(let i in this.books){}
        for(let book of this.books){}	
    }
}
```

每一个计算属性都包括getter和setter

```javascript
computed{
   fullName:{//认为是一个属性
    get:function(){return this.firstName}// 只读属性
	} 
}
```

-----

ES6语法：

let var

const:优先使用const,  常量，初始化必须赋值。常量指向的对象不能修改，但是可以改变对象内部的属性（没有改变内存地址）。

**对象的增强写法**

```javascript
const name= 'why'
const age = 18;
const address = 'xxx'
const obj = {//es6自动将上面变量赋予到对象中，成为键值对
    name,
    age,
    address
}

函数的增强写法：
const obj = {//不用 run:function(){}
    run(){},
    eat(){}
}
```

----

### 事件监听    v-on

```html
<button v-on:click="increment">+</button>
<button @click="increment">+</button>    //语法糖
```

在事件定义时候，写方法省略了小括号，但是方法本身是需要一个参数的，这个时候，Vue会默认将浏览器生产的event事件对象作为参数传入到方法中

方法定义的时候，既需要event又需要其他参数，通过 **$event**

```html
<button @click="btn3Click('abc',$event)">anniu</button>
```

**v-on 修饰符**

**.stop :**一般嵌套组件被点击时，外层div事件也会被触发，称之为事件冒泡，.stop作为修饰符会阻止事件冒泡

```vue
<div @click="divClick">
    <button @click.stop="btnClick">按钮</button>
</div>>
```

**.prevent**  :阻止默认事件，如submit的默认提交事件，如需自己监听再提交即可使用.prevent修饰符

**.{keyCode|keyAlias}** :只是事件从特定键触发时才触发回调

```vue
<input type="text" @keyup="keyup">
<input type="text" @keyup.enter="keyup">//回车键触发函数
```

**.native**:监听组件根元素的原生事件  ，在自定义的组件中使用

**.once** 只触发一次回调

```html
 <button @click.once="btnClick">按钮2</button>
```

---

#### 条件判断

```html
<h2 v-if="score>=90"></h2>
<h2 v-else-if="score>=90"></h2>
<h2 v-else></h2>
```

小问题：

```html
		<div id="app">
			<span v-if="isUser">
				<label for="account">用户账号</label>
				<input type="text" id="account" placeholder="用户账号">
			</span>
			<span v-else>
				<label for="account">用户邮箱</label>
				<input type="text" id="account" placeholder="用户邮箱">
			</span>
			<button @click="isUser = !isUser">change</button>
		</div>
		<script src="vue.js"></script>
		<script type="text/javascript">
			const app = new Vue({
				el: '#app',
				data:{
					isUser:true
				},
				method:{
					email:function(){
						this.isUser = !this.isUser;
					}
				}
			})
		</script>
```

当没有输入内容是，切换了类型，会发现文字依然显示之前输入的内容，是因为：Vue在进行DOM渲染，处于性能考虑，会尽量服用已存在的元素，而不是创建新的元素。 **如果不希望出现重复利用的的问题，需要向input添加不同的key**  。

**v-show**  :决定是否显示 (boolean)   元素被隐藏，v-if决定是否显示时，直接删除那一个元素

----

##### 数据是响应式的

Vue会自动监听数组数据的变化

```js
push() //数组向末尾增加数据
pop()	//弹出数组末尾的数值
shift()	//删除元素的第一个值
unshift()//在数组前面添加元素 unshift(1,2,3) unshift(1,2)都行
splice(start,p1,p2)//删除元素（第二个变量表示删除几个元素，如果没有指定，就删除所有元素）/插入元素/替换元素(第二个表示换几个元素，后面用于替换奇幻其他元素,splice(start,2,12,23))
sort()//排序
reverse()//反转

Vue.set(this.array,0,'bbb')//通过索引值修改数组中的元素

function sum(...num){} //可变参数，...num是个数组，可以容纳数量不同的参数

```

----

### 过滤器 filter

```js
全局过滤器：

Vue.filter('globalFilter', function (value) {

  return value + "!!!"

})

组件过滤器（局部）：

filters:{

    componentFilter:function(value){

         return value + "!!!"

    }

  }
用法：
1.{{ 'ok' | globalFilter }}
2.<div v-bind:data="'ok' | globalFilter" ></div>

```

{{message|f1|f2}}中message是作为参数传给f1,f1的返回值作为参数传给b2,最终结果是由f2显示的

----

### JS高阶函数

**filter** 的回调函数必须返回boolean值，filter内部会自动生成数组，当返回true的时候函数内部会自动将这次回调的n加入到新的数组中,当返回true的时候自动过滤掉这次的n

```js
const nums = [10,1,2,3,4,5]
let new = nums.filter(function(n){
    return n<3
})
```

编程范式：命令式编程/声明式编程

​		面向对象编程(第一公民：对象)/函数式编程（第一公民：函数）

**map**：调用传入的函数，得到新的array作为结果

```js
let newNums = num.map(function(n){
    return n*2;
})//newNums会得到新的数组
```

**reduce**:将一个函数作用于这个Array的[x1,x2,x3],这个函数必须接受两个参数，reduce将结果和序列的下一个元素做累计计算

```js
var arr = [1, 3, 5, 7, 9];
arr.reduce(function (x, y) {
    return x + y;
}); // 25
```

```js
let total = nums.filter(function(n){
    return n<100
}).map(function(n){
    return n*2
}).reduce(function(preValue,n){		//n是intitalValue,可选
    return preValue+n
},0)

let total = nums.filter(n =>n<100).map(n=>n*2).reduce((pre,n)=>pre+n)//箭头函数！！！

return this.books.reduce(function(proValue,book){
    return preValue + book.price*book.count
},0)
```

----

**v-model:checkbox**:(1)单个勾选框，v-model即为bool，此时input的value并不影响v-model的值（2）多个复选框：可以选中多个，所以对应的data属性是一个数组，当选中一个的时候，就会将input的value添加到数组中

`<input type="checkbox" v-model="hobbies" value="piano">//hobbies是数组`

**v-model:select**:也可以选择单个或多个值

```js
<select name="ig" v-model="fruit" >
    <option value="aaa">aaa</option>
    <option value="bbb">bbb</option>
    <option value="ccc">ccc</option>
    <option value="ddd">ddd</option>
</select>
<h5>{{fruit}}</h5>
```

#### 值绑定 :绑定value  ":value"  相当于v-bind:value

```js
<label v-for="item in oHobbies" :for="item">
    <input type="checkbox" :value="item" v-model="hobbies">{{item}}
   </label>
```

-----

### 修饰符

**lazy**：懒加载。默认情况v-model是在input事件中同步输入框的数据的，一旦有数据发生改变对应的data中的数据自动发生改变.**v-model.lazy**可以使数据失去焦点或者回车的时候才更新

**number**:v-model在给变量赋值的时候总会变成字符串类型，v-model.number会自动转变成number类型

**trim**: 删除输入的左右两侧的空格

----

### Vue组件化思想：

提供了一种周次昂，让我们可以开发出一个独立客服用的小组件来构造我们的应用。

任何应用都会被抽象成一颗组件树

![](E:\pmh\笔记\img\1.png)

**注册组件的基本步骤**

+ 创建组件构造器
+ 注册组件
+ 使用组件

![](E:\pmh\笔记\img\2.png)

es6就可以用extend实现类的继承

es6 tips:``也可以定义字符串（tab上面的点点），可以有换行的功能

```js
<div id="app">
    使用组件
    <cpn></cpn>
    <cpn></cpn>
    <cpn></cpn>
    <cpn></cpn>
</div>
<script src="vue.js"></script>
<script>
    //1.创建组件构造器对象
    const cpn = Vue.extend({
        template:`<div>
        <h2>xxxxxx</h2>
        <h2>yyyyyyy</h2>
        </div>`
    })

//2.注册组件
Vue.component('cpn',cpn)
const app = new Vue({
    el:'#app',
})
</script>
```

Vue CLI3.x(构建Vue的项目)  Vue的脚手架

**全局组件和局部组件：**

上面的案例就是全局组件，可以在多个Vue的实例下面使用；

**局部组件**：注册在Vue实例中的components中

```js
components:{
    cpn:conc
}
```

#### 父组件和子组件

````js
//子组件
			const cpn = Vue.extend({
				template:
				`<div>
					<h2>xxxxxx</h2>
					<h2>yyyyyyy</h2>
				</div>`
			})
			//父组件
			const cpn1 = Vue.extend({
				template:
				`
				<div>
					<h2>son</h2>
					<h2>sonssss</h2>
					<cpn1></cpn1>
				</div>
				`,
				components:{
					cpn1:cpn
				}
			})
			
			//root组件
			const app = new Vue({
				el:'#app',
				components:{
					cn:cpn1
				}
			})
````

**注册组件语法糖**

```js
Vue.component('cpn1',{
    template:`
    <div>
    <h2>son</h2>
    <h2>sonssss</h2>
    <cpn1></cpn1>
    </div>	
	`
})//注册全局组件

const app =new Vue({
    el:
    components:{
    'cpn1':{
    template:`
    <div>
    <h2>son</h2>
    <h2>sonssss</h2>
    <cpn1></cpn1>
    </div>	
	`
}//局部组件语法糖
}
})
```

模板的分离写法:注意类型是text/x-template

```js
<script type="text/x-template" id="xxx">
 模板内容   
 </script>

Vue.component('cpn',{
    template:'#cpn'
})
```

也可以使用template

```htm
<template id="cpn">
	模板内容
</template>
```

**组件内部是不能直接访问vue实例中的数据**，组件中的data属性就是来存储数据的，data必须是函数

```js
Vue.component('cpn',{
    template:'#cpn',
    data(){
        return{title:'abc'}//返回一个对象
    },
    methods{
    
	}
})
```

当组件被服用时，如果data不是一个函数而是一个对象，那么所有复用的组件所指向的都是同一个内存地址，这样会引起数据混乱，而data强制成为一个函数并返回一个对象时，复用的组件所指向的内存地址就是新的了。

**父子组件的通信**：

1.通过props向子组件传递消息（子组件向父组件中发送emit传递消息）

在组件中，使用选项props来声明从父级接受到的数据：props的值有两种 

+ 字符串数组，数组中的字符串就是传递的名称

+ 对象，对象可以设置传递的类型，也可以设置默认值等 

  ```js
  <div id="app">
  			<cpn v-bind:cMovies="movies" :cmessage="message">
  				
  			</cpn>
  		</div>
  		
  		<template id="cpn1">
  			<p>{{cMovies}}</p>
  		</template>
  		<script src="vue.js"></script>
  		<script>
  			const cpn = {
  				template:'#cpn1',
  				props:['cMovies','cmessage']
                 
  			}
  			
  			//root组件
  			const app = new Vue({
  				el:'#app',
  				data:{
  					message:'hello',
  					movies:['海王','海贼王','海尔兄弟']
  				},
  				components:{cpn}
  			})
  		</script>
  
    也可以规定props类型
    props:{
        //cmovies:Array,
        //cmessage:String
        cmessagr:{
            type:string,
                default:'aaaa',
                    required:true//必须传值
        }
    }
  ```

  ![](E:\pmh\笔记\img\3.png)

**props中的驼峰标识**：Vue 能够正确识别出小驼峰和下划线命名法混用的变量，如这里的`forChildMsg`和`for-child-msg`是同一值。(v-bind:不支持驼峰！会显示不出来，但是 :c-info表示cInfo是可以的)

当组件中有很多标签时，必须有一个根元素

2.**子传父**通过事件向父组件发送消息

```js
<!-- 父组件模板 -->
		<div id="app">
			<!-- v-bind -->
			<son @item-click="cpnClick"></son>//绑定item-click事件
		</div>
		
		<!-- 子组件模板 -->
		<template id="cpn">
			<div>
				<button v-for="item in categories" @click="btnClick(item)">{{item.name}}</button>
			</div>
		</template>
		<script src="vue.js"></script>
		<script>
			const son = {
				template:'#cpn',
				data(){
					return{
						categories:[
							{id:'aaa',name:'strawberry'},
							{id:'bbb',name:'apple'},
							{id:'ccc',name:'lemon'},
							{id:'ddd',name:'melon'},
						]	
					}
				},
				methods:{
					btnClick(item){
						this.$emit('item-click',item)//自定义事件
					}
				}
			}
			
			const app =new Vue({
				el:'#app',
				components:{
					son	//注册组件
				},
				methods:{
					cpnClick(item){//对应v-bind监听到子组件在html中的自定义的事件
						console.log(item);
					}
				}
			})
```

#### 父子组件的访问方式(操作对象)

1.父访问子  使用$chirdren 或 $ref

$ref必须要先加载在标签上（对象类型） ref='bbbb'

2.子访问父 $parent

```js
const app = new Vue({
    el:'#app',
    methods:{
    },
    components:{
        cpn:{
            template:'#cpn',
            methods:{
                btnClick(){
                    console.log(this.$parent)
                }
            }
        }
    }
})
```

访问根组件：$root ,直接访问Vue实例

----

### 插槽 slot（替换改为v-slot）

 组件的插槽让封装的组件更有扩展性，使用者可以决定组件内部展示什么

```js
<template id="cpn">
	<slot> </slot>  //添加插槽
</template>

<cpn><h1>xxx</h1> </cpn> //h1会在组件中的slot的地方显示
```

slot还可以设置默认值`<slot><div>111</div></slot>` ,如果组件没有指定，则会使用默认值

如果有多个值，同时放入到组件进行替换，一起作为替换元素

**具名插槽**：`<slot name="xxx"></slot>`

使用时：`<cpn><span slot="xxx">titlt</slot></cpn>`

#### 编译作用域

组件使用到的变量,Vue会第一时间去模板中定义的变量里去查找，而不是去组件中查找

```html
<cpn v-show="isShow">会去模板里找变量  </cpn>

<template>
    <h2 v-show="isshow">
        会去组件中找变量
    </h2>
</template>
```

#### 作用域插槽

父组件替换插槽的标签，但是内容由子组件来提供

如：父组件希望子组件将子组件自身的数据不一样的展示

```html
目的是获取子组件的pLanguage
<cpn>
	<template slot-scope="slot"></template>
</cpn>

<template id="cpn">
	<div>
 		<slot :data="pLanguages">
        	<ul>
                <li v-for="item in pLanguage"></li>
            </ul>
        </slot>   
    </div>
</template>

const app =new Vue({\
	components:{
		cpn:{
		template:'#cpn',
		data(){
		return{
	pLanguage:['xxx']
}
}
}
}
})
```

### 模块化开发:导出，导入

模块化雏形

```js
var moduleA = (function(){
    return something//moduleA就是简单的模块化，避免冲突，增加代码的重用
})
```

常见的模块化规范：CommonJs,AMD,CMD,Es6的Modules

#### CommonJS

**导出**：一个js文件可以看做一个模块化，

```js
module.exports={
    flag:true,
    test(a,b){
        return a+b;
    },
    demo(a,b){
        return a*b
    }
}
```

**导入**：

```js
var {flag,sum} =required('xxx.js')
var a = required('xxx.js')
```

#### ES6的模块化：export.import

`<script src="xxx" type="module"></script>` xxx作为一个模块，具有新的作用域

-----

## webpack

从本质上来讲,webpack是一个现代的js应用的静态**模块打包**工具

打包：grunt/gulp/webpack/rollup

模块化规范：AMD,CMD,CommonJS,ES6等规范

webpack可以让我们可能进行模块化开发，而且会帮助我们处理模块间的依赖关系，css,图片,json文件都可以被webpack当做模块来使用

webpack打包过程中，可以对资源进行处理，比如压缩图片，将scss转成css，将ES6语法转变成ES5等等。

**和grunt/gulp的对比**：

grunt/gulp的核心是task，并且自定义task处理的事务，然后依次执行task，让整个流程自动化，所以也被称为前端自动化任务管理工具

grunt/gulp更加强调前端流程的自动化，模块化不是核心。webpack更加强调模块化开发管理，而文件压缩合并、预处理是他附加功能。

dist目录是用于发布的文件夹

**webpack打包**：webpack ./src/main.js ./dist/bundle.js   将main文件打包到bundle.js

**webpack的配置**:webpack.config.js（固定的）

```js
const path = require('path')//动态获取路径

module.exports={
    entry:'./xxx.js',//入口
    output:{//出口
        path:path.resolve(_dirname,'dist'), //绝对路径,动态获取
        filename:''
    }
}
```

在cmd中使用npm init命令初始化package.json文件,编写webpack.config.js文件将命令简化为webpack,当命令很长的时候使用npm run build(build是自定义在package.json文件上的命令指令)

当希望webpack转化不同种的文件时，需给webpack装载不同的loader（安装loader的命令见webpack官网）

css-loader只负责将css文件加载，style-loader则负责将样式添加到Dom里面

图片的loader:url-loader