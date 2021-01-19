BOM全称Browser Object Model - 浏览器对象模型，他提供了很多对象，用于访问浏览器的功能，没有规范，BOM的核心是window。



**window**是js中最大的对象，表示窗口，包含document

**document**文档对象，表示HTML



## 1、window对象

#### 1、window

```js
// 所有 JavaScript 全局对象、函数以及变量均自动成为 window 对象的成员。
// 全局变量是 window 对象的属性。全局函数是 window 对象的方法。

var a = 10;
function fn() {
    console.log('平头哥');
}

console.log(a);
console.log(window.a);

fn();
window.fn();

// -----------------------------------
// window是一个对象，我们就可以for-in循环它
var n = 0;
for (var attr in window) {
    n++;
    console.log(n, attr, '------', window[attr]);
}
```

- 系统对话框

```js
// alert: 只有确定按钮的弹窗，返回undefined
var n = window.alert('谁是我？');
console.log(n);

// confirm：带有确定和取消按钮的弹出窗，确定返回true，取消返回false
var n = window.confirm('吃饭不?');
console.log(n);

// prompt 带有输入框的弹出窗，确定返回输入框的值，取消返回null
var n = window.prompt('考了多少分？', 100);
console.log(n);
```

- open和close

```html
<button>打开</button>
<button>关闭</button>
```

```js
// 可以通过js的方式，打开一个页面

// 打开
// window.open(url, 打开窗口的方式, 设置窗口大小, 新窗口是否取代浏览器记录中的位置)
// 	    _self ：在当前窗口打开
// 	    _blank:在新窗口打开
// 	    返回新页面的window对象

// 关闭
// 被关闭窗口的window对象.close();  只能关闭由js打开的窗口

var btn = document.querySelectorAll('button');
var w = null; // 存储打开开新窗口的window对象

// 打开
btn[0].onclick = function () {
    w = open('https://www.baidu.com', '_blank', 'width=500px,height=300px');
}

// 关闭
btn[1].onclick = function () {
    w.close();
}
```



#### 2、location对象

```js
console.log(location === window.location); // true
console.log(location === document.location); // true
// var n = 0;
// for (var attr in location) {
//     n++;
//     console.log(n, attr, location[attr]);
// }

console.log(location.hash); // 返回#号以后的东西，包括#号 （可设置）
console.log(location.search); // 返回?号以后的东西，包括?号 （可设置）
console.log(location.host); // 返回服务器名称和端口号
console.log(location.hostname); // 返回不带端口号的服务器名称
console.log(location.href); // 返回当前加载页面的完整URL  （可设置，相当于open）
console.log(location.pathname); // 返回URL中的目录和（或）文件名  /day10/1代码/6 location.html
console.log(location.port); // 端口号
console.log(location.protocol); // 协议


// -----------------------
// 可设置的部分
location.hash = 'ddd';
location.search = 'aa=123'
setTimeout(function () {
    // location.href = 'https://www.baidu.com' // 可以实现打开新面羰
    location.reload(); // 刷新页面
}, 5000);
```

#### 3、history对象

保存着用户上网的历史记录，从窗口被打开的那一刻算起。

- history.go(-1); // 后退一页
- history.go(1); // 前进一页
- history.go(2); // 前进两页
- history.back(); // 后退
- history.forward();  // 前进

#### 4、navigator对象

navigator 对象的属性通常用于检测显示网页的浏览器类型

```js
console.log("浏览器代号: " + navigator.appCodeName);
console.log("浏览器名称: " + navigator.appName);
console.log("浏览器版本: " + navigator.appVersion);
console.log("启用Cookies: " + navigator.cookieEnabled);
console.log("硬件平台: " + navigator.platform);
console.log("用户代理: " + navigator.userAgent);
console.log("用户代理语言: " + navigator.systemLanguage);
```

## 2、位置属性

#### 1、元素宽高

- 获取元素的宽高（不能获取隐藏元素的宽高）

```js
var box = document.getElementById('box');

// box.style.width：只能得到行间的样式
// getStyle(box, 'width'); 样式宽

// 元素的宽高    高也一样，即clientHeight  offsetHeight
// 不能获取隐藏元素的宽高
console.log(box.clientWidth); // 120 width + padding
console.log(box.offsetWidth); // 122 width + padding + border
```

