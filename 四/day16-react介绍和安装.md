# react介绍和安装

## 一.介绍

react是Facebook公司中前端开发团队进行开发和维护.

定义:

​	用于构建用户界面的 JavaScript 库

特点:

- 基于组件化的开发
- 数据驱动和视图进行相结合的开发模式
- 渲染模板也是使用虚拟DOM
- react中没有基本指令,计算属性,过滤器,监听的概念 
- react没有自动的数据双向绑定
- React 是react.js的核心对象
- ReactDOM是react-dom.js的核心对象

## 二.下载安装

1.手动下载,通过script标签引入

```js
<script src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
```

2.npm 在线下载安装

```
npm i react -save
```

## 三.核心对象及方法介绍

- React
  - React 是react.js的核心对象

```
React.createElemnt('标签名','属性集合',内容)
```

- ReactDOM
  - ReactDOM是react-dom.js的核心对象

```
ReactDOM.render(标签对象,真实的dom对象)
```



## 四.开发流程

- 基础代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!--development:开发模式  -->
    <!-- 
        react是react.js的核心
        react-dom是react-dom.js的核心
     -->
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
</head>
<body>
    <!-- 有一个容器 -->
    <div id="app"></div>
</body>
<script>
    // React 是react.js的核心对象
    // React.createElement('标签名','属性集合',内容)
    //得到标签对象
    const h1 = React.createElement('h1',{title:'第一次学习react'},'hello react')
    // console.log(h1);

    // 将标签对象插入到真实的dom节点中
    //ReactDOM是react-dom.js的核心对象
    //ReactDOM.render(标签对象,真实的dom对象)
    ReactDOM.render(h1,document.querySelector('#app'))
</script>
</html>
```



- 嵌套代码

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!--development:开发模式  -->
    <!-- 
        react是react.js的核心
        react-dom是react-dom.js的核心
     -->
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <style>
        .container{
            background-color: aqua;
            color: palevioletred;
        }
    </style>
</head>
<body>
    <!-- 有一个容器 -->
    <div id="app"></div>
</body>
<script>
    // React 是react.js的核心对象
    // React.createElement('标签名','属性集合',内容)
    //得到标签对象
    const h1 = React.createElement('h1',{title:'第一次学习react'},'hello react')
    const img = React.createElement('img',{src:'./img/food.jpg'},null)
    const div = React.createElement('div',{className:'container'},h1,img)

    // 将标签对象插入到真实的dom节点中
    //ReactDOM是react-dom.js的核心对象
    //ReactDOM.render(标签对象,真实的dom对象)
    ReactDOM.render(div,document.querySelector('#app'))
</script>
</html>
```

## 五.jsx模板语法介绍

- jsx是在js的基础上结合了xml语法
- jsx不能被浏览解析
- jsx是通过babel进行解析
- jsx模板语法主要应用于react项目的构建中

### 1.xml语法结构(简单了解)

- xml只能有一个根节点
- 双标签必须要有开始和结束
- 单标签必须要有结束符
- xml严格区分大小写

### 2.jsx语法结构

- jsx模板必须严格遵循xml语法
- jsx模板语法中只能有一个根节点
- jsx模板语法中双标签必须有开始和结束
- jsx模板语法中单标签必须要有结束

### 3.jsx模板语法

- 基本使用

```jsx
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <!--development:开发模式  -->
    <!-- 
        react是react.js的核心
        react-dom是react-dom.js的核心
     -->
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <!-- 1.引入babel -->
    <script src="./libs/babel.min.js"></script>
    <style>
        .container{
            background-color: aqua;
            color: palevioletred;
        }
    </style>
</head>
<body>
    <!-- 有一个容器 -->
    <div id="app"></div>
</body>
<!-- 2.作用: 浏览器在解析是,看到是babel,就不做解析,交给babel进行解析-->
<script type="text/babel">
    // 3.使用jsx
    /*
    1.jsx模板语法只能有一个根节点
    2.在jsx模板语法中一定不能有'',如果有''就当做字符串进行处理
    */
    const div = <div className="container">
                    <h1>hello react</h1>
                    <img src="./img/food.jpg" />
                </div>
    console.log(div);
    // 将标签对象插入到真实的dom节点中
    //ReactDOM是react-dom.js的核心对象
    //ReactDOM.render(标签对象,真实的dom对象)
    ReactDOM.render(div,document.querySelector('#app'))
</script>
</html>
```

