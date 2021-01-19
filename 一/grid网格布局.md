# Grid网格布局

网格布局是最强大的css布局方案，将网页划分成一个一个的网格，可以任意组合出不同的网格，做出各种各样的布局。网格布局将容器划分成"行"和"列"，然后指定"项目所在"的单元格，可看做是2维布局

### 1、基本概念

##### 采用网格布局的区域交"容器"，容器内部采用网格定位的子元素叫项目"项目"

```html
<容器>
    <项目>项目里面的东西</项目>
    <项目>项目里面的东西</项目>
    <项目>项目里面的东西</项目>
</容器>
```

##### 行和列

容器里的水平区域称为行（row）,垂直区域称为列（column）

##### 单元格

行和列的交叉区域，称为单元格

##### 网格线

划分网格的线叫网格线，水平网格线划分出行，垂直网格线划分出列

n行有n+1跟水平网线，m列有m+1跟垂直网线

### 2、容器属性

- #### display:grid（inline-grid）  

项目的float、display: inline-block、display: table-cell、vertical-align和column-*等设置都将失效

- #### grid-template-rows行高，grid-template-columns列宽

  - ##### repeat(重复次数,重复的值)
  
  ```css
  .wrap{
      display: grid;
      /*grid-template-columns: 500px 500px 500px;
      grid-template-rows: 300px 300px 300px;*/
      grid-template-columns: repeat(1,100px) repeat(2,200px) repeat(3,300px);
      grid-template-rows: repeat(1,100px) repeat(2,200px) repeat(3,300px);
   	/* grid-template-rows: repeat(2,100px 200px 300px);*/
  }
  ```
  
  - ##### fr比例
  
  ```css
  wrap{
      display: grid;
      /*要使用行高比例，父元素必须有高*/
      height:1000px;
      grid-template-columns: repeat(1,1fr) repeat(2,2fr) repeat(3,3fr);
      grid-template-rows: repeat(1,1fr) repeat(2,2fr) repeat(3,3fr);
  }
  ```
  
    - ##### minmax(最小值,最大值)
  
  ```css
  wrap{
      display: grid;
     /*grid-template-columns: minmax(100px,200px) minmax(200px,300px) minmax(300px,400px);
       grid-template-rows: minmax(100px,200px) minmax(200px,300px) minmax(300px,400px);*/
       grid-template-columns: repeat(1,minmax(100px,200px)) repeat(2,minmax(200px,300px)) repeat(3,minmax(300px,400px));
              grid-template-rows: repeat(1,minmax(100px,200px)) repeat(2,minmax(200px,300px)) repeat(3,minmax(300px,400px));
  }
  ```
  
  - ##### auto  关键字
  
    由浏览器自己决定长度
  
  ```css
   .wrap {
       display: grid;
        /*要使用行高auto，父元素必须有高*/
       height: 3000px;
       grid-template-columns:100px auto auto auto 200px;
       grid-template-rows: 100px auto  auto auto 100px;
       /*auto-fill  浏览器自己计算次数
       grid-template-columns: repeat(1,50px) repeat(auto-fill,200px) repeat(1,50px);
       grid-template-rows: repeat(1,100px) repeat(2,200px) repeat(3,300px); 
       */
  }
  ```
  
  - ##### auto-fill
  
    ​	浏览器自己计算次数
  
  - ##### 还可以给网格线的起名称
  
  ```css
  .wrap{
      display:grid;
      grid-template-columns:[线名1 线名2] 100px [线名] 100px [线名] 100px [线名] ;
      grid-template-rows:[线名] 100px [线名] 100px [r3] 100px [线名] ;
  }
  ```
  
- ####  grid-row-gap 行间距，grid-column-gap 列间距

grid-row-gap行与行的间隔

grid-column-gap 列与列的间隔

```css
.wrap{
    display: grid;
     /*grid-row-gap: 10px;
     grid-column-gap: 10px;
   	 grid-gap: 10px 20px;*/
     row-gap: 10px;
     column-gap: 20px; 
     gap:10px 20px;
}
```

