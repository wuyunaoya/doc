# 多栏布局

网页在不同大小的设备上能自适应的显示

# 1、两栏自适应

```html
<div class="left">left</div>
<div class="right">
        <div class="right_inner">right</div>
</div>
```

```css
.left{
      width: 300px;
      background-color: red;
      position: absolute;
}
.right{
      width: 100%;
      background-color: blue;
}
.right_inner{
      padding-left: 300px;
      background-color:yellow;
}
```

# 2、等高布局

##### 1、margin和padding互相抵消

```html
<div class="wrap">
    <div class="box1">左</div>
    <div class="box2">中</div>
    <div class="box3">右</div>
</div>
```

```css
.wrap{
    width: 300px;
    border: 10px solid;
    overflow: hidden;
}
.wrap div{
    width: 100px;
    float: left;
    padding-bottom: 9999px;
    margin-bottom: -9999px;
}
.box1{
    background-color: red;
}
.box2{
    background-color: green;
}
.box3{
    background-color: blue;
}
```

优点：结构简单，兼容所有浏览器

缺点：伪等高，需要合理的控制margin和padding

##### 2、容器嵌套

```html
<div class="wrap1">
    <div class="wrap2">
        <div class="wrap3 clearfix">
            <div class="box1">左</div>
            <div class="box2">中</div>
            <div class="box3">右</div>
        </div>
    </div>
</div>
```

```css
.clearfix:after {
     content: "";
     display: block;
     clear: both;
}
.wrap1,.wrap2,.wrap3 {
    width: 100%;
    min-height: 100px;
}
.wrap1 {
    background-color: red;
    overflow: hidden;
}
.wrap2 {
    position: relative;
    left: 30%;
    background-color: green;
}
.wrap3 {
    position: relative;
    left: 40%;
    background-color: blue;
}

.wrap3 div {
    float: left;
}
.box1 {
    width: 30%;
    margin-left: -70%;
}
.box2 {
    width: 40%;
    margin-left: -40%;
}
.box3 {
    width: 30%;
}
```

优点：兼容各浏览器，无列数限制

缺点：结构嵌套复杂，不易于理解

# 3、圣杯布局和双飞翼布局

圣杯布局和双飞翼布局都是为了实现左右两栏固定宽度，中间部分自适应的三栏布局

1、三栏布局

2、左右两栏固定宽度

3、中间部分自适应的

![img](file:///C:\Users\IBM\AppData\Local\Temp\ksohtml9088\wps1.jpg) 

## 圣杯布局         

```html
<div id="wrap">
   <div id="center">中间</div>
   <div id="left">左边</div>
   <div id="right">右边</div>
</div>
```

1. 原布局
![图片1](images\图片1.png)

2. 浮动
![图片2](images\图片2.png)

3. margin-left把左右两个放到正确的位置
![图片3](images\图片3.png)

4. 给外套加padding，把红色区域挤到中间显示区
![图片4](images\图片4.png)

5. 用相对定位把左右两个移到padding区
![图片5](images\图片5.png)

### 双飞翼布局

```html
  <div class="wrap">
        <div class="center">
            <div class="center_inner">中间</div>
        </div>
        <div class="left">左边</div>
        <div class="right">右边</div>
    </div>
```

1. 原布局
   ![图片6](images\图片6.png) 

2. 浮动
   ![图片7](images\图片7.png)  

3. margin-left把左右两个放到正确的位置
![图片8](images\图片8.png)  

4. 给main加margin把main挤到红色
![图片9](images\图片9.png)  

# 滑动门技术

在没有圆角的时候会使用滑动门去实现圆角的设置。

**目的：**为了特殊形状的背景能够自适应元素文本内容的多少。（常用于导航栏）

**核心技术：**利用css的背景图的位置和盒子的padding值撑开宽度，以便适应不同字数的导航栏。