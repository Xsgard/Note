# 0 Spring Cloud

#### 0.1 微服务调用方式

1. ‌基于RestTemplate发起的http请求实现远程调用
2. ‌http请求做远程调用是与语言无关的调用，只要知道对方的ip、端口、接口路径、请求参数即可。



## 1.1.0 Eureka

#### 1.1.1 eureka的作用

![eureka1](C:\Users\Asgard\Desktop\myNote\assets\eureka1.jpeg)

![eureka2](C:\Users\Asgard\Desktop\myNote\assets\eureka2.jpeg)

#### 1.1.2 Eureka注册中心

![2462e34e3150ef77743393faacbdf9241e58bfc8](C:\Users\Asgard\Desktop\myNote\assets\2462e34e3150ef77743393faacbdf9241e58bfc8.jpeg)



![a77483271797fa8752da3d1e05c6dc6ddde1e772](C:\Users\Asgard\Desktop\myNote\assets\a77483271797fa8752da3d1e05c6dc6ddde1e772-1678521553187.jpeg)



![421d3ff543198ff2efef78d40cdeed29ae9d051b](C:\Users\Asgard\Desktop\myNote\assets\421d3ff543198ff2efef78d40cdeed29ae9d051b.jpeg)

#### 1.1.3 Eureka总结

![ee84d4f874c0baac66b1b4dbdf9d9396a5ea0784](C:\Users\Asgard\Desktop\myNote\assets\ee84d4f874c0baac66b1b4dbdf9d9396a5ea0784.jpeg)



### 1.2.0 Ribbon负载均衡

##### 1.2.1 负载均衡流程

![3ae95cc1149e7a257d8dc5e0bb56b87737189cf2](C:\Users\Asgard\Desktop\myNote\assets\3ae95cc1149e7a257d8dc5e0bb56b87737189cf2.jpeg)

![e3db08b5e6a0bc66f8e52b4878c485fd59a353ae](C:\Users\Asgard\Desktop\myNote\assets\e3db08b5e6a0bc66f8e52b4878c485fd59a353ae.jpeg)



##### 1.2.2 负载均衡策略

![5a21a979457aa19783cc1a881866ca02d637cf10](C:\Users\Asgard\Desktop\myNote\assets\5a21a979457aa19783cc1a881866ca02d637cf10.jpeg)



1.通过Bean注入负载均衡规则（作用于当前服务全局） 2.通过yml配置负载均衡规则

![09ac0c0601ffffcde47323925f91940d9b288362](C:\Users\Asgard\Desktop\myNote\assets\09ac0c0601ffffcde47323925f91940d9b288362-1678521896223.jpeg)

默认为懒加载

![84cf365b859ebb57f6bcc4346cd574e8cf7f2802](C:\Users\Asgard\Desktop\myNote\assets\84cf365b859ebb57f6bcc4346cd574e8cf7f2802.jpeg)



##### 1.2.3 Ribbon负载均衡总结

![df09e8450e35cab21ac4ba37d72015b98185e613](C:\Users\Asgard\Desktop\myNote\assets\df09e8450e35cab21ac4ba37d72015b98185e613.jpeg)



### 1.3.0 Nacos注册中心

##### 1.3.1 Nacos服务搭建

![5aa4070d2bd9ff21afaef7cea46d240c642d4346](C:\Users\Asgard\Desktop\myNote\assets\5aa4070d2bd9ff21afaef7cea46d240c642d4346.jpeg)

##### 1.3.2 Nacos服务分级模型

![8c3c5abb25cc9e9f53d3fa48c7d6689a498075ed](C:\Users\Asgard\Desktop\myNote\assets\8c3c5abb25cc9e9f53d3fa48c7d6689a498075ed.jpeg)

##### 1.3.3 Nacos负载均衡策略

![c48c88341690d1656fc30fb234d15cab3ffe3810](C:\Users\Asgard\Desktop\myNote\assets\c48c88341690d1656fc30fb234d15cab3ffe3810.jpeg)

##### 1.3.4 根据权重负载均衡

![9a02c54571f64fffd5606b062ffc2053d7cf1565](C:\Users\Asgard\Desktop\myNote\assets\9a02c54571f64fffd5606b062ffc2053d7cf1565.jpeg)

![ed33113a5143d399b0957951e892c06bf5db0fbd](C:\Users\Asgard\Desktop\myNote\assets\ed33113a5143d399b0957951e892c06bf5db0fbd.jpeg)

##### 1.3.5 环境隔离-namespace

![1af857716ae4c0eeb733351c173c239a89e74a43](C:\Users\Asgard\Desktop\myNote\assets\1af857716ae4c0eeb733351c173c239a89e74a43.jpeg)



##### 1.3.6 Nacos注册中心细节分析

![8561cc4b187de597bf0cf42e8ebc4112fd7fde15](C:\Users\Asgard\Desktop\myNote\assets\8561cc4b187de597bf0cf42e8ebc4112fd7fde15.jpeg)



##### 1.3.7 临时实例和非临时实例

