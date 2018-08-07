# 表格和表单

### 表格

#### 1、标准结构

```html
<table>
    <caption>日常消费</caption>
    <thead>表头
    <tr>
        <th>项目</th>
        <th>支出</th>
    </tr>
    </thead>
    <tbody>
    <tr>
        <td>聚餐</td>
        <td>200元</td>
    </tr>
    </tbody>
    <tfoot>
    <tr>
        <td>Sum</td>
        <td>$180</td>
    </tr>
    </tfoot>
</table>
```

> 写 `<thead> <tbody> <tfoot>`对SEO更好。 
>width（宽度）
>height（高度）
>border（边框宽度） 
>cellspacing（单元格与单元格的距离）
>cellpadding（内容距边框的距离）
>bgcolor（表格背景颜色）
>align=”left | right | center”
>​如果直接给表格用align=”center” 表格居中
>​如果给tr或者td使用 ，tr或者td内容居中。 
>cellpadding：单元格内容到边的距离，像素为单位。默认情况下，文字是紧挨着左边那条线的，即默认情况下的值为0。 注意不是单元格内容到四条边的距离哈，而是到一条边的距离，默认是与左边那条线的距离。如果设置属性dir="rtl"，那就指的是内容到右边那条线的距离。
>cellspacing：单元格和单元格之间的距离（外边距），像素为单位。默认情况下的值为0


#### 2、单元格合并

`<td colspan=“2”>填写内容</td>`：合并同一行的单元格，合并行数为2 

`<td rowspan=“3”>填写内容</td>` ：合并同一列的单元格，合并列数为3 

```html
<table border="2" cellspacing="0" width="400" height="100" align="center">
	<caption><strong>表头</strong></caption>
		<tr align="center" bgcolor="yellow" height="100">
			<td colspan="2">一二三四五六</td>
			<!-- <td><strong>2</strong></td> -->
			<td>一二三四五六</td>
		</tr>

		<tr align="center" bgcolor="#CCC" height="100">
			<td>一二三四五六</td>
			<td>一二三四五六</td>
			<td rowspan="2">一二三四五六</td>
		</tr>

		<tr align="center" bgcolor="#CCC" height="100">
			<td>一二三四五六</td>
			<td>一二三四五六</td>
		</tr>
	</table>
```
### 表单标签

表单标签用`<form>`表示，用于与服务器的交互。表单就是收集用户信息的，就是让用户填写的、选择的。


**属性：**
 - `name`：表单的名称，用于JS来操作或控制表单时使用；
 - `id`：表单的名称，用于JS来操作或控制表单时使用；
 - `action`：指定表单数据的处理程序，一般是PHP，如：action=“login.php”
 - `method`：表单数据的提交方式，一般取值：get(默认)和post

注意：表单和表格嵌套时，是在<form>标记中套<table>标记。

form标签里面的action属性和method属性，在《Ajax》课程上给大家讲解。稍微说一下：action属性就是表示，表单将提交到哪里。 method属性表示用什么HTTP方法提交，有get、post两种。


**get提交和post提交的区别：**

GET方式：
将表单数据，以"name=value"形式追加到action指定的处理程序的后面，两者间用"?"隔开，每一个表单的"name=value"间用"&"号隔开。
特点：只适合提交少量信息，并且不太安全(不要提交敏感数据)、提交的数据类型只限于ASCII字符。

POST方式：
将表单数据直接发送(隐藏)到action指定的处理程序。POST发送的数据不可见。Action指定的处理程序可以获取到表单数据。
特点：可以提交海量信息，相对来说安全一些，提交的数据格式是多样的(Word、Excel、rar、img)。

**Enctype：**
表单数据的编码方式(加密方式)，取值可以是：application/x-www-form-urlencoded、multipart/form-data。Enctype只能在POST方式下使用。
 - Application/x-www-form-urlencoded：**默认**加密方式，除了上传文件之外的数据都可以
 - Multipart/form-data：**上传附件时，必须使用这种编码方式**。



### 1、`<input>`：输入标签（文本框）

用于接收用户输入。

```html
<input type="text" />
```


**属性：**

- **`type="属性值"`**：文本类型。属性值可以是：
	- `text`（默认）
	- `password`：密码类型
	- `radio`：单选按钮，名字相同的按钮作为一组进行单选（单选按钮，天生是不能互斥的，如果想互斥，必须要有相同的name属性。name就是“名字”。
