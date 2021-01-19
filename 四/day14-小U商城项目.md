# 小U商城项目

## 一.项目框架

```
1.vue2.0创建项目:  npm init webpack umall-mobile  (router)
2.npm i vant vuex axios --save  安装依赖项
```

## 二.初始化工作

1.清空工作

```
assets  清空
components  清空
router  只留模板
App.vue  根组件  只留路由出口
main.js   唯一入口
```

2.页面布局工作

```js
App.vue  一级路由出口
layout.vue  二级路由出口
import Vue from 'vue'
import Router from 'vue-router'


Vue.use(Router)
const index = ()=>import('../pages/index.vue')
const cate = ()=>import('../pages/cate.vue')
const cart = ()=>import('../pages/cart.vue')
const user = ()=>import('../pages/user.vue')
const goodsList = ()=>import('../pages/goodsList.vue')
const login = ()=>import('../pages/login.vue')
const register = ()=>import('../pages/register.vue')
const layout = ()=>import('../pages/layout.vue')

export default new Router({
  routes: [
      {
        path:'/',
        component:layout,
        redirect:'/index',
        children:[
          {
            path:'/index',
            component:index,
          },
          {
            path:'/cate',
            component:cate,
          },
          {
            path:'/cart',
            component:cart,
          },
          {
            path:'/goodsList',
            component:goodsList,
          },
          {
            path:'/user',
            component:user,
          },
          {
            path:'/login',
            component:login,
          },
          {
            path:'/register',
            component:register,
          },
        ]
      }
  ]
})

```

## 三.开发流程三.开发流程

```js
使用vant,需要全局引入,在main.js 中引入
//引入vant全局
import Vant from 'vant';
import 'vant/lib/index.css';
Vue.use(Vant);
```



### layout.vue

```vue
<template>
  <div>
    <!-- 二级路由出口 -->
    <router-view></router-view>
    <!-- 标签页 -->
    <van-tabbar v-model="active" route>
      <van-tabbar-item icon="home-o" to="/index">首页</van-tabbar-item>
      <van-tabbar-item icon="apps-o" to="/cate">分类</van-tabbar-item>
      <van-tabbar-item icon="shopping-cart-o" to="/cart">购物车</van-tabbar-item>
      <van-tabbar-item icon="user-o" to="/user">我的</van-tabbar-item>
    </van-tabbar>
  </div>
</template>

<script>
export default {
  data(){
    return {
      active:0
    }
  }
}
</script>

<style>

</style>

```

### index.vue

```vue
<template>
  <div class="index-container">
    <!-- 导航 -->
    <van-nav-bar  title="首页" />
    <!-- 轮播图 -->
    <van-swipe class="my-swipe" :autoplay="3000" indicator-color="red">
      <van-swipe-item>1</van-swipe-item>
      <van-swipe-item>2</van-swipe-item>
      <van-swipe-item>3</van-swipe-item>
      <van-swipe-item>4</van-swipe-item>
    </van-swipe>
    <!-- 标签页商品展示 -->
    <van-tabs v-model="active">
      <van-tab title="热门推荐">
        <van-card
          v-for="item in 10"
          :key="item"
          price="2.00"
          title="商品标题"
          thumb="https://img.yzcdn.cn/vant/ipad.jpeg"
        >
          <template #footer>
            <van-button type="primary" size="small" icon="cart-o"></van-button>
          </template>
        </van-card>
      </van-tab>
      <van-tab title="发现新品">热门推荐</van-tab>
      <van-tab title="所有商品">所有商品</van-tab>
    </van-tabs>
  </div>
</template>

<script>
export default {
  data(){
    return {
       active: 0,
    }
  }
}
</script>

<style scoped>
.van-tabs.van-tabs--line{
  margin-bottom:50px;
}
  .my-swipe .van-swipe-item {
    color: #fff;
    font-size: 20px;
    line-height: 150px;
    text-align: center;
    background-color: #39a9ed;
  }
</style>

```

### index.vue(展示轮播图和商品数据)

```js
1.config/index.js
	proxyTable: {
      "/api":{
        target:"http://localhost:3000",
        changeOrigin:true,
        pathRewrite:{
          "^/api":"http://localhost:3000"
        }
      }
    },
 重启项目npm run dev 
2.utils/request.js
	import axios from 'axios';

    // 配置基础路径
    const baseUrl = '/api';


    // 响应拦截
    axios.interceptors.response.use(res=>{
      console.group("本次响应的路径为:"+res.config.url)
      console.log(res.data);
      return res.data
    })


    // 轮播图
    export const requestBanner = ()=>{
      return axios({
        method:'get',
        url:baseUrl+'/api/getbanner',
      })
    }

    // 获取首页商品信息
    export const requestIndexGoods = ()=>{
      return axios({
        method:'get',
        url:baseUrl+'/api/getindexgoods',
      })
    }
3.开发服务端
	npm start
4.index.vue 发起请求
	import {requestBanner,requestIndexGoods} from '../utils/request';
	 methods:{
    // 获取轮播图
    getBanner(){
      requestBanner().then(data=>{
        if(data.code == 200){
          this.bannerList = data.list
        }
      })
    },
    // 获取所有商品
    getIndexGoods(){
      requestIndexGoods().then(data=>{
        this.indexGoods = data.list;
      })
    }
  },
  mounted(){
    // 1.发起轮播图请求
    this.getBanner()
    // 2.发起获取商品请求
    this.getIndexGoods()
  }

```

