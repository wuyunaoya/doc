# 一.组件通信

## 1.父组件向子组件传递数据

### 实现步骤

- 父组件通过自定义属性进行传值
- 子组件中通过`this.props`进行接收数据

```jsx
父组件传值
<Child msg={this.state.msg} pageTitle={this.state.pageTitle}/>
    
 子组件接收
<div>{this.props.msg}</div>
<div>{this.props.pageTitle}</div>
```

## 2.子组件向父组件传递数据

### 实现步骤

- 父组件通过自定义属性,传递一个方法体
- 子组件中通过this.props接收父组件的方法体,同时进行调用,在调用时通过参数的形式将子组件数据传递过去
- 父组件中通过自定义的方法进行接收子组件的数据

父组件

```jsx
import React, { Component } from 'react'
import Child from './Child'
export default class Parent extends Component {
   state = {
     msg:'父组件的msg',
     pageTitle:'父组件的新闻首页',
     getChildMsg:'',
   }
    render() {
        return (
            <div className="alert alert-info">
                <h1>父组件</h1>
                {this.state.getChildMsg}
                <hr />
                <Child msg={this.state.msg} pageTitle={this.state.pageTitle} message={(e)=>this.sendMessage(e)}/>
            </div>
        )
    }
    sendMessage(event){
        // console.log(event);
        this.setState({getChildMsg:event})
    }
}

```

子组件

```jsx
import React, { Component } from 'react'

export default class Child extends Component {
    state = {
        msg:'子组件的msg'
    }
    render() {
        
        return (
            <div className="well">
                <h1>子组件</h1>
                <div>{this.props.msg}</div>
                <div>{this.props.pageTitle}</div>
                <button className="btn btn-info" onClick={()=>this.send()}>发送数据</button>
            </div>
        )
    }
    send(){
       this.props.message(this.state.msg)
    }
}

```

## 3.非父子通信

- 借助父向子及子向父间接实现

弊端:父子组件出现错综复杂的关系时,这种方式就不可取

- 使用自定义方式实现
- events是一个插件, 在https://www.npmjs.com/package/events

```
npm i events --save
```

```jsx
在components/Event.js
// 引入events
import EventEmitter  from 'events'
// 得到events对象
const ee = new EventEmitter ()

// 导出ee对象
export default ee
```

```
使用
 ee.emit('message',this.state.msg)
监听
 ee.on('message',(obj)=>{
            this.setState({msg:obj})
        })
```



# 二.表单处理

## 1.手动实现双向数据绑定

```jsx
import React, { Component } from 'react'

export default class Form extends Component {
    state = {
        msg:''
    }
    render() {
        return (
            <div className="alert alert-info">
                <h1>数据双向绑定</h1>
                <input type="text" onChange={(e)=>this.changeMsg(e)} value={this.state.msg} />
                <div>{this.state.msg}</div>
            </div>
        )
    }
    changeMsg(event){
        // console.log(event.target.value);
        this.setState({msg:event.target.value})
    }
}

```

```
总结:
组件通信:
	父传子: 自定义属性进行传值,this.props接收数据
	子传父: 自定义属性传递一个方法体,this.props接收方法体.,调用方法体,(传递参数)
	非父子: events插件ee.emit('自定义的事件名称',传递的数据)
					 ee.on('自定义的事件',(obj)=>{传递的数据就会进入回调函数中})
			
 表单处理
 	<input type="text" onChange={(e)=>this.send(e)} value={this.sate.msg}/>
 	send(event){
 		this.setState({msg:event.target.value})
 	}
 生命周期:
 	创建阶段:
 		componentWillMount  组件将要挂载
 			可以操作数据,不能操作真实dom
 		render:  编译jsx模板
 			可以操作数据,不能操作真实dom
 		componnetDidMount:  组件挂载完成
 			可以数据,操作真实dom
 	运行阶段:
 		shouldComponentUpdate:
 			必须有返回值:  true 更新视图  false不更新视图
 		componentWillUpdate  组件数据将要更新
 			没有完成数据更新
 			不能操作真实dom
 		render	编译模板
 			没有完成数据更新
 			不能操作真实dom
 		componentDidUpdate  组件更新完成
 			完成数据更新
 			操作真实dom
```



# 三.生命周期

定义:指一个组件从创建到销毁的一个过程.

钩子函数:在整个生命周期过程中,某一特定的时刻,系统方法被自动触发.

## 1.创建阶段

- `componentWillMount `:组件将要挂载
  - 可以操作数据,不能操作真实的DOM
  - 执行次数:1次
- `render`jsx模板编译(将jsx编译为虚拟DOM )
  - 可以操作数据,不能操作真实的DOM
  - 执行次数:1次
