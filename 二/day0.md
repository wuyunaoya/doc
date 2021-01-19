## 1、数据类型分类

- **基本数据类型(简单数据类型)**：Number(数值) String(字符串) Boolean(布尔) Null(空) Undefined(未定义)
- **引用数据类型(复杂数据类型)**：Object(对象)



#### 1、数据类型的判断

- 判断数据类型的方法：typeof 变量 或者 typeof(变量)

- 它返回的是6个字符串

  ​	Number： typeof返回 'number'

  ​	String： typeof返回 'string'

  ​	Boolean： typeof返回 'boolean'

  ​	Null： typeof返回 'object'

  ​	Undefined： typeof返回 'undefined'

  ​	对象 {}： typeof返回 'object'

  ​	对象 []： typeof返回 'object'

  ​	对象 函数： typeof返回 'function'



#### 2、Number

```js
// 整数 小数 负数都是数字
var a = 10;
console.log(a, typeof a); // 10 "number"

var b = 0.5;
console.log(b, typeof (b)); // 0.5 number

var c = -8;
console.log(c, typeof c); // -8 "number"

var d = 070; // 8进制
console.log(d, typeof d); // 56 "number"
```

NaN

```js
var e = '尹喆' - 5; // 你的算法本意想得到一个数字，但是没有办法给你一个数字，只能给你一个NaN。NaN是not a number，但它是数字类型
console.log(e, typeof e); // NaN "number"
console.log(NaN === NaN); // false
console.log(e + 5); // NaN

// NaN的特点：
// 1、虽然不是数字，但是typeof返回number
// 2、NaN和谁都不相等，包括它自己
// 3、凡是有NaN参与的运算，结果都是NaN
```

```js
var f = 1 / 0;
console.log(f, typeof f); // Infinity 无穷大   "number"

// -----------------------
var g = 0.1 + 0.2;
console.log(g); // 0.30000000000000004
if (g == 0.3) { // 不要做这种判断
    console.log('尹喆就去吃饭');
}
```



#### 3、String

单双引号引起来的都是字符串

```js
// 单双引号引起来的都是字符串
var str1 = '小尹';
var fn = "前端'开'发";
var str2 = '我是"平头哥"';
var str3 = '10';

console.log(str1, typeof str1); // 小尹 string

// ----------------------------------
// 通过下标获取某一个字符:  字符串[下标]      字符串.charAt(下标)
// 长度：字符串.length
var str4 = '我是平头妹';
console.log(str4[2]);
console.log(str4.charAt(2));
console.log(str4.length);

// ---------------------------------
// 从页面input中获取的都是字符串
var txt = document.getElementById('txt');
var btn = document.getElementById('btn');
btn.onclick = function () {
    var v = txt.value;
    console.log(v, typeof v);
}
```

#### 4、Boolean

```js
// Boolean：布尔（真true / 假false）

var b1 = true;
console.log(b1, typeof b1); // true "boolean"

var b2 = false;
console.log(b2, typeof b2); // false "boolean"
```

#### 5、null 与 undefined

```js
// null 表示变量已赋值但为空
// 声明一个变量，准备在将来给它赋值为对象时，但是现在没有值赋，就给它赋为null
var n = null;
console.log(n, typeof n); // null "object"
```

```js
// undefined   表示变量已声明但是没有赋值
var u; // 声明了没有赋值，它就是undefined
console.log(u, typeof u); // undefined "undefined"
```

**null和undefined的区别**

- 1、undefined是申明了，未赋值，null是值为空，是准备在将来存储为一个对象的
- 2、undefined的typoef返回的是undefined，null的typeof返回的是object
- 3、undefined转成数字是NaN，null转成数字是0



#### 6、Object

对象：本质上是一组无序的名值对

```js
// 默认提供的对象
console.log(window, typeof window); // "object"
console.log(document, typeof document); // "object"

// 自己定义
var obj = {
    age: 3,
    name: '小尹',
    fn: '前端开发'
}
console.log(obj, typeof obj); // {age: 3, name: "小尹", fn: "前端开发"}    "object"

// 读取
console.log(obj.age);
console.log(obj['name']);

// -------------------------------------
var arr = [1, 2, 3]; // 数组
console.log(arr, typeof arr); // [1, 2, 3]    "object"

// -------------------------------
function fn() { } // 函数
console.log(fn, typeof fn); // "function"
```



## 2、数据类型的强制转换

#### 1、转数字

##### 1、Number

语法：Number(变量)。可以将其它任何数据类型转换为数字，只有能转成功或不能转成功之分，能转成功就返回数字，不能转成功就返回NaN

- 1、字符串如果全是数字(包括小数点)转成数字；如果有不是数字的，转成NaN，空字符串和空格转成0
- 2、true转成1， false转成0
- 3、数字简单的返回
- 4、null转成0
- 5、undefined转成NaN
- 6、对象一般返回NaN，一般不用来转对象

```js
console.log(Number(10)); // 10

console.log(Number('12px')); // NaN
console.log(Number('12.34')); // 12.34
console.log(Number('')); // 0
console.log(Number('   ')); // 0

console.log(Number(true)); // 1
console.log(Number(false)); // 0

console.log(Number(null)); // 0

console.log(Number(undefined)); // NaN
```

