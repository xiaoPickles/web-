# 基本介绍

目的：入坑服务端。

熟悉服务端数据接收，与后台人员更好的配合。

掌握基本的网站开发能力。

##  1.1 node介绍

* Node.js ® is a JavaScript runtime built on [Chrome's V8 JavaScript engine](https://v8.dev/).
  1. Node.js 是一个JavaScript运行时环境。
  2. 可以解析执行JavaScript代码。
  3. 可以脱离浏览器执行 `js` 代码.（仅有`ECMAScript`）
  4. 提供一些服务器级别的操作 `API`
     * 文件读写
     * 网络服务构建
     * 网络通信
     * `http`服务器

* 事件驱动和非阻塞`I/O`模型（异步）。
* Node.js' package ecosystem [npm](https://www.npmjs.com/)
  * `npm` 是世界上最大的开源库生态系统

采用`JavaScript`进行编程，**凡事能`js`实现的，最终都会用`js`.**

## 1.2 Node能做什么

* web 服务后台
* 命令行工具
  + `npm`
  + `git(c语言开发)`
  + hexo(node)
  + . . .

## 1.3 预备知识

* HTML 
* CSS
* JavaScript
* 简单的命令行操作
  * cd
  * dir
  * Is

## 1.4 一些资源

* 《深入浅出Node.js》
  * 作者：朴灵
  * 偏理论，几乎无任何实战内容
* 《Node.js权威指南》
  * `API` 讲解
  * 无实战
* [Node入门](https://www.nodebeginner.org/index-zh-cn.html)

## 1.5 能学到啥

* B/S 编程模型
  * Browser-Server
  * 任何服务端技术这种B/S编程模型一样，与语言无关
* 模块化编程
  * 将`js`文件作为模块，以引入模块方式，加载`Javascript`文件
* `Node`常用`API`
* 异步编程
* `Express` 开发框架
* `ES6`

## 1.6 模块

`Nodejs`模块采用`CommonJS`规范,主要是以下三种模块。

* 核心模块
* 第三方模块
* 用户自定义模块

### 1.6.1 核心模块

Node中为JavaScript提供了许多服务器级别的`API`，这些`API`绝大多数都被包装到一个具名的核心模块中，例如文件操作`fs`核心模块，服务器构建的`http`模块,`path`路径操作模块,`os`操作系统信息模块。

只要是核心模块，我们就需要使用`require`方法加载方能使用。

```js
var fs = require("fs")//模块名固定，不得更改
var os = require("os")
...
```

### 1.6.2 自定义模块

1. 我们将公共的功能抽离为单独的`js`文件作为一个模块。默认情况模块内部定义的属性和方法，外界无法访问。如果外部需要访问模块内部定义的属性和方法，则需要在模块内部通过`exports`或者`module.exports`暴露属性和方法。
2. 使用这些模块时，通过`require`方式引入模块。

```js
//加载模块并执行
require("relative path") 
//可以省略后缀名
//填入相对路径，代码执行至此处时，会执行指定文件内的代码
```

Node中没有全局作用域，只有模块作用域（作用域是封闭的），不同模块内相同变量名、函数名、对象名不会冲突，不会污染其他文件。**内部文件访问不到内部，内部也访问不到外部。**

有时我们加载自定义模块不是为了执行里面的代码，而是访问内部的成员，我们需要借用`exports`借口对象.

`require`方法有两个作用：

1. 加载文件模块并执行文件内部的代码。
2. 拿到被加载文件模块导出的接口对象。

 每一个文件模块都提供一个接口对象`exports`,默认为空对象。

```js
//新建export.js文件
console.log(exports)// {}
```

我们需要做的便是将所有需要导出的成员作为exports对象的属性或者方法导出，然后在需要引用的文件中利用`require`方法引入。

```js
function add(a,b) {
  console.log(a+b)
}
exports.add=add
// 将函数add赋值给exports对象的add方法
```

```js
//新建 require.js文件，两文件必须在同一目录下
var obj = require("./export.js")
//obj接收require方法返回的对象
obj.add(1,3)
```

### 1.6.3 `npm`与第三方模块

`npm`是世界上最大的开放代码的生态系统，我们可以通过`npm`下载各式各样的源代码(包或者模块。

创建`package.json`文件

```js
//npm init
```



安装命令：

```js
// npm install MoudleName --save 
```

使用`--save`安装包，安装依赖在 `package.json` 中( 定义了这个项目所需要的各种模块，以及项目配置信息，如名称、版本号‘许可证等)，如果`node_moudles`被删除，可以通过**`npm i`**重新安装依赖(模块)。

删除包命令：

```js
// npm uninstall MoudleName
```

指定安装版本：

```js
// npm install Moudle@指定版本  --save
```



# 起步

## 2.1 安装Node环境

[node](https://nodejs.org/en/) 安装网站，选择`LTS`稳定版（long-time-sport），或者选择`current`体验版。

检查是否安装成功:`Windows+R`打开任务管理器，输入`cmd`,检查版本 `node --version`，输出`v12.13.1`,便安装成功。

## 2.2 Hello Word

编写一个名为`hello.js`的`JavaScript`文件。

```js
var demo = "Hello node.js"
console.log(demo)
```

定位该文件所在的目录，打开命令行窗口，输入`node hello.js`,命令行窗口打印`Hello node.js`.

在`Node`采用`ECMAScript`编码，没有`DOM`,`BOM`API

```js
console.log(window) //报错
```

## 2.3 文件基础操作

### 2.3.1 检测与创建

```js
const fs = require('fs')
// 检测资源是目录还是文件
fs.stat('./img',(error,data)=>{
  if(error){
    console.log('error')
    return
  }
  console.log(`是目录:${data.isDirectory()}`)//是目录:true
  console.log(`是文件:${data.isFile()}`) //是文件:false
})
//创建目录
fs.mkdir('./css',(error)=>{
  if(error){
    console.log(error)
    return
  }
  console.log('成功')
})
//不能创建已存在的文件,否则会报错
```



### 2.3.2 读取文件

Node中JavaScript具有文件操作能力。新建`read.js`文件,再新建一个`read.txt`文件,写入`JavaScript语言是一门优秀的编程语言。`，在`js`文件中写入代码。

1. 引入文件系统模块`fs`

   `fs`是`file-system`的简写，如要进行文件操作，就必须引入`fs`核心模块。

```js
var fs = require("fs")
```

2. 调用`readFile`方法。它接收两个参数，参数1是读取文件位置，第二个参数是回调函数，它又接收两个参数，`erroe`与`data`.
   * 读取成功，`data`为含数据的对象，`error`为`null`。
   * 读取失败，`error`为错误对象,`data`为`undefined`

```js
fs.readFile("./read.txt",function(error,data){
    console.log(data)
    //<Buffer 4a 61 76 61 53 63 72 69 70 74 e8 af...  
    //16进制的buffer结构
})
```

​      

 命令行输入：`node read.js`

如是输出以上内容，证明读取成功。打印的是16进制的buffer结构，需要通过`toString`方法转为字符串。

```js
fs.readFile("./read.txt",function(error,data){
    console.log(data.toString())
    //JavaScript语言是一门优秀的编程语言。
})
```

### 2.3.3  创建并写入文件

在`des`文件中写入内容。

调用`writeFile`函数，第一个参数为文件路径，第二个参数为文件内容，第三个参数为回调函数(`callback`),接收一个参数`error`.

* 文件写入成功，`error`为`null`。
* 文件写入失败,`error`为错误对象。

```js
var fs = require("fs")
var content = "Welcome node.js"
fs.writeFile("./des.txt",content,function(error){
  if(error === null){
    console.log("成功") //成功
  }else{
    console.log("失败")
  }
})
```

`des.txt`文件内容为Welcome node.js,原来的内容被覆盖。

### 2.3.4 追加文件

```js
const fs = require('fs')
const content = 'hello worl d撒旦'
fs.appendFile('./index.txt',content,(error)=>{
  if(error){
    console.log(error)
    return
  }
  console.log('追加文件成功')
})
```

追加文件与创建文件参数一致，不同的是，文件如已存在，只会追加内容，而不会替换原有内容。

### 2.3.5 读取目录

```js
const fs = require('fs')
fs.readdir('../www',(err,data)=>{
  if(err){
    console.log(err)
    return
  }
  console.log(data)
  //返回数组
})
```

### 2.3.6 重命名

```js
const fs = require('fs')
fs.rename('./index.txt','./str.txt',(err)=>{
  if(err){
    console.log(err)
    return
  }
  console.log('重命名成功')
})
```

`rename`方法接收三个参数，第一个为旧路径，第二个为新路径，参数三为回调函数，所以`rename`方法不仅可以重命名，也可以移动文件。

### 2.3.7 删除目录与文件

```js
const fs = require('fs')
fs.rmdir('./css',(err)=>{
  if(err){
    console.log(err)
  }
  console.log('删除目录成功')
})
```

上述目录为一个空目录，如果目录内部存在文件，则不能成功删除，需要借助`unlink`方法删除子文件，最后才能删除目录。

```js
// 删除文件演示代码
const fs = require('fs')
fs.unlink('./str.txt',(err)=>{
  if(err){
    console.log(err)
  }
  console.log('删除文件成功')
})
```



## 2.4 文件操作案例

1. 判断服务器上有没有upload目录，如果没有创建这个文件。

   ```js
   var fs = require('fs')
   const path = './upload'
   fs.stat(path,(err,data)=>{
     if(err){
       // 没有则创建upload目录
       fs.mkdir(path,(err)=>{
         if(err){
           console.log(err)
           return
         }
         console.log('创建新目录成功')
       })
     }else{
       if(data.isDirectory()){
           //判断是目录还是文件
         console.log('目录存在')
         return
       }
       // 删除文件
       fs.unlink(path,(err)=>{
         if(err){
           console.log(err)
           return
         }
         console.log('删除文件成功')
       })
       // 创建目录
       fs.mkdir(path,(err)=>{
         if(err){
           console.log(err)
           return
         }
         console.log('更新目录成功')
       })
     }
   })
   ```

   我们也可以选用第三方包`mkdirp`，直接生成目录。

2. 将`www`目录下所有的目录添加到数组中。

   **提示**：node中几乎所有的方法都是异步。

   ```js
   const fs = require('fs')
   const dirArray = []
   fs.readdir('../www',(err,data)=>{
     if(err){
       console.log(err)
       return
     }
     data.forEach((item)=>{
       fs.stat(`./${item}`,(error,result)=>{
         if(error){
           console.log(error)
           return
         }
         if(result.isDirectory()){
           dirArray.push(item)
             //异步操作总是最后执行，暂时想不到一个好方法打印dirArray
           console.log(dirArray)
         }
       })
     })
   })
   console.log(dirArray) // []
   ```

   **采用node新特性: `async`与`await`**

   ```js
   async function add() {
     return '1131'
   }
   console.dir(add()) 
   //Promise { '1131' } 返回promise对象
   ```

   `async`关键字用于将普通函数转化为异步函数，返回一个`promise`对象。

   `await` 用于获取异步方法中的数据，注意必须在异步函数中使用，否则报错。

   ```js
   // 创建一个getData异步函数，用于获取 add函数中的数据。
   async function getData() {
     const data = await add()//await 只能在异步函数中使用
     console.log(data)
   }
   getData()// 1131
   ```

   

## 2.4 端口与 IP

所有联网的程序都需要进行网络通信，为了保证正确通信的地址，则需要以IP地址来定位，而端口号则是用来定位具体的应用程序，所以需要进行联网通信的程序都会占用一个端口号。

**小知识**：端口号范围是`0~65336`之间。

## 2.5 简单的HTTP服务

node中专门提供了一个核心模块：`http`,用于创建web服务器。

新建`hello.js`文件,添加以下代码。

1. ```js
   var http = require("http")
   //加载http模块
   ```

2. ```js
   var server = http.createServer()
   ```

   使用`http.createServer`方法创建一个web服务器，返回一个`Server`实例。

3. ```js
   server.on("request",function(request,response){
     console.log(`请求地址${request.url}`)
     response.write("hello node.js")
      //响应内容只能是二进制数据或者字符串
     response.end()//结束响应
   })
   ```

   注册`request`请求事件，当接受到客户端请求时，自动触发服务器`request`请求事件，执行`request`请求事件处理函数。它接收两个参数。

   * 第一个参数是`request`请求对象，可以获取客户端的一些请求信息，例如请求路径。
   * 第二个参数是`response`响应对象，它有一个`write`方法，可以给客户端发送响应消息。`write`方法可以使用多次，但是最后一定要使用`end`方法结束响应，否则客户端会一直等待。

4. ```js
   // 绑定端口号，启动服务器
   server.listen(3000,function(){
       console.log("服务器启动成功，http://127.0.0.1:3000/")
   })
   ```

5. 思考：请求不同的路径返回的是hello node.js，我们现在有个需求，请求`/`路径返回主页，请求`/login`返回登录。

   ```js
   server.on("request",function(request,response){
     if(request.url==="/"){
       response.write("home")
     }else if(request.url==="/login"){
       response.write("登陆")
     }else{
       response.write("404 not found")
     }
     response.end()//结束
   })
   ```

   我们可以简化以下代码，在结束响应的同时，发送响应结果，则不需要使用`write`方法。

   ```js
   response.end("information")
   ```

6. 乱码问题。  

   服务端默认发送的数据是`utf-8`编码内容，浏览器在不知服务器响应内容编码的情况下，会按照当前系统默认编码解析(中文操作默认是`gbk`，导致出现乱码问题。我们需要告知浏览器响应内容类型即可，在步骤`5`中每个判断语句中写入以下响应头即可解决乱码问题

   ```javascript
   //中文乱码解决方案
   //设置响应头 状态码是200，文件类型为普通文本，字符集是utf-8
    res.writeHeader(200,{'Content-Type':'text/plain;charset="utf-8"'})
   ```

   如果相应内容为`html`标签，则响应内容类型为`text/html`。

**注意**：

* 如果同时开两个服务器，端口不能重复，否则会报错。
* 如有修改文件，需要重启服务器。



## 2.6 `url` 模块

我们有一个需求，需要获取`url`中的查询字符串，这就需要使用核心模块——`url` 模块。

```js
const url = require('url')
const result=url.parse('https://www.yuque.com/dashboardname=as&age=12'
 ,true)
//将url字符串解析为Url对象
/*第二个可选参数设置为true时，会使用
querystring模块来解析URL中的查询字符串部分，
返回一个query对象,否则是一个查询字符串
默认为 false*/
console.log(result)
//{ name: 'as', age: '12' },
```

我们了解`url`模块的基本使用方法，可以将其应用到`http`服务器中，当我们访问不同的路径地址，要求返回不同的查询字符串。

```js
const http = require('http') // 创建web服务
const url = require('url')
const server = http.createServer()
server.on('request',(req,res)=>{
  if(req.url !== '/favicon.ico'){
     /*客户端会发出两次请求，一个是我们客户输入的url,
     另一个是请求的是标题上的图标*/
    const result = url.parse(`http://127.0.0.1:3000${req.url}`,true)
    console.log(result.query.name)
  }
  //设置响应头 状态码是200，文件类型为普通文本，字符集是utf-8
  res.writeHeader(200,{'Content-Type':'text/plain;charset="utf-8"'})
  res.write('欢迎来到英雄联盟')
  res.end()//结束响应
})
server.listen(3000,()=>{
  console.log('http://127.0.0.1:3000')
})
```

我们只需在 http://127.0.0.1:3000 后面输入`/name=xxx`即可得到响应的查询字符串。

## 2.7 HTTP服务进阶



我们这次不在单纯响应简单的文本内容，这次响应`html` 页面，我们知道响应内容只能是二进制数据或者字符串，将`html`页面全部写入响应方法中很不现实，所以就需要读取文件，而文件本身是以二进制存储.  

```                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                  javascript
var http = require("http")
var fs = require("fs")
var server = http.createServer()
server.on("request",function(req,res){
  var url = req.url
  if(url==="/"){
    fs.readFile("./test.html",function(error,data){
      if(error){
        res.setHeader("Content-Type","text/plain;charset=utf-8")
          /*Content-Type 服务器将响应的内容的类型告知客户端，
          客户端会根据Content-Type进行解析处理*/
          //文本数据类型需添加编码，否则会乱码
        res.end("错误")
      }else{
        res.setHeader("Content-type","text/html;charset=utf-8")
        res.end(data)//读取二进制文件
      }
    })
  }
})
server.listen(3000,function(){
  console.log("server is running")
})
```

`小知识点`

采用无分号风格时，以 `(，[，` 开头,前面需要加上分号，以避免无必要的语法解析错误。

```js
;(function  add() {
    console.log("1+2")
})()
;['1'.'2'].forEarch((item)=>{
    console.log(item)
})
```



## 2.8  低仿阿帕奇服务器

上述服务器可以满足访问相关地址返回不同数据，但是实际开发过程中访问的页面可不仅仅这几个，如果采用如上方法，会造成代码冗余。所以接下来优化服务器，我们创建一个`www` 的文件夹，访问的`url`即子文件所在`www`文件夹中的相对路径。

```js
const http = require('http')
const fs = require("fs")
// 1.创建web服务器
const server = http.createServer()
const mainPath = 'C:/Users/Asus/Desktop/www'
//  2. 监听request事件，创建请求处理函数
server.on('request',function (req,res) {
  let filePath = '/index.html'
  if(req.url !== '/'){
    filePath = req.url
  }
  fs.readFile(`${mainPath}${filePath}`,function (err,data) {
    if(err){
      return res.end('404 not found')
    }
    res.end(data)
  })
})
//3 . 绑定端口号
server.listen(3000,function () {
  console.log("服务器已启动，请打开 http://127.0.0.1:3000")
})
```

这和以前的代码无异，分三步走。

1. 创建`web`服务器
2. 监听request事件，创建请求处理函数
3. 绑定端口号，开启服务

主要差别在监听`request` 事件上，我们设置一个基本 ` url` 变量，文件访问路径即主路径+子路径，而子路径即文件所在文件夹的相对路径，如是，难度似乎不大。

## 2.9 改进服务器

我们还需要根据不同的扩展名设置不同的响应头，需要用到`path`模块的`extname`方法，获取文件后缀名，根据不同后缀名，响应不同的文本类型。

```js
const http = require('http')
const fs = require('fs')
const path = require('path')
const server = http.createServer()
let extPath = ''
function extName(p) {
  switch (p) {
    case '.html':
      extPath = 'text/html'
      break;
    case '.css':
      extPath = 'text/css'
      break
    case '.png':
      extPath = 'image/png'
      break
    case '.json':
      extPath = 'application/json'
      break
    case '.js':
      extPath = 'text/js'
      break
    case '.zip':
      extPath = 'text/zip'
      break
    default:
      extPath = 'text/html'
      break;
  }
}
server.on('request',(req,res)=>{
  const url = req.url
  let filePath = '/index.html'
  if(url!=='/'){
    filePath = url
  }
  fs.readFile(`.${filePath}`,(err,data)=>{
     const p = path.extname(filePath)//获取扩展名
     extName(p)
    if(err){
      res.end('404 not found')
      return
    }
    res.writeHead(200,{'Content-Type':`${extPath};charset= "utf-8"`})
    res.end(data)
  })
})
server.listen(3001,()=>{
  console.log('http://127.0.0.1:3001')
})
```



## 非阻塞I/O、异步与事件驱动

```js
const fs = require('fs')
function getData() {
  fs.readFile('./index.css',(err,data)=>{
    return data
  })
}
console.log(getData()) // undefined
```

**解决方案**

1. 回调函数

```js
const fs = require('fs')
function getData(result) {
  console.log(result)
}
function readData(callback) {
  fs.readFile('./index.css',(err,data)=>{
    callback(data)
  })
}
readData(getData)
//<Buffer 68 32 7b 0d 0a 20 20 63 6f...
```

2. `event`模块

```js
const fs = require('fs')
const events = require('events')
// 创建eventEmitter 对象
const eventsEmitter = new events.EventEmitter()
// 订阅事件
eventsEmitter.on('getdata',(data)=>{
  console.log(data)
})
function getData() {
  fs.readFile('./index.css',(error,result)=>{
    // 发布事件
    eventsEmitter.emit('getdata',result)
  })
}
getData()
//<Buffer 68 32 7b 0d 0a 20
```

