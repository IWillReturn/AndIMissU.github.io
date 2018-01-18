---
title: 'CSS: hover选择器的使用'
date: 2018-01-18 11:00:49
tags: CSS
---

有些时候需要用到mouseover和mouseout这两个鼠标事件，但是写js又比较麻烦，还要添加监听事件，所以能用css解决的东西尽量yongcss解决，这样可以提高性能，下面说一下我对:hover 的了解:
之前在学计算机应用的时候，老师教我们使用了:hover选择器来完成下拉菜单，之前只知道怎么使用，并不知道为什么要这么用，现在记下怎么使用吧
定义和用法

<!--more-->

--------
**定义：**
:hover 选择器用于选择鼠标指针浮动在上面的元素。
:hover 选择器适用于所有元素

**用法1：**
这个表示的是：当鼠标悬浮在a这个样式上的时候，a的背景颜色设置为黄色

```
a:hover
    { 
        background-color:yellow;
    }
```

这个是最普通的用法了，只是通过a改变了style
**用法2:**
使用a 控制其他块的样式：

 - 使用a控制a的子元素 b：

```
    .a:hover .b {
            background-color:blue;
        }
```
 - 使用a控制a的兄弟元素 c(同级元素)：
 
```
    .a:hover + .c {
            color:red;
        }
```
 - 使用a控制a的就近元素d：

```
    .a:hover ~ .d {
            color:pink;
        }
```
 **总结一下：**

    1. 中间什么都不加  控制子元素；
    2. ‘+’ 控制同级元素（兄弟元素）；
    3. ‘～’ 控制就近元素；
    
----------
## 实例 ##

用一个按钮控制一个盒子的运动状态，当鼠标移到按钮上方时，盒子停止运动，鼠标移开时，盒子继续运动
    
**body代码：**

```
    <body>
        <div class="btn stop">stop</div>
        <div class="animation"></div>
    </body>
```
**css样式：**
```
    <style>
        .animation {
            width: 100px;
            height: 100px;
            background-color: pink;
            margin: 100px auto;
            animation: move 2s infinite alternate;
            -webkit-animation: move 2s infinite alternate;
        }
        @keyframes move {
            0% {
                transform: translate(-100px, 0);
            }
            100% {
                transform: translate(100px, 0);
            }
        }
        .btn {
            padding: 20px 50px;
            background-color: pink;
            color: white;
            display: inline-block;
        }
        .stop:hover ~ .animation {
            -webkit-animation-play-state: paused;
            animation-play-state: paused;
        }
    </style>
```
