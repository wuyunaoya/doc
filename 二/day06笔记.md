## 1、定时器

```js
var 定时器标识 = setTimeout(函数, 时间毫秒); // 延迟执行，延迟某个特定的时间开始执行，只执行一次
clearTimeout(定时器标识); // 停止定时器

var 定时器标识 = setInterval(函数, 时间毫秒); // 重复执行或者叫间歇执行，即隔某个时间就执行一次
clearInterval(定时器标识);
```

**应用**：

​	1、广告

​	2、发送验证码（防止多次点击，可以用 **先关后开** 、 disabled  、自定义开关）



**定时器中的问题：**

1、定时器中的this就是window

2、定时器是一个异步

```js
// 定时器调用的函数的this是window
setTimeout(function () {
    console.log(this); // window
}, 1000);


// 定时器是一个异步，它排在同步的后面执行
// 即所有的同步执行完了，才会执行异步
setTimeout(function () {
    console.log(1);
}, 0);
console.log(2);
```



## 2、运动框架

- 问题1：点一下动一下，不智能
- 问题2：开启之后，不能停止
- 问题3：多次点击，会加速
- 问题4：对外界条件依赖过多
- 问题5：现在只能从左向右，还不能从右向左
- 问题6：需要封装成一个函数
- 问题7：dir这个属性，不应该由用户输入，而应该由函数确定
- 问题8：添加回调函数（某一件事完成之后，要做的事）



## 3、数学对象

**Math**是 JavaScript 的原生对象，提供各种数学功能。该对象不是构造函数，不能生成实例，**所有的属性和方法都必须在Math对象上调用**。

```js
console.log(Math.floor(3.999)); // 向下取整  去掉小数部分   3
console.log(Math.ceil(3.001)); // 向上取整  只要有小数就进位  4
console.log(Math.round(3.14159)); // 四舍五入  3
console.log(Math.abs(-100)); // 绝对值   100
console.log(Math.max(1, 2, 36, 9)); // 参数的最大值  36
console.log(Math.min(1, 2, 36, 9)); // 参数的最小值   1
console.log(Math.pow(2, 10)); // 2的10次方   1024
console.log(Math.pow(3, 2)); // 3的2次方   9
console.log(Math.sqrt(60)); // 开根号   7.745966692414834
console.log(Math.PI);
```

- 随机数：Math.random()，返回大于等于0，小于1的一个随机数

- 随机数公式：
  - 1、大减小加1 
  - 2、乘以随机数
  - 3、加上最小数
  - 4、向下取整

```js
// 参数为：最小值 最大值
function getRandom(min, max) {
    return Math.floor(Math.random() * (max - min + 1) + min);
}
```

- 案例：抽奖（点名），验证码

