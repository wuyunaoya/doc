## 1、移动端事件

#### 1、移动端事件

移动端常用的事件，主要有三个，分别是：

- ontouchstart(手指按下)

- ontouchmove(手指移动)

- ontouchend(手指抬起)

注意：移动端事件绑定，要用addEventListener

```js
var box = document.getElementById('box');

// 手指按下
box.addEventListener('touchstart', function () {
    console.log('touchstart');
});

// 手指移动
box.addEventListener('touchmove', function () {
    console.log('touchmove');
});

// 手指抬起
box.addEventListener('touchend', function () {
    console.log('touchend');
});
```

#### 2、移动端事件和PC端事件区别

- 1、PC端事件比移动端的慢300ms

- 2、移动端事件会有点透的问题

#### 3、移动端事件对象

移动端事件：相对于pc端事件，它多出一个关于手指的列表

- ev.touches 当前位于屏幕上的所有手指的一个列表

- ev.targetTouches：位于当前DOM元素上的手指的一个列表

- ev.changedTouches：涉及当前事件的手指的一个列表（一般使用这个）

```js
var box = document.getElementById('box');
box.addEventListener('touchstart', function (ev) {
    console.log(ev);

    // 跟PC相比较，多关于手指的列表
    console.log(ev.touches); // 当前位于屏幕上的所有手指的一个列表
    console.log(ev.targetTouches); // 位于当前DOM元素上的手指的一个列表
    console.log(ev.changedTouches); // 涉及当前事件的手指的一个列表（一般使用这个）

    var touch = ev.changedTouches[0]; // 取得这个手指信息
    console.log(touch); // 一个手指的事件对象
    console.log(touch.target); // 事件源

    console.log(touch.clientX, touch.clientY); // 手指到可视区的距离
    console.log(touch.pageX, touch.pageY); // 手指到文档的距离
    console.log(touch.screenX, touch.screenY); // 手指到屏幕的距离

    console.log(touch.radiusX, touch.radiusY); // 手指头半径
    console.log('手指的标识', touch.identifier); // 手指的标识
    console.log('压力大小', touch.force); // 压力大小
    console.log('旋转角度', touch.rotationAngle); // 旋转角度
});
```

#### 4、案例：移动端轮播图



## 2、touch.js库

#### 1、介绍

Touch.js是移动设备上的手势识别与事件库，由百度云Clouda团队维护，也是在百度内部广泛使用的开发工具

Touch.js手势库专为移动设备设计， 请在Webkit内核浏览器中使用。

下载：https://www.bootcdn.cn/touchjs

#### 2、事件绑定

格式：touch.on( element, types, callback );

- 格式：touch.on( element, types, callback );
- element：可以是元素对象，也可以是一个选择器
- types: 事件（可以是原生事件，也可以是touch封装过的事件）

```js
var box = document.getElementById('box');

touch.on(box, 'touchstart', function () {
    console.log('点击了');
});

// 同时绑定多个事件
touch.on(box, 'tap doubletap hold', function (ev) {
    console.log('执行了');
    console.log(ev.type); // 事件类型
})
```

#### 3、事件代理

- 格式：touch.on(element, types, selector, callback);

- callback中的this，即被代理的这个元素

```html
<ul>
    <li class="ab">吃饭</li>
    <li class="ab">睡觉</li>
    <li>打豆豆</li>
</ul>
```

```js
touch.on('ul', 'touchstart', 'li.ab', function () {
    // console.log(this);
    this.style.backgroundColor = 'red';
});
```

#### 4、事件对象

```js
// 不同的手势行为，事件对象信息不同
touch.on('#box', 'dragend', function (ev) {
    // console.log(ev); // 被touch包装过以后的事件对象
    // console.log(ev.originEvent); // 返回原生的事件对象

    console.log('事件的名称：' + ev.type); // 事件的名称  
    console.log('旋转角度：' + ev.rotation); // 旋转角度
    console.log('缩放比例：' + ev.scale); // 缩放比例
    console.log('操作的方向属性：' + ev.direction); // 操作的方向属性
    console.log('操作的手势数量：' + ev.fingersCount); // 操作的手势数量
    console.log('相关位置信息：', ev.position); // 相关位置信息, 不同的操作产生不同的位置信息，它是一个对象
    console.log('swipe类两点之间的位移：' + ev.distance); // swipe类两点之间的位移
    console.log('x方向的位移值：' + ev.distanceX); // x手势事件x方向的位移值, 向左移动时为负数
    console.log('y方向的位移值：' + ev.distanceY); // 手势事件y方向的位移值, 向上移动时为负数
    console.log('旋转的角度：' + ev.angle); // rotate事件触发时旋转的角度
    console.log('时间戳：' + ev.duration); // touchstart 与 touchend之间的时间戳
});
```

#### 5、手势事件

Touch.js的手势事件有很多，主要分为：缩放类、旋转类、滑动类、拖动类、长按和点击这么几类。

| 类         | 事件           | 描述         |
| ---------- | -------------- | ------------ |
| 缩放类     | pinchstart     | 缩放手势起点 |
|            | pinchend       | 缩放手势终点 |
|            | pinch          | 缩放手势     |
|            | pinchin        | 收缩         |
|            | pinchout       | 放大         |
| 旋转类     | rotateleft     | 向左旋转     |
|            | rotateright    | 向右旋转     |
|            | rotate         | 旋转         |
| 滑动类     | swipestart     | 滑动手势起点 |
|            | swiping        | 滑动中       |
|            | swipeend       | 滑动手势终点 |
|            | swipeleft      | 向左滑动     |
|            | swiperight     | 向右滑动     |
|            | swipeup        | 向上滑动     |
|            | swipedown      | 向下滑动     |
|            | swipe          | 滑动         |
| 拖动类     | dragstart      | 拖动开始     |
|            | drag           | 拖动         |
|            | dragend        | 拖动结束     |
| 长按       | hold           |              |
| 单击、双击 | tap、doubletap |              |

#### 6、案例：改进轮播图