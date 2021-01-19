# 基础选择器

**\* 通配符** 选中所有标签

  tagName(标签名)——》选中叫这个名字的所有标签

​    语法：tagName{}

​    例如：`p{ } ` 选中所有p标签

  **className(类名)**——》选中具有这个类名的所有标签  一个标签可以有多个类名，一个类名可以给多个标签使用

​    语法：.className{ }

​    例如：`.box{ } `   选中类名是box的所有标签

  **idName(id名)**——》选中具有这个id名的标签  每个标签只能有一个id名，一个id名只能给一个标签使用（像身份证一样）

​    语法：#idName{ }

​    例如：`#box{ }`  选中id名是box的标签

# className和idName命名规则：

  1、由数字、字母、下划线_ 中划线- 组成

  2、不能以数字开头

  3、见名知意（看见这个名字就知道，他代表这个模块的能）

  4、推荐使用大驼峰或小驼峰,或者用_ - 连接（top_nav  top-nav）

​    大驼峰：多个单词组合的情况下，每个单词的首字母大写 TopNavLeft

​    小驼峰：多个单词组合的情况下，从第二个单词开始，每个单词的首字母大写 topNavLeft

# 文本和字体属性

### font系列

 **font-size:**长度单位; 浏览器默认字号是16px

​        固定像素px

​        %(父元素字号的百分比)

​        em (相对于父元素字号的倍数)

​        rem (相对于根元素html的font-size的倍数)

   **font-style:** 文字是否倾斜;

​        normal 不倾斜（必须保证这个字体有不倾斜和倾斜的设计）

​        italic 倾斜

​        oblique 强制倾斜（让没有倾斜设计效果的字体强制倾斜）

   **font-weight:** 文字是否加粗

​          normal 不加粗 400

​          bold 加粗 700

​          bolder 更粗 900

​          lighter 更细

​          100-900 整百鼠

   **font-family:**  "" , ""...;

   **line-height: ** 长度单位;

​         固定像素px

​         %(相对于本元素的font-size的百分比计算)

​         数字(相对于本元素的font-size的倍数计算)

​         em(相对于本元素的font-size的倍数计算)

​         rem(相对于根元素html的font-size的倍数计算)

#### 综合写法：

 **font: ** font-style  font-weight font-size/line-height font-family;

(font-size和font-family 必写)

### color:颜色    文字的颜色

# text系列

text-align: 文本和内联元素或者内联块元素在它父元素里的水平对齐方式

​        center 居中对齐

​        left  居左对齐

​        right 居右对齐

  text-decoration:underline 下划线

​          overline  上划线

​          line-through 中划线

​          none 去掉线

  text-indent:长度单位  首行缩进

​        em (相对于本元素的font-size的倍数)

​        px

​        rem

​        %

# 长度单位

 长度单位：

​    固定像素px 

​    em相对单位

​    rem相对于 (相对于html的font-size)

​    %相对单位

# 颜色表示法

#### 英文单词（不常用）

#### 16进制:#000000——#ffffff

​      10进制 0-9 10 11 12

​      8进制 0-7 10 11 12

​      16进制 0 1 2 3 4 5 6 7 8 9 a b c d e f

​      \#000000 黑(black)

​      \#ffffff 白(white)

​      \#ff0000 红(red)

​      \#00ff00 绿(lime)

​      \#0000ff 蓝(blue)

#### rgb(数值,数值,数值) 0-255 0-255 0-255

​      rgb(0,0,0)

​      rgb(255,255,255)

​      rgb(255,0,0)

​      rgb(0,255,0)

​      rgb(0,0,255)

#### rgba(0-255,0-255,0-255,0-1) 0完全透明 1不透明

# 盒模型

 一般会把一个元素看做一个盒子

​    **盒模型：**由 content内容区域 + padding内填充（内边距）+ border边框 + margin外边距 组成

​    **盒模型的宽：**content的宽+左右的padding+左右的border+左右的margin

​    **盒模型的高：**content的高+上下的padding+上下的border+上下的margin

​    **标准盒模型**

​    width——》content的宽

​    height——》content的高

​    max-width

​    max-height

​    min-width

​    min-height

​    **怪异盒模型**

​    width——》content的宽+左右的padding+左右的border

​    height——》content的宽+左右的padding+左右的border

# 边框

####  分写法：

​      border-top-width: 长度单位;

​      border-right-width: 长度单位;

​      border-bottom-width: 长度单位;

​      border-left-width: 长度单位;

​               medium（默认3px）

​               thick 粗5px

​               thin 细1px



​      border-top-style: solid;实线 /*必写 默认边框的宽度是3px 默认的颜色是字体的颜色*/

​      border-right-style: solid;实线 

​      border-bottom-style: solid;实线 

​      border-left-style: solid;实线 

​               dashed 虚线

​               dotted 点状线

​               double 双线



​      border-top-color: 颜色;

​      border-right-color: 颜色;

​      border-bottom-color: 颜色;

​      border-left-color: 颜色;



####     半综合写法：

​      **单个边框：**

​      border-top: width style color;

​      border-right: width style color;

​      border-bottom: width style color;

​      border-left:width style color;

​      **单个样式写法：**

​      border-width:上下左右       1个值

​      border-width:上下   左右     2个值

​      border-width:上    左右 下   3个值

​      border-width:上    右  下 左 4个值



​      border-style:上下左右       1个值

​      border-style:上下   左右     2个值

​      border-style:上    左右 下   3个值

​      border-style:上    右  下 左 4个值



​      border-color:上下左右       1个值

​      border-color:上下   左右     2个值

​      border-color:上    左右 下   3个值

​      border-color:上    右  下 左 4个值



####       综合写法：

​      border: width  style   color;

# padding内填充（内边距）

####   分写法：

  padding-top

  padding-right

  padding-bottom

  padding-left

####  综合写法：

  padding: 上下左右  							 	1个值

​					上下           左右               		2个值

​					上              左右       下          	3个值

​					上               右          下     左     4个值

# margin 外边距

元素和（兄弟元素） 或者 （父元素的边界）的空隙

####   分写法：

  margin -top

  margin -right

  margin -bottom

  margin -left

####  综合写法：

  margin :  上下左右  							  	1个值

​					上下           左右               	 	2个值

​					上              左右       下          	3个值

​					上               右          下     左     4个值





























