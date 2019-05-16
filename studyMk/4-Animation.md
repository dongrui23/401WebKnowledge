
> 在 CSS 过渡和动画中自动应用 class

> 可以配合使用第三方 CSS 动画库，如 Animate.css

> 在过渡钩子函数中使用 JavaScript 直接操作 DOM

> 可以配合使用第三方 JavaScript 动画库，如 Velocity.js

> Vue 提供了 transition 的封装组件


### Vue中CSS动画原理

```html
<div id="demo">
  <button v-on:click="show = !show">
    Toggle
  </button>
  <transition name="fade">
    <p v-if="show">hello</p>
  </transition>
</div>
```

如果你使用一个没有名字的 `<transition>`，则 `v-` 是这些类名的默认前缀。

如果你使用了 `<transition name="my-transition">`，那么 `v-enter` 会替换为 `my-transition-enter`。

```javascript
new Vue({
  el: '#demo',
  data: {
    show: true
  }
})
```

```cs
.fade-enter-active, .fade-leave-active {
  transition: opacity .5s;
}
.fade-enter, .fade-leave-to {
  opacity: 0;
}
```

![](https://cn.vuejs.org/images/transition.png)

### 在Vue中使用animate.css库

```html
<link rel="stylesheet" href="animate.css">

<div id="example-2">
  <button @click="show = !show">
    Toggle render
  </button>
  <transition
    name="fade"
    enter-active-class="animated tada"
    leave-active-class="animated bounceOutRight"
  >
    <p v-if="show">hello</p>
  </transition>
</div>
```

### 在Vue中同时使用过渡和动画

**初始渲染的过渡**

可以通过 `appear` 特性设置节点在初始渲染的过渡,刷新页面的时候

```html
<transition
  appear
  appear-class="custom-appear-class"
  appear-to-class="custom-appear-to-class" (2.1.8+)
  appear-active-class="custom-appear-active-class"
>
  <!-- ... -->
</transition>
```

**同时使用过渡和动画**

在一些场景中，你需要给同一个元素同时设置两种过渡动效

比如 `animation` 很快的被触发并完成了，而 `transition` 效果还没结束。

在这种情况中，你就需要使用 `type` 特性并设置 `animation` 或 `transition` 来明确声明你需要 Vue 监听的类型。

```css
type='transition'
enter-active-class="animated tada fade-enter-active"
leave-active-class="animated bounceOutRight fade-leave-active"
```

**过渡持续时间**

`<transition :duration="1000">...</transition>`

ni也可以定制进入和移出的持续时间：

`<transition :duration="{ enter: 500, leave: 800 }">...</transition>`

### Vue中的js动画与Velocity.js的结合

```html
<!--
Velocity 和 jQuery.animate 的工作方式类似，也是用来实现 JavaScript 动画的一个很棒的选择
-->
<div id="example-3">
  <button @click="show = !show">
    Toggle
  </button>
  <transition
    @before-enter="beforeEnter"
    @enter="enter"
    @leave="leave"
    :css="false"
  >
    <p v-if="show">
      Demo
    </p>
  </transition>
</div>
```

```javascript
<script src="velocity.min.js"></script>

new Vue({
  el: '#example-3',
  data: {
    show: false
  },
  methods: {
    beforeEnter: function (el) {
      el.style.opacity = 0
      el.style.transformOrigin = 'left'
    },
    enter: function (el, done) {
      Velocity(el, { opacity: 1, fontSize: '1.4em' }, { duration: 300 })
      Velocity(el, { fontSize: '1em' }, { complete: done })
    },
    leave: function (el, done) {
      Velocity(el, { translateX: '15px', rotateZ: '50deg' }, { duration: 600 })
      Velocity(el, { rotateZ: '100deg' }, { loop: 2 })
      Velocity(el, {
        rotateZ: '45deg',
        translateY: '30px',
        translateX: '30px',
        opacity: 0
      }, { complete: done })
    }
  }
})
```

### Vue中多个元素或组件的过渡

**多个元素的过渡**

```html
<transition>
  <button v-if="isEditing" key="save">
    Save
  </button>
  <button v-else key="edit">
    Edit
  </button>
</transition>


<transition>
  <button v-bind:key="isEditing">
    {{ isEditing ? 'Save' : 'Edit' }}
  </button>
</transition>
```

过渡模式

- in-out：新元素先进行过渡，完成之后当前元素过渡离开。

- out-in：当前元素先进行过渡，完成之后新元素过渡进入。

用 out-in 重写之前的开关按钮过渡：

```html
<transition name="fade" mode="out-in">
  <!-- ... the buttons ... -->
</transition>
```

组件的过渡

我们只需要使用动态组件：

```html
<transition name="component-fade" mode="out-in">
  <component :is="view"></component>
</transition>
```
```javascript
new Vue({
  el: '#transition-components-demo',
  data: {
    view: 'v-a'
  },
  components: {
    'v-a': {
      template: '<div>Component A</div>'
    },
    'v-b': {
      template: '<div>Component B</div>'
    }
  }
})
```

```cs
.component-fade-enter-active, .component-fade-leave-active {
  transition: opacity .3s ease;
}
.component-fade-enter, .component-fade-leave-to
/* .component-fade-leave-active for below version 2.1.8 */ {
  opacity: 0;
}
```

### Vue中的列表过渡

```html
// transition-group可看做transition的多个组合

<div id="list-demo" class="demo">
  <button v-on:click="add">Add</button>
  <button v-on:click="remove">Remove</button>
  <transition-group name="list" tag="p">
    <span v-for="item in items" v-bind:key="item" class="list-item">
      {{ item }}
    </span>
  </transition-group>
</div>
```

```javascript
new Vue({
  el: '#list-demo',
  data: {
    items: [1,2,3,4,5,6,7,8,9],
    nextNum: 10
  },
  methods: {
    randomIndex: function () {
      return Math.floor(Math.random() * this.items.length)
    },
    add: function () {
      this.items.splice(this.randomIndex(), 0, this.nextNum++)
    },
    remove: function () {
      this.items.splice(this.randomIndex(), 1)
    },
  }
})
```

```cs
.list-item {
  display: inline-block;
  margin-right: 10px;
}
.list-enter-active, .list-leave-active {
  transition: all 1s;
}
.list-enter, .list-leave-to
/* .list-leave-active for below version 2.1.8 */ {
  opacity: 0;
  transform: translateY(30px);
}
```

### Vue中的动画封装

```javascript
// 封装在fade这个子组件中
Vue.component('fade',{
  props:['show'],
  template: `<transition>
                <slot v-if='show'></slot>
             <transition>`
})
```



















