# 一.redux(状态管理)

```
npm i redux --save  安装
```

redux不仅可以使用react,也可以结合其他框架进行开发

- store(专门做数据存储对象)

  - ```js
    import {createStore} from 'redux'
    //得到就是store对象
    ?
    const store = createStore(fn)
    export default store
    ```

- state

  - ```js
    store.getState()  //获取数据存储对象中的数据
    ```

- action

  - ```js
    const action = {type:'操作类型',data:'自定义的数据'}
    ```

- ### store.dispatch()

  - store.dispatch()是有视图(view)发出来的
  - dispatch中有一个参数:action

- store.subscribe()

  - // 监听state数据发生改变的回调

  - ```js
    store.subscribe(()=>{
      hander()
    })
    ```

# 二.优音乐项目

## 1.启动服务端数据接口

```js
npm i 
npm start
http://localhost:4000/
```

## 2.搭建移动端服务

```js
create-react-app music
```

## 3.安装依赖项

```js
npm i axios andt @andt-design/icons react-router-dom --save
```

## 4.修改监听端口

```JS
在package.json文件中修改端口号
"scripts": {
    "start": "set port=5001&&node scripts/start.js",
}
```

## 5.清空工作

```js
src
	App.jsx
	index.js
```

## 6.重置样式

```js
assets
	css 
    	reset.css
在index.js引入
	
```

## 7.项目开发

### 1-1:layout布局

```js
import React, { Component } from 'react'
import { PageHeader,Button, } from 'antd';
import {NavLink,HashRouter as Router,Switch,Route} from 'react-router-dom'
import '../assets/css/layout.css'
import asyncComponents from '../components/asyncComponents'
const Commonet = asyncComponents(()=>import('./Commonet'));
const Hot = asyncComponents(()=>import('./Hot'));
const Search = asyncComponents(()=>import('./Search'));

export default class Layout extends Component {
    render() {
        return (
            <Router>
                 <div className="layout">
                {/* 头部 */}
                <div className="head">
                    {/* 页头 */}
                    <PageHeader
                        className="site-page-header"
                        title="优音乐"
                    />
                    <Button  size="middle" >下载App</Button>
                 </div>
                {/* 导航 */}
                <div className="nav">
                    <NavLink to="/commonet" activeClassName="select">推荐</NavLink>
                    <NavLink to="/hot" activeClassName="select">热歌</NavLink>
                    <NavLink to="/search" activeClassName="select">搜索</NavLink>
                </div>
                {/* 路由出口 */}
                <Switch>
                    <Route path="/commonet" component={Commonet}></Route>
                    <Route path="/hot" component={Hot}></Route>
                    <Route path="/search" component={Search}></Route>
                </Switch>
            </div>
            </Router>
           
        )
    }
}

```

需要引入懒加载

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

### 1-2comment(布局和数据请求)

banner  歌单推荐  最新音乐

```js
import React, { Component } from 'react'
import { Carousel,Row, Col,List } from 'antd';
import {PlayCircleOutlined} from '@ant-design/icons'
import '../assets/css/comment.css'

export default class Commonet extends Component {
    constructor(){
        super()
        this.state = {
            // banner图
            bannerList : [],
            // 推荐歌单列表
            commentList:[],
            // 最新音乐列表
            newList:[]
        }
    }
    render() {
        // console.log(this.$axios);
        return (
            <div className="commonet">
               {/* 轮播图 */}
                <div className="banner">
                    <Carousel autoplay>
                        {this.state.bannerList.map((item,index)=>(
                            <div key={index}>
                                <img style={{width:'100%'}} src={item.imageUrl} alt=""/>
                            </div>
                        ))}
                        
                        
                    </Carousel>
                </div>
                {/* 推荐热歌 */}
                <div className="section">
                    <h3>推荐歌单</h3>
                    <Row gutter={16}>
                        {this.state.commentList.map(item=>(
                            <Col className="gutter-row" span={8} key={item.id}>
                                <div>
                                    <img style={{width:'100%'}} src={item.picUrl} alt=""/>
                                    <h3 style={{textAlign:'center'}}>{item.name.substr(0,10)}</h3>
                                </div>
                            </Col>
                        ))}
                    </Row>
                </div>
                {/* 最新音乐 */}
                <div className="section">
                    <h3>最新音乐</h3>
                    <List
                        dataSource={this.state.newList}
                        renderItem={item => (
                            <List.Item
                            actions={[<PlayCircleOutlined  style={{fontSize:'22px'}}/>]}
                            >
                            {item.name}
                            </List.Item>
                        )}
                        />
                </div>
            </div>
        )
    }

    componentDidMount(){
        // 发起轮播图请求
        this.getBanner()
        // 发起推荐歌单请求
        this.getComment()
        // 发起最新音乐请求
        this.getNewMusic()
    }
    // 获取banner图请求
    getBanner(){
        this.$axios.get('/banner').then(res=>{
            if(res.code === 200){
                this.setState({bannerList:res.banners})
            }
        })
    }
    // 获取推荐歌单
    getComment(){
        this.$axios.get('/personalized').then(res=>{
            if(res.code === 200){
                this.setState({commentList:res.result})
            }
        })
    }

    // 获取推荐音乐
    getNewMusic(){
        this.$axios.get('/personalized/newsong').then(res=>{
            if(res.code === 200){
                this.setState({newList:res.result})
            }
        })
    }
}

```

