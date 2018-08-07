#  CSS定位和浮动

##   CSS定位
CSS的定位属性有三种，分别是绝对定位、相对定位、固定定位。

```
position: static;  <!-- 默认定位 -->

position: absolute;  <!-- 绝对定位 -->

position: relative;  <!-- 相对定位 -->

position: fixed;     <!-- 固定定位 -->

```

### 1、相对定位


**相对定位**：让元素相对于自己原来的位置，进行位置调整（可用于盒子的位置微调）。

我们之前学习的背景属性中，是通过如下格式：

```
	background-position:向右偏移量 向下偏移量;
```

但这回的定位属性，是通过如下格式：

```
	position: relative;
	left: 50px;
	top: 50px;
```

相对定位的举例：

```html
<!doctype html>
<html lang="en">
 <head>
  <meta charset="UTF-8">
  <meta name="Generator" content="EditPlus®">
  <meta name="Author" content="">
  <meta name="Keywords" content="">
  <meta name="Description" content="">
  <title>相对定位</title>
	<style type="text/css">
		body{
			margin: 0px;
		}
		.div1{
			width: 200px;
			height: 200px;
			border: 1px solid red;
		}
		.div2{
			position: relative;/*相对定位：相对于自己原来的位置*/
			left: 50px;/*横坐标：正值表示向右偏移，负值表示向左偏移*/
			top: 50px;/*纵坐标：正值表示向下偏移，负值表示向上偏移*/
			width: 200px;
			height: 200px;
			border: 1px solid blue;
		}
	</style>
 </head>

 <body>
	<div class="div1">我是A</div>
	<div class="div2">我是B</div>
 </body>

</html>
```

效果如下:
![](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/relative-pos.jpg)


#### 相对定位不脱标

**相对定位**：不脱标，老家留坑，**别人不会把它的位置挤走**。

也就是说，相对定位的真实位置还在老家，只不过影子出去了，可以到处飘。

#### 相对定位的用途

相对定位有坑，所以如果需要做一般不用于做“压盖”效果（把一个div放到另一个div之上）。页面中，效果极小。就两个作用：

- （1）微调元素
- （2）做绝对定位的参考，子绝父相

#### 相对定位的定位值

- left：盒子右移

- right：盒子左移

- top：盒子下移

- bottom：盒子上移

PS：负数表示相反的方向。

###  2、绝对定位
**绝对定位**：定义横纵坐标。原点在父容器的左上角或左下角。横坐标用left表示，纵坐标用top或者bottom表示。

格式举例如下：

```
	position: absolute;  /*绝对定位*/
	left: 10px;  /*横坐标*/
	top/bottom: 20px;  /*纵坐标*/
```

#### 绝对定位脱标

**绝对定位的盒子脱离了标准文档流。**

所以，所有的标准文档流的性质，绝对定位之后都不遵守了。

绝对定位之后，标签就不区分所谓的行内元素、块级元素了，不需要`display:block`就可以设置宽、高了。

#### 绝对定位的参考点（重要）

（1）如果用**top描述**，那么参考点就是**页面的左上角**，而不是浏览器的左上角：