）。非常像以前的收音机，按下去一个按钮，其他的就抬起来了。所以叫做radio。
	- `checkbox`：多选按钮，名字相同的按钮作为一组进行选择。
	- `checked`：将单选按钮或多选按钮默认处于选中状态。当`<input>`标签的`type="radio"`时，可以用这个属性。属性值也是checked，可以省略。
	- `hidden`：隐藏框，在表单中包含不希望用户看见的信息
	- `button`：普通按钮，结合js代码进行使用。
	- `submit`：提交按钮，传送当前表单的数据给服务器或其他程序处理。这个按钮不需要写value自动就会有“提交”文字。这个按钮真的有提交功能。点击按钮后，这个表单就会被提交到form标签的action属性中指定的那个页面中去。
	- `reset`：重置按钮，清空当前表单的内容，并设置为最初的默认值
	- `image`：图片按钮，和提交按钮的功能完全一致，只不过图片按钮可以显示图片。
	- `file`：文件选择框。
提示：如果要限制上传文件的类型，需要配合JS来实现验证。对上传文件的安全检查：一是扩展名的检查，二是文件数据内容的检查。

 - **`value="内容"`**：文本框里的默认内容（已经被填好了的）
 - `size="50"`：表示文本框内可以显示**五十个字符**。一个英文或一个中文都算一个字符。
注意**size属性值的单位不是像素哦**。
 - `readonly`：文本框只读，不能编辑。因为它的属性值也是readonly，所以属性值可以不写。
用了这个属性之后，在google浏览器中，光标点不进去；在IE浏览器中，光标可以点进去，但是文字不能编辑。
 - `disabled`：文本框只读，不能编辑，光标点不进去。属性值可以不写。

> 备注：HTML5中，input的类型又增加了很多（比如date、color，但是都不兼容，所以我们是在专门的HTML5课程中学）。


举例：

```html
	<form>
		姓名：<input value="1" >sincw<br>
		昵称：<input value="2" readonly=""><br>
		名字：<input type="text" value="name" disabled=""><br>
		密码：<input type="password" value="pwd" size="50"><br>
		性别：<input type="radio" name="gender" value="male" checked="">男
			  <input type="radio" name="gender" value="female" >女<br>
		爱好：<input type="checkbox" name="love" value="eat">吃饭
			  <input type="checkbox" name="love" value="sleep">睡觉
			  <input type="checkbox" name="love" value="bat">写代码
	</form>
```

四种按钮的举例：

```html
	<form>
		<input type="button" value="普通按钮"><br>
		<input type="submit"  value="提交按钮"><br>
		<input type="reset" value="重置按钮"><br>
		<input type="image" value="图片按钮1"><br>
		<input type="image" src="1.jpg" width="800" value="图片按钮2"><br>
		<input type="file" value="文件选择框">
	</form>
```

**前端开发工程师，只需要关心页面的美、样式、板式、交互。至于数据的保存、读取，都是后台工程师做的事情。**


#### 2、`<select>`：下拉列表标签

`<select>`标签里面的每一项用`<option>`表示。select就是“选择”，option“选项”。

select标签和ul、ol、dl一样，都是组标签。

**`<select>`标签的属性：**

- `multiple`：可以对下拉列表中的选项进行多选。没有属性值。
- `size="3"`：如果属性值大于1，则列表为滚动视图。默认属性值为1，即下拉视图。

**`<option>`标签的属性：**

 - `selected`：预选中。没有属性值。

举例：

```html
	<form>
		<select>
			<option>A</option>
			<option>B</option>
			<option>C</option>
			<option>D</option>
			<option selected="">E</option>
		</select>
		<br><br><br>

		<select size="3">
			<option>A</option>
			<option>B</option>
			<option>C</option>
			<option>D</option>
			<option>E</option>
		</select>
		<br><br><br>

		<select multiple="">
			<option>A</option>
			<option>B</option>
			<option selected="">C</option>
			<option selected="">D</option>
			<option>E</option>
		</select>
		<br><br><br>

	</form>
```

#### 3、`<textare>`标签：多行文本输入框

text就是“文本”，area就是“区域”。


**属性：**

 - `value`：提交给服务器的值。
 - `rows="4"`：指定文本区域的行数。
 - `cols="20"`：指定文本区域的列数。
 - `readonly`：只读。

举例：

```html
	<form>
		<textarea name="txtInfo" rows="4" cols="20">1、不爱摄影不懂设计的程序猿不是一个好的产品经理。</textarea>
	</form>
```

上方代码解释：textarea这个标签，是个标签对儿。对儿里面不用写东西。如果写的话，就是这个框的默认文字。


