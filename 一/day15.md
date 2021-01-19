# 一、移动端常用浏览器及其内核

UC浏览器、QQ浏览器、百度手机浏览器、360浏览器、搜狗浏览器、猎豹浏览器、Chrome浏览器、Firefox 浏览器、opera 浏览器

内核为webkit内核，都是在webkit内核的基础上做的二次开发

# 二、移动端视口

布局视口-----用来显示页面的区域,。在移动端里，viewport的默认大小就是它的布局视口（pc端是浏览器窗口）

视觉视口-----用户能看到的区域，移动端屏幕宽度（pc端是浏览器器窗口）

理想视口-----让viewport的width=device-width

# 三、viewport

移动端刚兴起时，没有专门针对移动端的页面，一个pc网页要放到一个移动端里，页面会乱掉。所有就有了虚拟viewport，这是个虚拟的布局视口，默认为980px(不同设备不一样)

**作用：** 它允许开发者去创建一个虚拟窗口，窗口可以有大小设置及伸缩功能

**不同设备的默认viewport大小：**

![viewport](图片/viewport.png)



快捷键：meta:vp

```html
<meta name="viewport"  content="width=device-width,initial-scale=1.0,maximum-scale=1.0,minimum-scale,user-scalable=no">
```

width=device-width  让虚拟窗口等于设备宽

initial-scale=1.0 初始缩放比例

user-scalable=no  不允许用户缩放  默认yes允许

maximum-scale=1.0 允许用户缩放的最大比例

minimum-scale=1.0 允许用户缩放的最小比例

# 四、固定布局

把viewport设置好，跟pc端一样，设想整个网页的宽度为320px居中即可，超出部分留白

优点：思路沿用PC端，上手简单。

缺点：大屏幕手机及手机横屏时，两边是留白较大，且大屏幕手机下看起来页面会特别小，操作的按钮也很小，用户体验较差

# 五、流式布局

流式布局——宽度自适应

高度固定，宽度使用%代替px，使用弹性布局、浮动、定位等技术综合，去创建可扩展的流式布局

优点：可以很好的解决自适应需求

缺点：随着浏览器宽度的变化，盒子会被拉伸，实际效果不协调。设计存在局限性

# 六、rem 布局

rem 相对于html的font-size的大小的单位（css3）

1rem等于html的font-size

优点：在不同屏上,只要我们动态的算出html的font-size大小,则可起到一改俱改的效果,实现等比例放大缩小

缺点：我们需要js代码动态的获取设备的宽度然后给html的font-size赋值，实现自适应

![rem](图片\rem.png)

# 七、vw适配

vw——viewport's width   css3规范中的视口单位

vh——viewport's height  

vw和vh都是将屏幕分成100份，100vw=屏幕宽度，100vh=屏幕高度

当设计稿是750px时，100vw=750px，1px=100/750=0.133333vw，那么100px*100px 的盒子，可以写为:

```css
div{
    width:12.33vw;
    height:12.33vw
}
```

**基准值：psd稿**   750px      750px=100vw ====》7.5px=1vw ====》1px=0.13333vw

​												10px *10px 的盒子====》 1.3333vw * 1.3333vh

​												50px * 50px 的盒子====》0.13333*50vw *  0.13333*50vh 

## vw+rem

使用vw的时候，比较难以计算。rem又需要动态的获取浏览器的宽度。我们发现，100vw就是浏览器的宽度，所以可以将二者结合起来，通过vw来设置html的fontsize值

基准值：psd稿宽 750px=100vw ===>100px=13.333vw

​			    font-size: 100px 即font-size: 13.3333vw

# 八、媒体查询

根据设备显示器的特性为它设置css样式

媒体查询可以检测的内容：viewport的宽高。设备的宽度和高度、设备的方向、分辨率

### 1、在样式表中引入

@media  mediaType  and  (media feature)  and  (media feature){

​		选择器{

​			

​		}

}

- mediaType  设备类型：
  - all
  - print 
  - screen 智能设备屏幕  
  - speech 屏幕阅读器

- media fearture 媒体特性表达式
  - width 浏览器宽度              height浏览器高度
  - max-width  最大宽度        max-height  最大高度 
  - min-width 最下小宽度      min-height  最下高度  
  - device-width 设备宽度     device-height  设备高
  - max-device-width 最大设备宽    max-device-height 最大设备高
  - min-device-width 最小设备宽     min-device-height 最小设备高
  - orientation  设备方向 （  landscape横屏   portrait竖屏）
  - aspect-ratio  可见宽度和高度的比例  （例如：1/4）
  - device-aspect-ratio   输出设备的屏幕可见宽度和高度的比例

```css
/*大于等于1024px*/
@media screen and (min-width:1024px){
     body{
         background-color: red;
     }
} 
/*小于等于1024px,大于等于768px*/
@media screen and (max-width:1024px) and (min-width:768px){
    body{
        background-color: orange;
    }
}
/*小于等于768*/
@media screen and (max-width: 768px){
    body{
        background-color: yellow;
    }
}
```

```css
/*横屏*/
@media screen and (orientation: landscape ){
    body{
        background-color: pink;  
    }
}
/*竖屏*/
@media screen and (orientation: portrait ){
    body{
        background-color: red;  
    }
}
/*宽高比例*/
@media screen and (aspect-ratio:1/2){
    body{
        background-color: green;  
    }
}
```

# 九、 写移动端项目的步骤

  1、建好文件夹

  2、设置好viewport

  3、引入reset.css

  4、引入remScale.js

  5、去ps里量psd稿子上的尺寸，把量出来的尺寸除以100，然后把px换成rem

  6、其他的跟pc端一样操作

  7、注意：1px的边框，就不要使用rem了，用px







