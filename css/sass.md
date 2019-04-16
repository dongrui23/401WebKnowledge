
**变量**

Variables: $

```css
/*css属性*/

$width: 5em;

/*属性中引用*/

#main {
  width: $width;
}
```

**嵌套规则**

```css
#main p {
  color: #00ff00;
  width: 97%;

  .redbox {
    background-color: #ff0000;
    color: #000000;
  }
}

/*被编译为：*/

#main p {
  color: #00ff00;
  width: 97%; }
  #main p .redbox {
    background-color: #ff0000;
    color: #000000; }
------------------------------
#main {
  width: 97%;

  p, div {
    font-size: 2em;
    a { font-weight: bold; }
  }

  pre { font-size: 3em; }
}
/*被编译为：*/

#main {
  width: 97%; }
  #main p, #main div {
    font-size: 2em; }
    #main p a, #main div a {
      font-weight: bold; }
  #main pre {
    font-size: 3em; }
```

**mixins**

Defining a Mixin: @mixin

```css
/* large-text的mixin定义 */

@mixin large-text {
  font: {
    family: Arial;
    size: 20px;
    weight: bold;
  }
  color: #ff0000;
}
----------------------
/* @include指令 */

.page-title {
  @include large-text; /* 包含large-text的mixin定义 */
  padding: 4px;
  margin-top: 10px;
}

/* 被编译为： */

.page-title {
  font-family: Arial;
  font-size: 20px;
  font-weight: bold;
  color: #ff0000;
  padding: 4px;
  margin-top: 10px; }
------------------------------------
/* Mixins可以将参数SassScript值作为参数 */

@mixin sexy-border($color, $width) {
  border: {
    color: $color;
    width: $width;
    style: dashed;
  }
}

p { @include sexy-border(blue, 1in); }

/* 被编译为： */

p {
  border-color: blue;
  border-width: 1in;
  border-style: dashed; }
```

**导入**

```css
/* @import */

@import "foo.css";

@import "foo" screen;

@import "http://foo.com/bar";

@import url(foo);

/* 引入多个文件 */

@import "rounded-corners", "text-shadow";

```

@import在mixins或控制指令中嵌套是不可能的。

**阅读**

[Sass文档](http://sass.bootcss.com/)