- 获取特殊标签

```js
console.log(document.body); // body
console.log(document.documentElement); // html
document.title = '平头哥';
```

- 获取可视区宽高 （html的宽高）

```js
alert(document.documentElement.clientWidth);
alert(document.documentElement.clientHeight);
```

- 元素上边框和左边框(用处不大)

```js
console.log(box.clientTop); // 获取元素上边边框的宽度
console.log(box.clientLeft); // 获取元素左边边框的宽度
```

#### 2、元素位置

- 元素.offsetParent: 返回元素离它最近的有定位属性的父级，如果没有定位的父级，返回body
- 元素.offsetLeft: 返回元素离它最近的有定位属性的父级的左边的距离，如果没有定位的父级，则到body的左边的距离
- 元素.offsetTop: 返回元素离它最近的有定位属性的父级的顶边的距离，如果没有定位的父级，则到body的顶边的距离

```html
<div id="box1">
    <div id="box2">
        <div id="box3"></div>
    </div>
</div>
```

```js
var box3 = document.getElementById('box3');
console.log(box3.offsetLeft);
console.log(box3.offsetParent);
```

```js
// 封装一个方法，用于获取元素到文档的距离
console.log(getPos(box3));

function getPos(ele) {
    var l = 0;
    var t = 0;

    while (ele) {
        l += ele.offsetLeft;
        t += ele.offsetTop;
        ele = ele.offsetParent;
        // console.log(ele);
    }
    return {
        left: l,
        top: t
    }
}
```

#### 3、滚动

- 获取元素的滚动条
  - 元素.scrollTop    被卷去的高
  - 元素.scrollLeft   被卷去的宽

- 设置滚动条
  - 元素.scrollTop = 值
  - 元素.scrollLeft = 值

- 滚动事件(在滚动的时候，会不断的触发)
  - 元素.onscroll = function(){}

- 窗口的滚动条
  - 标准浏览器认为是滚动条的高度是html的，而谷歌认为是body的（新版谷歌也认为是html的），所以要做兼容
  - console.log(document.documentElement.scrollTop);
  - console.log(document.body.scrollTop);

```js
// 在页面中滚动时，打出它的滚动条的高度
window.onscroll = function () {
    var scrollTop = document.documentElement.scrollTop || document.body.scrollTop;
    console.log(scrollTop);
}

// 在页面中点击一下，让滚动条到500
document.onclick = function () {
    document.documentElement.scrollTop = 500;
    document.body.scrollTop = 500;
}
```

案例：返回顶部

#### 4、总结

```js
// client系列
// 元素.clientWidth         width + padding    （可视区的宽高）
// 元素.clientHeight        height + padding
// 元素.clientTop           上边框的高度（不常用）
// 元素.clientLeft          左边框的宽度

// offset系列
// 元素.offsetWidth         width + padding + border
// 元素.offsetHeight        height + padding + border
// 元素.offsetParent        有定位的父级
// 元素.offsetTop           到有定位父级顶边的距离
// 元素.offsetLeft          到有定位父级左边的距离


// scroll系列
// 元素.scrollWidth         元素实际宽
// 元素.scrollHiehgt        元素实际高
// 元素.scrollTop           被卷去的高
// 元素.scrollLeft          被卷去的宽
```



## 3、懒加载

先只加载可视窗口区域的图片，当用户向下拖动滚动条时再继续加载后面的图片（也是只加载目前可视窗口区域内的图片）。

1、这样减少了加载时的线程数量，使可视区域内的图片也能够快速加载，优化了用户体验。

2、减少了同一时间发向服务器的请求数，服务器压力剧减。

方法：在写网页<img>标签时并不会将图片的路径放入src属性。而是自定义一个其他的属性_src。将路径放入这个自定义的属性中。那么在加载页面时，这个图片一开始是无法加载的。而当浏览器的可视区域移动到此图片上时，将_src中的路径赋值给src属性，并开始加载。



**resize事件**

```js
// resize: 可视区的大小发生变化时触发的事件
window.onresize = function () {
    var clientW = document.documentElement.clientWidth;
    var clientH = document.documentElement.clientHeight;
    console.log(clientW, clientH);
}
```

