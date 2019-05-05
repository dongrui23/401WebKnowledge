
###  (一)

渲染引擎是兼容性问题出现的根本原因

h1标签有什么作用？

答案：给文本增加主标题的语义。

`<!doctype html>`是HTML5标准。

HTML中表示长度的单位都是像素。HTML只有一种单位就是像素。

`<meta http-equiv="refresh" content="3;http://www.baidu.com">`

3秒之后，自动跳转到百度页面。

问：网页的head标签里面，表示的是页面的配置，有什么配置？

答：字符集、关键词、页面描述、页面标题。（今后我们还能看见一些其他的配置：IE适配、视口、iPhone小图标等等）

link属性表示默认显示的颜色、alink属性表示鼠标点击但是还没有松开时的颜色、vlink属性表示点击完成之后显示的颜色

```html
<body link='red' alink='blue' vlink='green'>
  <a href="#">我要像梦一样自由</a>
</body>
```

`<p align='center'>大河向东流啊</p>`,用text-align、color不行

- 文本级标签：p、span、a、b、i、u、em。文本级标签里只能放文字、图片、表单元素。（a标签里不能放a和input）

- 容器级标签：div、h系列、li、dt、dd。容器级标签里可以放置任何东西。

`<span>`(**文本级**)和`<div>`(**容器级**)唯一的区别在于：`<span>`是不换行的，而`<div>`是换行的。

div+css,div标签负责布局，负责结构，负责分块。css负责样式。

转义字符
- `&nbsp;`：空格	（non-breaking spacing，不断打空格）
- `&lt;`：小于号（less than）
- `&gt;`：大于号（greater than）

| 特殊字符 | 描述 |字符的代码 |
|:-------------|:-------------|:-----|
||空格符|`&nbsp;`|
|<|小于号|`&lt;`|
|> |大于号|`&gt;`|
|&|和号|`&amp;`|
|￥|人民币|`&yen;`|
|©|版权|`&copy;`|
|®|注册商标|`&reg;`|
|°|摄氏度|`&deg;`|
|±|正负号|`&plusmn;`|
|×|乘号|`&times;`|
|÷|除号|`&divide;`|
|²|平方2（上标2）|`&sup2;`|
|³|立方3（上标3）|`&sup3;`|

`<u>`：下划线标记

`<s>`或`<del>`：中划线标记（删除线）

`<i>`或`<em>`：斜体标记

[](https://camo.githubusercontent.com/98345450c27c2df774895a06d035b22772acc499/687474703a2f2f696d672e736d79687661652e636f6d2f323031352d31302d30312d636e626c6f67735f68746d6c5f31382e706e67)

target：告诉浏览器用什么方式来打开目标页面。target属性有以下几个值：

_self：在同一个网页中显示（默认值）
_blank：在新的窗口中打开。

_parent：在父窗口中显示

_top：在顶级窗口中显示

上标`<sup`> 下标`<sub>`

```html
O<sup>2</sup>    5<sub>3</sub>
```

###  (二)


无序列表`<ul>`，无序列表中的每一项是`<li>`

li不能单独存在，必须包裹在ul里面；反过来说，ul的“儿子”不能是别的东西，只能有li。

type="属性值"。属性值可以选： disc(实心原点，默认)，square(实心方点)，circle(空心圆)。

有序列表<OL>，里面的每一项是`<li>`

type="属性值"。属性值可以是：1(阿拉伯数字，默认)、a、A、i、I。结合start属性表示从几开始。

`<dl>`英文单词：definition list，没有属性。dl的子元素只能是dt和dd。

`<dt>`：definition title 列表的标题，这个标签是必须的

`<dd>`：definition description 列表的列表项，如果不需要它，可以不加

备注：dt、dd只能在dl里面；dl里面只能有dt、dd。

dt、dd都是容器级标签

表格标签用`<table>`表示。 一个表格`<table>`是由每行`<tr>`组成的，每行是由每个单元格`<td>`组成的 