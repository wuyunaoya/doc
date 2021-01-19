## 1、javascript介绍

#### 1、什么是javascript

JavaScript 是一种**具有面向对象能力**的、**解释型**的**程序设计语言**。更具体一点，它是基于对象和事件驱动并具有相对安全性的客户端脚本语言。

#### 2、JavaScript的诞生

作者：布兰登·艾奇 ([Brendan Eich](https://baike.baidu.com/item/Brendan Eich))

年代：1995

公司：Netscape（网景） 

Javascript诞生记：http://www.ruanyifeng.com/blog/2011/06/birth_of_javascript.html



#### 3、javaScript和java的关系

没有任何关系（雷峰和雷峰塔的关系）



#### 4、JavaScript 的组成（三部分）

ECMAScript：语言的核心（定义变量、语句、语法、关键词等等）

DOM：document object model   （文档对象模型）

BOM：browser object model  （浏览器对象模型）



#### 5、ECMAScript和JavaScript

ECMAScript 和 JavaScript 的关系是，前者是后者的规格，后者是前者的一种实现。在日常场合，这两个词是可以互换的。



#### 6、JavaScript的特点

1、解释性

- 编译性：在代码执行之前，要将整个代码进行编译，编译完成之后，再交给计算机执行
- 解释性：在代码执行的时候，会逐行解释代码，解释完一行，就执行一行

2、基于对象

- js中存在一些事先设置好的对象（工具），这些对象可以提供给我们一些方法，来实现一些最基本的效果。

3、事件驱动

- 通过事件驱动来解决用户和浏览器页面之间的交互的问题

4、跨平台

- 各个操作系统只要能运行浏览器，就能运行js



## 2、javascript初识

#### 1、引入js

```html
<!-- 1、行内，不建议使用 -->
<div onclick="alert('点我吧')">我是小王</div>

<!-- 2、内嵌，工作中不建议使用 -->
<script>
    alert('我是内嵌的');
</script>

<!-- 3、外链 -->
<script src="js/a.js"></script>
注意1：script标签有了src属性，就不能再用作内嵌了
注意2：script标签可以放在页面的任何位置，但是我们推荐放在</body>的前面，也可以放在head标签里面
```



#### 2、入六三步曲

交互效果可以遵循简单三步曲来实现：

- 1找: 找到谁: document.getElementById("id名")
- 2加: 加什么事件（做什么操作）: 标签.事件
- 3做: 做什么事: 标签.事件 = function(){ 要做的事情 }

```html
<div id="box"></div>

<script>
    // 需求，点击box，弹出一句话

    // 1、找元素：document.getElementById(元素的id)
    // document文档  get得到  element元素 ById通过ID

    // 2、加事件：加什么事件（做什么操作）  元素.事件

    // 3、做什么事：元素.事件 = function (){ 要做的事 }

    document.getElementById('box').onclick = function () {
        alert('我就是我，不一样的烟火');
    }
</script>
```

#### 3、window.onload

window.onload是html页面以及页面引用的相关的css js 图片等等都加载完成之后再执行

我们可以把代码写在页面的任何地方

```js
window.onload = function () {
    document.getElementById('box').onclick = function () {
        alert('我就是我，不一样的烟火');
    }
}
```

#### 4、鼠标事件

- onclick ：点击事件
- ondblclick ：双击事件
- onmouseover ： 鼠标移入元素
- onmouseout :  鼠标离开元素
- onmouseenter ：鼠标移入元素
- onmouseleave ：鼠标离开元素
- onmousemove:  鼠标在元素中移动
- onmousedown： 鼠标按下
- onmouseup： 鼠标抬起
- oncontextmenu ：鼠标右键菜单事件

```js
// 点击
document.getElementById('box').onclick = function () {
    console.log('点了我');
}

// 双击
document.getElementById('box').ondblclick = function () {
    console.log('双击了');
}

// 鼠标滑上  mouse鼠标  over滑上
document.getElementById('box').onmouseover = function () {
    console.log('滑上了');
}

// 鼠标滑离  mouse鼠标  over滑上
document.getElementById('box').onmouseout = function () {
    console.log('滑离了');
}

// 滑动 鼠标在元素上滑动时，会不断的触发这个事件
document.getElementById('box').onmousemove = function () {
    console.log('滑动');
}

// 鼠标按下
document.getElementById('box').onmousedown = function () {
    console.log('按下');
}

// 鼠标抬起
document.getElementById('box').onmouseup = function () {
    console.log('抬起');
}

// 滑上 （同onmouseover有区别）
document.getElementById('box').onmouseenter = function () {
    console.log('滑上');
}

// 滑离
document.getElementById('box').onmouseleave = function () {
    console.log('滑离');
}

// 点击右键触发(上下文菜单  环境菜单)
document.getElementById('box').oncontextmenu = function () {
    console.log('点了右键');
}
```



#### 5、变量

变量是对“值”的具名引用。变量就是为“值”起名，然后引用这个名字，就等同于引用这个值。变量的名字就是变量名。

- 格式：var 变量名 = 值;

```js
// 1、声明并赋值
var a = 10;
console.log(a);

// 2、先声明，再赋值
var b; // 声明
b = '老王'; // 赋值
console.log(b);

// 3、一次声明多个
var userName = '小王',
    age = 3,
    fn = '前端开发',
    sex;
console.log(userName, age, fn, sex);
```

变量名的命名规则：

- 1、只能包含英文、数字、下划线、$
- 2、不能以数字开头
- 3、不能使用关键字、保留字

建议：

- 1、见名知义 sex age name number num
- 2、小驼峰命名 fontSize userName



关键字：就是js这门语言现在正在使用的字。

保留字：js这门语言是发展的，将来可能要用到的就是保留字



#### 6、变量拼接

- 1、删除要替换的内容
- 2、在删除的地方写两引号
- 3、在引号之间写两加号
- 4、在加号之间，写你的变量名

```js
var name = '小王';
var age = 3;
var sex = '男';
var from = '武汉';

// console.log('我是xx，我今年xx岁，我是xx孩子，我来自xx');
console.log('我是' + name + '，我今年' + age + '岁，我是' + sex + '孩子，我来自' + from);
```

#### 7、注释

// 单行注释    ctrl+/

/* 多行注释 */   ctrl+shift+/



#### 8、调试命令

JavaScript中调试命令，用于调试代码，查看数据信息，常用的调试命令有alert()与console.log()。

- alert命令直接在页面弹出信息，一次只能显示一个数据，并且没有点击确定之前，不能显示下一个数据。
- console.log命令，在控制器台打印数据，一次可以打印多个，并且不会堵塞。



## 3、javascript元素操作

#### 1、内容操作

##### 1、操作表单元素内容

- 设置：元素.value = 值; 
- 获取：元素.value; 

```html
<input type="text" id="txt">
<button id="btn1">设置内容</button>
<button id="btn2">获取内容</button>
```

```js
// 1、获取元素
var txt = document.getElementById('txt');
var btn1 = document.getElementById('btn1');
var btn2 = document.getElementById('btn2');
// console.log(txt, btn1, btn2);

// 2、设置内容
btn1.onclick = function () {
    txt.value = '谁在看电影？';
}

// 3、获取内容
btn2.onclick = function () {
    console.log(txt.value);
}
```

案例：解密



##### 2、操作闭合标签内容

**innnerHTML**识别标签

- 获取：元素.innnerHTML
- 设置：元素.innnerHTML = 值; 会覆盖原有的内容

**innerText**不识别标签

- 获取：元素.innerText
- 设置：元素.innnerText = 值; 会覆盖原有的内容

```html
<div id="txt">我就是我，<strong style="color:red;">不一样</strong>的烟火</div>
<button id="btn1">按钮1</button>
<button id="btn2">按钮2</button>
```

```js
var txt = document.getElementById('txt');
var btn1 = document.getElementById('btn1');
var btn2 = document.getElementById('btn2');
// console.log(txt, btn1, btn2);

// 获取
btn1.onclick = function () {
    console.log(txt.innerHTML);
    console.log(txt.innerText);
}

// 设置
btn2.onclick = function () {
    // txt.innerHTML = '平<b>头</b>哥';
    txt.innerText = '平<b>头</b>哥';
}
```







#### 2、属性操作

点的形式

- 获取：元素.属性名
- 设置：元素.属性名 = 值

中括号的形式

- 获取：元素['属性名']
- 设置：元素['属性名'] = 值

```js
var box = document.getElementById('box');

console.log(box.title); // 获取
console.log(box['title']);

box.title = '平头哥'; // 设置
box['title'] = '平头哥';

// 中括号的形式比点的要强大，如果是变量，就不能用点的形式了，只能用中括号的形式
var t = 'title';
console.log(box[t]);
```

案例：开关灯



**class的操作**

- 获取：元素.className
- 设置：元素.className = 值



#### 3、样式操作

- 设置：元素.style.样式名 = 值;  最终都成为行间的样式
- 获取：元素.style.样式名;  只能获取行间的样式

```html
<div id="box" style="border: 10px solid #ccc;">平头哥</div>
```

```js
var box = document.getElementById('box');

// 设置样式
box.style.width = '100px';
box.style.height = '100px';
box.style.backgroundColor = 'red';
box.style.fontSize = '30px';
box.style.color = 'white';

console.log(box.style.color); // 获取样式
```

```js
// 元素.style.cssText = ''   会覆盖原来行间的
box.style.cssText = 'width:100px;height:100px; background-color: red; font-size: 30px; color: yellow;';
```





