## 1. Servlet

> servlet标准：
>
> 运行在服务器的一种技术组件，是JavaEE的标准，主要是制定了客户端与服务端进行通信处理的一种机制，由WEB服务器负责实现这个标准。比如：Tomcat
>
> Servlet做为JavaEE的一个技术标准，它的规范中定义了大量的接口，主要存放在如下包中：
>
> * javax.servlet 包
> * javax.servlet.http 包

### 1.0.1 Web应用的目录结构

appName/

​				lib/	用来存储此应用所以来的第三方jar包

​				WEB-INF/	存储需要受到容器【web服务器】保护的资源

​								web.xml	用来描述web资源的文件，比如：描述servlet组件[3.0之后，可以替换为注解]

​								classes/	自动生成，用来存放生成的字节码

​								....

​				....	与WEB-INF平级的目录，一般是存放不受容器保护的资源，如：html、css、js 等

### 1.0.2 servlet的定义

>就是一个接口【javax.servlet.Servlet】,它是运行在WEB SERVER中的一小段程序。Servlet与Web Server之间也是一个描述文件的，能通过这个描述文件，程序员要告诉WEB SERVER，你要去管理那些Servlet
>
>这个描述文件就叫：**web.xml**

### 1.0.3 开发servlet

1. 写一个类实现javax.servlet.Servlet接口
2. 重写Servlet接口中的所有方法，主要有：
   * init()	         初始化方法
   * service()；  服务方法
   * destroy()     销毁方法
   * getServletConfig()  获取Servlet的配置信息
   * getServletInfo()      获取Servlet的字符串信息
3. 

