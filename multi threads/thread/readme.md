# 显式继承Thread类

```java
public class DemoThread extends Thread {
  
  @Override
  //重写run方法
  public void run() {
    //TODO Auto-generated method stub
  }
  
  public static void main(String[] args) {
    Thread t = new DemoThread();
    t.start();
    ......
  }
}
```
从类图中我们可以看到，Thread类本身就继承自Runnable，所以继承Thread的本质也是实现Runnable接口定义的run()方法。
