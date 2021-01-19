### 一 :模块

一个js文件就是一个模块.

##### (1):node自带的核心模块:

let fs = require("fs")

##### (2):自定义模块

一个js文件就是一个模块,模块里面定义的属性或者方法都是私有的，外部文件想要去访问定义属性和方法，

那么这个模块文件就得暴露这个属性和方法，外部文件才可以加载该模块使用。

暴露模块:遵守CommonJs规范:

exports.属性名 = 属性值

module.exports.属性名 = 属性值



外部文件加载暴露模块:

let m = reqtuire("./模块名")

注意：加载核心模块，不能有路径./  ../，而加载自定义模块必须要有./ ../路径地址，这是为了和核心模块区分开来.



##### (3):加载第三方模块

第一步：初始化项目包(你是在哪个项目跟目录下使用，就在哪个项目根目录下面去初始化)

注意：你在哪个目录下下载包，就在哪个目录结构下初始化以及下载相关的包

格式1:(最外层的目录名可以是中文状态)

npm init 

格式2：(推荐使用)(外部项目目录名一定是一个英文名字,不能是中文的)

npm init -y

第二步：下载相关的包

npm i time-stamp

第三步:加载相关包

let timeStamp = require("time-stamp");

npm cache clean -f :清除下载包缓存内容

下载时：报错

request to https://registry.npm.taobao.org/time-stamp

这是网络问题导致



### 二:Buffer模块

Buffer模块:内置模块，这个模块不需要加载.

Buffer模块作用: 默认使用在fs模块文件读取和写入中，模块可以转换字符串生成base64加密方式，

通常这个方式用在注册和登录的时候给用户进行秘钥加密.

Buffer模块:他是二进制的内容存储，以16进制读取.

##### (1):Buffer模块转换字符串:

格式1：

```js
let buf = Buffer.from("abcd");

buf.toString();
```

Buffer中汉子占用3个字节.字符串中汉子占用2个字节.

格式2：

```js
let buf = Buffer.alloc(10); //存储10个字节大写内容

buf.write("abcd");

console.log(buf.toString());
```

##### (2):转换为对象

```js
let buf = Buffer.from(JSON.stringify({name:"李四"}));
console.log(JSON.parse(buf.toString()));
```

##### (3):合并

```js
let buf1 = Buffer.from("abcd");
let buf2 = Buffer.from("1234");
let allbuf = Buffer.concat([buf1,buf2])
```

##### (4):可以存储一个base64加密字符串(重点)

```js
const buf = Buffer.from('admin', 'utf8');
//console.log(buf.toString('hex'));
// 打印: 68656c6c6f20776f726c64
console.log(buf.toString('base64'));
```



### 二：fs模块

fs模块:对文件读取和写入操作

##### 写入格式:

###### (1):写入格式1:

  第一个参数:打开文件路径地址(这个文件如果不存在，则自动创建)

  第二个参数:以什么方式写入

  r:只读

 w:覆盖写入

 a:追加写入

```js
let fd = fs.openSync(__dirname+"/1.txt","w");
fs.writeSync(fd,"asfdsfdsf","utf8");
```

###### (2):写入格式2

 第一个参数:打开文件路径地址(这个文件如果不存在，则自动创建)

第二个参数:以什么方式写入

  r:只读

 w:覆盖写入

 a:追加写入

第三个参数:回调函数(err,fd)

err:返回的是目录地址是否正确

fd:打开文件

```js
fs.open(__dirname+"/2.txt","a",(err,fd)=>{
    if(err)
    {
    console.log("你读取目录文件有问题")
    }else
    {
       fs.write(fd,"写入格式2",(err)=>{
           if(err)
           {
             console.log("写入失败")  
           }else
           {
             console.log("写入成功")
           }
       }) 
    }
})
```



###### (3):写入格式3

 第一个参数:写入目录地址

 第二参数：写入内容

 第三个参数:以什么方式写入

 r:只读

 w:覆盖写入

 a:追加写入

 {flag:"a",encodeing:"utf8"}

