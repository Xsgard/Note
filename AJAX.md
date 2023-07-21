## 1.0.0 AJAX

> Asynchronous Javascript And XML，简称AJAX，异步的 js和XML，它不是一种新技术，只是老技术[js]采用新用法【引用了XMLHttpRequest对象】。
>
> 前提：
>
> 1. HTML
> 2. CSS
> 3. JavaScript
> 4. JSON

###	1.0.1 同步请求和异步请求

> **同步请求**是指当浏览器发出请求后，只有当服务端完成后响应回来，才能看到响应结果，这个过程中，浏览器不能做其他事情，只能等待服务端的响应。
>
> **异步请求**是指当浏览器发出请求后，等待服务端的响应，在此期间，浏览器不阻塞，你可去做其他的事情，直到服务端的响应结束。
>
> 所以，我们看到的同步请求就是整个浏览器的页面都会刷新一次。
>
> 而异步请求是局部刷新，他不会整体刷新页面。
>
> 本质上说，异步请求就是由浏览器开启一个新线程去发送请求到服务端，而主线程不受影响，知道这个异步线程从服务端响应回来，然后，主线程就要针对这个回来的响应进行处理。

### 1.0.2 AJAX的对象

XMLHttpRequest对象，专用来发送异步请求的对象，当然，也可以发送同步请求。

这个对象从IE7以后，IE的所有版本都是支持此对象的。而FF，safari，chrome都是支持的。



## 2.0.0 AJAX代码编写步骤

1. 创建XMLHttpRequest对象

2. 注册回调函数

3. 建立与服务端的连接

4. 发送请求

   ```js
   var xmlhttp;
       function ajax_demo() {
           //1.创建XMLHttpRequest对象
           if (window.XMLHttpRequest) {
               xmlhttp = new XMLHttpRequest();
           } else {
               xmlhttp = new ActiveXObject("Microsoft.XMLHTTP")
           }
           //2.注册回调函数
           xmlhttp.onreadystatechange = function () {
               //执行异步代码
               ....
           }
           //3.建立与服务端的连接
           xmlhttp.open("POST|GET","目标URL",true|false);//true表示异步 false表示同步
           //4.发送请求
           xmlhttp.send();//如果要传数据给服务端，把数据作为参数传过去
       }
   ```

### 2.0.1 XMLHttpRequest对象的属性

1. readyState属性

   > 此属性 0-4的值，共计5种状态
   >
   > 0  请求未初始化
   >
   > 1  服务器连接已经建立  
   >
   > 2  请求已接收
   >
   > 3  请求处理中
   >
   > 4  请求已完成，响应已经就绪2.

2. status属性

   >响应状态码，有5种类型的值，分别是：
   >
   >1xx	
   >
   >2xx	代表服务端正常响应客户端
   >
   >3xx	代表服务端资源没有发生改变
   >
   >4xx	代表资源错误
   >
   >5xx	代表服务端错误

3. responseText和responseXML

   > responseText表示以文本的信息获取服务端的响应，获取的就是字符串
   >
   > responseXML当服务端以XML格式返回给客户端时，则使用此属性去接收。获取的就是DOM对象

