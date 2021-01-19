# 一.美团项目

## 1.初始化vue项目

```
1.新建目录:meituan
2.初始化vue项目:vue init webpack 
3.安装依赖模块:cnpm i
3.安装路由:cnpm i vue-router --save
```

## 2.清空工作

```
main.js 不用动
App.vue 只留vue模板文件
components 清空
assets 清空
```

## 3.你的代码目录划分

```
src
	-assets  静态资源
	-components 公共组件
	-pages 局部组件
	-filters 过滤器
	-router 路由配置项
	.App.vue 唯一根组件
	.main.js 唯一入口文件
```

## 4.引入静态资源

```js
main.js中引入
// 1.引入css文件
import './assets/css/reset.css';

// 2.引入js文件
import './assets/js/ref.js';
```

注意:px 转rem 插件

```
1.vscode插件搜索:cssrem (做px转rem的插件) 
2.vscode中设置->用户设置->搜索px to rem ,将px to rem 值改为100.
3.按住快捷键:alt+z,将其转换
```

## 5.路由配置

路由出口

```vue
App.vue文件引入
  <!-- 路由出口 -->
  <router-view></router-view>

```

## 6.开发顺序

### login.vue

```vue
<template>
  <div>
    <h1>登录</h1>
    <div>角色:
      <select v-model="user.role">
        <option value="" disabled>--请选择--</option>
        <option value="0">外卖小哥</option>
        <option value="1">普通用户</option>
      </select>
    </div>
    <div>用户名:
      <input type="text" v-model="user.name">
    </div>
    <div>密码:
      <input type="password" v-model="user.pass">
    </div>
     <div>
      <button @click="login">登录</button>
    </div>
  </div>
</template>

<script>
export default {
  // 规定后台接口:角色:role 用户名:name 密码:pass
  data(){
    return {
      user:{
        role:'',
        name:'',
        pass:''
      }
    }
  },
  methods:{
    login(){
      // 判断用户信息
      if(this.user.name == 'aaa' && this.user.pass == '123'){
        // 跳转首页
        this.$router.push('/index');
      }else{
        alert('用户名或者密码错误');
      }

    }
  }
}
</script>
```

```js
知识点:连接跳转
this.$router.push('/index');  //c参数变为:连接地址
```

router/index.js

```js
import Vue from 'vue';
import Router from 'vue-router';
Vue.use(Router)

import login from '../pages/login/login.vue';
import index from '../pages/index/index.vue';


export default new Router({
  routes:[
    {
      path:'/login',
      component:login,
    },
    {
      path:'/index',
      component:index,
    }
  ]
})

```

### index.vue (二级路由)

```vue
<template>
  <div>
      //给index的子级留下路由出口
    <router-view></router-view>
   <footer>
      <router-link to="/index/home" active-class="select">首页</router-link>
      <router-link to="/index/order" active-class="select">订单</router-link>
      <router-link to="/index/mime" active-class="select">我的</router-link>
   </footer>
  </div>
</template>

<script>
export default {

}
</script>

<style>
footer{
  position: fixed;
  left:0;
  bottom:0;
  width:100vw;
  height:80px;
  background: grey;
  border-radius: 10px;
  text-align: center;
  line-height: 80px;
  display: flex;
}
footer a{
  flex:1
}
.select{
  background: pink;
  color:aquamarine;
}
</style>

```

新建目录:home/home.vue   order/order.vue  mime/mime.vue(只展示一句话即可)

路由:在/index路由下做二级路由配置.

```js
{
      path:'/index',
      component:index,
      children:[
        {
          path:'home',
          component:home,
        },
        {
          path:'order',
          component:order,
        },
        {
          path:'mime',
          component:mime,
        },
        {//此处需要做个重定向到home首页即可
          path:'',
          redirect:'home',
        },
      ]
    },
```

样式绑定:active-class="select"

```css
<footer>
      <router-link to="/index/home" active-class="select">首页</router-link>
      <router-link to="/index/order" active-class="select">订单</router-link>
      <router-link to="/index/mime" active-class="select">我的</router-link>
</footer>
 .select{
  background: pink;
  color:aquamarine;
}
```

优化index.vue,

```
将底部导航部分提取出来,放入components目录中名为,nav.vue
在index.vue中将nav模板导出,注册组件,调用即可.
```

### home.vue(三种路由跳转)

```vue
<template>
  <div>
    <div class="car">轮播图</div>
    <div class="adv">广告</div>
    <hr>
    <!-- 跳转列表之后,页面底部不会再有底部导航,所有应该放在一级组件下 -->
    <!-- 方式一跳转 -->
    <router-link to="/movie">电影</router-link>
    <router-link to="/food">美食</router-link>
    <hr>
    <!-- 方式二跳转 -->
    <button @click="movie">电影</button>
    <button @click="food">美食</button>
    <hr>
    <!-- 方式三跳转 -->
    <button @click="replaceUrl('/movie')">电影</button>
    <button @click="replaceUrl('/food')">美食</button>
  </div>
</template>

<script>
export default {
  methods:{
    movie(){
      this.$router.push('/movie');
    },
    food(){
      this.$router.push('/food');
    },
    replaceUrl(url){
      // 将当前路由替换成要跳转的路由,当使用window的返回键时,返回上一级则返回的是上上一级路由
      this.$router.replace(url);
    }
  }
}
</script>

<style scoped>
.car{
  width:100vw;
  height:1rem;
  background:aquamarine;
}
.adv{
  width:100vw;
  height:1rem;
  background:bisque;
}
hr{
  height:10px;
  width:100vw;
  background: blue;
}
</style>

```

