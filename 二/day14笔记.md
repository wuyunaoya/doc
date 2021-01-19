## 1、面向对象的概念

**对象**：无序的名值对

```js
{
    key1: value1,
    key2: value2,
    ...
}
```



**开发模式**：过程式    面向对象（OOP编程）



**面向对象基本概念：**

**类：类是对象的类型模板**，例如，定义Student类来表示学生，类本身是一种类型，Student表示学生类型，但不表示任何具体的某个学生

**实例：实例是根据类创建的对象**，例如，根据Student类可以创建出小明、小花等多个实例，每个实例表示一个具体的学生，他们全都属于Student类型。

**面向对象编程**，就是编写类（模具），让类产生实例（月饼）

![](D:\1009\day13\2笔记\类和实例.jpg)



**对象的组成**：由属性和方法组成

- 属性：对象的特征描述，静态，名词（不是函数的就是属性）

- 方法：对象的行为，动态（就是函数）



**对象的读写**

```js
var obj = {
    name: '小尹',
    age: 3,
    job: '前端开发',
    eat: function () {
        console.log(this);
        console.log('吃东西');
    }
}

// 读
console.log(obj.name);
console.log(obj['age']);

// 方法调用   方法中有this是谁，关键要看怎么调用的
obj.eat(); // obj
var v = obj.eat;
v(); // window

// ----------------------------
// 写
obj.name = '喆人'; // 写原来存在的，就覆盖
obj.sex = '不明'; // 原来不存在的，则添加
console.log(obj);
```



- 当我们试图访问一个不存在的属性时，会返回undefined。
- 我们也可以使用in操作符来判断属性是否存在。
- 另外，我们也可以通过delete操作来删除某个属性。

```js
var obj = {
    name: '小尹',
    age: 3,
    job: '前端开发',
    eat: function () {
        console.log(this);
        console.log('吃东西');
    }
}

delete obj.job; // 删除某个属性
console.log(obj);

// -------------------------
// 判断某个属性有没有，只问有没有，不问值
// 如果有，返回true，如果没有，返回false;
console.log('name' in obj); // true 这个属性在对象中存在 
console.log('fff' in obj); // false 没有这个属性


// -------------------------
// 对象遍历
for (var attr in obj) {
    console.log(attr, '----', obj[attr]);
}
```



## 2、面向对象的创建

#### 1、字面量创建

```js
// 字面量方式创建
// (不用模具，直接用手捏一个月饼。)
// 问题：如果创建多个，会有代码冗余
var obj = {
    name: '张三',
    age: 3,
    fn: function () {
        console.log(this.name);
    }
};
obj.fn();

var obj2 = {
    name: '李四',
    age: 5,
    fn: function () {
        console.log(this.name);
    }
}
```

#### 2、实例创建

```js
// 实例创建对象
// (不用模具，直接用手捏一个月饼。)
// 问题：如果创建多个，会有代码冗余
var obj = new Object(); // {}  实例
obj.name = 'zs';
obj.age = 3;
obj.fn = function () {
console.log(this.name);
}
// console.log(obj);

obj.fn();
```

#### 3、工厂模式

```js
// 工厂模式：归根到底是封装函数
function person(name, age) {
    // 1、准备原料
    var obj = new Object();

    // 2、加工
    obj.name = name;
    obj.age = age;
    obj.showName = function () {
        console.log(this.name);
    }

    // 3、出厂
    return obj;
}

var p1 = person('小王', 3);
console.log(p1);

var p2 = person('xl', 5);
console.log(p2);
```

**instanceof**

```js
// 不足：那就是识别问题，因为根本无法搞清楚他们到底是哪个对象的实例（即是哪个创建的）。

// 实例 instanceof 函数  判断这个实例是否由这个函数创建
console.log([] instanceof Array); // true  数组是由Array创建的
console.log([] instanceof Object); // true  数组是由Object创建的


console.log(p1 instanceof person); // false
```



#### 4、构造函数创建

构造函数的特点：（跟工厂模式对比）

● 构造函数名首字母大写(为了区分普通函数，不是必须，是约定)

● 构造函数方法没有显示的创建对象(new Object())

● 直接将属性和方法赋值给this对象

● 没有return语句，不需要返回对象

● 通过构造函数创建对象，必须使用new运算符(直接调用跟普通函数一样)

```js
// 构造函数创建
function Person(name, age) {
    this.name = name;
    this.age = age;
    this.showName = function () {
        console.log(this.name);
    }
}


// 要创建 Person 的新实例，必须使用 new 操作符。以这种方式调用构造函数实际上会经历以下 4个步骤：
// (1) 创建一个新对象；
// (2) 将构造函数的作用域赋给新对象（因此 this 就指向了这个新对象）；
// (3) 执行构造函数中的代码（为这个新对象添加属性）；
// (4) 返回新对象。
var p1 = new Person('张三', 3);
console.log(p1);

var p2 = new Person('ls', 5);
console.log(p2);
```

```js
// 好处：解决了工厂模式不能识别的问题
console.log(p1 instanceof Person); // true
console.log(p1 instanceof Object); // true

// 不足：如果创建多个对象，会创建多个函数，这样占内存
alert(p1.showName);
alert(p2.showName);
alert(p1.showName == p2.showName); // false
```