第四个参数:(err)

err:写入成功还是失败

```js
fs.writeFile(__dirname+"/写入文件/3.txt","格式3",{flag:"a",encodeing:"utf8"},(err)=>{
  if(err)
  {
    console.log("写入失败")
  }else
  {
    console.log("写入成功")
  }
})
```



###### (4):第4个格式写入(写入多个内容数据)

 第一个参数:读取指定的一个目录地址,该目录不存在，则自动创建.

 第二个参数:以什么方式写入

 {flags:"a"}

  r:只读

 w:覆盖写入

 a:追加写入

```js
let ws = fs.createWriteStream(__dirname+"/写入文件/4.txt",{flags:"a"});
ws.write("这是格式1");
ws.write("这是格式2");
```



##### (5)文件读取和写入(记忆)

 第一个参数:读取目录中文件.且这个文件必须存在.

 第二个参数:回调函数(err,data)

 err:读取目录地址是否正确，如果是错误的地址，那么err会返回一个错误地址信息

 如果是目录地址没有错误，返回一个null

 data:读取到文件的信息。

```js
fs.readFile(__dirname+"/写入文件/1.jpg",(err,data)=>{
    //console.log(err)
    //console.log(data);
    第一个参数:写入目录文件地址
    第二个参数:写入内容
    第三个参数:回调函数
    err:返回成功或者失败
    fs.writeFile(__dirname+"/写入文件/mm.jpg",data,(err)=>{
     if(err)
     {
     console.log("写入文件失败")
     }else
     {
     console.log("写入文件成功")
     }
    })
})
```



##### (6):流文件读取和写入(比较大的文件：叫做流文件(视频或者音频文件))

```js
//读取流文件
let rd = fs.createReadStream(__dirname+"/写入文件/沙漠骆驼.mp3");
//读取的流文件写入到流文件中
let ws = fs.createWriteStream(__dirname+"/写入文件/abcd.mp3");
/*
要想把一个流文件写入到流文件中，那么这个rd流文件需要触发一个事件,data
事件。
*/
rd.on("data",(data)=>{
  ws.write(data);
})
```



##### (7):读取目录结构详细的内容(记忆)

  第一个参数:读取目录地址,这读取是一个目录不是文件.

  第二个参数:回调函数(err,file)

  err:读取的目录地址是否正确如果正确，返回的是一个null，如果错误返回错误地址信息.

 file:返回读取该目录结构下详细的内容，并且把读取的内容存放到数组中.

```js
fs.readdir(__dirname+"/写入文件",(err,file)=>{
    
})
```

##### (8):stat方法使用(记忆)

第一个参数:读取目录或者是文件

第二个参数:回调函数(err,stats)

err:读取的目录地址或者是文件地址是否正确如果正确，返回的是一个null，如果错误返回错误地址信息.

stats.isFile() //判断读取是否是一个文件

stats.isDirectory()//判断读取是否是一个目录

fs.stat(__dirname+"/写入文件/1.txt",(err,stats)=>{

  //console.log(stats)

  //console.log(stats.isFile());//true

  console.log(stats.isDirectory());//

})



##### (9):文件和目录操作（记忆）

######  1: fs.unlink() 只能删除文件，不能删除目录.

```js
fs.unlink(__dirname+"/写入文件/demo",(err)=>{
    if(err)
    {
    console.log("删除文件失败")
    }else
    {
    console.log("删除文件成功")   
    }
})
```

###### 2: fs.rmdir() 只能删除一个空目录，不能删除非空目录，也不能删除文件。

```js
fs.rmdir(__dirname+"/写入文件/demo",(err)=>{
    if(err)
    {
     console.log("删除目录失败")
    }else
    {
     console.log("删除目录成功")
    }
})
```

###### 3: fs.rename("加载剪切文件源路径地址","剪切文件存放的目标地址",(err)=>{})    剪切功能

```js
fs.rename(__dirname+"/写入文件/ceshi.txt",__dirname+"/写入文件/demo/ceshi.txt",(err)=>{
    if(err)
    {
     console.log("剪切失败")
    }else
    {
     console.log("剪切成功")   
    }
})
```

