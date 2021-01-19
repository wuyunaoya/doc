JavaScript中的流程控制语句和其他的程序设计语言基本是一样的，主要分为 :

- 顺序结构：即按顺序执行代码 ;
- 条件选择结构(分支语句)：包括 if-else 以及 switch;
- 循环结构：包括 for 循环，while，do-while,for-in 等;
- 其他语句： break 和continue。



## 1、分支语句

分支语句又叫**条件选择语句**，主要包括if-else、switch等，通过条件判断，有选择性的执行某段代码。



**if**

```js
if (条件) {
    如果条件为真，执行这里的代码
}

if (条件) {
    条件为真，执行这里
} else {
    条件为假，执行这里
}

if (条件1) {
    如果条件1为真，执行这里
} else if (条件2) {
    如果条件2为真，执行这里
} else if (条件3) {
    如果条件3为真，执行这里
} else {
    如果以上条件都不满足，执行这里
}
```

案例：开关灯、文字放大缩小、成绩等级划分

**switch**

```js
switch (表达式) {
    case 条件1:
        如果条件1和表达式完全相等，执行代码;
        break;
    case 条件2:
        如果条件2和表达式完全相等，执行代码;
        break;
    case 条件3:
        如果条件3和表达式完全相等，执行代码;
        break;
        ...
    default:
        如果以上条件和表达式都不相等，则执行这里
}
```

案例：星期、成绩等级划分



注意：当分支有三条及以上，用switch。否则用if-else



## 2、DOM元素获取

#### 1、通过ID获取元素

- 返回的是一个元素
- document.getElementById('id')

```js
var ul1 = document.getElementById('list1');
console.log(ul1);
```



#### 2、通过标签名获取元素

- 返回的是一个类数组（伪数组、集合），它有长度，可以通过下标获取某一个元素
- document.getElementsByTagName('标签名')
- 父级.getElementsByTagName('标签名')

```js
// 找到文档下面所有的li
var li = document.getElementsByTagName('li');
console.log(li);
console.log(li.length); // 有长度
console.log(li[0]); // 可以通过下标获取某一个

// 找到list2下面所有的li
var ul2 = document.getElementById('list2');
var li = ul2.getElementsByTagName('li');
console.log(li);

// 给list2下面所有的li添加一个背景
// li.style.backgroundColor = 'red';　// li是一个集合，只有具体的元素才能有样式
li[0].style.backgroundColor = 'red';
li[1].style.backgroundColor = 'red';
li[2].style.backgroundColor = 'red';
```



#### 3、通过class名获取元素(IE8及以下不支持)

- 返回的是一个类数组（伪数组、集合），它有长度，可以通过下标获取某一个元素
- document.getElementsByClassName('类名')
- 父级.getElementsByClassName('类名')

```js
var li = document.getElementsByClassName('abc');
console.log(li);
console.log(li[0]);

var ul2 = document.getElementById('list2');
var li = ul2.getElementsByClassName('abc');
console.log(li);
li[0].style.backgroundColor = 'red';
```



#### 4、通过css选择器获取元素(IE7及以下不支持)

- 通过css选择器获取元素(IE7及以下不支持)
- document.querySelector('css选择器'); 获取的是一个，从上向下找到的第一个
- document.querySelectorAll('css选择器'); 获取的是一组(类数组、伪数组)，有长度，可以通过下标获取某一个

```js
var li = document.querySelectorAll('li');
console.log(li); // 类数组、伪数组、集合
console.log(li.length); // 有长度
console.log(li[2]); // 可以通过下标获取某一个


var li = document.querySelectorAll('#list1 li');
console.log(li);

var li = document.querySelectorAll('#list1 .abc');
console.log(li);

var ul = document.querySelector('#list2');
console.log(ul);

var abc = document.querySelectorAll('.abc');
console.log(abc);
```





## 3、循环

循环的作用是让一段特定的代码执行指定的次数

#### 1、for循环

```js
for (1初始循环变量; 2循环条件(为真循环执行，为假循环停止); 4更新循环变量) {
    3要执行的代码
}

// 循环三要素：初始化循环变量，跳出循环的条件，更新循环变量。
// 在循环中必须有结束循环的条件，要更新循环变量，否则会成为死循环。
```

```js
for (var i = 1; i <= 3; i++) {
    console.log(i);
}
console.log(i);

// 第一轮：1 2 3 4
// 1、var i = 1
// 2、i <= 3   true
// 3、console.log(i);
// 4、i++   2

// 第二轮: 2 3 4 
// 2、i <= 3;  true
// 3、console.log(i);
// 4、i++   3

// 第三轮: 2 3 4 
// 2、i <= 3;   true
// 3、console.log(i);
// 4、i++   4

// 第四轮: 2
// 2、i <= 3;   false
```



#### 2、while循环

```js
1初始循环变量
while (2循环条件) {
    3执行代码
    4更新循环变量
}
```

```js
var i = 1;
while (i <= 3) {
    console.log(i);
    i++;
}

var i = 1;
for (; i <= 3;) {
    console.log(i);
    i++;
}
```

#### 3、do-while循环

不论条件满足不满足，它至少会执行一次

```js
1初始循环变量
do {
    2执行代码
    3更新循环变量
} while (4循环条件)

var i = 1;
do {
    console.log(i);
    i++;
} while (i <= 5);


// ------------------
// 即例条件不满足，也会执行一次
var i = 100;
do {
    console.log(i);
    i++;
} while (i <= 5);
```



#### 4、for-in

for-in它专门循环对象的

```js
for(var 变量 in 对象){
    console.log(变量);  key值
    console.log(对象[变量]);  value值
}
```

```js
var obj = {
    name: '张三',
    age: 3,
    fn: '前端开发'
};

// 访问对象的值
// console.log(obj.name); // 点的形式
// console.log(obj['name']); // 中括号的形式

// var n = 'name';
// console.log(obj[n]); // 中括号的形式访问，还可以使用变量

// -----------------------
for (var attr in obj) {
    console.log(attr, obj[attr]);
}
```



#### 5、break 与 continue

- break 与 continue 都是在循环中，终止循环的操作。
- break 是结束循环，后面的循环都不再执行（本次break后面的代码也不再执行）
- continue 是结束本次循环，即本次循环中 continue 以后代码都不再执行，直接执行下一次循环

```js
// 求1--100之间，除了30 45 55之外的所有5的倍数的和
var num = 0;
for (var i = 1; i < 100; i++) { // 1--100的数
    if (i % 5 === 0) { // 5的倍数
        // console.log(i);
        if (i === 30 || i === 45 || i === 55) { // 排除30 45 55
            continue;
        }
        num += i;
    }
}
console.log(num);
```















