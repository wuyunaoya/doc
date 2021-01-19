# 一.路由

## 1.搭建一个项目

```
create-react-app meituan
npm i react-router-dom --save  安装路由
npm start  启动
```

## 2.清空工作

```
src
	App.js
	index.js
```

## 3.项目目录

```
src 	
	-assets 静态资源
	-components  公共组件
	-pages  你的代码
	utils    工具类
	App.js	根组件
	index.js  唯一入口
	
```

## 4.引入静态资源文件

```js
index.js
// 引入重置样式
import './assets/css/reset.css'
//引入js
import './assets/js/rem';
```

## 5.路由

### 1-1路由模式

```js
import {HashRouter,BrowserRouter} from 'react-router-dom'
//HashRouter:  http://localhost:3000/#/
//BrowserRouter: http://localhost:3000/

ReactDOM.render( 
<BrowserRouter>
<App />
</BrowserRouter>
,
  document.getElementById('root')
);
```

### 1-2路由出口

```js
import {Switch} from 'react-router-dom'
<Switch</Switch>
```

### 1-3路由规则配置

```js
import {Route} from 'react-router-dom'
 {/* 路由出口 Switch  相当于vue中的router-view*/}
      {/* 路由规则:Route    相当于vue中的routes */}
      <Switch>
        <Route path="/login" component={Login}></Route>
        <Route path="/index" component={Index}></Route>
        <Route path="/movie" component={Movie}></Route>
        <Route path="/movieDetail" component={MovieDetail}></Route>
        <Route path="/food" component={Food}></Route>
        <Route path="/foodDetail" component={FoodDetail}></Route>
      </Switch>
```

### 1-4重定向

```js
import {Redirect} from 'react-router-dom'
<Redirect to="/login"></Redirect>
```

### 1-5导航链接

- Link

```js
import {Link} from 'react-router-dom'
 <Link to="/index">首页</Link>
<Link to="/movie">电影</Link>
<Link to="/food">美食</Link>
```

- NavLink

```js
 import {NavLink} from 'react-router-dom'
<NavLink to="/index/home" activeClassName="select">首页</NavLink>
<NavLink to="/index/order" activeClassName="select">订单</NavLink>
<NavLink to="/index/mime" activeClassName="select">我的</NavLink>
```

### 1-6.编程式导航

- push  进入目标页面,返回上一级页面

```js
this.props.history.push('/movie')
```

- repalce 进入目标页面.替换掉原来的页面.返回上一级

```js
this.props.history.replace(url)
```

- go返回上一级

```js
 this.props.history.go(-1)
```

- goBack 返回上一级

```js
this.props.history.goBack()
```

在一些组件中,没有被路由规则包裹就属于普通组件,

- 在普通组件无法使用,编程式导航
- 想让普通组件变为路由组件.需要在外层包裹WithRouter

```js
import React, { Component } from 'react'
import {withRouter} from 'react-router-dom'
class GoBack extends Component {
    goback(){
        this.props.history.go(-1)
    }
    render() {
        return (
            <button onClick={()=>this.goback()}>返回</button>
        )
    }
}

export default withRouter(GoBack)

```



在一些组件中,又被路由规则包裹的就属于路由组件.

- 路由组件.可以使用,编程式导航

### 1-7路由传参

- :传参

```js
路由规则修改:
<Route path="/movieDetail/:id" component={MovieDetail}></Route>

传参
// : 传参
    this.props.history.push('/movieDetail/'+id)
接收参数
 const id = this.props.match.params.id;
```

- ?传参

```js
方式一:
    let search = this.props.location.search;//?id=1&name=aaa&age=20
    let searchNo = search.slice(1);//id=1&name=aaa&age=20
    let arr = searchNo.split('&');//[id=1,name=aaa,age=20]
    let result = {}
    arr.forEach(item => {
        let aa = item.split('=');//[id,1]
        result[aa[0]] = aa[1]
    });

方式二:
import querystring from 'querystring'
 let   result =  querystring.parse(this.props.location.search.slice(1))
```

### 1-8登录拦截(路由拦截)

1.需要自己封装路由拦截组件	MyRoute

```js
import React, { Component } from 'react'
import {Route,Redirect} from 'react-router-dom'

export default class MyRoute extends Component {
    render() {
        const user = sessionStorage.getItem('user')
        return (
            <div>
                {user ? <Route {...this.props}></Route> : <Redirect to="/login"></Redirect>}
            </div>
        )
    }
}

```

2.App.js

```js
// 将自己封装的路由规则导入
import MyRoute from './pages/MyRoute/MyRoute'
 <MyRoute path="/index" component={Index}></MyRoute>
 <MyRoute path="/movie" component={Movie}></MyRoute>
 <MyRoute path="/movieDetail/:id" component={MovieDetail}></MyRoute>
 <MyRoute path="/food" component={Food}></MyRoute>
 <MyRoute path="/foodDetail" component={FoodDetail}></MyRoute>
```

### 1-9懒加载

自己封装

```js
import React, { Component } from 'react'

function asyncComponents(fn) {
     class Zujian extends Component {
         constructor(){
             super()
             this.state = {
                 Obj : null
             }
         }
        componentDidMount(){
            // fn() 函数的调用的到结果就是promise
            fn().then((mode)=>{
                this.setState({Obj:mode.default})
            })
        }
        render() {
            const {Obj} = this.state;
            return (
                <div>
                    {Obj ? <Obj {...this.props}></Obj> : null}
                </div>
            )
        }
    }
     return Zujian
}
export default asyncComponents
```

使用懒加载

