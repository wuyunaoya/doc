## 数组

#### 1、概念

使用单独的变量名来存储一系列的值。数组是可以存储**任意数据**类型的数据。



#### 2、数组创建

```js
// 1、字面量方式(推荐)
var arr = []; // 创建一个空数组
var arr = [1, 2, 3]; // 创建有内容的数组
var arr = [1, 'ab', true, null, undefined, [], {}, function () { }];
console.log(arr);

// 2、构造函数方式
var arr = new Array(); // 创建一个空数组
var arr = new Array(1, 2, 3);
var arr = new Array(3); // 参数3做为了数组的长度  [undefined, undefined, undefined]
var arr = new Array('3'); // ['3']
console.log(arr);
```



#### 3、数组的读和写

```js
var arr = ['刘备', '关羽', '张飞'];

// 读    数组[下标]
console.log(arr[0]);
console.log(arr[1]);
console.log(arr[2]);
console.log(arr[5]); // undefined   读取一个不存在的下标，返回undefined

// 写    数组[下标] = 值
arr[0] = '宗子恒'; // [ "宗子恒", "关羽", "张飞" ]
arr[5] = '尹喆'; // [ "刘备", "关羽", "张飞", undefined, undefined, "尹喆" ]  如果给不存在的下标写内容，则数组的长度相应的增加以适应新的项
console.log(arr);

// ---------------------
// 循环
for (var i = 0; i < arr.length; i++) {
    console.log(arr[i]);
}
```

#### 4、数组的长度

```js
var arr = ['刘备', '关羽', '张飞'];

// 读
console.log(arr.length); // 3 

// -----------------------------

// 写
arr.length = 5; //  增加两项，以适应新数组的长度
console.log(arr); // [ "刘备", "关羽", "张飞", undefined, undefined ]

arr.length = 1;
console.log(arr); // [ "刘备" ]   数组长度为1，以适应新数组的长度

// ----------------------------------------
// 字符串的长度，只读不写
var str = '平头哥';
str.length = 1;
console.log(str);


// --------------------------
// 如何尽快清空一个数组
arr.length = 0;
arr = [];
```



#### 5、栈方法

- 四个小宝贝

```js
var arr = ['刘备', '关羽', '张飞'];

// 共同点：都会修改原数组
// 添加的方法，都会返回新数组的长度
// 删除的方法，都会返回被删除的项

// 数组.push(参数); 将参数添加到数组的尾部（参数可以是多个），返回新数组的长度
var n = arr.push('尹喆', '平头哥');
console.log(arr); // [ "刘备", "关羽", "张飞", "尹喆", "平头哥" ]
console.log(n); // 5

// 数组.unshift(参数); 将参数添加到数组的头部（参数可以是多个），返回新数组的长度
var n = arr.unshift('平头哥');
console.log(arr);
console.log(n);

// 数组.pop(); 删除数组的最后一个（没有参数，一次只能删除一个），返回被删除的项
var n = arr.pop();
console.log(arr);
console.log(n);

// 数组.shift(); 删除数组的第一个（没有参数，一次只能删除一个），返回被删除的项
var n = arr.shift();
console.log(arr);
console.log(n);
```

- 强大的splice方法(能修改数组本身)

```js
// 强大的splice方法，它可以实现任意位置的添加 删除 替换，返回由删除的项组成的数组
// 数组.splice(操作的起始位置, 要删除几项, 要添加的元素);

var arr = ['刘备', '关羽', '张飞'];

// 删除
var n = arr.splice(1, 1);
console.log(arr);
console.log(n);

// 添加
var n = arr.splice(2, 0, '关平', '周仓');
console.log(arr); // [ "刘备", "关羽", "关平", "周仓", "张飞" ]
console.log(n); // []

// 替换
var n = arr.splice(1, 1, '关平', '周仓');
console.log(arr); // [ "刘备", "关平", "周仓", "张飞" ]
console.log(n); // [ "关羽" ]
```



#### 6、sort排序

