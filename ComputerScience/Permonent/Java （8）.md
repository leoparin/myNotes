TODO：
- [ ] scanner（@2022-08-17）
- [ ] collection（@2022-08-17）
# 1 terminology
jdbc:java database connect
anonymous: of unknown name

# 2 Java基础
string is immutable：for security
override：子类重写父类函数（参数一样）需要加个@override的annotation

## 2.1 method chaining
each method in chain should return an object

## 2.2 interface:
extends parents class
implement interface (multi)
运行时动态设置对象（开始用接口来签名，然后后面在制定对象）

### 2.2.1 functional interface
#### 2.2.1.1 what?
only have one abstract method
#### 2.2.1.2 why?
used as signature of lambda expression(to represent)
#### 2.2.1.3 how?
```java

public interface Predicate { 
		boolean test (T t);        -->descriptor of lambda
}```
you should use the signature of the interface to sign for lambda

预设的：
predicate: `<T> ->boolean`
discriptor:test

### 2.2.2 default interface

## 2.3 Exceptions



## 2.4 static
### 2.4.1 what?
key word

### 2.4.2 why?
some var(global var) and method you do not want to bend to objects
and some methods should be established before any objects are created
create a member that can be used by itself, without reference to a specific instance.

### 2.4.3 how?
Methods declared as static have several restrictions:

• They can only directly call other static methods of their class.  
• They can only directly access static variables of their class.  
• They cannot refer to this or super in any way. (The keyword super relates

to inheritance and is described in the next chapter.)

classname.method( )
classname.obj

# 3 lib
## 3.1 junit
use for test,provide a runner to run your code and output exceptions.

## 3.2 file

## 3.3 thread

## 3.4 collections




# 4 Java8概念
## 4.1 lambda

### 4.1.1 what?
semantic sugar
### 4.1.2 why?
to eliminate the boiler plate
implementation of behavior parameterization
### 4.1.3 how?
(parameter) -> value;
(parameter) -> {expression;}
where you can use lambda?
you need functional interface,lambda is inline implementation of functional interface

```java
List<Apple> greenApples = filterApplesByPredicate(inventory, 
							(Apple a)->a.color==Color.GREEN);

private static List<Apple> filterApplesByPredicate(
			List<Apple> inventory,ApplePredicate p
) {  
	List<Apple> result = new ArrayList<>();  
	for(Apple a: inventory) {  
		if (p.test(a)==true)  //test的参数是lambda的参数
			result.add(a);  
	}
	return result;  
}
```
test() parameter is the parameter of lambda expression(front of arrow)

## 4.2 Stream

the difference between stream and collections:

### 4.2.1 what? 
是一系列的数据，程序从流中逐一读取数据
java Stream`.`in/out: 一系列功能的组合，并行处理数据（unix）

### 4.2.2 why？
以流的方式处理数据（optical），免去写thread的麻烦
     写java思路变成了把这样的流变成那样的流,无需告诉程序内部该如何实现，只需要说你想要什么（就像写数据库查询语句时的那种思路）
 
### 4.2.3 how?




## 4.3 函数是一等公民
函数（方法）：可以被任意传递（和对象一样）
**行为参数化**：把函数像参数一样传递
（函数之间无互动）
引用：： 将方法作为值传递


## 4.4 optional
optional<T> :avoid nullpointer

if a people don't have a car,set car as 
optional<car>
