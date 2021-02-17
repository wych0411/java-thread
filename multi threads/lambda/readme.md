# Lambda表达式

匿名内部类可以通过lambda表达式的方式来简化书写：
```java
public class Demo {
  public static void main(String[] args) {
    new Thread(() -> System.out.println("running")).start();
    ......
  }
}
```
