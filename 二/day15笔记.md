## 1、闭包

#### 1、匿名函数自执行

**函数分类**

```js
// 函数声明
function fn() { }

// 函数表达式
var fn = function () { }

// 事件函数
box.onclick = function () { }

// 构造函数
function Fn() { }

// 回调函数
move(box, 'left', 500, function () { })
function move(ele, attr, target, callback) { }

// 匿名函数  匿名函数自执行
(function () { })();
(function () { }());
```



**匿名函数自执行**

```js
// 匿名函数自执行，一定要加分号

// 匿名函数自执行
(function () {
console.log('我执行了');
})();

// 有参数
(function (a, b) {
console.log(a + b);
})(3, 5);

// 有返回值
var n = (function (a, b) {
return a + b;
})(5, 6);
console.log(n);
```

**匿名函数的好处**

```js
var a = 1;

(function () {
    // 防止全局变量的污染
    var a = 10;
    console.log(a);
})();

console.log(a);
```



#### 2、闭包

**什么是闭包**。

闭包就是能够读取其他函数内部变量的函数（函数里面套函数，内部函数访问外部函数变量），在本质上，闭包是将函数内部和函数外部连接起来的桥梁。

- 1、函数定义在函数内部
- 2、函数可以访问外部函数的变量、参数、或者其它函数
- 3、函数在包含它的外部函数外面被调用
- 这个函数就是一个闭包

```js
function fn() {
    var n = 10;
    return function () {
        n++;
        return n;
    }
}

var v = fn();
console.log(v()); // 11
console.log(v()); // 12
console.log(v()); // 13
```

**闭包最大的特点**：就是它可以“记住”诞生的环境，在本质上，闭包就是将函数内部和函数外部连接起来的一座桥梁。

**闭包的最大用处有两个**，一个是可以读取函数内部的变量，另一个就是让这些变量始终保持在内存中，即闭包可以使得它诞生环境一直存在。



**闭包的应用场景1**：模拟对象的私有属性

```js
function fn() {
    var _age = 3;
    return {
        // 设置
        setAge: function (val) {
            _age = val;
        },
        // 读取
        getAge: function () {
            return _age;
        }
    }
}

var obj = fn();
// console.log(obj);
obj.setAge(5);
console.log(obj.getAge());
```



**闭包的应用场景2**：循环中的闭包

```html
<ul>
    <li>吃饭</li>
    <li>睡觉</li>
    <li>打豆豆</li>
</ul>
```

```js
// 点击li，打出它的下标
var li = document.getElementsByTagName('li');

// 不可以
for (var i = 0; i < li.length; i++) {
    li[i].onclick = function () {
        console.log(i);
    }
}

// 自定义下标的方法
for (var i = 0; i < li.length; i++) {
    li[i].index = i; // 自定义下标
    li[i].onclick = function () {
        console.log(this.index);
    }
}


// 闭包的做法
for (var i = 0; i < li.length; i++) {
    li[i].onclick = (function (i) {
        return function () {
            console.log(i);
        }
    })(i);
}

for (var i = 0; i < li.length; i++) {
    (function (i) {
        li[i].onclick = function () {
            console.log(i);
        }
    })(i);
}
```



## 2、ajax



AJAX即“Asynchronous Javascript And XML”（**异步javaScript和XML**），是指一种创建交互式网页应用的网页开发技术，可以用于创建快速动态网页的技术。

**异步**：浏览器在请求数据的过程中，不会一直等待，这段时间还可以做其他的操作。

**同步**：浏览器在请求数据的过程中，会一直等待事件的响应，直到返回结果才会执行其他的操作。



#### 1、基本流程

