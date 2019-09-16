
**第一节初出茅庐**

安装vuex

npm install vuex --save

引用vuex

src/vuex/store.js

```
import Vue from 'vue;
import Vuex from 'vuex;
Vue.use(Vuex);

const state = {
  count:1
}
const mutations = {
  add(state,n){
    state.count+=n;
  },
  reduce(state){
    state.count--;
  }
}

//**第四节getters计算过滤操作**--类似vue里的computed属性
const getters={
  count:function(state){
    return state.count+=100;
  }
}

//**actions异步修改状态**
const actions={
  addAction(context){
    context.commit('add',10),
    setTimeout(()=>{context.commit('reduce')},3000)
  },
  reduceAction({commit}){
    commit('reduce')
  }
}

export default new Vuex.Store({
  state,
  mutations,
  getters,
  actions
})
```

## 模板

src/components/Count.vue

```html
<template>
  <div>
    <h2>{{msg}}</h2>
    //<h3>{{$store.state.count}}</h3>
    <h3>{{count}}</h3>  //显示count
    <p>
      <button @click='$store.commit("add",10)'>+</button>
      <button @click='$store.commit("reduce")'>-</button>
    </p>

//actions方法
    <p>
      <button @click='addAction'>+</button>
      <button @click='reduceAction'>-</button>
    </p>

  </div>
</template>

<script>
import store from '@/vuex/store';
export default{
  data(){
    return{
      msg:'hello vuex'
    }
  },

**第二节state访问状态对象**

  //1
  computed:{
    count(){
      return this.$store.state.count
    }
  },
  store
}
</script>

//2
import { mapState } from 'vuex';
computed:mapState({
  count:state=>state.count
})

//3推荐
import { mapState,mapGetters } from 'vuex';
computed:mapState(['count'])

ES6写法=>
computed:{
  ...mapState(['count']),

  //count(){
    return this.$store.getters.count;
  }

简写：
  ...mapGetters(['count'])

}

```

**第三节Mutations修改状态**

```html
简写
<p>
  <button @click='add'>+</button>
  <button @click='reduce'>-</button>
</p>

import { mapState,mapMutations,mapActions } from 'vuex';
methods:mapMutations(['add','reduce'])

//actions
es6=>
ethods:{
  ...mapMutations(['add','reduce']),
  ...mapActions(['addAction','reduceAction'])
```

## module模块组

```
** 声明模块组： **

在vuex/store.js中声明模块组，我们还是用我们的const常量的方法声明模块组。代码如下：

const moduleA={
    state,mutations,getters,actions
}
声明好后，我们需要修改原来 Vuex.Stroe里的值：

export default new Vuex.Store({
    modules:{a:moduleA}
})
** 在模板中使用 ** 现在我们要在模板中使用count状态，要用插值的形式写入。

<h3>{{$store.state.a.count}}</h3>
如果想用简单的方法引入，还是要在我们的计算属性中rutrun我们的状态。写法如下：

computed:{
    count(){
        return this.$store.state.a.count;
    }
},
```