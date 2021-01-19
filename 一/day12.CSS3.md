# CSS3基本介绍

CSS升级版本，最新版本的主流浏览器已经支持大部分新增属性，CSS3向后兼容，对CSS2可以做一个效果的加强

### 1、按模块新增：

选择器、框模型、背景和边框、文本效果、2d/3d转换、动画、多列布局、用户界面

### 2、CSS2和CSS3对比：

- css2：
  - 性能和访问相对较差
  - 更偏向于表现
  - 圆角和渐变等部分效果需要用图片实现
  - 无兼容性问题
- css3：
  - 性能和效果都能得到兼顾
  - 可实现动画效果
  - 在CSS2中需要使用图片的效果在CSS3中可以直接用代码实现
  - 部分属性需要兼容处理

### 3、渐进增强和优雅降级

**渐进增强：** 针对低版本浏览器进行页面建构，保证最基本功能的实现，然后再针对高级浏览器进行效果的设置。交互的实现，达到更好的用户体验

**优雅降级：** 一开始构建完美的用户体验，然后再针对低版本浏览器进行兼容

**区别： **优雅降级是从复杂的现状开始，并试图减少用户体验的供给，而渐进增强则是从一个非常基础的，能够起作用的版本开始，并不断扩充，以适应未来环境的需要。

![渐进增强和优雅降级](图片/渐进增强和优雅降级.png)

### 4、浏览器私有前缀（兼容性前缀）

Chrome、Safari——webkit——》    -webkit-

FireFox——gecko——》    -moz-

opera——presto——》  -o-

IE——trident——》   -ms-

**书写顺序：** 先写带有私有前缀的属性，再写标准的CSS3属性

```html
<div class="box"></div>
```

```css
.box{
    -webkit-border-radius:50%；
    -moz-border-radius:50%;
    -o-border-radius:50%;
    -ms-border-radius:50%;
    border-radius:50%; 
}
```

### 5、autoprefixer插件

css前缀自动生成（基于postCSS）

下载插件

**在css文件中**，按f1,执行  autoprefixer run

# css3新增选择器

## 1、属性选择器

### CSS2 :

**E[attr]　有attr属性的E元素** 

```css
/* 有title属性的元素 */
[title]{
        color: red;
}

/* 有title属性的元素div元素 */
div[title]{
         color: red;
}
```

**E[attr=value]    有attr属性，且attr=”value”的E元素** 

```css
/* title=div2 的div元素*/
div[title=div2]{
            color: red;        
}
```

**E[attr|=value]    attr属性的第一个属性值以value开头，的E元素 (适用于由连字符-分隔的属性值)**

```html
div[title|=div1]{
            color: red;
}
```

```html
<div title="div1-box">div1</div>
```

**E[attr~=value]   attr属性的其中一个属性值为value的E元素 (适用于由空格分隔的属性值)**

### CSS3 :

**E[attr^=value]    attr属性的属性值以value开头的E元素**

```css
div[title^=div1]{
        color: red;
}
```

```html
<div title="div1 box">div1</div>
<div title="div1-box">div1</div>
<div title="div1_box">div1</div>
<div title="div1box">div1</div>
```

**E[attr$=value]    attr属性的属性值以value结尾的E元素**

```css
div[title$=div1]{
        color: red;
}
```

```html
<div title="box div1">div1</div>
<div title="box-div1">div1</div>
<div title="box_div1">div1</div>
<div title="boxdiv1">div1</div>
```

**E[attr*=value]   attr属性的属性值包含value的E元素**

 ```css
div[title*=div1]{
    color: red;
}
 ```

```html
<div title="box div1 box">div1</div>
<div title="box-div1-box">div1</div>
<div title="boxdiv1box">div1</div>
```

## 2、结构性伪类选择器

E:first-child   属于父元素的第一个子元素的E元素（css2）

E:last-child    属于父元素的最后一个子元素的E元素

E:nth-child(n)  属于父元素的第n个子元素的E元素(odd奇，even偶,)

E:nth-last-child(n)   同E:nth-child(n)，从最后开始数 (n 可以是数字、关键词或公式)

E:nth-of-type(n)    属于父元素的第n 个E元素

E:nth-last-of-type(n)   同E:nth-of-type(n)，从最后开始数

## 3、状态伪类选择器

E:checked处于选中状态的E元素

E:enabled 处于可用状态的E元素

E:disabled 处于禁用状态的E元素

## 4、附完整选择器表

