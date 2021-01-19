# 一.数据交互

## 1.axios

名称:爱可信,爱可信基金会

axios是基于promise的ajax模块

## 2.安装

```
npm i axios --save
```



## 3.解决跨域问题

```js
z在config/index.js
 proxyTable: {
      "/api":{
        target:'http://localhost:3000',
        changeOrigin:true,//是否跨域
        pathRewrite:{
          "^/api":'http://localhost:3000'
        }
      }
    },

```



## 4.使用axios

```js
import axios from 'axios';
 axios({
        method:'post',
        url:'/api/login',
        data:{
          name:this.user.name,
          pass:this.user.pass,
        }
      }).then(res=>{
        if(res.data.isok){
          this.$router.push('/index')
          localStorage.setItem('dark',1);
          localStorage.setItem('userType',this.user.role)
        }else{
          alert(res.data.info)
          return
        }
      })
```



## 5.语法

```js
//get
axios({
    method:'get',
    url:'远程地址'
    
}).then(res=>{
    //请求成功的操作,有数据操作数据,没有数据,操作页面
})

//post
axios({
    method:'post',
    url:'远程地址',
    data:你提交的数据
}).then(res=>{
    //处理成功后的操作
})
```



# 二.登录请求方式

普通方式登录

```js
export const requestLogin = (data)=>{
  // 发送axios
  return axios({
    method:'post',
    url:'/api/login',
    data:data
  })
}
```

没有文件方式登录

```js
export const requestLogin = (data)=>{
  // 发送axios
  return axios({
    method:'post',
    url:'/api/login',
    data:qs.stringify(data)
  })
}
```

有文件方式登录

```js
export const requestLogin = (data)=>{
  // 发送axios
  var form = new FormData();
  form.append('name',data.name);
  form.append('pass',data.pass)
  return axios({
    method:'post',
    url:'/api/login',
    data:form
  })
}
```

# 三.响应拦截

```js
axios.interceptors.response.use(res=>{
  console.group('===响应拦截===')
  if(!res.data.isok){
    alert(res.data.info);
    return
  }
  console.log(res);
  return res
})
```

# 四.请求拦截

```
//请求拦截:用户拿着一个令牌访问整个项目,如果该令牌失效或者没有,直接出局
axios.interceptors.request.use(config=>{
  console.group('===请求拦截==')
  if(config.method.toUpperCase() == 'GET'){
    config.params = {}
  }
  config.params.token = '我是测试数据';
  console.log(config);
  return config
})
```



# 五.stylus

## 1.定义

stylus是一个css预处理器

## 2.什么是css预处理器

css预处理器为css提供了更多的灵活可编程性.

## 3.安装

```
npm i stylus stylus-loader@3.0.2 --save
```



## 4.新建styl文件

```
stylus/index.styl
stylus/color.styl
stylus/size.styl
```



## 5.引用

```css

<style lang="stylus">
@import './stylus/index.styl';
.h1
  color $primary-color
.h2
  color $warning-color
.btn
  color $success-color

</style>
```

# 面试题

```
1. vue-router是什么？它有哪些组件？
  答：Vue Router 是 Vue.js 官方的路由管理器。
  组件：router-link router-view
2. vue-router有哪几种导航钩子？ 他们有哪些参数

3. 怎么定义vue-router的动态路由？怎么获取传过来的动态参数？
  
4. Vue的路由实现：hash模式 和 history模式的区别？
5. $route和$router的区别？
  $route路由信息
  $router用来做路由跳转
6.如何让css只在当前组件起作用？
7.如何实现路由懒加载
8.在beforeRouteEnter可以使用this对象吗？
9.路由拦截如何实现？
```

