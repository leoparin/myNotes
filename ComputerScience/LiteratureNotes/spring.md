- [x] http request
- [ ] 现代企业级软件的架构（前后端复合逻辑） 

一些问题：
multipage网页应用是如何处理点击时间的交互的？
javascript吗？处理时是不是会冲洗拉去并加载界面？

tips:
browser only support post and get

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

**@Controller**
自动注册为bean（spring为何要把controller注册为bean，难道controller不是骨架吗）

## 3.1 SpringMVC:
@RequestMapping General-purpose request handling
@GetMapping Handles HTTP GET requests
@PostMapping Handles HTTP POST requests 
@PutMapping Handles HTTP PUT requests 
@DeleteMapping Handles HTTP DELETE requests 
@PatchMapping Handles HTTP PATCH requests

@PathVariable("id"):extract the id of the item from the path

### 3.1.1 Model
**@ModelAttribute**:
method level(on the head of the method)

``` java
@ModelAttribute 
public void addAttributes(Model model){
	model.addAttribute("msg", "Welcome to the Netherlands!"); 
}
```

called before @RequestMapping method,because the model object has to be created before any processing starts inside the controller methods.

as method argument:
从model里面取这个参数然后进行一些操作
```java
@RequestMapping(value = "/addEmployee", method = RequestMethod.POST)  
public String submit(@ModelAttribute("employee") Employee employee) { 
// Code that uses the employee object 
    return "employeeView"; 
}
```

**@SessionAttribute**:
spring will maintain it for the session,you should also annotate the method with modelattribute

## 3.2 Restful api
@RestfulController
@

# 4 核心概念
## 4.1 SpringMVC：
springWeb框架,核心是controller
implementation of mvc design pattern
Model-View-Controller


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
## 5.1 what ？
把创建对象的工作给别人做。
## 5.2 why？
when just one constructor spring applies autowireing through constructor parameter
降低数据耦合
## 5.3 how?
通过annotation注入
constructor DI
setter DI
Ioc container instantiate and scan annotations(@configuraion and @bean)
annotate the dependency needy element with @AutoWired spring will auto inject

## 5.4 element
**configuration**:java config class,with annotaion:@configuration on the class title and @bean on the instance head
**Ioc container**:
basic:bean factory
pro:Application Context

# 6 spring security


# 7 spring validation
防止用户输入错误格式的信息
传统解决办法:if then逐个检查
java bean api：Bean validation api
声明式检验：
数据类要声明校验规则

# 8 Thymeleaf
## 8.1 th:action
defines the path that the POST will happen on.
this will be mapped via @PostMapping method on controller

## 8.2 th:field 
degines the field inside the object that will be used to bind the value of the HTML input on
```html
<form th:action="@{/}" method="post" th:object="${item}"></form>
```

## 8.3 ${...}
The ${} operator tells it to use the value of a request attribute ("message", in this case).变量表达式
```html
<tr th:each="item:${userlist}">   iterate list
```
 
## 8.4 @{...} 
@{} operator is used to produce a context-relative path to the static artifacts that these tags are referencing.加载资源文件
Thymeleaf’s @{…} operator for a context-relative path,取图片之类的静态资源
**引入css**

```html
 <link rel="stylesheet" th:href="@{index.css}">
```
取普通字串，javabean对象，list

## 8.5 \*{...}
选择变量表达式，相当于把头交给上面去显示
```html
<div th:object="${user}">
    <p>Name: <span th:text="*{name}">赛</span>.</p>
    <p>Age: <span th:text="*{age}">18</span>.</p>
    <p>Detail: <span th:text="*{detail}">好好学习</span>.</p>
</div>

```
相当于：
```html
<div >
    <p>Name: <span th:text="${user.name}">赛</span>.</p>
    <p>Age: <span th:text="${user.age}">18</span>.</p>
    <p>Detail: <span th:text="${user.detail}">好好学习</span>.</p>
</div>
```

## 8.6 #{...}
消息表达式
从properties中间获得消息

## 8.7 conditions
### 8.7.1 ? :
provide a default text if a variable is null
```html
<td th:text="${teacher.additionalSkills} ?: 'UNKNOWN'" />
```

### 8.7.2 if unless
if teacher is f female will be rendered otherwise male is rendered
```html
<td> 
	<span th:if="${teacher.gender == 'F'}">Female</span> 
	<span th:unless="${teacher.gender == 'F'}">Male</span> 
</td>
```

### 8.7.3 switch
```html
<td th:switch="${#lists.size(teacher.courses)}"> 
	<span th:case="'0'">NO COURSES YET!</span> 
	<span th:case="'1'" th:text="${teacher.courses[0]}"></span> 
		<div th:case="*"> 
			<div th:each="course:${teacher.courses}"
				 th:text="${course}"/> 
		</div> 
</td>
```

## 8.8 fragment
what?
reusable snippets of html

why?
reuse some fragment

how?
`th:fragement` define a fragment
```html
<div th:fragment="separator">
	<div class="border-dashed border-2 border-red-300 mx-4">
	</div>
</div>
```
use a file as fragment `~{filename :: fragmentname}`
```html
<div>
<div th:insert="~{fragments :: separator}"></div>
</div>

or
<div th:insert="fragments :: separator"></div>
```
results:
```html
<div >//(The one that has the th:fragment="separator" attribute)
	<div class="border-dashed border-2 border-red-300 mx-4">
	</div>
```
防止标签太多可以合并th：fragment和class

### 8.8.1 th:classappend
apply css conditionally

# 9 JDBC
java database connection
![[Pasted image 20220827075007.png]]
cassandra(nosql)

![upgit_20220901_1661993427.png](https://raw.githubusercontent.com/leoparin/myObsidianPic/main/2022/09/upgit_20220901_1661993427.png)
## 9.1 configuration
yaml:
`---`:two file
key value pair
datastructure:list(缩进)

# 10 spring Integration
what?
整合模块实现功能

why？
spring无法单独完成工作

how？
1. maven导入依赖
2. 

# 11 Spring REST api
what?
一种spring或者现代网页设计模式，是singlepage不同于以前的multipage

why?
有更快的速度跟交互

how?
1. Resource identification 
根据需要设计nouns 

2. Resource representation 
设计输出格式json

3. Endpoint identification 
some conventions:
- use a base URI for restful service
- use plural nouns to name resource `http://localhost:8080/polls`
- use hierarchy to represent resources `http://localhost:8080/polls/{pollId}`

4. Verb/action identification
某个url能执行哪种操作比如polls只能PUT跟 GET而不能执行其他http request

为何不能吧所有nouns都变成resource？
