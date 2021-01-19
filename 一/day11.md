# 一、新增结构标签

新增了页眉、页脚、内容块等文档结构相关标签，可以让文档结构更加清晰明确

![模块布局](模块布局.png)![h5模块布局](h5模块布局.png)

### 1、header

定义文档中的头部或者一个模块的头部，通常可以包含这个页面或者模块的标题、logo、搜索框等。

### 2、footer

定义文档中的的尾部或者一个模块的尾部，通常可以包含页面中的版权信息、相关阅读链接。

### 3、nav

定义导航链接部分，一般用于主要导航链接组传统导航条、侧边导航、页内导航、翻页导航等。

```html
<nav>
    <a href="#">首页</a>
    <a href="#">列表页</a>
    <a href="#">关于我们</a>
</nav>
```

### 4、article

定义文档中独立完整的、可以独自被外部引用的内容。如一篇博文、论坛的帖子、报刊中的文章、一段用户评论或独立的插件。

### 5、section

定义页面中内容的分区或文章的章节。section 区域通常由标题及内容组成。

### 6、aside

定义侧边栏，页面或文章的附属信息。与主要内容相关的引用、广告、链接组等。

### 7、hgroup

可以为标题或者子标题分组，通常与h1-h6组合使用

```html
<hgroup>
	   <h1> 主标题 </h1>
 	   <h2> 副标题</h2>
</hgroup>
```

### 8、address

联系信息，通常包含文档的作者，编辑者的名字，电子邮箱，地址，电话号码等，自带倾斜效果

# 二、新增其他标签

### 1、figure>figcaption

定义独立的流内容（图片、图表、照片、代码等）

```html
<figure>
    	<img src="./王祖贤.jpg" alt="">
    	<figcaption>王祖贤</figcaption>
</figure>
```

### 2、mark

带标记的文本

```html
今天是个好日子，明天要<mark>放假</mark>  <!--默认黄色背景 -->
```

### 3、time

定义公历日期或时间

```html
抢购倒计时：<time>0:0:0</time>
今年<time datetime="2020-10-01">国庆</time>和<time datetime="2020-10-01">中秋</time>是同一天
```

### 4、progress

进度条  max最大值  value最小值

```html
<progress></progress>
<progress max="365" value="200"></progress>
```

### 5、canvas 图形容器

# 三、HTML5已移出的标签

以下的 HTML 4.01 标签在 HTML5 中已经被删除：

（1）acronym   首字母缩写

（2）applet   嵌入    html4.01 不赞成

（3）basefont   页面上的默认字体颜色和字号    html4.01 不赞成

（4）big   大号字体效果

（5）center   文字居中

（6）dir  目录列表

（7）font   文本的字体、字体尺寸、字体颜色

（8）frame   frameset 中的一个特定的窗口（框架）

（9）frameset   简单的多框架页面

（10）noframes  为那些不支持框架的显示文本

（11）strike  加删除线文本   html4.01 不赞成

# 四、HTML5标签兼容处理

#### 第一种方法：js创建标签

```js
	// 创建一个新标签
    var header=document.createElement("header");
    header.innerHTML="header区域"

   // 把新标签放到body
    var body=document.getElementById("body")
    body.appendChild(header)// 给body添加一个孩子
```

```css
 header{
     height: 100px;
     background-color: pink;
     display: block;/* js创建的标签是内联标签 */
}
```

#### 第二种方法：引入已经封装好的html5shiv.js

# 五、audio 音频

2007年苹果宣布不再支持flash

Internet Explorer 9+、 Firefox、Opera、Chrome 和 Safari 

| 格式 | MIME-type  | 支持的浏览器                              |
| ---- | ---------- | ----------------------------------------- |
| ogg  | audio/ogg  | Chrome、Firefox、Opera10+                 |
| wav  | audio/wav  | chrome、Firefox、Opera10+、Safari5+       |
| mp3  | audio/mpeg | Chrome、Firefox、Opera10+、Safari5+、IE9+ |

```html
 <audio src="./videoAudio/biubiubiu.ogg" controls loop>
        您的浏览器不支持audio标签，请升级浏览器
    </audio>
    <audio src="./videoAudio/nada.wav" controls muted>
        您的浏览器不支持audio标签，请升级浏览器
    </audio>
    <audio src="./videoAudio/ring.mp3" controls autoplay>
        您的浏览器不支持audio标签，请升级浏览器
    </audio>
```

