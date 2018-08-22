# Jquery Html

### jQuery DOM 操作

jQuery 中非常重要的部分，就是操作 DOM 的能力。

jQuery 提供一系列与 DOM 相关的方法，这使访问和操作元素和属性变得很容易。

#### dom内容及属性

- text() 设置或返回所选元素的文本内容
- html() 设置或返回所选元素的内容（包括 HTML 标记）
- val() 设置或返回表单字段的值
- attr() 设置或获取属性，可以传递回调函数


```javascript
<!DOCTYPE html>
<html>
<head>
    <script src="http://libs.baidu.com/jquery/1.11.1/jquery.min.js"></script>
    <script>
        $(document).ready(function(){
            $("#btn1").click(function(){
                alert("Text: " + $("#test").text());
            });
            $("#btn2").click(function(){
                alert("HTML: " + $("#test").html());
            });
            $("#btn3").click(function(){
                alert("Value: " + $("#test2").val());
            });
            $("#btn4").click(function(){
                alert($("#sincw").attr("title"));
            });
            $("#btn11").click(function(){
                $("#test").text("Hello world!");
            });
            $("#btn22").click(function(){
                $("#test").html("<b>Hello world!</b>");
            });
            $("#btn33").click(function(){
                $("#test2").val("Dolly Duck");
            });
            $("#btn44").click(function(){
                $("#sincw").attr("title",'#sincw2');
            });
            $("#btn55").click(function(){
                $("#sincw").attr("title",function(i,old){
                    return old + "999";
                });
            });
        });
    </script>
</head>

<body>
<p id="test">这是段落中的<b>粗体</b>文本。</p>
<button id="btn1">显示文本</button>
<button id="btn2">显示 HTML</button>
<button id="btn3">显示 VALUE</button>
<button id="btn4">显示 attr</button>
<button id="btn11">设置文本</button>
<button id="btn22">设置 HTML</button>
<button id="btn33">设置 VALUE</button>
<button id="btn44">设置 attr</button>
<button id="btn55">设置 attr(回调方法)</button>
<input type="text" id="test2" value="米老鼠">
<a href="#sincw" title="sincw" id="sincw">鼠标移入查看title变化</a>
</body>

</html>

```

#### dom添加

- append()  在被选元素的结尾插入内容
- prepend()  在被选元素的开头插入内容
- after()  在被选元素之后插入内容
- before()  在被选元素之前插入内容


```javascript

<!DOCTYPE html>
<html>
<head>
    <script src="http://libs.baidu.com/jquery/1.11.1/jquery.min.js"></script>
    <script>
        $(document).ready(function(){

            $("#btn1").click(function(){
                $("ol").append("<li>Appended item</li>");
            });

            $("#btn11").click(function(){
                var li = "<li>Prepended item</li>";
                $("ol").prepend(li,li);
            });

            $("#btn2").click(function(){
                $("li").eq(1).before("<b>Before</b>");
            });

            $("#btn22").click(function(){
                $("li").eq(1).after("<i>After</i>");
            });
        });
    </script>
</head>

<body>
<p>This is a paragraph.</p>
<p>This is another paragraph.</p>
<ol>
    <li>List item 1</li>
    <li>List item 2</li>
    <li>List item 3</li>
</ol>
<button id="btn1">向后追加</button>
<button id="btn11">向前追加2个</button>
<button id="btn2">向第2个前追加</button>
<button id="btn22">向第2个后追加2个</button>
</body>
</html>

```

#### dom删除

remove() - 删除被选元素（及其子元素）
empty() - 从被选元素中删除子元素

```javascript
<!DOCTYPE html>
<html>
<head>
    <script src="http://libs.baidu.com/jquery/1.11.1/jquery.min.js"></script>
    <script>
        $(document).ready(function(){
            $("#btn1").click(function(){
                $("#div1").remove();
            });
            $("#btn2").click(function(){
                $("p").remove(".italic");
            });
            $("#btn3").click(function(){
                $("#div1").empty();
            });
        });
    </script>
</head>

<body>

<div id="div1" style="height:100px;width:300px;border:1px solid black;background-color:yellow;">
    This is some text in the div.
    <p class="italic">This is a paragraph in the div.</p>
    <p>This is another paragraph in the div.</p>
</div>

<br>
<button id="btn2">删除  P 元素中class = italic的元素</button>
<button id="btn3">清空 div 元素</button>
<button id="btn1">删除 div 元素</button>
</body>
</html>

```

#### dom新增，删除样式

- addClass() 向被选元素添加一个或多个类
- removeClass() 从被选元素删除一个或多个类
- toggleClass() 对被选元素进行添加/删除类的切换操作
- css() 设置或返回样式属性

