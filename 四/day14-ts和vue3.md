# 一.配置ts编译文件

```
 tsc -p tsconfig.json -watch  监听
```

## 1.接口(interface)

定义

```ts
// 接口的定义
interface Animal{
    color:string,
    height:number,
}

let taidi:Animal = {
    color:'gold',
    height:50,
}
```

### 属性接口

```ts
// 属性接口
interface Person{
    name:string,
    age:number,
    car?:string//可选属性
}

let lukas:Person = {
    name:'卢卡斯',
    age:30,
    car:'奔驰'
}


interface Point{
    readonly x:number,//只读属性
    readonly y:number,
}
// 只读属性的值不能发生改变
let p:Point = {x:10,y:10}
// p.x = 20;//报错
console.log(p);
```

### 方法接口

```ts

// 方法接口
interface logA{
    // 定义方法
    (a:number,b:number):number
}

let add:logA = (a:number,b:number)=>{
    return a + b
}

let minus:logA = (x:number,y:number)=>{
    return x - y
}

console.log(add(10,20));
console.log(minus(30,10));
```

### 类接口

```ts
// 类接口
// 接口名称是自定义
//实现类接口 需要使用关键字 implements
interface logB{
    name:string;
    fn():void
}

// 类实现接口 implements(实现)
class People implements logB{
    name:string = '王五';
    fn():void{
        console.log(this.name);
        
    }
}

let p1 = new People()
p1.fn()
```



### 扩展接口

```ts
// 类实现多个接口
//接口可以继承接口: extends
//类实现接口:emplements
interface A{
    fn1():void
}

interface B {
    fn2():void
}

class C implements A,B{
    fn1():void{
        console.log('A接口');
    }
    fn2():void{
        console.log('B接口');
    }
}

let c1 = new C()
// c1.fn1()
// c1.fn2()


interface D extends A{
    fn3():void
}

class E implements D{
    fn1(){
        console.log('A接口');
    }
    fn3(){
        console.log('D接口');
    }
}

let e = new E()
e.fn1()
e.fn3()
```



## 2.装饰器(decorator)

装饰器本身是一个函数:使用来装饰类,类的属性,类的方法

装饰器定义:普通定义 | 工厂定义

### 普通定义

```ts
// 普通定义
// logC就是一个装饰器
function logC(obj:any):void{
    // 接收参数为装饰的类
    console.log(obj);
}

@logC
class Http{}
```

### 工厂定义

#### a.定义类装饰器

```ts
// 定义类装饰器
function logClass(params:any){
    return function(target:any){
        // 接收参数为装饰器传递的参数
        console.log('params',params);
        // 接收参数为装饰器装饰的类
        console.log('target',target);
        target.prototype.width = params
        target.prototype.fn = ()=>{
            console.log('aaa');
            
        }
    }
}

@logClass('平安夜')
class Http1{
    width:string | undefined;
    fn(){

    }
}

let a = new Http1()
console.log(a.width);
a.fn()
```



#### b.属性装饰器

```ts
// 属性装饰
function logProp(params:any){
    return function(target:any,attr:any){
        // 接收参数为装饰器传递的参数
        console.log('params',params);
        //接收参数为装饰器所在类
        console.log('target',target);
        // 接收参数为装饰器装饰的属性名
        console.log('attr',attr);
        target[attr] = params
    }
}

class Http2{
    @logProp('属性装饰器') name:string | undefined;   
}

let h1 = new Http2()
console.log(h1.name);
```



#### c.方法装饰器

```ts
// 方法装饰器
function logFn(params:any){
    return function(target:any,methodName:any,desc:any){
        // 接收参数为装饰器传递的参数
        console.log('params',params);
        // 接收参数为装饰器所在的类
        console.log('target',target);
        // 接收参数为装饰器装饰的方法名
        console.log('methodName',methodName);
        // 接收参数为方法的详细信息
        console.log('desc',desc);
        
    }
}

class Http3{
    @logFn('方法名称')
    add(){

    }
}
```



# 二.vue3.0

官网:https://www.vue3js.cn/docs/zh/guide/introduction.html

## 1.安装脚手架

```
//安装
cnpm i @vue/cli@3.0.0 -g

//查看你的版本
vue -V   | vue --version

//创建项目3.0
vue create demo
```

## 2.要想拉取2.x版本

