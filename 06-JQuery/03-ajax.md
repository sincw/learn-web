# ajax

### 什么是ajax

是与服务器交换数据的艺术，它在不重载全部页面的情况下，实现了对部分网页的更新。


####  $(selector).load(url,data,callback);

```javascript
<!DOCTYPE html>
<html>
<head>
    <script src="http://libs.baidu.com/jquery/1.11.1/jquery.min.js"></script>
    <script>
        $(document).ready(function(){
            $("#btn1").click(function(){
                $('#test').load('./sincw.text');
            })
            $("#btn2").click(function(){
                $('#test').load('./sincw.text h2',function(responseTxt,statusTxt,xhr){
                    if(statusTxt=="success")
                        alert("外部内容加载成功！" + responseTxt);
                    if(statusTxt=="error")
                        alert("Error: "+xhr.status+": "+xhr.statusText);
                });
            })
        })
    </script>
</head>

<body>

<h3 id="test">请点击下面的按钮，通过 jQuery AJAX 改变这段文本。<span id="hi"></span></h3>
<button id="btn1" type="button">获得外部的所有内容</button>
<button id="btn2" type="button">获得外部的h2的内容</button>

</body>
</html>
```


#### HTTP 请求：GET and POST

- GET - 从指定的资源请求数据
- POST - 向指定的资源提交要处理的数据

GET 基本上用于从服务器获得（取回）数据。注释：GET 方法可能返回缓存数据。
POST 也可用于从服务器获取数据。不过，POST 方法不会缓存数据，并且常用于连同请求一起发送数据。


##### $.get(URL,callback);

必需的 URL 参数规定您希望请求的 URL。

可选的 callback 参数是请求成功后所执行的函数名。

$.get() 方法通过 HTTP GET 请求从服务器上请求数据。

##### $.post(URL,data,callback);

必需的 URL 参数规定您希望请求的 URL。

可选的 data 参数规定连同请求发送的数据。

可选的 callback 参数是请求成功后所执行的函数名。

$.post() 方法通过 HTTP POST 请求从服务器上请求数据。

##### $.ajax

```javascript
$.ajax({
            url:"url",
            type:"get",
            dataType:"json",
            data:{
                name:"sincw"
            },
            success:function(response){
 
            },
            error:function() {
            }
        });
```

```javascript
<!DOCTYPE html>
<html>
<head>
    <script src="http://libs.baidu.com/jquery/1.11.1/jquery.min.js"></script>
    <script>
        $(document).ready(function(){
            $("#btn1").click(function(){
                $('#test').load('./sincw.text');
            })
            $("#btn2").click(function(){
                $('#test').load('./sincw.text h2',function(responseTxt,statusTxt,xhr){
                    if(statusTxt=="success")
                        alert("外部内容加载成功！" + responseTxt);
                    if(statusTxt=="error")
                        alert("Error: "+xhr.status+": "+xhr.statusText);
                });
            });
            $("#btn3").click(function(){
                $.get("./sincw.text",function(data,status){
                    alert("数据："  +data+ "\n状态：" + status);
                });
            })
            $("#btn4").click(function(){
                $.post("./sincw.text",
                    {
                        name:"Sincw",
                        city:"gz"
                    },
                    function(data,status){
                        alert("数据：" + data + "\n状态：" + status);
                    });
            })

            $("#btn5").click(function(){
                $(function () {
                    // 发送jsonp请求
                    $.ajax({
                        type:"get",
                        url:'http://api.map.baidu.com/telematics/v3/weather?output=json&ak=0A5bc3c4fb543c8f9bc54b77bc155724',
                        data:{
                            location:$("#city").val()||"上海"
                        },
                        dataType:"jsonp",
                        success: function (data) {
                            var html = data.results[0].weather_data;
                            $('#weather').html(html);

                        }
                    });
                });

                
            })
        });
        
    </script>
</head>

<body>
<div id="weather"></div>
<h3 id="test">请点击下面的按钮，通过 jQuery AJAX 改变这段文本。<span id="hi"></span></h3>
<button id="btn1" type="button">Load获得外部的所有内容</button>
<button id="btn2" type="button">Load获得外部的h2的内容</button>
<button id="btn3" type="button">$.Get获得外部的内容</button>
<button id="btn4" type="button">$.Post获得外部内容,大多数服务器不让静态文件响应post请求-405，访问其他域也会出现跨域问题</button>
<button id="btn5" type="button">$.ajax获得外部的内容</button>
</body>
</html>

```


##### 跨域问题

在进行网站开发的过程中经常会用到第三方的数据，但是由于同源策略的限制导致ajax不能发送请求，因此也无法获得数据。解决ajax的跨域问题有两种方法：

　　一、jsop 　

　　二、XMLHttpRequest2中可以配合服务端来解决，在响应头中加入Access-Control-Allow-Origin:*

1、**同源**：

同源策略是浏览器的一种安全策略，所谓同源是指，域名，协议，端口号完全相同
1.1目的：保护用户信息安全
1.2限制：cookie、localStorage和IndexDB无法读取
无法操作跨域的iframe里的dom元素
ajax请求不能发送

2、**跨域**：

当在https://api.example.com/detail.html请求http://api.example.com:8080的数据是，就会发生跨域问题。

![](imgs/1535031253(1).jpg)


不同源则为跨域，JSONP其本质是利用了标签具有可跨域的特性，由服务端返回预先定义好的javascript函数的调用，并且将服务端数据以该函数参数的形式传递过来。


在img中，我们使用跨域的图片是可以的，加载跨域的脚本也是可以的。利用这个原理，我们将请求的数据作为脚本返回，就可以达到跨域的效果。
看这两段代码就应该比较清楚了



**客户端代码**
```javascript
<html>
<head>
    <title>跨域测试</title>
    <script src="js/jquery-1.7.2.js"></script>
    <script>
        //回调函数
        function showData (result) {
            var data = JSON.stringify(result); //json对象转成字符串
            $("#text").val(data);
        }

        $(document).ready(function () {

            $("#btn").click(function () {
                //向头部输入一个脚本，该脚本发起一个跨域请求
                $("head").append("<script src='http://localhost:9090/student?callback=showData'><\/script>");
            });

        });
    </script>
</head>
<body>
    <input id="btn" type="button" value="跨域获取数据" />
    <textarea id="text" style="width: 400px; height: 100px;"></textarea>

</body>
</html>
```

**服务端代码**

```javascript

protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    response.setCharacterEncoding("UTF-8");
    response.setContentType("text/html;charset=UTF-8");

    //数据
    List<Student> studentList = getStudentList();


    JSONArray jsonArray = JSONArray.fromObject(studentList);
    String result = jsonArray.toString();

    //前端传过来的回调函数名称
    String callback = request.getParameter("callback");
    //用回调函数名称包裹返回数据，这样，返回数据就作为回调函数的参数传回去了
    result = callback + "(" + result + ")";

    response.getWriter().write(result);
}
```
