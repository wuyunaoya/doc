## 1、作用域

**作用域指**：变量或函数的有效使用范围，有**全局作用域**与**局部作用域**两种。



#### 1、全局变量和局部变量

**全局变量**：直接在 script 标签下声明的变量，任何地方都能访问，任何地方都能对其值进行改变。

**局部变量**：函数内部定义的变量，函数内能访问，出了函数的括号就不能访问（垃圾回收）。

```js
// 全局变量：直接在 script 标签下声明的变量，任何地方都能访问，任何地方都能对其值进行改变。
var a = 10;
function fun1() {
    a++;
    console.log(a); // 11
}
function fun2() {
    a++;
    a--;
    console.log(a); // 11
}
fun1();
fun2();
console.log(a); // 11

// ------------------------
// 局部变量：函数内部定义的变量，函数内能访问，出了函数的括号就不能访问（垃圾回收）
function sum() {
    var a = 10;
    console.log(a); // 10
    function s() {
        console.log(a); // 10
    }
    s();
}
sum();
console.log(a); // 报错
s(); // 报错
```



#### 2、预解析和逐行解读

浏览器如何执行js：至少会经历两步

- 1、预解析
  - 找东西：找var、函数、参数，给var赋一个值为undefined放到最前面(仓库)，函数就是函数整体放到最前面，参数同var
  - 如果var和var同名，后面的覆盖前面的，如果函数和函数同名，后面的覆盖前面的，如果var和函数同名，则函数覆盖var

- 2、逐行解读
  - 从上到下，一行一行的执行，遇到 = + - * / % ++ -- 等操作就去修改(仓库)对应的值，遇到读取操作，就去(仓库)里面读对应的值
  - 遇到函数调用，就又开启一个新的局部的域，又要执行预解析和逐行解读。逐行解读时，会先找自己仓库里面的，如果自己仓库没有，会找父级仓库，如果父级也没有，会一直找到全局，如果全局没有，则报错。



## 2、函数返回值

#### 1、return

函数是用来实现某个特定功能，如计算某个范围内的累加，操作完成之后，在函数外部可能需要使用计算好的这个值，但是在函数内部定义的变量外面访问不了，针对这个情况，函数通过返回值将计算好的数据传出函数，在外部使用。在函数中将某个值返回到函数外，使用 return 关键字。

```js
// 求1--n之间所有数的和
function fn(n) {
    var num = 0;
    for (var i = 1; i <= n; i++) {
        num += i;
    }
    // console.log(num);
    return num;
}

var v1 = fn(100); // 函数调用的结果，就是return后面的内容
var v2 = fn(50);

console.log(v1);
console.log(v2);
```

- return的特点
  - 1、函数通过关键字return 返回函数中的内容
  - 2、return 一次只能返回一个值（如果想返回多个值，只能返回数组或对象）
  - 3、函数中只要遇到return，函数就会结束(return后面代码都不会再执行)
  - 4、函数没有返回值，默认结果为undefined

```js
function fn() {
    // return '小王';
    console.log('小芳，约不？');
}

var s = fn();
console.log(s); // 小王
```



#### 2、返回值类型

- 可以返回任何数据类型

```js
// 函数的返回值，可以是任何数据类型
function fn() {
    // return 3;
    // return 'ab';
    // return true;
    // return null;
    // return [1, 2, 3]
    // return {}
    return function () { }
}

console.log(fn());
```



#### 3、返回值实例

获取元素的样式

```js
// 通过js获取box的样式
var box = document.getElementById('box');

// 设置：box.style.样式名 = 值;
// 获取：box.style.样式名;  (只能获取行间的)

// --------------------------------
// IE8及以下不支持
// window.getComputedStyle(元素)   返回的是一个对象，是这个元素所有的样式
console.log(window.getComputedStyle(box));
console.log(window.getComputedStyle(box).width);
console.log(window.getComputedStyle(box).height);
console.log(window.getComputedStyle(box).backgroundColor);

// --------------------------
// IE支持
// 元素.currentStyle   返回的是一个对象，是这个元素所有的样式
console.log(box.currentStyle);
console.log(box.currentStyle.width);
console.log(box.currentStyle.height);
console.log(box.currentStyle.backgroundColor);

// --------------------
// 兼容：检查window下面是否有getComputedStyle这个方法，如果有，则是标准浏览器，否则就是IE8及以下
// console.log(window.getComputedStyle); // 在IE8及以下返回undefined

if (window.getComputedStyle) {
    // 标准浏览器
    console.log(window.getComputedStyle(box).width);
} else {
    // IE8及以下
    console.log(box.currentStyle.width);
}

// -------------------------
// 封装，参数为：元素 样式名
function getStyle(ele, attr) {
    if (window.getComputedStyle) {
        // 标准浏览器
        return window.getComputedStyle(ele)[attr];
    } else {
        // IE8及以下
        return ele.currentStyle[attr];
    }
}
console.log(getStyle(box, 'width')); // 100px
console.log(getStyle(box, 'height')); // 120px
console.log(getStyle(box, 'backgroundColor')); // red
```



## 3、函数封装及复用

函数主要用于事件处理函数、函数封装及代码复用。例如下面这种情况，功能一样，结构一致，并且用循环不太好实现的时候，就需要使用代码复用实现这个功能。

代码复用：

1、html结构尽量标准一样

2、先实现一个，但是里面的标签必须通过父元素获取

3、封装成函数，将父元素作为函数参数传入

4、调用

- 购物车
- 编缉标题





## 4、递归

JavaScript 中允许函数递归调用。

1、函数调用函数自身（执行递的动作）

2、最后一次判断一个终止条件。执行归的动作。

```js
// 简单递归
// 打印1--10
var i = 0;
function fn() {
    i++;
    console.log(i);
    if (i >= 10) {
        return;
    }
    fn();
}
fn();
```

```js
// 封装一个函数，求1到5之间所有数的积，即：1*2*3*4*5

// 求5阶乘：5*4*3*2*1

// 循环实现
function fn(n) {
    var num = 1;
    for (var i = n; i >= 1; i--) {
        // console.log(i);
        num *= i;
    }
    return num
}
console.log(fn(5));

// ---------------------
// 递归
function fn(n) {
    if (n === 1) {
        return 1;
    }
    return n * fn(n - 1);
}
console.log(fn(5));

// 5 * 4 * 3 * 2 * 1
```





