一：node模块认知 

node他是由模块和包构成,模块：指的是封装好的功能.叫做模块.模块遵守了CommonJs规范.

每个模块都拥有他自身功能.每个模块的功能是不一样的.

模块:

1:node自身核心模块

fs模块:对系统文件操作（对系统文件读取和写入操作）

直接加载核心模块.

let fs = require("模块名");

2:http模块(主要交互数据,构建一个服务器)

创建服务格式1：

1:加载http模块

let http = require("http");

2：交互数据

地址栏输入一个地址:127.0.0.1:3000

3:监听端口

 格式1：

 第一个参数：绑定端口

 第二个参数：绑定地址

 server.listen(3000,"127.0.0.1",()=>{

 })

4:解析数据

​     解析头部文件数据

​     text/html :解析为html网页

​     text/css  :解析css文件

​     images/jpg :解析图片文件

​     application/json 解析json

​     text/plain 安装原样输出

​     res.writeHead(状态码,{解析内容})

创建服务格式2：

1:加载http模块

let http = require("http")

2:创建应用服务(有了服务之后，才可以把本地数据交互浏览器中响应)

let server = http.Server();

3:响应内容触发事件 

on 触发一个事件 

第一个参数：触发绑定的事件 request

第二个参数：回调函数

(req,res): req:请求

​           res:响应

server.on("request",(req,res)=>{



})

3：事件模块

1:加载events事件模块

let events = require("events");

let event =new  events.EventEmitter();//有了这个方法，可以自己定义事件名，绑定事件触发。 

on()  监听触发多次事件内容

once() 监听触发一次事件内容



4:认知路由

路由:地址栏输入不同地址，切换到他对应的地址栏下内容

127.0.0.1:3000/index

127.0.0.1:3000/admin

5:url模块

加载url模块(解析一个字符串地址,解析到他相应的内容参数中)

let url = require("url");

第一个参数：解析字符串地址

第二个参数:设置为true，之后解析字符串内容中有一个query属性会装换为对象的格式.默认是false不启用.

第三个参数:设置为true之后，解析的地址默认是由http开头也可以是https开头,设置为true之后，可以省略这个开始头部。他默认自动识别。

let parses = url.parse("字符串地址",true,true); 



6：静态网页文件以动态方式加载

 静态网页：.html   .htm

 静态资源:  js   json css  images

 地址栏输入一个规划地址:127.0.0.1:3000

加载网页首页,渲染过来首页的网页.

全局方法(魔术方法) 直接拿来使用:

__dirname : 获取当前项目完整跟目录地址

__filename : 获取当前模块的完整路径地址



7:path模块(处理路径和获取文件后缀名)

 let path = require("path");



2:自定义模块

模块:一个js文件就是一个模块.他遵守了CommonJs规范.

模块文件中定义的属性和方法都是私有的，外部文件是不能直接访问使用的。

外部文件要想访问，那么就要遵守CommonJs规范..

CommonJs规范：指的是模块的暴露方式.

格式1:

暴露属性名

exports.属性名 = 值

暴露方法:

exports.方法名 = ()=>{

}



格式2：

暴露属性名

module.exports.属性名 = 值

暴露方法:

module.exports.方法名 = ()=>{

}

暴露多个内容:

module.exports={

暴露内容1，

暴露内容2

}

注意:

加载模块：

1：核心模块加载

let fs = require("fs");

2:加载自定义模块

let m = require("./模块名");

(1):加载核心模块不能要模块的后缀名，而自定义的模块的后缀可以要可以不要。

(2):自定义加载模块要有路径./  或者是../  但是核心模块不能有路径./或者是../

​      这个加载是为了自定义模块和核心模块区分开来.



exports暴露和module.exports暴露区别？

(1):模块加载机制

   当你执行模块，模块执行过程中就会生成一个函数

  ```js
function(exports,require,model,__filename,__dirname)
  ```

 exports:模块暴露格式

 require:加载模块

model:模块暴露    exports.属性名=值   module.exports.属性名= 值

__filename:获取当前模块完整路径地址

__dirname:获取当前项目跟目录完整路径地址



(2):exports暴露和module.exports暴露区别？

a:先暴露exports不去暴露module.exports,exports只是一个收集者，他收集的属性和方法，都会赋值给module.exports



b:先暴露module.exports,不去暴露exports,module.exports有自己暴露，那么就指向自己暴露的地址内容，而exports还是指向原来的{}对象数据.



注意：后期再项目中使用，只能选择其中一种格式。一个模块中不能出现2种暴露格式.



3:第三方包模块

 包下载的指令:

   npm -v 查看npm的版本
•  npm version 查看所有模块的版本
•  npm init 初始化项目（创建package.json）
•  npm i/install 包名 安装指定的包    @版本号，不加版本默认为最新
•  npm i/install 包名 --save 安装指定的包并添加依赖
•  npm i/install 包名 -g 全局安装（一般都是一些工具）
•  npm i/install 安装当前项目所依赖的包
•  npm s/search 包名 搜索包	
•  npm r/remove 包名 删除一个包

npm 官网:

//下载时间包:

 time-stamp:时间戳包

第一步:

格式1：

初始化项目包(功能：后期可以这个文件中可以查看当前项目中下载了哪些包文件)

npm init 

注意：项目的跟目录文件名不能是关键字，你的项目跟目录文件是中文的，这个是可以识别读取.

在项目中生成一个package.json文件.



格式2（推荐使用）

npm init -y

注意：最外层的项目目录名字不能用中文



下载包:time-stamp:时间戳包

npm i  time-stamp



配置淘宝镜像:（国外的服务器改为国内的服务器）

npm config set registry https://registry.npm.taobao.org



作业:

1:加载小u商场  动态方式渲染静态资源文件 小u商场首页

127.0.0.1:3000



2:规划路由

127.0.0.1:3000/index/0001

输出你获取的首页的编号为0001

127.0.0.1:3000/admin/0002

输出你获取的登录的编号为0002



3:下载time-stamp包(走下载包的流程)



总结 :理解 路由概念

​          理解 静态文件以动态方式加载 

​          下载一个包(流程)

​          配置镜像环境

​          模块暴露