![15f23afd5ed1b462e29bc85697c658be992f03db](C:\Users\Asgard\Desktop\myNote\assets\15f23afd5ed1b462e29bc85697c658be992f03db.jpeg)



#### 1.3.8 Nacos和Eureka的区别

![eb6c61c58a205e51573db6918880fde661534d6c](C:\Users\Asgard\Desktop\myNote\assets\eb6c61c58a205e51573db6918880fde661534d6c.jpeg)



### 1.4.0 Naco配置管理

##### 1.4.1 统一配置管理

![07e37cf3fcc014a04f8e11903c516fd789167269](C:\Users\Asgard\Desktop\myNote\assets\07e37cf3fcc014a04f8e11903c516fd789167269.jpeg)

![66e3c3bea18560bf30708e189939387d4edd0971](C:\Users\Asgard\Desktop\myNote\assets\66e3c3bea18560bf30708e189939387d4edd0971.jpeg)



##### 1.4.2 配置自动刷新

方式1：@Value注入的变量所在类上添加注解@RefreshScope

方式2：@ConfigurationProperties注解

![6d6643bfaf3a4315565ad796981703c92e3b385f](C:\Users\Asgard\Desktop\myNote\assets\6d6643bfaf3a4315565ad796981703c92e3b385f.jpeg)

![755d57fca8cb86766840df8e8cdcebf32f1e9264](C:\Users\Asgard\Desktop\myNote\assets\755d57fca8cb86766840df8e8cdcebf32f1e9264.jpeg)

![3a0e5ac60820156e78a45dce2260f43981e1896d](C:\Users\Asgard\Desktop\myNote\assets\3a0e5ac60820156e78a45dce2260f43981e1896d.jpeg)



##### 1.4.3 多环境配置共享

![0c47a4640c53c44272199a4c2de701c2f36d212e](C:\Users\Asgard\Desktop\myNote\assets\0c47a4640c53c44272199a4c2de701c2f36d212e.jpeg)

![8a7d0f5488e238f3d9d1a0f26a665f21cdc07e93](C:\Users\Asgard\Desktop\myNote\assets\8a7d0f5488e238f3d9d1a0f26a665f21cdc07e93.jpeg)

优先级：服务名-环境.yaml >服务名.yaml >本地配置

![f9fd8b78cd22e6f81099765f31c85049111d391e](C:\Users\Asgard\Desktop\myNote\assets\f9fd8b78cd22e6f81099765f31c85049111d391e.jpeg)



##### 1.4.4 Nacos集群搭建

![bfe49020b5f40e015e46912de40af6d0ae8a09ad](C:\Users\Asgard\Desktop\myNote\assets\bfe49020b5f40e015e46912de40af6d0ae8a09ad.jpeg)



## 2.0.0 Fegin

##### 2.0.1自定义fegin的配置

![0ba2ae09ade5b69250b526dfab1a96fcfcd599be](C:\Users\Asgard\Desktop\myNote\assets\0ba2ae09ade5b69250b526dfab1a96fcfcd599be.jpeg)

![3e4890d619d3dadd3beea6d3a53a75c049e01cd1](C:\Users\Asgard\Desktop\myNote\assets\3e4890d619d3dadd3beea6d3a53a75c049e01cd1.jpeg)

![a81d931d3fa9922f1d5d6541452900fb6a48e580](C:\Users\Asgard\Desktop\myNote\assets\a81d931d3fa9922f1d5d6541452900fb6a48e580.jpeg)

![1678523815656](C:\Users\Asgard\Desktop\myNote\assets\1678523815656.png)

### 2.1.0 HTTP客户端Feign

#### 2.1.1 Fiegn性能优化

![1678524018461](C:\Users\Asgard\Desktop\myNote\assets\1678524018461.png)



##### 2.1.2 Feign性能优化-连接池优化

Feign添加HttpClient的支持：

引入依赖：

```xml
<!--HttpClient依赖-->
        <dependency>
            <groupId>io.github.openfeign</groupId>
            <artifactId>feign-httpclient</artifactId>
        </dependency>
```

配置连接池：

```yaml
feign:
  client:
  	config:
  		defult: # 全局配置
  			LoggerLevel: Bastic # 日志级别 Bastic就是基本的请求和响应信息
  httpclient:
    enabled: true # 支持HttpClient开关
    max-connections: 200 #  最大连接数
    max-connections-per-route: 50 # 单个路径的最大连接数
```

![1678525105088](C:\Users\Asgard\Desktop\myNote\assets\1678525105088.png)



##### 2.1.3 Feign的最佳实践

方式一（继承）：给消费者的FeignClient和提供者的Controller提供统一的父接口作为标准。

![1678525740566](C:\Users\Asgard\Desktop\myNote\assets\1678525740566.png)

方式二（抽取）：将FeignClient抽取为独立的模块，并把接口有关的POJO、默认的Feign的配置都放到这个模块中，提供给消费者使用。

![1678526014242](C:\Users\Asgard\Desktop\myNote\assets\1678526014242.png)

