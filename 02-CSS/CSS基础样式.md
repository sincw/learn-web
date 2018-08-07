#CSS基础样式


### 一、字体



#### 1、属性

```css
font-size: 50px;         /*文字大小*/
font-weight: 700;       /*值从100-900，文字粗细,700约等于Bold，不推荐使用font-weight:bold; */
font-family:微软雅黑;    /*文本的字体*/
font-style: normal | italic;  /*normal:默认值  italic:斜体*/
line-height: 50px            /*行高*/
/* 连写 font属性连写至少要有**字号和字体**，否则连写是不生效的*/
/* 格式：font: font-style font-weight  font-size/line-height  font-family; */
font: italic 700 50px/40px  微软雅黑;
```

#### 2、字体属性的说明
（1）为了防止用户电脑里，没有微软雅黑这个字体。就要用英语的逗号，隔开备选字体。如下：（可以备选多个）

```
	font-family: "微软雅黑","宋体";
```

上方代码表示：如果用户电脑里没有安装微软雅黑字体，那么就是宋体。


（2）我们须将英语字体放在最前面，这样所有的中文，就不能匹配英语字体，就自动的变为后面的中文字体：

```
	font-family: "Times New Roman","微软雅黑","宋体";
```

上方代码的意思是，英文会采用Times New Roman字体，而中文会采用微软雅黑字体（因为美国人设计的Times New Roman字体并不针对中文，所以中文会采用后面的微软雅黑）。比如说，对于`smyhvae哈哈哈`这段文字，`smyhvae`会采用Times New Roman字体，而`哈哈哈`会采用微软雅黑字体。

可是，如果我们把中文字体写在前面：(错误写法)

```
	font-family: "微软雅黑","Times New Roman","宋体";
```

上方代码会导致，中文和英文都会采用微软雅黑字体。

（3）所有的中文字体，都有英语别名。

微软雅黑的英语别名：

```
	font-family: "Microsoft YaHei";
```

宋体的英语别名：

```
	font-family: "SimSun";
```

当我们把字号、行高、字体这三个属性合二为一时，也可以写成：

```
	font:12px/30px  "Times New Roman","Microsoft YaHei","SimSun";
```



> 注意：font:后边写属性的值。一定按照书写顺序。

### 二、文本属性

CSS样式中，我们常用的文本属性有以下几种：

 - `letter-spacing: 0.5cm ;`  单个字母之间的间距
 - `word-spacing: 1cm;`   单词之间的间距
 - `text-decoration: none;` 字体修饰：none去掉下划线、**underline下划线**、line-through中划线、overline上划线、
 - `text-transform: lowercase;`  单词字体大小写。uppercase大写、lowercase小写
 - `color:red;` 字体颜色
 - `text-align: center;` 在当前容器中的对齐方式。属性值可以是：left、right、center（<font color="#0000FF">**在当前容器的中间**</font>）、justify
 - `text-transform: lowercase;` 单词的字体大小写。属性值可以是：`uppercase`（单词大写）、`lowercase`（单词小写）、`capitalize`（每个单词的首字母大写）

下面是所有的文本属性

