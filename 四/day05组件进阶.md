## 复习:

```
步骤:
1.安装webpack
npm i webpack -g
2.查看webpack版本 webpack -v   出现问题,需要安装webpack-cli
3.安装webpack脚手架
npm i webpack-cli -g  
4.webpack -v  

5.安装vue脚手架
npm i vue-cli -g
6.新建一个目录demo
7.vue init webpack (没有指定项目名称,则直接安装在demo目录下)
  vue init webpack demo1  (指定项目名称,则在demo目录下创建一个demo1目录,在demo1目录进行项目的搭建)
	
8.如果项目中没有node_modules,需要手动安装
	npm i
9.启动项目前进入demo目录中
10.npm run dev 启动项目

```



# 一.父传子

```
父传子:
	1.父组件通过自定义属性进行传值.
		<v-child a="10" :name="name"></v-child>
	2.子组件通过props接收父组件传递数据
		props:["a","name"]
```

```
父传子:
1.父传子,父变.子变,子变,父不变.并且报错.
2.要实现父变,子变,子变,父变,需要传递一个json即可
3.要实现父变,子不变,子变,父不变,需要在子组件中挂载完成时,将父组件传递的数据存入子组件的属性中即可. 
```

props验证

```js
当父组件给子组件传值时,需要通过props进行验证
props:{
    name:{
      type:String,
      required:true
    },
    age:{
      type:Number
    },
    sex:{
      type:String,
      default(){
        return '女'
      }
    }
  }
```



# 二.子传父

```
子传父:
	1.通过自定义事件进行传递数据
	2.子组件通过$emit('自定义事件名',[要传递的参数])
	3.父组件接收通过自定义属性,<v-child3 @自定义的事件名="要触发的函数"></v-child3>
```

```js
子组件传递
 /*
 $emit()
 参数一:传递的事件名
 参数二:传递的数据
 */
 this.$emit('bb',name);
```

```html
父组件接收,通过自定义属性进行接收,如果有参数,需要通过$event进行接收
<v-child3 @aa="changeName" @bb="changeName1($event)"></v-child3>
```



# 三.非父子通信

有三种方式:

1.eventBus:  A->B  A和B必须同时存在

2.vuex   任何组件之间数据的传递   缺点:页面刷新.数据消失

3.本地存储 localStorage  

```js
main.js中
Vue.prototype.event = new Vue()
```

```js
在a.vue 中
 this.event.$emit('aa',this.name)
```

```js
在b.vue 中
 // 监听事件是否触发
    this.event.$on('aa',(e)=>{
      // e是形式参数,是通过自定义事件传递的参数
      this.newName = e;
    })
```



# 四.is和ref

## 1.is

is可解决标签固定搭配问题

```html
<ul>
    <!-- is可解决固定搭配问题 -->
    <li is="v-one"></li>
</ul>
```



## 2.动态组件

```
安装animate.css并保存在package.json文件中

1.npm i animate.css --save   安装并保存
```

```
在main.js文件引入animate.css文件
import 'animate.css'
```

```html
动态组件使用
<!-- 动态组件 -->
<button @click="changeName='v-one'">one</button>
<button @click="changeName='v-two'">two</button>
<transition
enter-active-class="animate__animated animate__backInDown"
>
<div :is="changeName"></div>
</transition>
```

## 3.scoped

```css
scoped使得样式局部有效
<style scoped>
.red{
  background: blue;
  height: 30px;
  color: white;
}
</style>
```



## 3.ref(只做操作)

ref被用来给元素或者子组件注册引用信息。引用信息将会注册在父组件的$refs上。如果是普通的DOM元素上使用，引用指向的就是DOM元素；如果用在子组件上，引用就指向子组件的实例。

在普通dom节点上获取

```vue
<template>
  <div>
    <button @click="change('gold')">变成金色</button>
    <div class="red" ref="myDiv"></div>
  </div>
</template>

<script>
export default {
  methods:{
    change(name){
      // 在此处修改div元素的样式
      // console.log(this.$refs.myDiv);
      this.$refs.myDiv.style.background = name;

    }
  }
}
</script>

<style scoped>
.red{
  width:200px;
  height: 200px;
  background: greenyellow;
}
</style>

```

在子组件上,修改子组件的数据或者方法

```html
 <!-- 在子组件上使用ref -->
    <!-- 在父组件中修改子组件的值 -->
    <button @click="changeName('张柏芝')">张柏芝</button>
    <v-one ref="one"></v-one>
    
  changeName(name){
      // console.log(this.$refs.one);
      this.$refs.one.msg = name;
    }
```



# 五.jquery

```
安装jquery
npm i jquery --save
```

## 1.局部使用jquery

```
 在当前组件中引入
 import $ from 'jquery';
 // 使用jquery须遵循三要素: 先获取 加事件 在操作
    // 局部使用jquery
    // $('.show').click(()=>{
    //   $('.red').slideDown(400);
    // })
    // $('.hide').click(()=>{
    //   $('.red').slideUp(200);
    // })

```

## 2.全局使用jquery

```js
在main.js 中引入
//引入jquery
import $ from 'jquery';
Vue.prototype.$ = $;
```



```js
任何组件中都可使用this.$()
// 全局使用jquery
    this.$('.show').click(()=>{
      this.$('.red').slideDown(500);
    })
    this.$('.hide').click(()=>{
      this.$('.red').slideUp(500);
    })
```



# 六.插槽slot

## 1.匿名槽口

```html
父组件
<v-one>
      <!-- 匿名槽口,没有名字.子组件中留有槽口,父组件会将所有插入的信息放入一个槽口中 -->
      <div>我是父组件,我想进入你的世界</div>
 </v-one>
```

```html
子组件
<template>
  <div>
    <p>今天真是个好日子</p>
    <!-- 槽口 -->
    <slot></slot>
  </div>
</template>
```

## 2.具名槽口

```html
父组件
<!-- 具名槽口:有名字 -->
    <v-two>
      <ul slot="basketball">
        <li>科比</li>
        <li>詹姆斯</li>
      </ul>

      <ol slot="actors">
        <li>赵丽颖</li>
        <li>冯绍峰</li>
      </ol>
    </v-two>
```

```html
子组件
<template>
  <div>
    <slot name="basketball"></slot>
    <h2>第二个子组件</h2>
    <slot name="actors"></slot>
  </div>
</template>
```



# 七.面试题

```
	vue中的 ref是什么？如何使用ref？
	ref是用来获取素或者子组件的句柄。
	vue中如何使用jquery？
	说说你对 slot 的理解有多少？slot 使用场景有哪些？
	vue的is这个属性你有用过吗？主要用在哪些方面？
```

# 八.作业

1.弹框案例敲三遍

2.其他案例敲两遍