![1678526100623](C:\Users\Asgard\Desktop\myNote\assets\1678526100623.png)



##### 2.1.4 抽取FeignClient

**实现抽取FeignClient步骤：**

![1678526249337](C:\Users\Asgard\Desktop\myNote\assets\1678526249337.png)

当定义的FeignClient不在SpringBootApplication的扫描包范围时，这些FeignClient无法使用。有两种解决方案：

方式一：指定FeignClient所在包

```java
@EnableFeignClients(basePackages="cn.itcast.feign.client")
```

方式二：指定FeignClient的字节码

```java
@EnableFeignClients(clients={UserClients.calss})
```



![1678529049777](C:\Users\Asgard\Desktop\myNote\assets\1678529049777.png)



## 3.0.0 统一网关Geteway

##### 3.0.1 网关功能：

1. 身份认证和权限校验
2. 服务路由、负载均衡
3. 请求限流

##### 3.0.2 网关技术实现：

![1678617971461](C:\Users\Asgard\Desktop\myNote\assets\1678617971461.png)

### 3.1.0 搭建网关步骤：

1. 创建新的module，引入SpringCloudGateway的依赖和nacos服务发现依赖：

   ```xml
   <!--网关gateway依赖-->
           <dependency>
               <groupId>org.springframework.cloud</groupId>
               <artifactId>spring-cloud-starter-gateway</artifactId>
           </dependency>
           <!--nacos服务注册发现依赖-->
           <dependency>
               <groupId>com.alibaba.cloud</groupId>
               <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
           </dependency>
   ```

2. 编写路由地址及nacos地址

   ```yaml
   server:
     port: 10010
   spring:
     application:
       name: gateway
     cloud:
       nacos:
         server-addr: localhost:8848 #nacos地址
       gateway:
         routes:
           - id: user-service #路由标识，必须唯一
             uri: lb://userservice #路由的目标地址
             predicates: # 路由断言，判断请求是否符合规则
               - Path: /user/**  # 路径断言，判断路径是否是以/user开头，如果是则符合
           - id: order-service
             uri: lb://orderservice
             predicates:
               - Path: /order/**
   ```

   ![1678619396399](C:\Users\Asgard\Desktop\myNote\assets\1678619396399.png)

![1678619483806](C:\Users\Asgard\Desktop\myNote\assets\1678619483806.png)

##### 3.1.1 路由断言工厂Route Predicate Factory

![1678619546963](C:\Users\Asgard\Desktop\myNote\assets\1678619546963.png)

![1678619854377](C:\Users\Asgard\Desktop\myNote\assets\1678619854377.png)

##### 3.1.2 路由过滤器GatewayFilter

![1678620357838](C:\Users\Asgard\Desktop\myNote\assets\1678620357838.png)

##### 3.1.3 默认过滤器

```yaml
default-filters:  #默认路由,对全局生效 与routes同级
          - AddRequestHeader=Truth,Itcast is freaking awesome!
```

![1678691129618](C:\Users\Asgard\Desktop\myNote\assets\1678691129618.png)

##### 3.1.4 全局过滤器

![1678692330551](C:\Users\Asgard\Desktop\myNote\assets\1678692330551.png)

1. 自定义过滤器

   自定义类，实现GlobalFilter接口，添加@Order(-1)注解

   ```java
   @Order(-1)
   @Component
   public class AuthorizeFilter implements GlobalFilter {
       @Override
       public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
           //1.获取请求参数
           ServerHttpRequest request = exchange.getRequest();
           MultiValueMap<String, String> params = request.getQueryParams();
           //2.获取参数中的 authorization 参数
           String auth = params.getFirst("authorization");
           //3.判断参数值是否为admin
           if ("admin".equals(auth)) {
               //4.是，放行
               return chain.filter(exchange);
           }
           //5.否，拦截
           //5.1 设置状态码
           exchange.getResponse().setStatusCode(HttpStatus.UNAUTHORIZED);
           //5.2 拦截请求
           return exchange.getResponse().setComplete();
   
       }
   }
   ```

   ![1678692457356](C:\Users\Asgard\Desktop\myNote\assets\1678692457356.png)



##### 3.1.5 过滤器执行顺序

![1678692569793](C:\Users\Asgard\Desktop\myNote\assets\1678692569793.png)

![1678693058681](C:\Users\Asgard\Desktop\myNote\assets\1678693058681.png)

![1678693089699](C:\Users\Asgard\Desktop\myNote\assets\1678693089699.png)

##### 

##### 3.1.6 跨域问题处理

![1678693240391](C:\Users\Asgard\Desktop\myNote\assets\1678693240391.png)

网关处理跨域问题同样采用**CORS**方案，并只需要简单配置即可

