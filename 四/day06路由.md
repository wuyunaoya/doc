# 一.路由

## 1.定义

node中路由:web服务器根据用户输入的不同URL地址,返回不同的页面.

vue中的路由:路由是vue.js的一个路由插件,他需要跟组件进行深度结合,来构建单页面应用.

单页面应用:是基于根据用户访问的路由,结合组件进行构建单页面应用.

## 2.安装路由

```
npm i vue-router --save
```

## 3.清空工作

```
App.vue  只存模板文件(根组件)
main.js  唯一入口文件
components 局部组件(清空)
assets 		清空
```



## 4.components

```
局部组件:login.vue home.vue detail.vue
```



## 5.路由出口

```vue
   <!-- 路由出口 -->
  <router-view></router-view>
```

## 6.配置路由并使用

```js
//1.引入路由
// import Vue from 'vue'
import Router from 'vue-router'
Vue.use(Router)

// 2,引入组件路径
import login from './components/login.vue';
import home from './components/home.vue';
import detail from './components/detail.vue';


// 3.实例化对象时,需要传递一个json,在json中做路由规则的配置
const router = new Router({
  routes:[
    {
      path:'/login',
      component:login
    },
    {
      path:'/home',
      component:home
    },
    {
      path:'/detail',
      component:detail
    },
  ]
})


/* eslint-disable no-new */
new Vue({
  el: '#app',
  components: { App },
  template: '<App/>',
  router
})
```



## 7.客户端访问

```
http://localhost:8080/#/home
http://localhost:8080/#/login
http://localhost:8080/#/detail
```



## 8.重定向

```js
{
      // *表示任何不存在路径
      path:'*',
      redirect:'/home'
 }
```



## 8.路由优化

```js
-src
	-router
		index.js
		
//1.引入路由
import Vue from 'vue'
import Router from 'vue-router'
Vue.use(Router)

// 2,引入组件路径
import login from '../components/login.vue';
import home from '../components/home.vue';
import detail from '../components/detail.vue';


// 3.实例化对象时,需要传递一个json,在json中做路由规则的配置
export default new Router({
  routes:[
    {
      path:'/login',
      component:login
    },
    {
      path:'/home',
      component:home
    },
    {
      path:'/detail',
      component:detail
    },
    {
      // *表示任何不存在路径
      path:'*',
      redirect:'/home'
    }
  ]
})

```



# 二.二级路由

## 1.路由配置

```js
 routes: [
    {
      path:'/login',
      component:login
    },
    {
      path:'/home',
      component:home,
        //二级路由规则配置
      children:[
        {
          // 二级路由path后面不需要跟/
          path:'man',
          component:man
        },
        {
          // 二级路由path后面不需要跟/
          path:'women',
          component:women
        },
        {
          // 二级路由path后面不需要跟/
          path:'child',
          component:child
        },
        {
          path:'',
          redirect:'man'
        }
      ]
]
```



## 2.重定向

```js
{
    path:'',
    redirect:'man'
}
```



## 3.路由跳转

```vue
 <router-link to="/login">登录</router-link>
```



## 4.绑定样式

```css
两种方式:
方式一:使用系统内置的类名
/* .router-link-active{
  background: aqua;
  color:palevioletred;
} */

方式二:使用active-class设置一个值,进行选中的样式绑定
<router-link to="/home/man"  active-class="select">男装</router-link>
<router-link to="/home/women" active-class="select">女装</router-link>
<router-link to="/home/child" active-class="select">童装</router-link>

.select{
  background: red;
  color: blue;
}
```