```
cnpm i @vue/cli-init -g
创建项目2.0
vue init webpack demo
```

## 3.创建项目步骤

1.vue create demo3.0

2.![image-20201224112502437](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201224112502437.png)

3.![image-20201224112649250](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201224112649250.png)

4.![image-20201224112752800](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201224112752800.png)

5.![image-20201224112822907](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20201224112822907.png)

6.cd demo3.0

7.npm run serve  启动

8.若想修改启动的指令,去package.json

```
"scripts": {
    "start": "npm run serve",  //指:npm start ==== npm run serve
    "serve": "vue-cli-service serve",
    "build": "vue-cli-service build"
  },
```

9.npm start 修改后的启动

10,访问: http://localhost:8080

## 4.使用vue3.0的新语法

### 1.组件的创建

```ts
<template>
  <div>
      <h3>订单组件</h3>
  </div>
</template>

<script lang="ts">
import {Component,Vue} from 'vue-property-decorator'
@Component({})
export default class Order extends Vue{
    
}
</script>

<style>

</style>
```



### 2.属性

```ts
<template>
  <div>
      <h3>订单组件</h3>
      <p>{{name}}</p>
  </div>
</template>

<script lang="ts">
import {Component,Vue} from 'vue-property-decorator'
@Component({})
export default class Order extends Vue{
    // 属性  data()
    name:string = 'apple';
}
</script>
```



### 3.方法

```ts
      
<template>
  <div>
      <h3>订单组件</h3>
      <p>{{name}}</p>
      <button @click="changeName('banana')">banana</button>
  </div>
</template>

<script lang="ts">
import {Component,Vue} from 'vue-property-decorator'
@Component({})
export default class Order extends Vue{
    // 属性  data()
    name:string = 'apple';
    // 方法  methods:
    changeName(name:string){
        this.name = name
    }
}
</script>
```



### 4.计算属性

```ts
 // 计算属性  computed
//get 计算属性的名称(){return  xxxx}
    get reverseName(){
        return this.name.split('').reverse().join('');
    }
```



### 5.监听(Watch)

```ts
	name:string = 'apple';
    obj:object = {
        msg:'今天是平安夜,大家平平安安'
    }
//普通监听
    @Watch('name')
    changename(newVal:string,oldVal:string){
        // console.log('name变了');
        console.log(newVal,oldVal);
    }

    //深度监听
    @Watch('obj',{deep:true})
    changeObj(){
        console.log('obj改变了');
    }
```

### 6.组件之间通信

父传子

```ts
父组件:传值
<Child :myName="name"></Child>
子组件接收:
import {Component,Vue,Prop  } from "vue-property-decorator";
export default class Child extends Vue{
    @Prop() myName:string | undefined;
}

总结:父传子通过自定义属性进行传值
	子组件接收父组件的值:Prop装饰器接收
```

子传父

```ts
子组件:
 	<div><button @click="fn">宋小宝</button></div>
      <div><button @click="fn1">宋丹丹</button></div>
      <div><button @click="fn2('启佳')">宋启佳</button></div>

// 方式一:没有传参,自定义事件的名称就是装饰的方法的名称
    @Emit()
    fn(){

    }

    // 方式二:传递参数,自定义事件的名称是传递的参数名
    @Emit('dan')
    fn1(){

    }

    //方式三:传递参数,自定义事件的名称是传递的参数名,同时传递数据
    @Emit('qi')
    fn2(){

    }
父组件:
 <Child :myName="name" @fn="fn"  @dan="fn1" @qi="changeName"></Child>

总结:
	子传父:通过自定义事件进行传递.
    	子组件:子组件通过Emit装饰器进行事件的传递
        父组件:通过事件触发来接收
```



### 7.设置配置文件(做配置代理)

新建vue.config.js

```js
module.exports = {
      // 部署应用时的基本 URL
      publicPath:"",
      // build时构建文件的目录 
      outputDir: 'dist',
      // build时放置生成的静态资源 (js、css、img、fonts) 的目录
      assetsDir: 'static',
      // 指定生成的 index.html 
      indexPath: 'index.html', 
      // 设置代理请求
      devServer: {
          proxy: {
              '/api': {
                  target: '<url>',
                  ws: true,
                  changeOrigin: true
                },
            }
      }
}
```

