```yaml
spring:
  cloud:
    gateway:
      globalcors: # 全局的跨域处理
        add-to-simple-url-handler-mapping: true # 解决options请求被拦截问题
        corsConfigurations:
          '[/**]':
            allowedOrigins: # 允许哪些网站的跨域请求
              - "http://localhost:8090"
              - "http://www.leyou.com"
            allowedMethods: # 允许的跨域ajax的请求方式
              - "GET"
              - "POST"
              - "DELETE"
              - "PUT"
              - "OPTIONS"
            allowedHeaders: "*" # 允许在请求中携带的头信息
            allowCredentials: true # 是否允许携带cookie
            maxAge: 360000 # 这次跨域检测的有效期
```

![1678694638067](C:\Users\Asgard\Desktop\myNote\assets\1678694638067.png)





## 4.0.0 Docker

![1678695223235](C:\Users\Asgard\Desktop\myNote\assets\1678695223235.png)

##### 4.0.1 docker架构

![1678695824935](C:\Users\Asgard\Desktop\myNote\assets\1678695824935.png)

### 4.1.0 Docker基本操作

#### 4.1.1 容器相关命令：

![1678700856234](C:\Users\Asgard\Desktop\myNote\assets\1678700856234.png)

##### 4.1.2 Docker基本操作-容器

###### 案例一：nginx

![1678774706185](C:\Users\Asgard\Desktop\myNote\assets\1678774706185.png)

![1678775264700](C:\Users\Asgard\Desktop\myNote\assets\1678775264700.png)

###### 案例二：nginx

![1678775882755](C:\Users\Asgard\Desktop\myNote\assets\1678775882755.png)

![1678777173079](C:\Users\Asgard\Desktop\myNote\assets\1678777173079.png)

#### 4.2.0 数据卷

**数据卷**（volume）是一个虚拟目录，指向宿主机文件系统中的某个目录。

![1678779141214](C:\Users\Asgard\Desktop\myNote\assets\1678779141214.png)

一旦完成数据卷挂载，对容器的一切操作都会作用在数据卷对应的宿主机目录了。

这样，我们操作宿主机的/var/lib/docker/volumes/html目录，就等于操作容器内的/usr/share/nginx/html目录了

##### 4.2.1 数据卷操作命令

数据卷操作的基本语法如下：

```sh
docker volume [COMMAND]
```

docker volume命令是数据卷操作，根据命令后跟随的command来确定下一步的操作：

- create 创建一个volume
- inspect 显示一个或多个volume的信息
- ls 列出所有的volume
- prune 删除未使用的volume
- rm 删除一个或多个指定的volume

##### 4.2.2创建和查看数据卷

① 创建数据卷

```sh
docker volume create html
```

② 查看所有数据

```sh
docker volume ls
```

③ 查看数据卷详细信息卷

```sh
docker volume inspect html
```

我们创建的html这个数据卷关联的宿主机目录为`/var/lib/docker/volumes/html/_data`目录。



**小结**：

数据卷的作用：

- 将容器与数据分离，解耦合，方便操作容器内数据，保证数据安全

数据卷操作：

- docker volume create：创建数据卷
- docker volume ls：查看所有数据卷
- docker volume inspect：查看数据卷详细信息，包括关联的宿主机目录位置
- docker volume rm：删除指定数据卷
- docker volume prune：删除所有未使用的数据卷



##### 4.2.3.挂载数据卷

我们在创建容器时，可以通过 -v 参数来挂载一个数据卷到某个容器内目录，命令格式如下：

```sh
docker run \
  --name mn \
  -v html:/root/html \
  -p 8080:80
  nginx \
```

这里的-v就是挂载数据卷的命令：

- `-v html:/root/htm` ：把html数据卷挂载到容器内的/root/html这个目录中



###### 案例一：nginx

![1679038554661](C:\Users\Asgard\Desktop\myNote\assets\1679038554661.png)

![1679038592173](C:\Users\Asgard\Desktop\myNote\assets\1679038592173.png)



###### 案例二：mysql

![1679045443475](C:\Users\Asgard\Desktop\myNote\assets\1679045443475.png)

##### 4.2.4 数据卷挂载方式对比

![1679045490879](C:\Users\Asgard\Desktop\myNote\assets\1679045490879.png)

![1679045574657](C:\Users\Asgard\Desktop\myNote\assets\1679045574657.png)

#### 4.3.0 DockerFile自定义镜像

##### 4.3.1 镜像结构

镜像是将应用程序及其需要的系统函数库、环境、配置、依赖打包而成。

![1679045952942](C:\Users\Asgard\Desktop\myNote\assets\1679045952942.png)



###### 案例一：

![1679046187638](C:\Users\Asgard\Desktop\myNote\assets\1679046187638.png)

![1679047072513](C:\Users\Asgard\Desktop\myNote\assets\1679047072513.png)



#### 4.4.0 DockerCompose

![1679047867564](C:\Users\Asgard\Desktop\myNote\assets\1679047867564.png)



##### 4.4.1 镜像服务器

![1679051503889](C:\Users\Asgard\Desktop\myNote\assets\1679051503889.png)

![1679051445921](C:\Users\Asgard\Desktop\myNote\assets\1679051445921.png)





## 5.0.0 服务异步通讯

#### 5.1.0 初识MQ