- `componentDidMount`:组件挂载完成
  - 可以操作数据,可以操作真实的DOM
  - 执行次数:1次

```jsx
import React, { Component } from 'react'

export default class Life extends Component {
    state = {
        msg:'钩子函数'
    }
    // 组件将要挂载
    componentWillMount(){
        console.log("=====componentWillMount=====");
        console.log(this.state.msg);
        // 不能操作真实的dom节点
        // console.log(document.querySelector('h1').innerHTML);
    }
    render() {
        console.log("=====render=====");
        console.log(this.state.msg);
        // 不能操作真实的dom节点
        // console.log(document.querySelector('h1').innerHTML);
        return (
            <div>
                <h1>生命周期</h1>
            </div>
        )
    }
    // 组件挂载完成
    componentDidMount(){
        console.log("=====componentDidMount=====");
        console.log(this.state.msg);
        console.log(document.querySelector('h1').innerHTML);
    }
    
}

```



## 2.运行阶段

- `shouldComponentUpdate` 应该更细组件吗
  - 特点
    - 写`shouldComponentUpdate`在方法中必须有返回值,true:继续更新  false:不更新
    - return true  `componentWillUpdate`=>`render`:=>`componentDidUpdate`
    - return false  不执行
  - 作用:
    - 在企业开发中,有些业务逻辑不需要让用户看到更新的数据.
    - 性能调优
  - 系统自动注册的参数
    - nextProp: 没有获取到最新额props数据
    - nextState: 获取到状态层的最新数据
- `componentWillUpdate`:组件将要更新
  - 特点
    - 没有更新数据,
    - 视图没有更新
  - 系统自动注册的参数
    - nextProp: 没有获取到最新props数据
    - nextState: 获取到状态层的最新数据
- `render`:jsx模板渲染
  - 特点
    - 数据已经更新完成
    - 视图没有更新
- `componentWillReceiveProps`:组件将要接收props传递的数据
  - 特点
    - 当父组件向子组件传递数据并更新数据时,被自动触发
  - 系统自动注册的参数
    - nextProp: 获取到最新props数据
    - nextState: 没有获取到状态层的最新数据
- `componentDidUpdate`组件更新完成
  - 特点
    - 数据已经更新完成
    - 视图已经更新
  - 系统自动注册的参数
    - preveProp: 没有获取到最新之前的props数据
    - preveState: 获取到状态层更新之前的数据

## 3.销毁阶段

- `componentWillUnmonut`: 组件将要卸载

```jsx
Life.jsx
import React, { Component } from 'react'
import Child from './Child'
export default class Life extends Component {
    state = {
        msg:'钩子函数',
        isShow:true
    }
    send(){
        this.setState({msg:'数据更新'})
    }
    destroy(){
        this.setState({isShow:!this.state.isShow})
    }
    // 组件将要挂载
    componentWillMount(){
        console.log("=====componentWillMount=====");
        // console.log(this.state.msg);
        // 不能操作真实的dom节点
        // console.log(document.querySelector('h1').innerHTML);
    }
    render() {
        console.log("=====render=====");
        console.log(this.state.msg);
        // 不能操作真实的dom节点
        // console.log(document.querySelector('h1').innerHTML);
        return (
            <div>
                <h1>{this.state.msg}</h1>
                <button className="btn btn-info" onClick={()=>this.send()}>发送数据</button>
                
                <button type="button" class="btn btn-danger" onClick={()=>this.destroy()}>销毁</button>
                
                {this.state.isShow ? <Child msg={this.state.msg}></Child> : ''}
            </div>
        )
    }
    // 组件挂载完成
    componentDidMount(){
        console.log("=====componentDidMount=====");
        console.log(this.state.msg);
        console.log(document.querySelector('h1').innerHTML);
    }

    //应该更新组件吗?
    //作用:性能调优
   shouldComponentUpdate(nextProp,nextState){
       console.log("====shouldComponentUpdate=====");
       console.log(nextProp,nextState);
        return true
   }

    // 组件将要更新
    componentWillUpdate(nextProp,nextState){
        console.log("====componentWillUpdate====");
        console.log(this.state.msg);
        console.log(document.querySelector('h1').innerHTML);
        console.log(nextProp,nextState);
    }

    //组件更新完成
    componentDidUpdate(prevProp,prevState){
        console.log("====componentDidUpdate====");
        console.log(this.state.msg);
        console.log(document.querySelector('h1').innerHTML);
        console.log(prevProp,prevState);
    }
    
}

```

```jsx
Child.jsx
import React, { Component } from 'react'

export default class Child extends Component {
    render() {
        return (
            <div>
                <h2>子组件</h2>
                <div>{this.props.msg}</div>
            </div>
        )
    }
    componentWillReceiveProps(nextProp,nextState){
        console.log('======componentWillReceiveProps=======');
        console.log(nextProp,nextState);
    }
    componentWillUnmount(){
        console.log('======componentWillUnmount=======');
    }
}

```





