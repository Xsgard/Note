## 1. Servlet

> servlet标准：
>
> 运行在服务器的一种技术组件，是JavaEE的标准，主要是制定了客户端与服务端进行通信处理的一种机制，由WEB服务器负责实现这个标准。比如：Tomcat
>
> Servlet做为JavaEE的一个技术标准，它的规范中定义了大量的接口，主要存放在如下包中：
>
> * javax.servlet 包
> * javax.servlet.http 包

### 1.0.0 Servlet基础

**Servlet的使命**

1. 作为请求和响应的控制器而存在【最重要】
2. 输出动态页面【做的很差，所以才有了后面的JSP规范】

#### 1.0.1 Web应用的目录结构

appName/

​				lib/	用来存储此应用所以来的第三方jar包

​				WEB-INF/	存储需要受到容器【web服务器】保护的资源

​								web.xml	用来描述web资源的文件，比如：描述servlet组件[3.0之后，可以替换为注解]

​								classes/	自动生成，用来存放生成的字节码

​								....

​				....	与WEB-INF平级的目录，一般是存放不受容器保护的资源，如：html、css、js 等

#### 1.0.2 servlet的定义

>就是一个接口【javax.servlet.Servlet】,它是运行在WEB SERVER中的一小段程序。Servlet与Web Server之间也是一个描述文件的，能通过这个描述文件，程序员要告诉WEB SERVER，你要去管理那些Servlet
>
>这个描述文件就叫：**web.xml**

#### 1.0.3 开发servlet

1. 写一个类实现javax.servlet.Servlet接口

2. 重写Servlet接口中的所有方法，主要有：

   * init()	         初始化方法
   * service()；  服务方法
   * destroy()     销毁方法
   * getServletConfig()  获取Servlet的配置信息
   * getServletInfo()      获取Servlet的字符串信息

3. 通过在web.xml中进行描述，告诉Web Server，要去管理这个Servlet.

   注：在Servlet3.0之后，Servlet规范中提供了注解，使用注解后，就无需在web.xml中进行配置了。

4. 启动Web Server，进行测试

#### 1.0.4 Servlet的执行过程

1. 当客户端第一次请求目标Servlet时，容器会创建目标Servlet的实例。【只创建1次，默认情况下，Tomcat容器是采用单例模式去创建Servlet】
2. 在目标Servlet实例化成功后，调用它的init()方法，并传入ServletConfig对象。
3. 在初始化完成后，马上调用它的service()方法，传入ServletRequest和ServletResponse对象
4. 在此后的请求中，不再执行创建对象和init()方法。

注：

当我们在web.xml中配置Servlet时，使用了<load-on-startup>选项时，表示此Servlet在容器启动后就进行实例化和初始化，而不用等待第一次请求来临。

#### 1.0.5 Servlet相关API

```java
Servlet [I]
	\- GenericServlce[C]	\\通用型Servlet
    	\- HttpServlet[C]	\\专门针对Http协议的Servlet实现者，它里提供了doGet，doPost等方法，而且这些方法的擦书是HttpServletRequest和HttpServletResponse
    		\- 自定义的Servlet应从HttpServlet处继承。
    		
ServletRequest [I]	代表请求接口
	\- HttpServletRequest [I]	针对Http协议
ServletResponse [I]	代表响应接口
	\- HttpServletResponse [I]	针对Http协议
	
ServletConfig [I]	Servlet的配置，就是在web.xml中定义的信息。注：一个Servlet就对应一个ServletConfig

ServletContext [I]	代表当前的应用，被所有Servlet所共享。注：一个应用就对应一个ServletContext
```

#### 1.0.6 HttpServlet

> 针对Http协议的Servlet实现者，它提供了针对Http协议的一些方法，这些方法：
>
> * **doGet**  当用户发送GET请求时，Servlet将调用此方法来响应客户的请求
> * **doPost**  当用户发送POST请求时，Servlet将调用此方法来响应客户的请求
> * doDelete
> * doPut
> * doTrace
> * doHeader
> * doOption
> * ....

#### 1.0.7 请求和响应

> Http协议本来就是基于请求/应答模式的，浏览器向服务端发送请求，服务端向浏览器回应响应，所以，有请求就一定会有响应/应答。
>
> 不管是请求还是响应，都分为两个部分进行传递：
>
> 1. 请求头 或响应头	【header】
> 2. 请求体 或响应体    【body】

#### 1.0.8 GenericServlet的原理

> 这是一个为了扩展而准备的Sevlet实现类，我们不会直接使用这个类，这个类提供了一个空参的init()方法。可以有效地防止我们在重写Servlet的init(ServletConfig config)方法时，忘记去保存ServletConfig对象。
>
> 所以我们应该去重写空参的init方法，而不是规范中定义的带ServletConfig的init方法。

#### 1.0.9 HttpServlet的原理

