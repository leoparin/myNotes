# 1 OOP
## 1.1 what?

way of programming,different methods to process oriented programming

## 1.2 why?
比较符合人的直觉，可以很好的进行数据管理，能很好地进行软件扩展维护升级而不用整个改。（你需要车子，车子只是你的对象，你无需考虑内部如何运转，只要按照操作手册来进行操作就可以了）
用pop很容易看不懂别人的代码在干嘛，而且修改也很困难，耦合过于紧密。

## 1.3 analogy
u need what just go to the store and buy it instead of making it yourself, u are not farmer.

## 1.4 encapsulation
把一切都封装到对象里面，之保留对外接口，像是音响的开关。

## 1.5 inheritance
金毛是狗，狗会叫，所以金毛会叫

## 1.6 polymorphism
狗闻到不同的的气味有不同的处理，但狗是一样的，输入气味不同，避免了复制一遍代码的尴尬
```
Consider a stack (which is a last-in, first-out list). You might have a program that requires three types of stacks. One stack is used for integer values, one for floating-point values, and one for characters. The algorithm that implements each stack is the same, even though the data being stored differs. In a non–object-oriented language, you would be required to create three different sets of stack routines, with each set using different names. However, because of polymorphism, in Java you can specify a general set of stack routines that all share the same names.
```
# 2 builder pattern
## 2.1 

# factory pattern 
```java
class Dog implements Animal
{

       public void speak()
       {

System.out.println("Dog says: Bow-Wow."); }

       public void preferredAction()
       {

System.out.println("Dogs prefer barking...\n"); }

}
class Tiger implements Animal
{

       public void speak()
       {

System.out.println("Tiger says: Halum."); }

       public void preferredAction()
       {

System.out.println("Tigers prefer hunting...\n"); }

}  
abstract class AnimalFactory  
{  
/*Remember that the GoF definition says "....Factory method lets a class defer instantiation to subclasses."  
In our case, the following method will create a Tiger or Dog but at this point it does not know whether it will get a Dog or a Tiger. This decision will be taken by the subclasses i.e. DogFactory or TigerFactory. So,in this implementation, the following method is playing the role of a factory (of creation)*/

       public abstract Animal createAnimal();
}

class DogFactory extends AnimalFactory
{

       public Animal createAnimal()
       {

              //Creating a Dog

              return new Dog();
       }

}
class TigerFactory extends AnimalFactory
{

       public Animal createAnimal()
       {

              //Creating a Tiger

              return new Tiger();
       }

}

class FactoryMethodPatternExample {
       public static void main(String[] args) {
        System.out.println("***Factory Pattern Demo***\n"); 
       // Creating a Tiger Factory  
		AnimalFactory tigerFactory =new TigerFactory();  
		// Creating a tiger using the Factory Method
		
		Animal aTiger = tigerFactory.createAnimal();
		aTiger.speak();
		aTiger.preferredAction();
		
		// Creating a DogFactory
		AnimalFactory dogFactory = new DogFactory();
		// Creating a dog using the Factory Method
		Animal aDog = dogFactory.createAnimal();
		aDog.speak();
		aDog.preferredAction();
} }
```


## 2.1 factory pattern
what?
design pattern,related to OOP
why?
数据解耦合，简化对象创建
how？
建立工厂类，这个类实现一系列的子类（各种形状），调用get匹配想要的类就可以直接得到对象了，无需调用对应的类。