**对象的比较**

```js
// 基本类型的比较：值的比较
// 引用类型的比较：地址的比较

console.log(5 == 5); // true
console.log([] == []); // false
```

#### 5、原型创建对象

##### 1、原型、原型链

- 原型：js每声明一个function，都有prototype原型，prototype原型是函数的一个默认属性，在函数的创建过程中由js编译器自动添加。原型中存储对象共享的属性和方法。 （原型默认会有一个constructor的属性，这个属性又指向构造函数）

- 原型链：当你定义一个函数对象的时候，其内部就有这样一个链表关系。声明foo对象，自带了proto的属性，而这个属性指向了prototype，从而实现对象的扩展（例如继承等操作）。(当对象查找属性的时候，会先找自己，如果自己没有，则会顺着proto找到它的原型，如果原型有，则找到返回，如果原型没有，则继续顺着proto找到上一级原型，一直到Object.prototype，如果再找不到，则返回undefined)




```js
var arr = new Array();

console.log(Array.prototype); // {}  原型中存储对象共享的属性和方法。
console.log(Array.prototype.constructor); // Array  constructor又指向构造函数

console.log(arr.__proto__); // 通过实例访问原型

console.log(Array.prototype === arr.__proto__); // true
```

**构造函数、原型、实例三者关系**

![](D:\1009\day13\2笔记\构造函数、原型、实例三者关系.jpg)

##### 2、原型创建对象

```js
function Person() { }

// 这个Person会有一个原型，原型默认会有constructor属性
// {
//     constructor: Person
// }

Person.prototype.name = '张三'
Person.prototype.age = 3;
Person.prototype.showName = function () {
    console.log(this.name);
}

var p1 = new Person();
// console.log(p1);

console.log(p1.name); // 张三
console.log(p1.toString);
console.log(p1.aaa); // undefined


var p2 = new Person();
// console.log(p2);
console.log(p2.name); // 张三

// 1、解决了构造函数的不足
console.log(p1.showName === p2.showName); // true

// 问题：不能传参
```

![](D:\1009\day13\2笔记\原型链.jpg)

#### 6、混合模式创建对象

```js
// 混合模式创建(构造+原型)
// 公共的方法或属性，写在原型上面，自己的写在构造函数里面

// 创建对象的标准方法

function Person(name, age) {
    this.name = name;
    this.age = age;
}
Person.prototype.showName = function () {
    console.log(this.name);
}

var p1 = new Person('张三', 3);
console.log(p1);
console.log(p1.name);
p1.showName();
console.log(p1.toString);
```

#### 7、动态混合模式

好处：给人代码封装的感觉

```js
function Person(name, age) {
    this.name = name;
    this.age = age;
    if (typeof (Person.prototype.showName) !== 'function') {
        Person.prototype.showName = function () {
            console.log(this.name);
        }
        Person.prototype.showAge = function () {
            console.log(this.age);
        }
    }
}

var p1 = new Person('zs', 3);
console.log(p1);

var p2 = new Person('ls', 5);
console.log(p2);
```



## 3、面向对象的实例

**面向对象的选项卡**   **打地鼠**

原则：先写出普通的写法，然后改成面向对象写法

1、普通方法变型

尽量不要出现函数嵌套函数

可以有全局变量

把onload中不是赋值的语句放到单独函数中（init）

2、改成面向对象（）

​	先写构造函数

onload中创建对象，并init调用

全局变量就是属性

函数就是方法

(属性和方法前面，都要加this)

改this指向问题（尽量让this指向对象）

 

注意：this指向是这里的重点

演示时先把所有的this指向改了，然后再看报错，一步一步改。要一步一步分析this都指向谁了。

在事件或者定时器调用时，this指向特别容易出错。一定要注意（复习this的指向）

另外，还要注意event对象，它只能出现在事件函数里面。

阻止默认事件，也要出现在事件函数中。

 

结论：我们改成面向对象了之后，感觉是不是更复杂了？确实是这样，确实是更复杂了，但是我们这个面向对象特别适合复杂的开发，对于简单的，不太推荐使用面向对象。面对复杂开发时，它特别容易扩展，同时，复用性特别强。上面的例子，多添加几个，就可以发现特别方便复用和扩展。





## 4、命名空间

一般名字都是见名知意的，但是如果代码足够复杂，或者使用了很多的第三方框架和插件，变量名不够用了，我们可以使用命名空间即把同一类方法包在一起。

命名空间的实质是：只定义一个全局变量，并将其它变量和方法定义为该变量的属性。

```js
// 全局变量会导致冲突
var a = 10;
// .......很多代码
var a = 5;
```

```js
// 命名空间
var U = {}; // 全网站的唯一全局变量

// 只需要在需要全局变量，但是又不能设置全局变量时，可以放在以自己名为空间的对象里面
U.sqj = {}; // 小宋同的开发空间
U.sqj.a = 10;

U.jhf = {}; // 小金同学的开发空间
U.jhf.a = 5;

console.log(U.sqj.a);
console.log(U.jhf.a);
```





