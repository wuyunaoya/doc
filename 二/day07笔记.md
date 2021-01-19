## 1、时间对象

#### 1、时间对象

```js
var d = new Date(); // 时间对象，{}，里面有很多的属性和方法。没有传参，创建的是当前电脑此时此刻的时间
// console.log(d);

var year = d.getFullYear(); // 年
var month = d.getMonth() + 1; // 月  0--11  代表 1--12
var date = d.getDate(); // 日

var week = d.getDay(); // 星期  0--6  代表 周日--周六

var h = d.getHours(); // 小时
var m = d.getMinutes(); // 分钟
var s = d.getSeconds(); // 秒

console.log(year, month, date, week, h, m, s);
```

案例：数字时钟

#### 2、时间戳

**时间戳**：1970 年 1 月 1 日午夜（零时）开始到现在经过的毫秒数

```js
// 时间戳：返回从1970年1月1日零时到现在经过的毫秒数
// 所有浏览器都支持
var d = new Date();
console.log(d.getTime()); // 1602815209971

// IE8及以下不支持
console.log(Date.now()); // 1602815239148
```



#### 3、多种时间格式

```js
var d = new Date();

// console.log(d);

// 英文
console.log(d.toString()); // Fri Oct 16 2020 10:30:05 GMT+0800 (中国标准时间)
console.log(d.toDateString()); // Fri Oct 16 2020
console.log(d.toTimeString()); // 10:30:51 GMT+0800 (中国标准时间)

// 中文
console.log(d.toLocaleString()); // 2020/10/16 上午10:30:05
console.log(d.toLocaleDateString()); // 2020/10/16
console.log(d.toLocaleTimeString()); // 上午10:31:31
```



#### 4、创建特定时间

```js
// 没有传参，创建当前本地的时间
var d1 = new Date();
console.log(d1.toLocaleString());

// 传数字参数，分别是：年 月 日 时 分 秒
var d2 = new Date(2022, 10, 10, 12, 12, 12);
console.log(d2.toLocaleString());

// 传字符串参数
var d3 = new Date('2022,10,10 12:12:12');
console.log(d3.toLocaleString());

// 传时间戳参数
var d4 = new Date(12321421456500);
console.log(d4.toLocaleString());

// 修改时间某一部分
var d5 = new Date();
d5.setFullYear(2030); // 设置为2030年
d5.setMonth(15); // 设置月
d5.setDate(23); // 设置日
console.log(d5.toLocaleString());
```

#### 5、倒计时

```js
<h1>12天12小时12分钟12秒</h1>

<script>
    var h1 = document.querySelector('h1');
    var d1 = new Date(2020, 9, 16, 11, 5, 0); // 未来时间

    auto();
    var timer = setInterval(auto, 1000);

    function auto() {
        var d2 = new Date(); // 当前时间
        var d = Math.floor((d1 - d2) / 1000); // 取得差值毫秒，除以1000，取整得秒数

        // console.log(d);
        // 把秒转成 天 小时 分种 秒
        if (d <= 0) {
            clearInterval(timer);
            h1.innerText = '开始抢购吧';
            return;
        }

        var date = Math.floor(d / 86400); // 天
        var h = Math.floor(d % 86400 / 3600); // 小时
        var m = Math.floor(d % 86400 % 3600 / 60); // 分钟
        var s = d % 60; // 秒

        var str = date + '天' + h + '小时' + m + '分钟' + s + '秒';
        h1.innerText = str;
    }
</script>
```

#### 6、Moment.js

地址：http://momentjs.cn/

作用：moment.js是一个轻量级的JavaScript时间库，它方便了日常开发中对时间的操作，提高了开发效率。

日常开发中，通常会对时间进行下面这几个操作：比如获取时间，设置时间，格式化时间，比较时间等等。通过moment.js可以快速的格式化事件，得到想要的格式。

- 创建时间

