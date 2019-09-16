
```
根实例
└─ TodoList
   ├─ TodoItem
   │  ├─ DeleteTodoButton
   │  └─ EditTodoButton
   └─ TodoListFooter
      ├─ ClearTodosButton
      └─ TodoListStatistics
```

```html     
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>todolist</title>
    <script src='vue.js'></script>
</head>
<body>
    <div id= "root">
        <div>
            <input type="text" v-model='todoValue' />
            <button @click='handleBtnClick'>提交</button>
        </div>
        <ul>
            <!-- <li v-for="item in list">{{item}}</li> -->
        <todo-item v-bind:content='item'
                   v-bind:index="index"
                   v-for="(item,index) in list"
                   @delete='handleItemDelete'>
        </todo-item>
        </ul>
    </div>

    <script>


        var  TodoItem = {
            props:['content','index'],
            template:'<li @click="handleItemClick">{{content}}</li>',
            methods:{
                handleItemClick: function(){
                    // alert('click')
                    this.$emit('delete',this.index);
                }
            }
        }
        var app = new Vue({
            el:"#root",
            components:{
                TodoItem:TodoItem
            },
            data:{
                list:[], 
                todoValue:''
            },
            methods:{
                handleBtnClick:function(){
                    this.list.push(this.todoValue)
                    // alert(this.inputValue)
                    this.todoValue=''
                },
                handleItemDelete:function(index){
                    // alert('delete')
                    // alert(index)
                    // this.list=[]
                    this.list.splice(index,1)
                }
            }
        })
    </script>
</body>
</html>
```