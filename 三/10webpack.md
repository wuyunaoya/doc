## 什么是webpack

1. Webpack 前端资源模块化管理和打包工具。可以将许多松散的模块按照依赖和引用关系打包成符合生产环境部署的前端资源。并将按需加载的模块进行代码分隔，等到实际需要的时候再加载。

2. webpack功能

   它把所有的文件资源（js、json、css、sass,图片）都看作为模块

   \- 将这些文件资源 解析处理以后，生成对应的打包的文件

   webpack 是一个基于 Node.js 运行环境。用于打包本地文件之间相互依赖并最终输出成单个文件的工具.

   webpack 能够帮助我们解决模块之前相互依赖的问题.并把多个相互依赖的js文件生成一个js文件.

   3：webpack默认情况只识别js文件或者json文件

###   webpack.config.js文件

​	Webpack为开发者提供了程序打包的配置信息入口，让开发者可以更好的控制, 管理程序的打包过程与最后程序的输出结果。默认的webpack配置文件是webpack.config.js, 运行webpack打包命令, 会自动查看运行命令时, 所在目录下的webpack.config.js文件

### 核心概念讲解

官网链接: https://www.webpackjs.com/concepts/

| webpack的概念名 |                             解释                             |
| :-------------: | :----------------------------------------------------------: |
|    入口起点     | 基础目录, 指定了"./src"目录, 那么下面所有的配置中使用的相对路径, 都是以src为起点 |
|      入口       | 入口起点指示 webpack 应该使用哪个模块来作为构建其内部*依赖图*的开始<br />进入起点后，webpack 会找出有哪些模块和库是入口起点（直接和间接）依赖的 |
|                 |                                                              |
|      出口       | output告诉 webpack 在哪输出它所创建的结果及如何命名文件，默认值为 `./dist` |
|     加载器      | loader 让 webpack 能去处理非 JavaScript 文件(webpack 自身只理解 JavaScript）loader 可以将所有类型的文件转换为webpack 能够处理的有效模块<br />然后你就可以利用 webpack 的打包能力，对它们进行处理。 |
|      插件       | loader 被用于转换某些类型的模块，而插件则可以用于执行范围更广的任务。<br />插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量。<br />[插件接口](https://www.webpackjs.com/api/plugins)功能极其强大，可以用来处理各种各样的任务。 |

### 配置文件参数讲解

官网链接:  https://www.webpackjs.com/configuration/

| 键名    | 概念        | 解释                                                         |
| ------- | ----------- | ------------------------------------------------------------ |
| context | 入口起点    | 基础目录，**绝对路径**，用于从配置中解析入口起点(entry point) |
| entry   | 入口 (必须) | 配置打包入口文件的名字                                       |
| output  | 出口 (必须) | 打包后输出到哪里, 和输出的文件名                             |
| module  | 加载器配置  | 在rules对应数组中, 定义对象规则                              |
| plugins | 插件配置    | 配置插件功能                                                 |
| mode    | 模式        | 选择线上/线下环境模式                                        |

### webpack使用：

1：安装

  全局安装在

  打开cmd 运行：

  1.1. npm install webpack@3 -g      安装到全局

​          npm install webpack@3 --save-dev   安装到局部

   npm uninstall webpack@3 :卸载安装的文件

###  打包js模块代码

 1:初始化npm init -y

 2:规范目录结构

​            |- src 源文件  

​               |-app.js入口文件

​            |- dist 打包生成的文件

​               |—bundle.js打包生成的js

​            |- index.html

​            |- webpack.config.js  配置文件

​            |- package.json

​     3:在到src目录结构下创建模块

​     

​    4:打包命令 webpack 源文件 目标文件

​    webpack ./src/app.js ./dist/bundle.js



###    配置入口文件 单入口

```js
let path = require("path");
            module.exports = {
             //path.resolve 将相对路径的片段解析为绝对路径
             //规定入口文件 c:/demo1/src/app.js
             entry: path.resolve('./src/app.js'),//打包的路径
             //出口
             output:{
            //出口的路径
            path:path.resolve(__dirname,"./dist"), //将要打包程序路径
            //输出文件的名字
            filename:"bundle.js"
           },
        };
```


### 打包css代码

1:在到src目录下创建一个style.css文件,到app.js文件中加载style.css文件

 2:下载style-loader 和css-loader

npm i --save-dev style-loader@0.23.1  css-loader@1.0.0         

 3:到webpack.config.js文件里面配置使用下载style-loader 和css-loader

```js
module: {
//规则
rules: [{
//以.css为后缀名的文件 style.css
test: /\.css$/,
//使用style-loader css-loader
//loader的执行顺序是从右到左
use: ['style-loader','css-loader']
/*
css 解析css文件
style 动态的创建style标签 塞进去
*/
}]
}
```

4:需要到黑色窗口执行webpack 打包,浏览index.html页面



### 生成html文件

1:安装插件

npm i --save-dev html-webpack-plugin@3.2.0

2：在最外层index.html页面中写入:

```html
<p>webpack在打包后生成的html网页到dist目录下, 会以当前此文件为基准模板(在此文件基础上, 引入打包后的各种资源文件)</p>
```

3:webpack.config.js插件配置

```js
const HtmlWebpackPlugin = require("html-webpack-plugin");
 插件配置放置在css打包下方：
 plugins: [ // 配置插件
        new HtmlWebpackPlugin({ // 插件配置对象
            title: "webpack ldx使用", // 生成html网页里title标签里的值
            filename: "index.html", // 产出文件名(在dist目录查看)(名字尽量就叫index.html, 因为后期很多插件和功能找的都是index.html文件)
            template: __dirname + "/index.html", // 以此文件来作为基准(注意绝对路径, 因为此文件不在src下)
            inject: true, // 代表打包后的资源都引入到html的什么位置
            favicon: __dirname+"/src/assets/favicon.ico", // 插入打包后的favicon图标
            // base: "./", // html网页中所有相对路径的前缀 (一般不给/给./, 虚拟路径) 
            // 控制html文件是否要压缩(true压缩, false不压缩) 
            minify: {                             //对html文件进行压缩，
                    collapseBooleanAttributes: true,  //是否简写boolean格式的属性如：disabled="disabled"简写为disabled
                    collapseWhitespace: true,         //是否去除空格，默认false
                    minifyCSS: true,                  //是否压缩html里的css（使用clean-css进行的压缩） 默认值false
                    minifyJS: true,                   //是否压缩html里的js（使用uglify-js进行的压缩）
                    removeAttributeQuotes: true,      //是否移除属性的引号 默认false
                    removeComments: true,             //是否移除注释 默认false
                    removeCommentsFromCDATA: true,    //从脚本和样式删除的注释, 默认false
                    useShortDoctype: true             //使用短的文档类型，将文档转化成html5，默认false
             }
        }) // 数组元素是插件new对象
    ]
```

4：执行webpack



### 分离css代码

1:下载

npm i --save-dev extract-text-webpack-plugin@3.0.2

2：webpack.config.js加载器修改:

```js
const ExtractTextPlugin = require("extract-text-webpack-plugin"); 
module: { 
        rules: [
            { 
                test: /\.css$/, 
                use: ExtractTextPlugin.extract({ // 2. 从一个已存在的 loader 中，创建一个提取(extract) loader。
                    fallback: "style-loader",  // 应用于当CSS没有被提取(正常使用use:css-loader进行提取, 如果失败, 则使用fallback来提取)
                    use: "css-loader"  // loader被用于将资源转换成一个CSS单独文件
                })
            }
          ]
        },
         

    
    plugins: [ // 配置插件
	    new ExtractTextPlugin("css/index.css"), // 输出的文件名(会在dist目录下)
       
    ]



```

3:webpack打包



### 打包less

1:下载

npm install less@3.12.2 less-loader@5.0.0 --save-dev

2：在webpack.config.js中 配置加载器, 解析.less文件

需要更改原来的module里面的css打包和配置处理less文件

```js
module: { 
        rules: [
            { 
                test: /\.css$/, 
                use: ExtractTextPlugin.extract({
                    fallback: "style-loader", 
                    use: "css-loader"
                })
             },
			{ // 1. 配置处理less文件的加载器规则
                test: /\.less$/, 
                use: ExtractTextPlugin.extract({ // 以及分离less中的样式代码道单独的css文件中去
                    fallback: "style-loader", 
                    use: ['css-loader', "less-loader"]
                })
            }
          ]
        },
```

3:webpack 打包







### 压缩css文件(单个文件压缩 )

文件新建(不要复制)

1: npm install webpack@3 --save-dev   安装到局部

2：npm i --save-dev style-loader@0.23.1  css-loader@1.0.0       

3：npm i --save-dev extract-text-webpack-plugin@3.0.2

4：npm install --save-dev [optimize-css-assets-webpack-plugin@3.2.0](mailto:optimize-css-assets-webpack-plugin@3.2.0)

5 :  配置webpack.config.js

 const ExtractTextPlugin = require('extract-text-webpack-plugin') // css文件单独打包

 const OptimizeCssplugin = require('optimize-css-assets-webpack-plugin') // 压缩css文件

```js
module: {
  //规则
  rules: [{
            test: /\.css$/,
            use: ExtractTextPlugin.extract({
             fallback: 'style-loader',
             use: 'css-loader'
            })
           },
    ]
  },

  plugins:[
    //单独打包 生成的路径的
    new ExtractTextPlugin("style.css"), //生成css文件
    //压缩
    new OptimizeCssplugin() //压缩这个生成的css文件
  ]
```



### 压缩js文件

1：npm i --save-dev [webpack@3.1.0](mailto:webpack@3.1.0)

2: 配置webpack.config.js

​           var webpack = require("webpack");

​          plugins:[

​            //压缩js文件

​          new webpack.optimize.UglifyJsPlugin(),

​         ]

3:在到黑色窗口。运行webpack 打包,查看打包压缩之后的dist目录下bundle.js大小  





### 压缩图片（新建不要复制）

1:目录结构

​            |- src 源文件  

​               |-app.js入口文件

​            |- dist 打包生成的文件

​               |—bundle.js打包生成的js

​            |- index.html

​            |- webpack.config.js  配置文件

​            |- package.json

​     安装cnpm镜像指令：

​     npm install -g cnpm --registry=https://registry.npm.taobao.org 

​    2:初始化

​       cnpm init -y

   3:cnpm i --save-dev url-loader@1.1.2 file-loader@2.0.0 [image-webpack-loader@4.6.0](mailto:image-webpack-loader@4.6.0)

   4:cnpm i --save-dev webpack@3

   5:到src目录下拷贝一张图片,到app.js文件中加载.

   import "./2.jpg"



   6：配置webpack.config.js文件

```js
module: {
        //规则
        rules: [{
        //正则 匹配的是png jpg gif jpeg 
        test: /\.(png|jpg|gif)$/,
        use: [{
        loader: 'url-loader',
        options: {
        //大于byte 8192 加载本地
        //小于 base64
        //但是在文件大小（单位 byte）低于指定的限制时，
        //可以返回一个 DataURL。base64
        //大于limit 本地生成了一张图片
        limit: 10 * 1024, //100kb    

    }
    },
    
    {
    // 图片文件压缩
    loader: 'image-webpack-loader',
    options: {
    disable: false, // 启用.
    // jpg图片如何压缩
    mozjpeg: {
    progressive: true,
    quality: 70
    }
    }
    }
    ]
    }
    
    ] 

   }
```










### 小图标处理

​    

前端开发的过程中,会有很多的小图标.

  一般这些小图片都是以 .png结尾的背景透明的图片.

  这些小图标一般应用于一些按钮或者其他元素的图片.

  比如有一个按钮,需要一个相机的小图标.

  我们可能需要设置这样的 css 代码.

  首先,一般这些小图片的大小都很小.

  但不管有多小,都是一个http请求. background：url("./1.png")

  如果页面上的需要用到小图标的地方很多.

  比如有N个(假如是N张不同的小图片).

  那么就会有N个请求小图标的http请求.

  然而,浏览器的HTTP请求个数是有限制的.

  这样做无疑会浪费HTTP请求资源.

  常规做法

  之前的前端会让美工把所有的小图标布局到一张图片中.

  前端工程师,就根据这一张图片,来设置不同元素需要的背景图片.

  这里主要是搭配 background-poistion:x,y 来设置.

 具体的样式内容大概一般会是下面这个样子.

 

  .icon-Snip20190227_108 {

   background-image: url(../sprites/sprite.png);

   background-position: 0px 0px;

   width: 55px;

   height: 55px;

  }

  .icon-Snip20190227_109 {

   background-image: url(../sprites/sprite.png);

   background-position: 0px -57px;

   width: 69px;

   height: 66px;

  }

html中 使用

 <div class="icon-Snip20190227_109"></div>
 好处

  图片资源只有一个,所以请求的 HTTP 只有一次.

  即使第二个div的css中,又再次请求了一次

   background-image: url(../sprites/sprite.png);

   但实际上,这张图片已经被第一个div请求过来,

   并被浏览器缓存了.所以,

   第二个div背景图片资源实际上是来自浏览器缓存.



  麻烦点

  要事先和设计师沟通,把所有需要用到的小图标,

  都集成在一张图片中.

  我们需要拿到这张图片,利用 ps 

  等工具测量图标的大小,以及在整个图片中的 x,

  y坐标.

  最后,我们还需要为此编写一个特定的.css文件.

  <div class="icon-Snip20190227_112"></div>

​      webpack-spritesmith 插件自动的把零散的小图标生成一张大图.(小图标)

​     webpack-spritesmith 插件自动测量大图的中每一个小图标的大小以及位置,

  帮我们生成对应的 .css 文件.（css样式表）

(不用我们自己测量尺寸和位置以及编写.css文件)



​      第一步:1:初始化

​       npm init -y

​       3:cnpm install webpack-spritesmith@1.0.0 --save-dev

​       4:cnpm install webpack@3 --save-dev

​       5:cnpm i --save-dev [html-webpack-plugin@3.2.0](mailto:html-webpack-plugin@3.2.0)

​    第二步：

    ```js
到webpack.config.js中进行配置
plugins: [
new SpritesmithPlugin({
//目标的小图片
src: {
//小图标的路径
cwd: path.resolve(__dirname, 'src/icons'),
//后缀名是png
glob: '*.png'
},
        //生成文件的设置 生成两种东西 小图标 css
target: {
//小图标(大图的)文件存放路径
image: path.resolve(__dirname, 'dist/sprite/sprite.png'),
//生成的css路径
css: path.resolve(__dirname, 'dist/sprite/sprite.css')
},
//样式文件中 小图标的写法
apiOptions: {
cssImageRef: "./sprite.png"
},
//小图标生成的写法
spritesmithOptions:{
//如果排列及外边距 
algorithm:"top-down",//从上到下 默认是横着的
padding:2//每个小图标之间的间隙
}
}),
      
      
//html-webpack-plugin
//自动生成html 并自动引用生成的css文件，以模板生成新的html
new WebpackHtmlPlugin({
//模板
template:"index.html",
        //生成新的文件 所在路径 
        //注意：前边生成的小图标和css样式表 sprite
filename:"./sprite/a.html" //该路径参照根目录下模板index.html引入css的路径

})
]
    ```



   第三步：

   在根目录下的index.html中

   <link rel="stylesheet" href="./sprite.css">

​    </head>

​    <body>

    ```js
<link rel="stylesheet" href="./sprite.css">
    </head>
    <body>
   <div id="one"></div>
   <div id="two"></div>
   <div id="three"></div>
   <div id="four"></div>
    ```



第四步：

到src目录下把icon文件夹中图片拷贝过来，在新建一个 src/app.js 作为 webpack 打包的路口文件.

在里面键入

```js
document.getElementById('one').classList.add('icon-1')
document.getElementById('two').classList.add('icon-2')
document.getElementById('three').classList.add('icon-3')
```





在黑色窗口中webpack打包