# margin值塌陷问题

#### 父子之间：

   		 **问题：**当父元素没有垂直方向的border和padding时，垂直方向的margin值不会把父元素撑起来，而是会传递给父元素，且应用其中最大的值

​      	**解决：**1、给父元素加上垂直方向上的border(不推荐)。或者转换思路，将子元素的margin-top（margin-bottom），转换成父元素的padding-top（padding-bottom）

​				   2、让父元素触发BFC(块级格式上下文)，改变父级的渲染规则

​								(1)position:absolute / fixed

​								(2)display:inline-block

​								(3)float:left / right

​								(4)overflow:hidden / scroll / auto

####   兄弟之间：

​          **问题：**上面盒子的margin-bottom和下面盒子的margin-top会重叠，并且取两者之间的最大值

​         **解决：**只写一个

# 浮动

 网页布局核心：用css摆放盒子

  如何去摆放盒子？

  css布局的三大定位机制：**标准流（普通流）、浮动、定位（position）**

  			  **标准流：**在网页中盒子正常状态下从左往右或者从上往下进行排列，比如块元素垂直方向排列，内联元素水平方向排列

  		 	**浮动:** 设置了浮动的元素脱离标准流的控制，盒子会在一行排列，会尽量向左或者向右移动，直到碰到他的父元素的边界或者另一个浮动元素

​					目的：改变盒子的位置。核心技术：盒子在什么位置，是否占位

​				**定位（position）：**

### 浮动属性：

**float:left/right/none(默认不浮动)**

### 浮动带来的问题：

元素浮动之后，脱离文档流不占位，无法撑起父元素的高度，就会影响后续的布局

### 解决：清除浮动带来的影响

​    1、给父元素设置固定的高度（不灵活）

​    2、在父元素的最后添加一个空的块元素，然后给这个块元素设置 clear:both;(会造成代码冗余)

​    3、给父元素设置BFC属性，让父元素变为一个 BFC(块级格式化上下文) ，改变父元素的渲染方式

​     		   1.overflow:hidden/scroll/auto

​    		    2.display:inline-block

​    		    3.float:left/right(浮动本身不占位)

   		     4.position:absolute/fixed（定位本身不占位）

​    4、利用伪元素模拟第二种方法

​      给浮动元素的父元素添加一个伪元素，给伪元素设置display: block;clear: both;

 ```css
   .clearFix:after {
   		 content: "";
  	     display: block;
         clear: both;
   }
   .clearFix{

        *zoom: 1;/*兼容低版本IE浏览器*/
   }
 ```

ps:

```html
<a href="javscript:;"></a>  阻止跳转
```

