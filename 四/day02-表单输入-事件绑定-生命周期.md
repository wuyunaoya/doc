# 一.双for

```html
 <div id="app">
        <ul>
            <li v-for="(item,index) in movies">
                <h3>电影:{{item.name}}</h3>
                <div>导演:{{item.direc}}</div>
                <div>主演:
                    <span v-for="i in item.act">{{i}}&nbsp;&nbsp;</span>
                </div>
                <div>类型:
                    <span v-for="i in item.type">{{i}}&nbsp;&nbsp;</span>

                </div>
            </li>
        </ul>
    </div>
    <script>
        new Vue({
            el:'#app',
            data:{
                movies:[
                    {
                        name:'28岁未成年',
                        direc:'张末',
                        act:['倪妮','霍建华','马苏'],
                        type:['喜剧','爱情','奇幻']
                    },
                    {
                        name:'乘风破浪',
                        dicet:'韩寒',
                        act:['邓超','彭于晏','赵丽颖'],
                        type:['喜剧','剧情']
                    },
                    {
                        name:'我不是药神',
                        dicet:'文牧野',
                        act:['徐峥','王传君','周一围'],
                        type:['喜剧','剧情']
                    },
                    {
                        name:'西虹市首富',
                        dicet:'闫非',
                        act:['沈腾','宋芸桦','张一鸣'],
                        type:['喜剧']
                    }
                ]
            },
            methods:{},
        })
    </script>
```



# 二.key

使用key做真实DOM和虚拟DOM的中间键,进行对比,将产生差异的进行渲染,相同的不做修改.

```html
 <div id="app">
        <ul>
            <li v-for="(item,index) in stars" :key="item.id">
                <span>{{item.name}}</span>
                <button @click="del(index)">删除</button>
            </li>
        </ul>
    </div>
    <script>
        new Vue({
            el:'#app',
            data:{
                stars:[
                    {
                        id:1,
                        name:'张杰',
                    },
                    {
                        id:2,
                        name:'张靓颖',
                    },
                    {
                        id:3,
                        name:'邓紫棋',
                    },
                    {
                        id:4,
                        name:'王源',
                    }
                ]
            },
            methods:{
                del(i){
                    this.stars.splice(i,1);
                }
            },
        })
    </script>
```



# 三.表单输入

## 1.v-model

```
1.输入框:v-model的值就是输入框的value值
2.单选按钮:1.若没有value,提交的数据显示为null 
          2.data中sex的值就是选中之后对应的value值
          3.若初始值为对应的value值,则该选项默认选中
3.复选框:1.如没有value,提交的数据显示为null
        2.没有选中任何值,提交的数据显示为空数组
        3.如果选中值,提交的数据你选中的数据的array
4.下拉框: 1.数据data的值是和select进行绑定
         2.select的值option中的value
         3.禁止选中disabled
         4,多选,增加multiple属性
5.textarea:文本域  v-model做双向数据绑定
6.复选框:没有value值,默认是显示true和false
```