```js
// 数组.sort(); 
var arr = [5, 3, 12, 7, 1, 8];

// arr.sort(); // 默认以字符串的方式排序，即便你写的是数字，也以字符串的方式排序
// console.log(arr); // [ 1, 12, 3, 5, 7, 8 ]

// ---------------------------------
// 接收一个比较函数，以数字进行比较
// 比较函数接收的两个参数，即数组中的任何意项
// 比较函数接收两个参数，如果第一个参数应该位于第二个之前则返回一个负数，如果两个参数相等则返回 0，如果第一个参数应该位于第二个之后则返回一个正数。
arr.sort(function (a, b) {
    // return a - b; // 从小到大
    // return b - a; // 从大到小
    return Math.random() - 0.5; // 无序排序
});
console.log(arr);
```

- 根据数组的某个属性排序

```js
// 按date进行降序排序，如果date一样，按DIU进行降序排序
var arr = [
    { "date": "2018-08-01", "DIU": 1209, "country": "US" },
    { "date": "2018-08-02", "DIU": 680, "country": "GB" },
    { "date": "2018-08-01", "DIU": 2311, "country": "CN" },
    { "date": "2018-08-02", "DIU": 879, "country": "US" },
    { "date": "2018-08-03", "DIU": 1525, "country": "CN" },
    { "date": "2018-08-02", "DIU": 1525, "country": "CN" }
];

// Date.parse接收一个时间字符串，返回时间戳
// console.log(Date.parse('2018-08-02')); // 1533168000000

arr.sort(function (a, b) {
    var t1 = Date.parse(a.date); // 获取时间戳
    var t2 = Date.parse(b.date);

    if (t1 === t2) {
        return b.DIU - a.DIU;
    } else {
        return t2 - t1;
    }
});

console.log(arr);
```

- 根据中文排序

```js
var arr = [
    { name: '武丽昕', num: 78 },
    { name: '汤文博', num: 38 },
    { name: '卢文博', num: 58 },
    { name: '邓钧键', num: 97 },
    { name: '刘继昂', num: 56 },
    { name: '阿军安', num: 78 },
    { name: '屈晓月', num: 98 },
    { name: '付秋萍', num: 79 }
];

// 按人名排序
arr.sort(function (a, b) {
    return a.name.localeCompare(b.name, 'zh');
});
console.log(arr);

// 按分数排序
arr.sort(function (a, b) {
    return b.num - a.num;
});
console.log(arr);
```

#### 7、排序算法

- 选择排序

```js
// 选择排序：从第一项起，每一项都和后面所有项依次比较，如果被比较项比当前项小，则两项交换位置。
// 每一轮都找到一个最小的值放到最前面

var arr = [5, 32, 2, 7, 45];
console.log(fn(arr)); // [2, 5, 7, 32, 45]

function fn(arr) {
    for (var i = 0; i < arr.length - 1; i++) {
        for (var j = i + 1; j < arr.length; j++) {
            if (arr[i] > arr[j]) {
                var temp = arr[i];
                arr[i] = arr[j];
                arr[j] = temp;
            }
        }
        console.log(arr.toString());
    }
    return arr;
}
```



- 冒泡排序

```js
// 冒泡排序：从第一项起，比较相邻的两个元素，如果前一个比后一个大，则交换位置。第一轮的时候最后一个元素应该是最大的一个。每一轮最后一个元素已经是最大的了，所以最后一个元素下一轮不用比较。

var arr = [5, 32, 2, 7, 45];
console.log(fn(arr)); // [2, 5, 7, 32, 45]


function fn(arr) {
    for (var i = 1; i < arr.length; i++) {
        for (var j = 0; j < arr.length - i; j++) {
            if (arr[j] > arr[j + 1]) {
                var temp = arr[j];
                arr[j] = arr[j + 1];
                arr[j + 1] = temp;
            }
        }
        console.log(arr.toString());
    }
    return arr;
}
```



- 快速排序

```js
// 找到数组的第一项，把它删除，然后循环数组，如果比第一项小的，放在一个left数组中，如果比第一项大的，放在一个right的数组中，然后递归调用上面的方法。
var arr = [4, 6, 2, 6, 5, 8, 4, 7, 3];
console.log(fn(arr)); // 

function fn(arr) {
    // 归的动作
    if (arr.length <= 1) {
        return arr;
    }

    var num = arr.shift(); // 删除数组的第一项，并返回被删除的这一项
    var left = [];
    var right = [];

    for (var i = 0; i < arr.length; i++) {
        if (arr[i] < num) {
            left.push(arr[i]);
        } else {
            right.push(arr[i]);
        }
    }
    return fn(left).concat(num, fn(right));
}
```



