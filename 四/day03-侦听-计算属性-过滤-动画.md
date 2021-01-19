# 一.侦听器

## 1.定义

别名:监听器.

## 2.作用

当数据发生改变的时候,及时作出响应

## 3.普通监听

```
 监听属性:
 参数一:表示修改后的新值
 参数二:表示修改前的旧值
```

```html
 <div id="app">
        <input type="text" v-model="name">
        <div>状态:{{status}}</div>
    </div>
    <script>
        new Vue({
            el:'#app',
            data:{
                name:'霍建华',
                status:'未修改'
            },
            methods:{},
            watch:{//监听属性
                name:function(){
                    this.status = '已修改';
                }
            }
        })
    </script>
```



## 4.深度监听

如果是对象或者数组中包含有对象,需要使用深度监听.

```
 // 深度监听
 user:{
 // handler进行数据的监听,不可修改
 handler(){
 console.log('user变了');
 },
 deep:true,
 }
 
 
 总结:
 	1.深度监听需要使用方法:handler进行监听数据的改变
 	2.deep:true进行深度监听   deep默认为false
 	3.深度监听是对对象或者数组中包含对象的监听
 	4.计算属性中的属性名不能和data中的属性名相同
```



# 二.计算属性

```
1.在实际开发中.有一些相对复杂的计算,需要用到计算属性
2.如果一个表达式不能完成计算,需要用到计算属性
3.计算属性的名称,无需再data中进行定义,直接在页面中使用该变量
```

```html
<div id="app">
        <div>原数据为:{{name}}</div>
        <div>计算属性之后的数据为:{{changeName}}</div>
        <div>a的值为:{{a}}</div>
        <hr>
        <table border="1" width="400px">
            <tr>
                <th>序号</th>
                <th>姓名</th>
                <th>分数</th>
            </tr>
            <tr v-for="(item,index) in arr" :key="item.id">
                <td>{{item.id}}</td>
                <td>{{item.name}}</td>
                <td>{{item.score}}</td>
            </tr>
        </table>
        <div>
            总分为:{{count}}
        </div>
        <div>
            平均分为:{{avg}}
        </div>
    </div>
    <script>
        new Vue({
            el:'#app',
            data:{
                name:'hello',
                arr:[
                    {
                        id:1,
                        name:'王俊凯',
                        score:90,
                    },
                    {
                        id:2,
                        name:'王源',
                        score:87,
                    },
                    {
                        id:1,
                        name:'易烊千玺',
                        score:65,
                    },
                    {
                        id:4,
                        name:'王一博',
                        score:99,
                    }
                ]
            },
            methods:{},
            computed:{//计算属性
                changeName:function(){
                  return   this.name.split('').reverse().join('');
                },
                a:function(){
                    return 10
                },
                count:function(){
                    var num = 0;
                    this.arr.forEach(item=>{
                        num += item.score;
                    })
                    return num;
                },
                avg:function(){
                    return this.count/this.arr.length;
                }
            }
        })
    </script>
```



# 三.过滤

对数据进行部分处理

## 1.全局过滤器

```
Vue.filter('过滤器的名字',(e)=>{
	//e为要过滤的对象
	//选项
	return 
})
```

## 2.局部过滤器

```
 new Vue({
     el:'#app',
     data:{
     telphone:'18600998765',
     price:30.00,
     },
     methods:{},
     // 局部过滤
     filters:{
         过滤器的名字:function(e){
         //e为要过滤的对象
         //选项
         return 
         }
     }
     })
```

```
全局过滤器和局部过滤的区别
全局过滤器:任何地方都能使用
局部过滤器:仅限当前vue实例可使用
```



# 四.动画

## 1.原生写法

使用场景: 当插入,修改或者删除元素的时候,需要动画

```
内置的6个类名
出现前:enter
出现过程:enter-active
出现完成:enter-to
离开前:leave
离开过程:leave-active
离开完成leave-to

结合transition标签来使用,name='aa'
```

## 2.animate.css

```
1.安装
cnpm i animate.css --save

2.引入
<link rel="stylesheet" href="./node_modules/animate.css/animate.css">

3.使用  animate__animated是基类,必须写上
 <transition 
            enter-active-class="animate__animated animate__backInDown"
            leave-active-class="animate__animated animate__backOutRight"
        >
        <div class="box" v-if="show"></div>
  </transition>
```



# 五.面试题

1.说明watch和computed的作用与区别

```
watch中的函数是不需要调用的
computed内部的函数调用的时候不需要加()
 
watch  属性监听 监听属性的变化，需要在数据变化时执行异步或开销较大的操作时使用
computed:计算属性通过属性计算而得来的属性，属性的结果会被缓存，除非依赖的响应式属性变化才会重新计算。主要当作属性来使用；
 
watch擅长处理的场景：一个数据影响多个数据；
computed擅长处理的场景：一个数据受多个数据影响。
```

2.说明watch和methods的作用与区别

```
watch .是观察的动作，自动执行
methods 是方法，主动调用
```

3.Vue中过滤器如何定义和使用？
4.使用过滤器实现实现日期的格式化，只显示年月日。
5.过渡动画在什么场景下使用？有哪几个内置的类名？

6.vue中遇到bug？

```
1.如果使用{{}}，首屏会出现闪屏，用v-text解决
2.使用深度监听，可能会造成页面卡顿。解决：转成简单类型，进行监听
3.在vue中，不推荐v-for和v-if同时使用。如果需要同时使用，记得使用computed解决
4.数组或者json变了，页面不渲染。解决：Vue.set() vm.$set() ,如果是数组，还可以使用splice
```

7.字符串：slice substring substr,padStart padEnd indexOf includes 

8.时间对象：。。。

9.arr:splice push forEach map every some filter slice ...

# 六.作业

1.面试题用法

2.淘宝搜索

3.三个案例敲三遍