### cate.vue(分类展示)

```vue
<template>
  <div class="cate-container">
     <!-- 导航 页头-->
    <van-nav-bar left-arrow  @click-left="$router.go(-1)"  title="分类" />
    <!-- 侧边导航 -->
      <van-sidebar v-model="activeKey">
        <van-sidebar-item v-for="(item,index) in firstCate" :key="item.id" :title="item.catename" @click="changeCate(index)" />
      </van-sidebar>
      <div class="aside">
        <van-grid :border="false" :column-num="3">
          <van-grid-item v-for="item in secondCate" :key="item.id" :to="`/goodsList?fid=${item.id}`">
            <van-image :src="$preImg+item.img" />
            <p>{{item.catename}}</p>
          </van-grid-item>
        </van-grid>
      </div>
  </div>
</template>

<script>
import {requestTreeCate} from '../utils/request';
export default {
  data(){
    return {
      activeKey:0,
      // 一级分类列表
      firstCate:[],
      // 二级分类列表
      secondCate:[],
    }
  },
  methods:{
    getCateList(){
      requestTreeCate().then(data=>{
        if(data.code == 200){
          this.firstCate = data.list
          this.changeCate(0)
        }
      })
    },
    // 改变一级分类时的回调
    changeCate(index){
      this.secondCate = this.firstCate[index].children
    }
  },
  mounted(){
    // 发起获取分类数据
    this.getCateList()
  }
}
</script>

<style scoped>
.aside{
  position: absolute;
  top:55px;
  right: 0;
  /* background: blue; */
  width: calc(100% - 80px);
}
</style>

```

### goodsList.vue(商品列表)

```vue
<template>
  <div class="goods-container">
      <!-- 导航 页头-->
      <van-nav-bar left-arrow  @click-left="$router.go(-1)"  title="商品列表" />
      <!-- 商品列表展示 -->
      <div v-if="goodsList !== null">
        <van-card
          v-for="item in goodsList"
          :key="item.id"
          :price="item.price"
          :title="item.goodsname"
          :thumb="$preImg+item.img"
        >
          <template #footer>
            <van-button type="primary" size="small" icon="cart-o"></van-button>
          </template>
        </van-card>
      </div>
      <van-empty
            v-else
            class="custom-image"
            image="https://img.yzcdn.cn/vant/custom-empty-image.png"
            description="暂无数据"
          />
  </div>
</template>

<script>
import {requestGoodsList} from '../utils/request';
export default {
  data(){
    return {
      goodsList:[],
    }
  },
  methods:{
    getGoodsList(){
      let fid = this.$route.query.fid;
      requestGoodsList({fid:fid}).then(data=>{
        if(data.code == 200){
          this.goodsList = data.list
        }
      })
    }
  },
  mounted(){
    this.getGoodsList()
  }
}
</script>

<style scoped>
.custom-image .van-empty__image {
    width: 90px;
    height: 90px;
  }
</style>

```

cart.vue(页面布局)

```vue
<template>
  <div class="cart-contaier">
       <!-- 导航 页头-->
    <van-nav-bar left-arrow  @click-left="$router.go(-1)"  title="购物车" />
      <!-- 购物车列表 -->
      <van-card
          v-for="item in 10"
          :key="item"
          price="2.00"
          title="商品标题"
          thumb="https://img.yzcdn.cn/vant/ipad.jpeg"
        >
          <template #footer>
            <van-stepper v-model="value" theme="round" button-size="22" disable-input />
          </template>
        </van-card>

       <van-submit-bar :price="3050" button-text="提交订单" @submit="onSubmit" />
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.cart-contaier{
  margin-bottom: 100px;
}
.van-submit-bar{
  bottom: 50px;
}

</style>

```

user.vue(页面布局)

