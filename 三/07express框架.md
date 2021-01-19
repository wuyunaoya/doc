### 一:express框架

express框架:轻量级应用框架。随取随用API快速开发.web应用程序开发框架.

好处:

1：快速搭建项目和快速开发

2：有利于后期项目维护

3：有利于团队开发

使用express框架:

2种安装方式使用:

##### (1):使用包下载安装使用

   1:初始化项目包

​    npm init -y  (初始化只需要初始化一次)

​    2:下载相关包,express 框架

​    npm i express --save-dev(依赖安装)



##### (2):使用express框架

  ```js
//加载框架
let express = require("express");
//创建应用服务 
let app = express();
//规划路由
app.get("/",(req,res)=>{
  res.send("这是框架");
})
//监听端口
app.listen(3000);
  ```



##### (3):路由规划

路由规划:地址栏输入不同地址，切换到他相应的内容中.

127.0.0.1:3000/index

输出这是首页

127.0.0.1:3000/admin

输出这是后台

(4):get和post区别?

表单中：action=“交互数据地址(通常是后台的地址)”

method="get/post"  提交数据方式有get和post默认是get提交方式

get方式提交:

http://127.0.0.1:3000/login?username=admin&username=admin

(1):提交的数据可以在地址栏中可见

(2):提交的数据不怎么安全

(3):提交的数据是有大小的限制

post方式提交:

http://127.0.0.1:3000/login

(1):提交的数据在地址栏是不可见的

(2):提交的数据比较安全

(3):提交的数据是没有大小限制



规划路由的时候：

什么时候使用get规划路由，声明时候使用post规划路由:

get规划路由:加载静态页面或者是从数据库中读取数据使用get规划路由(get渲染页面,加载数据)

get规划:加载静态页面文件(html   css   js   images  json)   前端

127.0.0.1:3000  加载首页页面

pots规划路由:表单提交数据，需要交互数据时使用post规划路由.(处理表单提交数据逻辑功能)



##### (4)特殊路由规划

+:匹配+号前面的字符，匹配1个或者多个

?:匹配？号前面的字符，匹配0个或者1个

`*匹配*号所在的位置`

(匹配的字符)  匹配整体的字符

/a/ :只要路由中有这个字符，且整个路由满足条件

/abcd$/ : 以这个匹配的字符结尾，整个路由满足条件



##### (5):all中间件

app.all("/规划路由",(req,res)=>

)

表单提交不管是get提交还是post提交，这个all他都会去接收。不好，数据不怎么安全。



##### (6):二级路由规划

127.0.0.1:3000/user/login  登录

127.0.0.1:3000/user/reg    注册

express.Router()  即可以规划路由，也可以规划二级路由.



##### (7):获取地址栏参数值

127.0.0.1:3000/index/0001

req请求中包含方法:

 app.get(“/路由/:参数名（自定义名字,不能取数字名字,不能关键字)

 ```js
app.get("/index/:id",(req,res)=>{
    res.send("你获取的编号:"+req.params.id);
})
 ```

req.params.参数名    获取地址栏输入的参数值

req.body     获取表单提交文本框输入的值

req.query   获取表单提交地址栏显示的参数值

req.cookie  存储临时数据

router()

### (8):中间件

express框架自身只有1000多行代码,比较简洁。但是功能比较强大.express框架是由web服务和中间件构成。

中间件可以去调用req（请求）和res（响应）



中间件:中间过渡层(接口)

中间件分为:

##### (1):路由层中间件

   ```js
规划路由层 a.js:
let express = require("express");
let router = express.Router();
router.get("/login",(req,res)=>{
    res.send("这是登录")
})
router.get("/reg",(req,res)=>{
    res.send("这是注册")
})
module.exports = router;


主入口层  app.js:
let abcd = require("./07二级路由规划");
//中间件
app.use("/user",abcd);
   ```

##### (2):自定义中间件

    ```js
app.use((req,res,next)=>{
    req.abcd = new Date(); 
    console.log("123");
    next();
 })
    ```

##### (3):错误处理中间件

```js
app.use((req,res,next)=>{
    res.status(404).send("你访问的路由不存在");
})
//注意 放置在所有规划路由的下方
```

##### (4):内置中间件 (重点)

  静态资源:指的就是(css   js   json  ajax  images)

 ```js
express.static(加载静态资源文件地址目录)
 ```

  

##### (5):第三方中间件(重点)

###### 1：获取表单数据中间件

下载body-parser

npm i body-parser --save-dev

加载body-parser包

let bodyParser = require("body-parser");

使用中间件进行配置:

```js
//{extended:false}  表单提交的数据以json或者数组的格式进行解析
//{extended:true}   可以解析为任意的数据类型
//表单提交使用{extended:false} 这是为了表单提交数据的安全
 app.use(bodyParser.urlencoded({extended:false}));

 获取文本框输入的值:
 req.body
```

###### 2:cookie 中间件

 cookie(缓存) 临时存储

 特性:

1:cookie是存储在客户端的

2:cookie存储的数据不安全

3:cookie读取数据比较快



登录拦截:

1：下载cookie-parser

npm i cookie-parser

2:加载cookie-parser

let cookie = require("cookie-parser");

3:使用中间件配置

app.use(cookie())

4:使用cookie存储数据

   res.cookie("标签名（自定义名字）",存储的值)

```js
 res.cookie("username",username);
```

5:获取cookie里面存储的值

   req.cookies.标签名



总结： express框架规划路由

​            中间件（内置中间件，第三方中间件）

​           req请求下方法

​          



作业:

(1):规划路由

规划首页路由

规划注册路由

规划登录路由

(2):使用cookie做登录拦截(里面存储的用户不能写死)