| 选择器               | 例子                  | 例子描述                                              | CSS  |
| -------------------- | --------------------- | ----------------------------------------------------- | ---- |
| .class               | .intro                | 选择 class="intro" 的所有元素。                       | 1    |
| #id                  | #firstname            | 选择 id="firstname" 的所有元素。                      | 1    |
| *                    | *                     | 选择所有元素。                                        | 2    |
| element              | p                     | 选择所有 <p> 元素。                                   | 1    |
| element,element      | div,p                 | 选择所有 <div> 元素和所有 <p> 元素。                  | 1    |
| element element      | div p                 | 选择 <div> 元素内部的所有 <p> 元素。                  | 1    |
| element>element      | div>p                 | 选择父元素为 <div> 元素的所有 <p> 元素。              | 2    |
| element+element      | div+p                 | 选择紧接在 <div> 元素之后的所有 <p> 元素。            | 2    |
| [attribute]          | [target]              | 选择带有 target 属性所有元素。                        | 2    |
| [attribute=value]    | [target=_blank]       | 选择 target="_blank" 的所有元素。                     | 2    |
| [attribute~=value]   | [title~=flower]       | 选择 title 属性包含单词 "flower" 的所有元素。         | 2    |
| [attribute\|=value]  | [title\|=flower]      | 选择 title 属性以 "flower" 开头的所有元素             | 2    |
| :link                | a:link                | 选择所有未被访问的链接。                              | 1    |
| :visited             | a:visited             | 选择所有已被访问的链接。                              | 1    |
| :active              | a:active              | 选择活动链接。                                        | 1    |
| :hover               | a:hover               | 选择鼠标指针位于其上的链接。                          | 1    |
| :focus               | input:focus           | 选择获得焦点的 input 元素。                           | 2    |
| :first-letter        | p:first-letter        | 选择每个 <p> 元素的首字符。                           | 1    |
| :first-line          | p:first-line          | 选择每个 <p> 元素的首行。                             | 1    |
| :first-child         | p:first-child         | 选择属于父元素的第一个子元素的每个 <p> 元素。         | 2    |
| :before              | p:before              | 在每个 <p> 元素的内容之前插入内容。                   | 2    |
| :after               | p:after               | 在每个 <p> 元素的内容之后插入内容。                   | 2    |
| :lang(language)      | p:lang(it)            | 选择带有以 "it" 开头的 lang 属性值的每个 <p> 元素。   | 2    |
| element1~element2    | p~ul                  | 选择前面有 <p> 元素的每个 <ul> 元素。                 | 3    |
| [attribute^=value]   | a[src^="https"]       | 选择其 src 属性值以 "https" 开头的每个 <a> 元素。     | 3    |
| [attribute$=value]   | a[src$=".pdf"]        | 选择其 src 属性以 ".pdf" 结尾的所有 <a> 元素。        | 3    |
| [attribute*=value]   | a[src*="abc"]         | 选择其 src 属性中包含 "abc" 子串的每个 <a> 元素。     | 3    |
| :first-of-type       | p:first-of-type       | 选择属于其父元素的首个 <p> 元素的每个 <p> 元素。      | 3    |
| :last-of-type        | p:last-of-type        | 选择属于其父元素的最后 <p> 元素的每个 <p> 元素。      | 3    |
| :only-of-type        | p:only-of-type        | 选择属于其父元素唯一的 <p> 元素的每个 <p> 元素。      | 3    |
| :only-child          | p:only-child          | 选择属于其父元素的唯一子元素的每个 <p> 元素。         | 3    |
| :nth-child(n)        | p:nth-child(2)        | 选择属于其父元素的第二个子元素的每个 <p> 元素。       | 3    |
| :nth-last-child(n)   | p:nth-last-child(2)   | 同上，从最后一个子元素开始计数。                      | 3    |
| :nth-of-type(n)      | p:nth-of-type(2)      | 选择属于其父元素第二个 <p> 元素的每个 <p> 元素。      | 3    |
| :nth-last-of-type(n) | p:nth-last-of-type(2) | 同上，但是从最后一个子元素开始计数。                  | 3    |
| :last-child          | p:last-child          | 选择属于其父元素最后一个子元素每个 <p> 元素。         | 3    |
| :root                | :root                 | 选择文档的根元素。                                    | 3    |
| :empty               | p:empty               | 选择没有子元素的每个 <p> 元素（包括文本节点和空格）。 | 3    |
| :target              | #news:target          | 选择当前活动的 #news 元素。                           | 3    |
| :enabled             | input:enabled         | 选择每个启用的 <input> 元素。                         | 3    |
| :disabled            | input:disabled        | 选择每个禁用的 <input> 元素                           | 3    |
| :checked             | input:checked         | 选择每个被选中的 <input> 元素。                       | 3    |
| :not(selector)       | :not(p)               | 选择非 <p> 元素的每个元素。                           | 3    |
| ::selection          | ::selection           | 选择被用户选取的元素部分。                            | 3    |

