# 五大浏览器

Chrome谷歌浏览器、Firefox火狐浏览器、Safari浏览器、Opera欧朋浏览器、Internet Explorer（IE浏览器）

# 浏览器内核

Chrome谷歌浏览器——》webkit——》blink（webkit的分支）

Firefox火狐浏览器——》gecko

Safari浏览器——》webkit

Opera欧朋浏览器——》presto——》webkit——》blink

Internet Explorer（IE浏览器）——》trident（IE内核）

# 其他浏览器

QQ   UC   360  猎豹  2345   搜狗

# 常用编辑器

vscode     webstorm    sublime

# vscode基本操作

下载插件（左侧边栏最后一个，搜索插件）

中文语言包：Chinese  （install 中文简体，重启vscode）

**添加文件夹：**

1、在工作区中点击添加文件夹，选择需要的文件夹，确定打开

2、文件——》打开文件夹——》选择文件夹

**新建文件：**

1、ctrl+n 新建文件——ctrl+s 保存文件——选择保存的位置——确定

2、在vscode工作区中，将文件夹点击成蓝色，然后点击新建文件按钮，写上名字

**在浏览器打开文档： **

1、在文档名处，右键——复制路径——在浏览器地址栏中搜索

2、open in browser插件 

​		 ——》open in default browser  用默认浏览器打开

​		——》open  in  other  browsers 用其他浏览器打开

​	open in default browser 插件  

​		——》在浏览器中打开  



# 前端语言 

html （Hyper Text Markup Language）超文本标记语言（结构）

css （cascading  style  sheets）层叠样式表，表现（样式）

js（javascript）脚本语言，（行为）

# html

用来描述网页的超文本标记语言（不是编程语言）

html是一个网页（.html）

html用标签来描述网页

# HTML语法

**闭合标签：**

<标签名> 内容 </标签名>

<标签名>  开始标签

</标签名> 结束标签

```html
<div> div里面的内容 </div>
```

**自闭标签：**

<标签名 />

```html
<img />
```

**属性：** 对标签的描述，标签的附加信息

属性名="属性值"（下载开始标签里，在开始标签名后面空个格）

```html
<div class="box" id="box"> div里面的内容 </div>
```

# HTML的基本结构

英文的 !+enter 

`  <!-- 注释 ctrl+/   注释里面的内容，不会影响页面结构，不会渲染到页面 -->`

```html
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    
</body>
</html>
```

```html
 <!-- 声明文档，告诉浏览器这个文档是什么类型的文档，让浏览器用相应的规范去解析文件，这个一行代码不是HTML标签 -->
<!-- 
        <html></html> 根元素
            <head></head> 放一些文档的元数据
                <title>文档标题</title>
                <meta>  设置元素信息
                    charset 字符集
                            UTF-8 万国码
                            GBK   国标码（简体和繁体）
                            gb2312  中文简体
                    keywords 关键字，用于搜索引擎优化
                    description 对网站的描述，用于搜索引擎优化
                style   写css样式
                link     引入css文件
                script  引入js文件
            <body></body> 写页面能看到的东西
-->
```

# h1-h6 标题标签

```html
<h1>一级标题</h1>
<h2>二级标题</h2>
<h3>三级标题</h3>
<h4>四级标题</h4>
<h5>五级标题</h5>
<h6>六级标题</h6>
```

```html
<!-- 
 h1 一级标题  整个页面最重要的地方，一般用于一个网站的logo，或者文章和章节的标题，建议一个页面只用一个h1

 h2-h6 根据标题在页面的重要性去合理的搭配使用

 所有的标题都是加粗加黑的，
-->
```

# p段落标签

```html
 <!-- 
        p段落标签，用于文章或文字表达的段落区域
-->
```

# br和hr

br 强制换行

hr一条线

# 文本格式化标签

```html
<!--
		 b  文字加粗
         strong   文字加粗，但是有语义化，有强调的意思
         i 文字倾斜
         em 文字倾斜 有语义化，有强调的意思
         sub  下标字
         sup 上标字
         del 删除标签 文字中间有一条横线
-->
```

# div 和span

```html
<!-- 
   div 表示一块区域 没有特殊语义，万能标签，div独占一行
   span 没有特殊意义，表示一个区域（内容多大就多大） 不独占一行      
-->
```

# img

```html
<img src="周杰伦.jpg" alt="周杰伦123" height="100px" width="100px">
<!-- 
        img 专属属性
        src="图片的地址（链接）"  路径+名字
        alt="当图片路径出现问题时的替换文本"
        width 写了宽但是没写高，则图片等比缩放
        height 写了高但是没写宽，则图片等比缩放  
-->
```

# 路径

```html
<!-- 
路径：
	相对(推荐使用)：
		./  当前路径(./可省略)
		../ 上一级路径
		../../ 上上级路径
	 	./images/林俊杰.jpg   相对当前路径
		../资料/汪峰.jpg
	绝对：
		/ 代表c盘或者根路径    /1.jpg   ==>https://bkimg.cdn.bcebos.com/1.jpg
		本机上的绝对路径(从盘符开始)
			C:\Users\IBM\Desktop\0824\0824day01\代码\周杰伦.jpg
		网络上的路径
			https://bkimg.cdn.bcebos.com/pic/b90e7bec54e736d1efcd0abe95504fc2d46269ae?x-bce-process=image/resize,m_lfit,h_452,limit_1

-->
```

# 回顾

#### web发展历程

web1.0  静态页面（电子版的报纸）

web2.0  有了专门的前端工程师

web3.0  互联网+

#### 前端语言

html 结构（超文本标记语言）

css   表现（层叠样式表）

js 行为（脚本语言）

#### html标签

h1-h6 标题 * * * * *

p 段落 * * * * *

div 表示一块区域，独占一行 * * * * *

span   表示一块区域，不独占一行的* * * * * 

img 图片标签* * * * *

br 强制换行

hr 一条线

**文本格式化标签：**

strong  文本加粗且有强调语义

b 仅文本加粗

em 文本倾斜且有强调语义

i 仅文本倾斜

sup  上标

sub 下标

del  删除线标签

#### 标签归类

**块元素:** 独占一行   h1-h6   p   div  br hr

**内联元素：** 不独占一行  span   strong   b  i   em  （不支持宽高）

**内联块元素：** 不独占一行  img  （支持宽高）

#### 5大浏览器 和4大内核

Chrome  Firefox   Safari  Opera  IE

webkit  blink  trident  gecko









































