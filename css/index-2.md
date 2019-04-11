
**background系列属性**

```css
div {
    background-color: #ff99ff;
    /*设置元素的颜色:red、rgb（255,0,0）、#ff0000。
    常见颜色：#000   黑
	         #fff   白
	         #f00   红
	         #222   深灰
	         #333   灰
                #ccc   浅灰
             */
    background-image: url(images/1.gif);/*将图像设置为背景*/
    background-repeat: no-repeat;/*设置背景图像是否重复及如何重复，默认平铺满。
        no-repeat：不要平铺
        repeat-x：横向平铺
        repeat-y：纵向平铺
        */
    background-position: center top;/*设置背景图片在当前容器中的位置，
        background-position:向右偏移量 向下偏移量;
        background-position:100px 900px;
        */
    background-attachment: scroll;/*设置背景图片是否跟着滚动条一起移动。 
    属性值可以是：scroll（与fixed属性相反，默认属性）
                 fixed（背景就会被固定住，不会被滚动条滚走）
                 */
    background:red url(1.jpg) no-repeat 100px 100px fixed;/*	
        background-color:red;
	    background-image:url(1.jpg);
	    background-repeat:no-repeat;
	    background-position:100px 100px;
            background-attachment:fixed;
        */
}
```