- 模板变量的使用
  - {}在jsx模板语法中解析变量

```jsx
<script type="text/babel">
    const msg = 'hello react';
    const imgSrc = './img/food.jpg';
    // 3.使用jsx
    /*
    1.jsx模板语法只能有一个根节点
    2.
    */
    const div = <div className="container">
                    <h1>{msg}</h1>
                    <img src={imgSrc} />
                </div>
    console.log(div);
    // 将标签对象插入到真实的dom节点中
    //ReactDOM是react-dom.js的核心对象
    //ReactDOM.render(标签对象,真实的dom对象)
    ReactDOM.render(div,document.querySelector('#app'))
</script>
```

- 模板方法的使用
  - 系统方法,直接调用
  - 自定义方法 ,在自定义方法中必须要有return

```jsx
<script type="text/babel">
    const msg = 'hello react';
    function reverse(str){
        return  str.split('').reverse().join('')
    }
    
    // 3.使用jsx
    /*
    1.jsx模板语法只能有一个根节点
    2.
    */
    const div = <div className="container">
                    {/*jsx模板语法中系统的方法*/}
                    <h1>{msg.toUpperCase()}</h1>
                    {/*jsx模板语法中自定义方法*/}
                    <div>{reverse(msg)}</div>
                    
                </div>
    console.log(div);
    // 将标签对象插入到真实的dom节点中
    //ReactDOM是react-dom.js的核心对象
    //ReactDOM.render(标签对象,真实的dom对象)
    ReactDOM.render(div,document.querySelector('#app'))
</script>
```

- 模板注释

```jsx
 {/*这里是jsx模板的注释*/}
```

- 条件渲染
  - 不能使用if结构进行条件判断
  - 只能使用三元运算符进行条件判断

```jsx
<script type="text/babel">
    const age = 18;
    const div = <div className="container">
                    {/*不能使用if结构进行条件判断*/}
                    {/*<div>{if(age>=18){}else{}}</div>*/}

                    {/*使用三元运算符做条件判断*/}
                   { /*<div>{age >= 18 ? '已经成' : '未成年'}</div>*/}

                    <div>{age >= 18 ? <h2>已经成</h2> : <p>未成年</p>}</div>
                </div>
    
    //ReactDOM.render(标签对象,真实的dom对象)
    ReactDOM.render(div,document.querySelector('#app'))
</script>
```

- 关键字
  - `className`: 进行css样式选择器中的class改为`className`
  - `htmlFor`:在label标签中将for属性改为`htmlFor`

```jsx
<script type="text/babel">
    
    const div = <div className="container">
                    <label htmlFor="search">关键字搜索</label>
                    <input type="text" id="search" placeholder="请搜索关键字" />
                </div>
    
    //ReactDOM.render(标签对象,真实的dom对象)
    ReactDOM.render(div,document.querySelector('#app'))
</script>
```

- 通过`style`指定行内样式
  - {} 外层 : 表示jsx模板语法
  - {}内层:  表示js对象

```jsx
<script type="text/babel">
    const obj = {backgroundColor:'yellow',color:'pink',border:'1px solid blue'}
    const div = <div>
                    {/*
                    1.{}外层的{}表示jsx语法
                    2.{}内容的{}表示js对象
                    */}
                    <h1 style={obj}>hello</h1>
                </div>
    
    //ReactDOM.render(标签对象,真实的dom对象)
    ReactDOM.render(div,document.querySelector('#app'))
</script>
```

