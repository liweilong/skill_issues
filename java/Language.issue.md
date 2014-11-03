## Java 语言细节问题 ##

### 1. Java 重载函数的`参数`为 `继承关系` 时，调用最符合的方法 ###
```java
import java.util.*;
 
public class OverwriteTest{
    public void test(ArrayList<Integer> list){
        System.out.println("I am ArrayList");
    }
    public void test(List<Integer> list){
        System.out.println("I am List");
    }
    public static void main(String[] args){
        ArrayList<Integer> alist = new ArrayList<>();
		List<Integer> list = alist;
        new OverwriteTest().test(alist);	//输出：I am ArrayList
		new OverwriteTest().test(list);		//输出：I am List
    } 
}
```
以上代码能够正常运行，调用最合适的方法。

--
