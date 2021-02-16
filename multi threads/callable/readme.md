# 实现Callable接口并通过FutureTask包装

实现Callable接口通过FutureTask包装，可以获取到线程的处理结果，future.get()方法获取返回值，如果线程还没执行完，则会阻塞。

```java
public class DemoCallable implements Callable<String> {
  
  @Override
  public String call() throws Exception {
    //TODO Auto-generated method stub
    return null;
  }
  
  public static void main(String[] args) {
    DemoCallable c = new DemoCallable();\
    FutureTask<String> future = new FutureTask(c);
    Thread t = new Thread(future);
    t.start();
    ......
    String result = future.get(); //同步获取返回结果
    System.out.println(result);
  }
}
```
&emsp;&emsp;这个方法里，明明没有看到run()方法，没有看到Runnable，为什么说本质也是实现Runnable接口呢？

&emsp;&emsp;FutureTask实现了RunnableFuture，RunnableFuture则实现了Runnable和Future两个接口。因此构造Thread时，FutureTask还是被转型为Runnable使用。因此其本质还是实现Runnable接口。
