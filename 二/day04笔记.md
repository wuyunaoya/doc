## 1、this

- this一般在函数中使用，这个函数被谁调用，this就指向谁
- this不在定义的时候确定，而是在调用的时候确定的

```js
var box = document.getElementById('box');

box.onclick = function () {
    console.log(this); // box
}
```



## 2、自定义属性

自定义属性是指给标签添加已有属性的以外的属性，例如div标签id、class这些属性都是已有的，如果再添加一个tag属性，这就是自定义的。

- 自定义属性

```js
var pic = document.getElementById('pic');

pic.onOff = true; // 添加一个自定义属性

pic.onclick = function () {
    if (this.onOff) {
        this.src = 'img/on.png';
    } else {
        this.src = 'img/off.png';
    }
    this.onOff = !this.onOff;
}
```

- 自定义下标

```html
<ul>
    <li>吃饭</li>
    <li>睡觉</li>
    <li>打豆豆</li>
</ul>
```

```js
// 需求：一组列表，点击列表项，打出它的下标
var li = document.getElementsByTagName('li');
// for循环，给每个li绑定点击事件
for (var i = 0; i < li.length; i++) {
    li[i].index = i; // 添加自定义下标

    li[i].onclick = function () {
        // console.log(i);
        console.log(this.index);
    }
}
```

- 案例：**tab切换**



## 3、函数

函数是由事件驱动的或者当它被调用时执行的可重复使用的代码块。在使用函数时需要经过两个步骤，先声明函数后调用函数。

**所谓函数**，本质上是一种代码的分组形式。我们可以通过这种形式赋予某组代码一个名字，便于日后重用时调用。



#### 1、函数声明和函数表达式

**函数声明**

- 格式：function 函数名() { 代码块 }
- 调用：函数名();

```js
function fn() {
    console.log('我是平头哥');
}
fn();
```



**函数表达式**

- 格式：var 函数名 = function () { 代码块 }
- 调用：函数名();

```js
var fn = function () {
    console.log('我是平头妹');
}
fn();
```



#### 2、函数声明和函数表达式的区别

```js
function fn() {
    console.log(123);
}
fn();

var fn2 = function () {
    console.log('abc');
}
fn2();

// 函数声明和函数表达式的区别：
// 函数声明的调用可以在定义的前面或后面均可，而函数表达式的调用，只能放在函数定义的后面调用。
```

#### 3、函数的参数

- 如果在函数中，出现不能确定的、可变的值，我们会使用函数参数来实现。
- 格式
  - function 函数名(形参1, 形参2, ...) { 代码块 }
  - var 函数名 = function (形参1, 形参2, ...) { 代码块 }
  - 函数名(实参1, 实参2, ...)
- 注意：形参相当于函数中的var

```js
// 如果在函数中，出现不能确定的、可变的值，我们会使用函数参数来实现。
// 1--n之间所有数的和

function fn(n) {
    var num = 0;
    for (var i = 1; i <= n; i++) {
        num += i;
    }
    console.log(num);
}

fn(100);
fn(50);
fn(10);
```

```js
// 如果实参比形参多，则多的也白多，如果实参比形参少，则没有匹配的形参，值为undefined

function fn(a, b) {
    console.log(a, b);
}

fn(3, 5);
fn(7, 8);
fn(4, 5, 6, 7);
fn(7);
```



#### 4、arguments

arguments：实参的集合(对象、类数组、伪数组)，有长度，可以通过下标获取某一个参数

```js
function fn() {
    // console.log(arguments); // arguments: 是一个对象，是函数的实参的集合，是一个类数组（伪数组），有长度，可以通过下标获取某一个
    // console.log(arguments[0]); // 通过下标获取某一个

    var num = 0;
    for (var i = 0; i < arguments.length; i++) {
        // console.log(arguments[i]);
        num += arguments[i];
    }
    console.log(num);
}
fn(7, 8);
fn(2, 3, 4, 5);
```

arguments和形参的关系：arguments和形参一一对应，是同一个值的不同的名

```js
function fn(a, b) {
    a = 10;
    console.log(arguments[0]); // 10

    arguments[1] = 20;
    console.log(b); // 20
}

fn(7, 8);
```

4、函数参数的类型

- 参数可以任意数据类型

```js
// 参数可以任意类型
function fn(a) {
    console.log(typeof a, a);
}

fn(3);
fn('3');
fn(true);
fn(null);
fn();
fn([1, 2, 3]);
fn({});
fn(function () { });
```

#### 5、函数中的this

- 谁让这个函数执行，this就指向谁
- this不是在函数定义的时候确定的，而是在函数调用的时候确定的

```js
var box = document.getElementById('box');
function fn() {
    console.log(this);
}
// 谁让这个函数执行，this就指向谁
// this不是在函数定义的时候确定的，而是在函数调用的时候确定的

// 1、事件函数中的this
box.onclick = fn; // box

// 2、函数主动触发
fn(); // window

// 3、混合
box.onclick = function () { // box
    fn(); // window
}
```



## 4、函数中的问题

1、形参和实参个数的问题

- 如果实参比形参少，没有匹配上的形参，值为undefined。
- 如果实参比形参多，超过的实参忽略了。

```js
function fn(a, b) {
    console.log(a);
    console.log(b);
}
fn(2, 3);
fn(2);
fn(2, 5, 6, 7);
```

2、如果函数同名，后面的覆盖前面的

```js
function fn() {
    console.log(1);
}
function fn() {
    console.log(2);
}
fn();
```

























