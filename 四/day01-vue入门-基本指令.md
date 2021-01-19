# 课程介绍

## 1.讲师

刘海艳

## 2.课程介绍

```
2020最新大纲
vue:8天的基础+6天项目(git ts vue3.0.0 服务端渲染)+1天小U商城
	商城管理系统(内部人员)
react:4天基础+1答辩
```



## 3.前端工作

```
官网:BS+JQ(部分修改)
app:android+ios+h5(修改次数多,变换频率大的)
活动页:流行色 流行语 活动主题
后台管理系统
	内部人员使用(不对外公开)
	没有注册,只有登录
	权限(角色)
	table+form
	给公司高层去展示(统计,视图,数据可视化)
```



## 4.问题解决

```
1.如果遇到问题,不要慌,分析问题原因所在,找到问题点,在进行解决
2.求助他人解决(朋友,同学 同事),找我
3.总结分析:有道云笔记
```

## 5.作业

```
1.当天的作业当天清
2.面试题
3.归纳整理到一个地方
```



# vue简介

目的:快速开发  简单

## 1.介绍vue

### 优点:

易用 | 灵活 | 高效 | 渐进式 JavaScript 框架 | SPA(single page application)单页面应用

```
高效:超快虚拟 DOM
浏览器解析页面的步骤:
1.解析dom元素,生成dom树
2.解析css样式,生成样式树
3.dom树和样式树结合
4.生成坐标点
5.渲染页面

修改1个元素,执行上面5个步骤,如果10个元素修改,需要执行以上10次5个步骤.


虚拟dom(存在于内存当中)
一旦有要修改的元素,通过虚拟dom进行修改,修改完成,将虚拟dom跟真实dom进行差异比较,一旦产生差异,直接修改页面即可,如果有10个元素修改,直接修改虚拟dom即可.
虚拟dom你可以把它理解为是js的一个object(对象)

总结:js解析js会比js解析html快的多

```

```
高效:最省心的优化
transform:  -webkit -moz -ms -o
使用vue,直接transform,里边有做集成优化
```

```
渐进式JavaScript 框架:(主张少)
			入住
新房:		装家具,家电   =====主张少
二手房:	本身有家具,家电(直接使用我)  如果你想按照自己的风格进行装修:需要重构 ===== 主张多
```

```
spa:单页面应用
原生网站:  多个页面之间进行跳转(N个html)
单页面:始终只有一个页面(.html)

缺点:不理于SEO优化,首屏加载速度慢
```

### 缺点

```
缺点:
	1.首屏加载速度慢,
	2.不利于SEO优化
	3.不支持IE678.
	
```

### vue核心

```
数据驱动 组件化系统
```



## 2.下载及安装

```
下载两种:
方式一:直接引入<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
方式二:npm i vue --save(保存)  推荐
	如果没有安装成功,需要初始化:npm init(目的产生:package.json)
```

```html
实例:
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>案例</title>
    <!-- 1.引入vue -->
    <script src="./node_modules/vue/dist/vue.js"></script>
</head>
<body>
    <!-- 2.作用域 -->
    <div id="app">
        <h1>{{name}}</h1>
        <p>价格:{{num}}</p>
        <p>{{isShow}}</p>
        <p>{{arr}}</p>
        <p>{{fn()}}</p>
    </div>
    <!-- <div id="app1">
        <h1>{{name}}</h1>
    </div> -->
    <script>
        // 3.产生vue实例
        /*
        1.所有的css样式都可以为做为vue的挂载点
        2.mount:挂载
        3.vue实例不能挂载到HTML或者body上边
        4.一个vue实例只能作用在一个dom节点上,所以建议大家使用id选择器
        5.总结:vue实例跟dom节点是一一对应的关系
        6.总结:一个vue实例只能有一个根节点
        7.在dom节点上:使用{{}}进行data数据的展示
        */
        new Vue({
            el:"#app",//挂载点
            data:{//属性(变量)
                name:'你好vue',
                num:10,
                isShow:true,
                arr:[1,3,4],
            },
            methods:{//方法(函数)
                fn:function(){
                    alert('弹我一下');
                },
            }
        })

        // new Vue({
        //     el:"#app1",
        //     data:{
        //         name:'hello vue'
        //     }
        // })
    </script>
</body>
```



# vue基本指令

## 1.非表单元素(div p span )

```
			优点			缺点
{{}}:	    方便写				不能解析标签,可能会出现闪屏问题
v-html:		解析标签(方便)
v-text:		解决闪屏问题			不能解析标签

总结:以上三种方式都可做数据的展示

```



## 2.表单元素(input textarea)

