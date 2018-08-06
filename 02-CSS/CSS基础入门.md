#CSS基础入门

###布局

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


###边距
![]((https://raw.githubusercontent.com/sincw/learn-web/master/img/02/box-modal.jpg))

margin：层的边框以外留的空白

background-color：背景颜色

background-image：背景图片

padding：层的边框到层的内容之间的空白 

border：边框 

content：内容

#####margin
```css
#main {
  width: 600px;
  margin: 0 auto; 
}
```
设置块级元素的 width 可以防止它从左到右撑满整个容器。然后你就可以设置左右外边距为 auto 来使其水平居中。元素会占据你所指定的宽度，然后剩余的宽度会一分为二成为左右外边距。
唯一的问题是，当浏览器窗口比元素的宽度还要窄时，浏览器会显示一个水平滚动条来容纳页面。让我们再来改进下这个方案...


```css
#main {
  max-width: 600px;
  margin: 0 auto; 
}
```
在这种情况下使用 max-width 替代 width 可以使浏览器更好地处理小窗口的情况。这点在移动设备上显得尤为重要，调整下浏览器窗口大小检查下吧！
顺便提下， 所有的主流浏览器包括IE7+在内都支持 max-width ，所以放心大胆的用吧。
