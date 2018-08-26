# HTML5简介

### 什么是 HTML5

HTML5并不仅仅只是做为HTML标记语言的一个最新版本，更重要的是它制定了Web应用开发的一系列标准，成为第一个将Web做为应用开发平台的HTML语言。

HTML5定义了一系列新元素，如新语义标签、智能表单、多媒体标签等，可以帮助开发者创建富互联网应用，还提供了一些Javascript API，如地理定位、重力感应、硬件访问等，
可以在浏览器内实现类原生应用。我们甚至可以结合 Canvas 开发网页版游戏。

HTML5的广义概念：HTML5代表浏览器端技术的一个发展阶段。在这个阶段，浏览器的呈现技术得到了飞跃发展和广泛支持，它包括：HTML5、CSS3、Javascript API在内的一套技术组合。


### 语义化的标签

在此基础上，HTML5 增加了大量有意义的语义标签，更有利于搜索引擎或辅助设备理解 HTML 页面内容。
HTML5会让HTML代码的内容更结构化、标签更语义化。

**传统HTML布局:** 

![](imgs/1535286279(1).jpg)

```javascript
<!-- 头部 -->
<div class="header">
    <ul class="nav"></ul>
</div>

<!-- 主体部分 -->
<div class="main">
    <!-- 文章 -->
    <div class="article"></div>
    <!-- 侧边栏 -->
    <div class="aside"></div>
</div>

<!-- 底部 -->
<div class="footer">

</div>
```

**H5经典布局:**

![](imgs/1535286711(1).jpg)

```javascript
<!-- 头部 -->
<header>
    <ul class="nav"></ul>
</header>

<!-- 主体部分 -->
<div class="main">
    <!-- 文章 -->
    <article></article>
    <!-- 侧边栏 -->
    <aside></aside>
</div>

<!-- 底部 -->
<footer>

</footer>
```

#### H5中常用的新语义标签

##### 结构标签

- <nav> 表示导航
- <header> 表示页眉
- <footer> 表示页脚
- <section> 表示区块
- <article> 表示文章。如文章、评论、帖子、博客
- <aside> 表示侧边栏 如文章的侧栏
- <figure> 表示媒介内容分组。
- <mark> 表示标记 (用得少)
- <progress> 表示进度 (用得少)
- <time> 表示日期

本质上新语义标签与<div>、<span>没有区别，只是其具有表意性，使用时除了在HTML结构上需要注意外，其它和普通标签的使用无任何差别，
可以理解成<div class="nav"> 相当于<nav>。

##### 表单类型

- email 只能输入email格式。自动带有验证功能。
- tel 手机号码。
- url 只能输入url格式。
- number 只能输入数字。
- search 搜索框
- range 滑动条
- color 拾色器
- time	时间
- date 日期。
- datetime 时间日期
- month 月份
- week 星期

##### 表单属性

- placeholder 占位符（提示文字）
- autofocus 自动获取焦点
- multiple 文件上传多选或多个邮箱地址
- autocomplete 自动完成（填充的）。on 开启（默认），off 取消。用于表单元素，也可用于表单自身(on/off)
- form 指定表单项属于哪个form，处理复杂表单时会需要
- novalidate 关闭默认的验证功能（只能加给form）
- required 表示必填项
- pattern 自定义正则，验证表单。例如

##### 表单事件

- oninput()：用户输入内容时触发，可用于输入字数统计。

- oninvalid()：验证不通过时触发。比如，如果验证不通过时，想弹出一段提示文字，就可以用到它。


```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        * {
            padding: 0;
            margin: 0;
        }
        
        form {
            width: 600px;
            margin: 10px auto;
        }
        
        form > fieldset {
            padding: 10px 10px;
        }
        
        form > fieldset > meter,
        form > fieldset > input {
            width: 100%;
            height: 30px;
            margin: 8px 0;
            border: none;
            border: 1px solid #aaa;
            border-radius: 4px;
            font-size: 16px;
            padding-left: 5px;
            box-sizing: border-box; 
        }
        
        form > fieldset > meter {
            padding: 0;
        }
    
    </style>
</head>
<body>
<form action="">
    <fieldset>
        <legend>个人档案</legend>
        <label for="txt">姓名：</label>
        <input type="text" name="userName" id="txt" placeholder="请输入姓名" required>
        
        <label for="phone">手机号码：</label>
        <input type="tel" name="phone" id="phone" required
               pattern="^((13[0-9])|(14[5|7])|(15([0-3]|[5-9]))|(18[0,1,2,5-9])|(177))\\d{8}$">
        
        <label for="em">邮箱：</label>
        <input type="email" name="myemail" id="em" required>
        
        <label for="collage">学院：</label>
        <input type="text" name="collage" id="collage" list="dl" required>
        <datalist id="dl">
            <option value="A学院"></option>
            <option value="B学院"></option>
            <option value="C学院"></option>
            <option value="D学院"></option>
        </datalist>
        
        <label for="num">入学成绩：</label>
        <input type="number" name="num" id="num" required max="100" min="0" value="80" step="0.5">
        
        <label for="level">基础水平：</label>
        <meter id="level" max="100" min="0" high="90" low="59" value="80"></meter>
        
        <label for="edt">出生日期：</label>
        <input type="date" name="dt" id="edt" required>
        
        <input type="submit" id="sub">
    </fieldset>
</form>
<script>
    document.getElementById("phone").oninvalid = function () {
        this.setCustomValidity("请输入正确的手机号码");
    };
    document.getElementById("num").oninput = function () {
        document.getElementById("level").value = this.value;
    };
</script>
</body>
</html>

```

