## 1、获取节点

#### 1、节点树

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>

<body>
    <p>11111111</p>
    <ul id="ul1">
        <li>11111</li>
        <li>22222</li>
        <li>33333</li>
        <li>44444</li>
    </ul>
</body>

</html>
```

![](D:\1009\day09\2笔记\图片1.png)



#### 2、获取子节点

```html
<ul id="ul1">
    <li>11111</li>
    <li>22222</li>
    <li>33333</li>
    <li>44444</li>
</ul>
```

```js
// 父节点.childNodes  获取子节点，在标准浏览器，有可能获取换行节点，在IE8及以下，只获取元素节点
// 父节点.children    获取子节点，只获取元素类型的子节点(没有兼容性问题)

var ul = document.getElementById('ul1');
// var li = ul.childNodes;
var li = ul.children;

console.log(li);
```

#### 3、节点的基本属性

节点基本属性有nodeType, nodeName, nodeValue

````html
<p>11111111</p>
<ul id="ul1">
    <li>11111</li>
    <li>22222</li>
    <li>33333</li>
    <li>44444</li>
</ul>
````

```js
var p = document.getElementsByTagName('p')[0];
var ul = document.getElementById('ul1');
var li = ul.childNodes;
```

- nodeType

```js
// 节点类型：节点.nodeType  一共有12种 
// 元素节点：1      属性节点：2     文本节点：3       文档节点：9
// 作用：通过noddType，可以判断节点的类型
console.log(p.nodeType); // 1
console.log(ul.nodeType); // 1
for (var i = 0; i < li.length; i++) {
    console.log(li[i].nodeType);
}
```

- nodeName

```js
// 节点名称：节点.nodeName  
// 元素节点，返回大写的标签名
// 文本节点，返回#text

console.log(p.nodeName); // p
console.log(ul.nodeName); // UL
for (var i = 0; i < li.length; i++) {
    console.log(li[i].nodeName);
}
```

- nodeValue

```js
// 节点内容：节点.nodeValue
// 元素节点的内容：null    因为nodeValue认为这是文本节点的
// 文本节点的内容：就是这个文本的内容

console.log(p.nodeValue); // null
console.log(p.childNodes[0].nodeValue); // 11111111

// 推荐用：innerText  innerHTML
```



#### 4、其它节点

```html
<ul id="list">
    <li>11111</li>
    <li>22222</li>
    <li>33333</li>
    <li>44444</li>
</ul>
```

```js
var ul = document.getElementById('list');

// 1、通过父级获取第一个子节点
// 父级.fistChild   在标准浏览器下，有可能返回的是第一个文本节点，而在IE8及以下，返回第一个元素节点
// 父级.firstElementChild   在标准浏览器下，返回第一个元素节点，在IE8及以下，没有

// var first = ul.firstChild;
// var first = ul.firstElementChild;
var first = ul.firstElementChild || ul.firstChild;
first.style.backgroundColor = 'red';

// --------------------------
// 2、通过父级获取最后一个子节点
var last = ul.lastElementChild || ul.lastChild;
last.style.backgroundColor = 'blue';

// 3、获取下一个兄弟元素
var next = first.nextElementSibling || first.nextSibling;
next.style.backgroundColor = 'pink';

// 4、获取上一个兄弟元素
var prev = last.previousElementSibling || last.previousSibling;
prev.style.backgroundColor = 'green';
```



#### 5、属性操作

```html
<div id="box" title="我就是我" ab="我也来了">平头哥</div>
```

```js
var box = document.getElementById('box');

// 点和中括号的方式，只能操作原生的属性，而不能操作自定义的属性
// 点的方式
console.log(box.title);
box.title = '还差一个平头妹';
console.log(box.ab);

// 中括号的方式
console.log(box['title']);
box['title'] = '来一个平头妹';
console.log(box['ab']);

// -------------------------
// 可以操作自定义属性，也可以操作原生的属性（html结构里面可见）
// 获取：元素.getAttribute(属性名);
// 设置：元素.setAttribute(属性名, 值);
// 删除：元素.removeAttribute(属性名);

console.log(box.getAttribute('ab'));
box.setAttribute('ab', '又来一个平头妹');
box.removeAttribute('ab');