- 同步通讯

  **同步调用存在的问题：**

  ![1679120584904](C:\Users\Asgard\Desktop\myNote\assets\1679120584904.png)
  
  

- 异步通讯

  **事件驱动优势：**

  ​	**优势一**：服务解耦

  ​	**优势二**：性能提升，吞吐量提高

  ​	**优势三**：服务没有强依赖，不必担心级联失败问题

  ​	**优势四**：流量削峰

  ![1679295844400](C:\Users\Asgard\Desktop\myNote\assets\1679295844400.png)

- MQ常见框架

  ![1679296255654](C:\Users\Asgard\Desktop\myNote\assets\1679296255654.png)



#### 5.2.0RabbitMQ

##### 	5.2.1了解RabbitMQ

![1679297339570](C:\Users\Asgard\Desktop\myNote\assets\1679297339570.png)

![1679297389349](C:\Users\Asgard\Desktop\myNote\assets\1679297389349.png)



##### 5.2.2常见消息模型

![1679297605698](C:\Users\Asgard\Desktop\myNote\assets\1679297605698.png)



**HelloWorld案例：**	

​	![1679297729503](C:\Users\Asgard\Desktop\myNote\assets\1679297729503.png)

![1679298900483](C:\Users\Asgard\Desktop\myNote\assets\1679298900483.png)



#### 5.3.0 Spring AMQP

##### 5.3.1什么是SpringAMQP

![1679299178549](C:\Users\Asgard\Desktop\myNote\assets\1679299178549.png)

​	

**案例：利用SpringAMQP实现HelloWorld中的基础消息队列功能**

![1679299700534](C:\Users\Asgard\Desktop\myNote\assets\1679299700534.png)

步骤：

1. 引入AMQP依赖

   ```xml
   		<!--AMQP依赖，包含RabbitMQ-->
           <dependency>
               <groupId>org.springframework.boot</groupId>
               <artifactId>spring-boot-starter-amqp</artifactId>
           </dependency>
   ```

2. 在publisher中编写测试方法，向simple.queue发送消息

   `在publisher服务中编写application.yml,添加连接信息`

   ```yaml
   spring:
     rabbitmq:
       addresses: 192.168.52.128 #rabbitMQ IP地址
       port: 5672  #端口号
       username: root
       password: root
       virtual-host: / #虚拟主机
   ```

   在publisher服务中新建一个测试类，编写测试方法

   ```java
   @Test
       public void testSendMessage2SimpleQueue() {
           String queueName = "simple.queue";
           String message = "hello, spring amqp!";
           rabbitTemplate.convertAndSend(queueName, message);
       }
   ```

3. 在consumer中编写消费逻辑，监听simple.queue

   `在consumer服务中编写application.yml,添加连接信息`

   ```yaml
   spring:
     rabbitmq:
       addresses: 192.168.52.128 #rabbitMQ IP地址
       port: 5672  #端口号
       username: root
       password: root
       virtual-host: / #虚拟主机
   ```

   `在consumer服务中新建一个类，编写消费逻辑`

   ```java
   @Component
   public class SpringMQListener {
       @RabbitListener(queues = "simple.queue")
       public void listenSimpleQueue(String msg) {
           System.out.println("消费者接收到simple.queue的消息：【" + msg + "】");
       }
   }
   ```



![1679300933831](C:\Users\Asgard\Desktop\myNote\assets\1679300933831.png)

![1679301713009](C:\Users\Asgard\Desktop\myNote\assets\1679301713009.png)



##### 5.3.2 Work Queue工作队列

Work Queue，工作队列，可以提高消息处理速度，避免消息队列堆积

![1679302255488](C:\Users\Asgard\Desktop\myNote\assets\1679302255488.png)

1. 生产者循环发送消息到simple.queue

   在publisher服务中添加一个测试方法，循环发送50条消息到simple.queue队列

   ```java
   @Test
       public void testSendMessage2WorkQueue() throws InterruptedException {
           String queueName = "simple.queue";
           String message = "hello, spring amqp!";
   
           for (int i = 1; i <= 50; i++) {
               rabbitTemplate.convertAndSend(queueName, message + i);
               Thread.sleep(20);
           }
       }
   ```

2. 编写两个消费者，都监听simple.queue

   在consumer中添加一个消费者，也监听simple.queue

   ```java
   @RabbitListener(queues = "simple.queue")
       public void listenWorkQueue1(String msg) throws InterruptedException {
           System.out.println("消费者1接收到simple.queue的消息：【" + msg + "】"+ LocalDateTime.now());
           Thread.sleep(20);
       }
   
       @RabbitListener(queues = "simple.queue")
       public void listenWorkQueue2(String msg) throws InterruptedException {
           System.err.println("消费者2接收到simple.queue的消息：【" + msg + "】"+LocalDateTime.now());
           Thread.sleep(200);
       }
   ```

   **消费预取限制：**

   修改application.yml文件，设置preFetch的值，可以控制预取消息的上限

   ```yaml
   spring:
     rabbitmq:
       addresses: 192.168.52.128 #rabbitMQ IP地址
       port: 5672  #端口号
       username: root
       password: root
       virtual-host: / #虚拟主机
       listener:
         simple:
           prefetch: 1 #消息预取，每次只取一条消息，处理完成才能获取到下一条消息
   ```