```js
// 1、创建ajax对象
var xhr = new XMLHttpRequest();

// 2、open(打开方式(get/post), 地址, 是否异步);
// 异步：浏览器在请求数据的过程中，不会一直等待，这段时间还可以做其他的操作。
// 同步：浏览器在请求数据的过程中，会一直等待事件的响应，直到返回结果才会执行其他的操作。
xhr.open('get', './data/a.txt', true);

// 3、send发送
xhr.send();

// 4、等待服务器返回
// A、xhr.onreadystatechange  事件  当ajax的状态发生变化的时候，这个函数就会执行
// B、ajax状态   xhr.readyState  会返回 0 1 2 3 4
//      0	（初始化）还没有调用open()方法
//      1	（载入）已调用send()方法，正在发送请求
//      2	（载入完成）send()方法完成，已收到全部响应内容
//      3	（解析）正在解析响应内容
//      4	（完成）响应内容解析完成，可以在客户端调用了

// C、服务器状态码   xhr.status  
//      1XX系列：指定客户端应响应的某些动作，代表请求已被接受，需要继续处理。由于 HTTP/1.0 协议中没有定义任何 1xx 状态码，所以除非在某些试验条件下，服务器禁止向此类客户端发送 1xx 响应。
//      2XX系列：代表请求已成功被服务器接收、理解、并接受。这系列中最常见的有200、201状态码。
//      3XX系列：代表需要客户端采取进一步的操作才能完成请求，这些状态码用来重定向，后续的请求地址（重定向目标）在本次响应的 location 域中指明。这系列中最常见的有301、302状态码。
//      4XX系列：表示请求错误。代表了客户端看起来可能发生了错误，妨碍了服务器的处理。常见有：401、404状态码。
//      5XX系列：代表了服务器在处理请求的过程中有错误或者异常状态发生，也有可能是服务器意识到以当前的软硬件资源无法完成对请求的处理。常见有500、503状态码。
// D、返回的数据 xhr.responseText   字符串
xhr.onreadystatechange = function () {
    if (xhr.readyState === 4) { // ajax完成
        if (xhr.status === 200) { // 200成功
            console.log(xhr.responseText); // 响应的文本
        }
    }
}
```

#### 2、get请求并传数据

```js
var xhr = new XMLHttpRequest();

// get方式的数据，用?跟在url的后面
xhr.open('get', './data/a.txt?a=1&b=2', true);

xhr.send();

xhr.onreadystatechange = function () {
    if (xhr.readyState === 4) {
        if (xhr.status == 200) {
            console.log(xhr.responseText);
        }
    }
}
```

#### 3、post请求并传数据

```js
var xhr = new XMLHttpRequest();

xhr.open('post', './data/a.txt', true);

// post请求，数据以send的参数发送
// 在send发送前，要设置消息头
xhr.setRequestHeader('content-type', 'application/x-www-form-urlencoded');
xhr.send('c=3&d=4');

xhr.onreadystatechange = function () {
    if (xhr.readyState === 4) {
        if (xhr.status === 200) {
            console.log(xhr.responseText);
        }
    }
}
```

#### 4、封装

```js
// 参数：请求的方式, 请求的地址, 要传给后端的数据, 回调函数
function ajax(methods, url, data, callback) {
    // 第一步
    var xhr = new XMLHttpRequest();

    if (methods === 'get') {
        // get请求
        if (data) {
            url += '?' + data;
        }
        xhr.open('get', url, true);
        xhr.send();
    } else {
        // post请求
        xhr.open('post', url, true);
        xhr.setRequestHeader('content-type', 'application/x-www-form-urlencoded');
        xhr.send(data);
    }

    xhr.onreadystatechange = function () {
        if (xhr.readyState === 4) {
            if (xhr.status === 200) {
                // 请求成功了
                callback && callback(xhr.responseText);
            } else {
                // 失败
                throw new Error('ajax请求失败，失败的状态码是：' + xhr.status);
            }
        }
    }
}
```



#### 5、JSON

- JSON.parse(长得像对象的字符串); 将字符串转成对象
- JSON.stringify(对象); 将对象转成字符串

```js
var arr = ['刘备', '关羽', '张飞'];

var str = JSON.stringify(arr);
console.log(str); // 字符串 ["刘备","关羽","张飞"]
console.log(typeof str); // string
console.log(JSON.parse(str)); // 数组 [ "刘备", "关羽", "张飞" ]
```