![](http://raw.githubusercontent.com/sincw/learn-web/master/img/02/20180807_2120.png)

（2）如果用**bottom描述**，那么参考点就是**浏览器首屏窗口尺寸**（好好理解“首屏”二字），对应的页面的左下角：

![](http://raw.githubusercontent.com/sincw/learn-web/master/img/02/20180807_2121.png)

> 常见应用

“**子绝父相**”
这样可以保证父亲没有脱标，儿子脱标在父亲的范围里面移动。于是经常这样做：
父亲设置相对定位（零偏移），然后让儿子绝对定位一定的距离。

![](http://raw.githubusercontent.com/sincw/learn-web/master/img/02/prsa.jpg)

```html
                <div class="r-nav-top">
                    <div class="r-nav-logo">
                        <img src="//misc.360buyimg.com/mtd/pc/common/img/no_login.jpg">
                    </div>
                    <h5>Hi~欢迎来到京东</h5>
                    <p>
                        <a href="">登录</a>
                        <a href="">注册</a>
                    </p>
                    <p>
                        <a href="" class="btn">新人福利</a>
                        <a href="" class="btn2">PLUS会员</a>
                    </p>
                </div>
```

```css
.r-nav .r-nav-top {
    position: relative;
    padding-top: 62px;
    height: 78px;
    text-align: center;
}


.r-nav-logo {
    position: absolute;
    top: -10px;
    left: 50%;
    margin-left: -34px;
    border: 5px solid #e4e2e1;
    border-radius: 50%;
}

.r-nav-logo img {
    display: block;
    width: 55px;
    height: 55px;
    border-radius: 50%;
    overflow: hidden;
    -webkit-box-shadow: 3px 6px 25px #c3c3c3;
    -moz-box-shadow: 3px 6px 25px #c3c3c3;
    box-shadow: 3px 6px 25px #c3c3c3;
}

```

###  3、固定定位

**固定定位**：就是相对浏览器窗口进行定位。无论页面如何滚动，这个盒子显示的位置不变。

备注：IE6不兼容。

**用途1**：网页右下角的“返回到顶部”

比如我们经常看到的网页右下角显示的“返回到顶部”，就可以固定定位。

```html
	<style type="text/css">
		.top{
			position: fixed;
			bottom: 100px;
			right: 30px;
			width: 60px;
			height: 60px;
			background-color: red;
			text-align: center;
			line-height:30px;
			color:white;
			text-decoration: none;   
		}
	</style>
```

**用途2：**顶部导航条

我们经常能看到固定在网页顶端的导航条，可以用固定定位来做。
覆盖，我们要给body标签设置60px的padding-top。


### 4、z-index属性：

**z-index**属性：表示谁压着谁。数值大的压盖住数值小的。

有如下特性：

 （1）属性值大的位于上层，属性值小的位于下层。

 （2）z-index值没有单位，就是一个正整数。默认的z-index值是0。

 （3）如果大家都没有z-index值，或者z-index值一样，那么在HTML代码里写在后面，谁就在上面能压住别人。定位了的元素，永远能够压住没有定位的元素。


##   CSS浮动


### 1、文档流（标准流）

元素自上而下，自左而右，块元素独占一行，行内元素在一行上显示，碰到父集元素的边框换行。



### 2、浮动布局

```css
float:  left   |   right /*浮动方向*/
```

> **特点：**
> 1.元素浮动之后不占据原来的位置（脱标）
> 2.浮动的盒子在一行上显示
> *3.行内元素浮动之后自动转换为行内块元素。*（不推荐使用，转行内元素最好使用`display: inline-block;`）



### 3、浮动的作用

-  文本绕图

![](http://raw.githubusercontent.com/sincw/learn-web/master/img/02/float1.png)



- 制作导航（经常使用）

> 把无序列表 ul li 浮动起来做成的导航。

![](http://raw.githubusercontent.com/sincw/learn-web/master/img/02/douban.jpg)


- 网页布局

![](http://raw.githubusercontent.com/sincw/learn-web/master/img/02/jd-layout.jpg)



### 4、清除浮动
清除浮动不是不用浮动，清除浮动产生的问题。
> 问题：当父盒子没有定义高度，嵌套的盒子浮动之后，下边的元素发生位置错误（占据父盒子的位置）。



#### 方法一

给浮动元素的父集元素使用`overflow:hidden;`创建BFC 块级格式上下文

> 注意：如果有内容出了盒子，不能使用这个方法。



#### 方法二（推荐使用）

伪元素清除浮动。

```css
.clearfix:after {
    content: '';
    height: 0;
    display: block;
    clear: both;
}
```
> : after 相当于在当前盒子后加了一个盒子。
