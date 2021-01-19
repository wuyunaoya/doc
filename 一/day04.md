# 背景

background-color: red; 背景色

background-image: url(图片地址); 

background-repeat:图片是否平铺

​           						 repeat  默认平铺

​         						   repeat-x 沿着x轴平铺（仅水平方向平铺）

​        						    repeat-y 沿着y轴平铺（仅垂直方向平铺）

​     						       no-repeat 不平铺

background-position:水平方向的位置    垂直方向的位置; 

​            								  固定像素       固定像素

​             									 百分比       百分比  （图片的百分点位置和盒子的百分点位置重合）

​           										   left         top

​          										   right        bottom

​            										 center      center

【正值向右（下）负值向左（上）】 【只写一个值，默认是水平方向的值，另一个值是center】

background-attachment: fixed; 固定   背景图片会不会跟着页面滚动 

​             							    scroll 默认滚动

#### 综合写法：

background：color   image   repeat    position   attachment;  

# 复合选择器

##### 1、群组选择器（并集）

​      选择器1,选择器2,选择器3,...,选择器n{ }

```css
 		div , #op , .ospan{
            font-size: 20px;
            color: red;
        }
```

##### 2、交集选择器

​      选择器1选择器2{ }

```css
		p.opp#op{
            background-color: blue;
        }	
```

##### 3、后代选择器

​      祖辈元素的选择器 后代元素的选择器{ }

```css
		 div div{
            font-size: 100px;
        }
```

##### 4、子选择器

​      父元素的选择器>子元素的选择器{ }

```css
		div>div{
            width: 200px;
            height: 200px;
            background-color: pink;
        }
```

##### 5、伪类选择器：

   a:link 链接访问之前的初始状态

   a:visited 链接访问过后的状态

   a:hover 划上（鼠标停留在元素上）这个元素时的状态

   a:active 点击元素的这一刻的状态

# css三大特性

### 层叠性

层叠：同一个元素具有多个相同样式的时候，后写的会覆盖先写的（就近原则）

### 继承性

 继承性（一些样式可以被后代元素继承）

  color 字体颜色

  font-size 字号

  font-style: 是否倾斜

  font-weight: 是否加粗

  font-family: 字体

  line-height: 行高

  text-align: 水平对齐方式

  text-indent: 首行缩进

### 优先级

  1、行内样式>内部样式和外部样式（内部样式和外部样式按选择器权值计算，同级覆盖）    

  2、权重

`#idName>.className>tagName>*`

  **权值**（ 复合选择器的权重由基础选择器的权值相加）

| 选择器 | #idName | .className | tagName> |  *   |
| :----: | :-----: | :--------: | :------: | :--: |
|  权值  |   100   |     10     |    1     |  0   |

  3、权重相同，同级覆盖（就近原则）

  4、!important 权重最高

**总结：**!important > 行内样式 >内部样式和外部样式（#idName>.className>tagName>*，同级覆盖）> 默认样式

# 元素的分类和转化

####  块元素

​     1、display:block

​     2、独占一行

​     3、宽度默认是父元素的100%，高度默认由内容撑起来

​     4、支持width和height

​     5、支持padding

​     6、支持border

​     7、支持margin（但是会有margin塌陷问题）

​     8、支持行高line-height

​     9、div h1-h6 p ul ol dl

####    内联元素

​     1、display:inline;

​     2、不独占一行

​     3、宽度默认由内容撑起来，高度默认由内容撑起来

​     4、不支持width和height

​     5、支持左右的padding，上下padding不支持（不占位但是可以显示背景颜色）

​     6、支持左右的border，上下border不支持（边框不占位但是可以显示）

​     7、支持左右的margin，上下margin不支持

​     8、不支持行高line-height（不会把背景颜色撑起来，但是占位）

​     9、span b strong i  em

####    内联块元素

​     1、display:inline-block;

​     2、不独占一行

​     3、宽度默认由内容撑起来，高度默认由内容撑起来

​     4、支持width和height

​     5、支持padding

​     6、支持border

​     7、支持margin

​     8、支持行高line-height

​     9、会有基线问题

​     10、img input

### 元素转换：

  其他类型的元素转块元素：display:block

  其他类型的元素转内联元素：display:inline

  其他类型的元素转内联块元素：display:inline-block