#### 8、数组其它方法

- concat

```js
// 数组.concat(参数); 参数可以是数组 元素 可以多个
// 返回拼接以后的数组(不修改数组本身)

var arr1 = [1, 2, 3];
var arr2 = ['a', 'b', 'c'];

// [1, 2, 3, 'a', 'b', 'c']

var arr = arr1.concat(arr2, '尹喆');
console.log(arr1);
console.log(arr2);
console.log(arr);

// ---------------------
// 推荐使用方法
var arr = [].concat(arr1, arr2, '尹喆');
console.log(arr);
```

- join



- reverse

```js
// 数组.reverse(); 翻转，会修改原数组

var arr = ['a', 'b', 'c'];
arr.reverse();
console.log(arr); // [ "c", "b", "a" ]
```

- indexOf和lastIndexOf

```js
// 数组.indexOf(item, 起始位置);
// 数组.lastIndexOf(item, 起始位置);
// IE8及以下不支持

var arr = [34, 3, 21, 3, 76, 4, 3, 4, 6];

console.log(arr.indexOf(3)); // 1
console.log(arr.indexOf('3')); // -1  证明判断相等，用 ===
console.log(arr.indexOf(3, 2)); // 3
console.log(arr.lastIndexOf(3)); // 6

// ---------------------------
// 封装一个类似于indexOf的方法，让IE8及以下实现indexOf
indexOf(arr, 3); // 1   数组 要查找的项
indexOf(arr, 3, 2); // 3   数组 要查找的项 起始下标
function indexOf(arr, item, index) {

}
```

案例：数组去重



- slice

```js
// 数组.slice(起始下标, 结束下标);
// 截取数组

var arr = [4, 6, 2, 6, 5, 8, 4, 7, 3];

console.log(arr.slice()); //  [ 4, 6, 2, 6, 5, 8, 4, 7, 3 ] 没有参数，返回全部
console.log(arr.slice(2)); // [ 2, 6, 5, 8, 4, 7, 3 ]  有一个参数，从第一个参数处起，到最后
console.log(arr.slice(2, 6)); // [ 2, 6, 5, 8 ]  有两个参数，从第一个参数处起，到第二个参数处止，不包括第二个参数
console.log(arr.slice(6, 2)); // [] 如果第一个参数比第二个大（非负数），则返回空数组
console.log(arr.slice(2, -3)); // [ 2, 6, 5, 8 ] 负数和长度相加，再应用上面的规则
```



- Array.isArray

```js
// Array.isArray(参数)
// 判断参数是否为数组，如果是，返回true，否则返回false
// IE8及以下不支持（封装一个方法，用于任何类数的数据判断）

console.log(Array.isArray(3)); // false
console.log(Array.isArray('ab')); // false

console.log(Array.isArray([])); // true
console.log(Array.isArray({})); // false
```



#### 9、数组迭代方法

IE8及以下都不支持

```js
// 参数：项 下标 数组本身
// 数组.forEach(function (item, index, array) { });
// 没有返回值，仅仅用代替for循环数组
var arr = ['刘备', '关羽', '张飞'];
arr.forEach(function (item, index, array) {
    console.log(item, index, array);
});
```

```js
// 参数：项 下标 数组本身
// 数组.map(function (item, index, array) { });
// 有返回值：返回由函数调用的结果组成的新数组
var arr = [3, 6, 4];
var n = arr.map(function (item, index, array) {
    // console.log(item, index, array);
    return item * 2;
});
console.log(n);
```

```js
// 参数：项 下标 数组本身
// 数组.filter(function (item, index, array) { });
// 有返回值，函数调用的结果为true，则将对应的item放到返回的数组中
var arr = [5, 76, 18, 9];
var n = arr.filter(function (item, index, array) {
    // console.log(item, index, array);
    return item > 10;
});
console.log(n);
```

```js
// 利用filter做数组去重
var arr = [1, 2, 3, 1, 2, 3];
var n = arr.filter(function (item, index, array) {
    return array.indexOf(item) === index;
});
console.log(n);
```

```js
// 参数：项 下标 数组本身
// 数组.every(function (item, index, array) { });
// 如果函数调用的每一项都返回true，则结果为true
var arr = [5, 76, 18, 9];
var n = arr.every(function (item) {
    return item > 3;
});
console.log(n);
```