##### 2、parseInt、parseFloat

- parseInt(变量, 进制); 转整数，不识别小数点
  - 从左向右一位一位的看，如果是数字，则提出来，如果不是数字，则到此为止
- parseFloat(变量); 转小数，它识别一个小数点，并且没有第二个参数

```js
console.log(Number('12.34px')); // NaN

console.log(parseInt('12.34px')); // 12

console.log(parseInt('23ab123px')); // 23
console.log(parseInt('ab23sd123px')); // NaN

console.log(parseInt('070')); // 在IE8及以下，返回56，当作8进制
console.log(parseInt('070', 10)); // 加上进制之后，所有浏览器表现统一

// -----------------------------
console.log(parseFloat('12.34px')); // 12.34
console.log(parseFloat('12.3.4px')); // 12.3
```



#### 2、转字符串

- String(变量); 可以将任何类型转为字符串
- 变量.toString(); 不能转换null和undefined

```js
console.log(String('abc')); // 'abc'  字符串简单返回

console.log(String(10)); // '10'
console.log(String(NaN)); // 'NaN'
console.log(String(1 / 0)); // 'Infinity'

console.log(String(true)); // 'true'
console.log(String(false)); // 'false'

console.log(String(null)); // 'null'
console.log(String(undefined)); // 'undefined'

console.log(String({})); // [object Object]
console.log(String([])); // ''
console.log(String([1, 2, 3])); // '1,2,3'

// -----------------------------
console.log((10).toString());
console.log((NaN).toString());
console.log((true).toString());
console.log((false).toString());

// var n = null;
// console.log(n.toString()); // 报错

// var u;
// console.log(u.toString()); // 报错
```



#### 3、转布尔值

格式：Boolean(变量) 可以将其它任何数据类型转成布尔值

```js
console.log(Boolean(true)); // true
console.log(Boolean(false)); // false

console.log(Boolean('ab')); // true
console.log(Boolean('')); // false
console.log(Boolean('  ')); // true

console.log(Boolean(10)); // true
console.log(Boolean(1 / 0)); // true
console.log(Boolean(0)); // false
console.log(Boolean(NaN)); // false

console.log(Boolean(undefined)); // false
console.log(Boolean(null)); // false

// 一切对象都转为true
console.log(Boolean({})); // true
console.log(Boolean([])); // true
```

**js里面的假值**：false 空字符串 0 NaN null undefined

除了这六个值之外，其它的均是真值，一切对象都是真值，包括[] 和 {}



#### 4、isNaN

isNaN(变量); 是不是 不是一个数字。返回布尔值。如果不是数字，返回true，如果是数字，返回false

isNaN本身自己不做事，它交给它的好朋友Number()来做事，如果Number能成功转成数字，则isNaN返回false，如果转不成功，则isNaN返回true

```js
console.log(isNaN(10)); // false
console.log(isNaN(NaN)); // true

console.log(isNaN('10')); // false
console.log(isNaN('10px')); // true
console.log(isNaN('')); // false
console.log(isNaN('  ')); // false

console.log(isNaN(true)); // false
console.log(isNaN(false)); // false

console.log(isNaN(null)); // false
console.log(isNaN(undefined)); // true
```



## 3、运算符

#### 1、算术运算符

**加（+）**

- 1、如果两边都是数字，则就是普通的数学计算
- 2、如果有一边是字符串，则另一边也转成字符串，变成字符串的拼接
- 3、如果没有字符串，则调用Number方法，转成数字，再进行相加
- 4、如果有一边是对象，则对象调用toString得到字符串表示，再进行计算

```js
console.log(5 + 10); // 15
console.log(5 + '10'); // '510'
console.log(true + null); // 1

console.log(5 + undefined); // NaN
console.log('' + null); // 'null'
console.log('' + NaN); // 'NaN'
console.log(NaN + ''); // 'NaN'
console.log(true + [true]); // 'truetrue'
console.log(true + [1, 2, 3]); // 'true1,2,3'
```

```js
var a = 5;
var b = 10;
// console.log('5+10的和是15');
console.log(a + '+' + b + '的和是' + (a + b)); // 5+10的和是15
```

**减（-）乘（*）除（/）**

- 操作符的两边，调Number都转成数字

```js
console.log(10 - 5); // 5
console.log(10 - '5'); // 5
console.log('小尹' - 5); // NaN
```

**取余（%）**

- 操作符的两边，调Number都转成数字

```js
console.log(10 % 3); // 1
console.log(10 % '3'); // 1
console.log(10 % null); // NaN
```

```js
// 一个递增的值，取模n，返回的是0--n-1之间的数
console.log(0 % 3); // 0
console.log(1 % 3); // 1
console.log(2 % 3); // 2
console.log(3 % 3); // 0
console.log(4 % 3); // 1
console.log(5 % 3); // 2
console.log(6 % 3); // 0
```

**加加（++）减减（--）**

