## 1、BOM操作

#### 1、元素宽高

```js
// jQuery可以获取隐藏元素的宽高，而原生不可以

var box = $('#box');

console.log(box.css('width')); // 100px

// 只演示了宽，高也一样

// 获取
console.log(box.width()); // 100 width
console.log(box.innerWidth()); // 120 width+padding          clientWidth
console.log(box.outerWidth()); // 122 width+padding+border   offsetWidth
console.log(box.outerWidth(true)); // 142 width+padding+border+margin

// 设置
box.width(200);
box.innerWidth(200);
box.outerWidth(200);
box.outerWidth(200, true);
```

#### 2、可视区宽高

```js
alert($(window).width())
alert($(window).height())
```

#### 3、文档宽高

```js
alert($(document).width());
alert($(document).height());
```

#### 4、原素位置

- jQuery对象.offset(); 返回一个对象，包含 left top 两个属性

```js
// jQuery对象.offset();  返回一个对象，包含 left  top 两个属性

var box3 = $('.box3');
console.log(box3.offset());

// -------------------
// 原生
console.log(getPos(box3[0]));
function getPos(ele) {
    var l = 0;
    var t = 0;
    while (ele) {
        l += ele.offsetLeft;
        t += ele.offsetTop;
        ele = ele.offsetParent;
    }
    return {
        left: l,
        top: t
    }
}
```

#### 5、滚动条

- 获取滚动的位置
  - jQuery对象.scrollTop()
  - jQuery对象.scrollLeft()

- 设置滚动的位置
  - jQuery对象.scrollTop(值)
  - jQuery对象.scrollLeft(值)

- 滚动事件
  - jQuery对象.scroll(函数);

```js
// 在窗口上滚动，获取滚动条的位置
$(window).scroll(function () {
    console.log($(window).scrollTop());
});

// 在文档上点击一下，让滚动条到500去
$(document).click(function () {
    $(window).scrollTop(500);
});
```

案例：返回顶部



## 2、DOM操作

#### 1、创建节点

- 我们只需要给$()中传入html片段，就可以创建相应的html节点。

```html
$('<p></p>').appendTo('body');
$('<p>').appendTo('body');
$('<p class="abc" id="box" style="background: red">平头哥啊</p>').appendTo('body');

$(`<div class="e_nav fl clearfix">
    <div class="e_nd">
        <a href="">首页</a>
        <em></em>
    </div>
    <div class="e_nd">
        <a href="">OAO训练营</a>
        <em></em>
    </div>
</div>`).appendTo('body');
```

#### 2、插入节点

每一种操作都有两个方法，因为后续的链式操作不同

```html
<ul>
    <li>吃饭</li>
    <li class="abc">睡觉</li>
    <li>打豆豆</li>
</ul>
```

```js
var li = $('<li>我是尹喆</li>');

// 将元素插入目标中，作为子元素，放在最后
// 元素.appendTo(目标);
// 目标.append(元素);
li.appendTo($('ul')).css('background', 'red');
$('ul').append(li).css('background', 'red');


// 将元素插入目标中，作为子元素，放在最前
// 元素.prependTo(目标);
// 目标.prepend(元素);
li.prependTo($('ul'));
$('ul').prepend(li);


// 将元素插入到目标元素的后面，作为兄弟元素
// 元素.insertAfter(目标);
// 目标.after(元素);
li.insertAfter($('.abc'));
$('.abc').after(li);


// 将元素插入到目标元素的前面，作为兄弟元素
// 元素.insertBefore(目标);
// 目标.before(元素);
li.insertBefore($('.abc'));
$('.abc').before(li);
```



#### 3、删除节点

```js
var btn = $('button');
var ul = $('.list');

ul.click(function () {
    console.log(123);
})

// jQuery对象.remove();
// 返回被删除对象的引用，如果对象之前有事件，返回的不再保留之前的事件
btn.eq(0).click(function () {
    var v = ul.remove();

    setTimeout(function () {
        v.appendTo('body');
    }, 3000);
});

// ---------------------

// jQuery对象.detach();
// 返回被删除对象的引用，如果对象之前有事件，返回的保留之前的事件
btn.eq(1).click(function () {
    var v = ul.detach();

    setTimeout(function () {
        v.appendTo('body');
    }, 3000);
});

// --------------------
// jQuery对象.empty();
// 严格来讲，不是删除，而是清空
btn.eq(2).click(function () {
    // ul.empty(); // 建议使用

    ul.html('');
});
```



#### 4、克隆节点

```js
// jQuery对象.clone(true); 参数true，就可以保留之前的事件

var btn = $('button');
var box = $('.box');

box.click(function () {
    console.log(123);
});

btn.click(function () {
    // box.clone().appendTo('body'); // 克隆之后，再添加到body中来
    box.clone(true).appendTo('body'); // 克隆之后，再添加到body中来
});
```