上图的红框部分表示，我在文本区域进行了换行，所以显示的效果也出现了空白。

####  4、表单的语义化-[重要]

比如，我们在注册一个网站的信息的时候，有一部分是必填信息，有一部分是选填信息，这个时候可以利用表单的语义化。
举例：

```html
	<form>

		<fieldset>
		<legend>账号信息</legend>
		姓名：<input value="呵呵" >逗比<br>
		密码：<input type="password" value="pwd" size="50"><br>
		</fieldset>

		<fieldset>
		<legend>其他信息</legend>
		性别：<input type="radio" name="gender" value="male" checked="">男
			  <input type="radio" name="gender" value="female" >女<br>
		爱好：<input type="checkbox" name="love" value="eat">吃饭
			  <input type="checkbox" name="love" value="sleep">睡觉
			  <input type="checkbox" name="love" value="bat">打豆豆
		</fieldset>

	</form>
```

####  5、`<label>`标签

我们先来看下面一段代码：

```html
<input type="radio" name="sex" /> 男
<input type="radio" name="sex" /> 女

```

对于上面这样的单选框，我们只有点击那个单选框（小圆圈）才可以选中，点击“男”、“女”这两个文字时是无法选中的；于是，label标签派上了用场。

本质上来讲，“男”、“女”这两个文字和input标签时没有关系的，而label就是解决这个问题的。我们可以通过label把input和汉字包裹起来作为整体。

解决方法如下：

```html
<input type="radio" name="sex" id="nan" /> <label for="nan">男</label>
<input type="radio" name="sex" id="nv"  /> <label for="nv">女</label>
```

上方代码中，input元素要有一个id，然后label标签有一个for属性，和id相同，那么这个label和input就有绑定关系了。


当然了，复选框也有label：（任何表单元素都有label）

```html
<input type="checkbox" id="kk" />
<label for="kk">10天内免登陆</label>
```


### 列表标签

列表标签分为三种。

#### 1、无序列表`<ul>`，无序列表中的每一项是`<li>`

英文单词解释如下：

- ul：unordered list，“无序列表”的意思。
- li：list item，“列表项”的意思。

例如：

```html
<ul>
	<li>默认1</li>
	<li>默认2</li>
	<li>默认3</li>
</ul>
```

注意：

- li不能单独存在，必须包裹在ul里面；反过来说，ul的“儿子”不能是别的东西，只能有li。
- 我们这里再次强调，ul的作用，并不是给文字增加小圆点的，而是增加无序列表的“语义”的。



**属性：**

 - `type="属性值"`。属性值可以选： `disc`(实心原点，默认)，`square`(实心方点)，`circle`(空心圆)。


### 2、有序列表`<OL>`，里面的每一项是`<li>`

英文单词：Ordered List。

例如：

```html
<ol >
	<li>呵呵哒1</li>
	<li>呵呵哒2</li>
	<li>呵呵哒3</li>
</ol>
```
**属性：**
 - `type="属性值"`。属性值可以是：1(阿拉伯数字，默认)、a、A、i、I。结合`start`属性表示`从几开始`。


ol和ul就是语义不一样，怎么使用都是一样的。
ol里面只能有li，li必须被ol包裹。li是容器级。

ol这个东西用的不多，如果想表达顺序，一般也用ul。举例如下：

```html
<ul>
	<li>1. 小苹果</li>
	<li>2. 月亮之上</li>
	<li>3. 最炫民族风</li>
</ul>
```

### 3、定义列表`<dl>`

> 定义列表的作用非常大。

`<dl>`英文单词：definition list，没有属性。dl的子元素只能是dt和dd。

 - `<dt>`：definition title 列表的标题，这个标签是必须的
 - `<dd>`：definition description 列表的列表项，如果不需要它，可以不加

备注：dt、dd只能在dl里面；dl里面只能有dt、dd。

举例：

```html
<dl>
	<dt>CSS网站</dt>
	<dd>你好CSS</dd>
	<dd>HelloCss</dd>
	<dd>CSS是世界上最棒的语言？</dd>

	<dt>JS网站</dt>
	<dd>1</dd>
	<dd>0</dd>
	<dd>2</dd>
	<dd>4</dd>
</dl>
```

上图可以看出，定义列表表达的语义是两层：

- （1）是一个列表，列出了几个dd项目
- （2）每一个词儿都有自己的描述项。

备注：dd是描述dt的。

dt、dd都是容器级标签，想放什么都可以。所以，现在就应该更加清晰的知道：用什么标签，不是根据样子来决定，而是语义（语义本质上是结构）。