```html
v-model:绑定data数据
<div id="app">
        <!-- 
            1.v-model绑定的是data里的属性,data里的属性值就是输入框的value值

            MVVM: M:model(模型)  V:view(视图) VM:viewModel(视图模型)
            模型通过viewModel控制着视图, 视图也可以通过viewModel修改模型的数据
            viewModel 在这里起到了中间桥梁的作用
         -->
        <input type="text" v-model="name">
        <h1>{{name}}</h1>
    </div>
    <script>
        new Vue({
            el:"#app",
            data:{
                name:"hello"
            }
        })
    </script>
```



## 3.媒体元素(img)

```
v-bind:属性名 = "变量"
注意:属性名可以是系统属性,也可以自定义属性
<div id="app">
        <!-- 
            1.属性绑定:v-bind:属性名
         -->
        <img v-bind:src="url" alt="">
        <hr>
        <a v-bind:href="company.url">
            <img v-bind:src="company.logo" alt="" v-bind:title="company.name">
        </a>
        <hr>
        <!-- 2.v-bind可以省略 
             3.可以自定义属性 常量不需要加:  变量需要加:
        -->
        <a :href="company.url" a=10 b=20 :cc="people">
            <img :src="company.logo" alt="" :title="company.name">
        </a>

    </div>
    <script>
        new Vue({
            el:"#app",
            data:{
                url:"http://www.ujiuye.com/zt/webqzgcs/images/zg_logo.png",
                company:{
                    name:'尤就业',
                    logo:'http://www.ujiuye.com/zt/webqzgcs/images/zg_logo.png',
                    url:"http://ujiuye.com",
                },
                people:40000,
            }
        })
    </script>
```

## 4.v-if和v-show

```
v-if:元素的显示和隐藏
v-show:通过css样式中的属性display控制着元素的显示和隐藏

分析:使用情形:
	v-if:页面加载完成之后,很少进行修改可以使用v-if
	v-show:选项卡切换
```

## 5.v-for

```
数组:
v-for="(item,index) in arr"    item:数组的每一项   index:数组的下标
对象:
v-for="(item,key,index) in obj" item:每一项  key:对象的键  index:对象的下标

```

```html
遍历数组案例:
<div id="app">
        <ul>
          <!-- <li v-for="item in arr">{{item}}</li> -->
          <li v-for="(i,a) of arr" >{{a}}====={{i}}
          </li>
        </ul>
    </div>
    <script>
        new Vue({
            el:"#app",
            data:{
                arr:['LV','CUCCI','FENDI','香奈儿']
            }
        })
    </script>
```

```html
遍历对象:
 <div id="app">
        <ul>
          <li v-for="(item,key,index) in company">
              <p>{{index}}====={{key}}====={{item}}</p>
          </li>
        </ul>
    </div>
    <script>
        new Vue({
            el:"#app",
            data:{
                company:{
                    name:'中公',
                    logo:'http://www.ujiuye.com/zt/webqzgcs/images/zg_logo.png',
                    url:'http://ujiuye.com',
                    people:40000,
                }
            }
        })
    </script>
```

## 6.v-once

```html
v-once:使用v-once绑定的数据,只在页面中渲染一次,就不在发生改变
<div id="app">
        <!-- 数据一旦完成渲染,就不在发生改变 -->
       <div v-once>{{msg}}</div>
       <button @click="changeMsg()">++</button>
    </div>
    <script>
        new Vue({
            el:"#app",
            data:{
               msg:10
            },
            methods:{
                changeMsg(){
                    this.msg +=1;
                    console.log(this.msg);
                }
                
            }
        })
    </script>
```

## 7.class

```
class可以绑定多种数据格式
1.:class="变量名"
2.:class="表达式? '值1' : '值2"
3.:class = "{值1:true,值2:false}"
```

```html
 <div id="app">
        <!-- 在class中存放一个变量 -->
       <div :class="classN">杜绝公司对学历作为硬性限制条件</div>
       <button @click="changeBlue()">blue</button>
       <button @click="changeOrange()">orange</button>
       <hr>

        <!-- 2.三目运算符 -->
       <p :class="isShow ? 'blue lime' : 'orange lime'">青青子衿,悠悠我心</p>

       <ul>
           <li v-for="(item,index) in arr" :class="index%2===0 ? 'red lime' : 'blue lime'">{{item}}</li>
       </ul>
       <hr>

       <!-- 
        1 4 7  red   0 3 6    index%3 === 0
        2 5 8  blue  1 4 7    index%3 === 1
        3 6 9   orange 2 5 8  index%3 == 2
        :class={red:'',blue:'',orange:''}
        -->
        <!-- 通过Json去绑定class的值
        :class="{}"
        -->
       <ul>
            <li v-for="(item,index) in arr" :class="{red:index%3==0,blue:index%3==1,orange:index%3==2}">{{item}}</li>
        </ul>

        <!-- <div :class="{red:false,blue:true}">hahahaah</div> -->


    </div>
    <script>
        new Vue({
            el:"#app",
            data:{
               classN:'red lime',
               isShow:true,
               arr:['科比','詹姆斯','姚明','易建联','哈登','杜兰特'],
            },
            methods:{
                changeBlue(){
                    this.classN = 'blue lime';
                },
                changeOrange(){
                    this.classN = 'orange lime';
                }
            }
        })
    </script>
```