// --------------------
// 增加一个自定义的属性
box.setAttribute('aaa', '尹喆');
```









## 2、操作节点

#### 1、创建节点

- 创建标签节点：document.createElement('标签名');
- 创建文本节点：document.createTextNode('文本');

#### 2、添加节点

- 父级.appendChild(子级); 将子级添加到父级里面，放到最后

  ```js
  var body = document.getElementsByTagName('body')[0]; // 获取父级
  
  var div = document.createElement('div'); // 创建div
  // var text = document.createTextNode('我是被创建的'); // 创建文本
  // div.appendChild(text); // 文本添加到div中
  
  div.innerText = '我也是新来的';
  body.appendChild(div); // div添加到body中
  ```

  **案例：留言**

#### 3、插入节点

- 插入节点：父元素.insertBefore(要插入的节点, 参考的节点);

```html
<ul>
    <li>吃饭</li>
    <li class="ab">睡觉</li>
    <li>打豆豆</li>
</ul>
```

```js
// 父元素.insertBefore(要插入的节点, 参考的节点);

var ab = document.querySelector('.ab');

var li = document.createElement('li');
li.innerHTML = '盘它';

ab.parentNode.insertBefore(li, ab); // 将li添加到ab的前面，作为兄弟元素
```

#### 4、删除节点

- 删除节点：父元素.removeChild(被删除的元素)  返回被删除元素的引用，方便下次使用

```html
<ul>
    <li>吃饭</li>
    <li>睡觉</li>
    <li>打豆豆</li>
</ul>
```

```js
// 点击li，将它删除
var ul = document.getElementsByTagName('ul')[0];
var li = ul.querySelectorAll('li');

for (var i = 0; i < li.length; i++) {
    li[i].onclick = function () {
        var o = ul.removeChild(this); // o就是被删除的元素
        // console.log(o);

        setTimeout(function () {
            ul.appendChild(o);
        }, 3000);
    }
}
```

#### 5、替换节点

- 替换节点：父元素.replaceChild(新的节点, 被替换的节点);

  ```html
  <span>我就是我</span>
  <hr>
  <p>平头哥</p>
  <button>替换</button>
  ```

  ```js
  var body = document.body;
  var p = document.querySelector('p');
  var span = document.querySelector('span');
  var btn = document.querySelector('button');
  
  btn.onclick = function () {
      // body.replaceChild(p, span); // 利用页面中已有的元素来替换
  
      // 创建一个新元素来替换
      var div = document.createElement('div');
      div.innerText = '我是新来的';
      body.replaceChild(div, span);
  }
  ```

#### 6、复制节点(克隆)

- 复制节点：被复制的元素.cloneNode(参数布尔);

  - 默认只复制标签，不复制子孙节点，如果加参数true，则复制子孙节点

  ```html
  <button>复制</button>
  <ul>
      <li>吃饭</li>
      <li>睡觉</li>
      <li>打豆豆</li>
  </ul>
  ```

  ```js
  var body = document.body;
  var btn = document.querySelector('button');
  var ul = document.querySelector('ul');
  
  btn.onclick = function () {
      var o = ul.cloneNode(true); // ul复制一份
      body.appendChild(o);
  }
  ```



## 3、表格操作

DOM提供了可以简便快速获取表格元素的属性，先获取到表格table对象(oTab)，再通过table获取里面的元素，再通过 table 获取里面的元素



比如获取到了表格table为oTab：

thead-----oTab.tHead		一个

tfoot------oTab.tFoot 		一个

Tbody----oTab.tBodies	一堆

tr----------oTab.rows			一堆 

td----------oTab.tr.cells		一堆(必须通过tr来获取)



```js
var oTab = document.getElementsByTagName('table')[0]; // 获取表格盒子

var head = oTab.tHead; // 获取表格头 一个
head.style.backgroundColor = 'red';

var foot = oTab.tFoot; // 获取表格尾 一个
foot.style.backgroundColor = 'pink';

var tBody = oTab.tBodies; // 获取表格体  多个
// console.log(tBody);
tBody[1].style.backgroundColor = '#ccc';

var tr = tBody[1].rows; // 获取表格行 多个
tr[1].style.backgroundColor = 'green';

var td = tr[1].cells; // 获取这一行里面的列
// console.log(td);
td[1].style.backgroundColor = 'yellow';
```





