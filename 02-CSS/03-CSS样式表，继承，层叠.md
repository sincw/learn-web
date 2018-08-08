#CSS选择器（二）

### 1、继承
```html
<p>i am <span>sincw</span></p>
```

```css
p{
color: red;
}
```
p标签中的所有文字都是红色，表示span继承了p的color.

####  常见可继承性的属性

##### 1.字体
- font：组合字体

- font-family：规定元素的字体系列

- font-weight：设置字体的粗细

- font-size：设置字体的尺寸

- font-style：定义字体的风格

##### 2、文本

- text-indent：文本缩进

- text-align：文本水平对齐

- line-height：行高

- word-spacing：增加或减少单词间的空白（即字间隔）

- letter-spacing：增加或减少字符间的空白（字符间距）

- text-transform：控制文本大小写

- direction：规定文本的书写方向

- color：文本颜色

### 2.样式优先级别

#### 插入样式表的三种方法

> 外部样式表
```css
<link rel="stylesheet" type="text/css" href="mystyle.css">
```

>内部样式表
```css
<head> <style> hr {color:sienna;} p {margin-left:20px;} body {background-image:url("images/back40.gif");} </style> </head>
```

>内联样式
```css
<p style="color:sienna;margin-left:20px">这是一个段落。</p>
```

>多重样式

如果某些属性在不同的样式表中被同样的选择器定义，那么属性值将从更具体的样式表中被继承过来。


#####  样式层叠次序 优先级逐级增加
- 浏览器缺省设置
- 外部样式表
- 内部样式表（位于 head 标签内部）
- 内联样式（在 HTML 元素内部）

同一个样式表中，相同优先级，后出现的会覆盖先出现的。

### 3、权值计算
![](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/qzjs.jpg)

![](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/qzjs2.jpg)


高级别选择器会覆盖低级别选择器的样式（不论加载样式次序）

下面是一个简单的例子

![](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/cssshili11.jpg)

![](https://raw.githubusercontent.com/sincw/learn-web/master/img/02/cssshili22.jpg)

!important 规则
该样式声明会覆盖CSS中任何其他的声明
不推荐频繁使用，因为它打乱了级联规则，在样式复杂的网站中，会难以调试。