新建目录:movie/movie.vue   food/food.vue(只展示一句话即可)

路由配置:由于不用底部导航,所以配置一级路由.

```js
{
    path:'/movie',
    component:movie,
},
{
    path:'/food',
    component:food,
}
```

### movie.vue(列表展示和带参数跳转)

```vue
<template>
  <div>
    <h3>电影列表</h3>
    <!-- 方式一:展示列表 -->
    <ul>
      <li v-for="item in movies" :key="item.id" @click="movieDetail(item.id)">
        <h4>名称:{{item.name}}</h4>
        <p>价格:{{item.price}}</p>
        <p>时间:{{item.time}}</p>
      </li>
    </ul>
    <hr>
  </div>
</template>

<script>
export default {
  data(){
    return {
      movies:[
        {
          id:1,
          name:'姜子牙',
          price:30.00,
          time:1607758392233,
        },
        {
          id:2,
          name:'大话西游',
          price:29.90,
          time:1507758392233,
        },
        {
          id:3,
          name:'我和我的祖国',
          price:50.00,
          time:1407758392233,
        }
      ]
    }
  },
  methods:{
    movieDetail(id){
      this.$router.push('/movieDetail?id='+id);
    }
  }
}
</script>

<style>

</style>
```

新建目录movieDetail/movieDetail.vue(接收参数)

路由配置:在一级目录下配置路由

```js
{
      path:'/movieDetail',
      component:movieDetail,
 },
```

### movieDetail.vue(获取参数)

```vue
1.对象外:通过$route.query.id来获取
2.对象内:通过this.$route.query.id来获取
<template>
  <div>
    <h3>电影详情</h3>
    movieDetail{{$route.query.id}}
  </div>

</template>

<script>
export default {
 mounted(){
   console.log(this.$route);
 }
}
</script>

<style>

</style>
```

### food.vue同movie.vue

### foodDetail.vue同foodDetail.vue

```vue
路由跳转方式
方式一:
<ul>
      <li v-for="item in movies" :key="item.id" @click="movieDetail(item.id)">
        <h4>名称:{{item.name}}</h4>
        <p>价格:{{item.price}}</p>
        <p>时间:{{item.time}}</p>
      </li>
</ul>

 methods:{
    movieDetail(id){
      this.$router.push('/movieDetail?id='+id);
    }
  }

方式二:
<ul>
      <!-- 跳转方式二 -->
      <li is="router-link" :to="'/movieDetail?id='+item.id" v-for="item in movies" :key="item.id" >
        <h4>名称:{{item.name}}</h4>
        <p>价格:{{item.price}}</p>
        <p>时间:{{item.time}}</p>
      </li>
 </ul>
```

```
带参数方式
方式一:
methods:{
    movieDetail(id){
      this.$router.push('/movieDetail?id='+id);
    }
  }
  
 方式二:
 methods:{
    foodDetail(id){
      this.$router.push('/foodDetail/'+id);
    }
  }
 区别再:router/index.js 中添加站位符
 {
      path:'/foodDetail/:id',
      component:foodDetail,
 },
 
```

### goBack.vue

```vue
在components/goBack.vue
<template>
  <div>
    <button @click="$router.go(-1)">返回</button>
  </div>
</template>

<script>
export default {

}
</script>

<style>

</style

在components/index.js
import goBack from './goBack.vue';
export default {
    goBack,
}
    
在main.js中
 // 4.引入公共组件
import commonComponents from './components/index';
for(let i in commonComponents){
  Vue.component(i,commonComponents[i])
}
    
总结:全局可使用公共组件
```

# 二.总结

## 1.路由组件

```
<router-view></router-view>
<router-link to="" active-class=""></router-link>
```

## 2.编程式导航

```
this.$router.go()
this.$router.push()
this.$router.replace()
```

## 3.$router和$route的区别

```
$router 是路由跳转
$route 是获取数据
```



# 三.路由守卫

保安:全局路由前置守卫

前台小姐姐:组件内部守卫

马云的秘书:路由独享守卫

## 1.全局路由前置守卫

```js
在main.js中
//6.全局路由前置守卫
router.beforeEach((to,from,next)=>{
  // 一旦加上这个函数调用,什么都不写.任何页面都不会输出
  // 1.to,去往哪个路由页面
  // console.log(to);
  // 2.from 从哪个路由来
  // console.log(from);
  //一般情况下:登录不需要拦截,登录成功,
  //每去一个页面,需要拿着这个标记,去路由页面判断是否登录,是,直接进入.不是,直接去登录页
  if(to.path=="/login"){
    next();
    return;
  }
  if(localStorage.getItem('dark') == '1'){
    next();
    return 
  }
  next('/login');
  
})

```

