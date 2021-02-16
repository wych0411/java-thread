# 多线程的实现形式从本质上来讲，只有一种方式，就是实现Runnable接口。

```java
public class DemoThreadTask implements Runnable{
  @Override
  public void run() {
    //TODO Auto-generated method stub
  }
  
  public static void main(String[] args) {
    DemoThreadTask task = new DemoThreadTask();
    Thread t = new Thread(task);
    t.start();
    ......
  }
}
```
实现Runnable接口，利用Runnable实例构造Thread，是较常用且最本质实现。Thread构造方法相当于对Runnable实例进行一次包装，在线程启动时，调用Thread的run()方法从而间接调用target.run():
```java
public class Thread implements Runnable {
  /* what will be run */
  private Runnable target;
  
  public void run() {
    if(target != null) {
      target.run();
      ......
    }
  }
}
```
