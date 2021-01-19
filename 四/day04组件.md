# 一.组件介绍和注册

## 1.定义:

可复用的vue实例

## 2.作用

可重复调用

## 3.注册

全局注册

```js
  // 全局注册组件
  Vue.component('toubu',{
  template:'<div>头部:全局组件</div>'
  })
```

布局注册

```js
new Vue({
    el:'#app',
    // 局部注册组件
    components:{
        dibu:{
        template:'<h2>底部内容</h2>'
        }
        }
    })

```

```
全局注册和局部注册的区别:
1.全局注册:在整个项目都可以使用,即在任何一个组件中都可使用
2.局部注册:只能在当前的vue实例对象使用.

```

## 4.组件名称

```
 1.不能使用现有标签作为组件名  eg:div p span img 
 2.不能使用现有标签的大写作为组件名  eg:DIV dIV Div
 3.组件名中包含有大写的,将大写转为  -小写
 4.建议组件名有一个大写,方便书写  
```

## 5.template

```
使用vue组件时,可以只用template模板替换组件中template属性的值.
```



```html
<div id="app">
        <v-one></v-one>
        <v-two></v-two>
    </div>
    <template id="one">
        <div>
            <h3>组件</h3>
        </div>
    </template>
    <template id="two">
        <h4>第二个子组件</h4>
    </template>
    <script>
        new Vue({
            el:'#app',
            data:{},
            methods:{},
            components:{
                vOne:{
                    template:'#one',
                },
                vTwo:{
                   template:'#two', 
                }
                
            }
        })
    </script>
```

```
总结:
1.每一个组件就是一个新的vueComponent实例对象,
2.表示vueComponent对象也有data computed filter watch 以及八个生命周期等等
3.data的唯一区别是:data必须是个函数,且要有返回值
4.一个模板中只能有一个跟节点.
```



## 6.data

在组件中使用data,data必须是个函数,且要有返回值

```html
<div id="app">
        <v-one></v-one>
    </div>
    <template id="one">  
        <div>name为:{{name}}</div>
    </template>
    <script>
        new Vue({
            el:'#app',
            data:{},
            methods:{},
            components:{
                vOne:{
                    template:'#one',
                    // 在组件中使用,data必须是个函数,而且要有返回值
                    data(){
                        return {
                            name:'hahaha'
                        }
                    }
                }
            }
        })
    </script>

```



## 7.组件嵌套

```js
<script>
        const vLeft = {
                            template:'#left',
                      }
        const vRight = {
                            template:'#right',
                        }
        const vHeader = {
                            template:'#header'
                        }
        const vMain = {
                        template:'#main',
                        components:{
                            vLeft,
                            vRight,
                        }
                      }
        const vFooter = {
                            template:'#footer',
                        }
        const vPage = {
                        template:'#page',
                        components:{
                            vHeader,
                            vMain,
                            vFooter
                        }
                    }


        new Vue({
            el:'#app',
            data:{},
            methods:{},
            components:{
                vPage
            },
            template:'<v-page></v-page>',
        })
    </script>
```



# 二.脚手架

```
webpack:是项目打包的一个工具.


1.安装webpack全局
npm i webpack -g      npm uninstall webpack -g全局卸载

2.安装vue脚手架全局
npm i vue-cli -g

3.初始化vue项目
vue init webpack 项目名称

4.npm i 或者 cnpm i  安装依赖项

```



## 1.脚手架目录介绍

```
-build   webpack的打包配置文件
-config  项目的配置文件
-node_modules  安装依赖包等的相关模块
-src    	你写的项目
-static   静态资源文件eg:css js img等
			1.静态资源文件不参与压缩打包
			2.在index.html文件引入static的静态资源文件
.babelrc es6转es5的配置项
.editorconfig:  编辑器的配置项
.gitignore  上传到github上要忽略的文件
.postcssrc.js  css的配置文件
index.html   项目唯一的页面
package.json   存放项目的描述 依赖项的详细信息和相关版本
read.me   有关项目的启动信息
```