##### 5.3.3 发布（publish）、订阅（subscribe）

![1679304072890](C:\Users\Asgard\Desktop\myNote\assets\1679304072890.png)



##### 5.3.4 发布订阅--Fanout Exchange

![1679304182131](C:\Users\Asgard\Desktop\myNote\assets\1679304182131.png)



![1679304239245](C:\Users\Asgard\Desktop\myNote\assets\1679304239245.png)

SpringAMQP提供了声明交换机、队列、绑定关系的API，例如：

![1679304426383](C:\Users\Asgard\Desktop\myNote\assets\1679304426383.png)

1. 在consumer服务中声明Exchange、Queue、Binding

   `在consumer服务创建一个类，添加@Configuration注解，并声明FanoutExchange、Queue和绑定关系对象Binding`

   ```java
   @Configuration
   public class FanoutConfig {
   
       //itcast.fanout
       @Bean
       public FanoutExchange fanoutExchange() {
           return new FanoutExchange("itcast.fanout");
       }
   
       //fanout.queue1
       @Bean
       public Queue fanoutQueue1() {
           return new Queue("fanout.queue1");
       }
   
       //绑定队列1到交换机
       @Bean
       public Binding fanoutBinding1(FanoutExchange fanoutExchange, Queue fanoutQueue1) {
           return BindingBuilder.bind(fanoutQueue1).to(fanoutExchange);
       }
   
       //fanout.queue2
       @Bean
       public Queue fanoutQueue2() {
           return new Queue("fanout.queue2");
       }
   
       //绑定队列2到交换机
       @Bean
       public Binding fanoutBinding2(FanoutExchange fanoutExchange, Queue fanoutQueue2) {
           return BindingBuilder.bind(fanoutQueue2).to(fanoutExchange);
       }
   
   }
   ```

2. 在consumer声明两个消费者

   ```Java
     @RabbitListener(queues = "fanout.queue1")
       public void listenFanoutQueue1(String msg) throws InterruptedException {
           System.out.println("消费者1接收到fanout.queue1的消息：【" + msg + "】"+LocalDateTime.now());
       }
   
       @RabbitListener(queues = "fanout.queue2")
       public void listenFanoutQueue2(String msg) throws InterruptedException {
           System.err.println("消费者2接收到fanout.queue2的消息：【" + msg + "】"+LocalDateTime.now());
       }
   ```

3. 在publisher服务发送消息到fanout.Exchange

   ```Java
    @Test
       public void testFanoutExchange() {
           String exchangeName = "itcast.fanout";
           String message = "hello every one!";
           rabbitTemplate.convertAndSend(exchangeName, "", message);
       }
   ```



##### 5.3.5 发布订阅--Direct Exchange

![1679306941024](C:\Users\Asgard\Desktop\myNote\assets\1679306941024.png)

![1679307133699](C:\Users\Asgard\Desktop\myNote\assets\1679307133699.png)

1. 在customer服务声明Exchange、Queue

   `在customer服务中，编写两个消费方法，分别监听direct.queue1和direct.queue2`

   `利用@RabbitListener声明Exchange、Queue、RoutingKey`

   ```java
   @RabbitListener(bindings = @QueueBinding(
               value = @Queue(name = "direct.queue1"),
               exchange = @Exchange(name = "itcast.direct", type = ExchangeTypes.DIRECT),
               key = {"red", "blue"}
       ))
       public void listenDirectQueue1(String msg) {
           System.err.println("消费者接收到direct.queue1的消息：【" + msg + "】");
       }
   
       @RabbitListener(bindings = @QueueBinding(
               value = @Queue(name = "direct.queue2"),
               exchange = @Exchange(name = "itcast.direct", type = ExchangeTypes.DIRECT),
               key = {"red", "yellow"}
       ))
       public void listenDirectQueue2(String msg) {
           System.err.println("消费者接收到direct.queue2的消息：【" + msg + "】");
       }
   ```

2. 在publisher服务发送消息到direct.Exchange

   ```java
    @Test
       public void testDirectExchange() {
           String exchangeName = "itcast.direct";
           String message = "hello red";
           rabbitTemplate.convertAndSend(exchangeName, "red", message);
       }
   ```



##### 5.3.6 发布订阅--Topic Exchange

![1679308411146](C:\Users\Asgard\Desktop\myNote\assets\1679308411146.png)



![1679308467980](C:\Users\Asgard\Desktop\myNote\assets\1679308467980.png)

