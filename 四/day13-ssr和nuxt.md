# 一.ssr(服务端渲染)

## 1.定义

server side render:简称服务端渲染.即将组件或者页面通过服务端渲染,最后生成HTML字符串,发送给浏览器,浏览器再将字符串展示为客户端所识别的应用程序.

## 2.ssr的利弊

优势

```
1.利于SEO优化,用户体验好
2.首屏加载速度快.
```

弊端

```
1.增加服务端的解析压力
2.基于node.js
```

核心

```
核心就是:做服务端解析,生成HTML字符串返回给客户端.
```



## 3.使用

```
npm i express --save   安装express模块

npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm install vue vue-server-renderer --save

```

```js
//1.引入express
const express = require('express')
const server = express()

//2.创建一个vue实例
const Vue = require('vue')
const vm = new Vue({
    data:{
        msg:'使用服务端渲染',
        arr:['洪山区','江夏区','武昌区']
    },
    template:`
            <div>
                <h3>{{msg}}</h3>
                <ul>
                    <li v-for="item in arr" :key="item">{{item}}</li>
                </ul>
            </div>
    `
})

//3.创建服务端渲染
const render = require('vue-server-renderer').createRenderer()

//4.渲染页面和数据
//配置路由
server.get('/index',(req,res)=>{
    // 渲染页面
    render.renderToString(vm,(err,html)=>{
        if(err){
            res.send('服务端渲染失败')
            return
        }
        res.send(html)
    })
})


//监听服务端端口
console.log('你的服务器运行在3000');
server.listen(3000)
```



# 二.nuxt

官网:https://www.nuxtjs.cn/

## 1.定义

使用简便的 Vue 框架,封装

## 1.安装

```
npm i create-nuxt-app -g   全局安装nuxt
```

## 2.目录介绍

```
-assets   静态资源文件css img  js
			在nuxt.config.js中引入 css: [
                 '~/assets/css/reset.css'
              ],
              静态资源参与打包
components:公共组件   文件名称不能修改
layouts  : 页面布局    文件名称不能修改
			default.vue   是默认布局
middleware 中间件
pages:  你的代码
plugins:  插件
static : 静态资源  css img js  引入图片在开发环境下无法显示
			不参与打包
store  :状态管理
nuxt.config.js   配置文件

```



# 三.ts(typescript)

## 1.介绍

```
TypeScript是一种由微软开发的自由和开源的编程语言。
它是JavaScript的一个超集，并且可以编译为纯JavaScript，而且本质上向这个语言添加了可选的静态类型和基于类的面向对象编程，通俗的理解为JavaScript的一个特殊版本，其语法规范严谨，适用于开发大型项目运用。更有甚者描述，es的最终走向规范都将会是TypeScript。
```

核心:对值所具有的结构进行类型检查.

官网:https://www.tslang.cn/

## 2.安装

```
npm i typescript -g  全局安装
```

## 3.自动编译

1.新建目录demots

2.在当前目录下执行 tsc --init   创建一个tsconfig.json文件

3.tsconfig.json中做配置

```js
{
  "compilerOptions": {
       "outDir": "./dist",//开启
  },
  "include":["./src"]//新增
}
```

4.自动编译:  vscode终端->运行任务->typescript->监听tsconfig.json

## 4.变量的定义

```ts
定义一个变量
// 1.值是什么类型,变量就是什么类型
let num = 10;
// num = '20';

// 2.定义是什么类型,赋值就是什么类型
let num1:number = 20;//[推荐写法]

//3. 声明变量的数据类型,
let num2:number;
num2 = 30;
console.log(num2);
```

string number boolean

```ts
// string
let str:string = 'hello';
// number
let num3:number = 888;
//boolean
let bool:boolean = false;
```

数组

```ts
// 数组
let arr:[] = [];//声明一个空数组,值就是空
// arr = [1,2,3];//b不能修改空数组
let arr1:number[] = [1,2,3,4];//指定一个number类型的数组
let arr2:string[] = ['a','b','c'];//指定一个string类型的数组
```

元祖

```ts
// 元祖
// 数量不能多,也不能少,而且数据类型还得匹配上
let arr3:[number,string,boolean] = [1,'a',true];
```

enum枚举类型(名称可以是自定义的)

```ts
// 枚举  规定枚举类型首字母大写
// 枚举类型:在没有指定值得情况下,下标就是其对应的值
enum Sex{
    man,
    women
}
// 
let s1:Sex = Sex.man;
let s2:Sex = Sex.women;

// 设置枚举类型并且指定值
enum Method{
    get = "get",
    post = "post",
}

let m1:Method = Method.get;
let m2:Method = Method.post;


//订单
enum OrderStatus{
    consignment = '待发货',
    shipped = '已发货',
    evaluated = '已评价',
}

let o1:OrderStatus = OrderStatus.consignment;
let o2:OrderStatus = OrderStatus.shipped;
let o3:OrderStatus = OrderStatus.evaluated;
console.log(o1,o2,o3);
```

任意类型 any

```ts
// any  1.后端返回给前端的数据any,  2.dom元素节点可以是any
let  a:any = 10;
a = '123';
a = false;
a = [1,2,3];
window.onload = function(){
    a = document.getElementById('main');
    console.log(a);
}
```

void没有返回值

```ts
// void
function add():void{
    console.log('该函数没有返回值');
}
add()
```

object

```ts
//object
let obj:object = {}
obj = {
    name:'王一博',
    age:25,
    sex:'男'
}

let obj1:object[] = []
obj1 = [
    {
        id:1,
        name:'小王'
    }
]
// obj1 = [1,2,3]//报错
console.log(obj1);
```

