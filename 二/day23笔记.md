## 1、jQuery中的动画

#### 1、显示与隐藏

显示与隐藏：**宽、高、透明度**同时发生变化

- jQuery对象.show(speed, easing, callback); 显示
- jQuery对象.hide(speed, easing, callback); 隐藏
- jQuery对象.toggle(speed, easing, callback); 开关效果

**参数**

- speed: 速度、时间（number(单位是毫秒)  fast(200ms) normal(400ms) slow(600ms)）。如果不写，默认为0
- easing：运动的形式  "swing" - 慢快慢(默认)   "linear" - 匀速移动
- callback：回调(函数中的this，就是指这个运动的元素)  一件事做完了，下面跟着要做的事

**注意：**显示与隐藏，我们一般都不加参数，仅仅作为元素的显示或隐藏

```html
<button>show</button>
<button>hide</button>
<button>toggle</button>
<div id="box"></div>
```

```js
var btn = $('button');
var box = $('#box');

// 显示
btn.eq(0).click(function () {
    box.show(3000, 'linear', function () {
        console.log('我显示了');
    });
});

// 隐藏
btn.eq(1).click(function () {
    box.hide(3000, 'linear', function () {
        console.log('我隐藏了');
    });
});

// 切换
btn.eq(2).click(function () {
    box.toggle(3000, 'linear', function () {
        console.log('我切换了');
    });
});
```



#### 2、改变透明度

- jQuery对象.fadeIn(speed, easing, callback); 显示
- jQuery对象.fadeOut(speed, easing, callback); 隐藏
- jQuery对象.fadeTo(speed, 透明度, easing, callback); 透明到多少
- jQuery对象.fadeToggle(speed, easing, callback); 切换

注意：speed: 如果不写，默认为400ms

```html
<button>fadeIn</button>
<button>fadeOut</button>
<button>fadeTo</button>
<button>fadeToggle</button>
<div id="box"></div>
```

```js
var btn = $('button');
var box = $('#box');

// 显示
btn.eq(0).click(function () {
    box.fadeIn(3000);
});

// 隐藏
btn.eq(1).click(function () {
    box.fadeOut(3000);
});

// 透明到多少
btn.eq(2).click(function () {
    box.fadeTo(3000, 0.5);
});

// 切换
btn.eq(3).click(function () {
    box.fadeToggle(3000);
});
```

#### 3、改变高度

- jQuery对象.slideDown(speed, easing, callback); 显示
- jQuery对象.slideUp(speed, easing, callback); 隐藏
- jQuery对象.slideToggle(speed, easing, callback); 切换

```html
<button>slideDown</button>
<button>slideUp</button>
<button>slideToggle</button>
<div id="box"></div>
```

```js
var btn = $('button');
var box = $('#box');

// 显示
btn.eq(0).click(function () {
    box.slideDown(3000);
});

// 隐藏
btn.eq(1).click(function () {
    box.slideUp(3000);
});

// 切换
btn.eq(2).click(function () {
    box.slideToggle(3000);
});
```

#### 4、自定义运动

- jQuery对象.animate({动画的参数}, 时间, 运动形式, 回调);
  -  第一个参数 : 运动的值和属性 {width: 300, height: 300}
  -  第二个参数 : 时间(运动的快慢) 默认 : 400
  -  第三个参数 : 运动形式，两种运动形式( 默认 : swing(慢快慢) linear(匀速) )
  -  第四个参数 : 回调函数