## 5、call、apply

#### 1、call 和 apply

- 语法：函数.call(新的this指向, 参数1, 参数2, ...);
- 语法：函数.apply(新的this指向, [参数1, 参数2, ...]);
- 作用：调用函数，并修改函数中的this
- 区别：后续的参数传入不同，call是一个一个传入，而apply是以一个数组的形式传入
- 注意：如果第一个参数为null或undefined，则函数的this还是window

```js
function fn(a, b) {
    console.log(this);
    console.log(a, b);
}
var obj = {
    name: 'zs',
    age: 3
}
```

```js
fn(3, 5);
fn.call(obj, 5, 6);
fn.apply(obj, [7, 8]);
```

**apply实例**

```js
var arr = [5, 2, 6, 3, 5, 87, 8];
// 找数组中的最大值

// Math.max()  必须接收一个一个参数，
// 函数.apply(新的this指向, [参数1, 参数2, ...])

console.log(Math.max.apply(Math, arr)); // 87
console.log(Math.min.apply(Math, arr)); // 2
```



#### 2、bind

- 语法：函数.bind(新的this指向);   IE8及以下不支持
- 作用：修改函数中的this指向，返回修改以后的函数的引用
- 同call和aply的区别：call和apply是调用函数，bind是返回修改函数this以后的引用

多种调用方式

```js
var v = fn.bind(obj, 4, 5);
v();

var v = fn.bind(obj);
v(6, 7);

fn.bind(obj)(9, 8);

fn.bind(obj, 1)(2);
```



## 6、面向对象的继承

#### 1、原型链继承

```js
// 父类(超类)
function Student() {
    this.job = '学生';
    this.ah = ['跑步', '唱歌', '睡觉'];
}
Student.prototype.showJob = function () {
    console.log(this.job);
}

// 子类
function SmallStudent() {
    this.name = '小王';
}

// 原型链继承：将父类的实例，赋给子类的原型（一句话实现继承）
SmallStudent.prototype = new Student();

var s1 = new SmallStudent(); // 子的实例
console.log(s1);
s1.ah.push('学习'); // 如果继承了引用类型，会一改全改，一个实例对象改变了引用类型的数据，后面再创建出来的实例对象就已经是改过之后的数据。
console.log(s1.ah);

var s2 = new SmallStudent();
console.log(s2.ah);
```

![](D:\1009\day13\2笔记\原型链继承.jpg)



#### 2、对象冒充继承

```js
// 构造器借用法
// 父类(超类)
function Student() {
    this.job = '学生';
    this.ah = ['跑步', '唱歌', '睡觉'];
}
Student.prototype.showJob = function () {
    console.log(this.job);
}

// 子类
function SmallStudent() {
    Student.call(this); // 在子类的构造函数中，调用父类的构造函数，用call改this指向
    this.name = '小王';
}

var s1 = new SmallStudent(); // 实例
console.log(s1);
console.log(s1.name);
console.log(s1.job);
s1.ah.push('学习');
console.log(s1.ah);

// 不足，只能继承父类构造函数上的属性，而不能继承父类原型上的方法
// s1.showJob();

var s2 = new SmallStudent();
console.log(s2.ah);
```

![](D:\1009\day13\2笔记\对象冒充继承.jpg)



#### 3、组合继承（原型链+对象冒充）

```js
// 组合继承：对象冒充继承父类构造函数上的属性，原型链继承原型上的方法

// 父类(超类)
function Student() {
    this.job = '学生';
    this.ah = ['跑步', '唱歌', '睡觉'];
}
Student.prototype.showJob = function () {
    console.log(this.job);
}

// 子类
function SmallStudent() {
    Student.call(this); // 对象冒充继承
    this.name = '小王';
}
SmallStudent.prototype = new Student(); // 原型继承
SmallStudent.prototype.showName = function () { // 再添加自己原型上的方法
    console.log(this.name);
}

var s1 = new SmallStudent();
console.log(s1);

console.log(s1.ah);
s1.showName();
s1.showJob();

// 问题：
// 1、会两次调用父类的构造函数
// 2、同名的属性，即存在于实例上，又存在于原型上，完全没有必要
```

![](D:\1009\day13\2笔记\组合继承.jpg)



#### 4、寄生组盒继承（标准方法）

```js
// 父类(超类)
function Student() {
    this.job = '学生';
    this.ah = ['跑步', '唱歌', '睡觉'];
}
Student.prototype.showJob = function () {
    console.log(this.job);
}

// 子类
function SmallStudent() {
    Student.call(this); // 对象冒充继承
    this.name = '小王';
}
inherits(SmallStudent, Student); // 代替四句话
// 再添加自己原型上的方法
SmallStudent.prototype.showName = function () {
    console.log(this.name);
}

var s1 = new SmallStudent();
console.log(s1);


function inherits(Child, Parent) {
    var F = function () { };
    F.prototype = Parent.prototype;
    Child.prototype = new F();
    Child.prototype.constructor = Child;
}
```

![](D:\1009\day13\2笔记\寄生组合继承.jpg)

