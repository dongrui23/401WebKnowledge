
## 变量类型和计算

- JS中使用typeof能得到的哪些类型
图
- 何时使用===，何时使用==
```
if(obj.a == null){
  //obj.a===null || obj.a === undefined
  //jquery源码推荐写法
}
```
- JS中有哪些内置函数
图
- JS变量按照储存方式区分为哪些类型，并描述其特点
图
- 如何理解JSON
图

变量类型
- 值类型vs引用类型
- typeof运算符详解
图
变量计算-强制类型转换
- 字符串拼接
- ==运算符
- if语句
- 逻辑运算

**es6 typeof symbol**

```
var s=Symbol()
typeof s//Symbol
symbol类型
```

## 原型和原型链

- 如何准确判断一个变量是数组类型
- 写一个原型链继承的例子
- 描述new一个对象的过程
- zepto(或其他框架)源码中如何使用原型链
### 构造函数



### 5个原型规则

### 原型链

**原型链**

**instance**



## 作用域和闭包
### 执行上下文
### this

解析器在调用函数每次都会向函数内部传递进一个隐含的参数。

这个隐含的参数就是this，this指向的是一个对象，这个对象我们称为函数执行的上下文对象。

根据函数的调用方式的不同，this会指向不同的对象：

1.以函数的形式调用时，this永远都是window。比如fun();相当于window.fun();

2.以方法的形式调用时，this是调用方法的那个对象;

3.以构造函数的形式调用时，this是新创建的那个对象;

4.使用call和apply调用时，this是指定的那个对象



### 作用域
**es6块级作用域**
### 闭包
```javascript
      var a = [];
      for (var i = 0; i < 10; i++) {
          a[i] = function() {
          console.log(i);
        };
      }
      a[2]();//10
```
-----------------------------------------
## 异步和单线程

同步和异步的区别是什么？分别举一个同步和异步的例子

- 同步会阻塞代码执行，而异步不会

- alert是同步，setTimeout是异步

一个关于setTimeout的笔试题

```javascript
console.log(1)
setTimeout(function(){
  console.log(2)
},0)
console.log(3)
setTimeout(function(){
  console.log(4)
},1000)
console.log(5)
//1-3-5-2-4
```

前端使用异步的场景有哪些？

- 定时任务：setTimeout,setInverval

- 网络请求：ajax请求，动态`<img>`加载

- 事件绑定

特点：都需要等待

### 异步

什么是异步（对比同步）

异步无阻塞执行

```javascript
console.log(100)
setTimeout(function(){
  console.log(200)
},1000)
console.log(300)
//100-300-200
```

对比同步

同步阻塞执行

```javascript
console.log(100)
alert(200)
console.log(300)
//100-200-300
```

*js是基于异步的语言

何时需要异步

- 在可能发生等待的情况

- 等待过程中不能想alert一样阻塞程序运行

- 因此，所有的“等待的情况”都需要异步


前端使用异步的场景

- 定时任务：setTimeout,setInverval

- 网络请求：ajax请求，动态`<img>`加载

- 事件绑定

ajax请求代码示例

```javascript
console.log('start')
$.get('./data1.json',function(data1){
  console.log(data1)
})
console.log('end')
//start-end-data1
```

`<img>`加载示例

```javascript
console.log('start')
var img = document.createElement('img')
img.onload = function(){
  console.log('loaded')
}
img.src = '/xxx.png'
console.log('end')
//start-end-loaded
```

事件绑定示例

```javascript
console.log('start')
document.getElementById('btn1').addEventListener('click',function(){
  alert('clicked')
})
console.log('end')
//start-end-clicked
```

### 单线程

```javascript
console.log(100)
setTimeout(function(){
  console.log(200)
})
console.log(300)
//100-300-200
```

过程：

- 执行第一行，打印100

- 执行setTimeout后，传入setTimeout的函数会被暂存起来，不会立即执行（单线程的特点，不能同时干两件事）

- 执行最后一行，打印300

- 待所有程序执行完，处于空闲状态时，会立马看有没有暂存起来的要执行的程序

- 发现暂存起来的setTimeout中的函数无序等待时间，就立即过来执行

# 其他知识点

- 获取 2017-06-10 格式的日期