1. 在此类中，它重写了service(ServletRequest request,ServletResponse response)方法，在此方法通过对请求和响应进行强制类型转换，并调用service(HttpServletRequest req,HttpServletResponse resp)方法
2. 同样，实现service(HttpServletRequest,HttpServletResponse)方法，通过request.getMethod()方法来获取浏览器发送过来的请求方式，如果是get方式，则调用doGet方法，如果是post请求，则调用doPost方法。
3. 我们的Servlet类型，只需要重写doGet或doPost方法即可。

注：在HttpServlet中，保存了ServletConfig

#### 1.0.10 Servlet的url-pattern【3种匹配模式】

1. 精确匹配，如：/hello,/http/htllo

   > 一个Servlet可以映射多个url-pattern
   >
   > 一个精确的url-pattern只能对应一个Servlet

   注：通过调用request.getServletPath()方法就可以获取资源的路径

2. 扩展名匹配，如：*.xxx

   >通过request.getServletPath()方法可以获取具体的资源路径名

   注：通过调用request.getServletPath()方法就可以获取资源的路径

3. 模糊匹配，如：/\*，/user/\*，....

   注：通过调用request.getServletPath()方法只能获取通配中固定的那部分，如果通配是/* 的话，则getServletPath的结果是空。

#### 1.0.11 请求头部和体部的API

1. 头部的API
   * getHeaderNames()
   * getHeader(String headerName)
   * getHeaders(String headerName)
2. 体部的API
   * getParameters(String name);
   * getParameterValues(String name);
   * getParts();
   * getPart(String name);
3. 获取流的方法
   * getInputStream()  =>  ServletInputStream

#### 1.0.12 响应头部和体部的API

1. 头部的API
   - getHeaderNames()
   - getHeader(String headerName)
   - getHeaders(String headerName)
2. 获取流的方式
   * getOutputStream();  =>  ServletOutputStream
3. 修改响应头的方式
   * addHeader(String name,String value)
   * addDateHeader(String name,Long value)
4. 添加Cookie操作
   * addCookie(Cookie c)
5. 重定向方法
   * sendRedirect();
   * sendError();

## 2. Servlet处理请求的流程

1. 浏览器发送请求，一般有两种：一种是Get请求，另一种是Post请求
2. 根据请求的URL，容器决定由哪些资源【Servlet】来响应客户端的请求
3. 容器确定了是哪个Servlet来服务后，就创建此Servlet的实例，并且马上调用它的init方法完成初始化，初始化完成后再调用service方法来响应客户的请求，如果是第二次过来的请求，则直接调用service方法。
4. 在调完service方法后，对本次的请求响应就结束。

### 2.1 容器处理浏览器的响应

> 容器会维护一个核心线程池，每当一个请求来到时，容器就会派出一个线程去响应客户的请求，也就是调用目标Servlet的service方法。当service方法执行完成后，这个线程就会回到线程池。
>
> 所以，在容器面对高并发时，就会有可能造成核心线程池种分配不出线程来响应客户，只能等待它的service方法执行完成后，线程回到核心线程池，再来响应新的请求。

### 2.2 请求转发和重定向

**转发**

> 它是发生在服务端，由服务端决定把这个请求从一个资源上转发到另一个资源上去。Servlet规范中专门定义了请求转发的接口：RequestDispatcher

**包含**

> include方法，是包含 目标资源的输出内容。这是一种动态包含。

**重定向**

> 也是在服务端进行的，但是，它是指由服务端模拟产生一个新的请求，而之前的请求不在了。所以，重定向是不能跳到WEB-INF目录中的资源的。
>
> 另外，重定向由于是产生了新的请求，所以地址栏的地址也会发生变化。

**sendError方法**

> 把一个响应的状态码发送到浏览端，根据这个状态码来渲染页面。

**在Servlet或JSP之前传递数据**

> 容器提供了4种：
>
> * ServletContext 范围：这个对象的生命周期最长，它代表的是应用
> * HttpSession 范围：这个对象代表会话
> * HttpServletRequest 范围：这个对象代表请求
> * PageContext 范围：这个对象代表页面

以上类型都有一组相同的方法用来存和取绑定的对象。

```java
setAttribute(String key,Object value);
getAttribute(String key);  => Object
getAttributeNames(); //获取所有参数的名字
removeAttribute(String key);
```

## 3. 会话和Cookie

> HTTP协议是一种无状态的协议，所以，对于服务器来说，每一个客户的每一次请求都是”全新的“，服务端从协议层面上不会”识破“客户端。
>
> 但有些应用，必须要求服务端能”识别“客户端，现在可以通过一种”会话跟踪技术“来做到这一点。
>
> 这个会话跟踪技术有两种实现方式：
>
> 1. 基于Cookie实现
> 2. 基于URL重写来实现

### 3.1 Cookie

> 在浏览器端，可以存储服务端发送过来的一些信息，这些信息以Cookie方式来存储。
>
> 原理如下：
>
> 1. 第一次请求，服务端会产生一个Cookie，并生成唯一性id[JSESSIONID]存放在cookie中，并通过响应头写回到浏览器端。**注：服务端会维护所有生成的Cookie的列表**
> 2. 浏览器拿到服务端发送过来的这个Cookie，可以接收也可以不接收，用户可以在浏览器中进行设置，默认都是接受的。
> 3. 以后每一次再发请求到服务端时，自动通过请求头把这个Cookie发回到服务端，服务端会维护每一个服务端的Cookie，这样依赖，就可以通过比对，去识别客户端。

### 3.2 Session

> 就是一种会话跟踪技术，基于cookie来实现
>
> 当我们在服务端开启Session后【通过request.getSession()】，容器会自动创建一个名为JSESSIONID的cookie，它的value是一串唯一性字符串。
>
> 并把这个cookie通过响应写回到浏览器，浏览器接收到cookie后，以后的每一次请求都会自动发回这个cookie，这样一来，服务端通过这个cookie的JSESSIONID就可以识别这个客户端，从而达到会话跟踪的目的。

1. 开启Session的方法

   * 调用request.getSession(boolean create)方法

     此方法参数表示：

     当create为true时，如果此请求之前已经有了session，则返回之前的存在的session，如果之前没有session，则创建一个新的session

     当create为false时，如果此请求之前没有session，则返回null，如果之前已经存在了session，则返回之前的session。

     **注：request.getSession()与request.getSession(true)的结果一样**

     **而request.getSession(false)表示，有就返回之前的，没有就返回null**

     **当我们访问了服务端的jsp资源时，就会自动创建session**

2. session适合管理的资源

   * 跨请求的资源/对象，比如：登录的用户、购物车



## 4.  异步Servlet处理

### 4.1 异步处理API

**AsyncContext 异步上下文**

1. 在Servlet的@WebServlet注解中，要开启异步支持，使用asyncSupported = true
2. 在service方法中，通过request.startAsync()方法获取异步上下文对象
3. 调度新的线程来执行异步操作，有如下方法：
   1. 异步上下文对象的start()方法，申请一个线程执行异步操作【Tomcat的实现就是从线程池拿另一个线程来执行，所以不太可取】
   2. 我们重新创建一个新线程来服务
   3. 我们自定义一个线程池来服务

#### 4.1.1 `*` 有关线程池

> 在JDK的java.util.concurrent包中，提供了一些获取线程池的方法以及执行任务的操作。主要涉及到如下类型
>
> * ThreadPoolExecutor [C] 实现类ExecutorService接口
> * Excutors [C] 工具类，里面有很多工具方法来获取**ExecutorService**对象

#### 4.1.2  有关Servlet的输入输出流

> 在Servlet3.0中，虽然引入了异步操作，但是，输入【request.getInputStream】和输出流【response.getOutputStream】还是基于阻塞的，这样的话，同样会影响主线程回到线程池的效率。
>
> 基于这个原因，在Servlet3.1中引入了非阻塞的输入和输出流，前提是基于异步的上下文Servlet

针对输入流操作，提供了ReadListener接口和WriteListener接口

通过InputSteamListener.setReadListener(ReadListener listener) 来绑定一个读操作的监听事件    

### 4.2  Servlet文件上传下载

> 早期的Servlet规范中，没有文件上传的支持组件，需要利用第三方的技术组件，如：apache-filepuload组件。
>
> 现在，Servlet3.0中，提供了Part接口，可以直接做文件的上传操作，而无需提供第三方的技术组件。

#### 4.2.1  文件上传编码的过程

1. 在前端页面的上传表单中，一定要加enctype='multipart/form-data'属性。
2. 在后端的Servlet中，要打上@MultipartConfig注解
3. 在代码中通过request.getPart("上传组件的name值")；或reques.getParts();  获取Part实例
4. 通过Part完成上传

#### 4.2.2 文件的下载

1. 通过请求参数获取客户端要下载的文件，同时要定位到我们在服务端的下载目录。

2. 设置响应头：

   ```java
   //不缓存数据时，要设置的响应头
   response.setHeader("Pragma","No-cache");
   response.setHeader("Cache-Control","No-chche");
   response.setHeader("Expires",-1);
   
   response.setContentType("");
   //设置Http响应头，告诉浏览器以下载的方式处理我们的响应信息
   response.setHeader("content-dispostion","attachment;filename="+fileName);
   ```

3. 通过IO流完成由服务端向客户端输出

   ```java
   response.getOutputSteam();
   ```

## 5. Filter

> 过滤器，与Servlet一样，也是Servlet规范中的组件

### 5.1 开发Filter

1. 写一个类实现Filter接口
2. 重写Filter接口的三个方法
   1. init(Config config)
   2. doFilter(ServletRequest req,ServletResponse resp,FilterChain chain)
   3. destory()
3. 我们需要在doFilter中进行逻辑判断，以决定让请求是否通过这个Filter，如果让其通过，则调用chain.doFilter()方法，如果不想让其通过，可以响应输出或者重定向、跳转、sendError()

### 5.2 Filter的作用

> 对请求进行拦截/过滤；如：对请求和响应进行编码设置、用户认证（授权）、日志、审核、关键词过滤以及对请求和响应的包装....

