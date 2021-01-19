## 1、事件基础

**事件**是可以被 javaScript 侦测到的行为。 网页中的每个元素都可以产生某些可以触发javaScript函数的事件。比方说，我们可以在用户点击某按钮时产生一个 onclick 事件来触发某个函数。

#### 1、事件函数

事件函数：被事件触发的才是事件函数

```js
var box = document.getElementById('box');
function fn() { }

// 点击调用
box.onclick = fn; // fn就是事件函数

// 普通调用
fn(); // fn不是事件函数

box.onclick = function () { // 事件函数
    fn(); // 普通函数
}
```

#### 2、事件对象

**事件对象**：事件对象：一个事件发生时，与这个事件有关的详细信息保存在一个对象中，这个对象我们称为事件对象

- 事件对象存在哪里？IE和谷歌认为是全局的event对象，而其它标准浏览器认为是事件函数的第一个参数
- 兼容：var ev = ev || event;

```js
var box = document.getElementById('box');

box.onclick = function (ev) {
    // console.log(event); // IE和谷歌
    // console.log(ev); // 标准浏览器
    var ev = ev || event; // 事件对象兼容
    // console.log(ev);

    // --------------------------------------
    // 事件对象的属性
    console.log(ev.type); // 事件类型
    // console.log(ev.target); // 事件目标，IE8及以下不支持
    // console.log(ev.srcElement); // 事件目标，IE8及以下支持
    var target = ev.target || ev.srcElement; // 事件目标兼容
    console.log(target);

    console.log(ev.clientX, ev.clientY); // 鼠标到可视区的距离
    console.log(ev.pageX, ev.pageY); // 鼠标到文档的距离

    console.log(ev.shiftKey); // 事件发生时，shift键是否按下
    console.log(ev.altKey); // 事件发生时，alt键是否按下
    console.log(ev.ctrlKey); // 事件发生时，ctrl键是否按下

}
```

## 2、事件的绑定和取消

**需求：给box的点击事件同时绑定两个函数**

```js
var box = document.getElementById('box');
function fn1() {
    console.log(1);
    console.log(this === window);
}
function fn2() {
    console.log(2);
}
```

```js
// 后面的会覆盖前面的
box.onclick = fn1;
box.onclick = fn2;
```

```js
// 元素.addEventListener(不要on的事件, 函数, 是否捕获);
// IE8及以下不支持
box.addEventListener('click', fn1, false);
box.addEventListener('click', fn2, false);
```

```js
// 元素.attachEvent(要on的事件, 函数);
// IE8及以下支持
box.attachEvent('onclick', fn1);
box.attachEvent('onclick', fn2);
```

```js
// 标准的和IE的区别：
1、标准的有捕获，而IE的只有冒泡
2、标准的事件名没有on，而IE的有on
3、标准的执行顺序是正序，而IE执行顺序是倒序
4、标准执行的函数中的this是触发这个事件的元素，而IE执行函数中的this是window
```

```js
// 兼容原理，标准浏览器下返回函数，在IE8及以下返回undefined
console.log(box.addEventListener);
if (box.addEventListener) {
    // 标准浏览器
    box.addEventListener('click', fn1, false);
    box.addEventListener('click', fn2, false);
} else {
    // IE8及以下
    box.attachEvent('onclick', fn1);
    box.attachEvent('onclick', fn2);
}
```

```js
// 封装: 元素 事件 函数
function bind(ele, event, callback) {
    if (ele.addEventListener) {
        // 标准浏览器
        ele.addEventListener(event, callback, false);
    } else {
        // IE8及以下
        ele.attachEvent('on' + event, callback);
    }
}

bind(box, 'click', fn1);
bind(box, 'click', fn2);
```



**事件的取消：**

```js
// 这种写法是一种赋值的写法，后面的会覆盖前面的
box.onclick = fn1;
box.onclick = fn2;
box.onclick = null; // 取消
```

```js
// 元素.addEventListener(不要on的事件, 函数, 是否捕获);
// 元素.removeEventListener(不要on的事件, 函数, 是否捕获);

// IE8及以下不支持
box.addEventListener('click', fn1, false);
box.addEventListener('click', fn2, false);
box.removeEventListener('click', fn1, false); // 取消
```

```js
// 元素.attachEvent(要on的事件, 函数);
// 元素.detachEvent(要on的事件, 函数);

// IE8及以下支持
box.attachEvent('onclick', fn1);
box.attachEvent('onclick', fn2);
box.detachEvent('onclick', fn1); // 取消
```

