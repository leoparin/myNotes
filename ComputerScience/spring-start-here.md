# 1 chapter 3
## 1.1 circular dependency
## 1.2 choose multiple beans
with @Qualifier annotation

# 2 Using abstraction
## 2.1 how java use interface decouple dependency
spring context spring configuration spring instanced(鹦鹉和人)
通过stereotype加入。
通过@bean注解在configuration类里面加入

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

## 4.1 why?
decouple some code
有的代码需要复制多次比如log之类的，可能造成数据深度耦合

## 4.2 what?
design pattern

## 4.3 how?
some concepts:
aspects: code you want to use
advice: when to initialise the aspect
pointcut: method contain usage of aspects
target obj:the bean use aspects
proxy: if a bean is an aspects target, spring do not give reference to the actual obj but give you a proxy
joinPoint: 
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
### 5.1.1 architecture

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

# 7 spring web scope
## 7.1 request scope

## 7.2 session scope
spring matain a session of http for each customer

## 7.3 applicaiton scope

# 8 spring REST
@RestController
@RestControllerAdvice

# 9 consume REST API
## 9.1 FeignClient
### 9.1.1 why？
your app need another spring project to provide a kind of service(endpoint)

### 9.1.2 what?
a method provide by spring framework

### 9.1.3 how?
```java
@RestController
public class PaymentsController {

  private final PaymentsProxy paymentsProxy;

  public PaymentsController(PaymentsProxy paymentsProxy) {
    this.paymentsProxy = paymentsProxy;
}//DI

  @PostMapping("/payment")
  public Payment createPayment(

      @RequestBody Payment payment

){  
String requestId = UUID.randomUUID().toString();  
return paymentsProxy.createPayment(requestId, payment);

} }

@FeignClient(name = "payments", 
			 url = "${name.service.url}")

public interface PaymentsProxy {

@PostMapping("/payment") 
Payment createPayment(
	@RequestHeader String requestId, 
	@RequestBody Payment payment);
}

```

# 10 spring test
1. Test what happens if the app can’t find the source account details.  
2. Test what happens if the app can’t find the destination account details. 
3. Test what happens if the source account doesn’t have enough money. 
4. Test what happens if the amounts update fails.  
5. Test what happens if all the steps work fine.

## 10.1 unit test
only test a piece of logic of your app
one of dashboard of  a car
test parts
```
1. Assumptions—We need to define any input and find any dependency of the logic we need to control to achieve the desired flow scenario. For this point, we’ll answer the following questions: what inputs should we provide, and how should dependencies behave for the tested logic to act in the specific way we want?

2.  Call/Execution—We need to call the logic we test to validate its behavior.
    
3.  Validations—We need to define all the validations that need to be done for the given piece of logic. We’ll answer this question: what should happen when this piece of logic is called in the given conditions?
```

### dependencies
![[Screen Shot 2022-10-29 at 11.03.24.png]]
what?
anything the method use but don't create by itself
ex: parameters, obects instances (DI)

why?
to execute the code in the controlled way

## how?
mock: a fake object
replace the true depencencies and provide the fake one
assume findById() works in a given way and
assert that the tested method’s execution does what’s expected for the given situation.

instead of create a real object just give the need results which needed
in the snippets , the mock return the sender and receiver created in the test
``` java

public class TransferServiceUnitTests {

  @Test
  @DisplayName("Test the amount is transferred " +

   "from one account to another if no exception occurs.")
  public void moneyTransferHappyFlow() {

    AccountRepository accountRepository =
      mock(AccountRepository.class);

    TransferService transferService =
      new TransferService(accountRepository);

Account sender = new Account(); 
sender.setId(1);  
sender.setAmount(new BigDecimal(1000));

Account destination = new Account();
destination.setId(2);  
destination.setAmount(new BigDecimal(1000));

given(accountRepository.findById(sender.getId())) .willReturn(Optional.of(sender));

given(accountRepository.findById(destination.getId()))
.willReturn(Optional.of(destination));

transferService.transferMoney( 
		sender.getId(),
		destination.getId(),
		new BigDecimal(100)
);

verify(accountRepository) 
.changeAmount(1, new BigDecimal(900)); 

verify(accountRepository) 
.changeAmount(2, new BigDecimal(1100));

} 
}
```

next step:
tell the test what should happen when the tested method executes.

another way
```java
@ExtendWith(MockitoExtension.class) //use the annotation
public class TransferServiceWithAnnotationsUnitTests {

@Mock       //mock object(dependecies)
private AccountRepository accountRepository;

@InjectMocks  //test object
private TransferService transferService;

```

verify: test a method be executed 
assertEquals : compare the expected result

## 10.2 Integration test
使用场景：
- 测试两个obj之间的交互逻辑
- 测试obj与framework之间的交互
- 测试数据库

与unit test区别：
不必mock所有的dependencies，可以直接创建object来进行测试