undefined

```ts
//undefined
let u:number | undefined;
console.log(u);
```



## 5.函数的定义

定义

```ts
// 定义一个函数  参数和返回值都要有数据类型
function add1(num:number,num1:number):number{
    return num + num1
}

//只是调用做运算
function add2(a:number,b:number):void{
    console.log(a*b);
    
}
console.log(add1(30,40));
add2(666,777)
```

默认参数

```ts
// 默认参数
// 默认参数一般放在形参的最后
function add3(a:number,b:number = 10):number{
    return a + b
}
// console.log(add3());
console.log(add3(10));
console.log(add3(10,30));
```

可选参数 (形参后面加?) 

```ts

// 可选参数
// 可选参数放在参数的最后
function add4(a:number,b?:number):number{
    if(b){
        return a * b
    }else{
        return a + a
    }
}
```

剩余参数

```ts
// 剩余参数
function add5(a:number,...sheng:number[]):void{
    console.log(sheng);
    
}

function add6(a:number,...child:number[]):number{
    let sum = 0
    child.forEach(item=>{
        sum += item
    })
    return a + sum
}
```

箭头函数

```ts
// 箭头函数
let priceFilter = (price:number)=>price.toFixed(2)
```



## 6.类的定义

定义类

```ts
// 定义一个类
// 规定类名的首字母要大写
/**
 * 1.类中有属性和方法
 * 2.属性需要指定类型
 * 3.方法中参数和返回值都要指定数据类型
 */
class Person{
    user:string = '张三';
    // 构造函数
    constructor(name:string){
        this.user = name;
    }
    walk():void{
        console.log(this.user);
        
    }
}
let p1 = new Person('小王')
p1.walk()
```

继承

```ts
// 继承
class Animal{
    name:string;
    constructor(name:string){
        this.name = name
    }
    walk(k:number):void{
        console.log(this.name+'行走了'+k+'km');
        
    }
}

class Dog extends Animal{
    age:number;
    constructor(name:string,age:number){
        super(name)
        this.age = age
    }
    walk():void{
        // 调用父类的方法
        super.walk(4)
        console.log(this.name+'行走了8m');
        
    }
}

let taidi = new Dog('泰迪',4)
taidi.walk()
```

类修饰符:public protected private

```ts
public 修饰的属性在类内 类外 子类都可以被访问
class Car{
    public name:string;
    constructor(name:string){
        this.name = name
    }
    move():void{
        // 在类内可以被访问到
        console.log(this.name+'跑了100公里');
        
    }
}
class Bus extends Car{
    constructor(name:string){
        super(name)
    }
    move():void{
        // 在子类可以被访问
        console.log(this.name+'跑了80公里');
        
    }
}

let c = new Car('特斯拉');
// 在类外可以被访问
// console.log(c.name);
// c.move()

let b = new Bus('11路公交车')
b.move()
```

```ts
//protected  在类内 子类中可以被访问  在类外不能被访问
class People{
    protected name:string;
    constructor(name:string){
        this.name = name
    }
    say():void{
        // 在类内可以访问
        console.log(this.name+'说:明天是平安夜');
    }
}

class Man extends People{
    constructor(name:string){
        super(name)
    }
    say():void{
        // 在子类中可以被访问
        console.log(this.name+'后天是圣诞节');
        
    }
}
let p1 = new People('赵丽颖')
// 不能再类外访问
// console.log(p1.name);
// p1.say()

let p2 = new Man('萌萌')
p2.say()
```

```ts
private 在类内可以被访问 在类外和子类不能被访问
// private
class TuXing{
    private length:string;
    constructor(length:string){
        this.length = length
    }
    private getChang():void{
        // 在类内可以被访问
        console.log(this.length);
        
    }
}

class Chang extends TuXing{
    width:string;
    constructor(length:string){
        super(length)
        this.width = length
    }
    getWidth():void{
        // 在子类中不能访问
        console.log(this.length);
        
    }
}

let t1 = new TuXing('20')
// 在类外不能被访问
// console.log(t1.length);
// t1.getChang()
```



## 7.静态属性

```ts
// 静态属性  static
//静态属性,定义好之后,值就存在了
class Util{
    static name1:string = '工具类';
    static getRand(min:number,max:number):number{
       return Math.floor(Math.random()*(max-min)+min)
    }
}
console.log(Util.name1);
console.log(Util.getRand(1,10));
```



## 8.抽象类

```
1.抽象类中可以没有抽象方法,
2.抽象方法必须定义在抽象类中.
3.抽象类中的方法不去实现任何操作,只是定义.实现必须在子类中来实现.
```

```ts
// 抽象类 abstract
//抽象类中的所有的抽象方法都必须在派生类中实现
abstract class Tu{
    abstract getLength(width:number,height:number):number;
    abstract getArea(r:number):number;
}

// 派生类

class ChangFang extends Tu{
    width:number;
    height:number;
    constructor(width:number,height:number){
        super()
        this.width = width;
        this.height = height;
    }
    getLength():number{
        return (this.width+this.height)*2
    }
    getArea():number{
        return this.width*this.height
    }
}
// let c1 = new ChangFang(10,20)
// console.log(c1.getLength());
// console.log(c1.getArea());



class Circle extends Tu{
    r:number;
    constructor(r:number){
        super()
        this.r = r
    }
    getLength():number{
        return Math.PI*this.r*2
    }
    getArea():number{
        return Math.PI*this.r*this.r
    }
}
let c1 = new Circle(3)
console.log(c1.getLength());
console.log(c1.getArea());
```

