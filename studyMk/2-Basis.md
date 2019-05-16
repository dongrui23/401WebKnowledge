
### Vue实例

```javascript
<div id='app'>
  <div @click='handClick'>
    {{content}}
  </div>
  <item></item>
</div>

<script>
  Vue.component('item', {
    template: '<div>hello world</div>'
  })
  var vm = new Vue({
    el: '#app',
    data: {
      content: 'hello world'
    },
    methods: {
      handClick: function () {
        alert('666')
      }
    }
  })
</script>
```

### Vue实例生命周期

**生命周期函数就是Vue实例在某一个时间点会自动执行的函数**

生命周期图示:

![](https://cn.vuejs.org/images/lifecycle.png)

```javascript
//生命周期函数就是Vue实例在某一个时间点会自动执行的函数

//Init Events & Lifecycle 初始事件和生命周期

beforeCreate: function () {}

//Init injections & reactivity 初始反应

created: function () {}

//Has 'el' option? Has 'template' option : when vm.$mounted(el) is call

//Has 'template' option? Compile template into render function : Compile el's outerHTML as template

beforeMount: function () {} //即将挂载到页面的一瞬间

//Create vm.$el and replace 'el' with it

mounted: function () {} //页面挂载之后

//Mounted
//when data changes

beforeUpdate: function () {}

//Virtual Dom re-render and patch `Virtual Dom`重新渲染和修补

updated: function () {}

//--->Mounted
//when vm.$destroy() is called

beforeDestroy: function () {}

//Teardown watchers,child components and event listeners 拆解监视器，子组件和事件监听器
//Destroyed

destroyed: function () {}

//其他钩子

activated: function () {} //keep-alive 组件激活时调用

deactivated: function () {} //keep-alive 组件停用时调用

errorCaptured: function () {} //子孙组件的错误时被调用
```

### Vue的模板语法

[Vue指令](https://cn.vuejs.org/v2/api/#%E6%8C%87%E4%BB%A4)

[模板语法](https://cn.vuejs.org/v2/guide/syntax.html)

### 计算属性&方法&侦听器

**计算属性**

```javascript
computed: {
  handleBtnClick: function () {}
}
```

```javascript
<div id="example">
  <p>Original message: "{{ message }}"</p>
  <p>Computed reversed message: "{{ reversedMessage }}"</p>
</div>

var vm = new Vue({
  el: '#example',
  data: {
    message: 'Hello'
  },
  computed: {
    // 计算属性的 getter ,默认
    reversedMessage: function () {
      // `this` 指向 vm 实例
      return this.message.split('').reverse().join('')
    }
  }
})
```

**计算属性缓存&方法**

```javascript
<p>Reversed message: "{{ reversedMessage() }}"</p>

// 在组件中
methods: {
  reversedMessage: function () {
    return this.message.split('').reverse().join('')
  }
}
```

计算属性是基于它们的响应式依赖进行缓存的

**计算属性&侦听属性**

```javascript
// watch侦听
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar',
    fullName: 'Foo Bar'
  },
  watch: {
    firstName: function (val) {
      this.fullName = val + ' ' + this.lastName// val是this.firstName
    },
    lastName: function (val) {
      this.fullName = this.firstName + ' ' + val
    }
  }
})

// computed计算
var vm = new Vue({
  el: '#demo',
  data: {
    firstName: 'Foo',
    lastName: 'Bar'
  },
  computed: {
    fullName: function () {
      return this.firstName + ' ' + this.lastName
    }
  }
})
```

**计算属性的 setter**

设置值`vm.fullName`

```javascript
set: function (newValue) {
      var names = newValue.split(' ')
      this.firstName = names[0]
      this.lastName = names[names.length - 1]
    }
```

### Vue中的样式绑定

**绑定 HTML Class**

```html
// 对象语法
<div
 v-bind:class="{ active: isActive, 'text-danger': hasError }"
></div>

// 数组语法
<div
 v-bind:class="[activeClass, errorClass]"
></div>

// 用在组件上
<my-component
 v-bind:class="{ active: isActive }"
></my-component>
```

**绑定内联样式**

```
// 对象语法
<div
 v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"
></div>

// 数组语法
<div
 v-bind:style="[baseStyles, overridingStyles]"
></div>
```

### Vue中的条件渲染

**v-if**

```html
<h1 v-if="awesome">Vue is awesome!</h1>
<h1 v-else>Oh no 😢</h1>
```

- 在 <template> 元素上使用 `v-if` 条件渲染分组

切换多个元素,需<template>元素当做不可见的包裹元素

```html
<template v-if="ok">
  <h1>Title</h1>
  <p>Paragraph 1</p>
  <p>Paragraph 2</p>
</template>
```

- v-else&v-else-if

v-else 元素必须紧跟在带 v-if 或者 v-else-if 的元素的后面，否则它将不会被识别。

v-else-if 也必须紧跟在带 v-if 或者 v-else-if 的元素之后。

- 用 key 管理可复用的元素

```javascript
// 不会清除用户已经输入的内容
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address">
</template>

// key, `<label>` 元素仍然会被高效地复用，因为它们没有添加 key 属性。
<template v-if="loginType === 'username'">
  <label>Username</label>
  <input placeholder="Enter your username" key="username-input">
</template>
<template v-else>
  <label>Email</label>
  <input placeholder="Enter your email address" key="email-input">
</template>
```

**v-show**

不同的是带有 `v-show` 的元素始终会被渲染并**保留**在 DOM 中。

`v-show` 只是简单地切换元素的 CSS 属性 `display`。

注意，v-show 不支持 <template> 元素，也不支持 v-else。

*v-if vs v-show*

`v-if` 是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被**销毁**和**重建**。

`v-if` 也是惰性的：如果在初始渲染时条件为假，则什么也不做--直到条件第一次变为真时，才会开始渲染条件块。

相比之下，`v-show` 就简单得多--不管初始条件是什么，元素总是会被渲染，并且只是简单地基于 CSS 进行切换。

一般来说，`v-if` 有更高的**切换开销**，而 `v-show` 有更高的**初始渲染开销**。

因此，如果需要非常频繁地切换，则使用 `v-show` 较好；如果在运行时条件很少改变，则使用 `v-if` 较好。

*v-if 与 v-for*

不推荐同时使用 `v-if` 和 `v-for`,当 `v-if` 与 `v-for` 一起使用时，`v-for` 具有比 `v-if` 更高的优先级。

### Vue中的列表渲染

用 `v-for` 把一个**数组**对应为一组元素

```html
// items 是源数据数组
<li v-for="item in items">
    {{ item.message }}
</li>

<ul id="example-2">
  <li v-for="(item, index) in items">
    {{ parentMessage }} - {{ index }} - {{ item.message }}
  </li>
</ul>
```

可以用 `of` 替代 `in` 作为分隔符，因为它是最接近 JavaScript 迭代器的语法.

`<div v-for="item of items"></div>`

**一个对象的 v-for**

```html
<li v-for="value in object">
    {{ value }}//得到object的键值
</li>

<div v-for="(value, key) in object">
  {{ key }}: {{ value }}
</div>

<div v-for="(value, key, index) in object">
  {{ index }}. {{ key }}: {{ value }}
</div>
```

**key**

```html
// 理想的 key 值是每项都有的唯一 id
<div v-for="item in items" :key="item.id">
  <!-- 内容 -->
</div>
```

**一个组件的 v-for**

```html
<my-component
  v-for="(item, index) in items"
  v-bind:item="item"
  v-bind:index="index"
  v-bind:key="item.id"
></my-component>

---props接收
```

### Vue中的set方法

Vue.set( target, key, value )

vm.$set( target, key, value )

```
参数：
{Object | Array} target
{string | number} key
{any} value
```