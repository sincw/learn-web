#伪类和伪元素

###  伪类

**伪类**：CSS伪类(Pseudoclasses)是选择符的螺栓，用来指定一个或者与其相关的选择符的状态。伪类存在的意义是为了通过选择器找到那些不存在与DOM树中的信息以及不能被常规CSS选择器获取到的信息，伪类由一个冒号:开头，冒号后面是伪类的名称和包含在圆括号中的可选参数。


如果我想选择一个未被用户访问过的a标签，通过常规的CSS选择器我们无法明确的到我们想要的那一个，而伪类就对我们常规选择器筛选出的元素再次进行筛选。

#### 状态伪类

常见的状态伪类主要包括：

- :link 应用于未被访问过的链接；

- :hover 应用于鼠标悬停到的元素；

- :active 应用于被激活的元素；

- :visited 应用于被访问过的链接，与:link互斥。

- :focus 应用于拥有键盘输入焦点的元素。


#####  超链接的四种状态


a标签有4种伪类（即对应四种状态），要求背诵。如下：

- `:link`  	“链接”：超链接点击之前
- `:visited` “访问过的”：链接被访问过之后
- `:hover`	“悬停”：鼠标放到标签上的时候
- `:active`	“激活”： 鼠标点击标签，但是不松手时。
对应的代码如下：（带注释）

```
/*让超链接点击之前是红色*/
a:link{
    color:red;
}

/*让超链接点击之后是绿色*/
a:visited{
    color:orange;
}
/*鼠标悬停，放到标签上的时候*/
a:hover{
    color:green;
}
/*鼠标点击链接，但是不松手的时候*/
a:active{
    color:black;
```


PS:这四种状态必须按照固定的顺序写，在写`a:link`、`a:visited`这两个伪类的时候，要么同时写，要么同时不写。


##### 动态伪类

下面这三种动态伪类，针对所有标签都适用。

- `:hover` “悬停”：鼠标放到标签上的时候
- `:active`	“激活”： 鼠标点击标签，但是不松手时。
- `:focus` 是某个标签获得焦点时的样式（比如某个输入框获得焦点）

##### 表单相关伪类

- `:checked`　　匹配被选中的input元素，这个input元素包括radio和checkbox；
- `:disabled`　  匹配禁用的表单元素；
- `:enabled`　　匹配没有设置disabled属性的表单元素；
- `:valid　`　 　 匹配条件验证正确的表单元素；
- `:invalid`　　  与:valid相反，匹配条件验证错误的表单元素；

#### 结构化伪类

> :not　　　　　　否定伪类，用于匹配不符合参数选择器的元素；

```html
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>not选择器的使用</title>
<style type="text/css">
body *:not(h2){
	color:orange;
	font-family:"宋体";
	font-size:20px;
}
</style>
</head>
<body>
<h2>题李凝幽居</h2>
<p>闲居少邻并，草径入荒园。</p>
<p>鸟宿池边树，僧敲月下门。</p>
<p>过桥分野色，移石动云根。</p>
<p>暂去还来此，幽期不负言。</p>
</body>
</html>

```

![1](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/1533737534.jpg)

>  :first-child和 :last-child　

　匹配元素的第一个子元素，匹配元素的最后一个子元素；
```html
<!doctype html>
   <html>
   <head>
   <meta charset="utf-8">
   <title>first-child和last-child选择器的使用</title>
   <style type="text/css">
   p:first-child{
   	color:pink;
   	font-size:16px;
   	font-family:"宋体";
   }
   p:last-child{
   	color:blue;
   	font-size:16px;
   	font-family:"微软雅黑";
   }
   </style>
   </head>
   <body>
   <p>鲁山山行</p>
   <p>适与野情惬，千山高复低。</p>
   <p>好峰随处改，幽径独行迷。</p>
   <p>霜落熊升树，林空鹿饮溪。</p>
   <p>人家在何许？云外一声鸡。</p>
   </body>
   </html>
   ```

![1](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/1533737799.jpg)


> :first-of-type 和last-of-type　
 
 匹配属于其父元素的首个特定类型的子元素的每个元素；匹配元素的最后一个子元素；

```html
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>:targer选择器的使用</title>
<style type="text/css">
 .wrapper > p:last-of-type{
  background: orange;
}
.wrapper > p:first-of-type {
  background: orange;
}
</style>
</head>
<body>
<div class="wrapper">
  <p>我是第一个段落</p>
  <p>我是第二个段落</p>
  <p>我是第三个段落</p>
  <div>我是第一个Div元素</div>
  <div>我是第二个Div元素</div>
  <div>我是第三个Div元素</div>
</div>
</body>
</html>
```
![1](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/1533738452.jpg)


> :nth-child(n)　和 :nth-last-child(n)　  

:nth-child根据元素的位置匹配一个或者多个元素，它接受一个an+b形式的参数（an+b最大数为匹配元素的个数）；　　:nth-last-child与:nth-child相似，不同之处在于它是从最后一个子元素开始计数的；