1.   在customer服务声明Exchange、Queue

   `在customer服务中，编写两个消费方法，分别监听topic.queue1和topic.queue2`

   `利用@RabbitListener声明Exchange、Queue、RoutingKey`

   ```java
   @RabbitListener(bindings = @QueueBinding(
               value = @Queue(value = "topic.queue1"),
               exchange = @Exchange(value = "itcast.topic",type = ExchangeTypes.TOPIC),
               key = "china.#"
       ))
       public void listenTopicQueue1(String msg) {
           System.err.println("消费者接收到topic.queue1的消息：【" + msg + "】");
       }
   
       @RabbitListener(bindings = @QueueBinding(
               value = @Queue(value = "topic.queue2"),
               exchange = @Exchange(value = "itcast.topic",type = ExchangeTypes.TOPIC),
               key = "#.news"
       ))
       public void listenTopicQueue2(String msg) {
           System.err.println("消费者接收到topic.queue2的消息：【" + msg + "】");
       }
   ```

2. 在publisher服务发送消息到topic.Exchange

   ```java
   @Test
       public void testTopicExchange() {
           String exchangeName = "itcast.topic";
           String message = "局部晴朗!";
           rabbitTemplate.convertAndSend(exchangeName, "china.weather", message);
       }
   ```



##### 5.3.6 SpringAMQP--消息转换器

![1679309626800](C:\Users\Asgard\Desktop\myNote\assets\1679309626800.png)

![1679309762278](C:\Users\Asgard\Desktop\myNote\assets\1679309762278.png)

![1679309888248](C:\Users\Asgard\Desktop\myNote\assets\1679309888248.png)





## 6.0.0 分布式搜索

##### 6.0.1 初识 elasticsearch

![1679374581570](C:\Users\Asgard\Desktop\myNote\assets\1679374581570.png)



##### 6.0.2 正向索引和倒排索引

![1679374755423](C:\Users\Asgard\Desktop\myNote\assets\1679374755423.png)

![1679382081710](C:\Users\Asgard\Desktop\myNote\assets\1679382081710.png)



##### 6.0.3 分词器

![1679466551398](C:\Users\Asgard\Desktop\myNote\assets\1679466551398.png)

**ik分词器-停用词库**

![1679468244533](C:\Users\Asgard\Desktop\myNote\assets\1679468244533.png)



##### 6.0.4 索引库操作

- **mapping属性**

  ![1679468792058](C:\Users\Asgard\Desktop\myNote\assets\1679468792058.png)

![1679468851062](C:\Users\Asgard\Desktop\myNote\assets\1679468851062.png)



- **创建索引库**

  ![1679469024139](C:\Users\Asgard\Desktop\myNote\assets\1679469024139.png)

  

- **查看删除索引库**

  > 查看索引库语法：

  ​	`GET /索引库名`

  > 删除索引库语法：

  ​	`DELETE /索引库名`

- **修改索引库**

  ![1679470318825](C:\Users\Asgard\Desktop\myNote\assets\1679470318825.png)



##### 6.0.5 文档操作

- 新增文档

  ![1679471458779](C:\Users\Asgard\Desktop\myNote\assets\1679471458779.png)

- 查询文档

  ![1679471418507](C:\Users\Asgard\Desktop\myNote\assets\1679471418507.png)

- 删除文档

  ![1679471432998](C:\Users\Asgard\Desktop\myNote\assets\1679471432998.png)

- 修改文档

  ![1679471688559](C:\Users\Asgard\Desktop\myNote\assets\1679471688559.png)

![1679471792927](C:\Users\Asgard\Desktop\myNote\assets\1679471792927.png)



#### 6.1.0 RestClient

##### 6.1.1 操作索引库

- 创建索引库

  ```Java
  @Test
      void createHotelIndex() throws IOException {
          //1.创建Request对象
          CreateIndexRequest request = new CreateIndexRequest("hotel");
          //2.准备请求参数，DSL语句
          request.source(MAPPING_TEMPLATE, XContentType.JSON);
          //3.发送请求
          client.indices().create(request, RequestOptions.DEFAULT);
      }
  ```

- 删除索引库

  ```Java
  @Test
      void testDeleteHotelIndex() throws IOException {
          DeleteIndexRequest request = new DeleteIndexRequest("hotel");
          client.indices().delete(request, RequestOptions.DEFAULT);
      }
  ```

- 判断索引库是否存在

  ```Java
   @Test
      void testExistHotelIndex() throws IOException {
          GetIndexRequest request = new GetIndexRequest("hotel");
          boolean exists = client.indices().exists(request, RequestOptions.DEFAULT);
          System.out.println(exists ? "索引库已存在！" : "索引库不存在！");
      }
  ```



##### 6.1.2 操作文档

- 新增文档

  ```Java
  @Test
      void testAddDocument() throws IOException {
          Hotel hotel = hotelService.getById(36934L);
          HotelDoc hotelDoc = new HotelDoc(hotel);
  
          IndexRequest request = new IndexRequest("hotel").id(hotel.getId().toString());
          request.source(JSON.toJSONString(hotelDoc), XContentType.JSON);
  
          client.index(request, RequestOptions.DEFAULT);
      }
  ```

  