```vue
<template>
  <div class="user-container">
      <!-- 导航 页头-->
    <van-nav-bar left-arrow  @click-left="$router.go(-1)"  title="会员中心" />
    <div class="header">
        <van-image
            round
            width="10rem"
            height="10rem"
            src="https://img.yzcdn.cn/vant/cat.jpeg"
          />
          <div>小U</div>
    </div>
    <div class="button">
      <van-button round  type="danger" size="large">安全退出</van-button>
    </div>
    <div class="section">
      <van-cell title="我的收藏" is-link />
      <van-cell title="我的评论" is-link />
      <van-cell title="我的订单" is-link  />
    </div>
  </div>
</template>

<script>
export default {

}
</script>

<style scoped>
.user-container{
  margin-bottom: 50px;
}
.header{
  height: 260px;
  background: #eee;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.button{
  margin:10px;
}
.section{
  padding:20px;
}
</style>

```

### login.vue(页面布局)

```vue
<template>
  <div class="login-container">
       <!-- 导航 页头-->
    <van-nav-bar  right-text="注册"   @click-right="$router.push('/register')" title="登录" />
    <van-form @submit="onSubmit">
        <van-field
          v-model="user.phone"
          label="手机号"
          placeholder="手机号"
          :rules="[{ required: true, message: '请填写手机号' }]"
        />
        <van-field
          v-model="user.password"
          type="password"
          label="密码"
          placeholder="密码"
          :rules="[{ required: true, message: '请填写密码' }]"
        />
        <div style="margin: 16px;">
          <van-button round block type="danger" native-type="submit">提交</van-button>
        </div>
      </van-form>
  </div>
</template>

<script>
export default {
  data(){
    return {
      user:{
        phone:'',
        password:'',
      }
    }
  },
  methods:{
    onSubmit(){
      console.log(this.user);
    }
  }
}
</script>

<style>

</style>

```

### register.vue(页面布局)

```vue
<template>
  <div class="register-container">
        <!-- 导航 页头-->
    <van-nav-bar  right-text="登录"   @click-right="$router.push('/login')" title="注册" />
    <van-form @submit="onSubmit">
        <van-field
          v-model="user.phone"
          label="手机号"
          placeholder="手机号"
          :rules="[{ required: true, message: '请填写手机号' }]"
        />
        <van-field
          v-model="user.nickname"
          label="昵称"
          placeholder="昵称"
          :rules="[{ required: true, message: '请填写昵称' }]"
        />
        <van-field
          v-model="user.password"
          type="password"
          label="密码"
          placeholder="密码"
          :rules="[{ required: true, message: '请填写密码' }]"
        />
        <div style="margin: 16px;">
          <van-button round block type="danger" native-type="submit">会员注册</van-button>
        </div>
      </van-form>
  </div>
</template>

<script>
export default {
    data(){
    return {
      user:{
        phone:'',
        nickname:'',
        password:'',
      }
    }
  },
  methods:{
    onSubmit(){
      console.log(this.user);
    }
  }
}
</script>

<style>

</style>

```

## 四.功能开发

### 1.注册

```
npm i qs --save 
```



```js
request.js
// 注册
export const requestRegister = (data)=>{
  return axios({
    method:'post',
    url:baseUrl+'/api/register',
    data:qs.stringify(data)
  })
}


register.vue
methods:{
    onSubmit(){
      requestRegister(this.user).then(data=>{
        if(data.code == 200){
          // 1.提示用户注册成功
          this.$toast.success(data.msg)
          // 2.跳转页面
          this.$router.push('/login');
        }
      })
    }
  }
```

### 2.登录

```js
request.js
// 登录
export const requestLogin = (data)=>{
  return axios({
    method:'post',
    url:baseUrl+'/api/login',
    data:qs.stringify(data)
  })
}

login.vue
 onSubmit(){
      requestLogin(this.user).then(data=>{
        if(data.code == 200){
          // 3.sessionStorage
          sessionStorage.setItem('user',JSON.stringify(data.list))
          // 1.跳转user页面
          this.$router.push('/user');
          // 2.登录成功的提示
          this.$toast.success(data.msg)


        }else{
          this.$toast.fail(data.msg)
        }

      })
    }
```

### 3.退出

```js
   logout(){
      // 1.将sessionStorage中的用户信息清空
      sessionStorage.removeItem('user')
      // 2.提示退出成功
      this.$toast.success('退出成功')
      // 3..跳转登录页面
      this.$router.push('/login')
    }
```

### 4.路由前置守卫

```js
// 路由全局前置守卫
/**
 * to:到哪个路由去
 * from:从哪个路由来
 * next:允许进入哪个路由
 */
router.beforeEach((to,from,next)=>{
  if(to.path == '/user'){
    const user = JSON.parse(sessionStorage.getItem('user') || '{}')
    if(!user.token){
      // 用户token不存在
      //提示请登录
      Toast.fail('请登录');
      //跳转登录
      router.push('/login');
      return
    }
  }
  next()
})
```



```js
// 重定向时捕获异常
const origin = Router.prototype.push;

Router.prototype.push = function push(localtion){

 return origin.call(this,localtion).catch(err=>err)

}

```

