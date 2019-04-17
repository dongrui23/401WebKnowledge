
###1 初识jquery

```
<script>
  $(function (){
    var $div1=$('div');
    var $div2=$('.box1');//class
    var $div3=$('#box2');//id
    console.log($div1);
    console.log($div2);
    console.log($div3);

    $div1.css({
      background:'red'
    })
  });
</script>
```
2
引用
jquery固定写法$(document).ready((function)(){})

3
var width=window.getComputedStyle(img).width;得到图片宽度，原生js
var $width=$img.width()