#### 其他功能标签
- mark：标注；

- progress：进度条；

<progress max="最大进度条的值" value="当前进度条的值">

- time：数据标签，给搜索引擎使用；

发布日期 <time datetime="2014-12-25T09:00">9：00</time>

更新日期 <time datetime="2015-01-23T04:00" pubdate>4:00</time>

- ruby和rt：对某一个字进行注释；

<ruby><rt>注释内容</rt><rp>浏览器不支持时如何显示</rp></ruby>

- wbr：软换行，页面宽度到需要换行时换行；

- canvas：使用JS代码做内容进行图像绘制；

- command：按钮；

- deteils ：展开菜单；

- dateilst：文本域下拉提示；

- keygen：加密


#### 媒体标签

- video：视频；
- audio：音频；
- embed：嵌入内容（包括各种媒体），Midi、Wav、AU、MP3、Flash、AIFF等。

```javascript
<!DOCTYPE html>
<html>
<head> 
    <meta charset="utf-8">
     
</head>
<body>

<audio src="./midea/music.mp3" controls="controls">
    Your browser does not support the audio element.
</audio>

<button onclick="playVid()" type="button">播放视频</button>
<button onclick="pauseVid()" type="button">暂停视频</button>
<br/>
<br/>

<video id="video1" width="320" height="240" controls>
    <source src="./midea/9.mp4" type="video/mp4">
    您的浏览器不支持 HTML5 video 标签。
</video>
<script>
    var myVideo = document.getElementById("video1");

    function playVid() {
        myVideo.play();
    }

    function pauseVid() {
        myVideo.pause();
    }
</script>
</html>

```

#### DOM操作

##### 获取元素
- document.querySelector("selector") 通过CSS选择器获取符合条件的第一个元素。
- document.querySelectorAll("selector") 通过CSS选择器获取符合条件的所有元素，以类数组形式存在。

##### 类名操作
- Node.classList.add("class") 添加class
- Node.classList.remove("class") 移除class
- Node.classList.toggle("class") 切换class，有则移除，无则添加
- Node.classList.contains("class") 检测是否存在class



##### 自定义属性
js 里可以通过 box1.index=100; box1.title 来自定义属性和获取属性。

H5可以直接在标签里添加自定义属性，但必须以 data- 开头。

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        
        
        .red {
            color: red;
        }
    
    </style>
</head>
<body>

<div style="margin: 0 auto;text-align: center">
    
    <label id="myname" for="txt" >姓名：</label>
    <button id="remove" >remove</button><button id="add">add</button><button id="toggle">toggle</button>
    <div class="box" title="盒子" data-my-name="smyhvae" data-content="我是一个div">div</div>
    
</div>

<script>
    
    document.getElementById("add").onclick = function(){
        if(document.querySelector("#myname").classList.contains("red")){
            alert("已经有了")
        }
        document.querySelector("#myname").classList.add("red");
    }

    document.getElementById("remove").onclick = function(){
        document.querySelector("#myname").classList.remove("red");
    }

    document.getElementById("toggle").onclick = function(){
        document.querySelector("#myname").classList.toggle("red");
    }

    var box = document.querySelector('.box');

    //自定义的属性 需要通过 dateset[]方式来获取
    console.log(box.dataset["content"]);  //打印结果：我是一个div
    console.log(box.dataset["myName"]);    //打印结果：smyhvae

    //设置自定义属性的值
    var num = 100;
    num.index = 10;
    box.index = 100;
    box.dataset["content"] = "aaaa";
    alert(box.dataset["content"]);
</script>
</body>
</html>

```
