
**字体属性**

```css
p {
    font-size: 30px;     /*字体大小*/
    line-height: 50px;      /*行高*/
    font-family: "幼圆","黑体";     /*字体类型：如果没有幼圆就显示黑体，没有黑体就显示默认*/
    font-style: italic;     /*italic表示斜体，normal表示不倾斜*/
    font-weight: bold;      /*粗体：属性值写成bolder也可以*/
    font-variant: small-caps;       /*小写变大写*/

    /*文本属性*/
    letter-spacing: 0.5cm;      /*单个字母之间的间距*/
    word-spacing: 1cm;      /*单词之间的间距*/
    text-decoration: none;      /*字体修饰：none去掉下划线、underline下划线、line-through中划线、overline上划线*/
    text-transform: lowercase;      /*单词字体大小写。uppercase大写、lowercase小写、capitalize（每个单词的首个字母大写）*/
    color: red;     /*字体颜色*/
    text-align: center;     /*在当前容器中的对齐方式。属性值可以是：left、right、center（在当前容器的中间）、justify*/
}
```

**列表属性**

```css
ul li {
    list-style-image: url(images/1.png);    /*列表项前设置为图片*/
    margin-left: 80px;  /*公有属性*/
    overflow: hidden;   /*超出范围的内容。auto：浏览器自己解决，在必需时截切对象多余的内容或显示滚动条、visible：默认值，多余的内容不剪切也不添加滚动条，会全部显示出来、hidden：不显示超过对象尺寸的内容，对象将以包含对象的window或frame的尺寸进行截切，并且clip属性设置将失效、scroll：总是显示滚动条*/
}
```

**鼠标的属性**

```css
p:hover{
    cursor: pointer;/*鼠标放在那个标签上时，光标显示手状*/
}
```