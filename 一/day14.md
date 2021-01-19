# 一、弹性盒子

​		弹性盒子是 CSS3 的一种新的布局模式。提供一种更加有效的方式来对一个容器中的子元素进行**排列、对齐和分配空白空间**

![弹性盒子兼容](图片\弹性盒子兼容.png)

给容器（父元素怒）设置 display:flex （inline-flex）将其定义为弹性容器。子元素的float、clear和vertical-align等属性将失效

## 容器（父元素）属性

容器（父元素）：给容器设置display:flex （inline-flex）

###  flex-direction主轴方向

flex-direction: row; 从左往右，默认 

​                	 	row-reverse; 从右往左

​                		 column  从上往下

​             	       column-reverse 从下往上

![flex-direction](图片\flex-direction.png)

### justify-content项目在主轴方向上的排列方式

justify-content: flex-start   开头对齐  

​             		       flex-end    结尾对齐

​                	 	  center     居中对齐

​               	 	   space-between  两端对齐，两端没有缝隙，中间的缝隙相等

​      					space-around  分散对齐，左右两边的缝隙是中间缝隙的一半

![justify-content-content](图片\justify-content-content.png)   

### align-content项目在侧轴（交叉轴）方向上的排列方式

align-content: flex-start   开头对齐  

​             		    flex-end    结尾对齐

​                		 center     居中对齐

​               		  space-between  两端对齐，两端没有缝隙，中间的缝隙相等

​             		    space-around  分散对齐，左右两边的缝隙是中间缝隙的一半

![align-content](图片\align-content.png)

### align-items设置项目在侧轴（交叉轴）方向的对齐方式

 align-items:  flex-start 起点对齐（项目在容器的起点对齐，并且项目与项目之间也是起点对齐）

​              		  flex-end  终点对齐（项目在容器的终点对齐，并且项目与项目之间也是终点对齐）

​           		     center   居中对齐（项目在容器的居中对齐，并且项目与项目之间也是居中对齐）

​       		         baseline  项目的第一行文字的基线对齐

​         		       stretch   如果项目未设置高度(auto)，将占满整个容器的高度

![align-items](图片\align-items.png)

###  flex-wrap换行

 		弹性盒子内部，默认不换行。当容器一行盛放不下项目时，不会换行，会自动压缩项目的宽。 即使项目设置了固定宽度，也不会换行，同样也会自动压缩项目的宽

 flex-wrap: nowrap 默认不换行

​             	   wrap  换行

​           	     wrap-reverse 换行，且上下行做一个翻转

![flex-wrap](图片\flex-wrap.png)

##  项目（子元素）属性

 项目（子元素）默认按主轴方向排列

### align-self替代父元素的align-items

align-self:   flex-start 起点对齐（项目在容器的起点对齐，并且项目与项目之间也是起点对齐）

​                flex-end  终点对齐（项目在容器的终点对齐，并且项目与项目之间也是终点对齐）

​                center   居中对齐（项目在容器的居中对齐，并且项目与项目之间也是居中对齐）

​                baseline  项目的第一行文字的基线对齐

​                stretch   如果项目未设置高度(auto)，将占满整个容器的高度

### order项目在容器里的排列顺序

order:数值  默认值是0 

​            小值排前，大值排后，order相等的情况下，按结构顺序排列

### flex-grow容器剩余空间的分配               

flex-grow 当容器有剩余空间时，定义项目放大比例, 默认值0

### flex-shrink 容器空间不够时的分配

flex-shrink 当容器盛放不下项目，不够空间时，项目缩小的比例，默认值1

### flex: flex-grow flex-shrink;             

# 二、calc函数

calc() 函数用于动态计算长度值，是css3的一个新增的功能，用来指定元素的长度（常用于自适应布局）

移动端的浏览器仅有 “ firefox for android 14.0 ”支持

![calc兼容](图片\calc兼容.png)

**语法： **  calc(表达式)。   支持+-*/ 运算，   运算符前后都需要保留一个空格

```css
{
    	width: calc(100% / 10 );
        height: calc(100% / 5 );
    	margin-left: calc(-100% / 10 / 2 );
        margin-top: calc(-100% / 5 / 2 );
        font-size: calc( 100px + 2px );
    	font-size: calc( 100px - 2px );
        font-size: calc( 100px * 2 );
   		font-size: calc(100% / 10); 
}
```

# 三、预处理语言

**less**   sass(scss)   Compass、CoffeeScript

​		CSS 预处理语言，用一种专门的编程语言，为 CSS 增加了一些编程的特性，将 CSS 作为目标生成文件，然后开发者就只要使用这种语言进行编码工作。可以有让CSS更加简洁、适应性更强、可读性更佳，更易于代码的维护等诸多好处。
预处理语言工具：**语法  编译器**

## 编译器

koala（软件） 编辑器插件     后台程序      在线编译

## koala

#### 将语言设置为中文

![koala1](图片\koala1.png)

![koala2](图片\koala2.png)

#### 将项目拖动过来之后，设置输出路径

![koala5](图片\koala5.png)

#### 选择编译方式

![koala3](图片\koala3.png)

![koala4](图片\koala4.png)

#### 选择是否压缩css文件

![koala6](图片\koala6.png)

#### 在less文件里写代码

## vscode的扩展插件easy less

#### 安装easy less

![easy less01](图片\easy less01.png)

#### 在setting.json里设置less

```json
 {    
     "less.compile": {
         "compress":  false,  // true => 是否压缩
         "sourceMap": false,  // true => 是否生成映射文件
         "out": "./" ,        // 设置输出路径
     }
 }
```