#### 5、替换节点

```js
// jQuery对象.replaceAll(被替换的元素);
// 被替换的元素.replaceWith(jQuery对象);

$(function () {
    var p = $('p');
    var btn = $('button');
    var div = $('div');

    // 用页面中已有的元素替换
    // btn.click(function () {
    //     // p.replaceAll(div);
    //     div.replaceWith(p); 
    // });

    // 创建一个元素来替换
    btn.click(function () {
        $('<span>平头妹</span>').replaceAll(div);
    });

})
```



## 3、jQuery中的事件

#### 1、事件对象的属性

```js
$('.box').click(function (ev) {
    console.log(ev); // jQuery包装过以后的事件对象
    console.log(ev.originalEvent); // 返回原生的事件对象

    console.log(ev.type); // 事件类型
    console.log(ev.clientX, ev.clientY); // 鼠标到可视区的距离 （常用）
    console.log(ev.pageX, ev.pageY); // 鼠标到文档的距离 （常用）
    console.log(ev.offsetX, ev.offsetY); // 鼠标到box左上角的距离 
    console.log(ev.screenX, ev.screenY); // 鼠标到屏幕的距离

    console.log(ev.which); // 相当于keyCode，但比keyCode强大，还可以记录鼠标的键值，返回1\2\3即左\中\右;
    console.log(ev.target); // 事件源
    console.log(ev.delegateTarget); // 事件绑定的对象

    console.log(ev.ctrlKey); // 返回true或false，相应的ctrl键是否按下
    console.log(ev.shiftKey); // 返回true或false，相应的shift键是否按下
    console.log(ev.altKey); // 返回true或false，相应的alt键是否按下

    ev.preventDefault(); // 阻止事件默认行为
    ev.stopPropagation(); // 阻止冒泡
    return false; // 阻止事件默认行为 + 阻止冒泡

});
```



#### 2、on的事件绑定

- 原生事件都给函数化了
- jQuery都是用addEventListener绑定的
- blur、focus、load、resize、scroll、unload、click、dblclick、mousedown、mouseup、mousemove、mouseover、mouseout、mouseenter、mouseleave、change、select、submit、keydown、keypress、keyup和error

- **jQuery对象.on(事件名, 函数);**

```js
var box = $('.box');

box.click(function () {
    console.log('点我了');
});

// 普通on的绑定
box.on('click', function () {
    console.log('执行我了');
});

// 一次绑定多个事件
box.on('click mouseover mouseout', function (ev) {
    console.log(ev.type);
});

// 写成对象的形式
box.on({
    mouseover: function () {
        $(this).css('background', 'pink');
    },
    mouseout: function () {
        $(this).css('background', 'red');
    }
});

// 执行自定义事件
box.on('abc', function () {
    console.log('abc执行了');
})
box.trigger('abc'); // 自定义事件，必须要用trigger触发
```



#### 3、取消事件

- **jQuery对象.off(事件名);** 有参数，取消对应参数的事件，没有参数，取消这个元素上所绑定的所有事件

```js
var box = $('.box');

// 一次绑定多个事件
box.on('click mouseover mouseout', function (ev) {
    console.log(ev.type);
});

// box.off('click'); // 取消了click事件
box.off(); // 取消box上面所有绑定的事件
```



#### 4、事件命名空间

```js
var box = $('.box');

// 绑定点击，打印a
box.on('click.a', function () {
    console.log('a');
});

// 绑定点击，打印b
box.on('click.b', function () {
    console.log('b');
});

box.off('click.a'); // 取消命名空间为a的事件
```



#### 5、只执行一次的事件

jQuery对象.one(事件, 函数); 只触发一次的事件

```js
var box = $('.box');

// jQuery对象.one(事件, 函数); 只触发一次的事件
// box.one('click', function () {
//     console.log('执行了');
// });

// ----------------------
box.on('click.one', function () {
    console.log('执行了');

    $(this).off('.one'); // 取消
});
```



#### 6、事件代理

- jQuery对象.on(事件, 子级, 函数)
- 函数中的this是被代理的元素

```html
<ul>
    <li class="abc">吃饭</li>
    <li class="abc">睡觉</li>
    <li class="ddd">打豆豆</li>
    <div>ppp</div>
</ul>
```

```js
$('ul').on('click', '.abc, .ddd, div', function (ev) {
    // console.log(this); // li
    // console.log(ev.target); // li
    // console.log(ev.delegateTarget); // ul
    $(this).css('background', 'red');
})
```

#### 7、合成事件

- jQuery对象.hover(滑上执行, 滑离执行); 
- 同原生的 mouseenter mouseleave

```js
$('.box').hover(function () {
    // 滑上执行
    $(this).css('background', 'blue');
    // ...
}, function () {
    // 滑离执行
    $(this).css('background', 'red');
    // ...
});
```

