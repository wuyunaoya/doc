# 定位

 position: static 静态定位（ 默认不定位）

​      		  relative  相对定位（相对于自己） 

​      	      absolute  绝对定位（相对于，离自己最近的定位父辈元素）

​                 fixed   固定定位（相对于浏览器窗口定位）

  偏移量（定位必要配合偏移量）

  left 

  right

  top  

  bottom 

## 相对定位position:relative

#### 偏移量

  left  距自己原来的left边有多远的距离（正值向右，负值向左）

  right 距自己原来的right边有多远的距离（正值向左，负值向右）

  top  距自己原来的top边有多远的距离（正值向下，负值向上）

  bottom 距自己原来的bottom边有多远的距离（正值向上，负值向下）

# 绝对定位

 position:absolute  绝对定位（相对于，离自己最近的定位父辈元素）

####   偏移量

  left  自己的margin-left距最近的定位父元素的padding-left多远的距离

  right 自己的margin-right距最近的定位父元素的padding-right多远的距离

  top  自己的margin-top距最近的定位父元素的padding-top多远的距离

  bottom 自己的margin-bottom距最近的定位父元素的padding-bottom多远的距离

# 块元素水平垂直居中的方式

 **第一种，已知子元素宽高**

  父元素：相对定位

  ```css
  .wrap{
     position: relative;/*父相*/
   }
  ```



  子元素：绝对定位+ left: 50% + top: 50% + margin-left:负的宽度的一半 + margin-top:负的高度的一半;

  ```css
  .box{
      width: 100px;
     height: 100px;
     position: absolute;/*子绝*/
     left: 50%;
     top: 50%;
     margin-left: -50px;/*负的宽度的一半*/
      margin-top: -50px;/*负的高度的一半*/
    }
  ```

  **第二种：不知子元素的宽高**

  父元素：相对定位

  ```css
  .wrap{
      position: relative;/*父相*/
   }
  ```

  子元素：

  ```css
 .box {
 	 position: absolute;
	/*子绝*/
	 left: 0;
	 right: 0;
	 top: 0;
	 bottom: 0;
	 margin: auto;
 }
  ```

# 固定定位

 position: fixed 固定定位（相对于浏览器窗口定位，不会随着页面的滚动而滚动）

 偏移量（定位必要配合偏移量）

  left  距浏览器窗口左边的距离

  right  距浏览器窗口右边的距离 

  top   距浏览器窗口上边的距离

  bottom  距浏览器窗口下边的距离

# 定位特性

 **相对定位：**

  1、会提层级

  2、保留元素原来的占位，不脱离文档流 

  3、不写偏移量的时候，不会对元素有任何影响， 一般用在微量像素的调整，或者配合绝定定位使用

  **绝对定位：**

  1、提升层级

  2、脱离文档流并且脱离文本流，完全不占位置（文本和图片会完全的呼市定位元素，不会绕着定位元素排列）

  3、没有给偏移量的时候，位置不会变

  4、没有定位父元素时，相对于浏览器窗口定位，有定位父元素时，相对于最近的定位父元素

  5、可以让内联元素支持宽高和margin、padding、border等属性

  6、可以让块元素失去原来的默认宽高，让宽高适应内容

  **固定定位：**

  1、提升层级

  2、脱离文档流并且脱离文本流，完全不占位置（文本和图片会完全的呼市定位元素，不会绕着定位元素排列）

  3、没有给偏移量的时候，位置不会变

  4、可以让内联元素支持宽高和margin、padding、border等属性

  6、可以让块元素失去原来的默认宽高，让宽高适应内容

# 层级z-index

层级：元素在垂直电脑屏幕方向上的层叠顺序

默认：后写的覆盖先写的，子元素覆盖父元素 (z-index:0)。  浮动元素层级高于普通元素，低于定位元素；定位元素层级高于浮动元素和普通元素

z-index 必须配合定位使用

当父元素有z-index属性时，那么子元素z-index失效

#  浮动和定位对比：

  浮动：

  1、浮动脱离文档流，但是不脱离文本流，文字、图片（内联和内联元素会围绕着浮动元素排列）

  2、层级高于普通元素，低于定位元素

  定位：

  1、定位既脱离文档流又脱离文本流，

  2、定位元素层级高于浮动元素和普通元素

  脱离文档流的元素，没有类型的区分，所有元素会失去默认宽高，让宽高适应内容，并且支持width/height/margin/padding/border/line-height等属性、并且没有margin塌陷和基线问题

# 显示与隐藏

 display:block/inline/inline-block/none(元素隐藏且不占位)

 visibility:visible(默认不隐藏) / hidden;(隐藏且占位)

# overflow

 overflow:内容溢出

​     		  hidden 溢出隐藏

​     		  scroll 显示滚轮（溢出有滚动条）

​     		  auto 内容溢出就显示滚动条，没有溢出不会有变化

  overflow-x:只关注x轴方向

  overflow-y:只关注y轴方向

# vertical-align 垂直方向上的对齐方式

vertical-align : top 顶部对齐

​					      text-top  文本框的顶部

​					      middle   中部对齐

​					 	baseline  基线对齐

​				         text-bottom  文本框的底部

​				         bottom   底部对齐

​				     	super   上标对齐

​				     	sub      下标对齐

问题：内联块默认基线对齐

解决：vertical-align:top/middle/bottom

#  border-radius

   border-radius:圆角 px %    

​							  四个角                    										1个值时

​         					左上和右下   右上和左下        		 			  2个值时

​        					 左上     		 右上和左下     右下      			 3个值时

​       					  左上      		右上    			 右下  	左下     3个值时

  border-top-left-radius:第一个值是圆角x方向的倾斜  第二个值是圆角y方向的倾斜(当x=y 可简写为一个值)

  border-top-right-radius:

  border-bottom-right-radius:

  border-bottom-left-radius:















