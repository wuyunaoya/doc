# box-shadow盒子阴影

box-shadow 属性：用于向框添加一个或多个阴影。
语法：
		**box-shadow: h-shadow v-shadow blur spread color inset;**
参数说明：
		h-shadow	 必需，水平阴影的位置，允许负值；
		v-shadow	 必需，垂直阴影的位置，允许负值；
		blur		可选，模糊距离；
		spread 	可选，阴影的尺寸；
		color  	可选，阴影的颜色；
		inset	 	可选，将外部阴影 (outset) 改为内部阴影
注：box-shadow 向框添加一个或多个阴影,由逗号分隔的阴影列表。

# text-shadow文字阴影

text-shadow 属性：用于文字添加一个或多个阴影。
语法：
		**text-shadow: h-shadow  v-shadow   blur   color;**
参数说明：
		h-shadow	 必需，水平阴影的位置，允许负值；
		v-shadow	 必需，垂直阴影的位置，允许负值；
		blur		可选，模糊距离；
		color  	可选，阴影的颜色；
注：text-shadow 向文字添加一个或多个阴影,由逗号分隔的阴影列表。

# 单行文本溢出隐藏

**overflow : hidden**     必须配合使用

**text-overflow : clip**   溢出的文本直接裁剪掉

​		  			  	**ellipsis**  溢出显示省略号 

​							string   自定义字符串（仅火狐）

white-space : nowrap   强制不换行（中文内容会换行，所以必须有）

```html
<div class="box1">
    box1box1box1box1box1box1box1box1box1box1box1box1box1box1
</div>

<div class="box2">
    box2box2box2box2box2box2box2box2box2box2box2box2box2box2
</div>

<div class="box3">
    box3box3box3box3box3box3box3box3box3box3box3box3box3box3
</div>

<div class="box4">
    中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文
</div>
```

```css
 div {
     width: 200px;
     height: 200px;
     border: 2px solid;
     float: left;
     margin: 20px;
     
     overflow: hidden; /* 必配合使用overflow属性 */
}

.box1 {
    text-overflow: clip; /* 溢出的文本直接裁剪掉 */
}

.box2 {
    text-overflow: ellipsis; /* 溢出显示省略号 */
}

.box3{
    text-overflow: "********"; /* 自定义字符串，仅火狐 */
}

.box4{
    white-space: nowrap;/*强制不换行，中文内容必须配合使用*/
    text-overflow: ellipsis;
}
```

# 多行文本溢出显示省略号

### 第一种：仅webkit

**overflow : hidden** 必须溢出隐藏

**display : -webkit-box**   将元素设置为可弹性伸缩盒子

**-webkit-box-orient : vertical**  弹性伸缩盒子内部的朝向设置成垂直

**-webkit-line-clamp : 数值**   在第几行显示省略号

**line-height： height/数值   **配合使用效果更好

```html
<div>
    中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文
    中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文
    中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文中文
</div>
```

```css
  div {
      width: 200px;
      height: 200px;
      border: 5px solid red;
      float: left;

      overflow: hidden; /* 必须隐藏  */
      display:-webkit-box;/* 将盒子设置成弹性伸缩盒子 */
      -webkit-box-orient: vertical;/*弹性伸缩盒子内部的朝向orient */
      -webkit-line-clamp:10;/* 在第几行显示省略号 */
      line-height:20px ;/* 配合使用 height/10 */
}

```

### 第二种：伪元素模拟

```html
 <div>
     内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容
     内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容
     内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容内容
</div>
```

```css
 div {
     width: 200px;
     height: 200px;
     border: 2px solid;
     
     line-height: 22px;/* 要有一个合适的行高配合行数 */
     overflow:hidden; /* 溢出的部分要隐藏 */
     
     position: relative;
}

div::after {
    content: "...";
    position: absolute;
    bottom: 0;
    right: 0;
    background-color: #fff;
    padding: 0 3px;
    letter-spacing: 1px;/* 字与字之间，字母与字母之间的空隙 */
}
```











