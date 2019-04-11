
CSS只有/* */这种注释，没有//这种注释。而且注释要写在<style>标签里面才算生效

引入外部样式表css文件的方式。这种方式又分为两种：

```
1、采用<link>标签。例如：<link rel = "stylesheet" type = "text/css" href = "a.css"></link>

2、采用import，必须写在<style>标签中，并且必须是第一句。例如：@import url(a.css) ;
```