```html
案例:
 <!-- 
    约束后端的api接口
    1.用户名:username eg:'小王'
    2.密码: password   eg:....
    3.性别:sex  eg:1   说明:0-男   1-女  2-人妖
    4.爱好:hobby eg:['rap','coding','playing']  说明:rap-唱跳  coding-写代码  playing-打王者荣耀
    5.course:'web'  说明:web-web工程师  java-java工程师  PHP-PHP工程师
    6.吃的:eat eg:['reganmian','choudoufu']  说明:reganmian-热干面  choudoufu-臭豆腐
    7.说明:desc  eg:'我请大家吃烤鸭'
    8.我同意:isAgreen  eg:true    说明:true-同意  false-不同意
     -->
    <div id="app">
        <h2>注册用户</h2>
        <!-- v-model可做输入框数据双向绑定:v-model的值就是输入框的value值 -->
        <div>用户名:
            <input type="text" v-model="user.username">
        </div>
        <div>密码:
            <input type="password" v-model="user.password">
        </div>
        <div>确认密码:
            <input type="password" v-model="rpassword">
        </div>
        <!-- 
            单选按钮:1.若没有value,提交的数据显示为null 
                    2.data中sex的值就是选中之后对应的value值
                    3.若初始值为对应的value值,则该选项默认选中
         -->
        <div>性别:
            <input type="radio" v-model="user.sex" value="0">男
            <input type="radio" v-model="user.sex" value="1">女
        </div>
        <!-- 复选框:1.如没有value,提交的数据显示为null
                    2.没有选中任何值,提交的数据显示为空数组
                    3.如果选中值,提交的数据你选中的数据的array
        -->
        <div>爱好:
            <input type="checkbox" v-model="user.hobby" value="rap">唱跳rap
            <input type="checkbox" v-model="user.hobby" value="coding">写代码
            <input type="checkbox" v-model="user.hobby" value="playing">打王者荣耀
        </div>
        <!-- 
            下拉框: 1.数据data的值是和select进行绑定
                    2.select的值option中的value
                    3.禁止选中disabled

         -->
        <div>科目:
            <select v-model="user.course">
                <option value="" disabled>--请选择--</option>
                <option value="web">web工程师</option>
                <option value="java">java工程师</option>
                <option value="php">php工程师</option>
            </select>

        </div>
        <!-- 4,多选,增加multiple属性 -->
        <div>吃的:
            <select v-model="user.eat" multiple>
                <option value="" disabled>--请选择--</option>
                <option value="reganmian">热干面</option>
                <option value="choudoufu">臭豆腐</option>
                <option value="kaoya">烤鸭</option>
            </select>
        </div>
        <div>说明:
            <textarea v-model="user.desc" cols="30" rows="10"></textarea>
        </div>
        <div>
            <input type="checkbox" v-model="user.isAgreen">我同意
        </div>
        <div>
            <button @click="reg()" :disabled="!user.isAgreen">欢迎注册</button>
        </div>
    </div>
    <script>
        new Vue({
            el:'#app',
            data:{
                rpassword:'',
                user:{
                    username:'',
                    password:'',
                    sex:0,
                    hobby:['playing'],
                    course:'',
                    eat:[],
                    desc:'',
                    isAgreen:false
                }
            },
            methods:{
                reg(){
                    if(this.user.password !== this.rpassword){
                        alert('两次输入密码不一致');
                        return;
                    }
                    console.log(this.user);
                }
            },
        })
    </script>
```



## 2.表单修饰符

.lazy  .trim  .number

```html
 <!-- .lazy:失去光标的触发事件 -->
 <!-- <input type="text" v-model.lazy="user.username"> -->
 <!-- .number 将输入框中的值转为number类型
 实例开发:手机号  price 
 -->
 <!-- <input type="text" v-model.number="user.username"> -->
 <!-- .trim 将输入框中值得两边的空格去除 -->
 <input type="text" v-model.trim="user.username">
```



# 二.事件绑定

## 1.绑定事件

```
1.绑定事件
2.参数传递: 无参数 有参数
		方法调用时:不写(),表示无参数传递
		方法调用时:写(),表示有参数传递
		总结:vue中方法调用,()可写可不写
3.获取event对象
		方法调用时:没有传递$event参数,可直接获取event对象
		方法调用时:有传递$event参数,也可直接获取event对象
4.阻止默认事件
		@contextmenu(右键菜单)
		 e.preventDefault();
5.阻止事件传播
		 e.stopPropagation();
```

```html
<!-- 1.绑定事件v-on  简写为:@ -->
<button v-on:click="add()">点我</button>
<button @click="add()">点我</button>
```

```html
获取event 对象
        <!-- 3.事件绑定event -->
        <div>
            <!-- 方式一: 在函数调用时需要传递一个$event来接收event对象 -->
            <button @click="eventButton($event)">eventButton</button>
        </div>
        <div>
            <!-- 方式二:函数调用,不需要加(),同样也可以获取到event对象 -->
            <button @click="eventButton1">eventButton1</button>
        </div>
        
     eventButton(e){
     console.log(e);
     },
     eventButton1(e){
     console.log(e);
     }
```

```html
 <div>
 <!--阻止默认事件 -->
 <div class="box" @contextmenu="menu"></div>
 </div>

<div>
<!-- 阻止事件传播 -->
<div class="outer" @click="outer">
<div class="inner" @click="inner">

</div>
</div>
</div>

js部分
 menu(e){
 e.preventDefault();
 console.log('右键了');
 },
 outer(){
 console.log('outer outer');
 },
 inner(e){
 e.stopPropagation();
 console.log('inner inner');
 }
```



## 2.修饰符

```
1.阻止默认事件   .prevent  阻止默认事件修饰
2.阻止事件传播
3,阻止事件传播,是自己才触发
4.up down left right enter 13
5.捕获:由外向内进行捕获
```