```javascript
function formatDate(dt){
  if(!dt){
    dt = new Date()
  }
  var year = dt.getFullYear()
  var month = dt.getMonth() + 1
  var date = dt.getDate()
  if(month<10){
    //强制类型转换
    month = '0' +month
  }
  if(date<10){
    //强制类型转换
    date = '0' +date
  }
  //强制类型转换
  return year + '-' + month + '-' + date
}
var dt = new Date()
var formatDate = formatDate(dt)
console.log(formatDate)
```

- 获取随机数，要求是长度一致的字符串格式

```javascript
var random = Math.random()
var random = random + '0000000000'//后面加上10个0
var random = random.slice(0,10)
console.log(random)
```

- 写一个能遍历对象和数组的通用的forEach函数

```javascript
function forEach(obj,fn){
  var key 
  if(obj instanceof Array){
    //准确判断是不是数组
    obj.forEach(function(item,index){
      fn(index,item)
    })
  }else{
    //不是数组就是对象
    for (key in obj){
      fn(key,obj[key])
    }
  }
}


var arr = [1,2,3]
//注意，这里的参数顺序换了，为了和对象的遍历格式一致
forEach(arr,function(index,item){
  console.log(index,item)
})

var obj = { x:100,y:200,z:300}
forEach(obj,function(key,value){
  console.log(key,value)
})
```

日期、Math、数组API、对象API

日期

```
Date.now()//获取当前时间毫秒数
var dt = new Date()
dt.getTime()//获取毫秒数
dt.getMonth()//年
dt.getDate()//月（0-11）
dt.getHours()//小时（0-23）
dt.getMinutes()//分钟（0-59）
dt.getSeconds()//秒（0-59）
```

Math

- 获取随机数Math.random()

数组API

- forEach 遍历所有元素

- every 判断所有元素是否都符合条件

- some 判断是否有至少一个元素符合条件

- sort 排序

- map 对元素重新组装，生成新数组

- filter 过滤符合条件的元素

forEach

```javascript
var arr = [1,2,3]
arr.forEach(function(item,index){
  //遍历数组的所有元素
  console.log(index,item)
})
```

every

```javascript
var arr = [1,2,3]
var result = arr.every(function(item,index){
  //用来判断所有的数组元素，都满足一个条件
  if(item<4){
    return true
  }
})
console.log(result)//true
```

some

```javascript
var arr = [1,2,3]
var result = arr.some(function(item,index){
  //用来判断所有的数组元素，只要有一个满足条件即可
  if(item<2){
    return true
  }
})
console.log(result)//true
```

sort

```javascript
var arr = [1,4,7,4,9,6]
var arr2 = arr.sort(function(a,b){
  //从小到大排序
  return a-b

  //从大到小排序
  //return b-a
})
console.log(arr2)
```

map

```javascript
var arr = [1,2,3,4]
var arr2 = arr.map(function(item,index){
  //将元素重新组装，并返回
  return '<b>' + item + '</b>'
})
console.log(arr2)
```

filter

```javascript
var arr = [1,2,3,4]
var arr2 = arr.filter(function(item,index){
  //通过某一个条件过滤数组
  if(item>=2){
    return true
  }
})
console.log(arr2)
```

对象API

```javascript
var obj = {
  x:100,
  y:200,
  z:300,
}
var key 
for (key in obj){
  //注意这里的hasOwnProperty,再讲原型链时候讲过了
  if(obj.hasOwnProperty(key)){
    console.log(key,obj[key])
  }
}
```

## JS-Web-API

**回顾JS基础知识**

- 变量类型和计算

- 原型和原型链

- 闭包和作用域

- 异步和单线程

- 其他（如日期、Math、各种常用API）

- 特点：表面看来并不能用于工作中开发代码

- 内置函数：Object、Array、Boolean、String

- 内置对象：Math、JSON

**JS-Web-API**

JS（浏览器执行的JS）包含两部分：

JS基础知识：ECMA262标准

JS-Web-API：W3C标准

W3C标准中关于JS的规定有：

- DOM操作

- BOM操作

- 事件绑定

- ajax请求（包括HTTP协议）

- 存储

页面弹框是window.alert(123),浏览器需要做：

