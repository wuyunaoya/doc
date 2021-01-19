# 一、transition过渡

### 分写

transition-property: all 默认全部属性   （过渡属性）

​					   			 width   height  color   可以单写，支持一个或多个

transition-duration: 默认0s   （过渡时间，单位：s秒、ms毫秒）

transition-timing-function: 默认ease  加速-减速

​											 	ease-in   加速

​												 ease-out    减速

​										         ease-in-out   慢速-加速-减速

​												 linear  匀速

![transtion-timing-function](图片\transtion-timing-function.png)

transition-delay: 默认0s  （过渡推迟执行的时间，单位：s秒、ms毫秒）

### 综合写法

 transition: transition-property   transition-duration  transition-timing-function   transition-delay

# 二、transform

transform 允许我们对元素进行位移、旋转、缩放或倾斜

transform : transform-functions

## 1、变形函数transform-functions

平移：translate()

旋转：rotate()

缩放：scale()

倾斜：skew()  仅2d

## 2、2D变换

### 2.1、translate() 位移

正值向右向下，负值向左向上

- translate( x , y )  水平方向和垂直方向同时移动（只写一个值代表x轴）
- translateX( x )   仅水平方向移动（X 轴移动）
- translateY( y )    仅垂直方向移动（Y 轴移动）

### 2.2、rotate() 旋转

- rotate(角度)   （ 默认以自己的中心为旋转中心）

  - 正值：顺时针

  - 负值：逆时针

### 2.3、scale() 缩放

默认值为1，0~1 缩小，1+∞放大、负数会翻转再缩放，（默认以自己的中心为缩放中心）

- scale( x , y )  水平方向和垂直方向同时缩放，（只写一个值代表x=y）

- scaleX( x )  仅水平方向（X 轴）缩放

- scaleY( y )  仅垂直方向（Y 轴）缩放
![image-20200714002715488](图片\scale.png)

### 2.4、skew() 倾斜

- skew( xdeg , y deg)  水平方向和垂直方向同时倾斜，只写一个代表x的值

- skewX( x deg)    仅水平方向（X 轴）倾斜

- skewY( ydeg )    仅垂直方向（Y 轴）倾斜

## 3、transform-origin 变形原点

transform-origin : 50%   50% （center   center）初始值

​								%          %

​								px        px

​								em       em

​							   left        top

​							  center  center

​							  right    bottom

## 4、3D变换

![3d](图片/3d.png)

- ### transform-style 如何在3d空间中呈现元素

  必须与transform一起使用，若同时设了 transform-style: preserve-3d; 和 overflow: hidden;，3D 效果将失效

  - transform-style : flat(平面) | preserve-3d 
    -  flat   子元素将不保留其 3D 位置。
    -  preserve-3d   子元素将保留其 3D 位置。

- ### perspective 视距或景深

  - perspective : px | none
    - px    眼睛距离物体的视觉距离，以像素计。
    - none 默认值，与 0 相同，不设置。

### 4.1、translate 位移

- translate3d( x , y , z ) 必须3个值

- translateX( x )   仅水平方向移动（X 轴移动）
- translateY( y )    仅垂直方向移动（Y 轴移动）
- translateZ( z )    仅垂直方向移动（Z 轴移动）（配合视距才能看出来）

### 4.2、rotate 旋转

- rotate3d（x矢量值，y矢量值，z矢量值，角度）
- rotateX( 角度 )
- rotateY( 角度 )
- rotateZ( 角度 )
  - 正值：顺时针
  - 负值：逆时针

### 4.3、scale缩放

![scale3d](图片/scale3d.png)

# 三、animation动画

### 1、自定义动画帧

 @keyframes 动画的名字{

​    	  0%{ 动画初始状态 }

​    	    。。。

   		 。。。中间状态

​     	 100%{ 动画结束状态状态  }

 }

 @keyframes 动画的名字{

​    	  from{ 动画初始状态 }

​     	 to{ 动画结束状态状态  }

 }

### 2、使用动画

**animation:**  name    duration     timing-function     delay     iteration-count     direction

**animation-name:** 动画名字（自己取的）

**animation-duration:** 动画执行之间（从初始到结束使用的时间，单位:s|ms   默认0s） 

**animation-timing-function:**  运动曲线 （默认ease）

​              							            ease 加速-减速

​                							          ease-in 加速

​             								         ease-out 减速

​                  						           ease-in-out 慢速-加速-减速

​                   						   	   linear 匀速

**animation-delay :** 动画延迟执行时间（过一段时间后才执行，单位：s|ms  默认0s）

**animation-iteration-count:**  执行次数 默认1（可以写数字，或者infinite无数次）

**animation-direction:** 是否轮流反向轮播

​										 normal  正常

​           						     alternate  奇数次从0%-100%播放动画，偶数次的时候，从100%-0%播放动画

​              						  alternate-reverse 奇数次从100%-0%播放动画，偶数次的时候，从0%-100%播放动画       

# 四、animate动画库

animate.css   css3动画库，预设了抖动（shake）、闪烁（flash）、弹跳（bounce）、翻转（flip）、旋转（rotateIn/rotateOut）、淡入淡出（fadeIn/fadeOut）等动画效果

网址：https://animate.style/ 或 https://daneden.github.io/animate.css/

### 1、引入

第一种：link引入CND地址：https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css

```html
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css">
```

第二种：在浏览器地址栏中访问CND地址

![animateCDN1](图片\animateCDN1.png)

ctrl+a 全选 -------ctrl+c复制------新建animate.min.css-----ctrl+v 粘贴到css文件里

![animateCDN2](图片\animateCDN2.png)

```html
<link rel="stylesheet" href="./css/animate.min.css">
```

### 2、使用

`<h1 class="animate__animated animate__xxx">文字文字文字文字文字文字</h1>`

```html
<h1 class="animate__animated  animate__fadeInDownBig">文字文字文字文字文字文字</h1>
<h1 class="animate__animated  animate__fadeInUp">文字文字文字文字文字文字</h1>
```