```js
import asyncComponent from './utils/asyncComponents'
const Login = asyncComponent(()=>import('./pages/Login/Login'));

const Index = asyncComponent(()=>import('./pages/Index/Index'));

const Movie = asyncComponent(()=>import('./pages/Movie/Movie'));

const MovieDetail = asyncComponent(()=>import('./pages/MovieDetail/MovieDetail'));

const Food = asyncComponent(()=>import('./pages/Food/Food'));

const FoodDetail = asyncComponent(()=>import('./pages/FoodDetail/FoodDetail'));
```

## 6.打包

```
npm run build
```

# 二.flux(状态管理)

Flux应用有三个主要部分：Dispatcher调度 、存储Store和视图View(React 组件)

flux是单项数据流

```
npm i flux --save
```

```js
store.js 做数据存储
import ee from './events'
const store = {
    // 声明的一个数据
    state:{
        num:0
    },
    // 添加方法
    addNum(){
        this.state.num += 1;
        // console.log(this.state.num);
        ee.emit('message')
    },
    // 减少方法
    reduceNum(){
        this.state.num -=1;
        // console.log(this.state.num);
        ee.emit('message')
    }
}
export default store
```

```js
// Dispatcher是一个构造函数,做调度
import {Dispatcher} from 'flux'
import store from './store';
// 实例化dispatcher对象
const dispatcher = new Dispatcher()
// dispatcher 有一个方法register
// register有一个参数:  是一个匿名函数
// action:{type:'类型',data:'额外参数'}
dispatcher.register(function(action){
    switch (action.type) {
        case 'add':
            // 走添加方法
            store.addNum()
            break;
        case 'reduce':
            // 走添加减少
            store.reduceNum()
            break;
        default:
            break;
    }
})
export default dispatcher
```

```js
视图层
import React, { Component } from 'react'
import dispatcher from '../../utils/dispatcher';
import store from '../../utils/store';
import ee from '../../utils/events'
export default class Order extends Component {
    constructor(){
        super()
        this.state = {
            // num:''
        }
    }
    render() {
        const {num} = store.state
        ee.on('message',()=>{
            // console.log(store.state);
            this.setState(store.state)
        })
        return (
            <div>
               {num}
               <div>
                   <button onClick={()=>this.add()}>添加</button>
                   <button onClick={()=>this.reduce()}>减少</button>
               </div>
            </div>
        )
    }
    add(){
        // 添加操作
        const action = {type:'add'}
        dispatcher.dispatch(action)
    }
    reduce(){
        const action = {type:'reduce'};
        dispatcher.dispatch(action)
    }
}
```

# 面试题

```
1.react router和常规路由有何不同？
    答案：
        参与的页面：
            reactRouter：只涉及单个HTML页面；
            常规路由：每个视图对应一个新文件。
        URL更改：
            reactRouter：仅更改历史记录属性
            常规路由：http请求被发送到服务器并且接收相应的html页面
        体验：
            reactRouter：用户认为自己正在不同的页面间切换
            常规路由：用户实际在每个视图的不同页面切换
2.当你调用setState的时候，发生了什么事？
    答案：
        当调用 setState 时，React会做的第一件事情是将传递给 setState 的对象合并到组件的当前状态。这将启动一个称为和解的过程。和解的最终目标是以最有效的方式，根据这个新的状态来更新UI。 为此，React将构建一个新的 React 元素树（您可以将其视为 UI 的对象表示）。
        一旦有了这个树，为了弄清 UI 如何响应新的状态而改变，React 会将这个新树与上一个元素树相比较（ diff ）。
        通过这样做， React 将会知道发生的确切变化，并且通过了解发生什么变化，只需在绝对必要的情况下进行更新即可最小化 UI 的占用空间。
    
    3.在 React 当中 Element 和 Component 有何区别？
    答案：
        一个 React element 描述了你想在屏幕上看到什么。换个说法就是，一个 React element 是一些 UI 的对象表示。
        一个 React Component 是一个函数或一个类，它可以接受输入并返回一个 React element

    4.React中路由有哪些常用组件？说明它们的作用？

    答案：
        BrowserRouter，在需要使用路由的页面中引入；
        Switch，路由选择器
        Route，路由配置规则
        Redirect，路由重定向
        Link，路由导航
        NavLink，带activeClass的路由导航
        WithRouter 使用路由规则
    5.为什么虚拟 dom 会提高性能?
    答案：虚拟DOM其实就是一个JavaScript对象。通过这个JavaScript对象来描述真实DOM。
    为什么用虚拟dom？真实DOM的操作，一般都会对某块元素的整体重新渲染。采用虚拟DOM的话，当数据变化的时候，只需要局部刷新变化的位置就好了。
    
     6.在 React 中，refs 的作用是什么？
    答案：Refs 是 React 提供给我们的安全访问 DOM 元素或者某个组件实例的句柄。我们可以为元素添加 ref 属性然后在回调函数中接受该元素在 DOM 树中的句柄，该值会作为回调函数的第一个参数返回。 用于对 render() 返回的特定元素或组件的引用。当需要进行 DOM 测量或向组件添加方法时，它们会派上用场。
    
     7.(组件的)状态(state)和属性(props)之间有何不同?
    答案：state是一种数据结构，用于组件挂载时定义数据的默认值。修改state使用setState,会触发render函数执行，渲染页面。
    props是由父组件传递给子组件的。对于子组件而言，props是不可变的。
    
    8.(在构造函数中)调用 super(props) 的目的是什么?
    答案：在super被调用之前，子类是不能使用this的，在ES5中，子类必须在constructor中调用super().
    传递props给super()的原因则是便于子类能在constructor中访问this.props 
```