```js
在login.vue中
 login(){
      // 判断用户信息
      if(this.user.name == 'aaa' && this.user.pass == '123'){
        // 跳转首页
        this.$router.push('/index');
        localStorage.setItem('dark','1')
      }else{
        alert('用户名或者密码错误');
      }

    }
```

## 2.组件路由特享守卫

```js
在movie.vue组件 中进行组件特享守卫

// 组件路由特享守卫
  beforeRouteEnter(to,from,next){
    console.log(from);
    if(from.path == '/index/home' || from.path == '/movieDetail'){
      next();
      return
    }else{
      next('/index/home');
    }
  }
```

## 3.路由独享守卫

```js
在router/index.js
{
      path:'/foodDetail/:id',
      component:foodDetail,
      beforeEnter(to,from,next){
        if(localStorage.getItem('userType') == 0){
          next();
          return;
        }else{
          next('/index/mime');
        }
      }
    },
```

# 四.全局过滤器

```js
1.main.js中
//6.全局过滤器
    import filters from './filters/index';
    for(let i  in  filters){
      Vue.filter(i,filters[i])
    }
2.filters/index.js
	import priceFilter from './priceFilter';
    import timeFilter from './timeFilter';

    export default {
      priceFilter,
      timeFilter
    }
3.filters/priceFilter.js
	export default  (e)=>{
      return e.toFixed(2)
    }
4.filters/timeFilter.js
	export default (e)=>{
      var date = new Date(e);
      var year = date.getFullYear();
      var month = (date.getMonth()+1+'').padStart(2,'0')
      var day = (date.getDate()+'').padStart(2,'0')
      var hours = (date.getHours()+'').padStart(2,'0')
      var minutes = (date.getMinutes()+'').padStart(2,'0')
      var seconds = (date.getSeconds()+'').padStart(2,'0')
      return `${year}-${month}-${day} ${hours}:${minutes}:${seconds}`
    }


```



# 五.动画

```
1.npm i animate.css --save
2.在你需要使用动画的地方加上transition
	<transition
    enter-active-class="animate__animated animate__backInUp">
       <router-view></router-view>
    </transition>
```



# 六.懒加载

## 1.为什么使用懒加载

```
为给客户更好的客户体验，首屏组件加载速度更快一些，解决白屏问题。

   懒加载则可以将页面进行划分，需要的时候加载页面，可以有效的分担首页所承担的加载压力，减少首页加载用时。
定义：
懒加载简单来说就是延迟加载或按需加载，即在需要的时候的时候进行加载。
```

```js
// 非懒加载模式
import login from '../pages/login/login.vue';

// 懒加载模式
const login  = ()=>Promise.resolve(import('../pages/login/login.vue'));
const index  = ()=>import('../pages/index/index.vue');
```



# 七.别名和name

```js
别名alias:
在访问路由时,使用别名会方便访问
routes:[
    {
      path:'/login',
      alias:'/l',
      component:login
    },
  ]
```

```
name:
在路由配置规则中增加name,方便访问当前组件时获取{{$route.name}
 {
     path:'order',
     name:'订单',
     component:order,
 },
```



# 八.hash模式

```
1.在router/index.js
	export default new Router({
      mode:'history',//默认是hash
      routes:[]
2.打包npm run build
3.把dist下面的文件放在服务端的www目录下
4.根据你设置的是hash还是histroy进行访问
```



```
hash模式：
	访问：http://localhost:8080/#/index/home    端口/#
	放在服务端：后面的路由不会影响请求，前进 后退 刷新 都ok
history模式“：
	访问：http://localhost:8080/index/home			端口/文件路径
	放在服务端：  / 后面的路由会影响请求，前进、后退ok ,刷新，显示404
```

### hash和history模式的区别

```js
区别：
hash模式：
  1.采用的是window.onhashchange事件实现。
  2.可以实现前进 后退 刷新。
  3.比如这个URL：http://www.abc.com/#/hello, hash 的值为#/hello。
  它的特点在于：hash 虽然出现URL中，但不会被包含在HTTP请求中，
  对后端完全没有影响，因此改变hash不会重新加载页面
history模式：
  1.采用的是利用了HTML5 History Interface 中新增的pushState() 和replaceState() 方法。
  2.可以前进、后退，但是刷新有可能会出现404的报错
  3.前端的url必须和实际向后端发起请求的url 一致，如http://www.abc.com/book/id 。
  如果后端缺少对/book/id 的路由处理，将返回404错误。 
  不过这种模式要玩好，还需要后台配置支持。因为我们的应用是个单页客户端应用，
  如果后台没有正确的配置，当用户在浏览器直接访问 http://oursite.com/user/id 就会返回 404，这就不好看了。
```

