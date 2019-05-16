
### 兼容性

Vue 不支持 IE8 及以下版本，因为 Vue 使用了 IE8 无法模拟的ECMAScript 5 特性。但它支持所有兼容**ECMAScript 5 的浏览器**。

**原生js操作dom**

```javascript
<body>
    <div id='app'></div>
    <script>
        var dom = document.getElementById('app');
        dom.innerHTML = 'hello world'
    </script>
</body>
```

**vue操作dom**

```javascript
<head>
    <script src='vue.js'></script> //引入vue.js
</head>
<body>
    <div id='app'>{{content}}</div>//插值表达式
    <div>{{content}}</div>
    <script>
        var vm = new Vue({
            el: '#app',
            data: {
                content: 'Hello World'
            }
        })
    </script>
</body>
```

页面输出：

```
Hello World
{{content}}
```

创建一个vue实例，el配置项是vue实例管理的区域,vue实例接管了`id='app'`下的内容。

**延时器**

```javascript
// js
setTimeout(function() {
    dom.innerHTML = '3秒后我改变了！'
},3000)

// vue
setTimeout(function() {
    app.$data.content = '3秒后我改变了！'
},3000)

// es6
setTimeout(() => {
    代码；
},3000)
```

### vue指令

**v-for遍历，循环数据**

用法：

```html
元素Element
<div v-for="item in list" :key="item.id">
  {{item.text}}
</div>

数组Array
<div v-for="(item, index) in list" :key="item.id"></div>

对象Object
<div v-for="(value, key) in object" :key="key"></div>
<div v-for="(value, key, index) in object" :key="key"></div>

key是特殊属性
```

**v-on绑定事件监听器**

用法：

```javascript
<button v-on:click="Click">commit</button>

Click方法定义在methods上
methods: {
    Click: function() {
        alert('click')
    }
}
```

页面上鼠标点击`commit`会执行Click方法，弹出click。

ps：`v-on`可以缩写为`@`

**v-model数据双向绑定**

用法：

```javascript
<input v-model='value' />

data:{
    value: ''
}
```

**v-bind动态绑定**

用法：

```javascript
<!-- 绑定一个属性 -->
<img v-bind:src="imageSrc">

<!-- 动态特性名 (2.6.0+) -->
<button v-bind:[key]="value"></button>
```

子组件Props-从父组件接收数据

ps：`v-bind`可以缩写为`:`

**v-text更新元素的`textContent`**

用法：

```javascript
<span v-text="msg"></span>
<!-- 和下面的差值表达式一样 -->
<span>{{msg}}</span>
```
ps：不会动态渲染，直接显示内容

**v-html更新元素的`innerHTML`**

```html
<div v-html="html"></div>
```
ps:可以动态渲染任意HTML,容易导致XSS攻击,仅可信内容上使用

### MVVM模式

**理解MVP模式**

Model-View-Presenter

Controller/Presenter负责逻辑的处理，Model提供数据，View负责显示，如下图：

![](https://user-gold-cdn.xitu.io/2018/6/27/16441ddf9fc513ef?w=513&h=389&f=png&s=2042)

举例：

```javascript
//jQuery

//v层视图
<body>
<input id='input'/>
<button id="btn">commit</button>
<ul id='list'></ul>
</body>

//p层控制器
<script>
    function Page() {

    }

    $.extend(Page.prototype, {
        init: function () {
            this.binfEvents()
        },
        bindEvents: function () {
            var btn = $('#btn');
            btn.on('click', $.proxy(this.handleBtnClick, this))
        },
        handleBtnClick: function () {
            var inputElem = $("#input");
            var inputValue = inputElem.val();
            var ulElem = $("#list");
            ulElem.append('<li>' + inputValue + '</li>');
            inputElem.val('');
        }
    })

    var Page = new Page();
    page.init();
</script>
```

jQuery，面向dom开发

v层发出一个事件交给p层，p层通过ajax请求调用m层获取数据，p层通过dom操作改变v层，p层是中转站，是核心。

**MVVM模式**

Model-View-ViewModel，如下图：

![](https://images.cnblogs.com/cnblogs_com/Mainz/201105/201105031754285061.png)

Vue，面向数据开发

ViewModel(虚拟dom)是Vue内置的一层，对m层进行操作，会通过vm层映射到v层，从而发生改变。

### 组件化

**全局组件**

```javascript
<body>
    <imag-src v-bind:src='imageSrc'></imag-src>  //向子组件传入一个绑定值
</body>

<script>
    Vue.component("ImageSrc", {
        props: ['src'],  //接收src
        template: '<div>{{this.src}}</div>'
    })
</script>
```

**局部组件**

```javascript
<body>
    <div id='app'>
        <image-src v-bind:src='imageSrc'></image-src>  //向子组件传入一个绑定值
    </div>
    <script>
        var ImageSrc = {
            props: ['src'],  //接收src
            template: '<div>{{this.src}}</div>'
        }

        var vm = new Vue({
            el: '#app',
            components: {
            ImageSrc: ImageSrc  //注册组件
            },
            data: {
                ImagSrc: '?'
            }
        })
    </script>
</body>
```

**组件间传值**

子组件向父组件传值

```javascript
<body>
    <div id='app'>
        <imag-src
            v-bind:src='item'
            v-bind:index='index'
            v-for='(item, index) in list'
            @change='changeElem'
        ></imag-src>  //向子组件传入一个绑定值,监听change事件
    </div>
</body>

<script>
    Vue.component('ImagSrc',{
        props: {
            src: String,
            index: String
        },
        template: '<div @click="handClick">{{this.src}}</div>',
        methods: {
            handClick: function () {
                this.$emit('change',this.index);  //向外触发事件
            }
        }
    })

    var vm = new Vue({
        el: '#app',
        data:{},
        methods: {
            changeElem: function (index) {
                this.list.splice(index, 1)
            }
        }
    })
</script>
```