- 列表的渲染
  - forEach | map    在遍历的直接子元素上绑定key
  - key作用: 在数据和试图层做一一对应的关系，方便试图进行局部更新

```jsx
<script type="text/babel">
   const arr = ['vue','react','angular']
   const arr1 = [<h2 key="0">赵丽颖</h2>,<h2 key="1">王一博</h2>,<h2 key="2">范冰冰</h2>]

    //forEach  没有返回
    const arr2 = []
    arr.forEach(item=>{
        arr2.push(<h2 key={item}>{item}</h2>)
    })

    //map  有返回值
    const arr3 = arr.map(item=><h2 key={item}>{item}</h2>)


    // 复杂的数组
    const brandList = [
        {
            id:1,
            name:'香奈儿包包',
            price:60000
        },
        {
            id:2,
            name:'爱马仕鳄鱼皮包包',
            price:600000
        },
        {
            id:3,
            name:'好利来包包',
            price:899
        },
    ]

    const div = <div className="container">
                    {/*直接将数组中的是当做字符串统一展示出来*/}
                   { /*{arr}*/}
                    <hr />
                    {arr1}
                    <hr />
                    {arr2}
                    <hr />
                    {arr3}
                    <hr />
                    {arr.map(item=><h2 key={item}>{item}</h2>)}
                    <hr />
                    <h1>品牌列表</h1>
                    {brandList.map(item=><h3 key={item.id}>{item.name}------{item.price}</h3>)}

                    </div>
    
    ReactDOM.render(div,document.querySelector('#app'))
</script>
```

- 富文本
  - dangerouslySetInnerHTML={{__html:变量名}}

```jsx
<script type="text/babel">
    const editer = `<div>
                        <h1>商城首页</h2>
                        <img src="./img/food.jpg" />
                    </div>`
    const div = <div className="well">
                    <div dangerouslySetInnerHTML={{__html:editer}}></div>
                </div>
    
    //ReactDOM.render(标签对象,真实的dom对象)
    ReactDOM.render(div,document.querySelector('#app'))
</script>
```

## 六.组件

### 函数组件

- 使用规范
  - 使用函数方式进行声明，首字母必须的大写
  - 函数中必须有返回值
  - 返回值值只能有一个根组件
- 父组件向函数组件传值
  - 父组件通过自定义属性进行传值
  - 函数组件通过参数进行接收传递的数据  结果是一个{}

```jsx
<script type="text/babel">
// 函数组件
/*
1.首字母必须大写
2.必须有返回值
*/
   function Header(params){
       console.log(params);
    return <div>
                <h2>{params.pageTitle}</h2>
                <p>{params.news}</p> 
            </div>
   }

   function Footer(){
       return <div>
                <h4>底部导航</h4>
            </div>
   }
   const pageTitle = '首页';
   const news = '新闻列表';
    const div = <div className="well">
                    <Header pageTitle={pageTitle} news={news}/>
                    <hr />
                    <Footer />
                </div>


    
    //ReactDOM.render(标签对象,真实的dom对象)
    ReactDOM.render(div,document.querySelector('#app'))
</script>
```

```
总结上午知识点:
	1.React	react.js的核心对象
		React.createElement('标签名','属性集合',内容)
	2.ReactDOM react-dom.js的核心对象
		ReactDOM.render(标签对象,真实dom对象)
	3.jsx模板语法
		变量: {}  在{}写js语法
		方法: {方法名()}
		条件: 不能if结构,必须使用三元运算符
		列表:  forEach   map 
		关键字: className  htmlFor
		注释: {/*这里写注释*/}
		style:  {{}}  外层{}表示jsx语法  内层{}表示js对象
		富文本:  dangerouslySetInnerHTML={{__html:富文本变量}}
	4.函数组件
		function Header(){return }
		//函数名首字母大写  
		//函数中要有返回值
```

### 类组件