- 查询文档

  ```Java
  @Test
      void testGetDocumentById() throws IOException {
          //1.准备request
          GetRequest request = new GetRequest("hotel", "36934");
          //2.发送请求，得到响应
          GetResponse response = client.get(request, RequestOptions.DEFAULT);
          //3.解析响应结果
          String json = response.getSourceAsString();
          HotelDoc hotelDoc = JSON.parseObject(json, HotelDoc.class);
          System.out.println(hotelDoc);
      }
  ```

  

- 更新文档

  ```Java
   @Test
      void testUpdateDocument() throws IOException {
          //1.准备request
          UpdateRequest request = new UpdateRequest("hotel", "36934");
          //2.准备请求参数
          request.doc(
                  "price", "380",
                  "starName", "三钻"
          );
          //3.发送请求
          client.update(request, RequestOptions.DEFAULT);
      }
  ```

  

- 删除文档

  ```Java
  @Test
      void testDeleteDocument() throws IOException {
          DeleteRequest request = new DeleteRequest("hotel", "36934");
          client.delete(request, RequestOptions.DEFAULT);
      }
  ```

- 批量导入文档

  ```Java
  @Test
      void testBulkRequest() throws IOException {
          //获取hotel数据
          List<Hotel> hotels = hotelService.list();
  		//创建request
          BulkRequest request = new BulkRequest();
          for (Hotel hotel : hotels) {
              //转换为文档类型
              HotelDoc hotelDoc = new HotelDoc(hotel);
              //创建新增文档的request对象
              request.add(new IndexRequest("hotel")
                      .id(hotelDoc.getId().toString())
                      .source(JSON.toJSONString(hotelDoc), XContentType.JSON));
          }
  		//批处理提交请求
          client.bulk(request, RequestOptions.DEFAULT);
      }
  ```




#### 6.2.0 elasticSearch搜索功能

##### 6.2.1DSL 查询文档

​	**DSL Query的分类**

![1679552927256](C:\Users\Asgard\Desktop\myNote\assets\1679552927256.png)

![1679553215756](C:\Users\Asgard\Desktop\myNote\assets\1679553215756.png)

​	

##### 6.2.2 全文检索查询

![1679557253909](C:\Users\Asgard\Desktop\myNote\assets\1679557253909.png)

![1679557317626](C:\Users\Asgard\Desktop\myNote\assets\1679557317626.png)



##### 6.2.3 精确查询

![1679557779342](C:\Users\Asgard\Desktop\myNote\assets\1679557779342.png)

![1679557802349](C:\Users\Asgard\Desktop\myNote\assets\1679557802349.png)



##### 6.2.4 地理查询

![1679557843898](C:\Users\Asgard\Desktop\myNote\assets\1679557843898.png)



![1679557915231](C:\Users\Asgard\Desktop\myNote\assets\1679557915231.png)

##### 6.2.5 符合查询

​	**相关性算分**

![1679558912818](C:\Users\Asgard\Desktop\myNote\assets\1679558912818.png)

![1679559003750](C:\Users\Asgard\Desktop\myNote\assets\1679559003750.png)



###### 	Function Score Query

![1679559275999](C:\Users\Asgard\Desktop\myNote\assets\1679559275999.png)

###### 	Boolean Query

![1679559793401](C:\Users\Asgard\Desktop\myNote\assets\1679559793401.png)

![1679560043602](C:\Users\Asgard\Desktop\myNote\assets\1679560043602.png)

##### 6.2.6 搜索结果处理

- **排序**

  ![1679560277438](C:\Users\Asgard\Desktop\myNote\assets\1679560277438.png)

- **分页**

  ![1679560755464](C:\Users\Asgard\Desktop\myNote\assets\1679560755464.png)

- **深度分页问题**

  ![1679560934165](C:\Users\Asgard\Desktop\myNote\assets\1679560934165.png)

  ![1679561198811](C:\Users\Asgard\Desktop\myNote\assets\1679561198811.png)

- **高亮**

  ![1679561792304](C:\Users\Asgard\Desktop\myNote\assets\1679561792304.png)

  ![1679561845120](C:\Users\Asgard\Desktop\myNote\assets\1679561845120.png)

#### 6.3.0 RestClient查询文档

##### 快速入门![1679640201848](C:\Users\Asgard\Desktop\myNote\assets\1679640201848.png)

![1679640157879](C:\Users\Asgard\Desktop\myNote\assets\1679640157879.png)



##### 6.3.1 全文检索查询

![1679646711529](C:\Users\Asgard\Desktop\myNote\assets\1679646711529.png)

##### 6.3.2精确查询

![1679646752914](C:\Users\Asgard\Desktop\myNote\assets\1679646752914.png)

#####  6.3.3符合查询-Boolean Query

![1679646817751](C:\Users\Asgard\Desktop\myNote\assets\1679646817751.png)

![1679732381292](C:\Users\Asgard\Desktop\myNote\assets\1679732381292.png)



#### 6.4.0 数据聚合

##### 6.4.1 聚合的分类

![1679899685761](C:\Users\Asgard\Desktop\myNote\assets\1679899685761.png)

![1679899726719](C:\Users\Asgard\Desktop\myNote\assets\1679899726719.png)