```js
// ----------------------------------
// 兼容原理，标准浏览器下返回函数，在IE8及以下返回undefined
console.log(box.removeEventListener);

// ------------------------------
// 事件绑定封装: 元素 事件 函数
function bind(ele, event, callback) {
    if (ele.addEventListener) {
        // 标准浏览器
        ele.addEventListener(event, callback, false);
    } else {
        // IE8及以下
        ele.attachEvent('on' + event, callback);
    }
}
// 事件取消封装: 元素 事件 函数
function unbind(ele, event, callback) {
    if (ele.removeEventListener) {
        // 标准浏览器
        ele.removeEventListener(event, callback, false);
    } else {
        // IE8及以下
        ele.detachEvent('on' + event, callback);
    }
}

bind(box, 'click', fn1);
bind(box, 'click', fn2);
unbind(box, 'click', fn1); // 取消
```

## 3、DOM事件流

#### 1、事件流

事件流有三个阶段

- 1、捕获阶段：从外面不具体的元素到具体的元素：document - html - body - box1 - box2 - box3
- 2、处于目标阶段
- 3、冒泡阶段：从最具体的元素到最不具体的元素：box3 - box2 - box1 - body - html - document

注意：事件流经过每个节点，如果节点上面绑定着有对应的事件，这个事件就会被触发



addEventListener  第三个参数：true，则在捕获阶段触发，如果为false，则在冒泡阶段触发

注意：冒泡是默认存在的

![](D:\1009\day11\2笔记\事件流.jpg)

```html
<div id="box1">
    <div id="box2">
        <div id="box3"></div>
    </div>
</div>
```

```js
var box1 = document.getElementById('box1');
var box2 = document.getElementById('box2');
var box3 = document.getElementById('box3');
function fn() {
    console.log(this.id);
}

// 事件流有三个阶段
// 1、捕获阶段：从外面不具体的元素到具体的元素：document - html - body - box1 - box2 - box3
// 2、处于目标阶段
// 3、冒泡阶段：从最具体的元素到最不具体的元素：box3 - box2 - box1 - body - html - document
// 事件流经过每个节点，如果节点上面绑定着有对应的事件，这个事件就会被触发

// 第三个参数：true，则在捕获阶段触发，如果为false，则在冒泡阶段触发
// 冒泡是默认存在的

box1.addEventListener('click', fn, false);
box2.addEventListener('click', fn, false);
box3.addEventListener('click', fn, false);

box1.addEventListener('click', fn, true);
```





#### 2、阻止事件冒泡

- 标准浏览器：ev.stopPropagation();
- IE浏览器：ev.cancelBubble = true;

**二级菜单**

```js
var btn = document.getElementById('btn');
var box = document.getElementById('box');

// 点击按钮，box显示
btn.onclick = function (ev) {
    var ev = ev || event;
    stopPropagation(ev);
    box.style.display = 'block';
}

// 点击页面的其它地方，box隐藏
document.onclick = function () {
    box.style.display = 'none';
}

function stopPropagation(ev) {
    if (ev.stopPropagation) {
        // 标准浏览器
        ev.stopPropagation();
    } else {
        // IE8及以下
        ev.cancelBubble = true;
    }
}
```



## 4、事件的默认行为

**事件的默认行为**，即赋予了元素特殊的操作，如点击链接会跳转到其他的网页，在浏览器中右击鼠标会弹出菜单，当我们不需要这些默认行为的时候，可以手动阻止

- 标准：ev.preventDefault();
- IE8及以下：ev.returnValue = false;
- 或者：return false;

```js
var a = document.querySelector('a');

a.onclick = function (ev) {
    var ev = ev || event;
    preventDefault(ev);
}

function preventDefault(ev) {
    if (ev.preventDefault) {
        // 标准浏览器
        ev.preventDefault();
    } else {
        // IE8及以下
        ev.returnValue = false;
    }
}
```

案例：自定义右键菜单



## 5、键盘事件

- keydown : 键盘按下
- keyup ：键盘抬起
- input ： 只要内容发生变化就会触发

键盘事件只能加给能响应键盘输入的元素，能响应键盘输入的元素有：input textarea document...