- 定义一个window全局变量，对象类型

- 给它定义一个alert属性，属性值是一个函数

获取元素document.getElementById(id)，浏览器需要做：

- 定义一个document全局变量，对象类型

- 给它定义一个getElementById的属性，属性值是一个函数

W3C标准只定义用于浏览器中JS操作页面的API和全局变量

JS内置的全局函数和对象有哪些？

window、document、navigator.userAgent

## DOM

DOM是哪种基本的数据结构？

- 树

DOM操作的常用API有哪些？

- 获取DOM节点，以及节点的property和Attribute

- 获取父节点，获取子节点

- 新增节点，删除节点

DOM节点的Attribute和property有何区别？

- property只是一个JS对象的属性的修改

- Attribute是对html标签属性的修改

### DOM本质

DOM可以理解为：

浏览器把拿到的html代码，结构化一个浏览器能识别并且js可操作的一个模型而已

### DOM节点操作

- 获取DOM节点

```javascript
var div1=document.getElementById('div1')//元素
var divList=document.getElementsByTagName('div')//集合
console.log(divList.length)
console.log(divList[0])

var containerList=document.getElementsByClassName('.container')//集合
var pList=document.querySelectorAll('p')//集合
```

- prototype

```javascript
var pList=document.querySelectorAll('p')//集合
var p=pList[0]
console.log(p.style.width)//获取样式
p.style.width='100px'//修改样式
console.log(p.className)//获取class
p.className='p1'//修改class

//获取nodeName和nodeType
console.log(p.nodeName)
console.log(p.nodeType)
```

- Attribute

```javascript
var pList=document.querySelectorAll('p')
var p=pLis[0]
p.getAttribute('data-name')
p.setAttribute('data-name','dongrui23')
p.getAttribute('style')
p.setAttribute('style','font-size:30px')
```

### DOM结构操作

- 新增节点

```javascript
var div1=document.getElementById('div1')
//添加新节点
var p1=document.createElement('p')
p1.innerHTML='this is p1'
div1.appendChild(p1)//添加新创建的元素
//移动已有节点
var p2=document.getElementById('p2')
div1.appenChild(p2)
```

- 获取父元素和获取子元素

```javascript
var div1=document.getElementById('div1')
var parent=div1.parentElement

var child=div1.childNodes
div1=removeChild(child[0])
```

- 删除节点

```javascript
var div1=document.getElementById('div1')
var child=div1.childNodes
div1=removeChild(child[0])
```

## BOM

如何检测浏览器的类型

```javascript
var ua = navigator.userAgent
var isChrome=ua.indexOf('Chrome')
console.log(isChrome)
```

拆解url的各部分

```javascript
//location
console.log(location.href)
console.log(location.protocol)
console.log(location.pathname)
console.log(location.search)
console.log(location.hash)
```

### BOM操作

navigator&screen

```javascript
//navigator
var ua = navigator.userAgent
var isChrome=ua.indexOf('Chrome')
console.log(isChrome)

//screen
console.log(screen.width)
console.log(screen.height)
```

location&history

```javascript
//location
console.log(location.href)
console.log(location.protocol)//'http:' 'https:'
console.log(location.pathname)// '/learn/199'
console.log(location.search)
console.log(location.hash)

//history
history.back()
history.forward()
```

## 事件

编写一个通用的事件监听函数

描述事件冒泡流程

- DOM树形结构

- 事件冒泡

- 阻止冒泡

- 冒泡的应用

对于一个无限下拉加载图片的页面，如何给每个图片绑定事件

- 使用代理

- 知道代理的两个优点

通用事件绑定

```javascript
var btn = document.getElementById('btn1')
btn.addEventListener('click',function(event){
  console.log('clicked)
})

function bindEvent(elem,type,fn){
  elem.addEventListener(type,fn)
}
var a = document.getElementById('link1)
bindEvent(a,'click',function(e){
  e.preventDefault()//阻止默认行为
  alert('clicked')
})
```

关于IE低版本的兼容性

- IE低版本使用attachEvent绑定事件，和W3C标准不一样

- IE低版本使用量以非常少。很多网络都早已不支持

- 建议对IE低版本的兼容性：了解即可，无需深究

