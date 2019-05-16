
### 使用组件的细节点

```javascript
// is
<div id='app'>
  <table>
    <tbody>
      <tr is='row'></tr>//符合H5代码规范
    </tbody>
  </table>
</div>

<script>
  Vue.component('row',{
    template: '<td><td>?????</td></tr>'
  })

  var vm = new Vue({
    el: '#app'
  })
</script>
```

```javascript
//data是一个函数
Vue.component('row',{
    data: () {
      return {
        content:'aaa'
      }
    }
    template: '<td><td>?????</td></tr>'
  })
```

```html
<div
 ref='aaaname'
 @click='dick'
>ko</div>

methods: {
  dick: function(){
    console.log(this.$refs.aaaname.innerHTML)//对应div这个dom节点
  }
}
```

`vm.$emit( eventName, […args] )`

触发当前实例上的事件。附加参数都会传给监听器回调。

```javascript
<counter
 ref='ana'
 @chang='handleChange'
></counter>
<div>{{total}}</div>

Vue.component('counter',{
  template:'<div @click='dick'></div>',
  data: () {
    return{
      number: 0
    }
  },
  methods:{
    dick: () {
      this.number++
      this.$emit('change')
    }
  }
})

methods: {
  handleChange: function(){
    this.total=this.$refs.ana.number
  }
}
```

### 父子组件间的数据传值

**Prop 验证**

```javascript
props: {
  title: String,
  props: {
      type: Number,
      default: 100
    },
  likes: Number,
  isPublished: Boolean,
  commentIds: Array,
  author: Object,
  callback: Function,
  contactsPromise: Promise // or any other constructor
}
```

给 `prop` 传入一个静态的值

`<blog-post title="My journey with Vue"></blog-post>`

`prop` 可以通过 `v-bind` 动态赋值

```html
<!-- 动态赋予一个变量的值 -->
<!-- 这是一个 JavaScript 表达式而不是一个字符串。-->
<blog-post v-bind:title="post.title"></blog-post>
```

**单向数据流**

所有的 `prop` 都使得其父子 `prop` 之间形成了一个**单向下行绑定**：父级 `prop` 的更新会向下流动到子组件中，但是反过来则不行。

定义一个本地的 `data` 属性并将这个 `prop` 用作其初始值：

```javascript
props: ['initialCounter'],
data: function () {
  return {
    counter: this.initialCounter
  }
}
```

### 组件参数校验与非props特性

Prop 验证

非 Prop 的特性

一个非 `prop` 特性是指传向一个组件，但是该组件并没有相应 `prop` 定义的特性。

### 给组件绑定原生事件

使用 `v-on` 的 `.native`(监听组件根元素的原生事件) 修饰符：

```html
// 不用$emit向外触发事件
<base-input v-on:focus.native="onFocus"></base-input>
```

### 非父子组件间的传值

![](https://cn.vuejs.org/images/components.png)

bus/总线、发布订阅模式、观察者模式

```javascript
<script>
  Vue.prototype.bus = new Vue()
  Vue.component('child',{
    props: {
      content:String
    },
    data () {
      return{...}
    },
    template:'@...',
    methods: {
      * : (){
        this.bus.$emit('change', this.scontent)
      }
    },
    mounted : () {
      var _this = this
      this.bus.$on('change',function(msg){
        _this.scontent = msg
      })
    }
  })
</script>
```

`m.$on( event, callback )`
参数：

{string | Array<string>} event (数组只在 2.2.0+ 中支持)
{Function} callback
用法：

监听当前实例上的自定义事件。事件可以由`vm.$emit`触发。回调函数会接收所有传入事件触发函数的额外参数。

示例：

```javascript
vm.$on('test', function (msg) {
  console.log(msg)
})
vm.$emit('test', 'hi')
// msg => "hi"
```

**Vuex**

![](https://vuex.vuejs.org/vuex.png)

### 在Vue中使用插槽

`v-slot` 代替 slot、slot-scope

```
// 元素1=元素2
<child>
  <p>rrrrr</p>// 元素1
</child>

template:`<div>
            <slot></slot>// 元素2
          </div>`
```

**具名插槽**

```html
<div class="container">
  <header>
    <!-- 我们希望把页头放这里 -->
  </header>
  <main>
    <!-- 我们希望把主要内容放这里 -->
  </main>
  <footer>
    <!-- 我们希望把页脚放这里 -->
  </footer>
</div>
```

对于这样的情况，`<slot>` 元素有一个特殊的特性：**name**。这个特性可以用来定义额外的插槽：

```html
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>
```

### 作用域插槽

```html
// template：<current-user>
<span>
  <slot :user="user">
    {{ user.lastName }}
  </slot>
</span>
```

绑定在 `<slot>` 元素上的特性被称为插槽 prop。

现在在父级作用域中，我们可以给 `v-slot` 带一个值来定义我们提供的插槽 prop 的名字：

```html
//  v-slot:default="slotProps" => slot='default' slot-scope="slotProps"
<current-user>
  <template v-slot:default="slotProps">
    {{ slotProps.user.firstName }}
  </template>
</current-user>
```

### 动态组件与v-once指令

**动态组件**

```javascript
<div id='app'>
  <component :is=type></component>
  <button @click='lolo'>
<div>

<script>
  Vue.component('child-one',{
    template:'<div>child-one</div>'
  })
  Vue.component('child-two',{
    template:'<div>child-one</div>'
  })

  var vm = new Vue({
    el:'#app',
    data:{
      type:'child-one'
    },
    methods:{
      lolo:function(){}
    }
  })
</script>
```

**v-once**

不需要表达式,直接加就行，与 `v-if` 结合使用

只渲染元素和组件一次。随后的重新渲染，元素/组件及其所有的子节点将被视为**静态内容**并跳过。这可以用于优化更新性能。