### 1-3hot.jsx(布局和数据请求)

```jsx
import React, { Component } from 'react'
import {List} from 'antd'
import {PlayCircleOutlined} from '@ant-design/icons'
import '../assets/css/hot.css'
export default class Hot extends Component {
    constructor(){
        super()
        this.state = {
            hotList :[],
        }
    }
    render() {
        return (
            <div className="hot">
                <div className="img">
                    
                </div>
                {/* 热歌列表 */}
                <List
                    dataSource={this.state.hotList}
                    renderItem={item => (
                        <List.Item
                        key={item.id}
                        actions={[<PlayCircleOutlined  style={{fontSize:'22px'}}/>]}
                        >
                        {item.name}
                        </List.Item>
                    )}
                    />
            </div>
        )
    }

    componentDidMount(){
        this.getHot()
    }

    // 获取热歌列表
    getHot(){
        this.$axios.get('/top/list',{params:{idx:1}}).then(res=>{
            if(res.code === 200){
                this.setState({hotList:res.playlist.tracks})
            }
        })
    }
}

```

### 1-4search.jsx(布局和数据请求)

```js
import React, { Component } from 'react'
import {Input,Button,Divider,Space,List } from 'antd'
import {SearchOutlined,PlayCircleOutlined} from '@ant-design/icons'
import '../assets/css/search.css'
export default class Search extends Component {
    constructor(){
        super()
        this.state = {
            keyWords:'',
            searcList:[],
            hotSearchList:[]
        }
    }
    // 做双向数据绑定
    changeKey(e){
        this.setState({keyWords:e.target.value})
    }
    submit(e){
        if(e.keyCode === 13){
            if(this.state.keyWords.trim() === ''){
                return alert('请输入关键字')
            }
            this.getKeyWords(this.state.keyWords)
        }
    }
    // 根据热门关键字进行搜索
    handler(key){
        this.setState({keyWords:key})
        this.getKeyWords(key)
    }
    render() {
        return (
            <div className="search">
                <div className="sear">
                <Input size="middle"
                 placeholder="请输入关键字" onKeyUp={(e)=>this.submit(e)} onChange={(e)=>this.changeKey(e)} value={this.state.keyWords}  prefix={<SearchOutlined />} />
                </div>
                {/* 分割线 */}
                <Divider />
                <Space>
                    {this.state.hotSearchList.map((item,index)=>(
                         <Button onClick={()=>this.handler(item.first)}  size="middle" key={index} shape="round">{item.first}</Button>
                    ))}
                   
                   
                </Space>
                {/* 列表展示 */}
                <List
                    dataSource={this.state.searcList}
                    renderItem={item => (
                        <List.Item
                        key={item.id}
                        actions={[<PlayCircleOutlined  style={{fontSize:'22px'}}/>]}
                        >
                        {item.name}
                        </List.Item>
                    )}
                    />
            </div>
        )
    }

    componentDidMount(){
        this.getHotSearch()
    }

    getHotSearch(){
        this.$axios.get('/search/hot').then(res=>{
            if(res.code === 200){
                this.setState({hotSearchList:res.result.hots})
            }
        })
    }

    getKeyWords(data){
        this.$axios.get('/search',{params:{keywords:data}}).then(res=>{
            if(res.code === 200){
                this.setState({searcList:res.result.songs})
            }
        })
    }
}

```



