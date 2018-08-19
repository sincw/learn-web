# 04-Jquery链式调用


### 链式调用
 jQuery的核心理念是Write less,Do more(写的更少,做的更多)，那么链式方法的设计与这个核心理念不谋而合
 ```javascript
$('input[type="button"]').eq(0).click(
    function() {
    alert('点击我!');
}).end().eq(1).click(
    function() {
    $('input[type="button"]:eq(0)').trigger('click');
}).end().eq(2).toggle(
    function() {
    $('.sinw').hide('slow');
}, function() {
    $('.sinw').show('slow');
});
```

上面代码的含义是

  ☑  找出type类型为button的input元素

  ☑  找到第一个按钮，并绑定click事件处理函数

  ☑  返回所有按钮，再找到第二个

  ☑  为第二个按钮绑定click事件处理函数

  ☑  为第三个按钮绑定toggle事件处理函数

通过简单扩展原型方法并通过return this的形式来实现跨浏览器的链式调用。

### 自己实现一个简单的链式调用

```html
<!DOCTYPE HTML>
<html>
<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    <title>无标题文档</title>
</head>
<body>

<button id="test1">test1</button>
<button id="test2">test2</button>
<button id="test3">test3</button>
<button id="test4">test4</button>

<script type="text/javascript">
    //创建工厂用于生产链式调用的对象，并在原型上添加方法
    (function(){
        function _$(obj){
            var elements;
            if(typeof obj === "string"){
                elements = document.getElementsByTagName(obj);
            }else if(Array.isArray(obj)){
                elements = obj;
            }else{
                elements = [obj];
            }
            this.elements = elements;
        }

        _$.prototype = {
            each : function(fn){
                for(var i = 0, len = this.elements.length; i < len; i++){
                    fn.call(this.elements[i], this.elements[i]);
                }
                return this;
            },
            sayHi : function(){
                this.each(function(){
                    console.info("hi " + this.id);
                });
                return this;
            },
            sayHello:function(){
                this.each(function(){
                    console.info("hello " + this.id);
                });
                return this;
            },
            //由工厂产生一个新的对象，并设置其父亲
            eq:function(i){
                var that = new _$(this.elements[i])
                that.pre = this;
                return that;
            },
            //返回其父亲
            end:function(){
                return  this.pre;
            }
        }

        // 公开接口
        window.$ = function(tagname){
            return new _$(tagname);
        }
    })();
    
    var sincw = $("button");
    sincw.sayHello();
    console.info("---------------------")
    sincw.eq(0).sayHello().end().eq(3).sayHi().end().sayHello();

</script>

</body>
</html>


```

![](imgs/1533999884.jpg)
