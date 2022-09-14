- [x] http request
- [ ] 现代企业级软件的架构（前后端复合逻辑） 

# 1 roadmap:
![upgit_20220824_1661302540.png](https://raw.githubusercontent.com/leoparin/myObsidianPic/main/2022/08/upgit_20220824_1661302540.png)

1. Chapter 2 discusses building the web layer of an application using Spring MVC. In this chapter, you’ll build controllers that handle web requests and views that render information in the web browser. 
2. Chapter 3 delves into the backend of a Spring application, where data is persisted to a relational database.
3. Chapter 4 continues the subject of data persistence by looking at how to persist data to nonrelational databases, specifically, Cassandra and MongoDB. 
4. In chapter 5, you’ll use Spring Security to authenticate users and prevent unauthorized access to an application. 
5. Chapter 6 reveals how to configure a Spring application using Spring Boot configuration properties. You’ll also learn how to selectively apply configuration using profiles.  

**Part 2 covers topics that help integrate your Spring application with other applications:**
7. Chapter 7 expands on the discussion of Spring MVC started in chapter 2, by looking at how to write and consume REST APIs in Spring. 
8. Chapter 8 shows how to secure the APIs created in chapter 7, with Spring Security and OAuth 2.
9. Chapter 9 looks at using asynchronous communication to enable a Spring application to both send and receive messages using the Java Message Service, RabbitMQ, or Kafka. 
10. Chapter 10 discusses declarative application integration using the Spring Integration project. 

**Part 3 explores the exciting new support for reactive programming in Spring:** 
12. Chapter 11 introduces Project Reactor, the reactive programming library that underpins Spring 5’s reactive features. 
13. Chapter 12 revisits REST API development, introducing Spring WebFlux, a new web framework that borrows much from Spring MVC while offering a new reactive model for web development.
14. Chapter 13 takes a look at writing reactive data persistence with Spring Data to read and write data to Cassandra and Mongo databases. 
15. Chapter 14 introduces RSocket, a new communication protocol that offers a reactive alternative to HTTP for creating APIs.
 **In part 4, you’ll ready an application for production and see how to deploy it:** 
17. Chapter 15 introduces the Spring Boot Actuator, an extension to Spring Boot that exposes the internals of a running Spring application as REST endpoints. 
18. In chapter 16, you’ll see how to use Spring Boot Admin to put a user-friendly browser-based administrative application on top of the Actuator. 
19. Chapter 17 discusses how to expose and consume Spring beans as JMX MBeans

# 2 lib:
slf4j:logger
lombok:automaticly generate useful methods of data class

# 3 annotations
**@SessionAttributes**:
maintain the order to scan the users' input.TacoOrder object that is put into the model a little later in the class should be maintained in session.

**@ModelAttribute**.
These methods are much simpler and create only a new TacoOrder and Taco object to place into the model.

**@AutoWired**
automaticially implement DI, put on the top of constructor and getter setter

## 3.1 SpringMVC:
@RequestMapping General-purpose request handling
@GetMapping Handles HTTP GET requests
@PostMapping Handles HTTP POST requests 
@PutMapping Handles HTTP PUT requests 
@DeleteMapping Handles HTTP DELETE requests 
@PatchMapping Handles HTTP PATCH requests

## 3.2 Restful api
@RestfulController
@

# 4 核心概念
## 4.1 springmvc：
springWeb框架,核心是controller
implementation of mvc design pattern




**注释**（annotation)：
补充说明，提供信息，不参与运行
来自于java scanner
spring自动扫描，通过xml文件来进行自动装配

1.  Spring Core Annotations
2.  Spring Web Annotations
3.  Spring Boot Annotations
4.  Spring Scheduling Annotations
5.  Spring Data Annotations
6.  Spring Bean Annotations

REST API:
一种api架构，

Controller:
处理http请求

servlet:excecute in server
![upgit_20220905_1662351749.png](https://raw.githubusercontent.com/leoparin/myObsidianPic/main/2022/09/upgit_20220905_1662351749.png)


# 5 Dependency Injection：
what is dependency?
a类需要使用b类的function，in Java首先需要创建b对象。这就是a依赖于b
what ？
把创建对象的工作给别人做。
why？
when just one constructor spring applies autowireing through constructor parameter
降低数据耦合
how?
通过annotation注入
constructor DI
setter DI
Ioc container instantiate and scan annotations(@configuraion and @bean)

## 5.1 element
**configuration**:java config class,with annotaion:@configuration on the class title and @bean on the instance head
**Ioc container**:
basic:bean factory
pro:Application Context


# 6 spring校验
防止用户输入错误格式的信息
传统解决办法:if then逐个检查
java bean api：Bean validation api
声明式检验：
数据类要声明校验规则

# 7 Thymeleaf
1. The ${} operator tells it to use the value of a request attribute ("message", in this case).
2. @{} operator is used to produce a context-relative path to the static artifacts that these tags are referencing.
3. Thymeleaf’s @{…} operator for a context-relative path

# 8 JDBC
java database connection
![[Pasted image 20220827075007.png]]
cassandra(nosql)

![upgit_20220901_1661993427.png](https://raw.githubusercontent.com/leoparin/myObsidianPic/main/2022/09/upgit_20220901_1661993427.png)
## 8.1 configuration
yaml:
`---`:two file
key value pair
datastructure:list(缩进)

# 9 spring Integration
what?
整合模块实现功能

why？
spring无法单独完成工作

how？
1. maven导入依赖
2. 
 