- 如果遇到对IE低版本要求苛刻的面试，果断放弃

事件冒泡

```html
<body>
  <div id='div1'>
    <p id='p1'>激活</p>
    <p id='p2'>取消</p>
    <p id='p3'>取消</p>
    <p id='p4'>取消</p>
  </div>
  <div id='div2'>
    <p id='p5'>取消</p>
    <p id='p6'>取消</p>
  </div>
</body>
```

```javascript
var p1 = document.getElementById('p1')
var body = document.body
bindEvent(p1,'click',function(e){
  e.stopPropatation()
  alert('激活')
})
bindEvent(body,'click',function(e){
  alert('取消')
})
```

代理

```html
<div id='div1'>
  <a href="#">a1</a>
  <a href="#">a2</a>
  <a href="#">a3</a>
  <a href="#">a4</a>
  <!-- 会随时新增更多a标签 -->
</div>
```

```javascript
var div1 = document.getElementById('div1')
div1.addEventListener('click',function(e){
  var target = e.target
  if(target.nodeName === 'A'){
    alert(target.innerHTML)
  }
})
```

完善通用绑定事件的函数

```javascript
function bindEvent(elem,type,selector,fn){
  if(fn == null){
    fn = selector
    selector = null
  }
  elem.addEventListener(type,function(e){
    var target
    if(selector){
      target = e.target
      if(target.matches(selector)){
        fn.call(target,e)
      }
    }else{
      fn(e)
    }
  })
}
```

```javascript
//使用代理
var div1 = document.getElementById('div1')
bindEvent(div1,'click','a',function(e){
  console.log(this.innerHTML)
})

//不使用代理
var a = document.getElementById('a1')
bindEvent(div1,'click',function(e){
  console.log(a.innerHTML)
})
```

代理的好处

- 代码简洁

- 减少浏览器内存占用

## Ajax

手写编写一个ajax，不依赖第三方库

跨域的几种实现方式

- JSONP

- 服务器端设置http header

### Ajax-XMLHttpRequst

```javascript
var xhr = new XMLHttpRequest()
xhr.open('GET','/api',false)
xhr.onreadystatechange = function(){
  //这里的函数异步执行，可参考之前JS基础中的异步模块
  if(xhr.readyState == 4){
    if(xhr.status == 200){
      alert(xhr.responseText)
    }
  }
}
xhr.send(null)
```

IE兼容性问题

IE低版本使用ActiveXObject，和W3C标准不一样，同上

状态码说明

```javascript
xhr.onreadystatechange = function(){
  if(xhr.readyState == 4){
    if(xhr.status == 200){
      alert(xhr.responseText)
    }
  }
}
```

readyState

- 0 - (未初始化)还没有调用send()方法

- 1 - (载入)已调用send()方法，正在发送请求

- 2 - (载入完成)send()方法执行完成，已经接收到全部响应内容

- 3 - (交互)正在解析响应内容

- 4 - (完成)响应内容解析完成，可以在客户端调用了

status

- 2xx - 表示成功处理请求。如200

- 3xx - 需要重定向，浏览器直接跳转 

- 4xx - 客户端请求错误，如404

- 5xx - 服务器端错误

### 跨域

什么是跨域

- 浏览器有同源策略，不允许ajax访问其他接口

- 跨域条件：协议、域名、端口，有一个不同就算跨域

可以跨域的三个标签

- 但是有三个标签允许跨域加载资源

- `<img src=xxx>`

- `<link href=xxx>`

- `<script src=xxx>`

三个标签的场景

- `<img>`用于打点统计，统计网站可能是其他域

- `<link>``<script>`可以使用CDN，CDN的也是其他域

- `<script>`可以用于JSONP

跨域注意事项

- 所有的跨域请求都必须经过信息提供允许

- 如果未经允许即可获取，那是浏览器同源策略出现漏洞

JSONP实现原理

```javascript
<script>
window.callback = function(data){
  //这是我们跨域得到的信息
  console.log(data)
}
</script>
<script src='url'></script>
//以上将返回 callback({x:100,y:200})
```

服务器端设置http header

- 另外一个解决跨域的简洁方法，需要服务器端来做

- 是解决跨域问题一个趋势

### 储存

请描述一下cookie，sessionStorage和localStorage的区别？

