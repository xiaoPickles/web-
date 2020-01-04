# jQuery

## 1.概述

### 1.1 JavaScript库

>  `JavaScript`库：即library,是一个封装好的函数与方法集合，即这个库中预先定义好的函数在里面，比如`animate`,`show`,`hide`等常用函数。

就库本身来说，就是一个JS文件，对我们原生的`js`代码进行封装，这样我们可以利用本有的函数快速高效的进行开发。

### 1.2 jQuery概述

`jQuery`是一个快速、简洁的`JavaScript`库，其设计宗旨是`write less,Do More`。

j 就是`JavaScript`，`Query`就是查询，即把`JavaScript`中的DOM操作进行封装，我们可以快速查询并使用库中封装好的功能。

jQuery封装了JavaScript常用的功能代码，优化DOM操作，事件处理、动画设计和Ajax交互。

我们学习`jQuery`就是学习调用这些函数与方法，学习成本低。

优点：

1. 轻量级，核心文件才几十kb,不会影响页面加载速度
2. 跨浏览器兼容，基本兼容现在的主流浏览器
3. 链式编程，隐式迭代
4. 支持插件扩展开发，有着丰富的第三方插件，如树形菜单、日期控件、轮播图等。
5. 免费、开源

## 2 基本使用

### 2.1 jQuery下载

[jQuery官网](https://jquery.com/)

<img src="./jquery.png" style="zoom:120%;" />

选择版本

 各版本区别

* 1x:兼容IE6,7,8，官网不再更新维护
* 2x:不兼容IE6,7,8，官网不再更新维护
* 3x:不兼容IE6,7,8，是官网主要更新维护的版本

### 2.2 jQuery基本使用

做一个隐藏`div`的小案例，体验`Jquery`的便捷与高效，代码不必看懂，但需要理解`jQuery`入口函数。

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    div{
      width: 100px;
      height: 100px;
      background-color: pink;
    }
  </style>
  <script src="./jquery.js"></script>
    //引入jQuery文件
  <script>
      //方法一：
    $(function(){
        //页面DOM加载完成时的入口
      var $div = $('div')
      $div.hide()
    })
      //方法二：
    // $(document).ready(function(){
      //页面DOM加载完成时的入口
    //   $('div').hide()
    // })
  </script>
</head>
<body>
  <div></div>
</body>
</html>
```

其中

```js
$(function(){
    ...
})
```

与

```js
$(document).ready(function(){
    ...
})
```

为Jquery的入口函数，它会等待DOM结构渲染完毕即可执行内部代码，不必等到所有外部资源加载完毕，相当于原生JavaScript中的`DOMContentLoaded`.

不同于原生JavaScript中的load事件必须等待页面文档外部`js`文件，`css`文件以及图片加载完毕才执行内部代码。

**对于上面两个入口函数，作用一致，推荐使用第一个**

### 2.3 $符号

1. $符号是jQuery的别称，在代码中可以使用jQuery代替$，但一般为了方便，通常直接使用$.

   我们可以把上面案例中的$换成`JQuery`，同样会隐藏div.

   ```js
   //js
   jQuery(function(){
       jQuery('div').hide()
   })
   ```

   

2. $是jQuery的顶级对象，相当于原生JavaScript中的window.我们可利用$把元素包装成jQuery对象，就可以调用jQuery的方法。

   ```js
   $(function(){
       console.log($('div'))
   })
   //打印jQuery对象
   ```

   <img src="./jqobj.png" alt="jquery对象" style="zoom:150%;" />

   

### 2.4 DOM对象与jQuery对象

1. DOM对象

   用原生JavaScript获取的对象就是DOM对象

   ```js
   //原生js获取对象
   window.onload = function(){
       var div = document.querySelector('div')
       console.dir(div)
       //有各种属性有方法
   }
   ```

   ![dom对象](./DOMobj.png)

2. jQuery

   用jQuery获取的对象就是jQuery对象。

   ![jQuery对象](./jqobj.png)

   我们再深究jQuery对象，属性是0→`length-1`的字符串和length，这是分明就是伪数组的标配。

3. `JQuery`对象只能使用jQuery方法，DOM对象则使用原生的JavaScript属性和方法。

   ```js
   window.onload = function(){
       var div = document.querySelector('div')
       div.style.display='none'
       //原生JavaScript隐藏盒子
       // $('div').style.display= 'none' 错误
   }
   ```

###  2.5 转换

> 因为原生JavaScript比jQuery更大，原生的一些属性与方法jQuery没有给我们封装，想要使用这些属性和方法就需要把jQuery对象转换为DOM对象才能使用。

1. DOM对象转换为jQuery对象。

   ```js
   $('DOM元素')
   ```

   

2. 