# 缓存

### 内存泄漏

C#和Java等语言采用了自动垃圾回收方法管理内存，正常使用的情况下几乎不会发生内存泄露。
浏览器中也是采用自动垃圾回收方法管理内存，但由于浏览器垃圾回收方法有bug，会产生内存泄露。
其实绝大部分内存泄漏都不是由Javascript引起的，浏览器的回收机制已经做的相当好了，多数的泄漏都是由于与DOM交互而产生的。


浏览器内存泄露主要是由于DOM对象与JS对象的循环引用导致的

```javascript
//1 多个对象循环引用
var a=document.getElementById(selector);
var b=document.getElementById(selector)t;

a.r=b;
b.r=a;
  
//2 循环引用自己
var a=document.getElementById(selector);
a.r=a;
```

DOM中remove了元素，但是依然有变量或者对象引用了该DOM对象。然后内存中无法删除。
使得浏览器的内存占用居高不下。这种内存占用，随着浏览器的刷新，会自动释放。


一个DOM对象和JS对象之间互相引用，这样造成的情况更严重一些，即使刷新，内存也不会减少。

在平时实际应用中, 我们经常需要给元素缓存一些数据，并且这些数据往往和DOM元素紧密相关。
由于DOM元素(节点)也是对象, 所以我们可以直接扩展DOM元素的属性，但是如果给DOM元素添加自定义的属性和过多的数据可能会引起内存泄漏，所以应该要尽量避免这样做。
因此更好的解决方法是使用一种低耦合的方式让DOM和缓存数据能够联系起来。所以我们必须有一种机制，避免引用数据直接依附在DOM对象上，这样尽量避免内存泄漏的产生。
jQuery的缓存系统就很好的解决了这一问题。

### $.data(element, key, value)

jQuery从1.2.3版本引入数据缓存系统

#### 使用方式
```javascript
    var ele1 = $("#sincw");
    var ele2 = $("#sincw");

    //=======第一组=========
    ele1.data('a',1111);
    ele2.data('a',2222);
    console.info('第一组,通过$().data()的方式,只取到最后一个a值,之前的被覆盖')
    console.info(ele1.data('a'))
    console.info(ele2.data('a'))

    //=======第二组=========
    
    $.data(ele1,"b","1111")
    $.data(ele2,"b","2222")
    console.info('第二组,通过$.data的方式,取到2组b值，未覆盖')
    console.info($.data(ele1,"b"))
    console.info($.data(ele2,"b"))
    //为什么不被覆盖的原因在后面说明
```

#### 基本原理

jQuery缓存设计接口对数据的处理有如下几种：

>用name和value为对象附加数据
一个对象为对象附加数据
为 DOM Element 附加数据


常规的数据缓存，我们都大多为了方便直接就绑定到了dom对应的元素上了，最为常见的就是事件对象的回调函数了，还有一些DOM的属性。当然这也不是不可以，jQuery早期就是这么干的，但是容易引发循环引用，也会带来一定的全局污染的问题。那么jQuery在之后的改进就独立出了一个”数据缓存“的模块。

其核心的关键就是：

>数据存放在内存中，通过一个映射关系与直接的DOM元素发生关联

数据缓存，jQuery现在支持两种：

> dom元素，数据存储在jQuery.cache中。
普通js对象，数据存储在该对象中。

首先先要在内存中开辟一个区域，用来保存数据，jQuery用cache对象{},那么所有的数据无法就是针对cache的CURD操作了。

1:如果是DOM元素，通过分配一个唯一的关联id把DOM元素和该DOM元素的数据缓存对象关联起来，关联id被附加到以jQuery.expando的值命名的属性上，数据存储在全局缓存对象jQuery.cache中。在读取、设置、移除数据时，将通过关联id从全局缓存对象jQuery.cache中找到关联的数据缓存对象，然后在数据缓存对象上执行读取、设置、移除操作。

2:如果是Javascript对象，数据则直接存储在该Javascript对象的属性jQuery.expando上。在读取、设置、移除数据时，实际上是对Javascript对象的数据缓存对象执行读取、设置、移除操作。

3:为了避免jQuery内部使用的数据和用户自定义的数据发生冲突，数据缓存模块把内部数据存储在数据缓存对象上，把自定义数据存储在数据缓存对象的属性data上。

```javascript
<!DOCTYPE HTML>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    <script src="../jq/jquery-2.1.1.js"></script>
    <title></title>
</head>
<body>

<div id="sincw">缓存测试</div>
</br>

<script type="text/javascript">

    var cache = {};

    function Data() {

    }

    Data.prototype.get = function (select, key) {
        return cache[select.JQueryID][key];
    }

    Data.prototype.set = function (select, key, value) {
        if (!select.JQueryID) {
            select.JQueryID = Math.random();
        }
        if (cache[select.JQueryID]) {
            cache[select.JQueryID][key] = value;
        } else {
            var obj = {};
            obj[key] = value;
            cache[select.JQueryID] = obj;
        }
    }
    
    //为什么$.data和$(selector).data不同的原因如下，使用$(selector)，他们的cache是加在DOM对象上的
    // 而使用$.data时，他们的cache是加在JQuery对象上的

    var ele1 = $("#sincw");
    var ele2 = $("#sincw");
    var Data = new Data();
    Data.set(ele1, "NAME", "SINCW");
    Data.set(ele2, "NAME", "SINCW2");
    console.info(Data.get(ele1, 'NAME'));
    console.info(Data.get(ele2, 'NAME'));

    console.info('-------------------------');

    var ele1 = document.getElementById("sincw");
    var ele2 = document.getElementById("sincw");
    Data.set(ele1, "NAME", "SINCW");
    Data.set(ele2, "NAME", "SINCW2");
    console.info(Data.get(ele1, 'NAME'));
    console.info(Data.get(ele2, 'NAME'));


</script>

</body>
</html>

```