```js
// 创建时间
var d = moment(); // 创建当前的时间
var d = moment('2020-12-12'); // 年月日
var d = moment('2020-12-12 12:12:12'); // 年月日 时分秒
var d = moment(2342342423432); // 时间戳
var d = moment(new Date() - 86400000); // 昨天
var d = moment('20201212'); // 年月日

console.log(d.format('YYYY年MM月DD日 HH:mm:ss'));
```

- 格式化时间

```js
var d = moment(); // 创建当前的时间

// 格式化时间
console.log(d.format('YYYY'));
console.log(d.format('MM'));
console.log(d.format('DD'));
console.log(d.format('HH'));
console.log(d.format('mm'));
console.log(d.format('ss'));

console.log(d.format('YYYY年MM月DD日 HH:mm:ss'));
```

- 修改或获取时间某一部分

```js
var d = moment().year(2030).month(4); // 创建时间，再设置某一部分
var d = moment().set('year', 2050).set('month', 7); // 创建时间，再设置某一部分

console.log(d.format('YYYY年MM月DD日 HH:mm:ss'));
```

- 其它操作

```js
// 支持的度量有 years、months、weeks、days、hours、minutes 和 seconds

// 增加时间
// 格式：时间.add(增加的数量, 时间的键);

// 增加三个月零5天
var d = moment().add(3, 'month').add(5, 'day');
console.log(d.format('YYYY年MM月DD日 HH:mm:ss'));

// -------------------------------
// 减少时间
// 格式：时间.subtract(减少的数量, 时间的键);

// 三个月以前
var d = moment().subtract(3, 'month');
console.log(d.format('YYYY年MM月DD日 HH:mm:ss'));

// ---------------------
// 时间比较  两个时间的差值
// 格式：时间1.diff(时间2, '比较的值');  时间1和时间2比较

var d = moment().diff(moment('20011010'), 'year');
console.log(d);
```



## 2、字符串对象

#### 1、创建

```js
// 字面量方式创建 成对的单双引号引起来即可
var str1 = '我是平头哥';
console.log(str1, typeof str1);

// 方法创建，不推荐
var str2 = String('我就是我');
console.log(str2, typeof str2);

// 3、构造函数创建，不推荐
var str3 = new String('东风吹');
console.log(str3, typeof str3);
```



#### 2、charAt

- 格式：字符串.charAt(下标);
- 作用：返回对应下标的字符

```js
// 下标 从0开始数
// 通过下标获取某一个字符
console.log(str[3]); // IE7及以下返回undefined
console.log(str.charAt(3)); // 所有浏览器都支持
```



#### 3、charCodeAt

- 格式：字符串.charCodeAt(下标);
- 作用：返回对应下标字符的Unicode编码，值是 0 - 65535 之间的整数

```js
// 返回对应下标字符的 Unicode 编码
console.log(str.charCodeAt(3)); // 99

console.log('a'.charCodeAt(0)); // a--97
console.log('z'.charCodeAt(0)); // z--122

console.log('A'.charCodeAt(0)); // A--65
console.log('Z'.charCodeAt(0)); // Z--90

console.log('0'.charCodeAt(0)); // 0--48
console.log('9'.charCodeAt(0)); // 9--57

console.log('彭作洪'.charCodeAt(0)); // 24429
console.log('彭作洪'.charCodeAt(1)); // 20316
console.log('彭作洪'.charCodeAt(2)); // 27946

// -----------------------------
// String.fromCharCode(编码)  将编码转成对应的字符
console.log(String.fromCharCode(24429, 20316, 27946)); // 彭作洪
```

![](D:\1009\day07\2笔记\e824b899a9014c08bcd720b8057b02087bf4f43b.jpg)

#### 4、indexOf和lastIndexOf

