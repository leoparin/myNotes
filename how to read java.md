# chapter 1 know your app
debugger: a tool allow to pause the app at certain line
profiler: tool use to analyze details of an app's execution
## typically scenario for using investigation
-   Understand why a particular piece of code or software capability provides a different result than the expected one.
-   Test a new capability you implemented in an app.
-   Learn how certain dependencies work (libraries or frameworks).
-   Identify causes for performance issues such as app slowness.
-   Finding out root causes for cases in which an app suddenly stops.

### Demystifying the unexpected output
stub : a fake app you can control to identify issue

### Learning certain technologies
reading document is essential

### clarifying slowness


### understanding app crashes
1. The app completely stops  
2. The app still runs but doesn't respond anymore to requests

# charpter 2 how to use debugger
## reading code
```java
public class Decoder {

  public Integer decode(List<String> input) {
    int total = 0;
    for (String s : input) {

      var digits = new StringDigitExtractor(s).extractDigits();
//you need to read the constructor of StringDigitExtractor
      total += digits.stream().collect(Collectors.summingInt(i -> i));
    }

    return total;
  }

}
```
### why debugger is useful?
it can avoid you go too deep and forget where you start, you just make a breakpoint at the  line of code which you want to learn the behavior and see the return data.

## how debugger work
-   Providing you with a means to pause the execution at a particular step and execute each instruction manually at your own pace.
-   Showing you where you are and where you came from in the code reading path. This way, the debugger works as a map releasing you from having to remember all the details.
-   Showing you the values that variables hold, making the investigation more visual and easier to process.

steps to use debug
1. use other techniques to find the piece of code you want to investigate
2. make breakpoints and observe the change of data
![[Screenshot 2022-10-31 at 11.32.57.png]]
### what is stack trace?
![[Screenshot 2022-10-31 at 11.35.11.png]]
## navigate with debugger
1.  Step over – you continue the execution with the next line of code in the same method. 直接拿到数据然后进入下一行，直接知道这个方法做了什么事情而忽略细节
2.  Step into – you continue the execution inside one of the methods called on the current line.  enter the method you called
3.  Step out – you return the execution to the method that called the one you investigate now.  从method里面出来（cave）

![[Screenshot 2022-10-31 at 11.54.45.png]]
## when debugger is not enough
-   Investigating output problems when you don’t know which part of the code creates the output
-   Investigating performance problems
-   Investigating app crashes
-   Investigating multithreaded implementations

# chapter 3 advance debugger
## conditional debugger
### what?
a debug technique

### why?
sometimes you just want to invest a piece of code' s behaviour in 
specific condition

### how?
![[Screenshot 2022-11-04 at 09.55.10.png]]

## using breaking point don't pause the execution
aim: using breaking points to log messages can be used later

![[Screenshot 2022-11-04 at 10.24.45.png]]

## dynamic altering the investigation scenario