```
src目录

-assets  存放静态资源文件: eg:css js img
		1.静态资源文件参与压缩打包
		2.在main.js文件引入asstes的静态资源文件
-components:  局部组件
-common   全局组件
-utils   工具类
-filters  过滤
App.vue   唯一的根组件
main.js   唯一的入口文件
```

vuter  vscode插件

## 2.项目介绍

```
1.清空工作
App.vue  清空,只留vue模板
components  清空(删除helloWorld.vue)
assets  清空(删除logo.png)


2.src目录中仅留下四个文件
	assets(空的)
	components(空的)
	App.vue(只有vue模板)
	main.js
	
```

## 3.使用项目

```
1.导入模板,并且给模板起个名字vheader
	import vHeader from './components/header.vue';
2.注册组件,注意:组件名和模板名保持一致
	export default {
      components:{
        vHeader,
        vMain,
        vFooter
      }
    }
 3.调用模板:
 	<template>
      <div class="container">
        <v-header></v-header>
        <v-main></v-main>
        <v-footer></v-footer>
      </div>
    </template>
 4.谁要使用其他模板.就在谁处引入

```

## 4.父传子

```
 分析:
 1.父子之间传值,必须找到他们之间唯一关联
 2.父组件向子组件传值通过自定义属性传递,
 3.子组件通过props属性进行接收
```

```
1.父传子,父变,子变.子变,父不变,而且会报错
2.如果想要实现父变,子变.子变.父变.,需要传递一个json
3.要实现父变,不变.子变,父不变?
    解决方案:
        在子组件中挂载完成里将父组件的数传递到子组件的data中.
```

```vue
父组件通过自定义 属性进行传值
<v-child a="10" b="20" :name="name"  :user="user" :arr="arr" :age="age"></v-child>
```

```js
子组件中通过props接收
 props:["a","b","name","user","arr","age"],
```



# 三.面试题

1.列举出在vue中组件的定义方式有哪几种？

```js
一种：全局方式
  // 全局注册组件
  Vue.component('toubu',{
  template:'<div>头部:全局组件</div>'
  })
 二种：局部方式
 new Vue({
    el:'#app',
    // 局部注册组件
    components:{
        dibu:{
        template:'<h2>底部内容</h2>'
        }
        }
   })
```

2.组件中的data为什么必须是函数？

```
 答案：组件是可复用的vue实例，一个组件被创建好之后，就可能被用在各个地方，而组件不管被复用了多少次，
        组件中的data数据都应该是相互隔离，互不影响的，基于这一理念，组件每复用一次，data数据就应该被复制一次，之后，当某一处复用的地方组件内data数据被改变时，其他复用地方组件的data数据不受影响。

        组件中的data写成一个函数，数据以函数返回值形式定义，这样每复用一次组件，就会返回一份新的data，
        类似于给每个组件实例创建一个私有的数据空间，让各个组件实例维护各自的数据。
        而单纯的写成对象形式，就使得所有组件实例共用了一份data，就会造成一个变了全都会变的结果。
```

3.vue.cli中怎样定义和使用组件？

```

```

4.请说出vue.cli项目中src目录每个文件夹和文件的用法？

```
src目录

-assets  存放静态资源文件: eg:css js img
		1.静态资源文件参与压缩打包
		2.在main.js文件引入asstes的静态资源文件
-components:  局部组件
-common   全局组件
-utils   工具类
-filters  过滤
App.vue   唯一的根组件
main.js   唯一的入口文件
```

5.vue中父组件是如何向子组件传值的?

```
父组件通过自定义 属性进行传值
<v-child a="10" b="20" :name="name"  :user="user" :arr="arr" :age="age"></v-child>
子组件中通过props接收
props:["a","b","name","user","arr","age"],
```



# 四.作业

1.每个案例写2遍

2.熟悉脚手架

3.练习父传子