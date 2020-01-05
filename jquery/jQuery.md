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

> 因为原生JavaScript比jQuery更大，如某些情况下，原生的一些属性与方法jQuery没有给我们封装，想要使用这些属性和方法就需要把jQuery对象转换为DOM对象才能使用。

我们现在想播放一个小视频，[视频链接地址](https://www.sample-videos.com/),但是`jQuery`并没有帮我们封装这个`play`方法，只能使用DOM对象的`play`方法，我们有两种方法获取DOM对象：

| 序列 | 方式                      |
| ---- | ------------------------- |
| 1    | 使用原生js获取DOM对象     |
| 2    | 将jQuery对象转换为DOM对象 |



1. 原生js获取DOM对象

   语法：`$(DOM对象)`

   ```html
   <!DOCTYPE html>
       <html lang="en">
           <head>
           <meta charset="UTF-8">
               <meta name="viewport" content="width=device-width, initial-scale=1.0">
                   <meta http-equiv="X-UA-Compatible" content="ie=edge">
                       <title>Document</title>
   <script src="./jquery.js"></script>
   <script>
       $(function(){
       var video = document.querySelector('video')
       // 原生js获取DOM元素
       console.log($(video))
       // $(video)就是一个通过DOM对象转换而来的jQuery对象
       //  但是我们不能使用$(video).play()
       // 因为jQuery对象没有play这个方法，想要播放功能只能使用DOM对象
       video.play()
   })
   </script>
   </head>
   <body>
       <video src="./test.mp4" style="width: 500px;" muted></video>
   <!-- 添加muted属性，否则谷歌默认不播放视频 -->
           </body>
   </html>
   ```

   

   * 直接获取

     ```js
     // $('DOM元素或选择器')
     ```

2. jQuery对象转换为DOM对象

   我们有两种方式可将`jQuery`对象转换为`DOM`对象：

   | 序列 | 方式                    | 备注                                 |
   | :--- | ----------------------- | ------------------------------------ |
   | 1    | $('element')[index]     | `index`是索引号，element是`html`元素 |
   | 2    | $('element').get(index) | `index`是索引号                      |

   ```js
   $(function(){
       $('video')[0].play()
   })
   ```

   


## 3 常用API

### 3.1 选择器

原生`js`获取的元素方式很多很杂，而且兼容性不一致，因此`JQuery`进行了封装，获取元素使用统一标准。

```js
$('选择器')//直接填写CSS选择器，但是要加引号
```

| 名称       | 用法                    | 描述                                                         |
| ---------- | ----------------------- | ------------------------------------------------------------ |
| ID选择器   | $('#id')                | 获取指定ID元素                                               |
| 全选选择器 | $('*')                  | 匹配所有元素                                                 |
| 类选择器   | $(".class")             | 获取同一类class元素                                          |
| 标签选择器 | $('element')            | 获取同一类标签的所有元素                                     |
| 并集选择器 | $('#id,.class,element') | 获取多个元素                                                 |
| 交集选择器 | $(".class#id")          | 选择器之间没有任何连接符，用于获取交集元素                   |
| 子代选择器 | $(".class > element")   | 使用>号，获取亲儿子层级的元素；注意，不会获取孙子层级的元素。 |
| 后代选择器 | $(".class  element")    | 使用空格，代表后代选择器，获取当前层级下的所有元素。         |

```js
//获取类型为 .nav的元素
$('.nav')
//与css选择器一致
```

### 3.2  隐式迭代

>  遍历内部DOM元素（伪数组形式存储）的过程就叫做隐式迭代。
>
> 即将匹配到的所有元素进行循环遍历，执行相应的方法，而不用我们再循环遍历，简化我们的操作，方便我们使用。

案例：获取页面的`div`,将背景颜色设置为你喜欢的颜色。

**注意：**`jQuery`对象不能使用DOM对象的`style`之类的属性设置样式。

`jQuery`设置样式：

```js
$('element').css('属性名','属性值')
```

设置样式代码：

```js
$(function(){
    $('div').css('backgroundColor','pink')
})
```

`jQuery`对匹配到的所有`div`元素进行循环遍历，添加背景样式，应此行为不是人为，所以称为隐式迭代。

### 筛选选择器

| 语法       | 用法                | 描述                                           |
| ---------- | ------------------- | ---------------------------------------------- |
| :first     | $("element:first")  | 获取第一个元素(element表示要获取的元素)        |
| :last      | $("element:last")   | 获取最后一个元素                               |
| :eq(index) | $("element :eq(2)") | 获取到的元素中，索引号为2的元素，索引号从0开始 |
| :odd       | $("element:odd")    | 获取到的元素中，索引号为奇数的元素             |
| :even      | $("element:even")   | 获取到的元素中，索引号为偶数的元素中           |

案例：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="./jquery.js"></script>
  <script>
    $(function(){
      $('div:first').css("fontSize","40px")
      // 获取到的第一个div字体设置为40px
      $('div:last').css('color',"red")
       // 获取到的最后一个div颜色设置为红色
       $('div:eq(2)').css("color","pink")
       // 获取到的div索引号为2的颜色设置为粉红色
       $('div:odd').css("backgroundColor","rgb(200,200,200)")
       //索引号为奇数的背景颜色设置为灰色
       $("div:even").css("backgroundColor","rgb(100,200,200)")
       //索引号为偶数的背景颜色设置为绿色
    })
  </script>
</head>
<body>
  <div>0</div>
  <div>1</div>
  <div>2</div>
  <div>3</div>
  <div>4</div>
</body>
</html>
```

### 3.3  jQuery的筛选方法

| 语法               | 用法                              | 说明                                     |
| ------------------ | --------------------------------- | ---------------------------------------- |
| parent( )          | $("element").parent( )            | 查找最近的父级                           |
| children(selector) | $("element").children("elenment") | 查找最近一级的子级元素，相当于子代选择器 |
| find(selector)     | $("element").find("element")      | 相当于后代选择器                         |

**注意以上全是方法**

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <script src="./jquery.js"></script>
  <script>
    $(function(){
     $('span').parent().css('fontSize','30px')
     $('.test').children('p').css('color','red')
     $('.test').find('p').css('backgroundColor','#ccc')
    })
  </script>
</head>
<body>
  <div>
    父级
    <span></span>
  </div>
  <div class="test">
    <p>wrap</p>
    <div>
      <p>inner</p>
    </div>
  </div>
</body>
</html>
```

### 3.4 下拉菜单

**案例：英雄联盟官网常用的更新与赛事下拉菜单：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <style>
    *{
      margin: 0;
      padding: 0;
      list-style: none;
    }
    .wrap{
      margin-top: 20px;
      display: flex;
      justify-content: center;
    }
    .inner{
      width: 158px;
      padding: 0 5px 0 5px;
      background-color: rgb(209, 81, 226);
    }
    .inner>li{
      cursor: pointer;
    }
    .hide{
      display: none;
    }
  </style>
  <script src="./jquery.js"></script>
  <script>
    $(function(){
      //移入
   $('.inner').mouseover(function(){
     $(this).children('.hide').show()
       //$(this)表示当前元素，show()显示元素
   })
   //移出
   $('.inner').mouseout(function(){
     $(this).children('.hide').hide()
       //hide()隐藏元素
   })
    })
  </script>
</head>
<body>
  <div class="wrap">
    <ul class="inner">
      <li>综合</li>
      <ul class="hide">
        <li>2020LPL春季赛程公布</li>
        <li>2019德玛西亚杯冠军</li>
        <li>云顶之弈</li>
      </ul>
    </ul>
    <ul class="inner">
      <li>公告</li>
      <ul class="hide">
        <li>转区变更通知</li>
        <li>处罚名单</li>
        <li>英雄联盟更新公告</li>
      </ul>
    </ul>
    <ul class="inner">
      <li>攻略</li>
      <ul class="hide">
        <li>高胜率打野</li>
        <li>中单剑魔</li>
        <li>云顶之弈上分攻略</li>
      </ul>
    </ul>
  </div>
</body>
</html>
```

### 3.5 其他筛选方法

| 语法                | 用法                               | 说明                                             |
| ------------------- | ---------------------------------- | ------------------------------------------------ |
| sibilings(selector) | $('element').sibilings('element')  | 查找兄弟元素，不包括自己（重要）                 |
| nextAll()           | $('element').nextAll( )            | 查找当前元素之后的所有同辈元素                   |
| pervtAll()          | $('element').prevtAll( )           | 查找当前元素之前的所有同辈元素                   |
| hasClass(class)     | $('element').hasClass('className') | 检查当前元素是否含有某个特定的类，如有，返回true |
| eq(index)           | $('element').eq(index)             | 相当于`$('element:eq(index)')`（重要）           |

```html
...
<script src="./jquery.js"></script>
<script>
    //重点掌握siblings()方法和eq()方法
    $(function(){
        //除.order外的所有兄弟元素li
        $("ol .order").siblings('li').css("color",'red')
        // 选择第n个元素
        //(1)筛选选择器
        $('ul li:eq(2)').css('backgroundColor','pink')
        //eq方法(推荐)
        $('ul li').eq(1).css('color','#ccc')
    })
</script>
</head>
<body>
    <ol>
        <li>有序1</li>
        <li class="order">有序2</li>
        <li>有序3</li>
    </ol>
    <ul>
        <li>1</li>
        <li>2</li>
        <li>3</li>
    </ul>
</body>
...
```

### 3.6 jQuery排他思想

案例：在页面写入四个按钮，当点击某个按钮时，该按钮变色，其他的按钮恢复原来的颜色。

```html
...
<script src="./jquery.js"></script>
<script>
    $(function(){
        //利用隐式迭代思想，无需遍历
        $('button').click(function(){
            //获取当前按钮并设置背景颜色
            $(this).css('backgroundColor','pink')
            //去除其他按钮背景颜色
            $(this).siblings('button').css('backgroundColor','')
        })
    })
</script>
</head>
<body>
    <button>1</button>
    <button>2</button>
    <button>3</button>
    <button>4</button>
</body>
...
```

### 3.7 淘宝服饰精品案例

```js

```