# 多背景图background:背景1, 背景2,...;

IE8以及以下不支持

#### 综合写法：

background: url(1.png) no-repeat center , url(2.png)  no-repeat center ;

#### 分写法：

background-image: url(images/pic1.jpeg),  url(images/pic2.jpeg);

background-repeat: no-repeat;

background-position: left top,  right bottom;

# background-size背景图片的尺寸

IE9+

background-size: xpx  ypx 只设一个，第二个值是auto，等比例缩放

​								  x%  y% 盒子的宽高%。只设一个，第二个值是auto，等比例缩放，

​								  cover 等比缩放，刚好盖住

​								  contain 等比缩放，刚好盛下

# background-origin背景图开始位置

background-origin: border-box 

padding-box 默认

content-box

# background-clip背景的绘制区域

background-clip: border-box 默认

padding-box

content-box

# 5、背景颜色渐变

在两个或多个指定的颜色之间显示平稳的过渡 

### 5.1线性渐变Linear Gradients

background-image: linear-gradient(方向, 颜色1  渐变 ,颜色2  渐变2, ...)

#### 颜色结点（至少定义两种颜色结点）

background-image: linear-gradient( color1, color2, ...),

 									linear-gradient( color1, color2, ...),

​									 ...

background-image: repeating-linear-gradient(color1, color2, ...);

![渐变颜色节点](C:\Users\IBM\Desktop\0824\0908day12\笔记\图片\渐变颜色节点.png)

#### 渐变结点(% px em)

background-image: linear-gradient(

​       	color1  从哪里开始渐变(默认0%),

​	       color2  从哪里开始渐变,

​      	color3  从哪里开始渐变,

 	     ......

)

background-image: repeating-linear-gradient(

​       	color1  从哪里开始渐变(默认0%),

​	       color2  从哪里开始渐变,

​      	color3  从哪里开始渐变,

 	     ......

)

![线性渐变渐变节点](图片\线性渐变渐变节点.png)

#### 方向

加前缀：top | right | left | bottom | left top | left bottom | right top | right bottom

不加前缀：to  top | to right | to left | to bottom | to left top | to  left bottom | to  right top |to right bottom

角度 :0deg

background-image: -webkit-linear-gradient(top,red ,green);

background-image: -o-linear-gradient(top,red ,green);

background-image: -ms-linear-gradient(top,red ,green);

background-image: -moz-linear-gradient(top,red ,green);

![线性渐变角度（有前缀）](图片\线性渐变角度（有前缀）.png)

background-image: linear-gradient( **to top**, color1, color2, ...)

background-image: linear-gradient( 0deg, color1, color2, ...)

![线性渐变角度](图片/线性渐变角度.png)

### 5.2径向渐变Radial Gradients

background-image: radial-gradient(形状  大小  at  圆心位置, 颜色1  渐变点1,,......);

background-image: repeating-radial-gradient(形状  大小  at 圆心位置, 颜色1  渐变点1,......);

background-image: -webkit- radial-gradient(圆心位置 , 形状 大小, 颜色1  渐变点1,......);

#### 圆心位置

at    水平  垂直   ( 有前缀不加at  没前缀加at）

​		 %	  %

​		px	  px

​		em	  em

​	    left	  top

​	center  center

​	 right    bottom

#### 形状

ellipse 椭圆（默认，跟随着元素的宽高变化）

circle  圆 

# 用户界面

### resize

​	 resize: none;/* 不允许用户改变 */

​      resize: both;/* 允许用户改变 */

​      resize: vertical;/* 允许用户改变垂直方向*/

​      resize: horizontal; /*允许用户改变水平方向 */

### box-sizing

**box-sizing : content-box**

   标准盒模型由  content  padding   border   margin 组成

   标准盒模型的宽：width+左右padding+左右border+左右margin

   标准盒模型的高：height+上下padding+上下border+上下margin

**box-sizing : border-box**

   怪异盒模型（ie盒模型）由  content  padding   border   margin 组成

   怪异盒模型的宽：width(content宽+左右padding+左右border)+左右margin

   怪异盒模型的高：height(content高+上下padding+上下border)+上下margin

  



























