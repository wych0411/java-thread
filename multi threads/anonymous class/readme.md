# 匿名内部类

&emsp;&emsp;匿名内部类的优点在于使用方便，不用额外定义类，缺点就是代码可读性差。

&emsp;&emsp;‘implements Runnable’、‘extends Thread’、‘implements Callable’三种线程的实现方式都可以使用匿名内部类来隐式实例化：
```java
public class Demo {
  
  public static void main(String[] args) {
    //方式一：Thread匿名内部类
    new Thread(){
      @Override
      public void run() {
        //TODO Auto-generated method stub
      }
    }.start();
    ......
    //方式二：Runnable匿名内部类
    new Thread(new Runnable(){
      @Override
      public void run() {
        //TODO Auto-generated method stub
      }
    }).start();
    ......
  }
}
```
