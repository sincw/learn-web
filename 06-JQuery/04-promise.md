# promise对象

### 什么是promise
romise 是异步编程的一种解决方案：从语法上讲，promise是一个对象，从它可以获取异步操作的消息；从本意上讲，它是承诺，承诺它过一段时间会给你一个结果。
promise有三种状态：pending(等待态)，fulfiled(成功态)，rejected(失败态)；状态一旦改变，就不会再变。创造promise实例后，它会立即执行。


### $.deferred
Jquery1.5后开始引入了$.deferred，$.deferred是Jquery对于Promise/A+规范的实现 。

deferred对象是一个延迟对象，意思是函数延迟到某个点才开始执行，改变执行状态的方法有两个（成功：resolve和失败：reject），分别对应两种执行回调（成功回调函数：done和失败回调函数fail）

```javascript
//JS1.5之前的ajax操作
$.get('api1/data', function(resp1) {
    // Next that depended on the first response.
    $.get('api2/data', function(resp2) {
        // Next request that depended on the second response.
        $.get('api3/data', function(resp3) {
            // Next request that depended on the third response.
            $.get(); // ... you get the idea.
        });
    });
});

//JS1.5之后的ajax操作
$.ajax("index.html")
.done(function () { alert("success"); })
.fail(function () { alert("error"); })
.done(function () { alert("success2");});

$.when($.ajax("index.html"), $.ajax("addorder2.html"))
.done(function () { alert("success"); })
.fail(function () { alert("error");})
```

（1）$.Deferred()生成一个deferred对象。

（2）deferred.done()指定操作成功时的回调函数

（3）deferred.fail()指定操作失败时的回调函数

（4）deferred.promise()没有参数时，作用为保持deferred对象的运行状态不变；接受参数时，作用为在参数对象上部署deferred接口。

（5）deferred.resolve()手动改变deferred对象的运行状态为"已完成"，从而立即触发done()方法。

（6）$.when()为多个操作指定回调函数。

除了这些方法以外，deferred对象还有三个重要方法，上面的教程中没有涉及到。

（7）deferred.then()
有时为了省事，可以把done()和fail()合在一起写，这就是then()方法。
$.when($.ajax( "/main.php" ))
.then(successFunc, failureFunc );
如果then()有两个参数，那么第一个参数是done()方法的回调函数，第二个参数是fail()方法的回调方法。
如果then()只有一个参数，那么等同于done()。

（8）deferred.reject()
这个方法与deferred.resolve()正好相反，调用后将deferred对象的运行状态变为"已失败"，从而立即触发fail()方法。

（9）deferred.always()
这个方法也是用来指定回调函数的，它的作用是，不管调用的是deferred.resolve()还是deferred.reject()，最后总是执行。
$.ajax( "test.html" )
.always( function() { alert("已执行！");} );

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
</body>
<!--<script src="http://libs.baidu.com/jquery/1.11.1/jquery.min.js"></script>-->
<script src="http://libs.baidu.com/jquery/2.1.4/jquery.min.js"></script>
<script>
    function asynDosome(flag,time) {
        var def = $.Deferred();
        setTimeout(function () {
            if (flag) {
                var value = "OK";
                def.resolve(value);
            } else {
                var value = "FAIL";
                def.reject(value);
            }
        }, time);
        return def.promise();
    }
    //2.0版本前的then要写在done后面，将下例的done,then交换位置，会出现一个bug,会无法触发fail操作
    $.when(asynDosome(true,1000),asynDosome(true,2000)).done(function (message,message2) {
        console.info("when1:"+message +" when2:" + message2);
    }).done(function (message) {
        console.info("then:"+message);
        return asynDosome(true,500);
    }).then(function (message) {
        console.info("done:"+ message);
        return asynDosome(false,500);
    }).always(function(){
        console.info("allways");
    }).fail(function (err) {
        console.info("fail:"+err);
    });
</script>
</html>

```
