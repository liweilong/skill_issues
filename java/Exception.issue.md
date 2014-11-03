## Java 异常处理相关问题 ##

### 1. return finally 执行顺序问题
```java
int func(){
	int a = 1;
	try{
		return a;
	}catch(Exception e){
		a = 2;
		return a;
	}finally{
		a = 3;
	}
}
```
运行 `func()` 之后返回 `1` ，原因：
```
java的return执行过程分为三个步骤
1.  把要返回的值copy到一个‘槽’中（如果是对象则copy引用），等待函数返回
2.  执行 finally 语句块的内容，这时修改变量的值不会影响槽中的值
3.  返回函数
```
所以说 **finally快在return中间执行**

--
### 2. Java 异常设计问题 ###

异常是面向对象语言非常重要的一个特性，良好的异常设计对程序的可扩展性、可维护性、健壮性都起到至关重要。
JAVA根据用处的不同，定义了两类异常  
> * **Checked Exception**: Exception的子类,方法签名上需要显示的声明throws，编译器迫使调用者处理这类异常或者声明throws继续往上抛。
* **Unchecked Exception**: RuntimeException的子类，方法签名不需要声明throws，编译器也不会强制调用者处理该类异常。

现实中，异常主要分为以下两类：
>* **系统异常**：软件的缺陷，客户端对此类异常是无能为力的，通常都是Unchecked Exception。
* **业务异常**：用户未按正常流程操作导致的异常，都是Checked Exception 


异常的设计应遵循以下原则：
> 1. 如果方法遭遇了一个无法处理的意外情况，那么抛出一个异常。
2. 避免使用异常来指出可以视为方法的常用功能的情况。
3. 如果发现客户违反了契约（例如，传入非法输入参数），那么抛出非检查型异常。
4. 如果方法无法履型契约，那么抛出检查型异常，也可以抛出非检查型异常。
5. 如果你认为客户程序员需要有意识地采取措施，那么抛出检查型异常。
6. 异常类应该给客户提供丰富的信息，异常类跟其它类一样，允许定义自己的属性和方法。
7. 异常类名和方法遵循JAVA类名规范和方法名规范
8. 跟JAVA其它类一样，不要定义多余的方法和变量。(不会使用的变量，就不要定义,spring的BadSqlGrammarException.getSql() 就是多余的)
9. 不要使用异常来控制流程 

相关链接：  
[Java异常设计原则](http://tech.e800.com.cn/articles/2009/79/1247105040929_1.html)  
[异常设计](http://www.cnblogs.com/JavaVillage/articles/384483.html)  
[Java异常处理最佳实践](http://tech.e800.com.cn/articles/2009/79/1247105040929_1.html)
