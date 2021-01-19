# form表单：为了收集用户信息

form 表单区域

​    	action="提交的地址"

   	 method="提交的方式"   GET默认   POST

​        			1、GET提交方式，数据会在地址栏中显示  index.html?userName="张三"

​        				 	 POST会提交到form的数据体

​     			   2、GET没有POST安全，因为数据会在地址栏中显示

​    			    3、GET 2KB  POST 没有限制

​     			   4、POST一般用于用户向服务器发送信息，GET一般用于服务器向用户反馈信息

```html
<form action="https://www.baidu.com" method="POST">
       
</form>
```

#  表单元素：

### input

`<input type="表单控件"> `

​              text 文本输入框

​              password 密码框

​              checkbox 复选框（多选框）

​              radio   单选框（同组的选项，必须有name属性，并且name值相等）

​              submit  提交

​              reset   重置

​              button  普通按钮，一般用于js操作

​              file   上传文件

​              image   图片提交按钮（必须有src来引入图片）

​              hidden  隐藏域(用于向后台提价数据，但是页面中又不需要显示内容)

###  select     

​			  selected默认选中（用于下拉框）

      ```html
 <select>
        <option>请选择</option>
        <option selected >武汉</option>
        <option>黄冈</option>
        <option>赤壁</option>
 </select>
      ```

### textarea

textarea表单区域

 		 cols="30" textarea的列数

​		  rows="10" textarea的行数

用于textarea的css样式（属于用户界面）

​		  resize: both; 默认值，用户可以随意改变大小 

​		  resize: none; 禁止用户改变大小 

​		  resize:vertical; 用户只可以改变垂直方向的大小 

​		  resize:horizontal; /*用户只可以改变水平方向的大小

```html
<textarea cols="30" rows="10"></textarea>
```

# 表单属性

**action="提交的地址"**

   		 method="提交的方式"   GET默认   POST

​        			1、GET提交方式，数据会在地址栏中显示  index.html?userName="张三"

​        				 	 POST会提交到form的数据体

​     			   2、GET没有POST安全，因为数据会在地址栏中显示

​    			    3、GET 2KB  POST 没有限制

​     			   4、POST一般用于用户向服务器发送信息，GET一般用于服务器向用户反馈信息

  **type**  表单控件（表示表单的类型）

  **name**  向后提交数据，必须给元素起个名

  **value**  input的默认值 （用户输入的就是value）

  **placeholder**  占位符（一般用于提示）

  **maxlength**  用户可输入的最大长度

  **checked**  默认选中（用于单复选框）

  **selected**  默认选中（用于下拉框）

  **readonly**  只读

  **disabled**  禁用

  **cols**="30"  textarea的列数

  **rows**="10"  textarea的行数

 **outline**  表单点击时（获取焦点时）的外框  outline: none;去掉点击单表时的外框



  用于textarea的css样式（属于用户界面）

  resize: both; 默认值，用户可以随意改变大小 

  **resize: none;** 禁止用户改变大小 

  resize:vertical; 用户只可以改变垂直方向的大小 

  resize:horizontal; /*用户只可以改变水平方向的大小



  