```js
// 同时运动多个值
$('#box').click(function () {
    $(this).animate({
        width: 300,
        height: 300,
        left: 500
    }, 3000, 'linear', function () {
        console.log(this); // box
        console.log('我运动完成了');
    })
})

// ------------------------------

// 累加累减
$('#box').click(function () {
    $(this).animate({
        left: '+=50'
    })
})

// ---------------------------
// 链式运动
$('#box').click(function () {
    $(this)
        .animate({ width: 300 }, 3000)
        .animate({ height: 300 }, 3000)
        .animate({ left: 300 }, 3000)
        .animate({ top: 300 }, 3000)
        .animate({ opacity: 0.5 }, 3000);
});

// -------------------------

// 动画队列：
// 需求：元素宽运动到了500后，再把元素背景变成黄色，然后高再到500
$('#box').click(function () {
    $(this)
        .animate({ width: 500 }, 3000)
        .css('background', 'yellow'); // 这样不受运动队列管控，因为css不是动画
});

// 方式一：
$('#box').click(function () {
    $(this)
        .animate({ width: 500 }, 3000)
        .queue(function (next) { // queue可以将参数函数加入到队列
            $(this).css('background', 'yellow');
            next(); // queue的函数有一个next参数，即执行动画队列后面的动画
        })
        .animate({ height: 500 }, 3000)
});

// ---------------------
// 方式二：回调函数
$('#box').click(function () {
    $(this)
        .animate({ width: 500 }, 3000, function () {
            $(this).css('background', 'pink');
        })
        .animate({ height: 500 }, 3000)
});
```



#### 5、是否处于动画状态

- jQuery对象.is(':animated')  如果元素正在做运动，返回真，否则返回假

```html
<button>按钮</button>
<div id="box"></div>
```

```js
$('#box').click(function () {
    $(this).animate({
        left: 500
    }, 5000);
});

$('button').click(function () {
    console.log($('#box').is(':animated'));
});
```



#### 6、延迟动画

- jQuery对象.delay(时间);  即动画停顿多长时间，单位毫秒

```js
$('#box').click(function () {
    $(this)
        .animate({ width: 300 }, 3000)
        .delay(3000) // 延迟动画
        .animate({ height: 300 }, 3000);
});
```

#### 7、停止运动

- jQuery对象.stop(clearQueue, gotoEnd);
  - clearQueue：代表是否要清空未执行完的动画队列，默认false。
  - gotoEnd：代表是否直接将正在执行的动画跳转到末状态，默认false。

- jQuery对象.finish(); 所有动画都到未状态

```js
var btn = $('button');
var box = $('#box');

box.click(function () {
    $(this)
        .animate({ width: 300 }, 3000)
        .animate({ height: 300 }, 3000);
});

// 停止
btn.click(function () {
    // box.stop(); // 停止当前的运动，继续执行后续的运动
    // box.stop(true); // 停止当前的运动，清空后续运动
    // box.stop(true, true); // 当前动画跳转到未状态，清空后续的动画

    box.finish(); // 所有的动画到未状态
});
```







## 2、ajax的应用

#### 1、ajax优势与不足

**优势：**

1、不需要插件支持

2、优秀的用户体验

3、提高web程序的性能

4、减轻服务器和带宽的负担

**不足：**

破坏浏览器前进、后退按钮的正常功能

对搜索引擎的支持不足

#### 2、$.ajax({参数})

是jquery的ajax请求最**底层**的方法

```js
$.ajax({
    url: './data/networkClass.json', // 请求的地址
    cache: false, // 是否缓存。get请求时，如果url地址和上次没有发生变化，则会走缓存，为了不走缓存，jQuery在地址的后面加了_=时间戳
    type: 'get', // 请求的方式，get/post 默认get
    timeout: 5000, // 设置超时时间 时间ms
    data: 'a=1&b=2', // 发送到后端的数据
    // dataType: '', // 期待后端返回的数据类型，xml, html, script, json, jsonp, text
    success: function (data) { // 成功的回调
        console.log(data);
    },
    error: function (e) { // 失败的回调
        console.log(e);
    },
    complete: function () { // 不论成功失败，都会走这里
        console.log('执行到我了');
    }
})
```

#### 3、$.get()  

它是建立在$.ajax之上的一个请求

格式：$.get(url, 发到后端的数据, 成功的回调);                  没有数据，可以不写，发送get请求

```js
// 不带参数
$.get('./data/networkClass.json', function (data) {
    console.log(data);
})

// 带参数
$.get('./data/networkClass.json', 'a=1&b=2', function (data) {
    console.log(data);
})
```

