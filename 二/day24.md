## 1、jQuery插件的编写

官网地址：http://plugins.jquery.com

虽然jQuery很强大，但是有些方法还是没有给我们封装，所以我们要自己实现。为了公用，我们会把它做成插件的形式。

**插件**：本身我们不直接对jQuery代码进行操作，而是间接和对jQuery代码进行修改。

插件分为**类级插件**和**对象级插件**

```js
// 类级插件
// jQuery对象可以使用，原生对象也可以使用
// 扩展在$下面
// $.each()  $.map()  $.ajax()
; (function ($) {
    $.extend({
        插件名1: function () { },
        插件名2: function () { }
    });
})(jQuery);
// 调用：$.插件名1()
```

```js
// 对象级插件
// 只能jQuery对象使用
// 扩展在$.fn下面
// jQuery对象.css()   jQuery对象.html()
; (function ($) {
    $.fn.extend({
        插件名1: function () { },
        插件名2: function () { }
    });
})(jQuery);
// 调用：jQuery对象.插件名1()
```

**插件的基本要点**

1、jQuery插件的文件名推荐命名为jquery.[插件名].js，以免和其他javascript库插件混淆。

2、所有的对象方法都应当附加到jQuery.fn对象上，而所有的全局函数都应当附加到jQuery对象本身上。

3、在插件内部，this指向的是当前通过选择器获取的jQuery对象，而不像一般的方法那样，例如click()，内部的this指向的是DOM元素。

4、可以通过this.each来遍历所有元素。

5、所有的方法或函数插件，都应当以分号结尾，否则压缩的时候可能出现问题，为了更稳妥些，甚至可以在插件头部先加上一个分号，以免他人的不规范代码给插件带来影响。

6、插件应该返回一个jQuery对象，以保证插件的可链式操作，除非插件需要返回的是一些需要获取的量，例如字符串或者数组等。

7、避免在插件内部使用$作为jQuery对象的别名，而应该使用完整的jQuery表示。这样可以避免冲突。当然，也可以利用闭包这种技巧来回避这个问题，使插件内部继续使用$作为jQuery的别名。很多插件都是这样做的。

#### 1、封装类级插件

```js
; (function ($) {
    $.extend({
        // 去左空格
        leftTrim: function (str) {
            var re = /^\s+/;
            return str.replace(re, '');
        },
        // 去右空格
        rightTrim: function (str) {
            var re = /\s+$/;
            return str.replace(re, '');
        }
    });
})(jQuery);
```

```js
var str = '    老王    ';
console.log($.leftTrim(str)); // '老王    '
console.log($.rightTrim(str)); // '    老王'
```

#### 2、封装对象级插件

```js
; (function ($) {
    $.fn.extend({
        color: function (val) {
            // console.log(this); // $('li')
            if (typeof val === 'undefined') {
                // 获取
                return this.eq(0).css('color');
            } else {
                // 设置
                this.css('color', val);
                return this;
            }
        }
    });
})(jQuery);
```

```js
<ul>
    <li>吃饭</li>
    <li>睡觉</li>
    <li>打豆豆</li>
</ul>

$(function () {
    // 所有的li颜色变为红色（设置）
    $('li').color('red').css('font-size', 50);

    // 获取第一个li的的颜色（获取）
    console.log($('li').color());
})
```

## 2、Zepto.js

Zepto是移动端开发框架,是jQuery的轻量级代替品；API及语句同jQuery相似，但文件更小(可压缩至8KB)。是目前功能完备的库中最小的一个。随着移动端的愈加火爆，目前很多HTML5的框架都在支持移动方向，Zepto就是jQuery的移动端版本, 可以看做是一个轻量级的jQuery。如果你会用jQuery，那么你也会用Zepto，Zepto的设计目的是提供 jQuery 的类似的API，但并不是100%覆盖 jQuery 。Zepto有一个5-10k的通用库、下载并快速执行、有一个熟悉通用的API，所以你能把你主要的精力放到应用开发上。

Zepto.js 中文文档：https://zeptojs.bootcss.com/

#### 1、Zepto.js 特点

- 针对的是移动端

- 轻量级，压缩版本只有8KB

- 语法大部分同jQuery一样，学习成本低，上手快，响应，执行快，同jQuery一样以$作为核心函数和核心对象

#### 2、jQuery和Zepto的区别在哪里

- jQuery更多是在PC端被应用，因此，考虑了很多低级浏览器的的兼容性问题；而Zepto.js则是直接抛弃了低级浏览器的适配问题，显得很轻盈；
- Zepto.js在移动端被运用的更加广泛；
- jQuery的底层是通过DOM来实现效果的，Zepto.js 是用css3 来实现的；
- Zepto.js可以说是轻量级版本的jQuery。
- 需要注意的是 Zepto 的一些可选功能是专门针对移动端浏览器的； 因为它的最初目标在移动端提供一个精简的类似 jQuery 的工具库。
- 总之，Zepto 希望在所有的现代浏览器中作为一种基础环境来使用。 Zepto 不支持旧版本的 Internet Explorer浏览器(<10)。

#### 3、使用

```html
<!-- 引入库文件，这里引入基础库和touch -->
<script src="js/zepto.js"></script>
<script src="js/touch.js"></script>
```

```js
$(function () {
    $('#box').on('tap', function () {
        console.log('点了我');
    })

    $('#box').tap(function () {
        console.log('再次点了我');
    });
})
```

#### 4、和jquery不一样的使用

- 1、不能获取隐藏元素的宽高
  - jQuery可以获取隐藏元素的宽高，Zepto无法获取隐藏元素宽高。



- 2、offset()的返回值
  - jQuery返回的包知top和left。而Zepto返回的还包括width和height。

 

- 3、获取元素宽高的方法width()、height()
  
- Zepto的width()、height()是根据盒模型决定的，包含padding和border的值。Zepto中没有innerWidth()和outerWidth()系列。
  
- 4、touch事件

  ```html
  <script src="js/zepto.js"></script>
  <script src="js/touch.js"></script>
  ```

  ```js
  var box = $('#box');
  
  // 单击
  box.on('tap', function () {
      console.log('tap');
  })
  
  // 单击  singleTap和doubleTap   这一对事件可以用来检测元素上的单击和双击。(如果你不需要检测单击、双击，使用 tap 代替)
  box.on('singleTap', function () {
      console.log('singleTap');
  })
  
  // 双击
  box.on('doubleTap', function () {
      console.log('doubleTap');
  })
  
  // 长按 （当一个元素被按住超过750ms触发）
  box.on('longTap', function () {
      console.log('longTap');
  })
  
  // 滑动
  box.on('swipe', function () {
      console.log('swipe');
  })
  
  // 左滑
  box.on('swipeLeft', function () {
      console.log('swipeLeft');
  })
  
  // 右滑
  box.on('swipeRight', function () {
      console.log('swipeRight');
  })
  
  // 上滑
  box.on('swipeUp', function () {
      console.log('swipeUp');
  })
  
  // 下滑
  box.on('swipeDown', function () {
      console.log('swipeDown');
  })
  ```
  
  