```javascript
<!DOCTYPE html>
<html>
<head>
    <script src="http://libs.baidu.com/jquery/1.11.1/jquery.min.js"></script>
    <script>
        $(document).ready(function(){
            $("#btn1").click(function(){
                $("h1,h2,p").addClass("blue");
                $("div").addClass("blue");
            });

            $("#btn2").click(function(){
                $("h1,h2,p").addClass("blue important");
                $("div").addClass("important blue");
            });

            $("#btn3").click(function(){
                $("h1,h2,p").removeClass("blue");
                $("div").removeClass("blue");
            });

            $("#btn4").click(function(){
                $("h1,h2,p").removeClass("important blue");
                $("div").removeClass("important blue");
            });

            $("#btn5").click(function(){
                $("div").toggleClass("blue");
            });
            
        });
    </script>
    <style type="text/css">
        .important
        {
            font-weight:bold;
            font-size:xx-large;
        }
        .blue
        {
            color:blue;
        }
    </style>
</head>
<body>

<h1>标题 1</h1>
<h2>标题 2</h2>
<p>这是一个段落。</p>
<p>这是另一个段落。</p>
<div>这是非常重要的文本！</div>
<br>
<button id="btn1">向元素添加类</button>
<button id="btn2">向元素添加多个类</button>
<button id="btn3">向元素移除类</button>
<button id="btn4">向元素移除多个类</button>
<button id="btn5">添加/删除类的切换操作</button>
</body>
</html>

```

```javascript
<!DOCTYPE html>
<html>
<head>
    <script src="http://libs.baidu.com/jquery/1.11.1/jquery.min.js"></script>
    <script>
        $(document).ready(function(){
            $("#btn1").click(function(){
                $("h1,h2,p").addClass("blue");
                $("div").addClass("blue");
            });

            $("#btn2").click(function(){
                $("h1,h2,p").addClass("blue important");
                $("div").addClass("important blue");
            });

            $("#btn3").click(function(){
                $("h1,h2,p").removeClass("blue");
                $("div").removeClass("blue");
            });

            $("#btn4").click(function(){
                $("h1,h2,p").removeClass("important blue");
                $("div").removeClass("important blue");
            });

            $("#btn5").click(function(){
                $("div").toggleClass("blue");
            });

            $("#btn6").click(function(){
                $("h3").css("background-color",'red');
            });

            $("#btn7").click(function(){
                alert($("h3").css("background-color"));
            });

            $("#btn8").click(function(){
                var style = {
                    "background-color":'red',
                    "font-size":"28px"
                }
                $("h3").css(style);
            });
            
        });
    </script>
    <style type="text/css">
        .important
        {
            font-weight:bold;
            font-size:xx-large;
        }
        .blue
        {
            color:blue;
        }
    </style>
</head>
<body>

<h1>标题 1</h1>
<h2>标题 2</h2>
<p>这是一个段落。</p>
<p>这是另一个段落。</p>
<div>这是非常重要的文本！</div>
<h3>CSS()方法！</h3>
<br>
<button id="btn1">向元素添加类</button>
<button id="btn2">向元素添加多个类</button>
<button id="btn3">向元素移除类</button>
<button id="btn4">向元素移除多个类</button>
<button id="btn5">添加/删除类的切换操作</button>
<button id="btn7">CSS()获取样式</button>
<button id="btn6">CSS()新增样式</button>
<button id="btn8">CSS()新增多个样式</button>
</body>
</html>

```

#### dom宽高获取和设置

- width() 方法设置或返回元素的宽度（不包括内边距、边框或外边距）。offsetWidth - border - padding
- height() 方法设置或返回元素的高度（不包括内边距、边框或外边距）。 
- innerWidth() 方法返回元素的宽度（包括内边距）。offsetWidth - border
- innerHeight() 方法返回元素的高度（包括内边距）。
- outerWidth(param) 方法返回元素的宽度（包括内边距、边框和外边距）。 offsetWidth + (param ? margin: 0)
- outerHeight(param) 方法返回元素的高度（包括内边距、边框和外边距）。

```javascript
<!DOCTYPE html>
<html>
<head>
    <script src="http://libs.baidu.com/jquery/1.11.1/jquery.min.js"></script>
    <script>
        $(document).ready(function(){
            $("#btn0").click(function(){
                $("#div1").width($("#div1").width() - 100);
                $("#div1").height($("#div1").height() - 20);
                var txt="";
                txt+="Width of div: " + $("#div1").width() + "</br>";
                txt+="Height of div: " + $("#div1").height();
                $("#div1").html(txt);
            });
            $("#btn1").click(function(){
                var txt="";
                txt+="Width of div: " + $("#div1").width() + "</br>";
                txt+="Height of div: " + $("#div1").height();
                $("#div1").html(txt);
            });
            $("#btn2").click(function(){
                var txt="";
                txt+="innerWidth of div: " + $("#div1").innerWidth() + "</br>";
                txt+="innerHeight of div: " + $("#div1").innerHeight();
                $("#div1").html(txt);
            });
            $("#btn3").click(function(){
                var txt="";
                txt+="outerWidth of div: " + $("#div1").outerWidth(true) + "</br>";
                txt+="outerHeight of div: " + $("#div1").outerHeight(true);
                $("#div1").html(txt);
            });
            $("#btn4").click(function(){
                var txt="";
                txt+="outerWidth of div: " + $("#div1").outerWidth() + "</br>";
                txt+="outerHeight of div: " + $("#div1").outerHeight();
                $("#div1").html(txt);
            });
        });
    </script>
</head>
<body>

<div id="div1" style="display:inline-block;height:100px;width:300px;padding:10px;margin:30px;border:5px solid blue;background-color:lightblue;"></div>
<br>
<button id="btn0">设置 div width()的尺寸</button>
<button id="btn1">显示 div width()的尺寸</button>
<button id="btn2">显示 div innerWidth()的尺寸</button>
<button id="btn3">显示 div outerWidth(true)的尺寸</button>
<button id="btn4">显示 div outerWidth()的尺寸</button>
</body>
</html>

```
