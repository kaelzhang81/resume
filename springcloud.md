# Spring Cloud从0到1
Spring Cloud是一个基于Spring Boot的微服务开发工具，它为微服务架构中涉及配置管理、服务治理、断路器、智能路由、微代理、控制总线、全局锁、决策竞选、分布式会话和集群状态管理等操作提供了一种简单的开发方式。


![](/microservices/spring-cloud/spring-io-tree.png
)



## Spring Boot
SpringBoot让创建独立的、生产级的、基于Spring的应用更加快捷简易。 大部分Spring Boot Application只要一些极简的配置，即可“一键运行”。

NOTE:

如果您编写过基于 Spring 的应用程序，就会知道只是完成 “Hello, World” 就需要大量配置工作。这不是一件坏事：Spring 是一个优雅的框架集合，需要小心协调配置才能正确工作。但这种优雅的代价是配置变得很复杂（别跟我提 XML）。


### Spring Boot的特性

* 创建独立的Spring applications
* 能够使用内嵌的Tomcat, Jetty or Undertow，不需要部署war
* 提供定制化的starter poms来简化maven配置（gradle相同）
* 追求极致的自动配置Spring
* 提供一些生产环境的特性，比如特征指标，健康检查和外部配置。
* 零代码生成和零XML配置

Note:

Spring由于其繁琐的配置，一度被人认为“配置地狱”，各种XML、Annotation配置，让人眼花缭乱，而且如果出错了也很难找出原因。而Spring Boot更多的是采用Java Config的方式，对Spring进行配置。


## Spring Cloud全家桶
![](/microservices/spring-cloud/spring-cloud-components.png)

NOTE:

在Spring Cloud中，整合了很多功能组件，包括Config、Messaging、Netflix OSS以及对Heroku、Amazon Web Service、Cloud Foundry等云平台的接口支持。


### ![](/microservices/spring-cloud/netflix.png)

Spring Cloud的子项目之一，主要内容是对Netflix公司一系列开源产品的包装，它为Spring Boot应用提供了自配置的Netflix OSS整合。通过一些简单的注解，开发者就可以快速的在应用中配置一下常用模块并构建庞大的分布式系统。
它主要提供的模块包括：服务发现（Eureka），断路器（Hystrix），智能路由（Zuul），客户端负载均衡（Ribbon）等。


#### ![](/microservices/spring-cloud/netflix-eureka.jpg)

云端服务发现，一个基于 REST 的服务，用于定位服务，以实现云端中间层服务发现和故障转移。

Note:

Service discovery client & server Maintains registry of clients with metadata    Host/port    Health indicator URLClient heartbeats (30 sec default - changing not encouraged)    Lease renewed with serverService available when client & server(s) metadata cache all in sync    Can take up to 3 heart beats

Eureka特点
* REST based service registry
* Supports replication
* Caches on the client
* Resilient
* Fast
* ...but not consistent
* Foundation for other services


#### ![](/microservices/spring-cloud/netflix-zuul.png)

Zuul是在云平台上提供动态路由，监控，弹性，安全等边缘服务的框架。Zuul相当于是设备和Netflix流应用的Web网站后端所有请求的前门。

Note:

> One URL to the outside> Internal: Many Microservices> In particular: REST> Power through filters

JVM based router & load balancerProvides single point of entry to services
    Including single point of authentication
By default creates route for every service in Eureka    Refer to http://localhost/credit-service routes to http://credit- serviceFilters provide limited entry points to system


#### ![](/microservices/spring-cloud/netflix-ribbon.png)
提供云端负载均衡，有多种负载均衡策略可供选择，可配合服务发现和断路器使用。

Note:

Client side loan balancerCan delegate to Eureka for server listsOr list servers    stores.ribbon.listOfServers=... + ribbon.eureka.enabled=false


#### ![](/microservices/spring-cloud/netflix-turbine.png)

Turbine是聚合服务器发送事件流数据的一个工具，用来监控集群下hystrix的metrics情况


#### ![](/microservices/spring-cloud/netflix-feign.png)

声明式服务调用客户端。只需要通过创建接口并用注解来配置它既可完成对Web服务接口的绑定。具备可插拔的注解支持，扩展了对Spring MVC注解的支持，同时还整合了Ribbon和Eureka来提供均衡负载的HTTP客户端实现。


#### ![](/microservices/spring-cloud/netflix-hystrix.png)

hystrix旨在通过控制那些访问远程系统、服务和第三方库的节点，从而对延迟和故障提供更强大的容错能力。Hystrix具备拥有回退机制和断路器功能的线程和信号隔离，请求缓存和打包、监控和配置等功能。

Note:

Circuit breakerThreshold breached (20 failures in 5 seconds) => breaker kicks inDefault timeout threshold 1 secondPer dependency thread poolsAsync command support (not Spring @Async)Sync or async fallback

> Enable resilient applications> Do call in other thread pool> Won’t block request handler> Can implement timeout


### ![](/microservices/spring-cloud/spring-cloud-config.png)

配置管理工具包，让你可以把配置放到远程服务器，集中化管理集群配置，目前支持本地存储、Git以及Subversion。

Note:

> Spring Cloud Config> Central configuration> Dynamic updates> Can use git backend> I prefer immutable server> & DevOps tools (Docker, Chef...)

CONFIG SERVER

Git hosted configuration repositorySVN & filesystem also supported (see implementations of org.springframework.cloud.config.server.EnvironmentR epository)Multiple security options w/Spring Security (HTTP Basic -> OAuth bearer tokens)Push updates via Spring Cloud Bus


### ![](/microservices/spring-cloud/spring-cloud-bus.png)

事件、消息总线，用于在集群（例如，配置变化事件）中传播状态变化，可与Spring Cloud Config联合实现热部署。


### ![](/microservices/spring-cloud/spring-cloud-sleuth.png)

日志收集工具包，封装了Dapper和log-based追踪以及Zipkin和HTrace操作，为SpringCloud应用实现了一种分布式追踪解决方案。


### 关键技术
![](/microservices/spring-cloud/keytech.png)


### 架构示例
![](/microservices/spring-cloud/msa.png)


## 参考资料
1. 《Spring Cloud微服务实战》
2. https://springcloud.cc/
3. http://blog.didispace.com/Spring-Cloud%E5%9F%BA%E7%A1%80%E6%95%99%E7%A8%8B/
4. https://dzone.com/articles/deploying-microservices-spring-cloud-vs-kubernetes
5. http://wldandan.github.io/blog/2016/11/07/microservices-in-action-spring-cloud-101/

