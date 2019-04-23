
## 变量类型和计算
**es6 typeof symbol**


## 原型和原型链
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
对于一个无限下拉加载图片的页面，如何给每个图片绑定事件

通用事件绑定

```
 
```

事件冒泡
代理

## Ajax
### Ajax-XMLHttpRequst
### 跨域
### 储存


## git
### git - 常用命令



## 模块化
### 模块化 - AMD
### 模块化 - CommonJS



## 构建工具
### 构建工具 - 安装nodejs
### 构建工具 - 安装webpack
### 构建工具 - 配置webpack
### 构建工具 - 使用jquery
### 构建工具 - 压缩JS



## 上线回滚
### 上线回滚 - 上线回滚流程
### 上线回滚 - linux基础命令



## 页面加载
### 页面加载 - 渲染过程
### 性能优化 - 优化策略
### 安全性 - XSS
### 安全性 - XSRF