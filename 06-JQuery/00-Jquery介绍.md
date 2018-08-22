# Jquery 介绍

## 什么是 jQuery
jQuery 是 js 的一个库，封装了我们开发过程中常用的一些功能，方便我们调用，提高开发效率。

js库是把我们常用的功能放到一个单独的文件中，我们用的时候，直接引用到页面里即可。

以下是jQuery的相关信息：

- 官网：http://jquery.com/

- 官网API文档：http://api.jquery.com/

- 中文汉化API文档：http://www.css88.com/jqapi-1.9/

### 学习jQuery，主要是学什么
初期，主要学习如何使用jQuery操作DOM，其实就是学习jQuery封装好的那些功API。

这些API的共同特点是：几乎全都是方法。所以，在使用jQuery的API时，都是方法调用，也就是说要加小括号()，小括号里面是相应的参数，参数不同，功能不同。

### jQuery 的两大特点
（1）**链式编程**：比如.show()和.html()可以连写成.show().html()。

链式编程原理：return this。

通常情况下，只有设置操作才能把链式编程延续下去。因为获取操作的时候，会返回获取到的相应的值，无法返回 this。

（2）**隐式迭代**：隐式 对应的是 显式。隐式迭代的意思是：在方法的内部会为匹配到的所有元素进行循环遍历，执行相应的方法；而不用我们再进行循环，简化我们的操作，方便我们调用。

如果获取的是多元素的值，大部分情况下返回的是第一个元素的值。

## jQuery的使用

### 使用 jQuery 的基本步骤
（1）引包

（2）入口函数

（3）功能实现代码（事件处理）


```javascript
<!DOCTYPE html>
<html>
<head>
<script src="/jquery/jquery-1.11.1.min.js"></script>
<script>
$(document).ready(function(){
  $("#btn1").click(function(){
    alert("Text: " + $("#test").text());
  });
  $("#btn2").click(function(){
    alert("HTML: " + $("#test").html());
  });
});
</script>
</head>

<body>
<p id="test">这是段落中的<b>粗体</b>文本。</p>
<button id="btn1">显示文本</button>
<button id="btn2">显示 HTML</button>
</body>

</html>

```