- #### grid-template-areas，grid-area  网格区域

```css
 html,body,.wrap{
     height: 100%;
     margin: 0;
}
.wrap {
    display: grid;
    grid-template-columns: repeat(5,1fr);
    grid-template-rows: repeat(6,1fr);
    grid-template-areas:
        "header header header header header"
        "nav nav nav nav nav"
        "article article article aside aside"
        "article article article aside aside"
        "article article article aside aside"
        "footer footer footer footer footer"
        ;
}
header {
    grid-area: header;
    background-color: red;
}
nav {
    grid-area: nav;
    background-color: pink;
}
article {
    grid-area: article;
    background-color: blue;
}
aside {
    grid-area: aside;
    background-color: green;
}
footer {
    grid-area: footer;
    background-color: gray;
}
```

```html
 <div class="wrap">
     <header>header</header>
     <nav>nav</nav>
     <article>
         article
         <section>section</section>
     </article>
     <aside>aside</aside>
     <footer>footer</footer>
</div>
```

- #### grid-auto-flow 项目排列方向

```css
.wrap {
    display: grid;
    grid-template-columns:200px 200px 200px;
    grid-template-rows: 200px 200px 200px;
    gap:10px 20px;
    grid-auto-flow: row;/*先行后列 默认*/
    grid-auto-flow:column;/*先列后行*/

}
```

- #### justify-items:  项目(子元素)在单元格中的水平位置

（1）start：对齐单元格的起始边缘。

（2）end：对齐单元格的结束边缘。

（3）center：单元格内部居中。

（4）stretch：拉伸，占满单元格的整个宽度

```css
 .wrap {
     display: grid;
     grid-template-columns:200px 200px 200px;
     grid-template-rows: 200px 200px 200px;
     gap:10px 20px;
     justify-items: start;
     justify-items: end;
     justify-items:center;
     justify-items:stretch; 
}      
```

![justify-items](笔记图片/justify-items.png)

- #### align-items: 项目(子元素)在单元格中的垂直位置

（1）start：对齐单元格的起始边缘。

（2）end：对齐单元格的结束边缘。

（3）center：单元格内部居中。

（4）stretch：拉伸，占满单元格的整个高度

```css
 .wrap {
     display: grid;
     grid-template-columns:200px 200px 200px;
     grid-template-rows: 200px 200px 200px;
     gap:10px 20px;
     align-items:start ;
     align-items:end ;
     align-items:center ;
     align-items:stretch ;
}     
```

![justify-items](笔记图片/align-items.png)

- #### place-items: align-items justify-items;

- #### justify-content  每一列在容器（父元素）里面的水平排列方式

![justify-items](笔记图片/justify-content.png)

- #### align-content 每一行在容器（父元素）里面的垂直排列方式

![justify-items](笔记图片/align-content.png)

- #### place-content:  align-content   justify-content;

### 3、项目属性

- #### grid-column-start，grid-column-end，grid-row-start，grid-row-end 

  这个项目四个边框定位到哪个网格线上，网格线分别以1234......表示（也可以自己起名字）

  grid-column-start: n  左边框所在的垂直网格线。

  grid-column-end: n  右边框所在的垂直网格线。

  grid-row-start: n  上边框所在的水平网格线。

  grid-row-end: n  下边框所在的水平网格线。

  grid-column-end: span   n  跨几列，所占网格数量

  grid-row-end: span n  跨几行

![grid-row和grid-column](笔记图片\grid-row和grid-column.png)

- #### grid-column，grid-row

  grid-column :  grid-column-start / grid-column-end

  grid-row :  grid-row-star / grid-row-end

- #### grid-area 项目放在哪一个区域，配合grid-template-areas

- #### align-self，justify-self，place-self  子元素在单元格的水平和垂直位置

  跟父元素的：align-items，justify-items，place-items 一模一样，只是加给项目















