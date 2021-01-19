# a链接

`<a href="地址链接" target="跳转的目标"></a> `

  href="地址链接" 

  target="跳转的目标" 默认是_self 在本窗口打开链接  _blank在新窗口打开

```html
	<a href="http:///www.baidu.com">百度</a>
    <a href="http:///www.jd.com" target="_blank">京东</a>
    <a href="http:///www.taobao.com" target="_self">淘宝</a>
```

**默认状态：**

​		有下划线

- 初始状态（链接未被访问过的时候）默认样式为 字体蓝色
- 当鼠标划上时，鼠标变小手
- 当鼠标点击的时候（正在访问的时候），字体变红色
- 当链接访问过的时候，字体变紫色

# 列表

### 无序列表

- 1
- 2
- 3

```html
<!--
        无序列表 ul>li 配合使用（ul的子元素只能是li） 
        type="disc" 默认是 实心圆
             circle 空心圆
             suqare 实心小方块
-->
<ul type="类型">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
</ul>
```

### 有序列表

1. 1
2. 2
3. 3

```html
<!-- 
        有序列表 ol>li 配合使用（ol的子元素只能是li） 
        type="1" 数字
              a  小写字母
              A  大写字母
              i  小写罗马数字
              I  大写罗马数字
-->
 <ol type="类型">
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
  </ol>
```

### 定义列表

```html
 <!--
         定义列表 dl>dt dd 配合使用（dl是父元素，dt和dd兄弟关系，dd是dt的一个解释说明） 
 -->
<dl>
        <dt>水果</dt>
        <dd>苹果</dd>
        <dd>香蕉</dd>
        <dd>梨</dd>
        <dd>桃子</dd>
</dl>
```

# 锚点链接

跳转到本页面的某个地方

  ```html
<a href="#id名">跳转到水果</a>
<dl>
        <dt id="id名">水果</dt>
        <dd>苹果</dd>
        <dd>香蕉</dd>
        <dd>梨</dd>
        <dd>桃子</dd>
</dl>
  ```

跳转到其他页面的某个地方

```html
<a href="路径#id名">跳转到水果</a>
```

# 表格

### 表格标签

 table 表格

  tr 行

  th 表头单元格 默认加粗加黑,文字水平居中，垂直居中

  td 数据单元格，默认文字水平居左，垂直居中

  caption  表格的标题

  tbody和thead、tfoot 

```html

 <table border="1" width="700px" height="500px">
        <caption>课程表</caption>
        <thead>
            <tr>
                <th>星期一</th>
                <th>星期二</th>
                <th>星期三</th>
                <th>星期四</th>
                <th>星期五</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>数学</td>
                <td>语文</td>
                <td>英语</td>
                <td>物理</td>
                <td>历史</td>
            </tr>
        </tbody>
        <tfoot>
            <tr>
                <td>晚自习</td>
                <td>晚自习</td>
                <td>晚自习</td>
                <td>晚自习</td>
                <td>晚自习</td>
            </tr>
        </tfoot>
    </table>
```

### 表格的属性

-  **border**="1" 边框（只能加给table）
-   **width**  (加给tr不生效)每一列的宽度都相等，宽度由这一列最宽的单元格决定，最宽的这个单元格的宽度默认由内容撑开
-   **heigh**  每一行的高度都相等，高度由这一行最高的单元格决定，最高的这个单元格的高度默认由内容撑开 
-   **bgColor**="yellow" 背景颜色
-   **align** 默认left center right (加给table时，是整个表格在页面的水平位置)（加给tr和td时，是单元格里面的内容在单元格里的水平位置）
-   **valign** 默认middle  top bottom （只能加给tr和td，是单元格里面的内容在单元格里的垂直位置）
-   **cellpadding**="0px" 单元格个单元格里面的内容之间的缝隙
-   **cellspacing**="0px" 单元格和单元格之间的距离
-   **rowspan**="数字" 跨行合并
-   **colspan**="数字" 跨列合并

### 表格的样式

-   **border-collapse**: separate;默认不合并  collapse;合并成一条线
-   **border-spacing**（跟cellspacing一样的效果）

### tbody和thead、tfoot 有什么作用？

thead和tbody、tfoot结合使用，让表格更完整，规定着表格的各个部分（表头，主体，页脚）

thead表示表格的头部

tbody表示表格的主体

tfoot表示表格的页脚

thead和tbody、tfoot 默认不会影响表格的布局

# 谈谈你对标签语义化的理解？

#### 标签语义化：

用合适的标签和它特有的属性去做合适的布局，例如：标题用h1-h6，段落用p，img标签要加alt属性

#### 语义化的好处：

- 在没有css的情况下，也很能很好的去显示页面
- 增加了代码的可读性，有利于团队合作
- 有利于用户体验（alt，title）
- 有利于seo（和搜索引擎建立良好的沟通，有利于爬虫去抓取更有效的信息，标签的使用和上下文的联系影响爬虫对信息的抓取）

# css 基本知识

css 层叠样式表 （装饰HTML，标签的颜色、大小、形状、位置等布局） 表现

注释：`/* 注释 ctrl+/ */`

#  css的三种引入方式和语法

#### 1、内联引入（行内引入） 

在开始标签名的后面添加一个style属性，样式就是style属性的属性值

 <标签名  style="样式名1:样式值1;样式名2:样式值2;......."></标签名>

```html
<div style="width: 100px;height: 100px;background-color: red;"></div>
```

#### 2、内部引入（内嵌引入） 

在head标签里面，title标签下面，添加一个style标签

​      选择器{

​        		样式名1:样式值1;样式名2:样式值2;.......

​      }

```html
<div></div>
```

```css
div {
       width: 100px;
       height: 100px;
       background-color: red;
}
```

####   3、外部引入（外链引入）

新建一个css文件，style标签里面怎么写，css文件里面就怎么写

在head标签里面，title标签下面，用link标签引入css文件：

`<link rel="stylesheet" href="css文件的地址">`

​      rel="stylesheet" 引入文件的类型

​      href="css文件的链接"

**例如：**

**html文件里**

```html
<p></p>
```

在head标签里面，title标签下面

```html
<link rel="stylesheet" href="./1.css">
```

**1.css文件里**

```css
  /* 外部css样式 */
p {
    width: 100px;
    height: 100px;
    background-color: green;
}
```

