![easy less02](图片\easy less02.png)

#### 在less文件里写代买

## less语法

### 1、注释

第一种`// 单行注释，不会编译到css文件里`

第二种`/* 多行注释，会编译到css文件里 */`

**less文件里：**

```less
// 单行注释，不会编译到css文件里
/* 多行注释，会编译到css文件里 */
```

**编译到css文件里:**

```css
/* 多行注释，会编译到css文件里 */
```

### 2、在less文件里面引入其他文件

#### **第一种引入css文件：**

**less文件里：**

```less
/*1. 引入重置css文件 */
@import "reset.css";
```

**编译到css文件里:**

```css
/*引入重置css文件 */
@import "reset.css";
```

#### 第二种引入less文件

**public.less文件里：**

```less
div{
    width: 100px;
    height: 100px;
}
```

**index.less文件里：**

```less
/* 引入公共样式文件 */
@import "public.less";//.less 可以省略不写
```

**编译到index.css文件里:**

```css
/* 引入公共样式文件 */
div {
  width: 100px;
  height: 100px;
}
```

### 3、变量

定义变量: @变量名:值

```less
@bgc:background-color;
@clr:red;
```

使用变量

@{变量名1} : @变量名2

```less
div{
    @{bgc}:@clr;
}
```

### 4、嵌套

选择器1{

​			样式名1: 样式值1；

​			样式名2: 样式值2；

​			选择器2{

​						选择器3{    }

​						**// & 代表选择器2**

​						**&: hover{   }**

​			}

​			**选择器2:hover{  }**

}

```less
.wrap{
    width:100px;
    ul{
        width:50px;
        li{ 
        	color:red;
        }
        // &代表ul
        &:hover a{
        	color:red;
        }
    }
    ul:hover a{ 
    	background-color:pink
    }
}
```

### 5、混入

**定义类：**

类选择器{

}

```less
.box{
    width: 100px;
    height: 100px;
}
```

**使用类：**

选择器{

​		类选择器；

​		类选择器()；

}

```less
.box1{
    .box();
    background-color: pink;
}
.box2{
    .box;
    background-color: blue;
}
```

**编译之后的css:**

```css
.box {
 	 width: 100px;
 	 height: 100px;
}
.box1 {
      width: 100px;
	  height: 100px;
 	 background-color: pink;
}
.box2 {
  	 width: 100px;
 	 height: 100px;
 	 background-color: blue;
}
```

#### 混入，有参数

**定义：**

类选择器(@形参名1,@形参名2,,,){

​			样式名: @形参名1；

}

```less
.obox(@x,@y){
 	 width: @x;
 	 height: @y;
}
```

**使用：**

选择器{

​			类选择器(实参1,实参2，，)

}

```less
.obox1{
 	 background-color: pink;
 	 .obox(100px,200px);
}
.obox2{
 	 background-color: blue;
 	 .obox(200px,100px)
}
```

#### 混入，有参数，且有默认值

**定义：** 

类选择器(@形参名1:默认值1,@形参名2:默认值2，，，){

​			样式名: @形参名1；

}

```less
.abox(@x:100px,@y:100px,@z:red){
	  width: @x;
	  height: @y;
	  background-color: @z;
}
```

**使用：**

选择器{

​			类选择器() //不传参，使用默认值，传参则使用传过来的实参

}

选择器{

​			类选择器(实参1,实参2，，，) 

}

```less
.abox1{
	.abox()//没有传参，使用默认值
}
.abox2{
   .abox(200px,200px,yellow)
}
```

**编译后的css:**

```css
//使用的默认值
.abox1 {
 	 width: 100px;
 	 height: 100px;
 	 background-color: red;
}
// 传实参
.abox2 {
 	 width: 200px;
 	 height: 200px;
 	 background-color: yellow;
}
```

#### 使用@arguments来引用所有传入的变量

**定义：** 

类选择器(@形参名1:默认值1,@形参名2:默认值2，，，){

​			样式名:@arguments;；

}

```less
.bbox(@w:1px,@s:solid,@c:red){
  	 // border:@w @s @c ;	 
    border:@arguments;
}
```

**使用：**

选择器{

​			类选择器() //不传参，使用默认值，传参则使用传过来的实参

}

选择器{

​			类选择器(实参1,实参2，，，) 

}

```less
.bbox1{
	.bbox()//没有传参，使用默认值
}
.bbox2{
   .bbox(5px,dotted,pink)
}
```

**编译后的css:**

```css
.bbox1 {
  border: 1px solid red;
}
.bbox2 {
  border: 5px dotted pink;
}
```

### 6、 extend继承 

**定义：**

类选择器{

}

```less
.cbox{
 	 width: 100px;
  	height: 100px;
}
```

**使用：**

```less
.cbox2:extend(.cbox){
	 background-color:pink;
}
.cbox3{
 	 &:extend(.cbox);
  	 background-color: blue;
}
```

**编译后的css:**

```css
// 重复的代码，自动归到一类
.cbox,
.cbox2,
.cbox3 {
  	width: 100px;
 	 height: 100px;
}
.cbox2 {
 	 background-color: pink;
}
.cbox3 {
	  background-color: blue;
}
```

### 7、计算

```less
.dbox{
    width: 10px+10px;
    height: 100%+10px;
    font-size: 20px*2;
    line-height: 30px/2;
    margin: 100px-2px;
    padding: 100*(1px+2px);
    color: red+rgb(0,1,0);
    background-color: red+#001100;
    border: 1px solid  red+lime+blue;
}
```