```js
var input = document.querySelector('input');

// 按下 按着键不动，会一直触发
input.onkeydown = function () {
    console.log(this.value);
}

// 抬起，按着不动，只在抬起的时候会执行一次
input.onkeyup = function () {
    console.log(this.value);
}

// 只要内容发生变化就会触发  (结合上面两个的优点，IE8及以下不支持)
input.oninput = function () {
    console.log(this.value);
}

// ----------------------------------
// 键盘事件的事件对象
input.onkeydown = function (ev) {
    var ev = ev || event;

    console.log(ev.key); // 具体的按键(IE8及以下不支持)
    console.log(ev.keyCode);
    // a:65  z:90  回车:13  esc:27  空格:32  左键：37 上键：38 右键：39 下键：40
}
```

案例：方向键控制div的移动



## 6、滚轮事件

**滚轮事件和滚轮方向**

```js
// 谷歌和IE：
// 事件：mousewheel
// 方向：ev.wheelDelta  上120 下-120
box.onmousewheel = function (ev) {
    var ev = ev || event;
    console.log(ev.wheelDelta);
}

// 火狐：DOMMouseScroll  而且必须用addEventListener绑定
// 方向：ev.detail  上-3 下3
box.addEventListener('DOMMouseScroll', function (ev) {
    console.log(ev.detail);
});
```

**滚轮方向兼容**

```js
// 谷歌和IE：
// 事件：mousewheel
// 方向：ev.wheelDelta  上120 下-120
box.onmousewheel = function (ev) {
    var ev = ev || event;
    console.log(wheelDelta(ev));
}

// 火狐：DOMMouseScroll  而且必须用addEventListener绑定
// 方向：ev.detail  上-3 下3
box.addEventListener('DOMMouseScroll', function (ev) {
    console.log(wheelDelta(ev));
});

// 滚轮方向的封装：上120 下-120
function wheelDelta(ev) {
    if (ev.wheelDelta) {
        // 谷歌和IE
        return ev.wheelDelta;
    } else {
        // 火狐
        return -ev.detail * 40;
    }
}
```

完整案例实现

```js
var box = document.getElementById('box');
var h = box.clientHeight; // 取得盒子的高度

function fn(ev) {
    var ev = ev || event;
    if (wheelDelta(ev) > 0) {
        // 向上
        h--;
    } else {
        // 向下
        h++;
    }
    box.style.height = h + 'px';
}

bind(box, 'mousewheel', fn); // 谷歌和ie
bind(box, 'DOMMouseScroll', fn); // 火狐

// 滚轮方向的封装：上120 下-120
function wheelDelta(ev) {
    if (ev.wheelDelta) {
        // 谷歌和IE
        return ev.wheelDelta;
    } else {
        // 火狐
        return -ev.detail * 40;
    }
}

// 封装: 元素 事件 函数
function bind(ele, event, callback) {
    if (ele.addEventListener) {
        // 标准浏览器
        ele.addEventListener(event, callback, false);
    } else {
        // IE8及以下
        ele.attachEvent('on' + event, callback);
    }
}
```



## 7、事件委托

**什么叫事件委托**？它还有一个名字叫事件代理，从JavaScript高级程序设计上讲：事件委托就是利用事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件。

**事件委托原理**：利用冒泡的原理，把事件加给父级，在触发事件时，找到事件源，判断事件源，做相应的操作

```html
<ul>
    <li>吃饭</li>
    <li>睡觉</li>
    <li>打豆豆</li>
</ul>
```

```js
// 点击li，给li加上背景
var txt = document.getElementById('txt');
var btn = document.getElementById('btn');

var ul = document.getElementById('list');
var li = ul.getElementsByTagName('li');

// 1、传统方法
// 给多个元素绑定，耗性能
// 新添加的元素，没有之前的事件
// for (var i = 0; i < li.length; i++) {
//     li[i].onclick = function () {
//         this.style.backgroundColor = 'red';
//     }
// }

// -------------------------
// 2、事件代理
// 只给父级绑定，提高性能
// 新添加的元素，也有之前的事件
ul.onclick = function (ev) {
    var ev = ev || event; // 事件对象
    var target = ev.target || ev.srcElement; // 事件源

    if (target.nodeName === 'LI') {
        target.style.background = 'yellow';
    }
}

// 添加元素
btn.onclick = function () {
    var val = txt.value; // 用户输入
    var li = document.createElement('li');
    li.innerText = val;
    ul.appendChild(li);
}
```