```js
var a = '5';
a++; // a = a+1;  加加在后   先参与表达式的运算，再自增
++a; // a = a+1;  加加在前   先自增，再参与表达式的运算
console.log(a);
```

```js
var num1 = 2;
var num2 = 20;
var num3 = num1-- + num2;
var num4 = num1 + num2;
console.log(num3, num4);
```

#### 2、赋值运算符

- 赋值（=）

- 操作符的两边先操作，结果赋给左边

  加等于（+=）

  减等于（-=）

  乘等于（*=）

  除等于（/=）

  取余等于（%=）

```js
var a = 5; // 将5赋给a

a += 3; // a = a + 3;
console.log(a);
```



#### 3、比较运算符

- 大于（>）   大于等于（>=）    小于（<）    小于等于（<=）

```js
// 如果两边都是字符串，则是字符串的比较。字符串是比较的ASCII编码，是一位一位的比较
// 只要有一边不是字符串，则是数值的比较（调Number()方法，转成数字）
console.log(12 > 2); // true
console.log(12 > '2'); // true
console.log('12' > '2'); // false

// ------------------------------
console.log(null >= ''); // true
console.log(null >= undefined); // false
console.log(null <= undefined); // false
```



- 值是否相等（==）    不等于（!=）

为了进行值的比较，会调用Number方法，转成数字(会进行隐式类型转换)。null和undefined不能转换

```js
console.log('10' == 10); // true
console.log(true == 1); // true

console.log(null == 0); // false
console.log(null == false); // false 

console.log(null == undefined); // true  规定的
console.log(null == null); // true
console.log(undefined == undefined); // true

console.log(null != undefined); // false
console.log(null != false); // true
```



- 绝对等于（===） 值和类型都要相等结果才为true(不会隐式类型转换)
- 绝对不等于（!==）

```js
console.log('10' === 10); // false
console.log('10' !== 10); // true

console.log(null === undefined); // false
console.log(null !== undefined); // true
```



#### 4、逻辑运算符

**&& 与**

操作符的两边都为真，结果为真

短路操作，即左边能够决定的，就不用跑到右边来

- 如果左边为假，则不用跑到右边；直接看左边，如果左边是表达式，则表达式求值，如果左边是值，则返回这个值
- 如果左边为真，则跑到右边；直接看右边，如果右边是表达式，则表达式求值，如果右边是值，则返回这个值

```js
console.log(10 > 8 && 20 >= 15); // true
console.log(10 > 8 && 20 < 15); // false
console.log(10 < 8 && 20 > 15); // false

console.log(10 > 8 && 3); // 3
console.log(NaN && 3); // NaN
console.log(8 && 5); // NaN
```

**|| 或**

操作符的两边只要有一边为真，则结果为真

短路操作，只要左边能决定的，就不用跑到右边

- 如果左边为真，则不用跑到右边；直接看左边，如果左边是表达式，则表达式求值，如果左边是值，则返回这个值
- 如果左边为假，则跑到右边；直接看右边，如果右边是表达式，则表达式求值，如果右边是值，则返回这个值

```js
console.log(10 > 8 || 10 < 8); // true
console.log(10 < 8 || 8); // 8
```

**!  非**

取反

```js
var a = 10;
console.log(!a); // false
console.log(!!a); // true
console.log(!!!!!!!!!!!a); // false
```



#### 5、三元运算符

格式：条件 ? 执行代码1 : 执行代码2;

- 如果条件为真，则执行代码1，否则执行代码2

```js
var age = 7;

// age >= 7 ? alert('上小学') : alert('上幼儿园');

// 推荐
var str = age >= 7 ? '上小学' : '上幼儿园';
alert(str);
```



## 4、数据类型的隐式转换

```js
// 加 +
console.log(10 + 100); // 110
console.log(10 + 'string'); // '10string'
console.log(19 + 10 + 'age' + 18 + 10) // 29age1810
console.log(10 + '100'); // 10100
console.log(10 + true); // 11
console.log(true + false); // 1
console.log('10' + true); // 10true
console.log('' + 100); // '100'
console.log(10 + null); // 10
console.log(10 + undefined); // NaN
// 减 -
console.log(100 - 10); // 90
console.log(100 - 't'); // NaN
console.log(100 - ''); // 100
console.log(100 - true); // 99
console.log(100 - '80'); // 20
console.log(100 - null); // 100
console.log(100 - undefined); // NaN
// 乘 *
console.log(100 * 'a'); // NaN
console.log(100 * ''); // 0
console.log(100 * '100'); // 10000
console.log(100 * null); // 0
console.log(100 * undefined); // NaN
// 除 /
console.log(100 / 'a'); // NaN
console.log(100 / ''); // 无穷大
console.log(100 / '70'); // 10/7
console.log(100 / null); // 无穷大
console.log(100 / undefined); // NaN
// 取余 %
console.log(100 % 'a'); // NaN
console.log(100 % ''); // NaN
console.log(100 % '70'); // 30
console.log(100 % null); // NaN
console.log(100 % undefined); // NaN
// ++
var n = '10';
n++;
console.log(n); // 11
// 取反
console.log(!true); // false
console.log(!10); // false
console.log(!'web'); // false
```