![]((https://raw.githubusercontent.com/sincw/learn-web/master/img/02/css-textField.jpg))

### 三、背景
```css
background-color：    /*背景颜色*/
background-image：    /*背景图片*/
Background-repeat：    repeat(默认)  |  no-repeat |   repeat-x   |  repeat-y     /*背景平铺*/
Background-position：  left  |  right  |  center（默认）  |  top  | bottom  /*背景定位*/
Background-attachment:   scroll（默认）  |  fixed   /*背景是否滚动*/
```

- background-position

>`background-position: right;` // 方位值只写一个的时候，另外一个值默认居中。
>`background-position: right bottom` // 写2个方位值的时候，顺序没有要求  
>`background-position: 20px 30px` //写2个具体值的时候，第一个值代表水平方向，第二个值代表垂直方向,可以是百分比

- Background-attachment 

> `scroll`: 背景图的位置是基于盒子（假如是div）的范围进行显示
>`fixed`：背景图的位置是基于整个浏览器body的范围进行显示，如果背景图定义在div里面，而显示的位置在浏览器范围内但是不在div的范围内的话，背景图无法显示。



- 背景属性连写

```css
background: red url("1.png") no-repeat 30px 40px scroll;
```

> PS：连写的时候没有顺序要求，url为必写项


### 四、边距
![]((https://raw.githubusercontent.com/sincw/learn-web/master/img/02/box-model.jpg))

####border
```css
Border-top-style:  solid   /*实线*/
dotted  /*点线*/
dashed  /*虚线*/
none /*无边框*/
Border-top-color   /*边框颜色*/
Border-top-width   /*边框粗细*/
```

> 除了有`top`系列外还有`left,right,bottom`系列

- 边框属性的连写

```css
border-top: 1px solid #fff;
```

> 没有顺序要求，线型为必写项

- 四个边框值相同的写法

```css
border: 1px solid #fff;
```

> PS: 没有顺序要求，线型为必写项



- 边框合并（细线边框）

```css
border-collapse:collapse;
```

####padding（内边距）

```css
padding-left   |   right    |  top  |  bottom
```

- padding连写

```css
Padding: 20px;   /*上右下左内边距都是20px*/
Padding: 20px 30px;   /*上下20px   左右30px*/
Padding: 20px  30px  40px;  /* 上内边距为20px  左右内边距为30px   下内边距为40px*/
Padding: 20px  30px   40px  50px;   /*上20px 右30px  下40px  左  50px*/
```



- 内边距撑大盒子的问题

> 盒子的宽度 = 定义的宽度 + 边框宽度 + 左右内边距

- 继承的盒子一般不会被撑大

> 包含（嵌套）的盒子，~~如果子盒子没有定义宽度~~，给子盒子设置左右内边距（内边距不大于子盒子宽度），不会撑大子盒子。至于设置了上下内边距的话是会撑大子盒子的。（不管怎样父盒子永不变）



####margin（外边距）

```
margin-left   | right  |  top  |  bottom
```

- 外边距连写

```css
margin: 20px;    /*上下左右外边距20PX*/
margin: 20px 30px;   /*上下20px  左右30px*/
margin: 20px  30px  40px;     /*上20px  左右30px   下40px*/
margin: 20px  30px   40px  50px; /*上20px   右30px   下40px  左50px*/
```
>注意: 
`margin: 0 auto;` 盒子居中对齐 
`text-align:center` 是盒子里面的内容居中


- 垂直方向外边距合并（取最大值）

> 两个盒子垂直布局，一个设置上外边距，一个设置下外边距，取的设置较大的值，而不是相加。



### 五、布局

如果你只想把所有内容都塞进一栏里，那么不用设置任何布局也是OK的。然而，如果用户把浏览器窗口调整的很大，这时阅读网页会非常难受：读完每一行之后，你的视觉焦点要从右到左移动一大段距离。试着调整下浏览器窗口大小你就明白我的意思了！
在解决这个问题之前，我们需要了解一个很重要的属性： display

display 是CSS中最重要的用于控制布局的属性。每个元素都有一个默认的 display 值，这与元素的类型有关。对于大多数元素它们的默认值通常是 block 或 inline 。一个 block 元素通常被叫做块级元素。一个 inline 元素通常被叫做行内元素。

####block
```html
<div class="elem">
  <span class="label">&lt;div&gt;</span>
  <p>
     <code>div</code> 是一个标准的块级元素。一个块级元素会新开始一行并且尽可能撑满容器。其他常用的块级元素包括 <code>p</code> 、 <code>form</code> 和HTML5中的新元素： <code>header</code> 、 <code>footer</code> 、 <code>section</code> 等等。
  </p>
  <span class="endlabel">&lt;/div&gt;</span>
</div>
```

####inline
span 是一个标准的行内元素。一个行内元素可以在段落中 <span> 像这样 </span> 包裹一些文字而不会打乱段落的布局。 a 元素是最常用的行内元素，它可以被用作链接。
```html
<span class="elem elem-inline">像这样</span>
```

####none
另一个常用的display值是 none 。一些特殊元素的默认 display 值是它，例如 script 。 display:none 通常被 JavaScript 用来在不删除元素的情况下隐藏或显示元素。

它和 visibility 属性不一样。把 display 设置成 none 元素不会占据它本来应该显示的空间，但是设置成 visibility: hidden; 还会占据空间。


####inline-block
简单来说就是将对象呈现为inline对象，但是对象的内容作为block对象呈现。之后的内联对象会被排列在同一行内。比如我们可以给一个link（a元素）inline-block属性值，使其既具有block的宽度高度特性又具有inline的同行特性。
```css
.copyright_auth a {
    display: inline-block;
    width: 100px;
    height: 100px;
}
```

####最后
以上是我们常用的4中状态，通过他们之间相互转换，我们可以做出很多特殊的布局，还有更多的状态大家可以自行查阅。