src 路径，必须有

controls 音频控件，必须有

loop  循环播放

muted 静音

autoplay （IE）（火狐可设置）（其他用js）

# 六、video视频

ie8及以下不支持video、audio标签

```html
 <video src="./videoAudio/movie.mp4" controls width="500" loop muted poster="王祖贤.jpg">
     您的浏览器不支持video视频
</video>
```

src 路径，必须有

controls 音频控件，必须有

poster="王祖贤.jpg"   视频封面  （默认是视频的第一帧作为封面）

loop  循环播放

muted 静音

width 视频播放器的宽度。只写一个的话，另一个等比缩放

height视频播放器的高度

# 七、source

source 资源（代替audio 和video 来引入资源）

链接不同格式的音频文件，浏览器识别第一个可识别的格式的第一个音频

```html
<audio controls loop>
    <source src="./videoAudio/biubiubiu.ogg">
    <source src="./videoAudio/nada.wav">
    <source src="./videoAudio/ring.mp3">
    <source src="./videoAudio/hanmai.mp3">
    您的浏览器不支持，请升级浏览器
</audio>

<video controls>
    <source src="./videoAudio/butterfly.ogg">
    <source src="./videoAudio/movie.mp4">
    您的浏览器不支持，请升级浏览器
</video>
```

# 八、新增表单元素

### 新增input表单控件：

### 1、url网址

必须以 http://w（https://w）开头 移动端会自动弹出带有【http://】键盘

```html
<input type="url">
```

### 2、email 邮箱

 邮箱地址 必须由@连接前后内容，在移动端会弹出带有@ 的键盘

```html
<input type="email">
```

### 3、search 搜索

带【x】框，点击x 可取消框里的内容

```html
<input type="search">
```

### 4、tel 电话号码

移动端会弹出带#*的数字键盘

```html
<input type="tel">
```

### 5、number 数值输入框

只能输入数字，移动端会弹出数字键盘

max  最大值  只能提交限制范围的数字

min  最小值

step 步数

```html
<input type="number">
<input type="number" max="11" min="1" step="3">
```

### 6、range 滑动条

max  最大值  

min  最小值

step 步数

```html
<input type="range">
<input type="range" max="11" min="-3" step="5">
```

### 7、color 选色盘

value只能是16进制，且不能缩写

```html
<input type="color" value="#fff000">
```

### 8、date 日期选择器

​	年 月 日 

```html
<input type="date">
```

### 9、time 时间选择器 

​	时 分  

```html
<input type="time">
```

### 10、datetime 

 	手动输入一个UTC日期时间

```html
<input type="datetime">
```

### 11、datetime-local 日期和时间选择器

​	年月日时分

```html
<input type="datetime-local">
```

### 12、month 月份选择器

​	年和月 

```html
<input type="month">
```

### 13、week 周选择器

年和周 

```html
<input type="week">
```

### datalist 下拉列表：

和input配合使用，可输入内容的下拉列表

```html
<input type="text" list="url">
<datalist  id="url">  
    <option value="百度">http://www.baidu.com</option>
    <option value="新浪">https://www.sina.com</option>
    <option value="搜狐">https://www.souhu.com</option>
    <option value="腾讯">http://www.tencent.com</option>
</datalist>
```

# 九、新增表单属性

#### 1、max="5"  最大值  

#### 2、min="-2"  最小值

#### 3、step="3" 步数

#### 4、placeholder 

#### 5、autofocus 自动聚焦

#### 6、autocomplete 自动完成输入内容 on默认   off (必须有name)

#### 7、requeried   必填项，不能为空

#### 8、multiple   允许多个上传

#### 9、pattern   验证正则表达式

`/^1[3578][0-9]{9}/ `  以1开头，第二位数从35789里选择一个，从0-9里随意选9个数

```html
<input type="tel" pattern="^1[3578][0-9]{9}">
```

#### 10、list="datalistId"     将input和datalist绑定

#### 11、form  将form标签外的表单跟form关联起来

```html
<form  id="绑定的名字">
    <input type="text" name="x"/>
	<input type="submit">
</form>
<input type="text" name="user" form="绑定的名字">
<input type="submit" form="绑定的名字">
```

#### 

#### 