#### 4、$.post()

格式：$.post(url, 发送到后端的数据, 回调);           没有数据，可以不写，发送post请求

```js
// 不带参数
$.post('./data/networkClass.json', function (data) {
    console.log(data);
})

// 带参数
$.post('./data/networkClass.json', 'a=1&b=2', function (data) {
    console.log(data);
})
```

#### 5、get请求和post请求的区别

1、get请求会将参数跟在URL后进行传递，而post请求则是作为HTTP消息的实体内容发送给WEB服务器。当然，在ajax请求中，这种区别对用户是不可见的。

2、get请求方式对传输的数据有大小限制（通常不能大于2KB），而使用post方式传递的数据量要比get方式大得多（理论上不受限制）。

3、get方式请求的数据会被浏览器缓存起来，因此其他人就可以从浏览器的历史记录中读取到这些数据，例如账号和密码等。在某种情况下，get方式会带来严重的安全性问题，而post方式相对来说可以避免这些问题。

4、get方式和post方式传递的数据在服务器端获取也不相同。在php中，get方式的数据可以用$_GET[]获取，而post方式可以用$_POST[]获取。两种方式都可以用$_REQUEST[]来获取。



#### 6、jQuery中的jsonp

**跨域**：域名、端口、协议任何一项不同，即为跨域

浏览器对于JavaScript的同源策略的限制：例如a.cn下面的js不能调用b.cn中的js。因为a.cn和b.cn是不同域，所以跨域就出现了。



**jsonp是jQuery中的跨域处理**

jquery中的jsonp，不是ajax，只不过它和ajax都集中在$.ajax里面

```js
var url = 'https://p.3.cn/prices/mgets?skuIds=J_5089253&type=1';
$.ajax({
    url: url,
    dataType: 'jsonp', // 解决跨域
    success: function (data) {
        console.log(data);
    },
    error: function (e) {
        console.log(e);
    }
});
```

#### 7、jsonp的原理

- 首先我们需要明白，在页面上直接发起一个跨域的ajax请求是不可以的，但是，在页面上引入不同域上的js脚本却是可以的。

- 那么如何使用<script src="">来完成一个跨域请求

- 当创建并添加一个<script src="xxx&callback=fn">标签，用于发起跨域请求；注意看请求地址后面带了一个callback=fn的参数；

- fn即是回调函数名称，传到后台，用于包裹数据。数据返回到前端后，就是fn(data)的形式，因为是script脚本，所以自动调用全局的fn函数，而data就是fn的参数。

- 至此，我们算是跨域把数据请求回来了，但是比较麻烦，需要自己写脚本发起请求，然后写个回调函数处理数据，不是很方便。

![](D:\1009\day23\2笔记\jsonp原理.jpg)

**注意：**

可以看到，jsonp方式不支持POST方式跨域请求，就算指定成POST方式，会自动转为GET方式；而后端如果设置成POST方式了，那就请求不了了。

jQuery的ajax方式以jsonp类型发起跨域请求，其原理跟<script>脚本请求一样，因此使用jsonp时也只能使用GET方式发起跨域请求。跨域请求需要服务端配合，设置callback，才能完成跨域请求。





#### 8、数据串连化

form表单.serialize() 串连成一个字符串

form表单.serializeArray()  串连成一个数组

作用：可以将 form中的数据，串连起来，不用一个一个去获取

```html
<form>
    <input type="text" name="a" value="1">
    <input type="text" name="b" value="2">
    <input type="text" name="c" value="3">
</form>
```

```js
var form = $('form');

console.log(form.serialize()); // a=1&b=2&c=3 串连成字符串
console.log(form.serializeArray()); // 串边成数组
// [
//     {name: 'a', value: '1'},
//     {name: 'b', value: '2'},
//     {name: 'c', value: '3'}
// ]

// --------------------------
$.ajax({
    url: './data/networkClass.json',
    // data: form.serialize(),
    data: form.serializeArray(),
    success: function (data) {
        console.log(data);
    }
})
```