```html
<div id="app">
        <!-- 阻止默认事件 .prevent -->
        <button @contextmenu.prevent="yj">点我</button>
        <textarea @keydown.enter.prevent="enter" id="" cols="30" rows="10"></textarea>

        <!-- 阻止事件传播 -->
        <div class="outer" @click="outer">
            <div class="inner" @click.stop="inner">

            </div>
        </div>



        <!-- 阻止事件案例 -->
        <button @click="isShow=true">删除</button>
        <div class="main" v-if="isShow" @click.self="isShow=false">
            <div class="con">
                <h3>确定要删除吗?</h3>
                <div>
                    <button @click="isShow=false">取消</button>
                    <button @click="confirm">确定</button>
                </div>
            </div>
        </div>


        <!-- 键盘事件 -->
        <input type="text" @keydown.up="up" @keydown.down="down" @keydown.left="left" @keydown.right="right" @keydown.13="enter" >


        <!-- 捕获 -->
        <div class="outer" @click.capture="outer">
            <div class="inner" @click="inner"></div>
        </div>
    </div>
    <script>
        new Vue({
            el:'#app',
            data:{
                isShow:false
            },
            methods:{
                yj(){
                    console.log('右键了');
                },
                enter(){
                    console.log('回车了');
                },
                outer(){
                    console.log('outer');
                },
                inner(){
                    console.log('inner');
                },
                confirm(){
                    this.isShow = false
                },
                up(){
                    console.log('上键了');
                },
                down(){
                    console.log('下键了');
                },
                left(){
                    console.log('左键了');
                },
                right(){
                    console.log('右键了');
                },
                enter(){
                    console.log('回车了');
                },
                
            },
        })
    </script>
```

总结:

```
1.v-on:   简写@   都可做事件绑定
2.只要是有事件绑定.必然有事件源 event,   注意:传递实际参数时,清您使用$event
3.阻止默认事件  e.preventDefault()   .prevent
3.阻止事件传播  e.stopPropagation    .stop
4..self(自我触发)  @keydown.up  @keydown.down @keydown.left @keydown.right @keydown.enter @keydown.13(键盘事件kedown)
5..capture():目的是由外向内进行捕获
```

# 三.生命周期

## 1.定义:

vue对象从出生到销毁的过程

## 2.钩子函数

某事某刻,自动触发

```
 1.beforeCreate创建之前:什么是undefined
 2.created创建完成:属性和方法已经OK了,但是el还是undefined
 3.beforeMount挂载之前:找到挂载点,但是还没有渲染页面
 4.mounted挂载完成:找到挂载点,且页面渲染完毕,这是就开启你的轮播图  计时器, 发送ajax等等
 5.beforeUpdate更新之前:数据已经发生改变,指的是页面渲染之前
 6.updated更新完成:数据已经发生改变,指的是页面渲染完成
 7.beforeDestroy销毁之前,清定时器
 8.destroyed销毁完成
```

# 四.$set

```html
要给对象或者数组(数组中有对象)添加新的属性,需要通过$set去设置
两种方式新增属性
局部:this.$set(数据,新的属性名,新的属性值)
全部:vm.$set(数据,新的属性名,新的属性值)
<div id="app">
        <div> 姓名: {{people.name}}  </div>
        <div> 年龄: {{people.age}}  </div>
        <div> 性别: {{people.sex}}  </div>
    </div>
    <script>
        var vm= new Vue({
            el:'#app',
            data:{
                people:{
                    name:'王俊凯',
                    age:20
                }
            },
            methods:{},
            mounted(){
                console.log(this.people);
                // this.people.sex = '男';
                // 局部设置
                this.$set(this.people,'sex','男');
            }
        })

        // 全局设置
        // vm.$set(vm.people,'sex','女');
    </script>
```



# 五.面试题

```
常用的事件修饰符都有哪些？分别说明它们的作用。
什么是Vue的生命周期？
	Vue生命周期是指vue实例对象从创建之初到销毁的过程，vue所有功能的实现都是围绕其生命周期进行的，在生命周		期的不同阶段调用对应的钩子函数可以实现组件数据管理和DOM渲染两大重要功能
解析Vue生命周期中各个钩子函数分别在什么场景下执行。
```

# 六作业

1.home

2.home1

3.案例敲1遍