## 8.style

```
style数据绑定
:style=变量名
:style={background:变量,color:变量1}
```



```html
<div id="app">
       <div class="box" :style="styleN">今夕何夕</div>
       <button @click="changeBlue('blue')">变蓝</button>

       <ul>
           <li v-for="(item,index) in arr" :style="{background:item.color}">
               <h3>{{item.name}}</h3>
               <h3>{{item.url}}</h3>
           </li>
       </ul>
    </div>
    <script>
        new Vue({
            el:"#app",
            data:{
              styleN:{
                background:"yellow",
                color:"green",
                textAlign:"center",
              },
              arr:[
                  {
                      name:'京东',
                      url:'http://www.jd.com',
                      color:'blue'
                  },
                  {
                      name:'天猫',
                      url:'http://www.tmall.com',
                      color:'yellow'
                  },
                  {
                      name:'百度',
                      url:'http://www.baidu.com',
                      color:'pink'
                  },
                  {
                      name:'尤就业',
                      url:'http://www.ujiuye.com',
                      color:'purple'
                  }
              ]
            },
            methods:{
                changeBlue(n){
                    this.styleN.background = n;
                }
            }
        })
    </script>
```



# 面试题

```
1.为什么要选vue？与其它框架对比的优势和劣势？
因为vue：易用 | 灵活 | 高效 | 渐进式 JavaScript 框架 | SPA(single page application)单页面应用
1.与React.js的区别
相同点：
a:React采用了JSX语法，Vue也可使用特殊文件格式
b:中心思想相同：一切都是组件，组件可以嵌套组件
c:都提供合理的钩子函数，可以让开发者定制
d:都不内置Ajax，Router等功能的核心包，而是以插件的形式加载
e:在组件开发中都支持mixins的特性。
不同点：
a:React依赖Virtual DOM,而Vue使用DOM模板，React使用的Virtual DOM会对渲染出来的结果做脏检查
b：vue在模板中提供了指令，过滤器等，可以非常方便的操作DOM

2.mvvm框架是什么？它和其它框架（jquery）的区别是什么？哪些场景适合？
MVVM是Model-View-ViewModel的缩写。MVVM是一种设计思想。Model 层代表数据模型，也可以在Model中定义数据修改和操作的业务逻辑；View 代表UI 组件，它负责将数据模型转化成UI 展现出来，ViewModel 是一个同步View 和 Model的对象。
在MVVM架构下，View 和 Model 之间并没有直接的联系，而是通过ViewModel进行交互，Model 和 ViewModel 之间的交互是双向的， 因此View 数据的变化会同步到Model中，而Model 数据的变化也会立即反应到View 上。
ViewModel 通过双向数据绑定把 View 层和 Model 层连接了起来，而View 和 Model 之间的同步工作完全是自动的，无需人为干涉，因此开发者只需关注业务逻辑，不需要手动操作DOM, 不需要关注数据状态的同步问题，复杂的数据状态维护完全由 MVVM 来统一管理。

区别：vue数据驱动，通过数据来显示视图层而不是节点操作。
场景：数据操作比较多的场景，更加便捷

3.vue单页面应用及其优缺点有哪些
    优点：
         1、用户体验好，快，内容的改变不需要重新加载整个页面，对服务器压力较小。
         2、前后端分离，比如vue项目
         3、完全的前端组件化，前端开发不再以页面为单位，更多地采用组件化的思想，代码结构和组织方式更加规范化，便于修改和调整；
    缺点：
        1、首次加载页面的时候需要加载大量的静态资源，这个加载时间相对比较长。
        2、不利于 SEO优化，单页页面，数据在前端渲染，就意味着没有 SEO。
        3、页面导航不可用，如果一定要导航需要自行实现前进、后退。（由于是单页面不能用浏览器的前进后退功能，所以需要自己建立堆栈管理）
        
4.说出至少4种vue当中的指令和它的用法？
v-html 显示数据可以识别html标签
v-text 显示数据不可以识别html标签
v-model 在form表单中 设置表单value属性
v-blind 修改标签中属性的值，可以简写为：
v-if  控制该标签显示和隐藏 v-if="true"
v-show 通过css中的display属性设置标签的显示和隐藏
v-for 循环
v-once 该标签渲染数据完成后数据不能修改
```

# 作业:

1.home作业

2.今天的案例敲3遍