- 语法规范

​	  1.类名首字母必须大写

 	 2.在定义的类组件中,必须继承自 React.Component基类

  	3.类组件中有一个系统自定的方法render(渲染jsx模板)

  	4.在render方法必须要有返回值

  	5.返回值中只能有一个根组件

- 组件传值
  - 父组件中也是自定义属性进行传值
  - 类组件中通过this.props进行接收自定义属性

```jsx
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link href="https://cdn.bootcdn.net/ajax/libs/twitter-bootstrap/3.3.7/css/bootstrap.min.css" rel="stylesheet">
    <!--development:开发模式  -->
    <!-- 
        react是react.js的核心
        react-dom是react-dom.js的核心
     -->
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <!-- 1.引入babel -->
    <script src="./libs/babel.min.js"></script>
</head>
<body>
    <!-- 有一个容器 -->
    <div id="app"></div>
</body>
<!-- 2.作用: 浏览器在解析是,看到是babel,就不做解析,交给babel进行解析-->
<script type="text/babel">
    /*
    1.类名首字母必须大写
    2.在定义的类组件中,必须继承自 React.Component基类
    3.类组件中有一个系统自定的方法render(渲染jsx模板)
    4.在render方法必须要有返回值
    5.返回值中只能有一个根组件
    */
    class PageTitle extends React.Component{
        // 系统中有一个render,
        render(){
            console.log(this.props);
            return <div>
                        <h1>首页</h1>
                        <p>{this.props.pageTitle}</p>
                    </div>
        }
    }
 
    const pageTitle = '新闻列表';
    const div = <div className="well">
                    <PageTitle pageTitle={pageTitle}></PageTitle>
                </div>


    
    //ReactDOM.render(标签对象,真实的dom对象)
    ReactDOM.render(div,document.querySelector('#app'))
</script>
</html>
```

## 七.脚手架

### 1.安装

```
npm i create-react-app -g   全局安装
create-react-app  -V   查看安装版本
```

### 2.项目初始化

```
create-react-app 项目名称
```

### 3.启动服务

```
cd demostart
npm start
```

### 4.项目打包

```
npm run build
```

```
目录介绍
config:  项目的配置文件
public   index/html  项目的唯一一个页面
src   	你的代码
		App.js  根组件
		index.js 唯一入口文件
```



案例

```jsx
import React, { Component } from 'react'

export default class Case extends Component {
    render() {
        return (
            <div>
                <h1>新闻列表</h1>
            </div>
        )
    }
}


App.jsx
import Case from './pages/Case';
function App() {
  return (
    <div className="App">
      <Case />

    </div>
  );
}

export default App;
```

## 八.事件处理

### 1.事件注册

​	   1.事件名称写法: on+事件名称(首字母必须大写)={事件函数}

​        2.事件函数后面不能有小括号(),因为:模板在编译的时候会自动触发事件函数

```jsx
<input type="text" onChange={this.hander}/>  //不加小括号
 <button className="btn btn-primary" onClick={function(){this.hander()}.bind(this)}>发送</button>  //将事件函数放入函数体中,可以加()

//箭头函数
<button className="btn btn-danger" onClick={()=>this.hander()}>发送1</button>
```

### 2.事件传参

```jsx
 <button className="btn btn-primary" onClick={function(){this.hander('王源')}.bind(this)}>发送</button>
 
 hander(params){
        alert('我被触发了'+params);
    }
```



### 3.通过箭头函数实现事件传参

```jsx
<button className="btn btn-danger" onClick={()=>this.hander('王俊凯')}>发送1</button>
  hander(params){
        alert('我被触发了'+params);
    }
```

## 九.事件对象(event)

```jsx
使用箭头函数传递event对象
<button className="btn btn-danger" onClick={(e)=>this.hander(e)}>发送1</button>
hander(event){
        console.log(event);
        // alert('我被触发了');
    }
```



## 十.组件状态数据的定义和更新