```js
// 查找字符在字符串中的位置，如果找到，返回下标，找不到，返回-1。（只查找一次）
// 字行串.indexOf(字符, 查找的起始位置);    从左向右找
// 字符串.lastIndexOf(字符, 查找的起始位置); 从右向左找

var str = 'welcome to js';

console.log(str.indexOf('o')); // 4
console.log(str.indexOf('o', 5)); // 9
console.log(str.indexOf('o', 10)); // -1
console.log(str.indexOf('O')); // -1  区分大小写
console.log(str.indexOf('ome')); // 4

// -------------------------
console.log(str.lastIndexOf('o')); // 9
console.log(str.lastIndexOf('o', 8)); // 4
```

```js
// 封装一个方法，用于字符串去重
var str = 'abcabsfsddsdsffdssafsafdsc';
console.log(fn(str)); // abc

function fn(str) {
    var newStr = ''; // 存储去重以后的字符
    for (var i = 0; i < str.length; i++) {
        if (newStr.indexOf(str[i]) === -1) {
            // 如果newStr里面没有str[i]，我们就把它加进来
            newStr += str[i];
        }
    }
    return newStr;
}
```

#### 5、字符串截取

```js
var str = 'welcome to js';
```

- substring

```js
// 字符串.substring(起始下标, 结束下标);
console.log(str.substring()); // welcome to js  没有参数，返回全部
console.log(str.substring(2)); // lcome to js  有一个参数，从第一个参数起，一直到最后
console.log(str.substring(2, 9)); // lcome t  有两个参数，从第一个参数处起，到第二个参数处止，不包括第二个参数的位置
console.log(str.substring(9, 2)); // lcome t  如果第二个参数比第一个参数小，则两个参数交换位置
console.log(str.substring(2, -9)); // we  负值当做0，然后应用上面的规则
```

- slice

```js
// 字符串.slice(起始下标, 结束下标);   建议使用
console.log(str.slice()); // welcome to js  没有参数，返回全部
console.log(str.slice(2)); // lcome to js  有一个参数，从第一个参数起，一直到最后
console.log(str.slice(2, 9)); // lcome t  有两个参数，从第一个参数处起，到第二个参数处止，不包括第二个参数的位置
console.log(str.slice(9, 2)); // ''  如果第二个参数比第一个参数小，则返回空字符串
console.log(str.slice(2, -3)); // 'lcome to'  负值和长度相加，然后应用上面的规则
```

- substr

```js
// 字符串.substr(起始下标, 截取的个数);
console.log(str.substr()); // welcome to js
console.log(str.substr(2)); // lcome to js
console.log(str.substr(2, 2)); // lc
console.log(str.substr(5, 2)); // me
console.log(str.substr(2, -5)); // '' 
```



#### 6、转大小写

```js
var str = 'abcdABD';

var s1 = str.toUpperCase(); // 转大写
console.log(s1);

var s2 = str.toLowerCase(); // 转小写
console.log(s2);
```



#### 7、字符串拆分和数组拼接

```js
// 字符串.split(参数);  以参数将字符串拆成数组
var str = '2020-10-12';
var arr = str.split('-');
console.log(arr); // [ "2020", "10", "12" ]
console.log(str.split('')); // ["2", "0", "2", "0", "-", "1", "0", "-", "1", "2"]
console.log(str.split()); // [ "2020-10-12" ]

// ----------------------------------------

// 以参数将数组拼接成字符串
// 数组.join(参数)
var arr = ["2020", "10", "12"];
console.log(arr.join('-')); // 2020-10-12
console.log(arr.join('')); // 20201012
console.log(arr.join()); // 2020,10,12
```



#### 8、replace替换

```js
// 字符串.replace(被替换的字符, 替换的字符)

var str = '13355556666'; // 133****6666
var s = str.replace('5555', '****');
console.log(s);
```



#### 9、trim去除字符串左右空格

```js
// 去除字符串左右空格。IE8及以下不支持（IE8及以下用正则）
// 字符串.trim();

var str = '   我是小王   ';
console.log(str.trim());
```



