# 线程池

线程池执行线程的时候由ExecutorService去执行，最终还是利用Thread创建线程。
```java
public class DemoThreadTask implements Runnable {
  @Override
  public void run() {
    //TODO Auto-generated method stub
    System.out.println("running");
  }
  
  public static void main(String[] args) {
    DemoThreadTask task = new DemoThreadTask();
    ExecuteService ex = Executors.newCachedThreadPool();
    ex.execute(task);
    ......
  }
}
```
线程池的优势在于线程的复用，从而提高效率。