# 四.ref属性

作用:操作dom元素和子组件

- ref属性操作dom元素

方式一:

```jsx
 {/* 方式一 */}
<div ref="div">ref方式一</div>

 <button type="btn tbn-info" onClick={()=>this.send()}>发送数据</button>
send(){
    // 方式一
    console.log(this.refs);
    this.refs.div.style.color = 'white';
    this.refs.div.style.background = 'blue';
    this.refs.div.style.border = '2px  solid yellow';
}

```

方式二:

```jsx
 {/* 方式二 */}
{/* 系统自制了一个dom */}
<div ref={(dom)=>this.add=dom}>ref方式二</div>
<button type="btn tbn-info" onClick={()=>this.send()}>发送数据</button>

  send(){
        // 方式二
        console.log(this.add);
        this.add.style.color = 'blue';
        this.add.style.background = 'red';
        this.add.style.border = '2px dashed orange';
  }
```

方式三

```jsx
  constructor(){
        super()
        // 创建一个ref对象
        this.divRef = React.createRef()
    }
{/* 方式三 */}
 <div ref={this.divRef}>ref方式二</div> 
 <button type="btn tbn-info" onClick={()=>this.send()}>发送数据</button>
 send(){
        // 方式三
        // console.log(this.divRef);
        this.divRef.current.style.color = 'red';
        this.divRef.current.style.background = 'yellow';
        this.divRef.current.style.border = '5px solid blue';

    }
```

- ref属性操作子组件

```jsx
 <button type="btn tbn-info" onClick={()=>this.send()}>发送数据</button>

 <Child ref={dom=>this.childRef=dom}></Child>
send(){
      console.log(this.childRef.state.msg);
      this.childRef.message()
}
```



# 五.插件使用

## 1.react-awesome-swiper轮播图插件

安装

```
npm i react-awesome-swiper --save
```

utils/Banner.jsx

```jsx
import React, { Component } from 'react'
import AwesomeSwiper from 'react-awesome-swiper';

export default class Banner extends Component {
    swiperRef = null
    config = {
        loop : true,
        autoplay: {
          delay: 3000,
          stopOnLastSlide: false,
          disableOnInteraction: true,
        },
        // Disable preloading of all images
        preloadImages: false,
        // Enable lazy loading
        lazy: true,
        speed: 500,
        navigation: {
          nextEl: '.swiper-button-next',
          prevEl: '.swiper-button-prev',
        },
        pagination: {
          el: '.swiper-pagination',
          bulletElement : 'li',
          hideOnClick :true,
          clickable :true,
        },
        on: {
          slideChange: function () {
            // console.log(this.activeIndex);
          },
        },
      }
    render() {
        return (
          <AwesomeSwiper ref={ref => (this.swiperRef = ref)} config={this.config} className="your-classname">
            <div className="swiper-wrapper">
            {this.props.imgs.map((item,index)=>(
                 <div className="swiper-slide" key={index}>
                    <img src={item} alt=""/>
                </div>
            ))}
            </div>
            <div className="swiper-button-prev"></div>
            <div className="swiper-button-next"></div>
            <div className="swiper-pagination"></div>
          </AwesomeSwiper>
        )
      }
}

```



# 六.UI组件库

## ant-design组件库

安装

```
npm i antd -S
在index.js入口文件中:
	import 'antd/dist/antd.css';
按需导入
import {Button,Divider,Space,Card  } from 'antd'
```

icon图标库

```
npm install --save @ant-design/icons
import {AppleFilled,UpCircleFilled} from '@ant-design/icons'
```

```jsx
import React, { Component } from 'react'
import Banner from '../utils/Banner';
import {Button,Divider,Space,Card  } from 'antd'
import {AppleFilled,UpCircleFilled} from '@ant-design/icons'
export default class Index extends Component {
    imgs=[
        '/slider/01.jpg',
        '/slider/02.jpg',
        '/slider/03.jpg',
    ]
    render() {
        return (
            <div>
                <AppleFilled style={{fontSize:'50px',color:'green'}}/>
                <UpCircleFilled />
                <Divider />
                <Space>
                    <Button type="primary">Primary Button</Button>
                    <Button type="dashed">Dashed Button</Button>
                    <Button type="primary" danger>Primary</Button>
                </Space>
                <Card title="Default size card" extra={<a href="#">More</a>} style={{ width: '100%' }}>
                    <p>Card content</p>
                    <p>Card content</p>
                    <p>Card content</p>
                 </Card>
                
                <Divider />
                <Banner imgs={this.imgs}></Banner>
            </div>
        )
    }
}

```

# 作业

1,案例写2遍