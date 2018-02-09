---
title: 'CSS: 实现tab切换'
date: 2018-02-08 21:43:19
tags: CSS
---

纯CSS能实现tab切换，目前我知道的有两种方法：
-  一种是用`<a href="...">`来写；
-  结合`<input>`和 `<label>`实现；

基本布局如下：
![基本布局][1]


  [1]: /photos/CSS/css-tab.png
<!--more-->

效果Gif：

![效果图][2]


  [2]: /photos/CSS/tab.gif

基础样式如下：



以下是两种方法的实现过程（以上的图片还画不了这么好看）：

### 1. 用`<a href="...">`实现tab切换
  -  HTML body 部分
    ``` Html
      <body>
        <div class="body">
          <div class="content" id="content-1">The Course Information</div>
          <div class="content" id="content-2">The Teacher Information</div>
          <div class="content" id="content-3">The Schoold Information</div>
          <ul class="tab">
            <li id="href-1">
              <a href="#content-1">Course</a>
            </li>
            <li id="href-2">
              <a href="#content-2">Teacher</a>
            </li>
            <li id="href-3">
              <a href="#content-3">School</a>
            </li>
          </ul>
        </div>
      </body>
    ```
  -  body的样式 
    ``` CSS
      * {
        margin: 0;
        padding: 0;
      }
      .body {
        width: 600px;
        height: 300px;
        margin: auto;
        margin-top: 100px;
        position: relative;
      }
      .tab {
        width: 100%;
        height: 50px;
        list-style: none;
        position: absolute;
      }
      #href-1,
      #href-2,
      #href-3 {
        width: 33%;
        border: 1px solid #666;
        float: left;
        text-align: center;
        line-height: 50px;
      }
      #href-1,
      #href-2 {
        border-right: none;
      }
      #href-1 {
        border-top-left-radius: 10px;
      }
      #href-3 {
        border-top-right-radius: 10px;
      }
      .tab li a {
        text-decoration: none;
        color: #333;
      }
      .content {
        width: 596px;
        height: 250px;
        border: 1px solid #666;
        position: absolute;
        border-top: none;
        border-bottom-left-radius: 10px;
        border-bottom-right-radius: 10px;
        margin-top: 50px;
        display: none;
        text-align: center;
        line-height: 220px;
        font-size: 20px;
      }
    ```
  -  target 部分，由于要使用到普通相邻选择符 “～”（ E ~ F ），E～F选择符中的E和F在文档中必须被相同的元素包含（**具有相同的父元素**），且文档中**F在E的后面出现**，无需紧随其后，这就是上面为什么内容的布局写在tab的后面的原因
    ``` CSS
      #content-1:target,
      #content-2:target,
      #content-3:target {
        display: block;
      }

      #content-1:target~.tab #href-1,
      #content-2:target~.tab #href-2,
      #content-3:target~.tab #href-3 {
        background: #666;
      }
    ```

### 2. 结合`<input>`和 `<label>`实现tab切换
  -  HTML部分
    ``` Html
      <div class="body">
        <input type="radio" class="tab1" id="li-1" name="tab" checked>
        <input type="radio" class="tab2" id="li-2" name="tab">
        <input type="radio" class="tab3" id="li-3" name="tab">
        <ul class="tab">
          <li class="tab-li-1">
            <label for="li-1">Course</label>
          </li>
          <li class="tab-li-2">
            <label for="li-2">Teacher</label>
          </li>
          <li class="tab-li-3">
            <label for="li-3">School</label>
          </li>
        </ul>
        <div class="content">
          <div id="content-1">The Course Information</div>
          <div id="content-2">The Teacher Information</div>
          <div id="content-3">The Schoold Information</div>
        </div>
      </div>
    ```
  -  style 部分
    ``` CSS
      * {
        margin: 0;
        padding: 0;
      }
      .body {
        width: 600px;
        height: 300px;
        margin: auto;
        margin-top: 100px;
        position: relative;
      }
      .tab {
        width: 100%;
        height: 50px;
        list-style: none;
      }
      .tab li {
        width: 33%;
        height: 50px;
        float: left;
        border: 1px solid #666;
        line-height: 50px;
        text-align: center;
      }
      .tab li:first-child {
        border-right: none;
        border-top-left-radius: 10px;
      }
      .tab li:last-child {
        border-left: none;
        border-top-right-radius: 10px;
      }
      .content {
        width: 596px;
        height: 250px;
        border: 1px solid #666;
        border-top: none;
        border-bottom-left-radius: 10px;
        border-bottom-right-radius: 10px;
        text-align: center;
        line-height: 230px;
        font-size: 20px;
      }
      .content div {
        display: none;
      }
      input[type="radio"] {
        display: none;
      }
    ```
  -  checked 部分代码
    ``` CSS
      .tab1:checked ~ .content #content-1,
      .tab2:checked ~ .content #content-2,
      .tab3:checked ~ .content #content-3 {
        display: block;
      }
      .tab1:checked ~ .tab .tab-li-1,
      .tab2:checked ~ .tab .tab-li-2,
      .tab3:checked ~ .tab .tab-li-3 {
        background: lightblue;
      }
    ```
  
  <br/>

**最后的结果我个人觉得 input的更好，因为`<a>`会在浏览器的网址后面添加跳转地址，但是这个网址是不存在的，所以强迫症的我用起来还是觉得结合`radio`使用更顺畅**