```jsx
import React, { Component } from 'react'

export default class Login extends Component {
    name:'aa',
    constructor(){
        super()
        // 状态层数据,相当于vue中得我data()
        this.state = {
            pageTitle :'林更新',
        }
    }
    // 页面一加载,该方法会被自动执行
    render() {
        // console.log(this.state);
        return (
            <div>
                <h1>状态层数据</h1>
                <div>{this.state.pageTitle}</div>
                <div><button className="btn btn-info" onClick={()=>this.changeName()}>改为刘德华</button></div>
            </div>
        )
    }
    changeName(){
        // this.state.pageTitle = '刘德华';
        // console.log(this.state);

        // 修改状态层的数据,同时更新到视图层

        this.setState({pageTitle:'刘德华'},()=>{
            console.log(this.state);
        })
        
    }
}

```

```jsx
修改状态层的数据并且同时更新到视图层需要使用this.setState()
  this.setState({pageTitle:'刘德华'},()=>{
            console.log(this.state);
        })
```



## 十一.品牌管理案例

```jsx
import React, { Component } from 'react'

export default class Brand extends Component {
    constructor(){
        super()
        this.state = {
            brandList:[
                {
                    id:2,
                    name:'宝马',
                    time:Date.now()
                },
                {
                    id:1,
                    name:'大众',
                    time:Date.now()
                }
            ],
            current:{}
        }
    }

    submit(event){
       if(event.keyCode === 13){
        let name = event.target.value;
          if(event.target.value === ''){
              return alert('请输入品牌名称')
          }
        //   判断当前走的添加还是修改
        if(this.state.current.id){
            // 这里修改
            this.update(this.state.current.id,name)
        }else{
            this.add(name)
        }
          event.target.value = ''
       }
    }

    //添加品牌名称
    add(name){
        let id = this.state.brandList.length > 0 ? this.state.brandList[0].id+1 : 1;
        let time = Date.now()
        let  arr = {
            id,
            name,
            time
        }

        //将添加的数据插入brandList中
        this.state.brandList.unshift(arr)
        // 将状态层最新数据更新到视图层
        this.setState({brandList:this.state.brandList})
    }
    // 删除品牌
    del(id){
        // 根据i找到索引
        const index = this.state.brandList.findIndex(item=>item.id === id);
        //根据索引删除数组中的数据
        this.state.brandList.splice(index,1)
        // 更新视图
        this.setState({brandList:this.state.brandList})
    }
    edit(row){
        document.querySelector('input').value = row.name;
        this.state.current = row;
        
    }
    // 修改
    update(id,name){
        let index = this.state.brandList.findIndex(item=>item.id === id)
        this.state.brandList[index].name = name;
        this.state.brandList[index].time = Date.now()
        this.setState({brandList:this.state.brandList})
        this.setState({current:{}})
    }
    render() {
        return (
            <div className="container">
                <h1>品牌管理列表</h1>
                <div className="well">
                    <input className="form-control" type="text" placeholder="请输入品牌名称" onKeyUp={(e)=>this.submit(e)}/>
                </div>
                <table className="table table-hover">
                    <thead>
                        <tr>
                            <th>编号</th>
                            <th>名称</th>
                            <th>创建时间</th>
                            <th>操作</th>
                        </tr>
                    </thead>
                    <tbody>
                        {this.state.brandList.map(item=>(<tr key={item.id}>
                                        <td>{item.id}</td>
                                        <td>{item.name}</td>
                                        <td>{item.time}</td>
                                        <td>
                                            <button onClick={()=>this.edit(item)} className="btn btn-primary">编辑</button>
                                            <button onClick={()=>this.del(item.id)} className="btn btn-danger">删除</button>
                                        </td>
                                    </tr>
                        ))}
                        
                        
                    </tbody>
                </table>
            </div>
        )
    }
}

```

# 作业:

1.案例敲两遍

2.品牌管理案例3遍