- 容量

- 是否会携带到ajax

- API易用性

cookie

- 本身用于客户端和服务器端通信

- 但是它有本地存储的功能，于是就被'借用'

- 使用document.cookie = ...获取和修改即可

cookie用于存储的缺点

- 存储量太小，只有4kb

- 所有http请求都带着，会影响获取资源的效率

- API简单，需要封装才能用document.cookie = ...

sessionStorage和localStorage

- HTML5专门为存储而设计，最大容量5M

- API简单易用:

- localStorage.setItem(key,value);localStorage.getItem(key);

## 开发环境

面试官想通过开发环境了解面试者的经验(聊天为主)

**关于开发环境**

- IDE(写代码的效率) > vscode/webstom/sublime/atom > 常用插件!!!

- git(代码版本管理，多人协作开发 -> 大型项目)

- JS模块化

- 打包工具

- 上线回滚的流程

## git

代码版本管理，多人协作开发

**git - 常用命令**

常用Git命令

## 模块化

**不使用模块化**

![](https://github.com/dongrui23/attention/blob/master/picture/web/%E4%B8%8D%E4%BD%BF%E7%94%A8%E6%A8%A1%E5%9D%97%E5%8C%96.png)

- util.js getFormatDate函数

- a-util.js aGetFormatDate函数  使用getFormataDate

- a.js aGetFormatDate

```
//util.js
function getFormatDate(data,type){}
```

引用：

```
<script src='util.js'></script>
<script src='a-util.js'></script>
<script src='a.js'></script>

<!-- 1.这些代码中的函数必须是全局变量，才能暴露给适用方。全局变量污染 -->
<!-- 2.依赖问题，互相依赖 -->
```

**使用模块化**

![](https://github.com/dongrui23/attention/blob/master/picture/web/%E4%BD%BF%E7%94%A8%E6%A8%A1%E5%9D%97%E5%8C%96.png)

```
//util.js
function FormatDate(){}
//a-util.js
var getFormatDate=require('util.js)
<!-- 直接`<script src='a.js'></script>`,其他的根据依赖关系自动引用 -->
<!-- 那两个函数，没必要做成全局变量，不会带来污染和覆盖 -->
```

### 模块化 - AMD

工具：require.js

![](https://github.com/dongrui23/attention/blob/master/picture/web/require.js.png)

引入：

`<script src='/require.min.js' data-main='./main.js'></script>`

全局define函数

全局require函数

依赖JS会自动、异步加载

### 模块化 - CommonJS

nodejs模块化规范，现在被大量用于前端，原因:

- 前端开发依赖的插件和库,都可以从npm中获取

- 构建工具的高度自动化，使得使用npm的成本非常低

- CommonJS不会异步加载JS，而是同步一次性加载出来

![](https://github.com/dongrui23/attention/blob/master/picture/web/common.png)

**AMD与CommonJS的使用场景**

- 需要异步加载JS，使用AMD

- 使用了npm之后建议使用CommonJS

## 构建工具

**构建工具 - 安装nodejs**

**构建工具 - 安装webpack**

**构建工具 - 配置webpack**

webpack.config.js

```
var path = require('path')
var webpack = require('webpack)

module.exports = {
  context:path.resolve(_dirname,'/src'),
  entry: {
    app:'./app.js'
  },
  output:{
    path:path.resolve(_dirname,'./dist'),
    filename:'bundle.js'
  }
}
```

**构建工具 - 使用jquery**

```
var $ =require('jquery')//首先npm安装jquery

var $root=$('#root')
$root.html('<p>jquery</p>')
```

**构建工具 - 压缩JS**

webpack.config.js

```
module exports={
  plugins:[
    new webpack.optimize.UglifyJsPlugin()
  ]
}
```

## 上线回滚

### 上线回滚 - 上线回滚流程

**上线流程要点**

- 将测试完成的代码提交到git版本库的master分支

- 将当前服务器的代码全部打包并记录版本号，备注

- 将master分支的代码提交覆盖到线上服务器，生成新的版本号

**回滚流程要点**

- 将当前服务器的代码打包并记录版本号，备份

- 将备份的上一个版本号解压，覆盖到线上服务器，并生成新的版本号

### 上线回滚 - linux基础命令

```
登陆
目录操作
mkdir a创建a文件
ls看名字
ll 看a
cd a进入a文件
pwd目录路径
cd ..返回上一级目录
rm -rf -a删除文件夹
vi a.js 创建a.js，退出:wq
cp a.js a1.js拷贝a到a1去
mkdir src
mv a1.js src/a1.js移动a1到src目录下
rm a.js删除a.js文件
vim a.js创建a.js,点键盘'i'输入，点'esc'就无法输入;保存-esc:w+回车，退出-:q
vim a.js看内容
cat a.js直接看a.js全部内容
head a.js看前一节部分
tail a.js看尾部一部分
head  -n 2 a.js看前两行
tail -n 2 a.js看后两行
grep '2yy' a.js搜索关键字那一行
```

## 页面加载

- 从输入url到得到html的详细过程

ps：2）加载一个资源的过程

- window.onload和DOMContentLoaded的区别

![](https://github.com/dongrui23/attention/blob/master/picture/web/window.onload%E5%92%8CDOMContentLoaded%E7%9A%84%E5%8C%BA%E5%88%AB.png)

-- 页面的全部资源加载完成才会执行，包括图片、视频等=onload

-- DOM渲染完即可执行，此时图片、视频还没有加载完=DOMContentLoaded

### 页面加载 - 渲染过程

1）加载资源的形式

- 输入url(或跳转页面)加载html

- 加载html中的静态资源(img/css/.js)

2）加载一个资源的过程

- 浏览器根据DNS服务器得到域名的IP地址

- 向这个IP的机器发送http请求

- 服务器收到、处理并返回http请求

- 浏览器得到返回内容

3）浏览器渲染页面的过程

- 根据HTML结构生成DOM Tree

- 根据CSS生成CSSOM

- 将DOM和CSSOM整合形成RenderTree

- 浏览器根据RenderTree开始渲染和展示

- 遇到`<script>`时，会执行并阻塞渲染//js会改变DOM树

### 性能优化 - 优化策略

**原则**

- 多使用内存、缓存或者其他方法

- 减少CPU计算、减少网络

1）加载资源优化

- 静态资源的压缩合并

- 静态资源缓存

- 使用CDN让资源加载更快

- 使用SSR后端渲染，数据直接输出到HTML中

2）渲染优化

- CSS放前面，JS放后面

- 懒加载(图片懒加载、下拉加载更多)

- 减少DOM查询，对DOM查询做缓存

- 减少DOM操作，多个操作尽量合并在一起执行

- 事件节流

- 尽早进行操作(如DOMContentLoaded)

示例：

资源合并，a、b、c(.js) => abc (.js)

缓存，通过连接名称控制缓存

CDN--cdn.bootcss.com

使用ssr后端渲染--vue、react

懒加载：

![](https://github.com/dongrui23/attention/blob/master/picture/web/%E6%87%92%E5%8A%A0%E8%BD%BD.png)

缓存DOM查询

![](https://github.com/dongrui23/attention/blob/master/picture/web/DOM%E7%BC%93%E5%AD%98.png)

合并DOM插入

![](https://github.com/dongrui23/attention/blob/master/picture/web/DOM%E6%8F%92%E5%85%A5%E7%BC%93%E5%AD%98.png)

事件节流

![](https://github.com/dongrui23/attention/blob/master/picture/web/%E4%BA%8B%E4%BB%B6%E8%8A%82%E6%B5%81.png)

尽早操作

![](https://github.com/dongrui23/attention/blob/master/picture/web/window.onload%E5%92%8CDOMContentLoaded%E7%9A%84%E5%8C%BA%E5%88%AB.png)


**安全性 - XSS**

- XSS跨站请求攻击

脚本攻击代码

解决：前端替换关键字，如<替换为&lt；（配合后端），后端替换

**安全性 - XSRF**

- XSRF跨站请求伪造

钓鱼网站，伪造

解决：输入指纹、密码、短信验证码

**技巧**

简历，项目经历--解决方案，博客，定期维护更新博客，维护开源项目，能力经历的真实性，建议不要太多加班，不要挑战面试官--给面试官惊喜-说出你知道的--缺点：你最近学什么？