###### 4:fs.rename("读取源文件目录地址","更名目录地址",(err)=>{})  更名

```js
fs.rename(__dirname+"/写入文件/demo/ceshi1.txt",__dirname+"/写入文件/demo/ceshi.txt",(err)=>{
    if(err)
        {
         console.log("更名失败")
        }else
        {
         console.log("更名成功")   
        }
})

//注意: 不管是更名还是剪切功能,他不能跨磁盘操作.
```

###### 5: fs.mkdir()   创建一层目录

fs.mkdir(__dirname+"/写入文件/demo2",(err)=>{

​    if(err)

​    {

​     console.log("创建目录失败")

​    }else

​    {

​     console.log("创建目录成功")

​    }

})

###### 6:{recursive:true}  一次性创建多次目录结构

```js
fs.mkdir(__dirname+"/写入文件/demo2/a/b/c",{recursive:true},(err)=>{
    if(err)
    {
     console.log("创建目录失败")
    }else
    {
     console.log("创建目录成功")
    }
})
```



### 三:path模块（记忆）

path模块功能:主要做路径处理

let path = require("path");

注意:路径地址在程序中使用文件直接分隔符用/   系统里面读取是以\读取识别.

##### (1):path.basename(path)  返回的是该路径中最后一部分



​    path:第一个参数：路径地址

​    [ext]：第二个参数:对文件操作，是给一个后缀名，获取该文件前面部分.

​    path.basename(path,[ext])  ext:参数是默认省略的，如果加上：是给一个后缀名，获取该文件前面部分.

##### (2):path.win32.basename(path)  兼容系统参数路径地址

##### (3):全局路径方法

​    __dirname : 获取项目根目录地址

   __filename:获取当前模块完整路径地址

##### (4):path.dirname(path)  获取当前路径地址返回路径中目录部分

##### (5):path.isAbsolute()  判断该路径是否是一个绝对路径 如果是，返回true，不是返回false

##### (6):path.extname()  获取文件扩展名(文件的后缀名)

##### (7):path.resolve(path,ext)  将一个路径转换为绝对路径地址.

##### (8):path.join()  将路径地址进行连接 ,形成一个路径地址

##### (9):path.parse()  将一个路径地址解析到path中响应的属性参数中

##### (10):url模块解析路径地址到相应属性参数中

   ```js
let {URL} = require("url");
let urlstr = "https://user:admin@xiaoming:8080/a/b?c=text&a=123";
let a = new URL(urlstr);
console.log(a);
   ```



### 四:递归删除非空目录(同步方式)

​     unlink()只能输出文件，不能删除目录.  rmdir()只能输出空目录，不能删除文件

​     text目录

​                 a

​                     a.txt

​                     d文件夹

​                 b

​                     h文件夹

​                        t.txt

​                        p文件夹    

​                 c

​                1.txt

​                2.txt

 第一步：读取该目录详细信息

```js
let file = fs.readdirSync(dir); 
```

 第二步:  循环读取该目录内容，把内容装换绝对地址

```js
 file.forEach((item,index)=>{
    //console.log(item); 
    let pathurl = path.resolve(dir,item);
    //console.log(pathurl); 
 })
```

 第三步:判断目录下的内容是文件还是目录

```js
let stats = fs.statSync(pathurl); 
    if(stats.isFile())
    {
      //删除文件
      fs.unlinkSync(pathurl);
      console.log("你删除"+pathurl+"文件");
    }else
    {
        undir(pathurl); //递归  从新走刚刚的流程
    }
```

第四步:删除剩下最外层的空目录文件

fs.rmdirSync(dir);





作业：

1：使用Buffer加密base64,在进行解密.



2:判断ceshi根目录下结构，是文件还是目录，最好打印输出时目录结构内容

ceshi根目录

​                   1.txt

   				2.txt

  				 a文件夹

  				 b文件夹

[1.txt,2.txt,a,b]

[1.txt,2.txt]

[a,b]