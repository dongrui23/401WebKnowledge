
## ES6开发环境搭建

创建文件dist(保存转化的es5代码)，src(es6代码)，index.html(引入文件为dist下的js文件)

在vsc终端上运行(ctrl+~)

`npm init -y`  生成package.json文件，-y是默认设置

`npm install -g babel-cli`  全局安装babel

安装两个包：babel-preset-es2015 & babel-cli

`npm install --save-dev babel-preset-es2015 babel-cli`

在根目录上创建文件.babelrc

```
{
  "presets":[
    "es2015"
  ],
  "plugins":[]
}
```

`babel src/index.js -o dist/index.js`  转换为es5，-o为输出的意思

转换完成

简化命令package.json里面的代码

```
"scripts": {
  "test": "echo \"Error: no test specified\" && exit 1"

改为

"scripts": {
  "build": "babel src/index.js -o dist/index.js"
```

## 新的声明方式

**var 全局声明**

```javascript
var a = 1;
console.log(a);//1

var a = 1;
window.onload = function () {
   console.log(a);//1
 }

var a = 1;
{
  var a = 'hello'
}
console.log(a)//hello 会污染到外面的声明

for (var i=0;i<10;i++) {
  console.log('里面'+i);//0到9
}
console.log('外面'+i);//10,被污染了
```

**let 局部声明**

```javascript
var a = 1;
{
  let a = 'hello';//不会污染到外面
}
console.log(a);//1

for (let i=0;i<10;i++) {
  console.log('里面'+i);//0到9
}
console.log('外面'+i);//未定义undefined
```

**const 常量**

```javascript
const a = '007';
var a = '009';
console.log(a);//报错
```

## 变量的解构赋值

**数组的解构赋值**

```javascript
let[a,b,c]=[0,1,2];//顺序一一对应
console.log(a);
console.log(b);
console.log(c);

let[foo='true']=[];
console.log(foo);//true,默认值可用

let[a,b='haha']=[0,undefined];//0haha,如为null，则0null
console.log(a+b);
```

**对象的解构赋值**

```javascript
let {foo,bar} = { foo:'WWW',bar:'OOO'};//key值对应
console.log(foo+bar)

let foo;
({foo}={foo:'999'});//要加括号,语法
console.log(foo)
```

**字符串的解构赋值**

```javascript
const [a,b,c]='555';//应用于权限有关
console.log(a);
console.log(b);
console.log(c);
```