```html
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>nth-child(n)和nth-last-child(n)选择器的使用</title>
<style type="text/css">
p:nth-child(2){
	color:pink;
	font-size:16px;
	font-family:"宋体";
}
p:nth-last-child(2){
	color:blue;
	font-size:16px;
	font-family:"微软雅黑";
}
</style>
</head>
<body>
<p>梅花</p>
<p>数萼初含雪，孤标画本难。</p>
<p>香中别有韵，清极不知寒。</p>
<p>横笛和愁听，斜枝倚病看。</p>
<p>朔风如解意，容易莫摧残。</p>
</body>
</html>

```
![1](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/1533737974.jpg)


> :nth-of-type和:nth-last-type　 
  
  :nth-of-type与nth-child相似，不同之处在于它是只匹配特定类型的元素；nth-last-of-type与nth-of-type相似，不同之处在于它是从最后一个子元素开始计数的；
```html
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>nth-of-type(n)和nth-last-of-type(n)选择器</title>
<style type="text/css">
h2:nth-of-type(odd){color:#f09;}
h2:nth-of-type(even){color:#12ff65;}
p:nth-last-of-type(2){font-weight:bold;}
</style>
</head>
<body>
<h2>李白</h2>
<p>李白（701年－762年） ，字太白，号青莲居士，又号“谪仙人”，是唐代伟大的浪漫主义诗人，被后人誉为“诗仙”。</p>
<h2>杜甫</h2>
<p>杜甫（712年—770年），字子美，汉族，本襄阳人，后徙河南巩县。自号少陵野老，唐代伟大的现实主义诗人。</p>
<h2>李商隐</h2>
<p>李商隐（约813年-约858年），字义山，号玉溪（谿）生，又号樊南生，祖籍怀州河内（今河南焦作沁阳），出生于郑州荥阳（今河南郑州荥阳市），晚唐著名诗人。</p>
<h2>温庭筠</h2>
<p>温庭筠（约812年-约866年），本名岐，艺名庭筠，字飞卿，男，汉族，唐代并州祁县（今山西省晋中市祁县）人，晚唐时期诗人、词人。</p>
</body>
</html>

```
![1](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/1533738078.jpg)


> :only-child　　    当元素是其父元素中唯一一个子元素时，:only-child匹配该元素；
```html
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>only-child选择器的使用</title>
<style type="text/css">
li:only-child{color:red;}
</style>
</head>
<body>
	<div>
    	国内电影：
    	<ul>
        	<li>一代宗师</li>
            <li>叶问</li>
            <li>非诚勿扰</li>
        </ul>
        美国电影：
        <ul>
        	<li>侏罗纪世界</li>
        </ul>
        日本动漫：
        <ul>
        	<li>蜡笔小新</li>
            <li>火影忍者</li>
            <li>航海王</li>
        </ul>
    </div>
</body>
</html>
```

![1](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/1533737673.jpg)

>  :target　　　　　  当URL带有锚名称，指向文档内某个具体的元素时，:target匹配该元素；
```html
<!doctype html>
<html>
<head>
<meta charset="utf-8">
<title>:targer选择器的使用</title>
<style type="text/css">
:target{background-color:#e5eecc;}
</style>
</head>
<body>
<h1>这是标题</h1>
<p><a href="#news1">跳转内容 1</a></p>
<p><a href="#news2">跳转内容 2</a></p>
<p>请单击上面的链接，:target选择器会突出显示当前活动的HTML锚。</p>
<p id="news1"><b>内容 1...</b></p>
<p id="news2"><b>内容 2...</b></p>
</body>
</html>
```
![1](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/1533738138.jpg)


### 伪元素

实际上来说，CSS 中的伪元素在HTML上是不存在的，使用的时机通常都是针对某样元素特殊处理时才会用到，使用：：老将伪类和伪元素分开

常用的 伪元素有：
- ::first-line
可以指定 p 元素第一行的样式
- ::first-letter
可以指定 p 元素第一个字的样式
- ::selection
定义使用者反白后的效果
- ::before
在元素之前插入内容
- ::after
在元素之后插入内容

```html
<!doctype html>
<html>
<head>
    <meta charset="utf-8">
    <title>:targer选择器的使用</title>
    <style type="text/css">
        /* 第一行樣式 */
        p::first-line {
            color: red;
        }
        /* 開頭第一個字樣式 */
        p::first-letter {
            font-size: 30px;
        }
        div::selection {
            background: red;
            color: #FFF;
        }

        .wrapper div:last-child::before {
            content: ' hi ';
        }

        .wrapper div:last-child::after {
            content: ' bye ';
        }
    </style>
</head>
<body>
<div class="wrapper">
    <p>我是第一个段落1111111111111111111111111111111111111111111111111111</p>
    <p>我是第二个段落</p>
    <p>我是第三个段落</p>
    <div>我是第一个Div元素</div>
    <div>我是第二个Div元素</div>
    <div>我是第三个Div元素</div>
</div>
</body>
</html>
```

![1](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/1533739228.jpg)
