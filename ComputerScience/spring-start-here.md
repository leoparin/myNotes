# 1 chapter 3
## 1.1 circular dependency
## 1.2 choose multiple beans
with @Qualifier annotation

# 2 Using abstraction
## 2.1 how java use interface decouple dependency

# 3 Bean scope and lifecycle
## 3.1 singleton bean scope
what?
default spring create and manage beans approach
why?

how?
per name in one app(different singleton design pattern,per app per instance of one class)
spring can hava multiple instance but name is unique.

## 3.2 prototype bean scope
每次调用都创建一个新的bean，适用于冲突的场景（两个thread同时对bean进行修改）

# 4 AOP
## 4.1 what?
design pattern

## 4.2 why?
decouple some code
有的代码需要复制多次比如log之类的，可能造成数据深度耦合

## 4.3 how?

some concepts:
aspects:code you want to use
advice:when to initialise the aspect
pointcut:method contain usage of aspects
target obj:the bean use aspects
proxy: if a bean is an aspects target, spring do not give reference to the actual obj but give you a proxy
weave: 

逻辑：
调用的时候不直接调用target obj而是调用了proxy，在这个过程中插入了代码进来（aspect里面给的内容）
而aop还可以轻松获取他的参数跟输出内容
```java
String methodName = joinPoint.getSignature().getName();  //获取参数

Object[] arguments = joinPoint.getArgs();

```

# 5 spring boot and spring mvc
## 5.1 web app architecture
分类：
前后端分离：后端rest 前端用前端app（react，vue，angular）
前后端不分离：（后端传送html片段，browser只负责显示）

如何交互：http ![[html#^38e58a]]
## 5.2 how spring understand http?
### 5.2.1 tomcat 
#### 5.2.1.1 what?
servlet container
#### 5.2.1.2 why?
spring cannot understand http 
#### 5.2.1.3 how?
translate http and response java obj
接request回复java对象
本身也是个java instance

## 5.3 how spring web app work
![[Screen Shot 2022-10-02 at 14.39.44.png]]

# 6 implement a spring mvc app
## 6.1 spring send data to client

## 6.2 spring get data from client
small amount:use request parameters(key value pair)
