# CSS选择器（一）

### 1、ID选择器

id 选择器可以为标有特定 id 的 HTML 元素指定特定的样式。
HTML元素以id属性来设置id选择器,CSS 中 id 选择器以 "#" 来定义。
以下的样式规则应用于元素属性 id="para1":
```html
<p id='sincw' class="center">i am sincw</p>
```
```css
#sincw
{
text-align:center;
color:red;
}
```

### 2、类选择器
class 选择器用于描述一组元素的样式，class 选择器有别于id选择器，class可以在多个元素中使用。
class 选择器在HTML中以class属性表示, 在 CSS 中，类选择器以一个点"."号显示：
在以下的例子中，所有拥有 center 类的 HTML 元素均为居中。
```html
<p class="center">i am sincw</p>
```
```css
.center {
text-align:center;
color:blue;
}
```


### 3、标签选择器
标签选择器用于描述一组元素的样式，标签选择器相似与于class 选择器。
在 CSS 中，标签选择器以标签显示：
在以下的例子中，所有 p 元素均为居中。
```html
<p class="center">i am sincw</p>
```
```css
p {
text-align:center;
color:green;
}
```

### 4、通配符选择器
```css
* {
margin: 0px;
padding: 0px;
}
```
特点：给所有的标签都使用相同的样式。 PS：★不推荐使用，增加浏览器和服务器负担。

### 5、复合选择器

#### 1、后代选择器: 定义的时候用空格隔开

```html
<div class="r-nav-top">
    <a href="">Hi~欢迎来到京东</a>
    <p>
        <a href="">登录</a>
        <a href="">注册</a>
    </p>
</div>
```
```css
.div a{
display: inline-block;
width: 100px;
height: 100px;
}
```

将Div下的所有的a标签的样式都改变


#### 2、交集选择器
```html
<p class="center">i am sincw</p>
```
```css
p.center {
text-align:center;
color:blue;
}
```

选择的元素要求同时满足两个条件：必须是p标签，然后必须是center类。主要要和后代选择器分开，交集选择器没有空格。


#### 3、并集选择器
```html
<p >i am sincw</p>
<span>i am sincw2</span>
<a class="center">i am sincw3</a>
```
```css
p,span,.center {
text-align:center;
color:blue;
}
```

将我们所需要设置样式的目标用，隔开。


#### 4.子代选择器，用符号`>`表示

> IE7开始兼容，IE6不兼容。

```css
div>p{
	color:red;
}
```
div的儿子p。和div的后代p的截然不同。

能够选择：

```html
	<div>
		<p>我是div的儿子</p>
	</div>
```

不能选择：

```html
	<div>
		<ul>
			<li>
				<p>我是div的重孙子</p>
			</li>
		</ul>
	</div>
```


#### 5.序选择器

> IE8开始兼容；IE6、7都不兼容

设置无序列表`<ul>`中的第一个`<li>`为红色：

```html
	<style type="text/css">
		ul li:first-child{
			color:red;
		}
	</style>
```

设置无序列表`<ul>`中的最后一个`<li>`为红色：

```css
		ul li:last-child{
			color:blue;
		}
```

#### 6.下一个兄弟选择器
> IE7开始兼容，IE6不兼容。

`+`表示选择下一个兄弟

```html
	<style type="text/css">
		h3+p{
			color:red;
		}
	</style>
```

上方的选择器意思是：选择的是h3元素后面紧挨着的第一个兄弟。不常用。

#### 7.兄弟选择器
> IE7开始兼容，IE6不兼容。

`+`表示选择下一个兄弟

```html
	<style type="text/css">
		h3~p{
			color:red;
		}
	</style>
```

上方的选择器意思是：选取了所有h3元素之后的所有相邻兄弟元素 <p>。不常用。


#### 8.属性选择器


下面的例子是把包含标题（title）的所有元素变为蓝色：
```html
<a href="" title="">sincw</a>
```
```css
a[title]
{ 
color:blue; 
}
```
下面的例子是把包含标题（title）并且title=sinw的所有元素变为蓝色：
```html
<a href="" title="sincw">sincw1</a>
<a href="" >sincw2</a>
```
```css
a[title='sincw']
{ 
color:blue; 
}
```
