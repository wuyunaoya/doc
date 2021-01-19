# 移动端布局方案flexible.js

**flexible.js** 来自手机淘宝团队，用来解决 H5 页面终端适配的（remScale没有考虑到ios和Android的问题）

由于 viewport 单位得到众多浏览器的兼容，flexible 这个过渡方案已经被弃用

### 原理：

- 动态改变viewport设置（获取了屏幕的宽度）
- 动态设置DPR=物理像素/逻辑像素（获取设备像素比）
- 动态设置html字体font-size

flexible 将设备宽度（psd稿）划分成100份，把其中的10份设置成html的font-size

**psd稿：**宽750px ===>flexible会自动设置 html { font-size:75px }

​				75 px=1 rem ===> 1px= （1/75） rem -------------**px和rem的换算率**

​				100px * 100px 的盒子===》100*（1/75）rem  *   100*（1/75）rem 

**psd稿 ：**宽640px ===>flexible 会自动设置 html{ font-size:64px }

​				64px=1rem ===> 1px=（1/64）rem -------------**px和rem的换算率**

​				100px * 100px的盒子===》100*（1/64）rem * 100（1/64）rem

**我们需要做的事：**根据psd稿的宽，得到px和rem的换算率，然后将从ps里量的尺寸换算成rem去写页面				

### 使用：

**1、引入**

```html
<script src="http://g.tbcdn.cn/mtb/lib-flexible/0.3.4/??flexible_css.js,flexible.js"></script>
```

**2、根据psd稿的宽，得到px和rem的换算率**

**3、在ps中测量元素尺寸**

​		将px转换成rem

**4、找一个可以自动将px换算rem的vscode扩展**

  （px to rem ）（cssrem）

换算率设置：设置----搜索rem---找到对应的扩展，手动改变root的font-size

