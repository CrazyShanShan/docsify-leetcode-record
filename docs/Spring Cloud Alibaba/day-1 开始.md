2021年10月16日，正式开始学习Spring Cloud Alibaba，种一颗树最好的时间是10年前，其次是现在。

微服务架构现在已经变成一个必备的技能了，我刚入学的时候好像还是SSM框架。

微服务架构： 微服务模块会把很多模块进行拆分，一个又一个多服务器上开启的springboot项目，调用的链路非常复杂。

Spring Cloud： 以微服务为核心的一系列组建，提出了一套标准。

原来的一套架构： Spring Cloud netflix

组件有很多： Nacos、Ribbon/LoadBalancer Feign Sentinel Seate Skywalking

视频2:  

1. 各自服务把自己的启动服务   注册到 服务注册中心Nacos server
2. 订单系统如果要调用库存系统 订单系统通过你的名称去注册中心把你的信息拿到自己的本机
3. 本季通过Ribbon 来进行负载均衡去轮训调用
4. 注册中心可以感知，几秒钟定时和服务端进行通信（心跳任务），然后就在注册表里面删掉
5. Nacos Server，其实都是Server

NACOS要看 1.X之后的版本。

1. nacos能够动态感知服务

2. registerInstance注册，把IP和端口号传递给服务端。

   发起了请求 /nacos/v1/ns/instance

   Http调用 xrequest（url, headers, params, UtilAndComs.ENCODING, method);

   ```yml
   yml文件中指定了cloud的ip和端口号
   cloud:
   	nacos:
   		discovery:
   			# 指定nacosserver的地址
   			server-addr: localhost:8848
   			# 集群名称
   			cluster-name: BJ
   			metadata:
   				version: v3
   ```

1. SpringBoot自动装配原理:

   找到依赖包，可以看到都可以在包下的META-INF文件下会找到spring,factories文件，然后文件中有非常多的配置类，然后这些配置类的上面都会有：

   ```
   org.springframework.boot.autoconfigure.EnableAutoCOnfiguration = \
   ...一系列的
   org.springframework.cloud.bootstrap.BootstrapConfiguration = \
   ```

2. AppllicationListener ：监听器 任何实现了ApplicationListener接口的会回调用一个函数onApplicationEvent这个方法, bind()方法有一个非常核心的方法， start()

3. nacos server注册的核心方法： consistencyService.put(key, instances);

   然后把信息放到了一个阻塞队列里面去了。

4. 从阻塞队列里面取信息放到Set中去了。

Nacos高并发支撑异步任务与内存队列，这个很关键。

Nacos服务组册表结构： Map<namespace, Map<group:serviceName, Service>>

看了一半，这个源码太顶了，学的头痛，草。

那个P2、P3留到后面去看把，顶不住了。





# 1. 微服务介绍

## 1.1 系统架构演变

单体应用架构->垂直应用架构>分布式架构->SOA架构->微服务架构-> Service Mesh（服务网格化）

### 1.1.1 单体应用架构 MVC

all in one：ORM

### 1.1.2 垂直 MVC

流量分担，提升容错率

### 1.1.3 分布式服务 RPC

把公共模块抽取成一个一个服务，然后补充，应用层进行保留

### 1.1.4 SOA 资源调度和治理中心(Service Oriented Architecture)

解决分布式架构中调用非常复杂的问题，采用**治理中心**（ESB \ dubbo)解决了服务间调用关系的自动调节 强耦合

服务间会有依赖关系，一旦某个环节出错会影响较大（服务雪崩）

服务关系复杂，运维、测试部署困难

### 1.1.5 微服务架构

去中心化，但是不会像SOA中是强耦合的

网关：路由到不同的服务当中，不强要求使用

降级： 可以解决服务雪崩的问题

**微服务架构与分布式架构不同点:**


微服务架构在某种程度上是面向服务的架构的SOA继续发展的下一步，本质上也是一种分布式服务，但是拆分的更彻底

**微服务架构与SOA架构的不同：**

微服务架构比SOA架构细粒度更加精细，让专业的人做专业的事情，目的提高效率，每个服务与服务之间互不影响，微服务架构中，每个服务必须独立部署，微服务架构更加轻巧，轻量级。

SOA架构中可能数据库会发生共享，微服务强调每个服务都是单独数据库，保证每个服务与服务之间互不影响。

项目体现特征微服务架构比SOA架构更加适合与互联网公司敏捷开发、快速迭代版本，因为细粒度非常精细。

优点： 服务原子化拆分，独立打包、部署和升级，保证每个微服务清晰的任务划分，利于扩展， 微服务之间采用Restful等轻量级http协议相互调用， SOA采用SOAP。

缺点： 分布式系统开发等技术成本高（学习成本、维护、容错）部署的时候比较麻烦。分布式缓存、分布式锁、分布式事务就很关键了，草，去阿里实习的两个室友强调面试一定要会。麻中麻。

都没有淘汰，都没有完美无缺。

## 1.2 微服务架构介绍

作者： Martin Fowler

扩展时扩展所有的单体机器，会对服务器的性能进行了浪费。

### 1.2.1 微服务架构的常见问题

一旦采用微服务系统架构，就会遇到这样几个问题：

- 小服务，如何进行管理（服务治理 注册中心【服务注册 发现 提出】）

- 小服务，如何进行通讯 httpclient("url", 参数) -> （restful roc dubbo feign） 序列化和反序列化比较麻烦

  springboot 提供了一个工具可以免去序列化和反序列化的问题 restTemplate("url",  参数)

  feign 更加简单直接server.add() 牛逼plus

- 小服务，客户端如何去访问这些服务呢？ 

  通过网关来进行 gatewat

- 小服务，出现问题，如何自处理？

  sentinel

- 小服务，出现问题，如何排错？

  链路追踪,来进行排错和解决  skywalking 

<img src="../../docs/pictures/alibaba cloud.png" alt="image-20211016210159259" style="zoom:50%;" />

### 1.2.2 常见微服务架构

**1. dubbo: zookeeper + dubbo + Springmvc/springboot**

- 通信方式： rpc
- 注册中心： zookeeper/redis
- 配置中心：diamond

**2. SpringCloud： 全家桶+ 第三方组建Netflix(闭源)**

- 通信： http restful
- 注册中心： eruka / consul
- 配置中心： config
- 断路： hystrix
- 网关：zuul
- 分布式追踪系统： sleuth + zipkin

**3. SpringCloud Alibaba**

以微服务为核心的分布式系统构建标准

比较主流，相关的功能也比较相似，当下比较有优势

# 2. Spring Cloud Alibaba 介绍

微服务开发的一站式解决方案

Spring Cloud Alibaba 

分布式配置： Nacos Config

服务注册/发现： Nacos Discovery

服务熔断： Sentinel

服务调用: Dubbo RPC 因为很多人不懂Dubbo，然后转而使用OpenFeign RestTemplate

服务路由： Dubbo + Servlet

分布式消息： SCS RocketMQ Binder

消息总线： RocketMQ Bus

负载均衡： Dubbo LoadBalance.  Ribbon(netflix)

分布式事务： Seata

Sidecar: Spring Cloud Alibaba Sidecar