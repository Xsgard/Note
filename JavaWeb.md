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

#### 2.0.1 容器处理浏览器的响应

> 容器会维护一个核心线程池，每当一个请求来到时，容器就会派出一个线程去响应客户的请求，也就是调用目标Servlet的service方法。当service方法执行完成后，这个线程就会回到线程池。
>
> 所以，在容器面对高并发时，就会有可能造成核心线程池种分配不出线程来响应客户，只能等待它的service方法执行完成后，线程回到核心线程池，再来响应新的请求。

#### 2.0.2 请求转发和重定向

**转发**

> 它是发生在服务端，由服务端决定把这个请求从一个资源上转发到另一个资源上去。Servlet规范中专门定义了请求转发的接口：RequestDispatcher

